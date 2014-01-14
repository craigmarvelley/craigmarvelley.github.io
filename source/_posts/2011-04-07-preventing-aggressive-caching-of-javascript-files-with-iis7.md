---
title: Preventing aggressive caching of JavaScript files with IIS7
author: Craig
layout: post
permalink: /2011/04/07/preventing-aggressive-caching-of-javascript-files-with-iis7/
aktt_notify_twitter:
  - no
categories:
  - IIS
---
I was playing with the new beta of Ext JS 4 the other day and noticed that sometimes the scripts were being cached, so my changes weren&#8217;t taking effect. Initially I thought this was because I&#8217;d upgraded to Firefox 4 &#8211; I use the [Web Developer][1] add-on which allows me to disable browser caching, and I&#8217;d assumed the cache setting had reverted when I upgraded. However the cache was indeed disabled, so I had to dig a little deeper.

It turns out that IIS 7 will automatically cache static resources, such as JavaScript files. While this is probably what you&#8217;d want for a default production environment it almost certainly isn&#8217;t from a development point of view, when changes are being made by the minute. It wasn&#8217;t too hard to turn this feature off, however. To do so, just do the following:

*   Open up IIS Manager
*   Optionally select the site you&#8217;re working with
*   Open the &#8216;Output Caching&#8217; module
*   Select &#8216;Add&#8230;&#8217; from the right hand menu
*   Enter a file extension of &#8216;.js&#8217; and disable both user-mode and kernel-mode caching, click OK.

<div id="attachment_173" class="wp-caption alignnone" style="width: 310px">
  <a href="http://marvelley.com/wp-content/uploads/2011/04/output_caching.png"><img class="size-medium wp-image-173" title="output_caching" src="http://marvelley.com/wp-content/uploads/2011/04/output_caching-300x224.png" alt="" width="300" height="224" /></a><p class="wp-caption-text">
    Select the 'Output Caching' Module
  </p>
</div>

<div id="attachment_174" class="wp-caption alignnone" style="width: 310px">
  <a href="http://marvelley.com/wp-content/uploads/2011/04/add_cache_rule.png"><img class="size-medium wp-image-174" title="Disabling JavaScript caching" src="http://marvelley.com/wp-content/uploads/2011/04/add_cache_rule-300x224.png" alt="Disabling JavaScript caching" width="300" height="224" /></a><p class="wp-caption-text">
    Disabling JavaScript caching
  </p>
</div>

[  
According to the IIS blog][2] IIS should flush the cache when files are modified; however this wasn&#8217;t the behaviour that I was seeing. I had to completely disable caching to guarantee file modifications made it to the browser.

 [1]: https://addons.mozilla.org/en-us/firefox/addon/web-developer/
 [2]: http://blogs.iis.net/bills/archive/2007/05/02/iis7-output-caching-for-dynamic-content-dramatically-speed-up-your-asp-and-php-applications.aspx