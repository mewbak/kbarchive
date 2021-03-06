---
layout: page
title: "Q231274: Macintosh Client Computer May Hang When Searching for Files"
permalink: /kb/231/Q231274/
---

## Q231274: Macintosh Client Computer May Hang When Searching for Files

{% raw %}

	Article: Q231274
	Product(s): Microsoft Windows NT
	Version(s): winnt:4.0,4.0 SP1,4.0 SP2,4.0 SP3,4.0 SP4
	Operating System(s): 
	Keyword(s): kbnetwork
	Last Modified: 10-AUG-2001
	
	-------------------------------------------------------------------------------
	The information in this article applies to:
	
	- Microsoft Windows NT Server, Enterprise Edition versions 4.0, 4.0 SP4 
	- Microsoft Windows NT Server versions 4.0, 4.0 SP1, 4.0 SP2, 4.0 SP3, 4.0 SP4 
	-------------------------------------------------------------------------------
	
	SYMPTOMS
	========
	
	When you search for files on a Macintosh client computer, the computer may
	temporarily stop responding (hang). This behavior occurs even though the
	CatSearch function is disabled on the Macintosh volume the client is searching.
	
	CAUSE
	=====
	
	The Macintosh client may be running an AppleScript that requests a CatSearch,
	even though the CatSearch function is disabled.
	
	When the CatSearch function is disabled on a Macintosh volume, the information is
	passed to Macintosh clients when volume parameters are passed, and the clients
	do not search volumes by requesting a CatSearch. Instead, they perform an
	Enumerate request. However, Macintosh clients can run an AppleScript that
	overrides the information passed to the client so the client can request a
	CatSearch.
	
	RESOLUTION
	==========
	
	To resolve this issue, alter or remove the AppleScript.
	
	MORE INFORMATION
	================
	
	You can verify whether or not the Macintosh client is using the CatSearch
	function by performing a network trace during the slowness between the Macintosh
	client and the Windows NT Server-based computer hosting the Macintosh volume.
	
	REFERENCES
	==========
	
	For additional information, please see the following articles in the Microsoft
	Knowledge Base:
	
	  Q162189 Macintosh Clients May Hang Temporarily with Multiple Mac Volumes
	
	  Q158796 Macintosh Clients Connected to WinNT Server Appear to Hang
	
	Additional query words: SFM MAC
	
	======================================================================
	Keywords          : kbnetwork 
	Component         : MAC Macintosh
	Technology        : kbWinNTsearch kbWinNT400search kbWinNTSsearch kbWinNTSEntSearch kbWinNTSEnt400sp4 kbWinNTSEnt400 kbWinNTS400sp4 kbWinNTS400sp3 kbWinNTS400sp2 kbWinNTS400sp1 kbWinNTS400search kbWinNTS400
	Version           : winnt:4.0,4.0 SP1,4.0 SP2,4.0 SP3,4.0 SP4
	Hardware          : ALPHA MAC x86
	Issue type        : kbprb
	
	=============================================================================
	

{% endraw %}
