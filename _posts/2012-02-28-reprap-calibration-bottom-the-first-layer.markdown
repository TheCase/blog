---
layout: post
title: 'Reprap calibration: Bottom, the First Layer and Z-Home'
date: '2012-02-28 20:32:18'
collections:
- 3D-Printing
---


The technical details of the bottom, or first layer, on a reprap print was something that eluded my understanding when I first started working with my printer.  Here’s my best understanding of the subject, as it relates to your reprap (or repstrap or TOM) and your slicing software.  I focus on skeinforge in particular.

First off, we should focus on what the software and your controller board will think is the Home or zero position.  Most tutorials say the print head should be “the width of a piece of paper” above your print platform when to Z-home endstop is engaged. No paper being identical, I decided to use something a bit more reliable to measure the distance: a gap indicator or “feeler” gauge.  Here’s a link to an [inexpensive example that conveniently has the metric measurements marked in addition to the SAE units](http://www.amazon.com/gp/product/B000BYGIR4/ref=as_li_ss_tl?ie=UTF8&tag=repulsornet-20&linkCode=as2&camp=1789&creative=390957&creativeASIN=B000BYGIR4 " Click for larger image and other views     Share your own related images OEM 25025 26-Blade Master Feeler Gauge ").

In my case, with a .5 mm nozzle,  I currently print with .3mm layer height.  In my skeinforge configuration, the Bottom module is enabled and Additional Height over Layer Thickness ratio is set to 0.5 – this means that it will move the print head up .15 mm ( 0.5 ratio * .3mm layer height ) in the Z direction (from Z-Home) before it starts extruding the first layer.

So… based on these numbers, in theory, I should make sure my print head is .15mm from the platform when Z is in the Home position. BUT… we do want to make sure we are a bit closer than that, so we can get good adhesion to the print platform for that first layer.  How close you go will ultimately depend on your printer the platform surface.  I mostly print PLA on glass, with a 2.2 width over height ratio (giving me a .66 mm extrusion width), so I try to make my gap as close to that .15mm as possible  [though being: more plastic surface area = better the surface grip].

Now the actual measurements: the smallest gap I can test with my particular gauge is .006″, or .152 mm.  My platform is mounted at four corners, so I make sure to measure at the extent of each of those corners.  I also have some fairly stiff springs supporting my platform, so the way I “feel” the height may differ from yours.  I place the gauge between the print head and the platform, and adjust the platform height while slowly moving the gauge back and forth until I feel the gap is close enough to start interfering with that movement.  After that, I tighten another half turn to reduce the gap another fraction to add the extra “squish” that will help with adhesion of that first layer.  I only do this extra half-turn because I do not have a gauge that will measure past .15 mm.  I’m hoping that I’m getting somewhere between .12 mm and .14 mm as my actual gap size with this method.  This height, added to the additional height ratio that comes from the Bottom skeinforge module will have our print head starting a couple hundreds less than my .3mm layer height for that first layer (hopefully somewhere between .27 mm and .29 mm).

I try to keep that extra “squish” as minimal as possible.  If you get the head too close to the platform, the plastic needs to go somewhere – and that will be to either side making your extruded stream wider than expected.  When laying down infill on the initial layers, the extruded material will start to overlap and flow upward past the current level of the print head.  This could interfere with the movement of the head, even on the next layer…

Extra Notes:

I recently printed up some thumbwheels with trapped nut holes and added them to the bottom of the screws (with 6/32″ nylocks) that hold my platform.  That single improvement made platform height adjustments a SNAP.  Once I get up from the couch here, I hope to take some pics of my setup.  In the meantime, here’s the [Thingiverse link](http://www.thingiverse.com/thing:13807 "parametric thumbwheel") to the parametric model that I used.  I sized my wheels to about 1″ in diameter.  Anything smaller proved to be difficult to turn for micro-adjustments.  Anything bigger and you might start limiting your X and Y extents.

 

 


