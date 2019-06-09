+++
date = "2016-01-15T13:44:30-04:00"
title = "Wireshark on Android"
description = "How to read Android packet dumps in Wireshark"

+++

If you are looking for a Wireshark alternative for Android devices, unfortunately, there are none viable. All know apps on the Google Play doesn't work well or lack updates and features.

The best way to use Wireshark with an Android device is to install [tPacket Capture](https://play.google.com/store/apps/details?id=jp.co.taosoftware.android.packetcapture) or [tPacket Capture pro](https://play.google.com/store/apps/details?id=jp.co.taosoftware.android.packetcapturepro), pull your .pcap dump to your computer with `adb pull` and open them in Wireshark.

You can download [tPacket Catpure pro](http://www.aptoide.com/app/jp.co.taosoftware.android.packetcapturepro/tpacketcapture-pro) from the alternative app store [Aptoide](http://www.aptoide.com/).

### Related docs

* [adb documentation](http://developer.android.com/tools/help/adb.html)
* [full tutorial on using adb pull](http://www.androidauthority.com/android-customization-transfer-files-adb-push-adb-pull-601015/)
* [how to use tPacket Capture on Android](https://www.youtube.com/watch?v=PjJbfYfDsX4)
