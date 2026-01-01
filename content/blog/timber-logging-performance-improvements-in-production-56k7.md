---
title: "Android Logging Performance Improvements in Production"
date: 2024-06-20
summary: "When logging in production using timber, you can easily exclude certain log levels to prevent..."
draft: false
tags: ["androiddev", "performance", "crashlytics", "android"]
canonicalURL: "https://dev.to/funkyidol/timber-logging-performance-improvements-in-production-56k7"
---
When logging in production using timber, you can easily exclude certain log levels to prevent sensitive debug data from transmitting online. 
```kotlin
private inner class CrashReportingTree : Timber.Tree() {
        override fun log(priority: Int, tag: String?, logMessage: String, throwable: Throwable?) {
            if (priority == Log.ERROR || priority == Log.INFO) {
                FirebaseCrashlytics.getInstance().log(logMessage)
                if (throwable != null) {
                    FirebaseCrashlytics.getInstance().recordException(throwable)
                }
            } else return
        }
    }
```

What this doesnt do is ignore the said logs. If timber comes across a debug log in the above case, it will still be processed completely until the time comes to actually log it, for e.g. operations like formatting and splitting. This can create a performance overhead in production if the logging is being done generously and with potentially large data like network request results.

There is a way where you can tell Timber if it should ignore certain log types completely and not process the log message at all.
```kotlin
private class CrashReportingTree : Timber.Tree() {  
    override fun log(priority: Int, tag: String?, logMessage: String, throwable: Throwable?) {  
        if (!isLoggable(tag, priority)) {  
            return // Skip logging if not loggable  
        } else {  
            FirebaseCrashlytics.getInstance().log(logMessage)  
            if (throwable != null) {  
                FirebaseCrashlytics.getInstance().recordException(throwable)  
            }  
        }  
    }  
  
    // Overridden to stop processing of all logs less then info level within Timber  
    override fun isLoggable(tag: String?, priority: Int): Boolean {  
        return priority >= Log.INFO  
    }  
}
```

Overriding `isLoggable` tells the Timber api to match and process only allowed log types internally before it does any processing
[timber/timber/src/main/java/timber/log/Timber.kt](https://github.com/JakeWharton/timber/blob/e6db346a2934a55bb940d0a5d293a931f54de066/timber/src/main/java/timber/log/Timber.kt#L149)

Hope this brings some finer performance boost to your apps
