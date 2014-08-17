---
title: moving to github pages
author: Juan B. Rodriguez
date: 2013-03-03T23:23:23Z
tags:
  - hosting
  - github
  - rackspace
  - wordpress
  - vertx

---

it all started when i started considering the deployment of the [vert.x](vertx.io) app i'm working on.

i will deploy to [OpenShift](openshift.redhat.com), but i will also open source the code through [Github](github.com).

so, when i was analyzing how to transfer the code over, i came across [Github Pages](pages.github.com).

i already had two sites:

- apertoire.net (hosted on [Rackspace](rackspace.com))
- apertoire.tumblr.com (hosted on [Tumblr](tumblr.com))

the rackspace site held a wordpress blog and some software products i've developed over the years.

i started the tumblr site when [i dove into mac osx](apertoire.net/why-i-m-switching-to-mac-osx/) and there i chronicled some other infrastructure endeavours.

when i started digging into the whole github pages, i found out about custom domains and read a lot of articles about people switching from any blog framework to github pages.

in my case, it makes a lot of sense as well:

- streamlined content creation and publishing (all i need is a text editor and git)
- no more messing around with wordpress
- no more maintenance of the hosted box (no more watching out for ubuntu updates)
- no more hosting fees !!

the hosting fees aren't really that much (about $12 per month), but in the end all savings add up.

for the record, my custom domain transitions was done following instructions on [setting up a custom domain with pages](https://help.github.com/articles/setting-up-a-custom-domain-with-pages)

on my dns registrar ([Namecheap](namecheap.com)), it went down like this

![change a and cname records](/img/dns.png)

my mail hosting is done via google, so i used namecheap's option to "Automatically set MX records necessary for **Google Apps Email**"

dns propagation already happened for me (i did this about an hour ago), so it should be a smooth transtion all things considered.

