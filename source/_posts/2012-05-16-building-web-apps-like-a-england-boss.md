---
title: Building web apps like a (England) boss.
author: Craig
layout: post
permalink: /2012/05/16/building-web-apps-like-a-england-boss/
aktt_notify_twitter:
  - no
categories:
  - General
---
If you think app development and football have nothing in common, read on.

There was a discussion on our IRC server at work this morning which centred on how to best mitigate the risk involved with using third party tools in web applications. Not just at the code level, as in a JavaScript library like [jQuery][1], or a PHP framework like [Symfony2][2], but right through the stack &#8211; from the OS, to the web server, to the app codebase and beyond.

Much of the discussion was along the lines of what you&#8217;d expect when devops (or sysadmins) and developers collide &#8211; those responsible for managing the stack want things that can be easily automated, are verifiable (ideally through something like checksums) and reliable (i.e. not placed directly on a production server from a Pentium 3 machine in some teenager&#8217;s bedroom half way round the world), while those responsible for writing the code want to be able to use the best tool for the job, whether it be a tried and trusted web server or the newest, shiniest Symfony2 bundle.

The general consensus was that both have equal importance. Personally, I think that depending on the nature of the app, it&#8217;s wise to proportion risk accordingly; an app with a USP centred around some novel, interactive UX may want to incorporate a new innovative JavaScript toolkit even if it&#8217;s yet to reach version 1.0, whereas an app with paramount speed and scalability requirements might want to try [PHP-FPM with nginx][3] in place of a more familiar solution like mod-php with Apache.

In isolation, either of these decisions probably wouldn&#8217;t pose a problem. Combining many such scenarios, though, may eventually load the project with enough risk as to eventually make it untenable. The holy grail is to arrive at a point where we have an app that delivers its required functionality while making use of as many trusted, reliable tools as possible, and can be managed in such a way as to make deployment and maintenance safe and simple.

Now, to the title of this post. While this discussion was raging in IRC, there was much furore over the [selection of the provisional England squad][4] for the Euro 2012 tournament. It occurred to me that the new England manager, Roy Hodgson, is facing many of the same challenges myself and my coworkers face when trying to decide on a strategy for selecting the players he thinks will combine to great effect in a few month&#8217;s time. He wants a team that blends reliable, experienced, mature players with younger, modern ones &#8211; with maybe a sprinkling of unpredictable, yet highly creative, firebrands that can make the difference between a good squad and a great one. This is essentially what I was trying to articulate in the conversation, but swapping players for libraries, or tools, written by myself, or by others.

So when I was scanning the list of players that are going to Poland and the Ukraine this summer, I couldn&#8217;t help but think of them in a technical fashion. For example:

*   John Terry (Defender) &#8211; Very experienced, but can be unreliable and prone to catastrophic behaviour. (Windows OS &#8211; ever tried hosting a PHP app on Windows?).
*   Alex Oxlade-Chamberlain (Midfielder) &#8211; New kid on the block, has a speciality that offers a new dimension (see: nginx and content distribution networks)
*   Stuart Downing (Midfielder) &#8211; Does what he does and does it well enough, but isn&#8217;t going to make a massive difference overall. Comes with baggage and divides opinion. (CodeIgniter/CakePHP/any other technically limited PHP framework)
*   Wayne Rooney &#8211; Best of breed, unrivalled, links up with others very well, difficult to replicate or replace (jQuery)

It&#8217;s a popular argument at the moment that more people should be aware of, and be able to, code. But perhaps we&#8217;re missing a trick &#8211; perhaps a few games of [Football Manager][5] is all it takes to be able to understand how to compose a fabulous web app these days.

 [1]: http://jquery.com/
 [2]: http://symfony.com/
 [3]: http://blog.digitalstruct.com/2010/07/12/getting-started-with-nginx-and-php-fpm/
 [4]: http://www.guardian.co.uk/football/2012/may/16/euro-2012-england-squad-announcement-live
 [5]: http://www.footballmanager.com/