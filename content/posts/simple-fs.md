---
title: "Simple Filesystem"
date: 2022-11-15T18:11:00-08:00
draft: false
tags:
    - fs
# categories:
#     - tech
keywords:
    - filesystem
    - ipfs
    - s3
    - arweave
---

I want a simple file system like thing.

Every file storage thing I use has a bunch of different quirks.

* S3 works, but it's a pain to use for small use cases.
* IPFS is nice, but it has a bunch of data availability concerns, and everything being content addressed can be nice in some cases but awful in others.
* arweave is cool, but getting tokens is a problem in the US?

So what am I looking for?

I just want something where I can dump a bunch of files. I can organize the metadata later.

* Files should be decentralized
* Files should be able to be provably deleted
* Files should exist as long as I want them to. They shouldn't randomly dissapear.
* Files should be able to be accessed by a URL
* Files should be able to be accessed by a hash 

I would love to be able to use IPFS as a file system, but I can't delete files? This doesn't work.