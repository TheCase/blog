---
layout: post
title: '40W Chinese Laser:  Brain Transplant!'
date: '2015-09-03 21:14:10'
categories:
- 40w-laser
---


[![IMG_0857](https://i1.wp.com/res.cloudinary.com/thecase/image/upload/h_225,w_300/v1514683176/IMG_0857_yjtncu.jpg?resize=300%2C225)](https://i1.wp.com/res.cloudinary.com/thecase/image/upload/v1514683176/IMG_0857_yjtncu.jpg)

I’m removing the stock controller board. The proprietary software is terrible. It is getting replaced with the Open Source RapRep RAMPS G-Code controller. Thanks to the [customized Marlin firmware](https://github.com/TurnkeyTyranny/buildlog-lasercutter-marlin) by [TurnkeyTyranny](https://github.com/TurnkeyTyranny), this gives us several new advantages:

- open source software chain (thanks again to TurnkeyTyranny and the [Inkscape G-Code Export Extension](https://github.com/TurnkeyTyranny/laser-gcode-exporter-inkscape-plugin))
- programmatic control over the laser output power (ditching that terrible manual pot)
- A slick new LCD control panel
I’m surprised I’ve not seen this elsewhere, but I plan to use a thermistor in my coolant tank to monitor the coolant temperature. Hopefully I can hack the firmware to stop firing the laser if the tank temperature rises beyond the set threshold.

I ordered a new ribbon connector and made a new transfer cable to connect to the RAMPS pins. I was too impatient to design and order a wiring harness board, so I just soldered the cable right to the pins on the connector. I covered the contacts with some [Liquid Electrical Tape](http://amzn.to/1QcufwC).

[![IMG_0928](https://i1.wp.com/res.cloudinary.com/thecase/image/upload/h_300,w_225/v1514683174/IMG_0928_dckvym.jpg?resize=225%2C300)](https://i1.wp.com/res.cloudinary.com/thecase/image/upload/v1514683174/IMG_0928_dckvym.jpg)

Below is a diagram of the wiring. Thankfully this was my exact power supply, so I didn’t have to get creative. Now, on the RAMPS, the servo pins are marked 2B 2A 1A 1B and the diagram has A- A+ B- B+. Here is the translation:  
```
<br></br>
A- -> 2B (ribbon cable pin 9)<br></br>
A+ -> 2A (ribbon cable pin 10)<br></br>
B- -> 1A (ribbon cable pin 11)<br></br>
B+ -> 1B (ribbon cable pin 12)<br></br>```

It’s also not very clear on the diagram, but the XHOME goes on the first Signal pin on the endstop header and YHOME goes to the third signal pin. Even though it shows the 5v and GND going to the AUX-3/SPI header, you can use any 5V/GND connections on the other AUX or SERVOS header blocks.

The Y stepper cable connects the following colors to pins:  
```
<br></br>
red -> 2B<br></br>
blue -> 2A<br></br>
white > 1A<br></br>
yellow -> 1B<br></br>```

I’m borrowing this photo from TurnkeyTyranny’s git repo and putting this here so I can find it later:

[![wiring_diagram](https://i1.wp.com/res.cloudinary.com/thecase/image/upload/h_300,w_246/v1514683172/wiring_diagram_fbsjcf.jpg?resize=246%2C300)](https://i1.wp.com/res.cloudinary.com/thecase/image/upload/v1514683172/wiring_diagram_fbsjcf.jpg)

This is not the greatest photo, but some of the wiring choices can been seen here:

[![IMG_0927](https://i1.wp.com/res.cloudinary.com/thecase/image/upload/h_300,w_225/v1514683170/IMG_0927_tql2ay.jpg?resize=225%2C300)](https://i2.wp.com/res.cloudinary.com/thecase/image/upload/v1514683170/IMG_0927_tql2ay.jpg)

I made sure to test the steppers and homes before I even hooked up the laser fire and PWM controls to the RAMPS board. Once everything was moving as I expected, it was time to test the laser! Something about this screen preparing to push the button had me feeling like a mad evil genius set to take over the world: “FIRE ZEE LAZOOR!”

[![IMG_0930](https://i1.wp.com/res.cloudinary.com/thecase/image/upload/h_300,w_225/v1514683168/IMG_0930_bmlh0c.jpg?resize=225%2C300)](https://i0.wp.com/res.cloudinary.com/thecase/image/upload/v1514683168/IMG_0930_bmlh0c.jpg)

As you can see by the burn, the initial tests were a success:

[![IMG_0932](https://i0.wp.com/res.cloudinary.com/thecase/image/upload/h_300,w_225/v1514683166/IMG_0932_udufql.jpg?resize=225%2C300)](https://i1.wp.com/res.cloudinary.com/thecase/image/upload/v1514683166/IMG_0932_udufql.jpg)

Now its time to mount the board and get the wiring cleaned up to make room for more upgrades!



