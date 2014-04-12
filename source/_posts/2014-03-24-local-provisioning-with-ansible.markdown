---
layout: post
title: "Local Provisioning With Ansible"
date: 2014-04-11 21:24:00 +0000
comments: true
categories: ansible, provisioning
---

I recently [mentioned](http://marvelley.com/blog/2014/03/18/vagrant-1-dot-5-syncing-situation/)
I'm going all-in on provisioning and running all my development
environments in VMs provisioned with Ansible. My Ansible use doesn't end there though -
I'm also using it to provision my MacBook.

I'd read of a few other people doing this - Benjamin Eberlei has a particularly
[good post](http://whitewashing.de/2013/11/19/setting_up_development_machines_ansible_edition.html)
on the topic, and was pretty much the inspiration for me doing the
same. Setting up a new machine can be a bit of a bore, and while in theory it
only happens whenever I upgrade hardware I have been caught out in the past with kernel
corruption forcing a reinstall, and I'd like
to minimise the hassle should it ever happen again. I have [backups](http://backblaze.com)
, but one of the few upsides of going back to scratch with a machine is that it's an
opportunity for spring clean; a script that effectively lists all the essential
components of my computer, and configures them to my taste, makes that so much easier.

Anyway. A couple of people mentioned they'd be interested in the playbooks I wrote
to provision my laptop, so I've taken out anything personal to me and [mirrored them
on Github](https://github.com/craigmarvelley/macbook-provisioning).

Currently the provisioning involves four things:

- Install Homebrew and various brews
- Install Homebrew Casks and various casks
- Enable zsh as default shell and install oh-my-zsh
- Install dotfiles to configure git, vim, etc. (my dotfiles repo is [here](https://github.com/craigmarvelley/dotfiles))

It's all straightforward, but a couple of implementation details:

- I've ended up using Alfred as my OS X search tool because I store my casks under `/usr/local`
with the other brew stuff and symlink to /Applications, and Spotlight doesn't
grok symlinks. Instead I configure Alfred to link in the cask files
- I read on a few places on the web that the method I use to determine my current shell
process - `echo $SHELL` - isn't foolproof. Works for me, but YMMV

There's more I could do in terms of what I manage, especially when it comes to
dotfile configuration (incidentally one of the best things about automating
provisioning in this way is you end up looking at other people's approaches,
and finding out about libraries and tools that you never even knew existed - [Thoughtbot's rcm](http://robots.thoughtbot.com/rcm-for-rc-files-in-dotfiles-repos)
is one such example here).
Also I'm still finding my way with Ansible, so my playbooks can undoubtedly be improved, especially
when it comes to idempotency.
Nevertheless I'm really happy to have a record of my machine's starting state, and will enjoy adding to it as time
passes.
