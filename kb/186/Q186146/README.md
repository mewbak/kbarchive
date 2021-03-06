---
layout: page
title: "Q186146: Double-Clicking .reg File Will Not Add Extended ANSI Values"
permalink: /kb/186/Q186146/
---

## Q186146: Double-Clicking .reg File Will Not Add Extended ANSI Values

{% raw %}

	Article: Q186146
	Product(s): Microsoft Windows NT
	Version(s): WinNT:4.0
	Operating System(s): 
	Keyword(s): 
	Last Modified: 09-AUG-2001
	
	-------------------------------------------------------------------------------
	The information in this article applies to:
	
	- Microsoft Windows NT Server version 4.0 
	- Microsoft Windows NT Workstation version 4.0 
	- Microsoft Windows NT Server, Enterprise Edition version 4.0 
	-------------------------------------------------------------------------------
	
	SYMPTOMS
	========
	
	Extended ANSI values in a .reg files are not added to the registry.
	
	If you create a .reg file that contains any @=hex(2) values or you modify and
	existing .reg fil,e none of the extended ANSI values after the @=hex(2) value
	will be added to the registry.
	
	Example of a .reg file:
	
	     REGEDIT4
	
	     [HKEY_CLASSES_ROOT\aifffile\DefaultIcon]
	     @=hex(2):44,3a,5c,57,49,4e,4e,54,34,30,5c,53,79,73,74,65,6d,33,32,5c,
	     71,75,61,72,74,7a,2e,64,6c,6c,2c,2d,32,30,32,00
	     "AMovie.bak"="MPlayer.exe,2"
	
	Changing any of the ANSI codes after the @=kex(2) value and then double- clicking
	the .reg file will not yield any changes to the registry for that key; neither
	will running REGEDIT Test.reg.
	
	NOTE: You can create a .reg file by running REGEDIT, selecting the key you want
	to export, and then selecting Export Registry from the Registry menu.
	
	CAUSE
	=====
	
	This problem is a limitation with Regedit.exe
	
	RESOLUTION
	==========
	
	To work around this problem, export the key(s) you want to modify with the
	Windows NT Server 4.0 Resource Kit utilities Regdmp.exe and Regini.exe.
	
	For information about how to use REGDMP and REGINI, please refer to the Windows
	NT Server 4.0 Resource Kit documentation.
	
	STATUS
	======
	
	Microsoft has confirmed this to be a problem in Windows version 4.0. We are
	researching this problem and will post new information here in the Microsoft
	Knowledge Base as it becomes available.
	
	======================================================================
	Keywords          :  
	Technology        : kbWinNTsearch kbWinNTWsearch kbWinNTW400 kbWinNTW400search kbWinNT400search kbWinNTSsearch kbWinNTSEntSearch kbWinNTSEnt400 kbWinNTS400search kbWinNTS400
	Version           : WinNT:4.0
	Issue type        : kbbug
	
	=============================================================================
	

{% endraw %}
