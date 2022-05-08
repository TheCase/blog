---
layout: post
title: salvaging a XBOX 360 wireless controller module for use in OS X
date: '2012-02-13 15:48:35'
collections:
- hacks
---


A few days back, I saw the [post on Hackaday](http://hackaday.com/2012/02/03/reclaim-the-wireless-controller-module-from-a-broken-xbox-360/ "post on Hackaday") about how you can solder a USB cable and some components on the powerbutton/wireless module from a XBOX 360 and [use it as a host for wireless controllers on your PC](http://diru.org/wordpress/2011/03/wireless-xbox360-controller-on-a-pc-without-the-commercial-dongle/ "dil isi lib").

I just happened to have one on hand, but had some different ideas from previous projects. First, I wanted the hack to be non destructive, so I wouldn’t be soldering stuff directly to the control board. Secondly, I wanted to use this on my Mac, not a PC.

Hardware you’ll need:

- wireless module from a 360
- XBOX 360 wireless controller
- XBOX 360 Charge and Play cable
- USB cable
- proto board with solder pads – mine was from radioshack, but something [like this](http://www.sparkfun.com/products/8808) should work too
- A Windows PC to complete the pairing process
- A Mac running OS X

Here’s what that wireless module looks like once removed from the 360:

[![](https://i0.wp.com/res.cloudinary.com/thecase/image/upload/v1514683258/dsc_4799_wslheq.jpg?resize=300%2C200 "XBOX 360 wireless module")](https://i0.wp.com/res.cloudinary.com/thecase/image/upload/v1514683258/dsc_4799_wslheq.jpg)

So, for the first part. I’ve made my own USB connectors in the past with a proto board and some blobs of solder. Just cut the board down to fit and add some even height blobs of solder to make contact with the pins in the socket.

[![](https://i0.wp.com/res.cloudinary.com/thecase/image/upload/v1514683257/dsc_4801_mpyeo0.jpg?resize=300%2C200 "my connector")](https://i0.wp.com/res.cloudinary.com/thecase/image/upload/v1514683257/dsc_4801_mpyeo0.jpg)

This hack also requires a couple 1N4001 diodes to drop the supply voltage from +5v to around +3.3v – and the proto board is perfect for that. I attached some 30 gauge kynar wire to each blob to make it a bit easier to connect the circular traces on this board.

The edge seen in the right side of this picture will be the side that is inserted into the connector on the wireless module.

The top most part of the connector on the wireless module has 4 pins.  This is where my proto board bumps will be making contact with those pins:

[![](https://i0.wp.com/res.cloudinary.com/thecase/image/upload/v1514683259/dsc_4797_l3sv7i.jpg?resize=300%2C199 "connector top")](https://i0.wp.com/res.cloudinary.com/thecase/image/upload/v1514683259/dsc_4797_l3sv7i.jpg)

Here’s a closer shot of the board making contact with those pins.  Note that you’ll have to be careful in how you size down the edges of the proto board to insure proper alignment of the contacts:

[![](https://i1.wp.com/res.cloudinary.com/thecase/image/upload/v1514683256/dsc_4815_spp50h.jpg?resize=300%2C200 "connector bottom")](https://i1.wp.com/res.cloudinary.com/thecase/image/upload/v1514683256/dsc_4815_spp50h.jpg)

Part 2: connecting to the Mac

Prior to all of this, I tested it on a PC, following the directions in Dil’s writeup – just to make sure my cable was working as expected.

Then, get and install the OSX drivers for 360 controllers:

[http://tattiebogle.net/index.php/ProjectRoot/Xbox360Controller/OsxDriver](http://tattiebogle.net/index.php/ProjectRoot/Xbox360Controller/OsxDriver)

The syncing trick that was discussed on Dil’s blog does not seem to work on the Mac.  You must plug both the module and a controller with the Charge and Play cable into a PC to get the module and the controller to sync (you’ll need to follow his procedure for getting the software installed and modified for the new wireless module).

Once you’ve completed the pairing on a PC, plug the module into the Mac and hold down the silver/center/large X button on the 360 controller.  It should start to blink and then connect to the module.  Open System Preferences -> Xbox 360 Controllers – you should see your controller in the Device: pulldown selection!

[![](https://i1.wp.com/res.cloudinary.com/thecase/image/upload/v1514683255/screen-shot-2012-02-13-at-1-50-27-pm_z4f1rm.png?resize=604%2C337 "Screen Shot 2012-02-13 at 1.50.27 PM")](https://i1.wp.com/res.cloudinary.com/thecase/image/upload/v1514683255/screen-shot-2012-02-13-at-1-50-27-pm_z4f1rm.png)

If you don’t have the Windows PC that is necessary for the syncing step, you could always [use an arduino to do it](http://diru.org/wordpress/hacking/xbox-360-rf-module-arduino/) instead.


