---
title: Determining the type of Appcelerator objects.
author: Craig
layout: post
permalink: /2011/03/09/determining-the-type-of-appcelerator-objects/
aktt_notify_twitter:
  - no
categories:
  - Appcelerator
  - JavaScript
---
The Appcelerator platform doesn&#8217;t provide a way to determine what the type of an Appcelerator object is (e.g. a Window, a View, a Button, etc.). This is often necessary because one may wish to tailor logic to the type of object being dealt with.

For example, when working with a SplitWindow in an iPad app built in Appcelerator I needed to know if an object that was to be added to the detail view was a navigation group or a window. I ended up using toString() on the object to get its type, then using a regex. This is the way I ended up doing it:

`<br />
if(! window.toString().match(/TiUIiPhoneNavigationGroup/)) {<br />
var nav = Ti.UI.iPhone.createNavigationGroup({<br />
window: window<br />
});`

`return nav;<br />
}`

` `

`return window;<br />
`