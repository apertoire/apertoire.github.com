---
title: blackbeard
layout: post
author: Juan B. Rodriguez
tags:
  - mac
  - osx
  - lion
  - filevault

---

i'm writing this from blackbeard, my hackintosh mac.

i was able to build this machine and have it working flawlessy under OSX Lion, mainly due to [tonymacx86's excellent site](tonymacx86.blogspot.com).

two articles showed me in detail how to build the machine

- [Building a Sandy Bridge CustoMac: Buyer's Guide](http://tonymacx86.blogspot.com/2011/11/building-sandy-bridge-customac-buyers.html)
- [UniBeast: Install Mac OS X Lion Using an All-In-One Bootable USB Drive](http://tonymacx86.blogspot.com/2011/10/unibeast-install-mac-os-x-lion-using.html)

i chose the following specs for my mac:

- case: [Corsair Obsidian 650D](http://www.amazon.com/)</li>
- mobo: [Gigabyte GA-Z68XP-UD3](http://www.amazon.com/gp/product/B0054OWTQU/ref=as_li_ss_tl?ie=UTF8&amp;tag=tonymacx86com-20)
- cpu: [Intel Core i5-2500K](http://www.amazon.com/gp/product/B004EBUXHQ?ie=UTF8&amp;tag=tonymacx86com-20)
- ram: [Corsair 1600MHZ DDR3 16GB](http://www.amazon.com/gp/product/B004RFBIUU/ref=as_li_ss_tl?ie=UTF8&amp;tag=tonymacx86com-20)
- gpu: [AMD Radeon HD 6850](http://www.amazon.com/gp/product/B004F6GJAU/ref=as_li_ss_tl?ie=UTF8&amp;tag=tonymacx86com-20)
- power supply: [Corsair 650 watts](http://www.amazon.com/gp/product/B002LVUPZQ/ref=as_li_ss_tl?ie=UTF8&amp;tag=tonymacx86com-20)
- ssd: [OCZ Nocti Series 60GB](http://www.amazon.com/OCZ-Technology-Nocti-mSATA-NOC-MSATA-60G/dp/B005FYFV3W)
- hard disk: [Western Digital 1TB EARS](http://www.amazon.com/Western-Digital-Caviar-Desktop-WD10EARS/dp/B002U1N95K/ref=sr_1_5?s=electronics&amp;ie=UTF8&amp;qid=1324784170&amp;sr=1-5)

the keyboard, mouse and display come from my previous pc rig.

with this hardware and following the instructions on tonymacx86's blog, i had no problem installing OSX Lion and everything is working properly.

to be honest, i have installed lion about 20 times, looking for the best setup possible.

i had two main drivers:

<ol>
	<li>use the hard disk for bulk storage, that's where the data should reside</li>
	<li>encrypt my system so that no prying eyes can get a hold of my data</li>
</ol>

the first objective was kind of easy to achieve, but i really struggled with the second.

i'm using truecrypt in my pc, and since there's a version published for the mac, i thought it would be a breeze to install and setup.

it turned out that mac support is very limited in truecrypt. there is no system encryption or full disk encryption for that matter. additionally, it's really cumbersome the mounting of an encrypted volume under osx.

i went through several iterations of a setup with truecrypt. in the last one, i had an encrypted device partition on the hard disk, but every reboot was painful since (even with an automator script), i had to enter two passwords (the partition and my user's).

in the meantime, i was toying around with filevault. at first it didnt work because it needs a recovery hd partition, which isnt created during install on a hackintosh.

i managed to manually create a recovery hd and got to turn on filevault, but then it wouldn't boot (something to do with a real mac's firmware not being present).

so i was almost contemplating a life of two-password-insert-on-reboot, until i came around [AgileBits Knox](https://agilebits.com/knox).

i installed it, toyed around with it a bit ... and then ... i figured i could run filevault manually from the command line
two sites were invaluable on getting this to work:

- [Lion's Whole Disk Encryption](http://www.red-sweater.com/blog/1935/lions-whole-disk-encryption)
- [Unlock](https://github.com/jridgewell/Unlock)

so i can't encrypt my startup disk (ssd), but i can encrypt my hard disk.

and i moved my /Users folder to the hard disk, so i don't occupy precious ssd space.

thinks look good so far ! 
