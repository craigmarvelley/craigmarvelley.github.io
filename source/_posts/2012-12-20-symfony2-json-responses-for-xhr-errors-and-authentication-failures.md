---
title: 'Symfony2: JSON responses for XHR errors and authentication failures'
author: Craig
excerpt: Investigating the options for handling XHR exceptions when making AJAX requests to a Symfony2 application.
layout: post
permalink: /2012/12/20/symfony2-json-responses-for-xhr-errors-and-authentication-failures/
categories:
  - PHP
  - Symfony2
---
I&#8217;ve been working on a Symfony2 application whose user interface is presented as a single page application that makes heavy use of JavaScript. The app sends [XHR][1] requests to the Symfony2 backend API to retrieve and modify data, and it uses Symfony&#8217;s authorisation/authentication functionality to protect resources so they are only accessible to logged in users.

In an ideal world every request made by the application will succeed, but in reality things often go wrong; the user may have provided invalid data, their session may have expired meaning they are no longer logged in, or we may have a bug in our API code which causes a server error. With an out-of-the-box installation of Symfony2, each of these scenarios will result in the default error handler rendering a HTML page which isn&#8217;t much use to our client JavaScript application &#8211; instead we want the server to issue a JSON response to our AJAX request, complete with some contextual error details, with which we can give the user a meaningful error message.

I did a bit of Googling and came across a [few][2] [posts][3] [which][4] dealt with some of these challenges, and by putting them all together I arrived at a solution which I&#8217;ll detail here in case it&#8217;s of use to anyone else.

[I&#8217;ve put together a demo app][5] which hopefully illustrates everything. Have a play with it (installation instructions are in the README), then read on <img src='http://marvelley.com/wp-includes/images/smilies/icon_smile.gif' alt=':)' class='wp-smiley' /> 

[<img class="aligncenter size-full wp-image-341" title="The demo application" src="http://marvelley.com/wp-content/uploads/2012/12/Screen-Shot-2012-12-20-at-21.55.12-e1356040628744.png" alt="" width="600" height="398" />][6]

The app consists of a few components:

Client side:

*   A jQuery global AJAX error handler
*   A login form &#8211; I have two, a Symfony2/Twig-based HTML login page which the user is redirected to if they try to access the app without a valid session, and a JavaScript login dialog which we will display if the server rejects an AJAX request due to authentication/authorisation failure, allowing the user to reauthenticate without leaving the app

Server side:

*   An authentication failure handler
*   An authentication success handler
*   A kernel exception listener

As far as the rest of the app goes, I&#8217;m using the [FOSUserBundle][7] with a standard configuration, which supplies the rest of the auth functionality, including the HTML login page.

Let&#8217;s start with the server components &#8211; three classes and a bit of config:

<noscript>
  <p>
    View the code on <a href="https://gist.github.com/4340230">Gist</a>.
  </p>
</noscript>

The `XHRAuthenticationSuccessHandler` and `XHRAuthenticationFailureHandler` class&#8217; code is triggered when the user logs in, or fails to log in, respectively. We check to see if the original request was an AJAX (XHR) one, and if so we respond with JSON. If it&#8217;s a failure we&#8217;re dealing with, we also include the exception message to give the user some feedback &#8211; note that this is a quick solution; it might be prudent to vet the message, or to translate it. I&#8217;ve also included a &#8216;success&#8217; property which is a JavaScript convention that some frameworks (like [ExtJS][8]) use to execute appropriate callbacks. Finally, we wire up these handlers with the security component in our application&#8217;s [security configuration][9].

The `XHRCoreExceptionListener` class code is triggered whenever a kernel exception occurs &#8211; check the [service definition][10] for this listener, you&#8217;ll see we tell Symfony to call its `onCoreException` method whenever an exception event is fired. Again, we only want to act if the request that caused the exception was an AJAX one. Assuming it is, we try to work out the status code to return from the exception code &#8211; if it&#8217;s a valid HTTP code, we use that, otherwise we assume a server error (500). As before, we&#8217;re reusing the exception message to provide context &#8211; but in this case, where the exception could relate to anything in the system (like a database query) we&#8217;d really want to be cautious about exposing it to the user, so this code certainly isn&#8217;t suitable for a production environment.

That&#8217;s it for the server, now for the client. All the functionality is in `src/Acme/DemoBundle/Resources/views/Welcome/index.html.js`.

First we define a global error handler, which will be fired whenever an uncaught AJAX error occurs:

<noscript>
  <p>
    View the code on <a href="https://gist.github.com/4348746">Gist</a>.
  </p>
</noscript>

If the problem is that the user does not have a valid authentication token, we invite them to log in.

<noscript>
  <p>
    View the code on <a href="https://gist.github.com/4348760">Gist</a>.
  </p>
</noscript>

The login process is interesting &#8211; the modal login form is essentially a duplicate of the HTML one, but lacks the CSRF token which is automatically injected into the HTML form by Symfony. This helps prevent spoofing so I didn&#8217;t want to remove it, so the approach I took was to request the HTML login page, capture the value of the CSRF field in the response, then use that in a second request to actually authenticate the user. This meant I could reuse the same authentication code on the server.

The demo app also includes two other demonstrations &#8211; making a valid request (which will fail, and force a login, if the user does not have a valid session) and an invalid one (which displays the error message returned by the server). There&#8217;s not much to say about those, the code should be self explanatory.

That&#8217;s it really. The code is a little rough and ready, but hopefully it&#8217;ll give you enough to go on if you&#8217;re trying to do something similar!

 [1]: http://en.wikipedia.org/wiki/XMLHttpRequest
 [2]: http://stackoverflow.com/questions/8607212/symfony2-ajax-login
 [3]: https://groups.google.com/forum/?fromgroups=#!topic/symfony-devs/WvESDBprKrU
 [4]: http://stackoverflow.com/questions/12385923/handle-errors-in-ajax-within-symfony2-controller
 [5]: https://github.com/craigmarvelley/symfony2-xhr-error-handling
 [6]: http://marvelley.com/wp-content/uploads/2012/12/Screen-Shot-2012-12-20-at-21.55.12-e1356040628744.png
 [7]: https://github.com/FriendsOfSymfony/FOSUserBundle/blob/master/Resources/doc/index.md
 [8]: http://www.sencha.com/products/extjs
 [9]: https://gist.github.com/4340230#file-security-yml
 [10]: https://gist.github.com/4340230#file-services-xml