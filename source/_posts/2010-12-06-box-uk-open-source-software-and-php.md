---
title: Box UK, Open Source Software and PHP
author: Craig
layout: post
permalink: /2010/12/06/box-uk-open-source-software-and-php/
aktt_notify_twitter:
  - no
categories:
  - PHP
---
Over the last couple of weeks I&#8217;ve been involved in a new initiative at [Box UK][1] to [package and release some of our code under an open source license][2]. This decision stemmed from some conversations I had with fellow developers at the PHPNW 2010 conference,  specifically relating to dependency injection and how it can be useful in larger PHP applications. People seemed interested in the DI container solution developed for [Amaxus][3] using features introduced to PHP in the 5.3 release, so we decided to make both that and a thumbnailing library available to the wider community in the hope that they may prove useful.

More can be read about boxuk-di, the dependency injection library, [on this page][4]. The article outlines some of the nifty features of the library, such as using reflection to achieve automatic dependency resolution, doing away with the configuration files commonly found in DI solutions. The [code][5] itself is available at [BoxUK&#8217;s github][6] page. It&#8217;s pretty cool, and makes creating objects with loads of dependencies a breeze.

The second library, Obscura, is a wrapper for [PHP&#8217;s GD library][7] that aims to make it easy to do image thumbnailing using an object oriented approach. I wrote the library earlier in the year, and it&#8217;s currently used in the Amaxus CMS. It&#8217;s still in its infancy, and there&#8217;s plenty I hope to add to it in the near future (like cropping and watermarking) but as a simple thumbnailer it does the job. I don&#8217;t know of too many thumbnailers for PHP with such a permissive license, which was the driving force behind my desire to write this one. More details can be found at [Box UK&#8217;s website][8], while again the [code][9] can be found at the [company&#8217;s github repository][6].

Hopefully there&#8217;ll be more to come if these initial releases prove successful. I&#8217;m glad to have been involved in the project, as it&#8217;s helped alleviate some of my guilt at using so many excellent open source tools but, until now, not giving anything back. I&#8217;m aiming to release some of my own code in a similar fashion in the near future.

 [1]: http://boxuk.com
 [2]: http://www.boxuk.com/news/announcing-box-uk-open-source-software-libraries
 [3]: http://amaxus.com
 [4]: http://www.boxuk.com/labs/dependency-injection-and-reflection-library
 [5]: http://github.com/boxuk/boxuk-di
 [6]: http://github.com/boxuk
 [7]: http://php.net/gd
 [8]: http://www.boxuk.com/labs/obscura,-the-php-thumbnail-library
 [9]: http://github.com/boxuk/obscura