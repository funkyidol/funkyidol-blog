---
title: "Exploring CameraX Beta (Part - 1): Basic Setup"
date: 2020-05-18
summary: "CameraX is probably one of the most requested API's that most developers dealing with the Android cam..."
draft: false
tags: ["android", "kotlin", "camerax"]
canonicalURL: "https://dev.to/funkyidol/exploring-camerax-beta-release-part-1-19hh"
---
CameraX is probably one of the most requested API's that most developers dealing with the Android camera API setup are looking forward to. What the team developing the CameraX API is doing is no easy feat and this also shows in the development path of the API with pretty massive changes happening throughout the Alpha development stage. ([Release notes & history](https://developer.android.com/jetpack/androidx/releases/camera))

This blog post is first of the series on CameraX where I try and explore the API (1.0.0-beta03 at the time of writing this article) in a more in-depth manner at an implementation level with a real-use setup (read 'fragments') since most of the CameraX explorations I have found have been prior to the [1.0.0-alpha7](https://developer.android.com/jetpack/androidx/releases/camera#camera-core-1.0.0-alpha07) release, which by now have been changed significantly.

## Implementation Steps ##

The following are the implementation steps I followed to get a simple camera preview using CameraX

* Include the following gradle dependencies in your project level `build.gradle`
```groovy
   dependencies {
       // CameraX core library
       def camerax_version = '1.0.0-beta03'
       implementation "androidx.camera:camera-core:$camerax_version"
   
       // CameraX Camera2 extensions
       implementation "androidx.camera:camera-camera2:$camerax_version"
   
       // CameraX Lifecycle library
       implementation "androidx.camera:camera-lifecycle:$camerax_version"
   
       // CameraX View class
       implementation 'androidx.camera:camera-view:1.0.0-alpha10'
       implementation 'androidx.fragment:fragment:1.2.4'
   }
```
* Add the `PreviewView` component in the fragment layout XML

   ```xml
   <androidx.camera.view.PreviewView
       android:id="@+id/view_finder"
       android:layout_width="match_parent"
       android:layout_height="match_parent" />
   ```

* Add the Camera permissions to the `AndroidManifest.xml` and implement the permissions provider in your fragment

   ```xml
   <uses-permission android:name="android.permission.CAMERA" />
   ```

* Add the following method to add the camera preview use-case to the fragment

   ```kotlin
   private fun bindCameraUseCases() {
   
           // Get screen metrics used to setup camera for full screen resolution
           val metrics = DisplayMetrics().also { viewFinder.display.getRealMetrics(it) }
           Log.d(TAG, "Screen metrics: ${metrics.widthPixels} x ${metrics.heightPixels}")
   
           val screenAspectRatio = aspectRatio(metrics.widthPixels, metrics.heightPixels)
           Log.d(TAG, "Preview aspect ratio: $screenAspectRatio")
   
           val rotation = viewFinder.display.rotation
   
           // Bind the CameraProvider to the LifeCycleOwner
           val cameraSelector = CameraSelector.Builder().requireLensFacing(lensFacing).build()
           val cameraProviderFuture = ProcessCameraProvider.getInstance(requireContext())
           cameraProviderFuture.addListener(Runnable {
   
               // CameraProvider
               val cameraProvider: ProcessCameraProvider = cameraProviderFuture.get()
   
               // Preview
               preview = Preview.Builder()
                   // We request aspect ratio but no resolution
                   .setTargetAspectRatio(screenAspectRatio)
                   // Set initial target rotation
                   .setTargetRotation(rotation)
                   .build()
   
               // Must unbind the use-cases before rebinding them
               cameraProvider.unbindAll()
   
               try {
                   // A variable number of use-cases can be passed here -
                   // camera provides access to CameraControl & CameraInfo
                   camera = cameraProvider.bindToLifecycle(this, cameraSelector, preview)
   
                   // Attach the viewfinder's surface provider to preview use case
                   preview?.setSurfaceProvider(viewFinder.createSurfaceProvider(camera?.cameraInfo))
               } catch (exc: Exception) {
                   Log.e(TAG, "Use case binding failed", exc)
               }
   
           }, ContextCompat.getMainExecutor(requireContext()))
       }
   ```

* Add the following helper method to find the correct aspect ratio of the device and set it to CameraX

   ```kotlin
   private fun aspectRatio(width: Int, height: Int): Int {
       val previewRatio = max(width, height).toDouble() / min(width, height)
       if (abs(previewRatio - RATIO_4_3_VALUE) <= abs(previewRatio - RATIO_16_9_VALUE)) {
           return AspectRatio.RATIO_4_3
       }
       return AspectRatio.RATIO_16_9
   }
   ```

* Start the camera

   ```kotlin
   private fun startCamera() {
       viewFinder.post {
           bindCameraUseCases()
       }
   }
   ```

That's all folks. You just need to handle the camera permissions in the usual manner and the above code will give you the basic camera preview setup. Now lets dig a little deeper and see what are we actually doing here.

## Explanation ##

* **Find the device aspect ratio and rotation values**
   We will use the `DisplayMetrics` API to find these values and use them later in both setting up CameraX as well as in future scenarios send this to MLKit.
   ```kotlin
   val metrics = DisplayMetrics().also { viewFinder.display.getRealMetrics(it) }
   val screenAspectRatio = aspectRatio(metrics.widthPixels, metrics.heightPixels)
   val rotation = viewFinder.display.rotation
   ```
* **Select which camera to use and create a `ListenableFuture` of the `ProcessCameraProvider`**

   ```kotlin
   val cameraSelector = CameraSelector.Builder().requireLensFacing(lensFacing).build()
   val cameraProviderFuture = ProcessCameraProvider.getInstance(requireContext())
   ```

   A `ListenableFuture` in short allows you to register callbacks to be executed once the asynchronous computation is complete, or if the computation is already complete, immediately. You can find more details in the [official documentation](https://github.com/google/guava/wiki/ListenableFutureExplained)
   Callback for this `cameraProviderFuture` contains the logic for when the `ProcessCameraProvider` is available to prepare it to be initialized by binding it to the lifecycle and required use cases

* **Prepare the camera preview use case**
   Here we prepare the camera preview use case using the aspect ratio and rotation values calculated earlier. 

   ```kotlin
   preview = Preview.Builder()
       // We request aspect ratio but no resolution
       .setTargetAspectRatio(screenAspectRatio)
       // Set initial target rotation
       .setTargetRotation(rotation)
       .build()
   ```

   Use-cases provide a very clear abstraction between the three main things we generally use camera for - preview the camera feed, capture from the camera feed and analyse the captured frames. CameraX provide these three use-cases as separate classes which we can extend as per our requirement. You can find more details about the use-cases in the [official documentation](https://developer.android.com/training/camerax/architecture#combine-use-cases) and we will explore them further in future articles in this series.

* **Bind the `ProcessCameraProvider` to the lifecycle along with the use-cases**
   First we have to unbind all the existing use-cases from the camera provider. If not it will throw runtime exception

   ```kotlin
   cameraProvider.unbindAll()
   ```

   Binding the `ProcessCameraProvider` to the lifecycle is a must as this allows the CameraX API to automatically manage the camera resources bases on the provided lifecycle, reducing a lot of boilerplate code needed earlier with `Camera2` API. We also attach our use-case here, `Preview` use-case in our sample, for the CameraX API to show the camera preview.  We now take this post-binding camera instance and set it to the `PreviewView` object from the layout xml. This is where the preview will be rendered on the UI

   ```kotlin
   try {
       // A variable number of use-cases can be passed here -
       // camera provides access to CameraControl & CameraInfo
       camera = cameraProvider.bindToLifecycle(this, cameraSelector, preview)
   
       // Attach the viewfinder's surface provider to preview use case
       preview?.setSurfaceProvider(viewFinder.createSurfaceProvider(camera?.cameraInfo))
   } catch (exc: Exception) {
       Log.e(TAG, "Use case binding failed", exc)
   }
   ```

* **Start the camera**
   Calling the 'bind' code in  `post` on the `viewFinder` ensures that the code is called on the UI thread, which is mandatory for initiating the CameraX API. Not doing this will give a run-time exception.

   ```kotlin
   viewFinder.post {
       bindCameraUseCases()
   }
   ```


And now we have a fully functional camera preview app using CameraX. You can find the complete source code here: https://github.com/funkyidol/CameraXSample. 

Hope this helps & give me a follow to receive notifications for future articles in this series.
