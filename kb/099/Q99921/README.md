---
layout: page
title: "Q99921: HOWTO: Obtain Network User IDs from Within FoxPro"
permalink: /kb/099/Q99921/
---

## Q99921: HOWTO: Obtain Network User IDs from Within FoxPro

{% raw %}

	Article: Q99921
	Product(s): Microsoft FoxPro
	Version(s): 
	Operating System(s): 
	Keyword(s): kb3rdparty kbinterop kbnetwork kbvfp300 kbvfp500
	Last Modified: 30-JUL-1999
	
	-------------------------------------------------------------------------------
	The information in this article applies to:
	
	- Microsoft Visual FoxPro for Windows, versions 3.0, 5.0 
	- Microsoft FoxPro for Windows, versions 2.5, 2.5a 
	- Microsoft FoxPro for MS-DOS, versions 2.0, 2.5, 2.5a 
	-------------------------------------------------------------------------------
	
	SUMMARY
	=======
	
	To create unique filenames based on individual workstation operators, each
	user's identification (ID) must be obtained from the environment. Third-party
	API libraries that can interface with the network to provide this information
	are available; however, you can also use a batch file to capture the user IDs
	during interactive logins if only medium security is required.
	
	MORE INFORMATION
	================
	
	To capture a user ID, you must create a batch file with the same name as the
	command normally executed to log in. For example, if the normal method is to
	type LOGIN followed by an ID, the batch file would be named LOGIN.BAT.
	
	To create the file:
	
	1. In a text editor, create a new file with the appropriate name.
	
	2. Within the new file, type the following:
	
	  
	
	        SET USER=%1
	        CD NET
	        LOGIN %1
	
	3. Save the file in the root directory.
	
	The next time the machine completes startup, LOGIN and the user ID are typed in
	as normal, but at subsequent logins, the LOGIN.BAT file will intercept the user
	ID and assign the ID (passed as the first parameter on the command line, [%1])
	to the MS-DOS environment variable USER and then pass it to the original LOGIN
	program in the NET subdirectory.
	
	If the network LOGIN file is found through the MS-DOS PATH statement, place
	LOGIN.BAT in the root directory so that it will be executed first. However, if
	the AUTOEXEC.BAT selects the subdirectory where the original LOGIN program is
	found, you need to modify AUTOEXEC.BAT to find LOGIN.BAT first. For added
	security, you can mark the LOGIN.BAT file as Hidden with the MS-DOS ATTRIB
	command.
	
	Once the login is finished and FoxPro is running, the ID can be retrieved with
	the GETENV() function. The following commands demonstrate its usage:
	
	     usrname=GETENV("USER")
	
	The variable usrname contains the user ID.
	
	Additional query words: password logon
	
	======================================================================
	Keywords          : kb3rdparty kbinterop kbnetwork kbvfp300 kbvfp500 
	Technology        : kbVFPsearch kbAudDeveloper kbFoxproSearch kbZNotKeyword3 kbFoxPro200DOS kbFoxPro250DOS kbFoxPro250aDOS kbFoxPro250 kbFoxPro250a kbVFP300 kbVFP500
	Issue type        : kbhowto
	
	=============================================================================
	

{% endraw %}
