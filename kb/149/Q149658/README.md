---
layout: page
title: "Q149658: TCP/IP Printing Causes File Cache to Grow"
permalink: /kb/149/Q149658/
---

## Q149658: TCP/IP Printing Causes File Cache to Grow

{% raw %}

	Article: Q149658
	Product(s): Microsoft Windows NT
	Version(s): 4.0
	Operating System(s): 
	Keyword(s): kbprint kbWinNT400sp4fix kbPrinting
	Last Modified: 20-FEB-2002
	
	-------------------------------------------------------------------------------
	The information in this article applies to:
	
	- Microsoft Windows NT Workstation version 4.0 
	- Microsoft Windows NT Server version 4.0 
	- Microsoft Windows NT Server version 4.0, Terminal Server Edition 
	-------------------------------------------------------------------------------
	
	
	SYMPTOMS
	========
	
	If you transfer large print jobs via LPR/LPD, either from a Windows NT computer
	to an LPD printer or from some other system to the LPD service, you notice a
	user interface performance degradation. The jobs need to have about the size of
	the physical memory of the computer.
	
	If you look at performance counters while this happens, you find that the counter
	for the file cache (Memory: Cache Bytes) is very high while the process working
	sets decline (Process: Working Set, instance _Total).
	
	CAUSE
	=====
	
	While copying spool files, the TCP/IP printing components do not use the flag
	FILE_FLAG_SEQUENTIAL_SCAN to open the files. Thus, cache manager increases the
	cache size when data is read or written because it expects the application to
	need it again.
	
	RESOLUTION
	==========
	
	To resolve this problem, obtain the latest service pack for Windows NT 4.0 or
	Windows NT Server 4.0, Terminal Server Edition. For additional information,
	please see the following article in the Microsoft Knowledge Base:
	
	  Q152734 How to Obtain the Latest Windows NT 4.0 Service Pack
	
	
	STATUS
	======
	
	Microsoft has confirmed this to be a problem in Windows NT 4.0 and Windows NT
	Server 4.0, Terminal Server Edition. This problem was first corrected in Windows
	NT 4.0 Service Pack 4.0 and Windows NT Server 4.0, Terminal Server Edition
	Service Pack 4.
	
	
	
	Additional query words:
	
	======================================================================
	Keywords          : kbprint kbWinNT400sp4fix kbPrinting 
	Technology        : kbWinNTsearch kbWinNTWsearch kbWinNTW400 kbWinNTW400search kbWinNT400search kbWinNTSsearch kbWinNTS400search kbWinNTS400 kbNTTermServ400 kbNTTermServSearch
	Version           : :4.0
	Issue type        : kbbug
	Solution Type     : kbfix
	
	=============================================================================
	

{% endraw %}
