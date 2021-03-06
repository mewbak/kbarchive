---
layout: page
title: "Q122784: PPT: Bullets Change with PowerPoint Viewer"
permalink: /kb/122/Q122784/
---

## Q122784: PPT: Bullets Change with PowerPoint Viewer

{% raw %}

	Article: Q122784
	Product(s): Microsoft PowerPoint for Windows
	Version(s): MACINTOSH:4.0; WINDOWS:3.0,4.0,4.0a,4.0c,7.0
	Operating System(s): 
	Keyword(s): kbinterop kbviewer kbFont
	Last Modified: 15-APR-2000
	
	-------------------------------------------------------------------------------
	The information in this article applies to:
	
	- Microsoft PowerPoint for Windows 95, version 7.0 
	- Microsoft PowerPoint for Windows, versions 3.0, 4.0, 4.0a, 4.0c 
	- Microsoft PowerPoint for Macintosh, version 4.0 
	-------------------------------------------------------------------------------
	
	SYMPTOMS
	========
	
	If you run a presentation on a computer that has only Microsoft PowerPoint
	Viewer installed, you may find that the bullets or other symbols have changed.
	
	CAUSE
	=====
	
	This behavior occurs when the font you originally used for your symbols or
	bullets is not available on the current computer. Many of the PowerPoint
	templates use Monotype Sorts for bullets. This font is supplied with PowerPoint
	but may not be present on a computer that does not have PowerPoint installed.
	
	WORKAROUND
	==========
	
	PowerPoint for Windows
	----------------------
	
	PowerPoint allows you to save fonts with a presentation so that they can be
	displayed on other computers. To save fonts with a presentation, follow these
	steps:
	
	1. Open your presentation.
	
	2. On the File menu, click Save As.
	
	3. In the File Name box, type either the current name of the presentation or a
	  new name.
	
	4. Click to select the "Embed TrueType Fonts" check box. (In PowerPoint 3.0
	  click to select the "Save Fonts With Presentation" check box.) Click OK.
	
	You can now view this presentation on a computer that does not have all the fonts
	that PowerPoint normally installs.
	
	PowerPoint for the Macintosh
	----------------------------
	
	PowerPoint for the Macintosh does not allow you to save the fonts with a
	presentation. Use one of the following methods to work around this problem:
	
	- Install the font on the other computer using PowerPoint Setup.
	
	  -or-
	
	- Copy the font from the System:Fonts folder to the same folder on the other
	  computer.
	
	  -or-
	
	- For the bullets, use a font other than Monotype Sorts, such as a normal text
	  bullet.
	
	Additional query words: power point 3.00 4.00 4.00a 4.00c 7.00 ppt95 macppt
	
	======================================================================
	Keywords          : kbinterop kbviewer kbFont 
	Technology        : kbHWMAC kbOSMAC kbPowerPtSearch kbPowerPt700 kbZNotKeyword2 kbPowerptMacSearch kbPowerPt700Search kbPowerPt400 kbPowerPt400Mac kbPowerPt300 kbPowerPt400c kbPowerPt400a
	Version           : MACINTOSH:4.0; WINDOWS:3.0,4.0,4.0a,4.0c,7.0
	Hardware          : MAC x86
	Issue type        : kbprb
	
	=============================================================================
	

{% endraw %}
