---
title: Learning about Windows Azure
author: Craig
layout: post
permalink: /2011/02/20/learning-about-windows-azure/
aktt_notify_twitter:
  - no
categories:
  - General
  - PHP
  - PHP on Azure
---
[This is a blog post related to the [PHP on Azure competition][1].]

I&#8217;ve spent the last few days reading about Windows Azure, mostly just trying to get a feel for what features it has and how I could use them in an application. The competition rules suggest that entrants &#8220;can earn extra points by using other parts of the Windows Azure platform&#8221; and the more I get to learn, the better, so I&#8217;m going to try to make use of as much of Azure&#8217;s functionality as possible.

Though I haven&#8217;t yet decided what application I&#8217;ll be writing it&#8217;ll probably be some sort of a CMS &#8211; it&#8217;s the genre of web app I&#8217;m most familiar and its likely I&#8217;ll get more done in the short time frame I have if I stick to what I know best. As a result I&#8217;ve been looking at Azure&#8217;s feature list and thinking &#8220;how I can map this platform feature to a feature of a CMS?&#8221;

I found plenty of resources which helped me get an overview of Azure, and which I&#8217;m sure I&#8217;ll continue to use as I progress. The most helpful were:

*   Maarten Balliauw&#8217;s exhaustive [Sitepoint article][2]
*   [Josh Holmes&#8217; blog][3] (plenty of posts concerning PHP on Azure)
*   [Brian Swan&#8217;s blog][4] (loads of good Microsoft/PHP content, including lots of Azure-related posts)

The Sitepoint article does a great job of summarising what Azure offers a PHP developer. As I was reading it I kept thinking &#8220;Ooh, that&#8217;d come in handy for this&#8221; or &#8220;That&#8217;d make so-and-so easy&#8230;&#8221; &#8211; here&#8217;s my reaction to some of the topics covered in the article.

## Platform as a Service

The article starts by explaining that unlike, for example, Amazon&#8217;s EC2, which is an example of Infrastucture-as-a-Service, Windows Azure is a Platform-as-a-service. This essentially means that a developer using Azure doesn&#8217;t need to worry about maintaining the server, and just has to focus on deploying and configuring the applications that run on it. This sounds good to me; while my experiences of EC2 have been mostly good, there is a lot of work involved with getting servers into a state where they are usable. This can be mitigated somewhat by creating build scripts, but even then these have to be maintained, while managing server security is another headache that I&#8217;d be glad to be rid of. I&#8217;m optimistic that Azure will prove itself to be very hospitable, though I suppose there&#8217;s a chance that it&#8217;ll be too inflexible for more demanding applications that require atypical server configurations.

## Blobs, Tables and Queues (oh my&#8230;)

Judging by how often they&#8217;re mentioned in the articles I&#8217;ve read, these three features seem to be what Microsoft deem the most valuable. All three will play their part in a highly scalable application, which is one of the advantages of the platform. Blobs can be leveraged to provide resources (images, downloads and the like) through a [Content Delivery Network][5], accessed via a REST API &#8211; this is very relevant to a CMS, so I&#8217;ll definitely be taking advantage of this feature.

Table storage is a document-oriented non-relational database in the same vein as [MongoDB][6] or [CouchDB][7]. While I imagine the application will use relational databases, hopefully there will be an opportunity to use Table storage; perhaps to hold the content itself. I don&#8217;t have a lot of experience with this type of database so it&#8217;ll be a good chance for me to learn something.

Queues are very exciting; a built-in way to pass processor-heavy tasks off to worker machines. I can immediately think of a few ways a CMS could make use of this feature: generating PDFs of pages; creating ZIP files of multiple downloads; analysing uploaded files for automated tagging and classification; computing internal analytics&#8230; there are plenty of scenarios where queuing could be invaluable. This feature interests me the most.

## SQL Azure

Microsoft have provided SQL Server support, albeit in a modified fashion, through SQL Azure. I&#8217;ve used SQL Server frequently over the last 4 years but have always preferred to use MySQL since until recently it&#8217;s been better supported by PHP through both highly maintained PDO drivers, and the mysqli client library. That has changed in the last year or so with [Microsoft&#8217;s SQL Server Driver for PHP][8], and this will be my first chance to make use of that driver. It&#8217;s likely that I&#8217;ll employ Doctrine 2&#8242;s [database abstraction layer][9] since it has support for the driver, and it&#8217;ll make my application more portable in future &#8211; plus I&#8217;ve been looking for an excuse to put Doctrine 2 through its paces, having used Doctrine 1 extensively.

## Windows Azure Platform Appfabric

Appfabric is a substantial element, comprising many components including Access Control, Caching, and Service Bus, which allows applications and services to communicate even through restrictive firewalls. Access control is a way to perform user authentication through federated identity services such as Active Directory, Microsoft Live, Yahoo!, Facebook and Google, which will be useful to web 2.0 style social applications that often delegate user identification. If it&#8217;s straightforward enough to do (and Microsoft say that it is) I may manage user authentication in this way; the web certainly doesn&#8217;t need another authentication device.

I&#8217;m unclear as to whether the caching system can currently be used; [this article][10] mentions only .NET applications, and suggests that it is only available for preview, which is a shame. If it isn&#8217;t, then there are other options available for caching &#8211; simple file-based caching, which will probably be too slow (and isn&#8217;t very scalable); the Wincache extension, which uses shared memory, which will be faster; or perhaps I&#8217;ll be able to implement a [Memcached solution][11].

While I think Service Bus is a neat idea, I&#8217;m not sure whether my application will require communication with other network devices &#8211; it seems to be more relevant to applications concerned with restrictive networks.

## Conclusion

I&#8217;ve read plenty about Windows Azure this week, and am quite excited about what it can offer a PHP application; some of the features make it almost too easy to dream up application functionality! Next I need to design my application, and get my development environment set up to work with Azure and its tools.

 [1]: http://www.phpazurecontest.com/
 [2]: http://articles.sitepoint.com/article/windows-azure-php
 [3]: http://www.joshholmes.com/blog/
 [4]: http://blogs.msdn.com/b/brian_swan/
 [5]: http://en.wikipedia.org/wiki/Content_delivery_network
 [6]: http://www.mongodb.org/
 [7]: http://couchdb.apache.org/
 [8]: http://sqlsrvphp.codeplex.com/
 [9]: http://www.doctrine-project.org/projects/dbal
 [10]: http://www.microsoft.com/windowsazure/AppFabric/Overview/default.aspx#top
 [11]: http://archive.msdn.microsoft.com/winazurememcached