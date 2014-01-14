---
title: Three20, XCode 4 and the case of the missing header files.
author: Craig
layout: post
permalink: /2011/08/25/three20-xcode-4-and-the-case-of-the-missing-header-files/
aktt_notify_twitter:
  - no
categories:
  - iOS
---
After a good hour of hitting my head against a brick wall, I finally managed to get Facebook&#8217;s three20 iOS library integrated with my XCode 4 based project, documented here for posterity and the hope that it may save someone else from the raw, savage agony I&#8217;m currently feeling.

I followed the instructions on the [three20 website][1] to the letter, using the python installation script to add the library to my project, but whenever I tried to include the main Three20.h header file within my application code I got a &#8216;file not found&#8217; warning which failed the build. After much trial and error / Stack Overflow searching I came across [this post][2] which seemed to suggest trying every header search path under the sun. Indeed, one of these finally worked &#8211; I narrowed it down to the $(BUILT\_PRODUCTS\_DIR)/../three20 entry, but YMMV.

As much as I like iOS, and XCode, Apple&#8217;s solution for integrating libraries is extremely error prone &#8211; and this was *with* a custom installation script. Hopefully once XCode 4 adoption has grown the process can be simplified, as newer libraries like [RestKit][3] seem to be less complicated to install.

 [1]: http://three20.info/article/2010-10-06-Adding-Three20-To-Your-Project
 [2]: http://stackoverflow.com/questions/6833804/problem-with-three20
 [3]: http://restkit.org/