---
layout: post
title: RK-007 MIDI Commander - Improved
date: '2021-04-30 18:05:56'
image:
  path: /assets/img/rk007-blog.jpg
categories:
- synthesizers
- 3d-printing
---

[](https://www.retrokits.com/shop/rk007/)

I recently stumbled across this incredible little device while trying to figure out how to get the USB MIDI transport messages from my [Roland GO\:KEYS](https://amzn.to/2PFm8Uk) keyboard to other devices on the MIDI chain. Its such a treat to have full control to send Sequence Start/Stop, Patch changes, Control changes or any Note (and Panic!) to any Channel with one little device!  It will operate as both a USB-MIDI device as well as through a 1/8" TRS jack to standard DIN-5 MIDI jack.

![IMG_2574-5](https://res.cloudinary.com/thecase/image/upload/q_auto:good/IMG_2574-5.jpg)

Here's a video by Retro Kits demoing the features: https://www.youtube.com/watch?v=v8QWg009FRE

I built an Arduino Pro Micro version of the device, but I found the instructions and part sourcing information to be quite light. Also, I felt the 3D-printed case could use some more beef, as 1mm thickness is a bit too flimsy for the walls of a device case.

Here is a link to my modified case STL: https://github.com/TheCase/rk007-arduino-pro-case-modified

You might be wondering what that random rectangle is in my redesign.  It is a spacer to put between the Arduino and the KeyPad for proper spacing when soldering it into place.  This will allow the proper clearance when plugging the USB Micro cable into the Arduino.

Here are some Amazon referral links to all the parts you will need.  Some of the parts are only available in sets of 2 or more to land on a reasonable per-unit price.  Use the extra parts to build one for a friend!

- Arduino Pro Micro https://amzn.to/2PDxIiP https://amzn.to/3e4HvYs
- I2C SSD1306 OLED Display https://amzn.to/3xwfhxD
- 4x4 Keypad https://amzn.to/3e2Rw8C
- 1/8" TRS Jack https://amzn.to/3e6zFO3
- 10k potentiometer https://amzn.to/3u9DS99
- 220 Ohm 1/4 watt resistors https://amzn.to/2ReixwG
- Dial Knobs https://amzn.to/3vyuJHK


#### Items of note

"TRS" stands for Tip, Ring, Sleeve. When shopping for a TRS->MIDI 5-DIN cable, you are looking for a "Type A" version.  Type A has the following pinout:

- Tip -> DIN Pin 5 (Data Reference) - TXD from Arduino 
- Ring -> DIN Pin 4 (Voltage Reference) - VCC from Arduino
- Sleeve -> DIN Pin 2 (Shield) - GND from Arduino

There are many cables on Amazon that advertise themselves as TRS->MIDI cables.  Yet, they are the "Type B" that has a pinout configuration that will not work with the RK-007.  Here is a link to an inexpensive Type A from Sweetwater -> https://www.sweetwater.com/store/detail/0-COASTMidi--make-noise-0-coast-midi-cable-1-8-inch-trs-to-5-pin-midi

#### Tools

In case you were wondering about my favorite soldering iron, wonder no more: [Weller WSTA6 Pyropen Junior Self-Igniting Cordless Butane Soldering Iron](https://amzn.to/3u8x7og).  Look ma!  No cords!

#### Need help?

If you have any other questions about the contstruction or operation of the MIDI Commander, drop a line in the commments.  Thanks for reading!
