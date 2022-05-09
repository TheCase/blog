---
layout: post
title: Cross Compiling for Raspberry Pi?  Use Docker!
date: '2014-05-06 03:09:39'
categories:
- devops
---


Stop fiddling with serveral downloads and linking toolchains.  

Head into your source code directory and do this:
```
docker run -it -v ${PWD}:/build mitchallen/pi-cross-compile
```

Boom.  You'll have fresh binaries in the build directory of your source!
