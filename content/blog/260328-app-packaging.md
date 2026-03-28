+++ 
title = "App packaging on Linux"  
date = "2026-03-21"  
description = "Quick guide to building a Debian package from some Go code"
tags = [ "linux", "debian", "talks", "go" ]  
+++

I gave a talk at this month's [Sydney Linux Use Group](https://www.slug.org.au/) meetup. There is a meeting on the last Friday of every month. It is a great way to meet fellow enthusiasts and learn something new.
Join us next time if you are in the neighbourhood.

My talk was about application packaging in Linux. My goal before the talk was basically to figure what a ```deb``` package contained. I have never bothered to do this before, in spite of using Linux for a very long time.
I took a simple Go program and walked through compiling, packaging, installing, and finally looking in the deb file. As with any magic trick, once you know it, it seems obvious.


Go binaries being statically linked by default, made building the package very easy. It also enables compiling the code for multiple architectures without having to install any cross-compilers.
The code and slides I used are [here](https://github.com/bobbyphilip/towel-day-countdown)

---
I wrote the slides in markdown, using [marp](https://marp.app/) to present them. I’m still figuring out the best way to combine images and text on a slide. Other that it was easy to use and being text based, I could just use vim as my editor. 🎉

