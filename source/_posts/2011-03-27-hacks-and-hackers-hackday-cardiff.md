---
title: Hacks and Hackers Hackday Cardiff
author: Craig
layout: post
permalink: /2011/03/27/hacks-and-hackers-hackday-cardiff/
aktt_notify_twitter:
  - no
categories:
  - General
---
It&#8217;s long overdue but here&#8217;s a quick recap of the [Hacks and Hackers Hackday][1] I attended on the 11th March 2011 at the [Atrium][2], Cardiff. It was my first hackday &#8211; though I&#8217;d been itching to try one for a while it seems they don&#8217;t tend to happen in Cardiff that often. I wasn&#8217;t disappointed, the day was really enjoyable.

The hackday was sponsored and organised by [Scraperwiki][3], an open-source effort which aims to make webscraper tools, and the data they harvest, easily available and modifiable to the general public. In particular, the event attempted to bring journalists (hacks) and developers (hackers) together so that by combining each other&#8217;s strengths, we might teach each one another how to obtain and interpret the masses of public data that exists on the internet.

I went along with [Carey][4] and [Warren][5] from [Box UK][6], and we formed a team with three &#8216;hacks&#8217; &#8211; <a href="http://twitter.com/#!/yessof" target="_blank">Steve Fossey</a>, Eva Tallaksen from <a href="http://www.intrafish.no/global/" target="_blank">Intrafish</a> and<a href="http://twitter.com/#!/digitalst" target="_blank"> Gareth Morlais</a> from <a href="http://www.bbc.co.uk/cymru/" target="_blank">BBC Cymru</a>. We named ourselves Co-Ordnance, though I can&#8217;t remember why &#8211; think it was decided while I was busy hacking!

<div class="mceTemp">
  <dl id="attachment_162" class="wp-caption alignnone" style="width: 650px;">
    <dt class="wp-caption-dt">
      <a href="/images/posts/2011/03/stock-exchange.jpg"><img class="size-full wp-image-162" title="Co-Ordnance (courtesy Scraperwiki blog)" src="/images/posts/2011/03/stock-exchange.jpg" alt="" width="640" height="478" /></a>
    </dt>
    
    <p>
      Co-Ordnance (courtesy Scraperwiki blog)
    </p>
  </dl>
</div>

Inspired by some ideas Eva had we initially decided to try to write an application to model stock market data, specifically a tool to collate stock market updates from floated companies. With a little more brainstorming we decided to make this a sub-feature of a larger tool that would plot companies on a UK map according to their registered addresses. The user would be able to filter by the type of business and the region in which it was registered, as well as letting them choose a specific point in time. Thus one could make observations about the behaviour of businesses, such as the popularity of certain sectors of business in certain areas, the impact the recession had on business growth or the collapse of businesses, which regions are ripe for investment, and so on.

While Warren and Eva focused on writing a Scraperwiki script to collect the stock market data the rest of us planned the application. The first thing we considered was how we could obtain geolocation data for the companies that we were to be referencing, and that led us into trying to scrape data from the [Companies House][7] website.

This proved to be difficult, as URLs within the site feature hashed components &#8211; possibly in an attempt to prevent spiders from navigating the site. This meant we&#8217;d never come up with a scraper solution in the time that we had available, but thankfully a member of the Scraperwiki team told us about [OpenCorporates][8], which aims to &#8220;have a URL for every company in the world&#8221;. Many of those URLs provide addresses for companies, which we could geo-encode (using Google&#8217;s Geoencoder) to obtain UK co-ordinates for that company. So we were able to plot companies per region on a map.

<div class="mceTemp">
  <dl id="attachment_161" class="wp-caption alignnone" style="width: 650px;">
    <dt class="wp-caption-dt">
      <a href="/images/posts/2011/03/coordnance2.jpg"><img class="size-full wp-image-161 " title="Carey presents our app (courtesy Scraperwiki blog)" src="/images/posts/2011/03/coordnance2.jpg" alt="" width="640" height="478" /></a>
    </dt>
    
    <p>
      Carey presents our app (courtesy Scraperwiki blog)
    </p>
  </dl>
</div>

Carey wrote a scraper tool so that we could download data for each company into a local MySQL database for indexing. This would allow us to retrieve businesses for a particular region. A nice feature of the OpenCorporate dataset is that one is able to access the data in JSON, which made saving and accessing the data really easy, especially as the application was mainly to be written in JavaScript using the ExtJS framework. Incidentally, I took the opportunity to try the beta version of ExtJS 4, but since the app ended up being pretty much just a map and a form to manipulate the plotted data I didn&#8217;t get to play with any of the stuff added in the new release.

So once we&#8217;d downloaded the data of a few thousand companies (enough for a sample dataset) and indexed the data by location, I needed to write the frontend to plot the companies on a Google Map. By this point we had a little under three hours left, so it was a bit of a push &#8211; especially since I hadn&#8217;t done any Google Maps development in about three years, and the API had completely changed during that period. Thankfully a generous supply of sweets, Coke and beer kept me energetic, and we just about made it. We didn&#8217;t get chance to integrate Warren&#8217;s work into the app, which was a shame, but we still managed to achieve two solutions, which I thought impressive considering the time we had available to us (about 7 hours, once we&#8217;d got started).

In the reckoning we came third, which we were chuffed with. In addition to this Warren also won an individual prize for making the best use of Scraperwiki, which was totally deserved. It would perhaps have been nice if the judges had explained why they voted as they had, as I, and others I spoke to, were confused as to what the marking criteria was. Nevertheless it was a really good day, which challenged me in ways I&#8217;d never been challenged before, and forced me to work within a totally new team, under pressure, on a topic that I knew nothing about. I&#8217;d recommend the Scraperwiki tools, and the next time I need to harvest some data I&#8217;ll definitely be making use of them.

The code I wrote on the day is available at my [Github page][9], and I&#8217;m hoping to get the app into a more usable state and hosted on this site in the near future.

 [1]: http://blog.scraperwiki.com/2011/03/15/cardiff-hacks-and-hackers-hacks-day/
 [2]: http://cci.glam.ac.uk/campus/
 [3]: http://scraperwiki.com/
 [4]: http://twitter.com/#!/HandyBiteSize
 [5]: http://twitter.com/#!/woogoose
 [6]: http://www.boxuk.com/
 [7]: http://www.companieshouse.gov.uk/
 [8]: http://opencorporates.com/
 [9]: https://github.com/craigmarvelley/hhhCar