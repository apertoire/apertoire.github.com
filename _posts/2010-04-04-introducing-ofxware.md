---
layout: post
title: Introducing ofxware

---

![ofxware](/img/ofxware-logo1-780x234.png "ofxware")

### Rationale

At the beginning of the year, I opened an account with a different bank than the one I was using exclusively for the past few years.

Although some external factors were involved, there was also some financial gains with this transaction.

Anyhow, this new bank has a somewhat challenging understanding of ofx (Money) format, so the ofx files I downloaded weren’t readable by [GnuCash](http://www.gnucash.org/).

I initially thought about doing some manual manipulation, but quickly realized it wasn’t scalable.

And so … ofxware was born !

It took me a couple of iterations but finally I reached a stage where I could use it in a live environment, that is actually using it to support my finance management.

This is not a finished product yet, but it works for me.

Additionally, it’s open source on purpose … you can be the one to enhance the functionality, make it easier and more available to the general public.

### Product

ofxware is a very simple application thats converts text data files downloaded from online banking sites into ofx format files.

It’s a C# application, using the MVVM paradigm and it’s based on a plugin architecture, which means it is extensible in order to accept and process different formats of input files.

Additionally it’s open sourced under a GPLv3 license, so feel free to review the code and contribute with your own enhancements.

Download at [ofxware Google Code project](http://code.google.com/p/ofxware/).