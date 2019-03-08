---
title: Tutorial for setting up Huawei E3276 4G/LTE wireless modem with Debian Linux and Raspberry Pi
date: "2015-03-04T23:46:37.121Z"
template: "post"
draft: false
slug: "/posts/tutorial-setting-up-huawei-e3276-4g-lte-wireless-modem-debian-linux-raspberry-pi/"
category: "Technology"
tags:
  - "Technology"
  - "Tutorial"
  - "Linux"
description: "Tutorial on how to set up the Huawei E3276 4G/LTE wireless modem with Debian Linux and a Raspberry Pi."
---

Wireless data modems have always been hit-and-miss with  Linux (Debian) and Raspberry Pi's. Recent Ubuntu releases have featured semi-plug’n’play functionality, but this only ever seems to work with hardware that has been around for at least 2 years.

I needed to get mobile internet on a robotic project I’m working on, which uses a Raspberry Pi. A bit of research online quickly revealed that no mainstream manufacturer officially supports Linux (big surprise!), but that Huawei is heads-and-shoulders above the competition in being somewhat Linux friendly. Huawei used to release Linux software for managing its 3G modems (although the most recent versions are Windows-only), and its adapters continue to be Linux-friendly with a bit of setup.

Now, if you Google for setting up a mobile modem with Linux, you’ll probably find references to Sakis3G, a script that provides both a terminal and GTK+ interface for setting up mobile internet sticks. Unfortunately, Sakis3G hasn’t been maintained recently, and it didn’t work for any of the configurations I tried. It probably works fine with older 3G modems, but don’t expect it to work with newer 4G/LTE wireless modems that are sold via mainstream cellular companies.

I bought a Huawei E3276 from Telus (in Canada), and tested it with Windows and Mac. Ironically, it didn’t work with Huawei’s Mac software out-of-the-box, and I didn’t bother trying to fix it! Onto Linux.

Now, as I mentioned above, the popular Sakis3G script didn’t work for me. Instead, let me outline a method that I have tested both with Debian Linux (on a standard x64 PC) and Raspbian on a Raspberry Pi (note that Raspbian is based off of Debian). I haven’t tested this with Ubuntu or other distributions, but I would be highly surprised if it doesn’t on all major Linux distributions.

Now, just as a little disclaimer, I don't take any responsibility for any of the following instructions; they are pretty straightforward, and I don't think they should cause any problems with your carrier... but nonetheless, since Linux is usually not carrier-supported, use at your own risk! The important thing, as outlined later on in the instructions, is getting your APN correctly setup, so that you don't get billed outside of your data plan!

With that out of the way, let's get started! First, install the following packages:
sudo apt-get install lsusb ppp usb-modeswitch wvdial sg3-utils

Now, plug in your Huawei E3276 and run the command “lsusb”, which should list all of your usb devices. Look down the list, and make sure that your modem is hooked up. Every 3G/4G/LTE modem has two modes, one for storage/miscellaneous use, and one for modem mode. We need the E3276 to be set in the latter mode, and sometimes this isn’t automatic. Just run the command "lsusb", and scroll down to see if your device is in the list, AND look for a line that looks something like this (yours may look different; the important part is that the description has "modem" in it! If it just says "Huawei Technologies Co.", then it hasn't switched into modem mode yet!):

Bus 001 Device 006: ID 12d1:1506 Huawei Technologies Co., Ltd. E398 LTE/UMTS/GSM Modem/Networkcard

Okay, so assuming that you’ve verified that the E3276 is in Modem mode, time to go hands-on editing a few configuration files. I like using the nano editor… I know, I know… vi is the “real” programmer/linux editor, but this isn’t time for a flamewar.

Edit the following file: /etc/wvdial.conf

```
[Dialer Defaults]
Init1 = ATZ
Init2 = ATE1
Init3 = AT+CGDCONT=1,"IP","isp.telus.com"
Stupid Mode = 1
MessageEndPoint = "0x01"
Modem Type = Analog Modem
ISDN = 0
Phone = *99#
Modem = /dev/ttyUSB0
Username = { }
Password = { }
Baud = 460800
Auto Reconnect = on
Important Note: You will need to change the "isp.telus.com" part to whatever your APN is for your provider! Also, make sure you use the correct APN: many providers have one APN for phones, and another APN for data-only plans. If you use the wrong APN with your SIM card, you will get charged for data outside of your plan... trust me, I learned that the hard way while setting this up!
```

Okay, if you've got your APN setup correctly, now we just have to edit one more file: /etc/network/interfaces
Append (not replace!) the following lines to the end of the file:

```
auto ppp0
iface ppp0 inet wvdial
```

Now, all you have to do is type the following in the terminal! (You may have to use sudo, but try without first)
wvdial & disown

And now you should be connected! To quickly test to see if it's working, just try pinging a server:
ping google.com

Or if we want to get fancy with our internet browsing experience from the terminal, there's nothing quite like lynx (the world's best text-based terminal browser, in case you've never heard of it!):
lynx google.com

Finally, the Huawei E3276 has an indicator light on it that will probably be useful for verifying the connection state:

Blue, blinking: 4G network available.
Cyan, blinking: 4G LTE available.
Blue, solid: Connected to a 4G network.
Cyan, solid: Connected to a 4G LTE network.
Good luck using your Huawei 4G modem with Linux!

NOTE: I only tested these instructions with a Huawei E3276, but they may very well work for some other modems from Huawei! I've heard that they are all very similar, possibly with the same chips inside.