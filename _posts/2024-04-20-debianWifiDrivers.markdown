---
layout: post
title:  "Installing Macbook Pro Broadcom Wifi Drivers on Debian"
date:   2024-04-20 16:37:26 -0500
image: https://jacobkaiserman.com/blog/assets/images/debian.png
---
<h1>Installing Macbook Pro Broadcom Wifi Drivers on Debian</h1>
![debian on macbook pro](https://jacobkaiserman.com/blog/assets/images/debian.png)
I am writing this article because I have found no resources on this issue. I hope that it can help the 2 and a half people with the same issue.

I had an old 2012 unibody MacBook Pro that was running very slow on macOS. Even though it had good specs (I upgraded the ram and replaced the HDD with an SSD), it was still running slow since macOS was no longer optimized for it. I decided to install a GNU/Linux distro to get some use out of it and learn a bit about Linux.

I chose to install Debian for its stability and plentiful documentation. When I first installed it, Debian could not find the old Broadcom BCM43142 driver. I had to plug it into my network via an ethernet cable to do a complete install. If you are unable to do this, you can do a minimal install and then download the desktop environment after getting the wifi drivers to work. After countless hours of searching, I finally found a solution on an old Reddit thread.

First, you will need to add the non-free repository to Debian if you haven’t already. This allows Debian to access proprietary drivers, such as Broadcom. On Debian Bookworm, navigate to the sources list:

<code>sudo nano /etc/apt/sources.list</code>

Add the following line to the file:

<code>deb http://deb.debian.org/debian bookworm main contrib non-free-firmware non-free</code>

Save the file with <code>ctrl+o</code> and close it with <code>ctrl+x</code>

Then, update the package list:

<code>apt-get update</code>

Then you will need to install the linux-image, linux-headers and broadcom-sta-dkms packages:

<code>apt-get install linux-image-$(uname -r|sed 's,[^-]*-[^-]*-,,') linux-headers-$(uname -r|sed 's,[^-]*-[^-]*-,,') broadcom-sta-dkms</code>

Unload the modules with this line:

<code>sudo modprobe -r b44 b43 b43legacy ssb brcmsmac bcma</code>

**Note: the above line needs to be ran as root. If you do not have the proper permissions, type “su”, press enter, and type your password. This will give you root access to run modprobe

The final step is to load the wl module:

<code>sudo modprobe wl</code>

The Broadcom wifi drivers should be functional now. If not, you may need to restart to apply the changes. I hope that this helped anyone who had this very specific problem.
