---
layout: post
title: "Restore missing audio in iMovie for Mac"
date: 2014-02-17 08:45:26 +0000
comments: true
categories:
---

![image](http://farm1.staticflickr.com/169/414411019_e702aa6d54_o.jpg)

I recently got a new Macbook (running Mavericks) and wanted to transfer the iMovie projects from my older machine (running Mountain Lion). The new machine featured the most recent version of iMovie (iMovie for Mac, version 10.0.2) while my old one was on 9.0.9.

I loaded the projects into iMovie for Mac by copying over the `iMovie Events`, `iMovie Original Movies` and `iMovie Projects` folders via AirDrop. Upon starting iMovie for Mac it prompted me to upgrade my projects to the new format. After some time a dialog appeared notifying me that some events had not been found, and that the upgrade had not been successful.

It turned out that the movie events were fine, but the background audio I'd added (via iTunes) was missing because I'd not copied over my iTunes folder (and hadn't planned to, since I now use iTunes in the Cloud). Attempting to open a ported project gave me a dialog along the lines of 'Upgrade now, with missing events, or upgrade later' - the choice was inconsequential since even by choosing 'Upgrade later' before putting the tracks in the places they were expected before opening the movie, the movie didn't seem to pick up on the fact that they were now there. The waveforms remained blank, and the audio didn't play. Of course, in most cases I didn't even know which files were missing because most of these movies were put together months ago.

I eventually fixed it by painstakingly downloading and importing each audio track into the movie alongside the original clip, which triggered a reload of the original. Then the second clip could be removed, leaving the original which now played. It would be nice if iMovie for Mac had a 'reload all events in this movie' feature (perhaps it does, and I couldn't find it - I've never found iMovie to have the most intuitive of interfaces)- thankfully I only had 20 or so tracks to fix, but for some more hardcore users it could be a lot worse.

(Waveform image copyright [Bernard Goldbach](http://www.flickr.com/photos/topgold/414411019/))