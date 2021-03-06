---
layout: page
title: "Q136624: Windows 95 Hangs When Starting on Canon Innova 10c Notebook"
permalink: /kb/136/Q136624/
---

## Q136624: Windows 95 Hangs When Starting on Canon Innova 10c Notebook

{% raw %}

	Article: Q136624
	Product(s): Microsoft Windows 95.x Retail Product
	Version(s): 95
	Operating System(s): 
	Keyword(s): win95
	Last Modified: 17-DEC-2000
	
	-------------------------------------------------------------------------------
	The information in this article applies to:
	
	- Microsoft Windows 95 
	-------------------------------------------------------------------------------
	
	SYMPTOMS
	========
	
	When you install Windows 95 on a Canon Innova 10c notebook computer, your
	computer may stop responding (hang) when Windows 95 tries to restart the
	computer the first time.
	
	If you can complete the Setup process, and you choose to enable Advanced Power
	Management (APM) support, your computer may hang when you start Windows 95, or
	when you click the Suspend command on the Start menu.
	
	CAUSE
	=====
	
	The BIOS in your computer is not completely compatible with Windows 95.
	
	
	RESOLUTION
	==========
	
	If you are attempting to install Windows 95 and your computer has stopped
	responding when attempting to restart for the first time, follow these steps to
	work around the problem:
	
	1. Start Windows 95 in Safe mode. To do so, restart your computer, press the F8
	  key when you see the "Starting Windows 95" message, and then choose Safe Mode
	  from the Startup menu.
	
	2. Use the right mouse button to click My Computer, and then click Properties on
	  the menu that appears.
	
	3. Click the Device Manager tab.
	
	4. Double-click the Hard Disk Controllers branch to expand it, and then
	  double-click the hard disk controller installed in your computer.
	
	5. Click the Original Configuration (Current) check box to clear it, and then
	  click OK.
	
	If you have enabled APM support and your computer hangs when Windows 95 attempts
	to start, or when you click Suspend on the Start menu, follow these steps to
	work around the problem:
	
	1. If you cannot start Windows 95 normally, start it in Safe mode. To do so,
	  follow the instructions in step 1 above.
	
	2. Use the right mouse button to click My Computer, and then click Properties on
	  the menu that appears.
	
	3. Click the Device Manager tab.
	
	4. Double-click the System Devices branch to expand it, and then double- click
	  Advanced Power Management Support.
	
	5. On the Settings tab, click the Enable Power Management Support check box to
	  clear it.
	
	6. Click OK.
	
	7. Use any text editor (such as Notepad) to open the System.ini file in the
	  Windows folder. Disable the following line in the [386Enh] section of the
	  file by placing a semicolon (;) at the beginning of the line:
	
	  device=*vpowerd
	
	8. Save and then close the System.ini file, and then restart your computer.
	
	You may want to contact your computer manufacturer to inquire about a possible
	BIOS upgrade that resolves these problems.
	
	MORE INFORMATION
	================
	
	This behavior may also occur on a Mitsubishi ApricotNote NS M3472 computer with
	an ACER BIOS and Advanced Power Management version 1.0. The resolution in this
	article also applies to this computer.
	
	======================================================================
	Keywords          : win95 
	Technology        : kbWin95search kbZNotKeyword3
	Version           : 95
	
	=============================================================================
	

{% endraw %}
