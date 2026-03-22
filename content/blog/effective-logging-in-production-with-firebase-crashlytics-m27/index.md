---
title: "Effective logging in Production with Firebase Crashlytics"
date: 2019-07-25
summary: "Logging and specifically crash logging is a very important aspect of any app that is available beyond..."
draft: false
tags: ["android", "ios", "crashlytics", "logging"]
canonicalURL: "https://medium.com/letsenvision/effective-logging-in-production-with-firebase-crashlytics-9fb3af9f242d"
---
Logging and specifically crash logging is a very important aspect of any app that is available beyond a developers machine. Its simply the act of getting the internal application details generated at the time of the application crash. Be it available to testers or available for public use, catching crashes and identifying errors is critically important for developers to provide a quality product. In mobile app development, Firebase Crashlytics is one of the most widely used Crash logging tool. Crashlytics was build by Fabric (Owned by Twitter) and was later bought by Google and integrated within Firebase.

At Envision, we heavily rely on Crashlytics to give us the insight into our app quality and any issues our users might be facing while using our app. With Crashlytics, we get the crashes our users face, as well as any internal issues our app might be running into which are not necessarily visible to end users.

### Goals

The goals we have with Crashlytics currently are:

1. Crash Logging
2. Issue Identification & Diagnosis
3. App Behaviour insight

### Implementation

There are various features in Crashlytics that generally go unnoticed. We would like to highlight some of the ways we use Crashlytics to achieve the aforementioned goals. 

P.S. - The following details are Android specific but can be easily translated for iOS. All the links below also contain the steps and details of implementing Crashlytics in iOS

- Automatic Crash Logging:
Part of the core feature set, automatic crash logging is what you get the moment you integrate Crashlytics in your project. You can find the integration steps [here](https://firebase.google.com/docs/crashlytics/get-started?platform=android). If you want to exclude debug builds from polluting your crash logs during active development, you can follow the steps [here](https://firebase.google.com/docs/crashlytics/customize-crash-reports?platform=android#enable_opt-in_reporting).
- Non-Fatal Logging:
Non-Fatal logging is where we start using the advanced features of Crashlytics which helps in diagnosing and fixing issues beyond the crashes logged while the app was being used. When exceptions are logged manually in Firebase, they are logged as non-fatals. The best way to use non-fatals in your app is to log all exceptions generated in the catch section of the try/catch block. Additionally, we also create exceptions and log them in situations where our app is in an undesirable state and needs to be examined for the cause and determine its effect on the app.
```kotlin
        try {
              methodThatThrows()
          } catch (e: Exception) {
              Crashlytics.logException(e)
              // handle your exception here
          }
```

- Debug Logging:
We use Timber for managing logs on Android and it makes it very easy for us to manage our logging in debug & production versions. The following configuration prints the logs to the console in the debug version, but in the production versions, it sends the debug logs along with the exception to Firebase.
```kotlin
        override fun onCreate() {
              super.onCreate()
                 if (!BuildConfig.DEBUG) {
                     Fabric.with(this, Crashlytics())
                     Timber.plant(CrashReportingTree())
                 } else {
                     Timber.plant(Timber.DebugTree())
                 }
           }
                
           private inner class CrashReportingTree : Timber.Tree() {
              override fun log(priority: Int, tag: String?, message: String, throwable: Throwable?) {
                 if (priority == Log.ERROR || priority == Log.DEBUG) {
                    Crashlytics.log(priority, tag, message)
                    if (throwable != null) {
                       Crashlytics.logException(throwable)
                    }
                 } else return
              }
          }
```
 
- User Id/Email tagging:
Firebase has the ability to attach the logs collected from a particular user to their unique UserId. This allows us to diagnose and fix issues reported to us by our users especially during the beta test phase. In Firebase console, we have the ability to filter crashes and non-fatal logs for a particular user.
`Crashlytics.setUserIdentifier(userId)`
- App Versioning
At Envision, we try to follow proper versioning of our beta and release builds so that all the crashes and logs collected in Firebase can be quickly filtered for a specific version and fixed for the next version. This same scheme is followed for the internal test builds as well so that additional data could be logged exclusively to the test versions.

### Bottlenecks

Even with all these advanced features, Firebase still falls short is some occasions.

1. Limited log collection storage
Debug Log storage is limited to 64KB per user in firebase and older logs are deleted as new logs come in. This can be a big hindrance in issue diagnostic since many at times by the time we identify an issue and begin diagnostics, the logs are gone.
2. Limited filtering options
The number of filtering options in Firebase is limited to app versions, crashes vs. non-fatals, and User Id. All these work fine for basic crash log usage but for more complex and rare issues these filtering options are restricting. There are no ways in which logs can be filtered out based on a specific OEM, device category or device model. This is especially useful for Android apps where the number of available devices and OEM's are huge and device specific issues are common.
3. No search functionality
There is no search functionality in Firebase crashlytics to search for a specific crash or debug log which again becomes very essential when dealing with specific issues or diagnosing rare crashes.
4. Slow interface
Using Firebase console overall feels very slow and bloated with very large page loading and rendering times. And that is when you are using the Chrome browser. I become much slower when using Firefox.
5. No custom alerts
Firebase is very limited when it comes to issues or trend alerts. They only send email alerts for new issues, regression issues, and trending issues. There are no ways to create custom alerts for e.g. alerts for trends for a specific issue or specific device.
6. No way to directly see debug logs
Currently, the only way to see debug logs os to find them inside a crash log or a non-fatal crash. We understand that the way debug logs are collected and associated on a per crash/non-fatal basis but there should be ways for us to traverse through debug logs on a per User Id or device model basis as well.
7. Limited dashboard & graph statistics
There is only one usable graph that is presented inside Firebase Crashlytics and that is the total crash count on a day, week or month basis. There should be more ways for us to visualize the crash statistics as well. Fabric had very useful graphs on their dashboards that gave a lot of value without us to dig around for that info.

### Going Forward

As our app matures and our use case, Crashlytics has come to a point where we are getting restricted on a regular basis in achieving our goals to quickly identify and resolve issues. We are now looking at some other 3rd party & more advanced crash logging solutions such as [BugSnag](notion://www.notion.so/letsenvision/bugsnag.com) which might be paid but add value to our product in terms of reaching higher quality.

*originally posted at https://medium.com/letsenvision/effective-logging-in-production-with-firebase-crashlytics-9fb3af9f242d*
