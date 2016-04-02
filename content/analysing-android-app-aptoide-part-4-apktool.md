+++
date = "2016-01-22T09:06:41-04:00"
title = "Case study: Depackaging with Apktool"
description = "In this case study we learn how to reverse engineer Android apps with Apktool"
+++

For this case study we are going to use [apktool, a tool for reverse engineering Android apk files](https://ibotpeaches.github.io/Apktool/), developed by [iBotPeaches](https://github.com/iBotPeaches). If you want to get the tool running on your system read the [installation doc](http://ibotpeaches.github.io/Apktool/install/).

We're analasing Aptoide 6.5.2.

Run **apktool decode cm.aptoide.pt.apk** and let's get started.

The first file we want to check is AndroidManifest.xml. The [Android Manifest official doc](http://developer.android.com/guide/topics/manifest/manifest-intro.html) help us understanding what info we can get. 

This file contain a list of permissions the app equire to run. So [READ_PHONE_STATE](https://encrypted.google.com/search?hl=en&q=android.permission.READ_PHONE_STATE) huh? Reading my [EMEI](https://en.wikipedia.org/wiki/International_Mobile_Station_Equipment_Identity) and my phone number. Why would it need to know that? Good thing we use a [dedicated hacking device](/getting-your-android-device-ready-for-hacking/). Another interesting permission is [READ_EXTERNAL_STORAGE](http://developer.android.com/reference/android/Manifest.permission.html#READ_EXTERNAL_STORAGE) which mean the app can read files on our device.

Next we can check the **smali** folder. In the Android language smali and baksmali mean compiling and decompiling. We recommend you read [this excellent post on understanding Android decompiling](https://www.quora.com/What-is-smali-in-Android).

The folder structure contain libraries included in the app. Well Aptoide certainly love tracking it's users. It contain at least tree analytic library; com.amazon.insights, com.flurry.android and com.localytics.android. Also, we can see it got the Paypal Android SK, which fit payment permission in the manifest.

That's interesting. Let's search for **paypal** in cm.aptoide.pt. 348 hits. All right. The payment management library is called OpenIAB. Let's Google that... and bingo!

If you've read the first case study our goal was to find malicious behaviour within the app, but turn out Aptoide is a decentralized app market place that run on Open Source Software. So it's very unlinkely to contain malicious code.

While looking at the [OpenIAB](https://github.com/onepf/OpenIAB) library I searched Wikipedia for [Aptoide](https://en.wikipedia.org/wiki/Aptoide) and found the [Aptoide source code and dev docs](http://aptoide.org/).

So we have our answer. It's very unlikely to be a malicious software. The binary provided on the website might include changes that are not in the code base. In order to verify this we can compile the app from the source and compare both packages signature but it's out of the scope for this post.

And that pretty much conclude our reverse engineering tutorial and case study series. Hope you liked it!

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
