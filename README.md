# rpi2rootfs
a raspberry pi 2 rootfs generator &amp; a disk image maker

# who need this tool?
I bought raspberry pi not for learning anything, I want to use it as a server. It 
may be a router, or help me to control other hardward. But image supplied by official website,
with GUI, and so many softwares I never use. for these software, I have to prepare a huge TF card,
at least 8G. I have a TF card with only 4G space, I can't install system NOOBS, raspbian depend on 
jessie, only raspbian depend on wheezy can run on it, but the system is too old. This made me very unhappy.
So I found this project, the basic system generate by it only need 1G space. If you think the same thing as me,
try these scripts, if you want to teach your kids programming, go to buy a new TF card.

If you want to run raspberry pi only as a router, maybe you should try openwrt. The newest version 15.05
support raspberry pi and raspberry pi 2.

# how to use

The scripts is tested on debian jessie, need package qemu-user-static installed. All script need user root.

step 1: edit mirrors.base and mirrors.raspberrypi, uncomment one line to choose your mirror. If you uncomment multiple lines, the first line will be used, so if you don't use the default one, comment it.

step 2: edit packages, add any package you need, or delete you don't use.

step 3: run command ./rpi2rootfs, it make a "rootfs", which is the root of new system.

step 4: run command ./rpi2image, it makes a 1G image, rpi.img. You can write it to the TF card. If you generate these on your remote server, download the rpi.img.tar.bz2 (yes, no need tar, bzip2 can compress directly, but bzip2 has bugs on read file alloced by tool fallocate), it is the same file but smaller.

step 5: write image to TF card, you should google it for the detail, or just read the guide of raspbian or NOOBS from raspberry pi official website, but the most important line is: pv &lt;rpi.img &gt;/dev/sdX, X is the device of you TF card. The TF catd's space more than 1G is enough. When it finished, use tool resize2fs to expand partition 2 to the whole TF card if you want. 

step 6: put TF card into raspberry pi, power on. You can login with root:root. It default support wired network and dhcp, so you can also login through ssh if you can get the ip address.

step 7: change root password (passwd), add new user (adduser), choose timezone (dpkg-reconfigure tzdata), choose locales (dpkg-reconfigure locales), and configure other things if you like. Yes, I default installed wifi tools, run command wicd-curses, if you don't understand the GUI, google for it.

step 7.5: Another thing you should know, the swapfile is not configure default. Someone think it is important,can make system more staticly, if you want it, run "apt-get install dphys-swapfile" and configure it. This swapfile tool can not install in script rpi2rootfs, the "mount" get bugs on chroot. 

step 8: Have Fun!!!
