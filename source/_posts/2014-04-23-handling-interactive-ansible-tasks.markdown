---
layout: post
title: "Handling interactive Ansible tasks"
date: 2014-04-23 09:40:10 +0000
comments: true
categories: ansible
---

I recently re-ran some Ansible provisioning scripts after upgrading the
base box to an Ubuntu 14.04 image and found they stalled midway through. The cause? One
task involved installing the PECL mongo module, and the installation process now prompts
the user to decide whether or not to build with Cyrus SASL support. I couldn't see a way to force
a decision via the PECL installer, and Ansible can't
respond to the prompt, so the provisioning process hung while awaiting an answer.

I found two ways to solve this.

## I've been expecting you

I did a bit of Googling and after coming across [this post](https://groups.google.com/forum/#!topic/ansible-project/pMy2VWgkQ1s)
on the Ansible forum, I took a look at [expect](http://linux.die.net/man/1/expect). Expect lets you
script interactions with a spawned command, using regex to match against prompt text, and send
appropriate responses. It's a sound approach; I wrote a script that looked like this:

```
#!/usr/bin/expect

spawn pecl install mongo

expect "Build with Cyrus SASL"
send "\r"

expect eof
```

And executed it on the box using Ansible's `script` module:

```
- name: Install PECL mongo extension
  script: install_pecl_mongo.expect
```

Mission achieved. I felt very pleased with myself for about 30 seconds, which is
how long it took for Paul to wander over and tell me there was a simpler way to do it.
Expect is a really good solution for scripting varied or complex responses, but I wasn't
faced with that problem here...

## Yes man

In this specific case, all I wanted to do was answer a prompt which needed a yes or no
answer, and I wasn't concerned which I went with. There's a linux command
called [yes](http://en.wikipedia.org/wiki/Yes_(Unix) which "outputs an affirmative response,
or a user-defined string of text continuously until killed", which is just what I needed.

So now my task looks like this:

```
- name: Install PECL mongo extension
  shell: yes '' | pecl install mongo
```

Which continuously pipes the 'y' character (by default) and a newline character into
the install command, automatically causing any prompts to be responded to in the
affirmative. For my simple use case it works perfectly, and is more straightforward than
writing expect scripts.
