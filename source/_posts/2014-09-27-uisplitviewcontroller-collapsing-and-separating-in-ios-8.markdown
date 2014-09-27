---
layout: post
title: "UISplitViewController collapsing and separating in iOS 8"
date: 2014-09-27 22:39:43 +0000
comments: true
categories: iOS
---

The new UISplitViewController class and delegate methods in iOS 8 is interesting, and caused me a lot of head scratching last week.
The problem Brent Simmons describes [here](http://inessential.com/2014/09/27/uisplitviewcontroller_question), where
after rotating the device from regular to compact size class and back again iOS uses the topmost master view controller
as the new detail view, instead of the previous detail view, is roughly the same issue I had.

As far as I can tell so far, I think the following approach solves the issue. Note that I don't think I have the same set up as
Brent - I have a navigation stack in each of the master and detail sides - but I think the general approach
is sound, based on advice from Apple in the the "Building Adaptive Apps with UIKit" session from this year's WWDC,
and the "AdaptivePhotos" sample app code they provide.

My UISplitViewController delegate looks like this:

{% gist c3cbbb717c3ef957cbbe %}

* In the 'collapse' method, which is called when the device rotates to portrait, we disregard the detail view controller and use the
master view controller if the detail view has no content
* In the 'merge' method, we look to see if there's a navigation controller which is displaying a NoteViewController (this controller
  is currently only used as a detail view, exclusively, so it's a safe bet). If it exists, we use it - otherwise we retrieve the 'stock'
  note view controller stack from the storyboard and use that.

This approach seems to have worked well so far. The majority of issues I've found have been on the iPhone 6 Plus, which combines the
single hierarchy approach of the smaller form factor devices in regular mode, with the side-by-side dual view approach or the larger form factors
in compact mode - this hybrid strategy seems to require more direction on our part, whereas elsewhere iOS tends to guess right on its own.

A final note - having to manually ensure the back button exists and is configured on the detail view controller is a bit icky, but I needed
to do this to avoid a crash. I'd love to hear from anyone with more elegant ways to handle this.
