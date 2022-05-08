---
layout: post
title: 'Using Ansible to update Synology with Acme certificates from pfSense Certificate Manager'
date: '2021-01-31 18:49:38'
collections:
  - DevOps
---
I love that my pfSense router can manage Acme certificates for my local domain.  I use [DigitalOcean](https://m.do.co/c/9c55dc5264ba) for hosting this blog, so I was able to configure pfSense manage my Acme certificate updates using a DNS Challenge controlled through [DigitalOcean](https://m.do.co/c/9c55dc5264ba)'s API (with a key).

I got tired of having to manually download and upload the certificate files to my Synology NAS every few months.  I'm already leveraging Ansible for other maintenance drudgery, so yesterday I decided to explore automating it.

Prerequisite:  you need to enable the "Write Certificates" option in pfSense's Acme Certificates module.  It is a checkbox that can be found if you follow Services -> Acme Certificates -> General Settings:

![Screen-Shot-2021-01-31-at-11.36.18-AM](https://res.cloudinary.com/thecase/image/upload/q_auto:good/Screen-Shot-2021-01-31-at-11.36.18-AM.png)

I'll just cut to the chase here, I have two Github Gists with the Ansible tasks.  There are two:

1) Copy certificates from pfSense to your Ansible workspace:

[https://gist.github.com/TheCase/d3ac39e7217f83f120e7c334c2f12e5c](https://gist.github.com/TheCase/d3ac39e7217f83f120e7c334c2f12e5c)

2) Copy the certificates to Synology and restart the affected services:

[https://gist.github.com/TheCase/8d53c1f44fba4eb49755731542bbece8](https://gist.github.com/TheCase/8d53c1f44fba4eb49755731542bbece8)

Even if you are not using either pfSense or a Synology, I'm sure these Ansible Tasks could prove useful in your particular situation.  Need help?  Feel free to leave and comment!

Shoutout to \[BIT\]arantno and [the discection of the certificate layout on the Synology filesystem](https://dokuwiki.bitaranto.ch/doku.php?id=synologyimportcertfrompfsense).  You saved me a lot of time! 
