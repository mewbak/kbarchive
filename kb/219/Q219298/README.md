---
layout: page
title: "Q219298: Fonts Display Incorrectly if More than 48 MB of Fonts Exists"
permalink: /kb/219/Q219298/
---

## Q219298: Fonts Display Incorrectly if More than 48 MB of Fonts Exists

{% raw %}

	Article: Q219298
	Product(s): Microsoft Windows NT
	Version(s): winnt:4.0,4.0 SP1,4.0 SP2,4.0 SP3,4.0 SP4
	Operating System(s): 
	Keyword(s): kbWinNT400sp5fix
	Last Modified: 16-MAY-2002
	
	-------------------------------------------------------------------------------
	The information in this article applies to:
	
	- Microsoft Windows NT Workstation versions 4.0, 4.0 SP1, 4.0 SP2, 4.0 SP3, 4.0 SP4 
	- Microsoft Windows NT Server versions 4.0, 4.0 SP1, 4.0 SP2, 4.0 SP3, 4.0 SP4 
	- Microsoft Windows NT Server, Enterprise Edition versions 4.0, 4.0 SP4 
	-------------------------------------------------------------------------------
	
	SYMPTOMS
	========
	
	When you run any program that includes True Type fonts (for example, Windows NT
	shell, Microsoft Office, Microsoft WordPad, and so forth), you may experience
	the following symptoms:
	
	- Fonts are displayed incorrectly.
	
	- Unknown characters are displayed.
	
	- Blank space are displayed.
	
	This article does not apply to printer fonts. Printer font output is not impacted
	by the 48 MB limit.
	
	CAUSE
	=====
	
	This behavior occurs because there is a 48 MB memory limit for fonts on a
	computer running Windows NT 4.0. After a computer running Windows NT reaches the
	48 MB font limit, that session's fonts are displayed incorrectly as there is no
	room available to load and map fonts.
	
	RESOLUTION
	==========
	
	To resolve this problem, obtain the latest service pack for Windows NT 4.0. For
	additional information, please see the following article in the Microsoft
	Knowledge Base:
	
	  Q152734 How to Obtain the Latest Windows NT 4.0 Service Pack
	
	
	STATUS
	======
	
	Microsoft has confirmed this to be a problem in Windows NT 4.0. This problem was
	first corrected in Windows NT 4.0 Service Pack 5.
	
	MORE INFORMATION
	================
	
	For example, a computer running Windows NT 4.0 Service Pack 3 with Office 2000
	installed has approximately 20 MB of total fonts. If you enable the Japanese (8
	MB), Korean (15 MB), and Chinese (8 MB) language settings, you reach
	approximately 51 MB of total fonts.
	
	The 48 MB limit is easily reached on a computer running Windows NT 4.0 Service
	Pack 4 with Microsoft Internet Explorer 5 and Office 2000 without enabling fonts
	for other languages. You can reach this limit by browsing Web pages. IE5
	automatically installs fonts not currently loaded.
	
	Simply deleting True Type fonts to an amount lower than the 48 MB limit may not
	resolve the issue.
	
	You can view the fonts loaded on your computer by using the Control Panel Fonts
	tool. You can view the size of each font by opening a command prompt and going
	to the \%SystemRoot%\Font folder and typing DIR. If the size of the
	\%SystemRoot%\Font folder is equal to or greater than 48 MB, you may experience
	this issue.
	
	Windows NT 4.0 Service Pack 5 increases the font limit to 128 MB.
	
	
	Additional query words: blank spaces chinese strange characters word wordpad IE5 IE5.0 Office 97 2000 Office97 Office2000 TrueType
	
	======================================================================
	Keywords          : kbWinNT400sp5fix 
	Technology        : kbWinNTsearch kbWinNTWsearch kbWinNTW400 kbWinNTW400search kbWinNT400search kbWinNTW400sp4 kbWinNTW400sp3 kbWinNTW400sp2 kbWinNTW400sp1 kbWinNTSsearch kbWinNTSEntSearch kbWinNTSEnt400sp4 kbWinNTSEnt400 kbWinNTS400sp4 kbWinNTS400sp3 kbWinNTS400sp2 kbWinNTS400sp1 kbWinNTS400search kbWinNTS400
	Version           : winnt:4.0,4.0 SP1,4.0 SP2,4.0 SP3,4.0 SP4
	Hardware          : ALPHA x86
	Issue type        : kbbug
	Solution Type     : kbfix
	
	=============================================================================
	

{% endraw %}
