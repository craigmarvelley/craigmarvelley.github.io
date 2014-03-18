---
layout: post
title: "Vagrant 1.5 syncing situation"
date: 2014-03-18 09:39:02 +0000
comments: true
categories: vagrant, provisioning
---

![image](/images/posts/2014/03/synchronised.jpg)

When starting work at [BipSync](http://www.bipsync.com) I resolved to put the bits
and bobs I'd learned about provisioning with Vagrant and Ansible into practice, and
no longer host development environments locally on my MacBook. The reasons were
twofold - firstly I wanted my development environment to mirror that
of live as closely as possible, and secondly when previously hosting multiple,
complex projects on one machine I experienced increased battery drain and frequent
slowdowns caused by active background services that I often didn't even need for my current
task. It was a pain to keep track of everything, especially when multiple versions
were required. So the attraction of having dev environments I could bring up and down, and if
necessary occasionally trash, was a strong one.

I'd played with Vagrant / VirtualBox hosted projects on smallish codebases before,
where the default VirtualBox synced folder support was sufficient; however when
attempting to host and develop BipSync's sizeable applications it was quickly clear
that this combination wouldn't be fast enough to be fit for purpose.

Since VirtualBox has been [acknowledged](http://puppetlabs.com/blog/new-vmware-provider-gives-vagrant-a-boost)
as the slowest of Vagrant's provider options, and we already had Parallels
licences for the development of our Windows applications, next I tried out the
third party [Parallels plugin for Vagrant](https://github.com/Parallels/vagrant-parallels).
Basically this was a non-starter - I immediately ran into bugs that were present in the project's
issue tracker, and the impression I got was that the plugin is still a work-in-progress.
The plugin is overseen by Parallels so I'm optimistic that it'll one day be a
first-class provider, but as it was it was unusable.

So I went back to VirtualBox (VMWare was another option but before forking out money on the
software and accompanying plugin I wanted to exhaust all other options) and tried the other
synced folder types. First I tried the new rsync support, which I'd [read good things
about](https://www.vagrantup.com/blog/feature-preview-vagrant-1-5-rsync.html). In terms of speed this was very quick because there isn't really a share to speak
of; shared items are copied to the guest rather than mounted. It requires a command
to be run constantly, to watch synced files for changes and copy them to the guest, and
this proved to be a problem; as [issues raised](https://github.com/mitchellh/vagrant/issues/3249)
by others attest, the approach wasn't scaling to large (20k+ files) codebases, which
is common in my experience. I tried excluding some folders to see if that would help,
but it didn't.

So after all that I ended up using the NFS sync option, which aside from requiring
a password for sudo when booting the VM has proved trouble free, so far. Performance
is good, both in terms of the applications themselves, and when browsing and modifying files
in the share; I've seen PHPStorm occasionally lock up but then it always has ;) It's
certainly good enough to work with now, and I'll be keeping an eye on the rsync and Parallels
options as they should improve in time.

("Moonlight Synchro" image courtesy of [Chris Phutully](http://www.flickr.com/photos/72562013@N06/12765457844/). [See license](https://creativecommons.org/licenses/by/2.0/).)
