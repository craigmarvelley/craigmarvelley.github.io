---
title: Including filtered thumbnail data with the WordPress JSON API plugin
author: Craig
layout: post
permalink: /2013/09/26/including-filtered-thumbnail-data-with-the-wordpress-json-api-plugin/
categories:
  - General
  - PHP
---
The [JSON API][1] plugin is a great tool for exposing your WordPress data. I&#8217;ve used it to provide content to a few mobile applications; it&#8217;s well featured and most importantly, quite flexible. If your content providers are happiest using a CMS like WordPress, your project can benefit by allowing them to use the authoring tools they&#8217;re comfortable with while allowing you to easily access the content they&#8217;re creating, either to use directly within your application, or as I tend to do, by exporting the data into another application which then proxies the data to mobile applications. I find the latter approach gives you greater control over features like caching, while making it easier to relate the data to domain models that aren&#8217;t handled by WordPress.

But I digress! This post was conceived because when requesting all posts of a certain type through the plugin, response times were hideously slow. The request I was making looked like this:

http://domain.com/?json=get\_posts&post\_type=artist&count=1000&order=ASC

Reading the documentation for the plugin, I found that it was possible to filter the response to only contain properties that I wanted, which I figured should reduce the amount of work WordPress was having to do:

http://domain.com/?json=get\_posts&post\_type=artist&count=2&order=ASC&include=id,title,content,custom\_fields,thumbnail\_images

This proved to be true, but I hit a snag when trying to include the thumbnail\_images property &#8211; adding it to the CSV of whitelisted fields had no effect. Through trial and error it transpired that including the thumbnail field also has the effect of including the thumbnail, thumbnail\_size, and thumbnail_images fields. The final URL ended up looking like this:

http://domain.com/?json=get\_posts&post\_type=artist&count=2&order=ASC&include=id,title,content,custom_fields,thumbnail

Problem solved!

 [1]: http://wordpress.org/plugins/json-api/