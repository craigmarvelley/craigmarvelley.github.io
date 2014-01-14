---
title: 'For the social good &#8211; Box UK Hackday #1 recap'
author: Craig
layout: post
permalink: /2011/11/24/for-the-social-good-box-uk-hackday-1-recap/
aktt_notify_twitter:
  - no
categories:
  - General
  - PHP
---
On the twentieth of November, 2011, the company for whom I work ([Box UK][1]) held a [hackday][2] in Cardiff at the Student&#8217;s Union. It was the first time that we&#8217;d organised such an event, but it seemed to go really well &#8211; feedback from the participants was good, it was well attended, and personally I had a really good (if stressful!) time.

The theme of the hackday was &#8216;For the social good&#8217; &#8211; applications built during the day had to have some sort of social theme, ideally to improve the lives of the people that would use them. That&#8217;s quite a broad topic, and it resulted in an array of different apps &#8211; not just in the sense of intended purpose, but in style, and also in platform. While teams typically used scripting languages to build their apps within those used (PHP, JavaScript, Python) were a lot of varied frameworks (Symfony2, Lithium, Django, jQuery Mobile, Node.js, PhoneGap and more), as well as SQL and No-SQL solutions alike. I initially suggested creating an iOS app, until it was pointed out to me that the verbose nature of Cocoa meant we&#8217;d probably only get one class done in the 8.5 hours we had!

My team comprised of myself; Paul, a former colleague, and Tom, a 3rd Year student at Cardiff University. Paul and I had decided to try to create a mobile app that used geolocation to provide the user with trivia and quizzes for the places of interest around them; we were only going to concern ourselves with Cardiff, so it would be a tourist aid for the city, or perhaps a learning tool for schoolchildren. Tom then joined us, and had originally wanted to work on a Corkboard-style app &#8211; after a discussion we modified that into a Q&A app which would be incorporated into our exploration tool idea, so the user could additionally ask questions and receive answers in realtime. That was the idea, anyway. We had 8.5 hours to implement it!

<div id="attachment_218" class="wp-caption aligncenter" style="width: 310px">
  <a href="/images/posts/2011/11/hackday54.jpg"><img class="size-medium wp-image-218" title="Team Explore Cardiff" src="/images/posts/2011/11/hackday54-300x199.jpg" alt="" width="300" height="199" /></a><p class="wp-caption-text">
    Photo courtesy of dangreenphotography.com
  </p>
</div>

We split our responsibilities up such that Paul would build the mobile app (he plumped for [jQuery mobile][3], version 1 of which having been released just days earlier), Tom would build an app to aggregate questions from users and allow a pool of authors to submit replies (he wanted to use [Cappuccino][4]), and I would build the webservice/content management system both apps would run on (I thought [Symfony2][5] would be a good framework). It sounded good in theory, but then it always does.

I&#8217;ve dabbled with Symfony2 since it was in beta so I knew *what* it could do, but not necessarily *how* to make it do it. So the first hour of the day was spent scanning the documentation and looking through the available &#8216;bundles&#8217; (Symfony nomenclature for packages of redistributable code) to see what community efforts I could re-use. I came across the [SonataAdminBundle][6] relatively quickly and it seemed a good fit &#8211; its purpose is to generate a [CRUD][7] interface for the models within the application&#8217;s domain. This would give me a quick way to add and manipulate the data in the app, so I plumped for it. I guess it&#8217;s a bit risky using an unknown in a hackday since if it turns out to be unsuitable, there&#8217;s not a lot of time to try something else &#8211; but I thankfully had no such problem here.

The SonataAdminBundle is impressive, in that with relatively little configuration and code I had a very functional app. The project documentation assumes a fair bit of Symfony2 knowledge from the developer, which isn&#8217;t ideal in a high pressure scenario where I didn&#8217;t really have time to read the source code, but I&#8217;d worked it out by lunchtime. I&#8217;d say within a couple of hours I had an app with which I could create models, specify forms which related to them, and manage data.

Most of the rest of my day was spent working with [Doctrine2][8], a PHP [ORM][9] that is tightly integrated with Symfony2 and the SonataAdminBundle. Doctrine2 I found to be the perfect tool for a hackday &#8211; create a class, put some annotations on properties to define the type of the field, and any relationship to other classes, then run a command line script which generates all the accessor code, and even updates the database schema &#8211; saving a substantial bit of work. There were some hiccups along the way, but I did manage to get a webservice together which could supply Paul and Tom&#8217;s apps with data.

By this point we were running quite low on time (I think I spent too long chowing down on the copious amounts of free pizza!), and so rather guiltily I left the other members of the team with only an hour to integrate the webservice into their apps &#8211; both were true heroes though, quickly turning everything around so that we could demo something fully featured to the other teams.

[<img class="size-medium wp-image-216 aligncenter" title="The ExploreCardiff mobile app" src="/images/posts/2011/11/Screen-Shot-2011-11-22-at-22.48.17-221x300.png" alt="" width="221" height="300" />][10]

Each of the other teams not only produced an app (I&#8217;ve been to hackdays where people don&#8217;t even get something together to demo, which is a little disappointing) but it was also gratifying to see that each app was functional, innovative and different. My personal favourite was Tomazs&#8217; mobile app for the Welsh Premier League (it doesn&#8217;t get enough love!), but the grit.ly team (who produced a mashup of several data sources to plot on a UK map areas at risk of accidents due to poor weather and lack of gritting), who won first prize, and a team of several 1st year Cardiff Uni students with another former colleague at Box UK, Warren Seymour, who took second with a cool Corkboard app for university students, thoroughly deserved their awards.

It was also great to see Tom take the best individual developer prize, as he demonstrated some serious coding chops despite having to wait until the very last for the data his app depended on. He also ran into some issues with Cappuccino during the day, and rather than abandon what he was doing, he just switched to [Prototype][11] and got on with it in a very pragmatic fashion.

[<img class="aligncenter size-medium wp-image-224" title="Ben and Kevin present their app" src="/images/posts/2011/11/IMG_1005-300x225.jpg" alt="" width="300" height="225" />][12]

As a bonus, after the prizes were handed out we decamped for a drink in the Tafarn, something I haven&#8217;t done since leaving Cardiff University 10 years ago. It was almost worth attending the event solely for the excuse to walk down memory lane!

The code for the CMS app I built can be found on [my Github page][13]. Time permitting, I&#8217;d like to take the idea a bit further; though it&#8217;ll require a bit more planning than the 15 mins it got on Sunday to be a proper success!

 [1]: http://boxuk.com
 [2]: http://hackday.boxuk.com/
 [3]: http://jquerymobile.com/
 [4]: http://cappuccino.org/
 [5]: http://symfony.com/
 [6]: http://sonata-project.org/bundles/admin/master
 [7]: http://en.wikipedia.org/wiki/Create,_read,_update_and_delete
 [8]: http://www.doctrine-project.org/projects/orm/2.0/docs/en
 [9]: http://en.wikipedia.org/wiki/Object-relational_mapping
 [10]: /images/posts/2011/11/Screen-Shot-2011-11-22-at-22.48.17.png
 [11]: http://www.prototypejs.org/
 [12]: /images/posts/2011/11/IMG_1005.jpg
 [13]: https://github.com/craigmarvelley/ExploreCardiffAdmin