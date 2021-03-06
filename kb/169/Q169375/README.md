---
layout: page
title: "Q169375: STOP 0X0000007B on HP NetServer LH Systems"
permalink: /kb/169/Q169375/
---

## Q169375: STOP 0X0000007B on HP NetServer LH Systems

{% raw %}

	Article: Q169375
	Product(s): Microsoft Windows NT
	Version(s): WINNT:4.0
	Operating System(s): 
	Keyword(s): kbsetup
	Last Modified: 10-AUG-2001
	
	-------------------------------------------------------------------------------
	The information in this article applies to:
	
	- Microsoft Windows NT Workstation version 4.0 
	- Microsoft Windows NT Server version 4.0 
	-------------------------------------------------------------------------------
	
	SYMPTOMS
	========
	
	After installing Windows NT 4.0 on a HP NetServer LH, the system may fail to
	start up, producing a Blue Screen with a STOP 0x0000007B error message.
	
	CAUSE
	=====
	
	Windows NT Setup may have been allowed to auto-detect mass storage devices.
	Setup correctly detected an Adaptec controller using the Aic78xx.sys driver from
	the third setup disk. Using this driver may cause the system BIOS to report
	invalid configuration information to the system.
	
	RESOLUTION
	==========
	
	To resolve this problem, you must install the correct aic78xx driver. You can
	obtain the correct aic78xx driver from HP or from the Navigator CD. After you
	obtain the updated driver, perform the following steps that correspond to the
	file system you are using:
	
	On a FAT Partition
	------------------
	
	1. Use a startup disk to start the computer to a command prompt.
	
	2. Rename or delete the %Systemroot%\System32\Drivers\Aic78xx.sys driver and
	  replace it with the same file obtained from HP.
	
	On an NTFS Partition
	--------------------
	
	1. Create a Windows NT startup disk with the correct ARC path. For information
	  on how to do this, see the following article in the Microsoft Knowledge Base:
	
	  Q119467 Creating a Boot Disk for an NTFS or FAT Partition
	
	2. After Windows NT has started, replace the Aic78xx.sys driver as stated for a
	  FAT partition above.
	
	STATUS
	======
	
	This problem occurs when you use Microsoft Windows NT version 4.0 and the
	Aic78xx.sys driver.
	
	MORE INFORMATION
	================
	
	The third-party products discussed here are manufactured by vendors independent
	of Microsoft; we make no warranty, implied or otherwise, regarding these
	products' performance or reliability.
	
	Additional query words: prodnt boot floppy
	
	======================================================================
	Keywords          : kbsetup 
	Technology        : kbWinNTsearch kbWinNTWsearch kbWinNTW400 kbWinNTW400search kbWinNT400search kbWinNTSsearch kbWinNTS400search kbWinNTS400
	Version           : WINNT:4.0
	Issue type        : kbprb
	
	=============================================================================
	

{% endraw %}
