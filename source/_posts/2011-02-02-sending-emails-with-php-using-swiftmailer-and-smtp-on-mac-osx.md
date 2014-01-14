---
title: Sending emails with PHP using Swiftmailer and SMTP on Mac OSX
author: Craig
layout: post
permalink: /2011/02/02/sending-emails-with-php-using-swiftmailer-and-smtp-on-mac-osx/
aktt_notify_twitter:
  - no
categories:
  - General
---
I&#8217;m a fan of [Swiftmailer][1] for sending emails through PHP &#8211; it&#8217;s a much more elegant alternative to the `mail() `function and recently was absorbed into the Symfony project, so its future seems certain. A big plus is its support for sending mail using the `<a href="ht<code></code>tp://en.wikipedia.org/wiki/Simple_Mail_Transfer_Protocol">SMTP</a>` protocol, which makes it great for more complex scenarios where authentication or performance are concerns.

Up until this week I&#8217;d only used Swiftmailer on Windows, with an SMTP server on our network. This changed when I needed to do a demonstration using my Macbook, and as OSX comes installed with [Postfix][2] I thought everything should just work if I [configured Swiftmailer to use an SMTP server][3] on `localhost` at the standard port (25). This was nearly the case &#8211; as I read [here][4] while Postfix is installed, it&#8217;s not enabled by default. After following the steps outlined there email started sending as expected.

 [1]: http://swiftmailer.org/
 [2]: http://www.postfix.org/
 [3]: http://swiftmailer.org/docs/smtp-howto
 [4]: http://www.freshblurbs.com/how-enable-local-smtp-postfix-os-x-leopard