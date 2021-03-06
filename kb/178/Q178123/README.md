---
layout: page
title: "Q178123: Multimedia: Video Clips Do Not Play Properly"
permalink: /kb/178/Q178123/
---

## Q178123: Multimedia: Video Clips Do Not Play Properly

{% raw %}

	Article: Q178123
	Product(s): Microsoft Home Multimedia Titles
	Version(s): 
	Operating System(s): 
	Keyword(s): kbdisplay kbenv kbimu
	Last Modified: 06-AUG-2002
	
	-------------------------------------------------------------------------------
	The information in this article applies to:
	
	- Microsoft Bookshelf 98 for Windows 
	- Microsoft Cinemania for Windows, 1992, 1993, 1994, 1995, 1996, 1997 editions 
	- Microsoft Encarta 98 Encyclopedia for Windows 
	- Microsoft Music Central for Windows, 1996, 1997 edition 
	-------------------------------------------------------------------------------
	
	SYMPTOMS
	========
	
	When you attempt to play a video clip in one of the Microsoft programs listed at
	the beginning of this article, you may experience any of the following
	symptoms:
	
	- Video playback may be distorted or scrambled.
	
	- Video playback may jump or skip.
	
	- Video playback controls may not be displayed.
	
	- When you open a new video clip, you may see the final frame of the last video
	  clip that you played.
	
	- When you use Cinemania or Music Central, when you click a video clip title in
	  the Gallery, it may not play automatically.
	
	CAUSE
	=====
	
	This behavior can occur for either of the following reasons:
	
	- The Microsoft DirectVideo driver is installed, and your video card does not
	  support it. DirectVideo accelerates playback of video clips that use Indeo or
	  Cinepak video compression.
	
	- The installation program for your video display card or video capture card
	  added legacy support for DCI functions that can conflict with the DCI support
	  in Microsoft Windows 95/98.
	
	RESOLUTION
	==========
	
	To resolve this issue:
	
	1. Click Start, point to Settings, and then click Control Panel.
	
	2. Double-click Multimedia.
	
	3. On the Advanced tab or the Devices tab, double-click Video Compression
	  Codecs.
	
	4. If DirectVideo Driver (DRAW) appears in the list, double-click it, and then
	  click Remove.
	
	5. When you are prompted to remove the DirectVideo driver, click Yes, and then
	  click OK until you return to Control Panel.
	
	6. Close Control Panel.
	
	7. Click Start, and then click Run.
	
	8. In the Open box, type "system.ini" (without the quotation marks), and then
	  click OK.
	
	9. On the Search menu, click Find.
	
	10. Type "[drivers]" (without the quotation marks), and then click Find Next.
	
	11. In the [drivers] section of the System.ini file, type a semicolon (;) at the
	  beginning of the following line
	
	  DCI=<device>
	
	  where <device> is one of the following values:
	
	   - RFMDCI
	   - MIRODCI
	   - DISPLAY
	
	12. On the Search menu, click Find.
	
	13. Type "[display]" (without the quotation marks), and then click Find Next.
	
	14. In the [display] section of the System.ini file, type a semicolon (;) at the
	  beginning of the following line:
	
	  DCI-Support=On
	
	15. On the File menu, click Save.
	
	16. On the File menu, click Exit.
	
	17. Restart the computer.
	
	
	Additional query words: multi multi-media media mm vfw
	
	======================================================================
	Keywords          : kbdisplay kbenv kbimu 
	Technology        : kbHomeProdSearch kbHomeMMsearch kbEncartaSearch kbBookshelfSearch kbEncartaEncycSearch kbCineManiaSearch kbBookShelf1998 kbMusicCentral kbEncartaEnCyc1998 kbMusicCentral1996 kbMusicCentral1997
	Version           : :
	Issue type        : kbprb
	
	=============================================================================
	

{% endraw %}
