---
layout: post
title: Dropbox and Skeinforge/Printrun
date: '2012-03-13 20:30:32'
tags:
- alterations
- configuration
- dropbox
- printrun
- profiles
- reprap-2
- skeinforge
---


If you’re like me and sometimes print from different hosts (desktop at home, laptop remotely), then you may have run into some issues in getting your settings all synced up between those machines.

I found Dropbox to be the perfect solution.  Keep all of your profiles, alterations and models in a Dropbox directory and stop worrying about copying stuff in a scramble before you pack up your stuff for the next meet-up.

If you don’t already have a Dropbox account, [get one today [link]](http://db.tt/75phMSId "get a FREE 2GB Dropbox account") – they are free and awesome!

Note: I’m on Mac/OSX on both my desktop and laptop.  These instructions will also work for linux.  However, I’m not sure about creating shortcuts and how reliable they can be on Windows OSes.  If you know the best way, please leave a note in the comments!  The cool thing about Dropbox is that it is cross platform and should work between mixed operating system configurations as well…

I created a 3d_printing/ directory in the Dropbox root.  Under that I have my printrun/ installation directory (with skeinforge in subdirectory below that), a 3d_objects/ directory (so that I always know where my printable models are) and most importantly, a skeinforge_settings/ directory.

I’ll address the latter mention first – as it is most important.  In the skeinforge_settings/ directory, I have copied the alterations/ and profile/ directories from the .skeiforge/ directory in my home folder.  Once that was copied, I made a symlink in my home directory (replacing the original .skeinforge directory) that points to the folder in Dropbox:

ln -s ~/Dropbox/3d_printing/skeinforge_settings ~/.skeinforge

The other important symlink is the printrun/pronterface settings file.  Copy the .pronsolerc file from your home directory into the Dropbox skeinforge setting directory, and make sure to rename it (I called it _pronsolerc) so that it won’t be hidden to the GUI file manager.  Symlink that file as well (you’ll have to remove/copy/rename the original first, of course):

ln -s ~/Dropbox/3d_printing/skeinforge_settings/_pronsolerc ~/.pronsolerc

Now… repeat this for the hosts that you plan on using as your printing hosts.

Once you’ve done this – you’ll gain two advantages over your previous setup:

1. any change you make on any host will be automatically synced between machines.
2. (and perhaps most important) you’ll have a revision history for your profile changes – this has saved my bacon more than I care to count


