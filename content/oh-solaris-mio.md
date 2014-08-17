---
title: oh solaris mio !
author: Juan B. Rodriguez
date: 2012-05-07T11:11:11Z
tags:
  - solaris 11
  - osx
  - zfs
  - crashplan
  - rsync

type: regular
---

so the plan is as follows:

- build a zfs box, with a two drive mirror pool
- rsync data from blackeard (my hackintosh mac) to the zfs box
- snaphot the zfs filesystem (full and incrementals)
- crashplan the backup to the cloud

this basically gives me a two factor backup scenario: time machine-like fast access (without all the storage wasting that time machine does, on the zfs box) and offsite more secure storage (crashplan pro on the cloud)

so let's start with my test setup

download [Solaris 11 11/11](http://www.oracle.com/technetwork/server-storage/solaris11/downloads/index.html) (you have to create an oracle account .. shrugs)

install Solaris on a VirtualBox VM (chose VMDK as format, since it will be easier to transfer to ESXi)

the first snag is related to NFSv4 ... although it's supposed to do uid mapping, [it actually doesn't](http://dfusion.com.au/wiki/tiki-index.php?page=Why+NFSv4+UID+mapping+breaks+with+AUTH_UNIX).

the first time i installed solaris i didn't change the uid for my replica solaris user (same user as my mac box).

so i installed again, but ... solaris 11 won't allow root logins, not even via console. so i did the easiest thing possible, which is to enable root logins back [more info here](http://candon123.blog.51cto.com/704299/712206):

<blockquote>
root@zfsbox# rolemod -K type=normal root
</blockquote>

so now drop to the root shell (su - won't work) and do
<blockquote>
usermod -u &lt;new uid&gt; username
</blockquote>

[here's a link that gave me the idea on how to do this](http://www.unix.com/solaris/183739-changing-uid-value.html) 

&lt;new uid&gt; should be the same uid as the user in the mac box.

while on the root shell, do
<blockquote>
cd /home

chown -R &lt;username&gt;:&lt;group&gt; &lt;username&gt;
</blockquote>

ok now solaris is installed. one of the first things i do with any new *nix box is setup public/private key ssh
<blockquote>
<span>$ ssh-keygen -t rsa</span>
<span>$ cat ~/.ssh/id_rsa.pub | ssh user@machine "mkdir ~/.ssh; cat &gt;&gt; ~/.ssh/authorized_keys"<br /></span>
</blockquote>

could have use ssh-copy-id, but osx doesn't have it by default and i'm too lazy to install it [credits for the cat/ssh technique](http://www.commandlinefu.com/commands/view/188/copy-your-ssh-public-key-to-a-server-from-a-machine-that-doesnt-have-ssh-copy-id)

now you have to edit /etc/ssh/sshd_config to disable password logins

ok so we can ssh into the solaris box ... let's build the backup pool

i previously created two 51Gb virtual disks in VirtualBox, it's time to use them
<blockquote>
user@zfsbox$ format
</blockquote>

this shows the name of the disks. now let's create the pool
<blockquote>
user@zfsbox$ sudo zpool create tank mirror c3t2d0 c3t3d0
</blockquote>

now the filesystem, which crashplan will back up
<blockquote>
user@zfsbox$ sudo zfs create -o atime=off -o mountpoint=/export/backup -o sharenfs=on -o compression=on -o encryption=aes-256-ccm tank/backup
</blockquote>

by default, zfs creates the /export/backup mount point with root:root ownership. make it writable for your user
<blockquote>
user@zfsbox$ sudo chown -R &lt;username&gt;:&lt;groupname&gt; /export/backup
</blockquote>

now, you can rsync from mac to zfs
<blockquote>
user@macbox$ rsync -avn --progress -e ssh ~/Storage user@zfsbox:/export/backup
</blockquote>

you should be all set now, watching your /export/backup folder having grown with your backup data.

something else ... in order to watch that data through nfs

go to disk utility, in the menu choose nfs mounts ... and add the nfs mountpoint, pay special attention to the advanced mount options, should be something like this
<blockquote>
resvport,vers=4,nolocks,locallocks,intr,soft,wsize=32768,rsize=32768
</blockquote>

next up, we'll work with the zfs snapshots, try to come up a script that automates the rsyncing and the snapshot creation and send it all up to crashplan
 
