---
title: Planning my Azure application (Part 1)
author: Craig
layout: post
permalink: /2011/02/25/planning-my-azure-application-part-1/
aktt_notify_twitter:
  - no
categories:
  - PHP
  - PHP on Azure
---
[This is a blog post related to the [PHP on Azure competition][1].]

I&#8217;ve had some time to think about how I&#8217;m going to build the application, and I&#8217;ve got some ideas for how I&#8217;d like to proceed. At this point I&#8217;d have liked to set my development environment up with the Azure tools and had a play with the example applications I&#8217;ve come across, mostly to get a feel for what&#8217;s possible, but unfortunately upon trying to install the [Azure SDK][2] I discovered that it requires Windows Vista or 7, and at home I&#8217;m still running XP. I toyed with the idea of installing Windows 7 into a Virtual Machine, which would probably be the quickest route to get back on track, but since I have been intending to migrate to 7 for a while this is probably the right time; technology is obviously evolving beyond XP (finally!).

So in the interim while I work on an upgrade I&#8217;ll start planning my CMS application. I&#8217;ve been thinking about the type of libraries and frameworks I want to take advantage of, and how I&#8217;m going to knit them together. I won&#8217;t be able to check they work on Windows Azure &#8217;til I get access to a machine, but I&#8217;m fairly confident that the vast majority, if not all of them, will work on the platform.

Firstly I&#8217;ll be using Zend Framework to provide the backbone of the application. I&#8217;ve not yet decided how much of the framework I&#8217;ll be taking advantage of, but I&#8217;ll definitely be using [Zend_Application][3] and its related classes to handle the bootstrapping phase of the application, because its flexibility will be key when loading the other libraries I intend to use. The application will then utilise the ubiquitous [MVC][4] pattern, using the following components:

*   Model: [Doctrine 2 ORM][5] / [Windows Azure Table Storage][6]
*   View: Not sure yet, probably [Zend_View][7] but needs more investigation
*   Controller: [Zend_Controller][8]

As I mentioned in my last post I don&#8217;t yet know how I&#8217;m going to work with the data layer: I really want to use Doctrine 2, which I know has SQL Server (and thus, I&#8217;m assuming, SQL Azure) support, but I&#8217;m not aware of similar support for Table Storage. Brian Swan posted [a tutorial][9] where he uses the OAuth SDK to access Table Storage, and that follows a similar annotations-driven approach to Doctrine 2; if one doesn&#8217;t exist, I&#8217;m wondering how much work it would take to write a Table Storage driver for Doctrine.

Functionally, it may be possible to use Table Storage exclusively within the app ([it sounds like it&#8217;ll be cheaper][10]) but there appear to be some crucial missing features, like [full-text searching][11]. I&#8217;ve been spoiled working with Solr for the past few years; I&#8217;d like to use Solr here, but have read [conflicting][12] [reports][13] as to whether it&#8217;s possible. The way things are looking, I&#8217;ll try to use Table Storage in the first instance, then fall back to SQL Azure if it doesn&#8217;t give me what I need.

For the view / templating component I&#8217;ll probably take the path of least resistance, which will probably mean Zend_View. My main requirement is easy support for different RESTful response response formats, i.e. HTML, XML and JSON, especially since I intend for the backend of the app to be JavaScript-heavy (using [ExtJS 4][14]) which will mean a lot of JSON.

Zend&#8217;s Controller classes are great, and I&#8217;ll probably use their routing system as well since it has RESTful support. There&#8217;s not much more to say about that really!

So in an ideal world, this is how the application will be laid out:

[<img class="alignnone size-full wp-image-100" title="Application Architecture Overview" src="http://marvelley.com/wp-content/uploads/2011/02/application_overview.jpg" alt="An overview of the application architecture" width="500" height="647" />][15]

Next I&#8217;ll think in more detail about the frontend and backend applications. Now I have to go to PC World to buy a hard drive and a copy of Windows 7&#8230;

 [1]: http://www.phpazurecontest.com/
 [2]: http://msdn.microsoft.com/en-us/windowsazure/cc974146.aspx
 [3]: http://framework.zend.com/manual/en/zend.application.html
 [4]: http://msdn.microsoft.com/en-us/library/ff649643.aspx
 [5]: http://www.doctrine-project.org/projects/orm
 [6]: http://msdn.microsoft.com/en-us/library/dd179423.aspx
 [7]: http://framework.zend.com/manual/en/zend.view.html
 [8]: http://framework.zend.com/manual/en/zend.controller.html
 [9]: http://blogs.msdn.com/b/brian_swan/archive/2010/09/16/accessing-windows-azure-table-data-as-odata-via-php.aspx
 [10]: http://www.intertech.com/Blog/post/Windows-Azure-Table-Storage-vs-Windows-SQL-Azure.aspx
 [11]: http://www.mygreatwindowsazureidea.com/forums/34192-windows-azure-feature-voting/suggestions/396315-provide-me-with-full-text-search-on-table-storage
 [12]: http://social.msdn.microsoft.com/Forums/en-US/windowsazuredevelopment/thread/ab80b97f-462b-4b7d-bd65-f484e65be30c/
 [13]: http://stackoverflow.com/questions/3846793/running-solr-on-azure
 [14]: http://www.sencha.com/blog/ext-js-4-preview-faster-easier-more-stable
 [15]: http://marvelley.com/wp-content/uploads/2011/02/application_overview.jpg