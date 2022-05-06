---
layout: post
title: Synthesizer Patch Visualizer
date: '2021-03-08 02:44:00'
tags:
- music
- hacks
- synthesizers
categories:
- music
- hacks
- synthesizers
---

So, I'm new to synthesizers.  

At least as far as owning and using one.  I have forever loved their use in movie soundtracks of the eighties - and beyond.  I recently became the proud owner of a [Roland SE-02](https://amzn.to/2OekyI6).  Its amazing!  There are hundreds of patches built-in and its incredibly easy to create, change and save those changes.  I've been happily learning, tweaking sounds (from great to terrible) and sequencing them.

But I had one small problem...

I wanted to be able to see the orignal settings of a patch.  Any patch.  

So I built this:  [Synthesizer Patch Visualizer](https://spv.repulsor.net)
![deck](https://res.cloudinary.com/thecase/image/upload/q_auto:good/deck.png)

### What does it do?

It takes patch program files from synthesizers and visualizes the dial and switch positions in a dynamically generated PNG image file (link included).  

### What synthesizer models are supported?

- [Roland SE-02](https://amzn.to/2OekyI6) 
- [Roland SH-01A](https://amzn.to/3kUVSR0)
- [Roland JU-06A](https://amzn.to/3cmPePI)

I'd love to add more Boutique Syths to this tool, but I only have these three.  If you'd like to work with me to build support for more, hit me up in the comments.

### How does it work?  

Either select from the factory patch list, or UPLOAD YOUR OWN!  You need to use the Backup function to download the patch file (ie: `SE02_PATCH00.PRM`).  Then you use the "Choose File" button to upload it to the server. 

The server will do some work and present you with a fully rendered PNG image representing the dial/switch setting of your patch.  You can download the image or copy the generated link and share with your friends and/or the community.  The server does not store any of your patch data.  Once the image is generated, it is up to you to decide how to share or distribute the image or link.  All of the actual patch data is securely encoded in the image as well as the form information included in the image link.

### Go check it out

Here's the link: [Synthesizer Patch Visualizer](https://spv.repulsor.net)

I hope you find it as interesting and useful as I do :) 

### UPDATE

I just added support for the [Roland SH-01A](https://amzn.to/3vjWNzl)!

### UPDATE 2
And I just added support for the [Roland JU-06A](https://amzn.to/3cmPePI)!

### Future Updates

I'd love to add more Boutique Synths to this tool, but I only have these three.  If you'd like to work with me to build support for more, hit me up in the comments.

- this post contains affiliate links to Amazon products
