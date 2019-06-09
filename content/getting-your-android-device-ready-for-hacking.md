+++
date = "2015-12-30T10:50:50-04:00"
title = "Getting your Android device ready for hacking"
description = "A guide on how to prepare your Android device for forensic analysis, reverse engineering and other hacking activities."

+++

So you want to hack some piece of software available on Android devices he? Here's how to set up a dedicate *debugging* (ahem) device.

## Getting a hackable device

We strongly recommend you use a dedicated device for developing, hacking, bug hunting, and testing. All of those can have undesirable effects on your device.

### Cheap devices

Repairing a broken mobile is cheap and a great way to learn. You will need a [repair kit](http://www.ebay.com/itm/New-45-In-1-Screwdriver-Repair-Opening-Tools-Set-Kit-Pry-for-Pad-Mobile-Phone-/252004540677?hash=item3aaca42105:g:RM0AAOSwPcVViS3j) and probably a [heat gun](http://www.ebay.com/itm/New-Heat-Gun-Hot-Air-Dual-Temperature-4-Nozzles-Power-Tool-1500-Watt-W-Heatgun-/181785532009?hash=item2a53431669:g:YVkAAOSwl9BWLsG7). Then Google around for instructions on how to fix your device.


### Install CyanogenMod OS
Get a [Cyanogen compatible device list](http://wiki.cyanogenmod.org/w/Devices#type=%22phone%22,%22phablet%22,%22tablet%22;). During CyanogenMod install, install the [TWRP](https://twrp.me/) recovery image and when [installing Google Apps](http://wiki.cyanogenmod.org/w/Google_Apps) install the smallest package possible.

### Installing software from other sources

During your hacking adventures, you are highly likely to need software that wasn't approved or submitted to Google Play. So you will need to enable installation form unknown sources. In the settings search for the term "Install" and select "Install from storage". Then activate "Unknown sources". You will see a box pop-up that asks if Google can analyze your device for "security" purposes. We don't want that. The box will pop-up from time to time. Always answer negatively.

### Disable Google history

If you use a Google account on the device, which I discourage, log into [Google history dashboard](https://history.google.com/history/) and pause the history features. Else it's going to track your searches, location, browsing history and much more.

### Cleanup

Once it's booted go to settings, apps and disable all the apps you think won't be useful. Since this list is different on each device, you'll have to figure it out yourself.

### Enable developer options

Now [activate developer mode](http://wccftech.com/enable-developer-options-in-android-6-marshmallow/) and the following options:

* Advance reboot
* Stay awake
* Bluetooth HCI log
* Full root access
* Android debugging
* Local terminal
* Bug report shortcut
* Development shortcut

### Install ADB debugging tools

[This guide](http://lifehacker.com/the-easiest-way-to-install-androids-adb-and-fastboot-to-1586992378) explains how to install ADB on Linux, OSX, and Windows.

*We strongly recommend you use a Linux desktop. [Ubuntu](http://www.ubuntu.com/desktop) is easy to pick up.*

## Trying a few things out

If everything is setup correctly you should have unrestricted access to your device. Let's try a few of them and see how it goes.

### Browsing through your phone files

In the terminal type: [adb shell](http://developer.android.com/tools/help/shell.html#shellcommands). You should see a command prompt that looks like **shell@device:/ $** From there you can wander around with [basic Linux commands](http://www.comptechdoc.org/os/linux/usersguide/linux_ugbasics.html) like; **cd** and **ls**.
 
### Fetching logs

It is possible to get the system logs. All apps write to this log file so game software is likely to have useful information in there. Type **adb logcat** in your command prompt and it should display.

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

