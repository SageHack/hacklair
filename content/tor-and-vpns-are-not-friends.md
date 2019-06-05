+++
date = "2019-06-05T00:00:00-04:00"
title = "Tor and VPNs are not friends"
description = "Let's take a look at why you should use a VPN, then connect to the Tor network."
+++

Recently, my colleagues and I were discussing the importance of the Tor network. At some point, we came to the topic of security and discussing our setup. One explained he was using his personal computer, which was running Windows, connected to a VPN and then connected to Tor. Believe it or not, 8 years ago when I got into digital activism, this was my exact setup.

This setup is very bad. The main concern here is the VPN. It's putting your data at risk, and decreasing anonymity benefits from the Tor network.

Let's review this setup, which I've used in the past and that I think, some others do use.

## Why is it bad?

There are multiple problems here.

### Windows (and Mac OS)

I hope I don't need to explain how week security and proprietary software is bad in the activism context. This OS security is so weak. Just [an example](https://twitter.com/TheHackersNews/status/1131567152522178560) I got from my Twitter feed today. Also, it's proprietary software. It's bound to have a hidden tracking mechanism.

Mac OS has better security, but it's bound to the same proprietary tracking concerns.

### Using your personal computer

Activism will lead you to unexpected places. Using a dedicated computer will greatly benefit your security. Once you engage in legal battles of with covert adversaries, a lack of security will usually mean your downfall.

First, it will separate your personal files from your activism files. Those probably include family photos, bills, passport scans, academic or work documents, and many other important documents that can be used to identify or track you. The computer you use for activism will likely be targeted at some point. Techniques to cripple activists vary widely but to my personal experience, seizing, stealing or destroying electronics are the primary means of doing arm. When that happens, you will likely be able to fall back to your main computer to a certain extent.

Second, you are probably using MacOS or Windows for your personal, academics or work-related tasks. Those OSes are not recommended for activism. [Debian](https://www.debian.org/distrib/netinst) is what I recommend. That being said, if you are new to Linux, I highly recommend using [Ubuntu](https://www.ubuntu.com/download/desktop). Having a second computer will allow you to use Linux without sacrificing your favorite OS. You can also back you important activist related files and documents to your primary computer, once encrypted.

Third, security is prime for your activist related tasks. You will use a stronger passphrase, multiple authentication layers, and encryption. Those are usually not in place on your personal computer and you are likely to never bother unless you switch to a dedicated computer.

Also, a virtual machine is not equivalent to a dedicated computer. VMs are not as secure as you'd think. There are also ways to monitor those, especially if you're not familiar with open source OSes and VM technologies. Regardless, it's still better than using Windows and is a great way to start learning using Linux.

### The VPN

#### Baseline: Do not trust VPNs

This is the core. Unless you use it properly, a VPN will do more harm than good to your privacy. Before we dig deeper into this, we need to establish a baseline: When anonymity is involved, no VPN can be trusted.

First, it's a black box and your security is based on trust. We all know how that works out. Two great articles to give you full context: [When law enforcement knocks on a VPN’s door](https://www.ivpn.net/blog/when-law-enforcement-knocks-on-a-vpns-door-what-happens) which cite a LulzSec member case, and [VPNs are lying about logs](https://restoreprivacy.com/vpn-logs-lies/).

Second, there are also cases where the service is trustworthy but simply not on par with the technical requirement thus, leaking your information.

#### How it's bad for your Anonymity

Ok so let's assume, you use a trustworthy technically capable VPN provider on dedicated hardware. There is still a problem:

Your VPN creates a permanent entry and exit point. Inevitably, you will do things that don't run over Tor and run over your VPN, like resolving a domain name through your DNS services or reading a PDF that loads an external resource. It's possible to build a profile based on that usage and there are known working escapes around VPNs, especially when it comes to DNS resolution.

Keep in mind, that this is the best case scenario and your specific case is unlikely to be the best.

Further reading: [Torproject.org/docs/ - Is Tor Like a VPN](https://2019.www.torproject.org/docs/faq#IsTorLikeAVPN).

## Conclusion

For most activists: Use Ubuntu as a desktop on a dedicated computer, build a Tor proxy on a separate Debian based computer, route everything to it through a single IP and port, and block everything else with a firewall. It works and I will write on how to set this up in an upcoming post.

Also, VPNs are meant to connect you to your home or work network while not on site. They do protect your privacy (but not your anonymity) when used properly and I highly recommend that you do use them especially when using public networks.
