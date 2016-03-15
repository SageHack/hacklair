+++
date = "2016-03-14T18:59:39-04:00"
title = "How to install Guild Wars 2 on Ubuntu"
description = "This guide will help you setup Guild Wars 2 on Ubuntu and get blazing fast FPS."

+++

Guild Wars 1 and Guild Wars 2 has been my favorite games for quite a while. Since I'm using Ubuntu and Debian full time and don't want to install Windows, I had to figure out how to make the game work.

## Vendor drivers

The first thing you want to do is to get the latests proprietary software drivers. I know it suck but the Open Source drivers just doesn't cut it.

From your terminal lunch "software-properties-gtk" and click on the "Additional Drivers". You should see drivers for your devices. Select the newest one for you graphic card and click "Apply changes". You'll need to reboot you machine in order for the drivers change to take effects.

If you feel like adventuring, you can Google around for newest drivers. Ubuntu offer a lot of proprietary drivers but in most case they are out of date.

## PlayOnLinux

Once your video drivers are properly setup [install PlayOnLinux](https://www.playonlinux.com/en/download.html).

### GW2 64bit client

Open PlayOnLinux and let it finish its updadtes. Then click "Install" and search Guild Wars 2. Ignore all the warning but be mindful of the prompts. The install wizard is going to prompt you for the client architecture and your graphic card memory. Select amd64 if your computer is compatible and make sure you specify the correct memory capability for your graphic card. This is very important.

When the game client start downloading the game, shut it down. If you previously installed Guild Wars 2 move the gw2.dat file from your previous install in "~/.PlayOnLinux/wineprefix/GuildWars2/drive_c/Program Files (x86)/ArenaNet/Guild Wars 2".

### Wine 1.9.5 and other tweaks

From the main window open the "Tools" menu and select "Manage Wine version". Click on the amd64 tab and download the latests version. Follow the wizard and complete the install. Return to the main window select Guild Wars 2 and click configure. 

In the "Install Components" tab select and install d3dx9. In the "Display" tab disable GLSL support.

### Finish up

Start the launcher, finish the update and play.

That's it! Enjoy :)


