---
title: DOMPDF and the mbstring extension
author: Craig
layout: post
permalink: /2010/10/13/dompdf-and-the-mbstring-extension/
categories:
  - PHP
---
I&#8217;ve been using [DOMPDF][1] for a while &#8211; it&#8217;s a great tool for converting HTML to PDF through PHP. I&#8217;ve been running it locally on several machines without issue, but I recently deployed it to a server running Centos 5.5 and was greeted with a blank page with no output every time I tried to generate a file. No errors on screen, no errors in the log file &#8211; and no way to step through the code.

After a painful couple of hours of old-school echo()-ing I noticed a call to one of the mb_* functions &#8211; PHP&#8217;s set of functions for dealing with [multibyte strings][2]. I don&#8217;t use that extension in my application, and DOMPDF doesn&#8217;t mention it in its installation notes along with its other dependencies, so I hadn&#8217;t thought I&#8217;d need it. A quick configure / make later though, and with the mbstring extension enabled PDFs were rendering quite happily.

 [1]: http://www.digitaljunkies.ca/dompdf/
 [2]: http://uk.php.net/mb_string