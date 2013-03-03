---
title: storage wars
layout: post
tags:
  - osx
  - unraid
  - zfs
  - esxi
  - das

---

i'm currently running an [unRaid](http://lime-technology.com) server, which hosts my media collection  (movies, tv series, music, pictures and data backups)

but, i'm running out of space on the server (currently 31.69TB used out of 32.51TB available)

so i started looking for options on how to expand my capacity and decided on adding a second unRaid server, virtualizing both unRaids in an ESXi 5 head server and putting the disks on two DAS boxes (discussions at [two unraid servers](http://lime-technology.com/forum/index.php?topic=14521.0), [atlas: a virtualized unraid](http://lime-technology.com/forum/index.php?topic=14695.0), [building a jbod das](http://www.servethehome.com/sas-expanders-diy-cheap-low-cost-jbod-enclosures-raid/)

at some point during that span of time, zfs came up. i researched as much as i could and finally found this enlightening thread: [Freenas vs unRaid](http://forum.xbmc.org/showthread.php?tid=82811&amp;page=17).

my take on this whole storage wars is that each solution has its merits and my plan changed slightly

- continue with the virtualized + das boxes unraid setup
- add a virtualized zfs implementation to backup my osx data

the idea is that unRaid is much better suited to hold an expanding media collection, where i can add drives when needed and keep having one parity disk to protect the array. under zfs, every drive (or more precisely every vdev) would hit me with a parity space penalty

in my next posts, i will write down my zfs test scenario, while i wait for the parts of my all-encompassing ESXi build

