+++
date = "2016-01-11T10:55:06-04:00"
title = "Case study: Reading memory content"
description = "In this case study we learn how to read memory dumps from Android apps"

+++

By using Logcat and Wireshark we were able to get a lot of interesting information but we can go deeper into the system. The Android Developer Studio includes multiple tools we can use. It allows us to check memory allocations, generate memory dumps, view thread executions, get performance statistics, etc. In this case, we want to investigate the app memory content.

First, we need to install Android Studio, and get it running, which isn't an easy process. If you are running Ubuntu, you can use this custom repository.

<pre>
sudo apt-add-repository ppa:paolorotolo/android-studio
sudo apt-get update
sudo apt-get install android-studio default-jdk lib32z1 lib32ncurses5 lib32bz2-1.0 lib32stdc++6
</pre>

*This will not install the latest version but we don't need it.*

Pro tip: You can install an operating system without affecting your current configuration with software like [Virtual Box](https://www.virtualbox.org/).

Once installed, we'll start Android Studio and create a blank project. Then we can connect our device to our computer via a USB cable and start monitoring via "Tools >> Android >> Android Device Monitor".

If you are having problems connecting your device, unlock it, fire up the console and type in **adb shell**. You will need to authorize your computer. A pop-up will ask you to validate the connection fingerprint.

Once Android Device Monitor is running you'll see a list of device processes on the left tab. From there, we can pick a process and activate profiling by clicking **Update Heap** and **Update Threads**. Information will appear on the right tab. We can also use the logcat output at the bottom. Use **adb shell ps | grep cm.aptoide.pt | cut -c10-15** to get the process id and filter out other app logs.

This part gets a bit technical. You will see Java execution threads and will have to dig out what is what. For example, I stumbled upon "Okio Watchdog" and Googled it. The app uses the [Okio external library](https://github.com/square/okio) to manage its input/output.

That's quite interesting but what we want to get is the memory content. For that, we will need to create a heap dump, a memory snapshot. On the top of the process list, there's a button called **Dump HPROF file**. That's what we need.

To analyze that file we need to [download Java Visual VM](https://visualvm.java.net/download.html). Android heap dumps aren't in the format JVM need but we can convert it with **hprof-conv cm.aptoide.pt.hprof cm.aptoide.pt.st.hprof**.  It's a binary from Android Studio. You'll need to find it on your computer. Now fire up **visualvm** and open the converted hprof.

Now we can browse Java objects instances, which in Java is pretty much everything. You can also use the OQL console, a query tool. Check the [Visual VM Object Query Language documentation](https://visualvm.java.net/oqlhelp.html) to get a basic understanding.

Ok, so what do we have from this dump?

* The app file path /storage/emulated/0/.aptoide/
* Some API endpoints
* And a bunch of database queries

With the OQL console, we can search strings for with the help of a [regex](https://en.wikipedia.org/wiki/Regular_expression).

<pre>
select s.toString() from java.lang.String s where /regex/(s.toString())
</pre>

There's way too much info in there...

Analyzing Aptoide with those tools wasn't that beneficial. We didn't learn much. But if we need to look at memory content at a later point we'll have no problem finding what we need.

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
