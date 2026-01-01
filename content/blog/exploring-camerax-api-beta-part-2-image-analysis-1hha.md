---
title: "Exploring CameraX API Beta (Part -2): Image Analysis"
date: 2020-06-13
summary: "Update since the previous post:                                       Exploring CameraX Beta (Part -..."
draft: false
tags: ["android", "camerax", "kotlin"]
canonicalURL: "https://dev.to/funkyidol/exploring-camerax-api-beta-part-2-image-analysis-1hha"
---
*Update since the previous post: [Part 1](/blog/exploring-camerax-beta-release-part-1-19hh/)*
Google has release a new beta update (1.0.0-beta4) to the CameraX api and one breaking change is that when setting the `createSurfaceProvider()` on the `viewFinder` we dont need to add the `cameraInfo` parameter. A very small and simple change that makes things a little more simpler.

```kotlin
preview?.setSurfaceProvider(viewFinder.createSurfaceProvider(camera?.cameraInfo))
// changes to 
preview?.setSurfaceProvider(viewFinder.createSurfaceProvider())
```

---

In our previous post we looked at how to setup CameraX api and create a simple camera preview screen within a fragment. In this post we will talk about how to setup an 'Analysis' use-case which will use the MLKit on-device text detection to read text. There are many samples available online which show this exact same thing but what I wanted to share is how to start and stop the analysis on-demand. Every sample that I have seen till now starts the analysis on camera start and does not show how you can stop it when required.

## Text Detection Implementation Steps

* Include the following dependency in the module level `build.gradle`

  ```groovy
  implementation 'com.google.android.gms:play-services-mlkit-text-recognition:16.0.0'
  ```

* Add the following meta data to the `AndroidManifest.xml`

  ```xml
  <application ...>
    ...
    <meta-data
        android:name="com.google.mlkit.vision.DEPENDENCIES"
        android:value="ocr" />
    <!-- To use multiple models: android:value="ocr,model2,model3" -->
  </application>
  ```

* Create a new `TextAnalyzer` class and extend `ImageAnalysis.Analyzer`

  ```kotlin
  class TextAnalyzer(private val result: (String) -> Unit) : ImageAnalysis.Analyzer {
    ...
  }
  ```

  We will also take a callback function parameter to send result back to the calling class

* Override the `analyze` method 

  ```kotlin
  override fun analyze(imageProxy: ImageProxy) {
  }
  ```

  * Get the `TextRecognizer` instance

    ```kotlin
    val recognizer = TextRecognition.getClient()
    ```

  * Get the image from the `imageProxy ` param

    ```kotlin
    val mediaImage = imageProxy.image
    ```

  * If the `mediaImage` is not null then execute the following code. Here we create the `InputImage` from the `mediaImage` and the `rotationDegrees` value from the `imageProxy`. We then send this `inputImage` to the `recognizer` for processing. In case of both success and failure we ensure that the `imageProxy.close()` is always called so CameraX api knows that the current frame processing is complete and it can move onto capturing the next frame.

  ```kotlin
    val image = InputImage.fromMediaImage(mediaImage, imageProxy.imageInfo.rotationDegrees)
    recognizer.process(image)
    	.addOnSuccessListener { text ->
        	Log.d(TAG, "Text ${text.text}")
            result.invoke(text.text)
            imageProxy.close()
        }
        .addOnFailureListener { e ->
        	Log.e(TAG, "Mlkit processing Failed", e)
            imageProxy.close()
        }
  ```

* In our camera fragment (`MainFragment`) we now create the analysis use case and attach to the  camera object. Please note that for now we are just attaching the use case and not the analyzer itself which we just created.

  ```kotlin
  imageAnalysis = ImageAnalysis.Builder()                              
      .setTargetResolution(Size(1280, 720))                            
      .setBackpressureStrategy(ImageAnalysis.STRATEGY_KEEP_ONLY_LATEST)
      .build()                                                         
  ```
  
  Camera binding now changes to 
  
  ```kotlin
  camera =
      cameraProvider.bindToLifecycle(
          this as LifecycleOwner,
          cameraSelector,
          preview,
          imageAnalysis
      )
  ```

* We now add a button to the UI to enable and disable the text analysis on demand

  ```kotlin
  btn_analyze.setOnClickListener { 
      if (!featureOn) {
          featureOn = true
          imageAnalysis.setAnalyzer(cameraExecutor, TextAnalyzer() { 
              tv_result.text = it
          })
      } else {
          featureOn = false
          imageAnalysis.clearAnalyzer()
      }
  }
  ```

  So now, when we have to turn on the text analysis we create a new instance of the `TextAnalyzer` class and set it to the `imageAnalysis` use-case. And on it callback result we show the text on the screen to show the detected text.
  When we turn off the the text analysis, we just clear the `imageAnalysis` use-case from all the attached analyzers.

And that's it. Just by attaching and clearing the use-cases we can create on-demand analysis features using the CameraX api. You can find the complete source code for this post on the commit [here](https://github.com/funkyidol/CameraXSample/commit/4397d1249ea49b6f2e13c10cc5be7c8adedb38f8)  
[GitHub: CameraXSample](https://github.com/funkyidol/CameraXSample)
