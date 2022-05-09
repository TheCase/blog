---
layout: post
title: 'Using Ansible to update Synology with Acme certificates from pfSense Certificate Manager'
date: '2021-01-31 18:49:38'
image: /assets/img/ans-syn-pfs.png
categories:
- devops
---
I love that my pfSense router can manage Acme certificates for my local domain.  I use [DigitalOcean](https://m.do.co/c/9c55dc5264ba) for hosting this blog, so I was able to configure pfSense manage my Acme certificate updates using a DNS Challenge controlled through [DigitalOcean](https://m.do.co/c/9c55dc5264ba)'s API (with a key).

I got tired of having to manually download and upload the certificate files to my Synology NAS every few months.  I'm already leveraging Ansible for other maintenance drudgery, so yesterday I decided to explore automating it.

Prerequisite:  you need to enable the "Write Certificates" option in pfSense's Acme Certificates module.  It is a checkbox that can be found if you follow Services -> Acme Certificates -> General Settings:

![Screen-Shot-2021-01-31-at-11.36.18-AM](https://res.cloudinary.com/thecase/image/upload/q_auto:good/Screen-Shot-2021-01-31-at-11.36.18-AM.png)

I'll just cut to the chase here, I have two Github Gists with the Ansible tasks.  There are two:

1) Copy certificates from pfSense to your Ansible workspace:


{% raw %}
~~~yaml
# file: "get_pfsense_certificates.yaml"

# alternatively, set as a variable in your inventory
- name: set domain_name
  set_fact: 
    domain_name: mydomain.org
  
- name: get certs
  fetch:
    src: "/conf/acme/{{ item }}"
    dest: ../.certs/ 
    flat: yes
  with_items:
  - "{{ domain_name }}.fullchain" 
  - "{{ domain_name }}.ca"
  - "{{ domain_name }}.key"
  - "{{ domain_name }}.crt"
~~~
{% endraw %}

2) Copy the certificates to Synology and restart the affected services:

{% raw %}
~~~yaml
# file: "update_synology_certificates.yaml"
update_synology_certificates.yaml
- name: set directories
  set_fact:
    sys_dir: /usr/syno/etc/certificate
    pkg_dir: /usr/local/etc/certificate
    stg_dir: /tmp/certs

- name: create cert staging directory
  file:
    path: "{{ stg_dir }}"
    state: directory

# certs from previous task
- name: stage certs
  copy:
    src: "../.certs/{{ item.s }}"
    dest: "/tmp/certs/{{ item.d }}"
  with_items:
    - { s: "{{ domain_name }}.crt",
        d: "cert.pem" }
    - { s: "{{ domain_name }}.fullchain", 
        d: "fullchain.pem" }
    - { s: "{{ domain_name }}.key",
        d: "privkey.pem" }

- name: read the certificate info
  shell:
    cmd: jq -r 'to_entries' {{ sys_dir }}/_archive/INFO
  register: cat_info

- name: set cert_info
  set_fact:
    cert_info: "{{ cat_info.stdout | from_json }}"

- name: copy staged certs to archives
  copy:
    src: "{{ stg_dir }}/"
    dest: "{{ sys_dir }}/_archive/{{ item.key }}/"
    remote_src: true
  with_items: "{{ cert_info | flatten }}"
  register: certs

- name: copy certs for packaged services
  copy:
    src: "{{ sys_dir }}/_archive/{{ item.0.key }}/"
    dest: "{{ pkg_dir }}/{{ item.1.subscriber }}/{{ item.1.service }}/"
    remote_src: true
  loop: "{{ cert_info | subelements('value.services') }}"
  when: item.1.isPkg

- name: copy certs for system services
  copy:
    src: "{{ sys_dir }}/_archive/{{ item.0.key }}/"
    dest: "{{ sys_dir }}/{{ item.1.subscriber }}/{{ item.1.service }}/"
    remote_src: true
  loop: "{{ cert_info | subelements('value.services') }}"
  when: not item.1.isPkg
  
- name: restart affected services
  shell:
    cmd: "/usr/syno/sbin/synoservicectl --reload {{ item }}"
  with_items:
    # different per server - no doubt you will need to add or 
    # remove services from this list
    - nginx                   # DSM
    - pkgctl-MailServer
    - pkgctl-SynologyDrive
    - ftpd
    - pkgctl-ReplicationService
  when: certs.changed

- name: remove cert staging directory
  file:
    path: "{{ stg_dir }}"
    state: absent
~~~
{% endraw %}


Even if you are not using either pfSense or a Synology, I'm sure these Ansible Tasks could prove useful in your particular situation.  Need help?  Feel free to leave and comment!

Shoutout to \[BIT\]arantno and [the discection of the certificate layout on the Synology filesystem](https://dokuwiki.bitaranto.ch/doku.php?id=synologyimportcertfrompfsense).  You saved me a lot of time! 
