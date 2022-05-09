---
layout: post
title: 'OLI Project: $50 radio control transmitter: from meh to yeah!'
date: '2013-02-07 16:01:30'
categories:
- hacks
---


My cheap 4-channel TX needed an upgrade, so I went large ($50!) and got myself a Turnigy 9x v2 for Christmas. Months later it arrived.

I just got to messing around with it a couple days ago. The main reason I wanted the upgrade was to get “clicky” switches for changing flight modes (rather than having to rely on a inaccurate pot to set between 6 modes). And… that’s when I noticed the best manual I could find was a google translation of the original Chinese text.

When I bought the transmitter, I had no idea it had a ATMEGA64p in it… let alone some handy soldering pads on the board… and TONS of custom, open firmware mods! Enter er9x custom firmware!

Out comes the screwdriver, soldering iron and AVR programmer:

TX with old (slow!) firmware:

[![IMG_0033](https://i2.wp.com/res.cloudinary.com/thecase/image/upload/h_300,w_225/v1514683133/IMG_0033_bvd0vg.jpg?resize=225%2C300)](https://i1.wp.com/res.cloudinary.com/thecase/image/upload/v1514683133/IMG_0033_bvd0vg.jpg)

ATMEGA64p – thanks for the massive solder pads! (hot glue > duct tape)

[![IMG_0031](https://i1.wp.com/res.cloudinary.com/thecase/image/upload/h_220,w_300/v1514683136/IMG_0031_hubr5b.jpg?resize=300%2C220)](https://i1.wp.com/res.cloudinary.com/thecase/image/upload/v1514683136/IMG_0031_hubr5b.jpg)

New firmware flashed!

[![IMG_0034](https://i2.wp.com/res.cloudinary.com/thecase/image/upload/h_225,w_300/v1514683131/IMG_0034_owuaou.jpg?resize=300%2C225)](https://i2.wp.com/res.cloudinary.com/thecase/image/upload/v1514683131/IMG_0034_owuaou.jpg)

Now, when I originally installed the wire harness, I figured it’d a one-shot deal: flash and done, then close up the case with wiring inside in case I needed to flash it again down the road (which would require cracking the case again). But then I quickly realized the power of being able to plug into the flash at any time, change some EEPROM settings with EEPE, and flash the new config. It is a ton easier than navigating on the LCD to make settings changes.

So I soldered another length of wire after some sawing, filing and hot glue work, I had an externally accessible port:

[![IMG_0037](https://i2.wp.com/res.cloudinary.com/thecase/image/upload/h_166,w_300/v1514683129/IMG_0037_nh8w6h.jpg?resize=300%2C166)](https://i0.wp.com/res.cloudinary.com/thecase/image/upload/v1514683129/IMG_0037_nh8w6h.jpg)

[![IMG_0038](https://i2.wp.com/res.cloudinary.com/thecase/image/upload/h_225,w_300/v1514683127/IMG_0038_zivryk.jpg?resize=300%2C225)](https://i1.wp.com/res.cloudinary.com/thecase/image/upload/v1514683127/IMG_0038_zivryk.jpg)

And here’s the finished product, ready to read/write, looking no worse for wear. Next up will be the oh-so-popular LCD backlight. It seems pretty necessary, as the LCD’s contrast is not the greatest. It’s an inexpensive addition, and seems to be a lot less effort than this hack!

[![IMG_0040](https://i0.wp.com/res.cloudinary.com/thecase/image/upload/h_300,w_225/v1514683126/IMG_0040_obi5id.jpg?resize=225%2C300)](https://i0.wp.com/res.cloudinary.com/thecase/image/upload/v1514683126/IMG_0040_obi5id.jpg)

I added LCD backlight. Much easier to read! I highly recommend adding to to your HobbyKing cart for $5. I ended up paying $15 from an eBay seller in the US.  
 Here’s the new LCD backlight:

[![IMG_0041](https://i2.wp.com/res.cloudinary.com/thecase/image/upload/h_200,w_300/v1514683124/IMG_0041_lqyp3t.jpg?resize=300%2C200)](https://i2.wp.com/res.cloudinary.com/thecase/image/upload/v1514683124/IMG_0041_lqyp3t.jpg)


