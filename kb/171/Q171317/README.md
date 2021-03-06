---
layout: page
title: "Q171317: Upgrade WinNT to 4.0 May Hang with Trident 94XX AGI Video Card"
permalink: /kb/171/Q171317/
---

## Q171317: Upgrade WinNT to 4.0 May Hang with Trident 94XX AGI Video Card

{% raw %}

	Article: Q171317
	Product(s): Microsoft Windows NT
	Version(s): WinNT:3.51,4.0
	Operating System(s): 
	Keyword(s): kb3rdparty kbsetup
	Last Modified: 09-AUG-2001
	
	-------------------------------------------------------------------------------
	The information in this article applies to:
	
	- Microsoft Windows NT Workstation version 4.0 
	- Microsoft Windows NT Server version 4.0 
	-------------------------------------------------------------------------------
	
	SYMPTOMS
	========
	
	When you upgrade from Windows NT version 3.51 to Windows NT version 4.0, the
	system may stop responding on the subsequent restart while entering the
	graphical user interface (GUI) portion of setup. When you use a Trident
	TGUI94XXAGI video adapter and the Windows NT 3.51 driver from Trident, the
	system may stop responding after carrying out the NTDETECT command while the
	operating system loader displays the following message:
	
	  Microsoft (r) Windows NT TM Version 4.0 (build 1381). 1 System Processor
	  [32 MB Memory]
	
	No error messages are displayed.
	
	CAUSE
	=====
	
	The Windows NT 3.51 video driver supplied by Trident for the AGI series video
	adapter, Agi.sys, is not compatible with Windows NT 4.0.
	
	RESOLUTION
	==========
	
	Windows NT Installed on FAT Drive
	---------------------------------
	
	If Windows NT is installed on a FAT drive, perform the following steps:
	
	1. Start the computer with another operating system (such as MS-DOS, Microsoft
	  Windows 95, or Microsoft Windows 3.x) and then rename Agi.sys in
	  \Winnt35\System32\Drivers.
	
	2. Copy Vga.sys to Agi.sys. Restart the computer and the upgrade will finish.
	
	3. Contact Trident to obtain the updated Windows NT 4.0 video drivers. Then
	  install them on your computer.
	
	-or-
	
	Continue to use the standard VGA driver.
	
	Windows NT Installed on NTFS Drive
	----------------------------------
	
	If Windows NT is installed on an NTFS partition, perform the following steps:
	
	1. Install a parallel copy of Windows NT 4.0 into a different directory and then
	  rename AGI.SYS in \Winnt35\system32\drivers.
	
	2. Copy VGA.SYS to AGI.SYS.
	
	3. Restart the computer and the upgrade will finish.
	
	4. Contact Trident to obtain the updated Windows NT 4.0 video drivers. Then
	  install them on your computer.
	
	-or-
	
	Continue to use the standard VGA driver.
	
	MORE INFORMATION
	================
	
	The third-party products discussed here are manufactured by vendors independent
	of Microsoft; we make no warranty, implied or otherwise, regarding these
	products' performance or reliability.
	======================================================================
	Keywords          : kb3rdparty kbsetup 
	Technology        : kbWinNTsearch kbWinNTWsearch kbWinNTW400 kbWinNTW400search kbWinNT400search kbWinNTSsearch kbWinNTS400search kbWinNTS400
	Version           : WinNT:3.51,4.0
	Issue type        : kbprb
	
	=============================================================================
	

{% endraw %}
