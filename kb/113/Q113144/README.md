---
layout: page
title: "Q113144: PC WSPlus: Schedule+ Schdupd.exe Update Available"
permalink: /kb/113/Q113144/
---

## Q113144: PC WSPlus: Schedule+ Schdupd.exe Update Available

{% raw %}

	Article: Q113144
	Product(s): Microsoft Schedule+ for Windows
	Version(s): WINDOWS:1.0a
	Operating System(s): 
	Keyword(s): kbgraphxlinkcritical
	Last Modified: 13-JUN-2001
	
	-------------------------------------------------------------------------------
	The information in this article applies to:
	
	- Microsoft Schedule+ for Windows, version 1.0a 
	-------------------------------------------------------------------------------
	
	SUMMARY
	=======
	
	Microsoft provides a replacement for the Schdist.exe file that is included with
	version 1.0a of Microsoft Schedule+ for Windows.
	
	The following file is available for download from the Microsoft Download Center:
	
	  DownloadDownload Schdupd.exe now
	  (http://download.microsoft.com/download/splus10win/Update/1.0a.2/WIN/EN-US/Schdupd.exe)
	
	Schdupd.exe contains the following files:
	
	  Schdist.exe  (194,154 byte)
	  Readme.txt
	
	Release Date: Jun-6-1994
	
	For additional information about how to download Microsoft Support files, click
	the article number below to view the article in the Microsoft Knowledge Base:
	
	  Q119591 How to Obtain Microsoft Support Files from Online Services
	
	Microsoft used the most current virus detection software available on the date of
	posting to scan this file for viruses. Once posted, the file is housed on secure
	servers that prevent any unauthorized changes to the file.
	
	MORE INFORMATION
	================
	
	This update corrects the following problems:
	
	- When multiple Mail for PC Networks postoffices have similar network and
	  postoffice names, the Schedule Distribution program (Schdist.exe) may not
	  fully validate the entire <network>\<postoffice> name address to
	  which the free/busy times are addressed.
	
	- Trap D errors occur under OS/2 after Schedule+ processes two non- Schedule+
	  messages.
	
	- Trap D errors occur under OS/2 or under the OS/2 subsystem of Windows NT
	  while the Admin.prf file is being updated.
	
	- The program fails to apply changes from PowerCore's Schedule/DOS on the third
	  request.
	
	- The Schdist.exe program does not import free/busy times via an SMTP gateway.
	  The line length for word wrapping is too long for Schedule Distribution
	  messages and, as a result, some encapsulated gateways rewrap the message.
	  This causes the Schdist program to reject the message because of an improper
	  format. The line length previously set at 82 (80 characters of data plus 2
	  characters for the terminator) was changed to 78.
	
	NOTE: If Schedule+ is interacting with the IBM PROFS calendar system, version
	3.4a of the PROFS Host should be used. Version 3.4 of the PROFS Host still wraps
	messages at 80 characters and will not function with this new version of
	Schdist.exe. After you download Schdupd.exe to a new folder, run it (by typing
	"schdupd" at the MS-DOS prompt) to extract the contents of the file. You should
	receive the following files:
	
	To Update Your Schdist.exe File
	-------------------------------
	
	At the MS-DOS command prompt, type the following and press ENTER
	
	  copy <path>:\schdist.exe <destination>
	
	where <path> is the drive and folder where you ran the self- extracting
	Schdupd.exe file and <destination> is the drive and folder where your
	Schdist.exe file currently resides. For example, if you ran the self- extracting
	file from the TEST folder on drive D, and your Schdist.exe file is located in
	the Mailexe folder on drive C, type the following command:
	
	  copy d:\test\schdist.exe c:\mailexe
	
	NOTE: Schdist.exe typically resides on the computer dedicated to performing
	schedule distribution. The Schedule+ Install.exe program places Schdist.exe in
	the path specified for the Admin files during installation. The default path is
	to the Adminsch folder on drive C of the computer where Install.exe is executed.
	Schdist.exe can also be installed to the postoffice server in the Mail
	executables folder. Make sure you update all copies of Schdist.exe.
	
	
	Additional query words: schedule plus 1.00a wga
	
	======================================================================
	Keywords          : kbgraphxlinkcritical 
	Technology        : kbScheduleSearch kbSchedule100a
	Version           : WINDOWS:1.0a
	
	=============================================================================
	

{% endraw %}
