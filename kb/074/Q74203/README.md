---
layout: page
title: "Q74203: MS-DOS 5 Can't Install On An IBM AT With Plus Hardcard II XL"
permalink: /kb/074/Q74203/
---

## Q74203: MS-DOS 5 Can't Install On An IBM AT With Plus Hardcard II XL

{% raw %}

	Article: Q74203
	Product(s): Microsoft Disk Operating System
	Version(s): MS-DOS:5.0
	Operating System(s): 
	Keyword(s): 
	Last Modified: 23-NOV-1999
	
	-------------------------------------------------------------------------------
	The information in this article applies to:
	
	- Microsoft MS-DOS operating system version 5.0 
	-------------------------------------------------------------------------------
	
	SUMMARY
	=======
	
	Microsoft MS-DOS 5 Upgrade cannot install on an IBM AT 6 MHz machine with a BIOS
	dated 1984 or earlier, and a Plus Hardcard II XL. To install MS-DOS, you must
	obtain a patch from Plus Development, then you must reinstall the Plus Hardcard
	II XL.
	
	MORE INFORMATION
	================
	
	To install MS-DOS 5.0, do the following:
	
	1. Contact Plus development and get an MS-DOS 5.0 patch for this configuration.
	
	2. Remove the hardcard from the computer.
	
	3. Install MS-DOS 5.0.
	
	4. Use the FORMAT /S commmand to format a floppy disk as an MS-DOS 5.0 system
	  disk.
	
	5. Copy SYS.COM to the floppy disk, then remove the floppy disk from the disk
	  drive and turn off the computer.
	
	6. Put the hardcard back into the computer.
	
	7. Turn the computer on, booting off of the hard drive.
	
	8. Put the System disk created in step 4 in drive A and the Patch disk in drive
	  B.
	
	9. Switch to drive B, then type:
	
	  " ATPLUS A: " (without the quotation marks)
	
	  NOTE: This procedure places the patch on the System disk.
	
	10. Restart the computer from drive A (using the System disk).
	
	11. From the System disk on the A drive, type "SYS C:" (without the quotation
	  marks).
	
	12. Remove the floppy disk from drive A, then restart your computer from drive
	  C.
	
	IMPORTANT: The Uninstall program cannot work because of how the patch affects the
	IO.SYS and the MSDOS.SYS files.
	
	Make sure that the device line for the hardcard in the CONFIG.SYS file reads as
	follows:
	
	     DEVICE=ATDOSXL.SYS
	
	If CONFIG.SYS cannot find this file, the following error message is displayed:
	
	  A serious disk error has occurred
	
	If ATDOSXL.SYS does not exist in the root directory of C:, correct the DEVICE=
	statement so that it points to the directory where this file resides. Use the
	following syntax:
	
	  device=[drive:] \ [directory] \ atdosxl.sys
	
	For more information, contact Plus Development.
	
	The products included here are manufactured by vendors independent of Microsoft;
	we make no warranty, implied or otherwise, regarding these products' performance
	or reliability.
	
	Additional query words: 3rdparty 5.00 errmsg
	
	======================================================================
	Keywords          :  
	Technology        : kbMSDOSSearch kbMSDOS500
	Version           : MS-DOS:5.0
	
	=============================================================================
	

{% endraw %}
