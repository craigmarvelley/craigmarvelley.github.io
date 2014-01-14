---
title: 24 hours of Windows
author: Craig
layout: post
permalink: /2011/03/03/24-hours-of-windows/
aktt_notify_twitter:
  - no
categories:
  - PHP
  - PHP on Azure
---
[This is a blog post related to the [PHP on Azure competition][1].]

I&#8217;m sure everyone blogging about this contest will at some point write a post describing their experiences setting up an Azure development environment, but writing two posts a week is hard, so I can&#8217;t pass up an easy topic! Mine won&#8217;t be terribly formal since there are plenty of guides out there that already do that, so: from a clean Windows 7 install, here&#8217;s a minute-by-minute style guide to getting a PHP on Azure development machine configured. I&#8217;m going to try to stay away from as many guides and tutorials as possible to see how intuitive this process is.

**The following takes place between 9.43pm and 01.56am on 02/03 March 2011.**

## 9.43 pm

The previous two hours involved me creating a new hard drive partition alongside my XP install and installing Windows 7 into it.  I&#8217;m using the [free Enterprise trial][2] for the time being. After booting for the first time, I install some Windows updates and reboot. The next thing I do is open Internet Explorer 8, search for Google Chrome and install it. IE&#8217;s come a long way recently, but it&#8217;ll have to go a lot further before I use it as my main browser. I write the intro to this blog post, and that takes us up to where we are now.

## 9.26

I go [here][3] and download the Microsoft Web Platform installer, a neat utility which allows developers to install both products such as IIS and PHP, and web applications like WordPress and Drupal. Looking through the list I remember that Windows 7 (Enterprise edition, at least) comes bundled with IIS, so I think I&#8217;d better install through Windows to avoid confusion.

## 9.31

I go into the add/remove Windows features programs bit in Control Panel and check the Internet Information Services option which installs IIS with the default settings.

## 9.33

I open up IIS Manager, and all seems OK. I hit http://localhost in Chrome and I get the delightful IIS7 landing page. Web server: check. Painless.

[<img class="alignnone size-large wp-image-111" title="IIS7" src="http://marvelley.com/wp-content/uploads/2011/03/IIS7-1024x754.png" alt="The IIS7 landing page." width="640" height="471" />][4]

## 9.38

I think I&#8217;ll add a picture of the IIS7 page since it looks so nice, and it gives me an excuse to try the new Paint application (which I think is a Windows 7 thing, though it may have come with Vista. I&#8217;ll never know). Paint&#8217;s a lot better these days, that&#8217;s for sure.

## 9.40

I run the Web Platform Installer (henceforth WPI) and select the Products tab. There&#8217;s plenty of stuff in there that looks cool, but for now I&#8217;m only going to bother with the essentials, so I choose:

*   SQL Server Express 2008
*   Windows Azure command line tools for PHP (sounds like that&#8217;ll come in handy!)
*   PHP Manager for IIS (I&#8217;ve used this in work, it makes configuring PHP for Windows a breeze)
*   PHP 5.3.5 for WebMatrix (not sure what the WebMatrix bit is about, but it&#8217;s nice to see the latest version of PHP in there)

There&#8217;s a whole bunch of other stuff there that looks like it&#8217;ll come in handy, but the above should get me to a point where I can get a PHP script running so we&#8217;ll start there. I hit install, and see A LOT of dependencies which will also be downloaded. Turns out the PHP 5.3.5 for WebMatrix install is a little bit of PHP, and a whole lot of WebMatrix &#8211; and PHP 5.3.5 is already being downloaded as a dependency of the Windows Azure command line tools. I&#8217;m a little freaked out, and decide to untick the WebMatrix trojan horse and just try installing PHP on its own for now until I discover that I need anything else.

Since I&#8217;m installing SQL Server, I get asked to set a password (I don&#8217;t have to, I could use Windows authentication, but I figure it&#8217;s safer). I choose a suitably fiendish one.

This could take a while, so I go downstairs for a chat with my wife and a cup of tea.

## 22.03

I come back to a screen notifying me that all programmes but SQL Server installed correctly. I open the install log to find out why, and would you believe it &#8211; my password wasn&#8217;t strong enough! Lesson learned. OK, another go, this time with a tougher password. I also add in the SQL Server Management Studio application for working with SQL Server which I&#8217;d missed the first time round.

## 22.16

It&#8217;s taking *ages *to install SQL Server Management Studio, so I go back and rewrite the intro which somehow is in a completely different tense to the rest of the article. I look at the copy of Strunk and White on my desk and realise I need to read more than the 10 pages of it that I&#8217;ve managed to date.

## 22.18

And at that moment, the installer finishes. No error messages this time, which means I&#8217;ve got l33t pa55w0rd skillz. Now to check if PHP is working.

## 22.25

I open up a command prompt and type &#8216;php&#8217; into it. Hit return. Error message &#8211; PHP isn&#8217;t recognised.

[<img class="alignnone size-full wp-image-114" title="PHP not recognised" src="http://marvelley.com/wp-content/uploads/2011/03/php_not_recognised.png" alt="A familiar sight on Windows" width="684" height="351" />][5]

Usually this means that PHP isn&#8217;t in Windows&#8217; PATH, so I probably need to do that. Hmm. Where&#8217;s the WPI put PHP? I find it under Program Files. Add that to the end of the path variable. Restart the cmd prompt. PHP is now responding, and the version is listed as 5.3.5. Fantastic.

[<img class="alignnone size-full wp-image-115" title="PHP - Recognised!" src="http://marvelley.com/wp-content/uploads/2011/03/php_recognised.png" alt="That's better." width="693" height="355" />][6]

## 22.38

I&#8217;m curious as to what modules come bundled with PHP when it&#8217;s installed via the WPI, so I&#8217;m going to check that out. I could do it through the command line with the -m switch but I also want to check the PHP manager for IIS is running, and configure PHP for IIS at the same time.

I open up IIS and select the default web site, then select the PHP Manager module. It tells me that my PHP configuration isn&#8217;t correct, and offers to set the default document for the website to index.php and monitor my php.ini file for changes, both of which are helpful suggestions. I do both. IIS seems to have picked up the correct version of PHP, so all is well in that regard.

## 22.43

The default web site is pointing to C:\inetpub\wwwroot, and it&#8217;s got some random stuff in it. I delete both the default web site and the files, then create a new site. I create a new one called &#8216;localhost&#8217; and set it to respond to &#8216;localhost&#8217;. I try to add PHP file called index.php which outputs phpinfo(), but I don&#8217;t have administrator rights for this folder. Grr. I add myself with read / write permissions, and save the file successfully.

## 22.49

I hit http://localhost in the browser, and wow &#8211; it&#8217;s working. The PHP interpreter, FastCGI as the SAPI &#8211; and all with pretty much zero configuration. Take it from someone who spent a good few evenings last year building a LAMP server from source and configuring PHP in Apache &#8211; this is impressive. OK, so I&#8217;ve done a lot of this before, but having the WPI take a lot of the grunt work away is so helpful. Also I always have to check which version of PHP I need on Windows &#8211; is it non-thread-safe? Thread-safe? VC6? VC9? It&#8217;s nice having all that uncertainty taken away.

[<img class="alignnone size-large wp-image-117" title="phpinfo" src="http://marvelley.com/wp-content/uploads/2011/03/phpinfo-1024x574.png" alt="The PHPInfo page, courtesy IIS" width="640" height="358" />][7]

I take a look at the modules list. The usual suspects, nothing too fancy. I&#8217;m surprised to see that the Microsoft SQL Server Driver for PHP isn&#8217;t on there, I assumed that would be bundled. I think I saw it in the WPI, actually. I&#8217;ve a few can&#8217;t-live-without modules like PECL HTTP and XDebug that I&#8217;ll have to add in due course.

## 22.59

OK, it&#8217;s getting late &#8211; time to wrap this up. I need to find a &#8216;my first Azure app&#8217; tutorial on the web and make sure I can run it.

It doesn&#8217;t take much Googling to come across [this article][8], which seems to be exactly what I&#8217;m looking for. I&#8217;m not too bothered about deploying to the cloud just yet, I just want to make sure I can develop on my local machine for now.

I seem to have covered the first few steps already (they&#8217;re concerned with the Azure command line tools for PHP which I installed via the WPI earlier &#8211; that article could do with an update to notify others in a similar position), so I skip on and open up the Azure SDK command prompt.

## 23.23

I keep following the steps, successfully creating a file and a temporary project. I come to packaging the project with the package.php script, and deploying to DevFabric, and get the following error:

> Runtime Exception: 0: Default document &#8220;ServiceDefinition.rd&#8221; does not exist in Service directory &#8220;ServiceDefinition.csx&#8221;!

No idea. Google tells me nothing. Maybe I missed something in the earlier part of the tutorial.

<img class="alignnone size-full wp-image-118" title="Runtime Exception" src="http://marvelley.com/wp-content/uploads/2011/03/uhoh.png" alt="Runtime Exception: 0: Default document “ServiceDefinition.rd” does not exist in Service directory “ServiceDefinition.csx”!" width="693" height="355" />

## 23.27

OK, looks like I might have needed to start the Compute Emulator. Let&#8217;s try that&#8230; Oh, and the Storage Emulator too.

## 23.29

Nope, that doesn&#8217;t fix it. I&#8217;d better re-read through everything in case I missed something.

## 23.42

I read through the package script code to see where things are going wrong. I see quickly enough where it attempts to reference the missing file, leading to the exception, but there doesn&#8217;t appear to be a point where the file is actually created. Is it supposed to be copied from somewhere? I can&#8217;t see anything obvious and there&#8217;s nothing on Google that mentions what that file is or where it comes from.

This isn&#8217;t good. My ass is nowhere near Vegas at the moment!

## 01.56

I&#8217;m totally out of ideas, and I&#8217;m not above begging for help, so I contact [Maarten Balliauw][9] (who has published a lot of material on PHP on Azure) [via][10] [Twitter][11] to see if he&#8217;s seen the error before and can point me in the right direction. He kindly offers to put me in touch with someone involved in creating the tools, and in the middle of [MVP 2011][12] festivities too!

## 02.11

Since I&#8217;ve followed the instructions in the articles to the letter, I&#8217;m wondering if Windows is to blame. I&#8217;m noticing other weird behaviour on my machine. Windows suggests folders to me in the command line that don&#8217;t exist; it&#8217;s been using my external hard drive to store installers from WPI; when I try to restart my machine to see if that&#8217;ll cure the problem it tries, and fails, to install Windows updates. Perhaps running Windows on a partition alongside XP wasn&#8217;t such a good idea after all. I decide enough&#8217;s enough, and go to bed frustrated.

## The Next Day

Despite having slept on it and coming back fresh I&#8217;m still having the same problems, and am less confident in my installation in general. It&#8217;s possible there may be a bug in the Azure tooling, but given I&#8217;m having other issues I think the best thing to do is to take the plunge and install Windows 7 onto a dedicated drive, in case there are conflicts arising from sharing one with XP (I don&#8217;t see how that could be the case, but strange things are definitely happening).

I&#8217;m a little disappointed because things seemed to be going very smoothly right up until the last hurdle. The WPI, with its dependency management, makes it so easy &#8211; I&#8217;ve since learned I need only to have installed the Azure Command Line Tools for PHP to have got everything else automatically, which is neat.

So I now face my second install of Windows 7 in 24 hours &#8211; a task I think even Jack Bauer would blanch at <img src='http://marvelley.com/wp-includes/images/smilies/icon_smile.gif' alt=':-)' class='wp-smiley' /> 

I&#8217;d like to thank Maarten for helping me out when I was seriously fed up. Hopefully after a re-install this problem will go away and I can finally start developing. Fingers crossed!

 [1]: http://www.phpazurecontest.com/
 [2]: http://technet.microsoft.com/en-us/evalcenter/cc442495
 [3]: http://www.microsoft.com/web/downloads/platform.aspx
 [4]: http://marvelley.com/wp-content/uploads/2011/03/IIS7.png
 [5]: http://marvelley.com/wp-content/uploads/2011/03/php_not_recognised.png
 [6]: http://marvelley.com/wp-content/uploads/2011/03/php_recognised.png
 [7]: http://marvelley.com/wp-content/uploads/2011/03/phpinfo.png
 [8]: http://azurephp.interoperabilitybridges.com/articles/deploying-your-first-php-application-with-the-windows-azure-command-line-tools-for-php
 [9]: http://blog.maartenballiauw.be/
 [10]: http://twitter.com/#!/craigmarvelley/status/43101712755605504
 [11]: http://twitter.com/#!/craigmarvelley/status/43101994981924864
 [12]: http://www.2011mvpsummit.com/