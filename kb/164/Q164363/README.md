---
layout: page
title: "Q164363: Troubleshooting RIP on Routing and Remote Access"
permalink: /kb/164/Q164363/
---

## Q164363: Troubleshooting RIP on Routing and Remote Access

{% raw %}

	Article: Q164363
	Product(s): Microsoft Windows NT
	Version(s): 4.0
	Operating System(s): 
	Keyword(s): kbusage
	Last Modified: 09-AUG-2001
	
	-------------------------------------------------------------------------------
	The information in this article applies to:
	
	- Microsoft Windows NT Server version 4.0 
	- Microsoft Routing and Remote Access Service Update for Windows NT Server version 4.0 
	-------------------------------------------------------------------------------
	
	SUMMARY
	=======
	
	This article provides information on troubleshooting possible configuration
	problems Internet Protocol (IP) Routing Information Protocol (RIP) when you use
	Routing and Remote Access Service (RRAS).
	
	MORE INFORMATION
	================
	
	The following list contains possible configuration problems with IP RIP. All the
	options mentioned in these steps are configured on a per-interface basis. You
	can accomplish this with the Routing and Remote Access administrator tool found
	in the Administrator Tool (Common) group. Routing and Remote Access
	administrator can also be started by running Mpradmin.exe. This is not the same
	as IP RIP service included with Microsoft Windows NT Server version 4.0.
	
	- If you have a mixed environment of RIP version 1 and RIP version 2, Check the
	  General tab to verify that RIP version 2 is using broadcast instead of
	  multicast.
	
	- If you have selected the Enable Authentication box on the General tab, make
	  sure that the password in the Password box is the same as the password on the
	  router receiving packets from this interface. By default, authentication is
	  off. Passwords are case sensitive.
	
	- Ensure that you are only accepting routes from the routers you want. Check
	  the Security tab to see which routers are allowed to exchange information. By
	  default, all routes are accepted.
	
	- If host routes or default routes are not being propagated as you expect,
	  change settings on the Advanced tab. By default, host and default routes are
	  not sent or accepted.
	
	- If RIP does not learn routes over a demand-dial link, use multicast instead
	  of broadcast. This is because demand-dial links can have endpoints on
	  different subnets where broadcast RIP requests cannot be heard.
	
	- When you use Auto-Static RIP on a demand-dial interface, you must manually
	  update routes the first time you make a connection. To do this, click Summary
	  in the IP Routing folder, select the demand-dial interface, right-click,
	  point to Update Routes and then click. This must also be done on the other
	  router for the corresponding interface. The routes then appear under Static
	  Routes.
	======================================================================
	Keywords          : kbusage 
	Technology        : kbWinNTsearch kbWinNT400search kbWinNTSsearch kbWinNTS400search kbWinNTS400 kbAudDeveloper kbRRASNTSearch kbRRASNT400
	Version           : 4.0
	
	=============================================================================
	

{% endraw %}
