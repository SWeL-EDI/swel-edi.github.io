---
id: 157
title: 'Using Garmin eTrex Vista HCx with Ubuntu 14.04LTS &amp; QLandkarte GT'
date: '2015-08-07T08:07:06+01:00'
author: 'Phil Barker'
excerpt: 'I have a rather old Garmin GPS eTrex that I use for GPS on walking holidays and cycle rides. I use it with OpenCycleMap contour maps downloaded from talkytoaster. To plan routes and manage the routes, tracks and maps&nbsp;on Ubuntu I use QLandkarte GT. &nbsp;This summer was the first time I used this combination on &hellip; <a href="http://blogs.pjjk.net/phil/using-garmin-etrex-vista-hcx-with-ubuntu-14-04lts-qlandkarte-gt/">Continue reading <span>Using Garmin eTrex Vista HCx with Ubuntu 14.04LTS &amp; QLandkarte GT</span> <span>&rarr;</span></a>'
layout: post
guid: 'http://blogs.pjjk.net/phil/?p=1443'
permalink: 'http://blogs.pjjk.net/phil/using-garmin-etrex-vista-hcx-with-ubuntu-14-04lts-qlandkarte-gt/'
enclosure:
    - "\n\n"
syndication_source:
    - 'Sharing and learning'
syndication_source_uri:
    - 'http://blogs.pjjk.net/phil'
syndication_source_id:
    - 'http://blogs.pjjk.net/phil/feed/'
syndication_feed:
    - 'http://blogs.pjjk.net/phil/feed/'
syndication_feed_id:
    - '2'
syndication_permalink:
    - 'http://blogs.pjjk.net/phil/using-garmin-etrex-vista-hcx-with-ubuntu-14-04lts-qlandkarte-gt/'
syndication_item_hash:
    - 40dd52c961232bc7ec2c13137b40773c
    - fcb1ede43005605fffb0c2ed5d13312a
    - fcb1ede43005605fffb0c2ed5d13312a
    - dd0c7c4c348aec5f8f115172d178cb39
    - dd0c7c4c348aec5f8f115172d178cb39
    - 40a98d873df149d4b3d104b05c67cc01
    - a6d14dc847fc021f8fe009302225af45
    - 4f13728d7dc718236d56f8669fffc357
categories:
    - GPS
    - Other
    - Ubuntu
---

[![garmin](http://blogs.pjjk.net/phil/content/uploads/garmin-150x150.jpg)](https://buy.garmin.com/en-GB/GB/outdoor/discontinued/etrex-vista-hcx/prod8703.html)I have a rather [old Garmin GPS eTrex](https://buy.garmin.com/en-GB/GB/outdoor/discontinued/etrex-vista-hcx/prod8703.html) that I use for GPS on walking holidays and cycle rides. I use it with [OpenCycleMap](http://www.opencyclemap.org/) contour maps downloaded from [talkytoaster](http://talkytoaster.co.uk/maps/). To plan routes and manage the routes, tracks and maps on Ubuntu I use [QLandkarte GT](http://www.qlandkarte.org/). This summer was the first time I used this combination on my new PC, and I found some of the config difficult because the info I could find (e.g. [this from GPS babel](http://www.gpsbabel.org/os/Linux_Hotplug.html)) related to old versions of Ubuntu (not surprising, this garmin is from the Ubuntu Feisty era). What needs doing seems similar but how you do it has changed.

I edited /etc/modprobe.d/blacklist to stop Ubuntu loading the garmin\_gps module. I don’t know if this is necessary, but everything I want seems to work with it there. That file now looks like:

```
# stop garmin_gps serial from loading for USB garmin devices

blacklist garmin_gps
```

The to make sure that the Garmin is automounted r/w for all users when plugged in to a USB post I created /etc/udev/rules.d/51-garmin.rules , with the content

```
SUBSYSTEM=="usb", ATTR{idVendor}=="091e", MODE="0666", GROUP="plugdev"
```

I found the lsusb and the [gpsbabel utility](http://www.gpsbabel.org/download.html) useful in testing the connexion. With it installed and the etrex plugged in I now see

```
phil@shuttle$ lsusb
Bus 002 Device 002: ID 8087:8001 Intel Corp. 
[...]
Bus 003 Device 004: ID 091e:0003 Garmin International GPS (various models)

phil@shuttle$ gpsbabel -i garmin -f usb:-1
0 3834401962 694 eTrex Vista HCx Software Version 3.40
```

And then in QLandkarte I can go to setup | general and under the “device and xfer” select Garmin in the main drop-down and EtrexVistaHCx in the Device Type (other Device options left blank) and happily transfer routes and tracks between the PC and the GPS.

![Screenshot from 2015-08-07 09:11:51](http://blogs.pjjk.net/phil/content/uploads/Screenshot-from-2015-08-07-091151-535x480.png)