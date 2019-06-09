+++
date = "2016-01-07T06:37:51-04:00"
title = "Case study: Capturing and reading packets"
description = "In this case study we learn how to dump Android app packets and analyze them in Wireshark"

+++

In the last post, we installed unapproved Android app Aptoide, installed an app and used ADB Logcat to check what was going on. This time we will be using [tPacketCapture pro](https://play.google.com/store/apps/details?id=jp.co.taosoftware.android.packetcapturepro) and [Wireshark](https://www.wireshark.org/).

[How to use Wireshark with Android](/wireshark-on-android/).

### The analysis tool

Wireshark is the most popular packet capture and analysis tool. It is immensely useful for software forensics. It can be used in a lot of different scenarios and hardware configuration. It is highly recommended that you start the software and open a .pcap file to understand what it can be used for. The statistics menu is particularly useful to figure out the big picture.

For this post, we will also be using tshark, in a bash command line, which allows for some fancy magic.

### Endpoints

Let's start this by checking all endpoint ip and figure out who they belong to:

<pre>
for ip in $( tshark -r capture.pcap -q -z dests,tree | grep -o -E "([0-9]{1,3}\.){3}[0-9]{1,3}" ); do
    curl ipinfo.io/$ip
done
</pre>

This gives us a detailed list of endpoints.

As you can see destinations are: Amazon, LeaseWeb and Yahoo. Connections to Yahoo are from the Flurry Analytics as we have seen from the logcat in the previous post. All other endpoints connect to the app servers, which can gather any type of data they want.

### HTTP

Now we know where the data traveled but it doesn't give us much insight on what it contained. Let's look at the HTTP requests since they are not encrypted and are easy to filter out.

Here's the command I used to get what seemed like most interesting.

List of domains:
<pre>$ tshark -r capture.pcap -T fields -e http.host | sort | uniq</pre>

All requested URLs:
<pre>$ tshark -r capture.pcap -T fields -e http.request.full_uri | sort | uniq</pre>

Same thing but not sorted, as a time line:
<pre>$ tshark -r capture.pcap -Y "http.request.method" -T fields -e http.request.full_uri</pre>

And let's look at all the data sent to the server via HTTP. It's a bit hard with the command line so let's use the graphical interface. I'll use the filter "http.request.method==POST" and look at each requests.

Most requests send data that any normal apps would. The following one stands out, /api/6/ListAppsUpdates. It sends a list of all the installed apps, even system processes, with a hash signature. This is not harmful but it's private information they can resell.

### SSL

I also want to know what encrypted data was transmitted over standard web protocols.

So let's list all the SSL chat:
<pre>$ tshark -r capture.pcap -Y "ssl"</pre>

And https packets:

<pre>$ tshark -r capture.pcap -Y "tcp.port==443"</pre>

There's quite a bit of encrypted data going around. Let's take a look at the I/O graph to check the proportion.

The problem here is that we can't see what is transited. There's a way to [decrypting TLS data that goes through your browser](https://jimshaver.net/2015/02/11/decrypting-tls-browser-traffic-with-wireshark-the-easy-way/) but from within an app that's an entirely different story. We'll have to find the SSL keys, and they could be stored anywhere.

We can also get info from all SSL endpoints with this command
<pre>
for ip in $( tshark -r capture.pcap -Y "ssl" -T fields -e ip.dst | sort | uniq ); do
      curl ipinfo.io/$ip
done
</pre>

My guess would that encrypted data is used mainly by external libraries. We know from the logcat that it uses two analytic libraries, one by Amazon and one by Yahoo, which correlate with the info we have here. Still, the app connects with SSL to LeaseWeb, which I'm starting to guess, is where the app is hosted.

Let's compared the bandwidth transferred in and out of LeaseWeb servers to the total bandwidth in the Statistic IO Graph menu.

And gotcha! 90% of the total bandwidth is from LeaseWeb and 10% is SSL. Which fit my guess.

### Conclusion

We learned that no data transmitted by the app is encrypted. That also means we can easily use Wireshark to validate what data is transmitted while using the app. In this case, it seems legit data. As of now, this app doesn't seem like a malicious piece of software.

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

