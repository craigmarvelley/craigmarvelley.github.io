---
title: 'Titanium Appcelerator &#8211; Resizing the Andriod emulator'
author: Craig
layout: post
permalink: /2010/11/28/titanium-appcelerator-resizing-the-andriod-emulator/
aktt_notify_twitter:
  - no
categories:
  - JavaScript
---
While messing around with Appcelerator it was annoying that on my 13&#8243; Macbook the Android emulator was too big for the screen &#8211; the Titanium Developer program doesn&#8217;t provide a way to change this. My workaround was to copy the command that&#8217;s being run to launch the emulator from the console output, and run the emulator manually with a resize option before deploying the app.

This can be accomplished using the emulator&#8217;s -scale option, which is a number from 0.1 to 3. I found setting it to 0.7 resulted in an emulator with a workable size for my Macbook.

From the root of your Android SDK folder run:

/tools/emulator -avd titanium\_2\_WVGA854 -port 5560 -sdcard ~/.titanium/android2.sdcard -logcat &#8216;\*:d \*&#8217; -no-boot-anim -partition-size 128 -scale 0.7

(titanium\_2\_WVGA854 is the name of the emulator created by Titanium, this will differ depending on your chosen emulator).