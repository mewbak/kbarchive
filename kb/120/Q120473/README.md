---
layout: page
title: "Q120473: Setup Hangs with Buslogic BT-946C on Powerstation/Powerserver"
permalink: /kb/120/Q120473/
---

## Q120473: Setup Hangs with Buslogic BT-946C on Powerstation/Powerserver

{% raw %}

	Article: Q120473
	Product(s): Microsoft Windows NT
	Version(s): 3.10 3.50 3.51 4.0
	Operating System(s): 
	Keyword(s): 
	Last Modified: 08-AUG-2001
	
	3.10 3.50 3.51 4.0
	
	WINDOWS
	
	kbsetup kbhw kb3rdparty
	
	-------------------------------------------------------------------------------
	The information in this article applies to:
	
	- Microsoft Windows NT Workstation versions 3.1, 3.5, 3.51, 4.0 
	- Microsoft Windows NT Advanced Server, version 3.1 
	- Microsoft Windows NT Server versions 3.5, 3.51, 4.0 
	-------------------------------------------------------------------------------
	
	SUMMARY
	=======
	
	If you have Micron Powerstation or Powerserver with Buslogic's BT-946C SCSI
	controller, Windows NT setup may hang without an error message while attempting
	to load Windows NT to complete the graphic portion of Setup.
	
	
	MORE INFORMATION
	================
	
	According to Micron and Buslogic these steps usually solve the problem:
	
	1. Press CTRL-B to go to Buslogic Auto Configuration.
	
	2. Select Configure Device Menu.
	
	3. Select Disconnection Option.
	
	4. Set "Disconnection on all ID's except 0 and 1" to YES.
	
	5. If these were already set this way you may need to toggle them, because some
	  hard drives do not support disconnection.
	
	Buslogic Product Support does not recommend permanently changing the controller
	configuration as indicated above unless there is only one SCSI device attached
	to the controller. The procedure may disable the functionality of SCSI devices
	on the SCSI chain during certain I/O actions carried out by the OS.
	
	If there are no scanning devices on this chain it is possible to Disable the SCAN
	MODE option, since this can cause problems with the installation of NT,
	according to Buslogic.
	
	If this does not solve the problem, go to the Buslogic Auto Configuration and
	verify that the IRQ pin is set to pin A (the default) on the Powerstations and
	Powerservers. On P90 models this should be set to pin C (the default); the
	adapter is installed next to the power supply. Then verify that the IRQ being
	used is set to 15 and that in the "Advanced Options" the BIOS is set to use
	4D8.
	
	Additionally Buslogic BIOS should be flashed to the most recent version (1.40E as
	of 9/4/96) since this solves most setup or operational problems related to NT
	3.51 and NT 4.0.
	
	These steps solve most of the setup hang problems with Windows NT. You can get
	more assistance by contacting the vendors listed below:
	
	- Buslogic technical support: (408) 970-1414
	
	- Buslogic BBS: (408)492-1984
	
	- Micron Technologies technical support: (208)465-3434
	
	The products discussed here are manufactured by Micron and Buslogic, vendors
	independent of Microsoft; we make no warranty, implied or otherwise, regarding
	the products' performance or reliability.
	
	Additional query words: prodnt hung stop vendor
	
	======================================================================
	Keywords          :  
	Technology        : kbWinNTsearch kbWinNTWsearch kbWinNTW400 kbWinNTW400search kbWinNT351search kbWinNT350search kbWinNT400search kbWinNTW350 kbWinNTW350search kbWinNTW351search kbWinNTW351 kbWinNTW310 kbWinNTSsearch kbWinNTS400search kbWinNTS400 kbWinNTS351 kbWinNTS350 kbWinNTAdvSerSearch kbWinNTAdvServ310 kbWinNTS351search kbWinNTS350search kbWinNT310Search kbWinNTW310Search
	Version           : 3.10 3.50 3.51 4.0
	
	=============================================================================
	

{% endraw %}
