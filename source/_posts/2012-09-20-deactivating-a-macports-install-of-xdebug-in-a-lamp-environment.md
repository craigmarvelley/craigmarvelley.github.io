---
title: Deactivating a Macports install of XDebug in a LAMP environment
author: Craig
layout: post
permalink: /2012/09/20/deactivating-a-macports-install-of-xdebug-in-a-lamp-environment/
categories:
  - PHP
---
A few times I&#8217;ve found myself cursing when trying to toggle [XDebug][1] on and off via [Macports][2]. Typically I&#8217;ll be debugging with it enabled, then disable it for development/testing to get the fastest experience possible (it tends to really impact performance on large codebases, such as a Symfony2 standard install), only to experience segfaults when I refresh the page I&#8217;m working on.

The solution I&#8217;ve found is when restarting Apache (which is necessary for the change to PHP&#8217;s installed modules takes effect), to use an explicit start/stop rather than a restart. [According to the Apache docs][3] restarting only kills off children processes, so the parent remains running:

> Sending the `HUP` or `restart` signal to the parent causes it to kill off its children like in `TERM`, but the parent doesn&#8217;t exit. It re-reads its configuration files, and re-opens any log files. Then it spawns a new set of children and continues serving hits.

I imagine this leading to a discrepancy in the loaded PHP modules, which causes the issue.

So when wanting to toggle XDebug, I use these commands:

<pre>Install (first time only):
sudo port install php5-xdebug

Disable:
sudo port deactivate php5-xdebug
sudo apachectl stop
sudo apachectl start

Enable:
sudo port activate php5-xdebug
sudo apachectl stop
sudo apachectl start</pre>

 [1]: http://xdebug.org/
 [2]: http://www.macports.org/
 [3]: http://httpd.apache.org/docs/2.2/stopping.html