---
layout: page
title: "Q153629: FP: No Prompt for User Name and Password on IIS Web"
permalink: /kb/153/Q153629/
---

## Q153629: FP: No Prompt for User Name and Password on IIS Web

{% raw %}

	Article: Q153629
	Product(s): Word Front Page
	Version(s): ; WINDOWS:1.1
	Operating System(s): 
	Keyword(s): kbdta
	Last Modified: 04-OCT-2001
	
	-------------------------------------------------------------------------------
	The information in this article applies to:
	
	- Microsoft FrontPage 97 for Windows with Bonus Pack 
	- Microsoft FrontPage for Windows 1.1 
	-------------------------------------------------------------------------------
	
	For a Microsoft FrontPage 2000 version of this article, see Q208628.
	
	For a Microsoft FrontPage 98 version of this article, see Q194037.
	
	SYMPTOMS
	========
	
	When you use FrontPage Explorer to open an existing Web or to create a new Web
	on a Microsoft Internet Information Server, you are not prompted to enter a user
	name or password.
	
	CAUSE
	=====
	
	This problem may occur for any of the following reasons:
	
	- You are running the Internet Information Server on a FAT partition of the
	  Windows NT file system.
	
	  -or-
	
	- The IUSR account has permission to the _vti_adm and _vti_aut directories on a
	  Windows NT NTFS partition.
	
	  -or-
	
	- The user name and password have been cached in FrontPage Explorer (therefore,
	  you will not be prompted for these when you open or create subsequent Webs).
	
	NOTE: If you are using FrontPage 97 and the Microsoft Internet Information
	Server, you may not be prompted for a user name and password if the user name
	and password that you used to log on to Windows is the same as the password you
	use to log on to the Web server and IIS is configured to use NTLM
	authentication.
	
	WORKAROUND
	==========
	
	To work around this behavior, use the method appropriate to your installation of
	FrontPage.
	
	Method 1: If FrontPage Is Running on a FAT Partition
	----------------------------------------------------
	
	Configure the Internet Information Server as specified in the Readme.iis file
	that accompanies the FrontPage Server Extensions for IIS.
	
	Method 2: If FrontPage Is Running on an NTFS Partition
	------------------------------------------------------
	
	The NTFS file permissions may be set incorrectly.
	
	For additional information, please see the following article in the Microsoft
	Knowledge Base:
	
	  Q162144 Minimum NTFS File Permission Requirements
	
	Additional query words: file allocation table
	
	======================================================================
	Keywords          : kbdta 
	Technology        : kbFrontPageSearch kbFrontPage1xSearch kbFrontPage97Search kbZNotKeyword3 kbFrontPage110
	Version           : :; WINDOWS:1.1
	Hardware          : x86
	Issue type        : kbprb
	
	=============================================================================
	

{% endraw %}
