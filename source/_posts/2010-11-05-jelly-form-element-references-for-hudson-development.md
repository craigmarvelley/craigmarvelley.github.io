---
title: Jelly form element references for Hudson development
author: Craig
layout: post
permalink: /2010/11/05/jelly-form-element-references-for-hudson-development/
categories:
  - Java
---
I&#8217;ve been working on a Hudson plugin, which has been interesting because it&#8217;s been years since I&#8217;ve done any Java development. The tag library used by Hudson, Jelly, seems powerful enough but it&#8217;s not immediately apparent what tags it supports, and the Hudson documentation doesn&#8217;t go into much detail. The only two resources I could find are:

A tag reference (think this is generated from the Jelly JavaDoc)  
<http://hudson-ci.org/maven-site/hudson-core/jelly-taglib-ref.html>

Browse the source  
<https://hudson.dev.java.net/source/browse/hudson/trunk/hudson/main/core/src/main/resources/lib/form/>

Though I picked up the most knowledge from checking out the Hudson source and just looking through the many plugins that have been added to the project &#8211; there are plenty of real-world examples of how to implement various UI patterns.