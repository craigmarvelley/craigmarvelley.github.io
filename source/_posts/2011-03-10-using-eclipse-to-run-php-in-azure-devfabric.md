---
title: Using Eclipse to run PHP in Azure DevFabric
author: Craig
layout: post
permalink: /2011/03/10/using-eclipse-to-run-php-in-azure-devfabric/
aktt_notify_twitter:
  - no
categories:
  - PHP
  - PHP on Azure
---
[This is a blog post related to the [PHP on Azure competition][1].]

As detailed in [my last blog post][2] I had some&#8230; problems getting a PHP/Azure development environment set up after creating a Windows 7 partition. Well, I scrapped the partition, said goodbye to my old XP OS and started afresh, and that looks to have done the trick &#8211; I&#8217;m finally able to deploy PHP applications to development storage on my local machine. I&#8217;m none the wiser as to why it didn&#8217;t work the first time, which is annoying, but at least it&#8217;s working now.

After I reinstalled Windows 7 I took care to install all the automatic updates before I went near any other programmes. After a lot of rebooting I eventually installed IIS and, through the Web Platform Installer, the Azure SDK and the Azure command line tools for PHP, along with their dependencies. Then, I installed [Eclipse PDT][3] and, following [this excellent article][4], the Azure plugin for eclipse that Brian Swan wrote a [great tutorial on][5].

I came across a few issues while doing all this that I should detail:

*   I had to set Eclipse to run as an administrator (right click eclipse.exe-> properties -> Compatibility -> Run as administrator) before it would install the plugin and allow me to use it within the application
*   I signed up for the [free introductory trial][6] of Azure so that I could follow the tutorial properly and configure a database on Azure

It&#8217;s a bit annoying that even when developing an app one has to run against SQL Azure in the cloud (which will eventually incur costs). I&#8217;d assumed I&#8217;d be able to use SQL Server locally but that doesn&#8217;t seem to be the case. Some sort of free quota for use in the development stage would make sense to me.

The really good thing about using the Eclipse plugin is that it brings together the [many][7] [disparate][8] [projects][9] that one needs to leverage to work with PHP on Azure. When I was trying to install all this stuff on my own I got a bit muddled, especially since some of the libraries are installed through the Web Platform Installer. The other advantage of the plugin is one can deploy to the cloud from within Eclipse. I&#8217;m not a fan of the Eclipse platform but I have to say in this case it&#8217;s a good experience (especially since the alternative is the command line!).

If I&#8217;ve one criticism of the documentation Microsoft provide (which is generally well-written and thorough) it&#8217;s that there&#8217;s no &#8216;official&#8217; site for PHP on Azure which gives a simple one-page overview of everything &#8211; after reading about this stuff for over two weeks I still don&#8217;t feel like I&#8217;ve grokked it, and without blogs like [Brian&#8217;s][10] and [Maarten&#8217;s][11] I&#8217;d be struggling. As a PHP developer I&#8217;m used to the awesome PHP manual and its direct approach to documentation and perhaps Azure (as far as PHP is concerned) could do with something similar. For developers like me, who are new to Azure and trying to get up to speed quickly in a short space of time (and with little time to read around) that sort of resource would be invaluable.

For the moment though I&#8217;m just happy that I can finally start developing my application. It&#8217;s been a frustrating week battling to get to the point where I can just write a line of code, but from here on in hopefully it&#8217;ll be worth it.

 [1]: http://www.phpazurecontest.com/
 [2]: http://marvelley.com/2011/03/03/24-hours-of-windows/
 [3]: http://www.eclipse.org/pdt/
 [4]: http://www.windowsazure4e.org/download/
 [5]: http://blogs.iis.net/bswan/archive/2010/10/12/using-the-windows-azure-tools-for-eclipse-with-php.aspx
 [6]: http://www.microsoft.com/windowsazure/free-trial/default.aspx
 [7]: http://phpazure.codeplex.com/
 [8]: http://phpazurecontrib.codeplex.com/
 [9]: http://www.interoperabilitybridges.com/projects/windows-azure-command-line-tools-for-php
 [10]: http://blogs.msdn.com/b/brian_swan/
 [11]: http://blog.maartenballiauw.be/