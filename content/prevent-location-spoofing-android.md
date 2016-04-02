+++
date = "2016-02-09T18:50:32-04:00"
title = "Prevent location spoofing in your Android apps"
description = "Learn how to prevent GPS and location spoofing in your Android apps."

+++

While studying Ingress development history it became pretty obvious that Niantic Labs became responsible for the location mocking detection APIs made available to Android developers. At some point GPS spoofing because a real problem for their community.

We'll study how they fixed that issue, at least on Android.

## Android mocking API

There's a way to verify is the user is mocking locations. It's rather easy to do implement.

[Stack Overflow - Disable check for mock location to prevent gps spoofing](http://stackoverflow.com/questions/6880232/disable-check-for-mock-location-prevent-gps-spoofing?answertab=votes#tab-top)

## Verifying package signatures

Whatever the steps you take to prevent location spoofing you will have to validate your packages signature. If you don't, modified versions of your APK can be used and you'll have no control over what's happening on the client side.

Read this guide [Adding Tampering Detection to Your App][tamp-detection] published by Scott Alexander-Bown on http://airpair.com

[tamp-detection]:https://www.airpair.com/android/posts/adding-tampering-detection-to-your-android-app
 
## User verification

As you can see in the Ingress [1.49][149] and [1.46.1][146] teardown they added a feature which require the user to verify the authenticity of their account by SMS.

If a user account is not authenticated it's still active but has limited features available to them.

It's not something available to all developers but it can definitely help in some cases. And this technique works on any device.

[149]:http://connortumbleson.com/2014/04/08/ingress-teardown-1-49-0/
[146]:http://connortumbleson.com/2014/03/02/ingress-teardown-1-46-1/
