---
layout: page
title: "Q194819: PC DirSync: Import Hangs when Processing Srvtrans.glb"
permalink: /kb/194/Q194819/
---

## Q194819: PC DirSync: Import Hangs when Processing Srvtrans.glb

{% raw %}

	Article: Q194819
	Product(s): Microsoft Mail For PC Networks
	Version(s): WINDOWS:3.2,3.2a,3.5
	Operating System(s): 
	Keyword(s): 
	Last Modified: 20-MAY-2002
	
	-------------------------------------------------------------------------------
	The information in this article applies to:
	
	- Microsoft Mail for PC Networks, versions 3.2, 3.2a, 3.5 
	-------------------------------------------------------------------------------
	
	SYMPTOMS
	========
	
	
	Import stops responding (hangs) when processing Srvtrans.glb on all requestors.
	MS-DOS Import displays the following error message:
	
	  Memory allocation error. Cannot load command, system halted.
	
	If you use the Import.exe program with Windows NT (using the bound version), the
	following error message will be displayed instead:
	
	  An OS/2 program caused a protection violation. The program will be
	  Terminated.
	
	If you are using the OS/2 version under OS/2, a Trap D error will occur.
	
	CAUSE
	=====
	
	Improperly formatted modify transactions caused memory to become corrupt and
	return the above errors.
	
	RESOLUTION
	==========
	
	A supported fix that corrects this problem is now available from Microsoft, but
	has not been fully regression tested and should be applied only to systems
	experiencing this specific problem.
	
	To resolve this problem, contact Microsoft Product Support Services to obtain the
	fix. For a complete list of Microsoft Product Support Services phone numbers and
	information on support costs, please go to the following address on the World
	Wide Web:
	
	  http://support.microsoft.com/default.aspx?scid=fh;EN-US;CNTACTMS
	
	The English version of this fix should have the following file attributes or
	later:
	
	  File Name    Version
	  --------------------
	  Import.exe   3.5.30
	
	This hotfix has been posted to the following Internet location as Dirsy2k.exe:
	
	  ftp://ftp.microsoft.com/bussys/mail/pcmail-public/All-Y2K/
	
	
	STATUS
	======
	
	Microsoft has confirmed this to be a problem in Microsoft Mail for PC Networks
	versions 3.2, 3.2a, and 3.5.
	
	MORE INFORMATION
	================
	
	Import.exe was changed to ignore these improperly formatted transactions and
	return "Transaction has no effect" to the screen and the Dirsync.log file.
	
	Additional query words:
	
	======================================================================
	Keywords          :  
	Technology        : kbMailSearch kbZNotKeyword3 kbMailPCN320 kbMailPCN320a kbMailPCN350
	Version           : WINDOWS:3.2,3.2a,3.5
	Issue type        : kbbug
	Solution Type     : kbfix
	
	=============================================================================
	

{% endraw %}
