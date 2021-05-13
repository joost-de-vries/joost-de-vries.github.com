---
layout: post
title: LinuxMicrosoft Chimaera
description: A hybrid developer laptop without dual boot.
image: pic03.jpg
---

For a developer laptop it starts with lots of cores and memory ofcourse. So having bought the top of the line 6 cores and 16 GB I had to pick an OS. 
Since Sadya Nadella replaced Steve Ballmer Microsoft has become a much much more interesting eco system for developers. Linux is a first class citizen on Azure. Typescript is fully developed in the open, including roadmap and issues. Docker is embraced. &c.
And just as well since SSH, Docker, Git, bash, Openjdk, Linux, Kubernetes are all essential for engineering.
So I've decided to see how far I'll get without a dual boot. 
I'll use Windows as the Gui. After all Firefox, Sublime Edit, IntelliJ, Visual Code are all the same on Mac OS, Linux and Windows anyway. And Apple is as much a walled garden as MS. 

And I'll run my builds in _native_ Linux. Without virtualisation. 

So how can that be? Microsoft mapped the Linux system calls to the Windows kernel. As long as your Linux binary runs in userland and doesn't know about Linux kernel it can run natively on Windows: it's called the Windows Linux Subsystem (WLS). 
`ssh`, `git`, `bash`, `zsh`; they can all be installed using the standard `apt-get` command and just work. No nasty file path issues etc like with Cygwin. Java could be more interesting since it contains a Gui part. But Java is mostly run headless on servers anyway so that also works. My `gradle` build is blazingly fast with 6 cores, no virtualization. Amazing.
Ofcourse Docker and Kubernetes do know about the kernel. So that's a bit more complicated. 
Running simple docker commands is easily done by creating a symlink to the Docker for Windows installation on Hyper V. 
But that doesn't suffice. So the answer there is to configure the Docker cli client within Linux to connect to the Docker server on the host Windows OS.

I've glossed over some annoying configuration issues TBH: 
- zsh uses the Powerline fonts that aren't available on Windows. 
- jdk 11 uses a different ca cert store format. So I had to install jdk 8 as well. Strange when I'm not using that JVM at all but there you are.