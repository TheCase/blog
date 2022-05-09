---
layout: post
title: Solution for OctoPrint's update "git diff failed with returncode 129" issue
date: '2017-06-29 21:26:01'
categories:
- 3D-printing
---


So I have been wrestling with performing updates within OctoPrint’s GUI update manager.  Returncode 129… every… time.

I searched the web.  The only answer was that maybe my local git repo was corrupted, or that I needed to use the OctoPi image instead of installing OctoPrint on a vanilla Raspian image. (I immediately ditched the OctoPi image once I noticed they renamed an ethernet device from `wlan0` to `wlan0-octopi`!)

Yeah, I was able to log into my Pi and get the update by pulling the new git version.  But that was lame.  I wanted to update through the GUI as it *seemed* everyone else was clearly able to do without issue.

Here’s what I got every time using the upgrade feature from within OctoPrint:

```
RuntimeError: Could not update, "git diff" failed with returncode 129
```

After debugging the update script, I discovered the solution through trial and error.

Here’s what you do, as the user ‘pi’:

~~~bash
cd /tmp
git init
git remote add origin https://github.com/foosel/OctoPrint.git
~~~

And then you should be able to update the app through the OctoPrint update interface! Celebrate!


