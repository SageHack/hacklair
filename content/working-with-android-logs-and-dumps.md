+++
date = "2016-01-02T15:59:52-04:00"
title = "Working with Android logs and dumps"
description = "Learn how to dump and read Android OS and App data."

+++

## Android debugging logs

ADB Logcat display the system debugging file. Apps that use the Android logging API will dump logs into this file which can be open and filtered.

Official doc:

* [Reading Android logs](http://developer.android.com/tools/debugging/debugging-log.html)
* [adb logcat](http://developer.android.com/tools/help/logcat.html)

This command is especially useful to see all logs by process name.

$ adb logcat | grep `adb shell ps | grep com.example.package | cut -c10-15`

## Logging bluetooth traffic

In the developper options activate **Enable Bluetooth HCI snoop log**. Then run **adb shell "cat /sdcard/btsnoop_hci.log"** to view the file or **adb pull /sdcard/btsnoop_hci.log** to save the file on disk.

You will need an hex editor. I recommend:

* Linux: [Qiew](https://github.com/mtivadar/qiew/)
* OSX: [hexcurse](https://github.com/LonnyGomes/hexcurse)
* Windows: [Notepad++](https://notepad-plus-plus.org/) w/ Hex Editor Plugin (included, have to activate)
 

## Capturing TCP/IP packets

[tPacketCapture Pro](https://play.google.com/store/apps/details?id=jp.co.taosoftware.android.packetcapturepro&hl=en) allow you to dump TCP/IP packets from specific apps to .pcap files, which can then be opened in [Wireshark](https://www.wireshark.org/) for analysis.

## RAM forensics

Analyzing allocated memory is quite complex but well documented. This [official Android documentation](http:/>/developer.android.com/tools/debugging/debugging-memory.html) provide all the necessary explanations.

You can use those two commands to get basics memory information:

$ adb shell dumpsys meminfo
$ adb shell dumpsys meminfo 'com.application.namespace'

## Other useful forensic commands

$ adb shell ps
$ adb sell netstart

Show running process
Show current connections
Show all process for an app process ID

## Using Android studio

If you install Android Studio you can use [DDMS](http://developer.android.com/tools/debugging/ddms.html) for complete device analysis.

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
