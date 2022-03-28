---
id: 149
title: 'Mobile computing'
date: '2015-09-06T11:54:46+01:00'
author: 'Phil Barker'
excerpt: 'Ages ago I had my raspberry Pi set up to run headless and wireless, and had built a motor driver based on an H-bridge, all ready for it to become mobile. In fact it did become mobile by canabilising a remote control dalek toy of my son&rsquo;s, but that didn&rsquo;t work too well (it didn&rsquo;t &hellip; <a href="http://blogs.pjjk.net/phil/mobile-computing/">Continue reading <span>Mobile computing</span> <span>&rarr;</span></a>'
layout: post
guid: 'http://blogs.pjjk.net/phil/?p=1509'
permalink: 'http://blogs.pjjk.net/phil/mobile-computing/'
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
    - 'http://blogs.pjjk.net/phil/mobile-computing/'
syndication_item_hash:
    - e4fb9fe2c5461f1d7aced310c3728ece
    - 7446b10a114321e2f078b4ab135e2e25
    - 822d5cc3224f862de529537924bd7051
    - 822d5cc3224f862de529537924bd7051
    - 0b9c34b19be6dc709d314448de231662
    - b0481d0a675d7d10e1e569c202823123
    - a0197bc0c66cb60babde9037801f8890
    - a9dc32cfbb2fcd95ed3b11bc79582b5a
    - a9dc32cfbb2fcd95ed3b11bc79582b5a
    - a9dc32cfbb2fcd95ed3b11bc79582b5a
    - a9dc32cfbb2fcd95ed3b11bc79582b5a
categories:
    - rasppi
    - 'Small computers'
---

Ages ago I had my raspberry Pi set up to run [headless](http://blogs.pjjk.net/phil/headless-pi/) and [wireless](http://blogs.pjjk.net/phil/wireless/), and had built a [motor driver](http://blogs.pjjk.net/phil/motor-driver/) based on an H-bridge, all ready for it to become mobile. In fact it did become mobile by canabilising a remote control dalek toy of my son’s, but that didn’t work too well (it didn’t all fit in). A short while ago I saw a video from @museumsinspire of some Pi-based moving robots which inspired me to try again.

> Moving robots in the 'Pi Power' session [@computermuseum](https://twitter.com/computermuseum) using [@Raspberry\_Pi](https://twitter.com/Raspberry_Pi) and [\#python](https://twitter.com/hashtag/python?src=hash) [pic.twitter.com/UXWjD7Av1X](http://t.co/UXWjD7Av1X)
> 
> — Learning Team (@MuseumsInspire) [August 13, 2015](https://twitter.com/MuseumsInspire/status/631848403450863616)

<script async="" charset="utf-8" src="http://platform.twitter.com/widgets.js"></script>

[@winkleink](https://twitter.com/winkleink) pointed me to the [parts required](http://winkleink.blogspot.co.uk/2014/11/preparing-for-2015-after-school.html)–just £8 for the bits I didn’t already have, and after a few weeks wait while they ship from China:[![2015-09-05 12.23.16](http://blogs.pjjk.net/phil/content/uploads/2015-09-05-12.23.16-640x360.jpg)](http://blogs.pjjk.net/phil/content/uploads/2015-09-05-12.23.16.jpg)  
No instructions, which I like: it saves all those “why don’t you read the instructions” arguments. After some help from my daughter[![2015-09-05 12.52.31](http://blogs.pjjk.net/phil/content/uploads/2015-09-05-12.52.31-640x360.jpg)](http://blogs.pjjk.net/phil/content/uploads/2015-09-05-12.52.31.jpg)

[![2015-09-05 18.50.40](http://blogs.pjjk.net/phil/content/uploads/2015-09-05-18.50.40-640x360.jpg)](http://blogs.pjjk.net/phil/content/uploads/2015-09-05-18.50.40.jpg) Soldering connectors to the motors was a real pain. Also, the chassis came with a 4xAA battery, but it was a bit bulky and I fancied 9v for two motors. However that PP3 doesn’t last long.

The pi and its power pack fit no the top in various configurations, I’m still not sure what works best. In the long run I guess I’ll drill some holes so they can be held more securely (sadly but not surprisingly, none of the existing holes are in the right place).  
[![2015-09-06 12.14.39](http://blogs.pjjk.net/phil/content/uploads/2015-09-06-12.14.39-640x360.jpg)](http://blogs.pjjk.net/phil/content/uploads/2015-09-06-12.14.39.jpg) (The motor controller is in a wee box hidden on the other side of the pi.

I use [the GPIO utility](https://projects.drogon.net/raspberry-pi/wiringpi/the-gpio-utility/) that comes with [WiringPi](http://wiringpi.com/) for quick tests of the motor driver, to work out which GPIO pin send which wheel forwards or backwards, and also to write short shell scripts such as

```
<pre class="brush: plain; title: ; notranslate">
#!/bin/bash
#go forwards
gpio mode 0 out
gpio mode 1 out
gpio mode 2 out
gpio mode 3 out
gpio write 1 0 && gpio write 2 0
gpio write 0 1 && gpio write 3 1
```

to put this little pi bot through its paces  
<iframe allowfullscreen="" frameborder="0" height="315" src="https://www.youtube.com/embed/QKlsp2GIrsY" width="560"></iframe>

Not a bad start. The battery was running low, it was nippier than that at first. Good enough to build on, I think. Once I’ve worked out where best to put all the parts, and got them fixed a little more securely, there are some other enhancements I would like to make. First, the wheels came with optical encoder discs but no sensors for them, so there is scope for some more precise control of positioning. Secondly there’s a pi camera module on that pi, so some scope for a seeing robot, and it would be nice to add other senses as well.