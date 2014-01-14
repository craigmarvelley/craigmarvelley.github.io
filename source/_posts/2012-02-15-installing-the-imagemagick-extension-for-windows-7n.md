---
title: 'It&#8217;s a kind of ImageMagick &#8211; installing the PHP extension for Windows 7.'
author: Craig
layout: post
permalink: /2012/02/15/installing-the-imagemagick-extension-for-windows-7n/
aktt_notify_twitter:
  - no
categories:
  - PHP
---
I had a bit of a nightmare recently trying to get the ImageMagick PHP extension working on Windows. Builds of the extension as a DLL are [provided by Mikko][1], which is awesome, but I had some trouble getting it to work.

The workstation I was using was running 64-bit Windows 7N, and the issue I was seeing was that the extension was being registered (if I ran php -m from the command line it seemed to be loaded) but when inspecting phpinfo() output the module was conspicuous by its absence.

Windows 7N is an EU version of Windows that comes without the Media Player framework &#8211; presumably an anti-trust related provision. Upon inspecting the extension DLL with [Dependency Walker][2] I discovered that it was linked to several missing DLLs that are supplied by the Media Player framework, and an additional DLL, IEShims.dll, which is an Internet Explorer library.

I installed the [Media Feature Pack][3] which resolved the majority of the missing DLLs. I also copied IEShims.dll from Program Files\Internet Explorer to Windows\SystemWOW64 (this probably wasn&#8217;t a good idea as the architectures of the DLLs will be fundamentally different, SystemWOW64 expects 32-bit DLLs &#8211; but I haven&#8217;t encountered any adverse effects as yet). After doing this the extension began to work as expected, and was visible in phpinfo() output.

There was a crucial comment on Mikko&#8217;s blog that I&#8217;ll repeat here &#8211; if the workstation is running PHP under IIS/FastCGI, install version **6.6.2-10 or earlier** of ImageMagick (available from [http://image\_magick.veidrodis.com/image\_magick/][4]). Don&#8217;t install any versions later than that &#8211; they were built with VC10 and will not be compatible with the extension, which was built with VC9.

Finally, when I attempted to use the extension (I wanted to convert some images from SVG to PNG) I ran into errors because ImageMagick defaults to using the Windows temp directory as its conversion directory, and IUSR doesn&#8217;t have rights to write there. Rather than add it to the permitted users list (not a very secure approach) I set the IMAGICK_TMP environment system variable to a less prominent location; this required a restart to take effect.

 [1]: http://valokuva.org/?page_id=50
 [2]: http://www.google.co.uk/url?sa=t&rct=j&q=dependency%20walker&source=web&cd=1&ved=0CCAQFjAA&url=http%3A%2F%2Fwww.dependencywalker.com%2F&ei=gmw7T6H-DqqO0AWCsrRt&usg=AFQjCNH2xHd_jlOFVUuUCGsxzdiAM2BlXg
 [3]: http://www.microsoft.com/download/en/details.aspx?id=16546&hash=7gyAvmSLCYr1yxwQ5Zti1LMYQjBvQzi8uADSX76Wzkj8h8n3XewG9LWsYhUlcMRMuXN1CUKhhqyeDDJZjZbygw%3d%3d
 [4]: http://image_magick.veidrodis.com/image_magick/