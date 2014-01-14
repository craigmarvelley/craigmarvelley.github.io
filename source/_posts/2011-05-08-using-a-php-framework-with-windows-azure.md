---
title: Using a PHP framework with Windows Azure
author: Craig
layout: post
permalink: /2011/05/08/using-a-php-framework-with-windows-azure/
aktt_notify_twitter:
  - no
categories:
  - PHP
  - PHP on Azure
---
[This is a blog post related to the [PHP on Azure competition][1].]

It&#8217;s been a while since my last PHP on Azure contest post, mostly due to commitments @work that have reduced my free time considerably. There&#8217;s not long left &#8217;til the competition closes though (I have a week), so I need to get my skates on!

Casting my mind back to my last post, I was able to finally deploy to the local development fabric. In the interim I&#8217;ve set up an Azure account and successfully deployed a simple script to the cloud, so everything&#8217;s fine on that front. It&#8217;s time to start developing my application.

Since my time is limited my application will be quite straightforward &#8211; a CMS to manage media files. This should allow me to use all the features of Azure (queuing, table storage, blobs) I&#8217;m interested in.

## Bittersweet Symfony

The first step in building the application is to decide on  framework to speed up development. The main reason I got into the contest in the first place was because I wanted to have more experience with Zend Framework &#8211; while I&#8217;d used its components in isolation before I&#8217;d never built an application with it. However in the months since I entered the competition I&#8217;ve started using Symfony 2 heavily. That, and the realisation that ZF2 is around the corner, have made me think that ZF isn&#8217;t the best choice for this contest, so I decided to use Symfony 2 instead.

That was easier said than done. I dropped the Symfony framework into my Azure WebRole project, and put together a &#8216;hello world&#8217; script, only to immediately run into [this issue][2] &#8211; apparently Azure has issues when building projects when paths to files or directories exceed 260 characters. Of course, in a framework of Symfony&#8217;s size, with many nested directories, this limit is unrealistic.The solutions recommended on Jim&#8217;s blog include changing the project paths to be shorter (impossible in this case) and setting a temporary environment variable which moves the location at which Azure builds projects, thus reducing the prefix of any paths. As Jim says, this isn&#8217;t a guaranteed fix and indeed, it didn&#8217;t work for me.

So including Symfony within the WebRole didn&#8217;t seem to be possible. I experimented with including in within my PHP include path, in the hope that it would save some characters, but that didn&#8217;t work at all, Azure didn&#8217;t even pick it up. I need to look around the net to see how Azure manages include paths, since it&#8217;s something I use often in PHP. How do PEAR modules work, I wonder? Can you manage PEAR within Azure as you would with a local PHP installation, or do you have to place the components within each WebRole? Topics for future posts, maybe.

Anyway, it didn&#8217;t look like Symfony was going to work any time soon, so I needed an alternative, and since[ Ben Waine had successfully deployed using Zend Framework][3] I thought briefly of using that after all. Then, I came across [Silex][4].

## Along came a Silex

Silex is a micro-framework based on Symfony 2 components, inspired by [Sinatra][5], the Ruby on Rails framework which presents an alternative to typical MVC web applications. It&#8217;s succinct and straightforward, and, crucially, is deployed as a PHAR archive. This means I only need to include a single file in the root of my project to be able to use the library &#8211; which means no long paths that Azure can&#8217;t handle.

I downloaded the Silex archive from its website and dropped it into the root of my project, then copied the &#8216;hello world&#8217; example provided within the Silex documentation into my index.php file:

<pre>require_once __DIR__.'/silex.phar'; 

$app = new Silex\Application(); 

$app-&gt;get('/hello/{name}', function($name) {
    return "Hello $name";
}); 

$app-&gt;run();</pre>

Then I deployed my project to dev fabric, and navigated to /hello/Craig. Of course, this didn&#8217;t work immediately &#8211; nothing ever does for me &#8211; because I didn&#8217;t have a web.config file set up to send all requests through the front controller, index.php. I got an IIS 404 page rather than the &#8216;Hello Craig&#8217; I was expecting. So I used IIS&#8217;s Apache config importer to convert the sample .htaccess file provided by Silex into a web.config file, then copied the relevant rewrite rules into my WebRole&#8217;s config file. Rebuilding the application resulted in a working application. Good to go!

Here&#8217;s what I needed to add to my web.config file in case it&#8217;s of any use to anyone:



## Compiling Silex on Windows

Because Silex is pretty new I&#8217;m expecting to find issues here and there, plus when working on Windows I&#8217;m accustomed to having to make little changes here and there to get PHP code that&#8217;s been written on *nix to run properly &#8211; so I wanted to build the Silex PHAR from source so I could make changes if necessary and properly understand how everything fits together.

This is quite straightfoward. First, I checked out Silex from its [github page][6]:

<pre>git clone https://github.com/fabpot/Silex.git silex</pre>

I merged in [a pending fix][7] which addresses compilation issues on Windows &#8211; there&#8217;s probably a fancy way to do this in git but I just applied the fix manually.

Then I needed to get Silex&#8217;s dependencies:

<pre>git submodule init
git submodule update --recursive</pre>

Silex provides a PHP script, named &#8216;compile&#8217;, which puts the archive together. I had to make some changes to my php.ini file before I could run it successfully:

<pre>phar.readonly = Off
phar.require_hash = Off</pre>

Then creating the archive was as simple as running:

<pre>php compile</pre>

 [1]: http://www.phpazurecontest.com/
 [2]: http://blogs.msdn.com/b/jnak/archive/2010/01/14/windows-azure-path-too-long.aspx
 [3]: http://www.ben-waine.co.uk/blog/php-azure/deploying-a-zend-framework-to-app-fabric.php
 [4]: http://silex-project.org/
 [5]: http://www.sinatrarb.com/
 [6]: https://github.com/fabpot/Silex
 [7]: https://github.com/Ziumin/Silex/commit/6abebd759850c1c2eabc678cfe4bb12a61412768