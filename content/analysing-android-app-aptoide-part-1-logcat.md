+++
date = "2016-01-03T09:25:09-04:00"
title = "Case study: Reading logs with adb logcat"
description = "In this study we will see how we can read an Android app logs with adb logcat."

+++

For this case study I will be using a dedicated Android device as [detailed here](/getting-your-android-device-ready-for-hacking/) and focus on [reading Android logs and dumps](/working-with-android-logs-and-dumps/) to find information on both software.

Here's more detail on the device:

* Google Nexus 4 (mako)
* Cyanogen 13.0-20151231-NIGHTLY-mako
* Android 6.0.1
* TWRP 2.8.7.0

If you would like to update TWRP before you start simply install the official [TWRP manager](https://play.google.com/store/apps/details?id=com.jmz.soft.twrpmanager) from Google Play. I personally prefer to use fastboot provided by the Android SDK.

### Backing up

Backups are always good. Especially in our case since we will mess things up and we never know what goods apps will bring us. Malware, root kits, trojan, etc. Take your pick.

<pre>
$ adb reboot recovery
</pre>

And go to backup and let the thing run. When it's done restart and save the files on your computer.

<pre>
$ adb reboot
$ adb pull /sdcard/TWRP
</pre>

### About Aptoide

For this case study we will analyze a piece of software that is not allowed on the Google Play store. This software allow to install other software, paid or unpaid, for free. It's likely that the software contain malicious instructions. We will use various tools to figure out what is going on under the hood.

### Installing the app

Visit http://www.aptoide.com/ with your phone browser and install the app. Once installed hit open and let's use logcat, and a bit of magic, to see what's going on.

<pre>
$ adb logcat | grep `adb shell ps | grep cm.aptoide.pt | cut -c10-15`
</pre>

A lot is happening here. But that's what we want. Let's take a closer look at what we got:

* Some app states
* HTTP requests
 * Headers
 * Response
* Execution errors
* External libraries logs
* OpenGL debug logs
* [Adreno GPU](https://developer.qualcomm.com/software/adreno-gpu-sdk/gpu) logs
* Download manager logs

In this case we can see the app use all of those external libraries:

* [Flurry Analytics](https://developer.yahoo.com/flurry/docs/analytics/gettingstarted/android/)
* [RoboSpice](https://github.com/stephanenicolas/robospice/wiki/Starter-guide)
* [Amazon Insights](http://www.i-programmer.info/news/83-mobliephone/6578-amazon-insights-sdk.html)
* [Retrofit](https://guides.codepath.com/android/Consuming-APIs-with-Retrofit)

And all API endpoints called over http:

* http://ws2.aptoide.com/api/7/getStore
* http://webservices.aptoide.com/webservices/2/listApkComments
* http://webservices.aptwords.net/api/2/getAds
* http://webservices.aptoide.com/webservices/3/listSearchApks
* http://ws2.aptoide.com/api/6/listAppsUpdates
* http://ws2.aptoide.com/api/7/getApp

Also errors:

* Search suggestions query threw an exception.

> Other posts from the **Android forensics and security analysis** series:
>
> * [Getting your device ready for hacking][android-hacking]
> * [Working with logs and dumps][basic-tools]
> * [Case study: Reading logs with adb logcat][cs-logcat]
> * [Case study: Capturing and reading packets][cs-packets]
> * [Case study: Reading memory content][cs-monitoring]
> * [Case study: Depackaging with Apktool][cs-apktool]

[android-hacking]:/getting-your-android-device-ready-for-hacking/
[basic-tools]:/working-with-android-logs-and-dumps/
[cs-logcat]:/analysing-android-app-aptoide-part-1-logcat/
[cs-packets]:/analysing-android-app-aptoide-part-2-wireshark/
[cs-monitoring]:/analysing-android-app-aptoide-part-3-systrace/
[cs-apktool]:/analysing-android-app-aptoide-part-4-apktool/
