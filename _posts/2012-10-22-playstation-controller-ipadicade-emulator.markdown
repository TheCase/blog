---
layout: post
title: Playstation controller -> iPad/iCade emulator
date: '2012-10-22 18:18:25'
categories:
- hacks
---


Silly me, I almost dropped $30 on one of these bluetooth game controllers for iOS… and thankfully I got my brain back in order and started thinking about how I could hack some stuff I already own to do this.

Essentially, these bluetooth game controllers for iOS/Android are just bluetooth keyboards. I started out thinking I could hack this tiny bluetooth keyboard that I already have – but hardwiring the keyboard keys to buttons…

So I started looking into the magic behind these controllers, starting with the bluetooth iCade cabinet. Turns out that they use a special version of keymapping that is not as straight foward in implementation. The deal with these is that when you hit a button, it sends a single keyboard key signal (like the letter A) and then sends another key signal when you release the button (like Q). This is true of the D-Pad/Joystick as well.

This is where I decided that hardwiring something wouldn’t “just work”. I’m sure there’s some hardware folks out there that’ll say “hey, no problem”, but that’s because you know more than I – but I’m sure it would include more hardware than just the controller, and that’s something I was trying to avoid.

Arduino to the rescue:

In researching how I might do this, I discovered that iPad Camera Connection Kit (again, something I already have) allows you to hook up USB keyboards to your iPad (how I didn’t know this, well, I don’t know). I also thought that I might use an old PC gamepad that I had lying around, but stumbled across an Arduino library for talking direct digital to Playstation controllers (also in a box in the garage). Also existing is a library for emulating a USB keyboard from the Arduino, but currently I’m two zener diodes short on the hardware side to test.

Research:

Playstation Controller Arduino Library:  
[http://www.billporter.info/playstation-2-controller-arduino-library-v1-0/](http://www.billporter.info/playstation-2-controller-arduino-library-v1-0/)  
 Arduino Virtual USB Keyboard:  
[http://code.rancidbacon.com/ProjectLogArduinoUSB](http://code.rancidbacon.com/ProjectLogArduinoUSB)  
 iCade controller reverse engineering discoveries:  
[http://gaming.stackexchange.com/questions/24774/icade-bluetooth-keyboard-mappings-for-mame](http://gaming.stackexchange.com/questions/24774/icade-bluetooth-keyboard-mappings-for-mame)

So, I start on this journey: Playstation Controller -> Arduino -> USB keyboard protoshield thingy -> iPad Camera Connection Kit -> iMAME for iOS

a couple of hours of hacking on the controller->Arduino bit. I dug up an old wireless dongle for a PSOne controller and ripped out the controller socket. [ Note: the case it was in is probably perfect to re-house all the guts once my DigiSparks arrive to replace the massive Duemilanove that I’m using for dev on the project.]

Followed the wiring diagrams:


## Controller -> Arduino

CLK -> Pin7  
 ATT -> Pin6  
 CMD -> Pin5  
 DAT -> Pin4  
 5v -> 5v  
 GND -> GND

I had to fiddle with the timings in the actual PS2X library code to get my buttons to be recognized correctly, but after a little tweaking, we have success!

[![Screen Shot 2012-10-22 at 1.43.12 PM](https://i1.wp.com/res.cloudinary.com/thecase/image/upload/h_194,w_300/v1514683110/Screen-Shot-2012-10-22-at-1.43.12-PM_vrjiul.png?resize=300%2C194)](https://i1.wp.com/res.cloudinary.com/thecase/image/upload/v1514683110/Screen-Shot-2012-10-22-at-1.43.12-PM_vrjiul.png)

Here we have the current hardware prototyping mess. Also included is the breadboarded USB breakout this is missing those zener diodes. As soon as I make my hardware run, the USB keyboard emulation tests will be the subject of the next post. Until next time!

[![IMG_4237](https://i0.wp.com/res.cloudinary.com/thecase/image/upload/h_225,w_300/v1514683106/IMG_4237_wljmum.jpg?resize=300%2C225)](https://i1.wp.com/res.cloudinary.com/thecase/image/upload/v1514683106/IMG_4237_wljmum.jpg)

I was cruising right along, until I started running into issues with the USB keyboard emulation. It’d work great for about a minute and the arduino would appear to hang.

So I decided to trash the USB keyboard emulation idea and got myself a Bluetooth HID module. I never did get into hacking on that thing (there were some lightly documented firmware changes that I’d have to make), so there in died the posting of updates for this project.

Until! After the holidays, ThinkGeek put the iCadeJr on clearance for $10 each (sadly, no longer offered at this price). Its a nifty little bluetooth thing that emulates a bluetooth keyboard, works with iOS and Android. Problem: its probably meant for full sized Smurfs to play on, as I find it impossible to make it work with any efficiency.

[![iCadeJr_Hands_media](https://i2.wp.com/res.cloudinary.com/thecase/image/upload/h_188,w_300/v1514683104/iCadeJr_Hands_media_wak3xk.jpg?resize=300%2C188)](https://i2.wp.com/res.cloudinary.com/thecase/image/upload/v1514683104/iCadeJr_Hands_media_wak3xk.jpg)

But that’s ok, as I knew I’d tear this thing apart anyhow. Ten minutes later, I have this:

[![IMG_0026](https://i2.wp.com/res.cloudinary.com/thecase/image/upload/h_225,w_300/v1514683102/IMG_0026_wbmctk.jpg?resize=300%2C225)](https://i1.wp.com/res.cloudinary.com/thecase/image/upload/v1514683102/IMG_0026_wbmctk.jpg)

So – this is what I’ll be hacking on the other end of the Arduino instead of an emulated USB keyboard. You can see that the Bluetooth controller is nice and exposed, and they even gave me a nice connector to work with for the front buttons. There are four buttons on the back of the unit – which is good, as I plan to map those to the shoulder buttons on the PS2 controller. Also what looks like a serial header that’s ready for a pin header to be soldered in there.

Hopefully I’ll have more details later. Wish me luck!


