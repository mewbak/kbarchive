---
layout: page
title: "Q255296: &quot;NET TIME&quot; Command Does Not Display the Time in Hungarian Window"
permalink: /kb/255/Q255296/
---

## Q255296: &quot;NET TIME&quot; Command Does Not Display the Time in Hungarian Window

{% raw %}

	Article: Q255296
	Product(s): Microsoft Windows NT
	Version(s): winnt:4.0
	Operating System(s): 
	Keyword(s): kbWinNT400PreSP7Fix
	Last Modified: 06-AUG-2002
	
	-------------------------------------------------------------------------------
	The information in this article applies to:
	
	- Microsoft Windows NT Server version 4.0 
	- Microsoft Windows NT Workstation version 4.0 
	-------------------------------------------------------------------------------
	
	SYMPTOMS
	========
	
	When you issue a "net time" command on Hungarian Windows NT 4.0, the time is not
	displayed. For example, if you run the "net time <computername>" command,
	you see the following response:
	
	  \\<computername> pontos ideje.
	  A parancs sikeresen befejezodott.
	
	Note that this output does not include the time.
	
	The correct response is:
	
	  \\<computername> pontos ideje: 2000.01.01. 0:00
	  A parancs sikeresen befejezodott.
	
	CAUSE
	=====
	
	A string resource is incorrectly localized.
	
	RESOLUTION
	==========
	
	A supported fix is now available from Microsoft, but it is only intended to
	correct the problem that is described in this article. Only apply it to systems
	that are experiencing this specific problem. This fix may receive additional
	testing. Therefore, if you are not severely affected by this problem, Microsoft
	recommends that you wait for the next Windows NT 4.0 service pack that contains
	this fix.
	
	To resolve this problem immediately, contact Microsoft Product Support Services
	to obtain the fix. For a complete list of Microsoft Product Support Services
	phone numbers and information about support costs, visit the following Microsoft
	Web site:
	
	  http://support.microsoft.com/default.aspx?scid=fh;EN-US;CNTACTMS
	
	NOTE: In special cases, charges that are ordinarily incurred for support calls
	may be canceled if a Microsoft Support Professional determines that a specific
	update will resolve your problem. The usual support costs will apply to
	additional support questions and issues that do not qualify for the specific
	update in question.
	
	The English version of this fix should have the following file attributes or
	later:
	
	  Date      Time    Size     File name     Platform
	  -------------------------------------------------
	  06/03/00  11:35   88,848   Netmsg.dll    Intel
	
	
	
	STATUS
	======
	
	Microsoft has confirmed that this is a problem in the Microsoft products that
	are listed at the beginning of this article.
	
	Additional query words:
	
	======================================================================
	Keywords          : kbWinNT400PreSP7Fix 
	Technology        : kbWinNTsearch kbWinNTWsearch kbWinNTW400 kbWinNTW400search kbWinNT400search kbWinNTSsearch kbWinNTS400search kbWinNTS400
	Version           : winnt:4.0
	Hardware          : ALPHA x86
	Issue type        : kbbug
	Solution Type     : kbfix
	
	=============================================================================
	

{% endraw %}
