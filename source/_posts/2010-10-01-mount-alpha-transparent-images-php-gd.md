---
title: Mounting alpha transparent images with PHP and GD
author: Craig
layout: post
permalink: /2010/10/01/mount-alpha-transparent-images-php-gd/
categories:
  - PHP
---
Yesterday brought a bug in a PHP thumbnail library I&#8217;ve been working on: when mounting a 24 bit PNG with alpha transparency onto another &#8216;framing&#8217; image the transparency was being lost. A simplified version of the code looks something like this:

<pre>// Read the transparent image
$image = imagecreatefrompng('transparent.png');
$width = imagesx($image);
$height = imagesy($image);

// Create the mount
$border = 10;
$mountWidth = $width + ($border * 2);
$mountHeight = $height + ($border * 2);
$mount = imagecreatetruecolor($mountWidth, $mountHeight);
$mountColour = imagecolorallocate($mount, 255, 0, 0);
imagefilledrectangle($mount, 0, 0, $mountWidth, $mountHeight, $mountColour);

// Centre the image within the mount
imagecopymerge($mount, $image, $border, $border, 0, 0, $width, $height, 100);

// Output to screen
header('Content-Type: image/png');
imagepng($mount);</pre>

This all worked well enough until someone tried mounting a PNG with alpha transparency, whereupon things became very messy. A bit of googling [suggested][1] [that][2] that the [imagecopymerge][3]() function was to blame (I&#8217;d used  it because it allowed the manipulation of opacity in the merged image) and that the [imagecopy][4]() function handled transparency better &#8211; which I found to be the case.

So a transparency-friendly version of the script looks like:

<pre>// Read the transparent image
$image = imagecreatefrompng('transparent.png');

...

// Centre the image within the mount
imagecopy($mount, $image, $border, $border, 0, 0, $width, $height);

// Output to screen
header('Content-Type: image/png');
imagepng($mount);</pre>

And problem solved &#8211; though I&#8217;d like to find a way to maintain image transparency while also being able to adjust the opacity of the mounted image.

 [1]: http://drupal.org/node/80369
 [2]: http://www.phpfreaks.com/forums/index.php?topic=127046.0
 [3]: http://uk.php.net/imagecopymerge
 [4]: http://uk.php.net/imagecopy