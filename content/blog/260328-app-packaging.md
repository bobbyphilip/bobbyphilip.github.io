+++ 
title = "App packaging on Linux"  
date = "2026-03-28"  
description = "Quick guide to building a Debian package from some Go code"
tags = [ "linux", "debian", "talks", "go" ]  
+++

I gave a talk at this month's [Sydney Linux User Group](https://www.slug.org.au/) meetup. There is a meeting on the last Friday of every month. It is a great way to meet fellow enthusiasts and learn something new.
[Join](https://meetup.com/Sydney-Linux-User-Group) us next time if you are in the neighbourhood.

My talk was about application packaging in Linux. My goal before the talk was basically to figure what a ```deb``` package contained. I have never bothered to do this before, in spite of using Linux for a very long time.
I took a simple Go program and walked through compiling, packaging, installing, and finally looking in the deb file. As with any magic trick, once you know it, it seems obvious.

The crux of building the package can be seen in the [Makefile](https://github.com/bobbyphilip/towel-day-countdown/blob/330af45071299c5d3a17df46d812b9901291428b/Makefile#L17)
- In some sort of a build directory,  create a sub-directory path ```/usr/bin``` and copy the binary there.
- In the same build directory, create a sub-directry DEBIAN and create a ```control``` file. This is nothing but a text file, with some metadata related to the package. This will be used during installation.
- Use ```dpkg-deb``` to package this up in to a deb file


To look inside the package
 - ``` ar x package-name.deb``` to "unarchive" the package, revealing two compressed tar files ```control.tar.zst``` and ```data.tar.zst```, which on extraction reveals the original files which we packaged up earlier 


This glosses over a lot of things like signing the package or actually distributing it. But I think it makes clear the core of what is in a a package. 

Go binaries being statically linked by default, made building the package very easy. It also enables compiling the code for multiple architectures without having to install any cross-compilers.
The code and slides I used are [here](https://github.com/bobbyphilip/towel-day-countdown)

---
I wrote the slides in markdown, using [marp](https://marp.app/) to present them. I’m still figuring out the best way to combine images and text on a slide. Other that it was easy to use and being text based, I could just use vim as my editor. 🎉

