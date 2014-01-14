---
title: 'Magento on Windows: Unable to log into admin area'
author: Craig
layout: post
permalink: /2010/10/13/magento-on-windows-unable-to-log-into-admin-area/
categories:
  - PHP
---
I&#8217;ve run into this issue a few times when setting [Magento][1] up on Windows, but keep forgetting how to resolve it. After the setup wizard, on attempting to log into the admin area with the correct credentials I was constantly being redirected back to the login screen with no errors to suggest why I&#8217;d been denied.

There&#8217;s [some advice][2] on the Magento forum that advocates commenting out some code relating to session cookie instantiation, but the fault seems to lie with Magento requiring a [TLD][3] in order to persist the session &#8211; therefore placing your installation at a URL like http://magento.something rather than http://magento should prevent this happening and let you access the store backend without having to hack modify the code.

 [1]: http://www.magentocommerce.com/
 [2]: http://www.magentocommerce.com/boards/viewthread/43148/
 [3]: http://en.wikipedia.org/wiki/Top-level_domain