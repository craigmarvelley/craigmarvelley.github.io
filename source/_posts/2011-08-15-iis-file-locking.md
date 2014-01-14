---
title: IIS file locking
author: Craig
layout: post
permalink: /2011/08/15/iis-file-locking/
aktt_notify_twitter:
  - no
categories:
  - General
  - IIS
tags:
  - IIS
---
This issue has bitten me so many times I&#8217;m going to document it here so hopefully I&#8217;ll remember it in future. Now and then, when deleting files using Windows Explorer, random files would fail an access check even though I&#8217;m the system administrator. [Unlocker][1] reported no locks on the file, but it wouldn&#8217;t let me delete it either. The only way I could get around it was a restart.

This got annoying so the next time it happened I started shutting down all my running programmes one by one and retrying the delete, until I discovered that it was in fact IIS that was causing the lock &#8211; even though the files weren&#8217;t web accessible. Turning off the webserver was enough to allow the files to be deleted.

 [1]: http://www.emptyloop.com/unlocker/