+++
date = "2016-03-09T08:16:05-04:00"
title = "Inspect encrypted packets on an Android device"
description = "Decrypt and log SSL traffic on your Android devices with a single app."

+++

It's rather easy to decipher SSL encrypted traffic on any Android device. You install a self sign CA Certificate and bam!

With this attack you can read and tamper data on the fly, as long as you can catch the data flow.

## Security implications

> Adding a new certificate to your list of trusted credentials potentially gives the owner of that certificate the ability to impersonate any secure server such as a secure website or email server, defeating the verification mechanism of SSL. Only install new credentials from sources that you trust.

> Source: http://tamingthedroid.com/trusted-credentials

## Your best buddy

Packet Capture does all the work for you.

[Download on Google Play](https://play.google.com/store/apps/details?id=app.greyshirts.sslcapture)

## How it works

* Add trusted fake SSL certificate to your device
* Encrypt traffic with fake certificate
* Send traffic through your device VPN
* Decrypt with fake certificate
* Capture
* Encrypt with real certificate
* Send to destination

The following article explain how to set things up manually. Everything is explained thoroughly. If you read it carefully, you'll understand the inner workings pretty easily.

[Intercepting and decrypting SSL communications between Android phone and 3rd party server](http://www.myhowto.org/java/81-intercepting-and-decrypting-ssl-communications-between-android-phone-and-3rd-party-server/)

## How to prevent the attack

To prevent tempering you can sign the data with a public key and verify the signature on your server with the private key.

I'm still trying to figure out how to prevent decryption

## Other revelant articles

* [Android 4.0 add user certificates](http://android.stackexchange.com/questions/57976/how-do-i-install-a-user-certificate?answertab=votes#tab-top)
* [Working with certificates](https://support.google.com/nexus/answer/2844832?hl=en)
* [Issue 67037:   Allow users to install own CA certificates](https://code.google.com/p/android/issues/detail?id=67037)
* [End to End security, or why you shouldn’t drive your motorcycle naked](http://www.cloudidentity.com/blog/2005/04/25/end-to-end-security-or-why-you-shouldn-t-drive-your-motorcycle-naked/)

