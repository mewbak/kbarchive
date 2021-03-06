---
layout: page
title: "Q94259: PC DB: Err Msg: Could Not Find Mail System Database"
permalink: /kb/094/Q94259/
---

## Q94259: PC DB: Err Msg: Could Not Find Mail System Database

{% raw %}

	Article: Q94259
	Product(s): Microsoft Mail For PC Networks
	Version(s): WINDOWS:2.1,3.0
	Operating System(s): 
	Keyword(s): 
	Last Modified: 28-OCT-1999
	
	-------------------------------------------------------------------------------
	The information in this article applies to:
	
	- Microsoft Mail for PC Networks, versions 2.1, 3.0 
	-------------------------------------------------------------------------------
	
	SYMPTOMS
	========
	
	When Microsoft Mail cannot find the postoffice database that stores the mail
	messages, one of the following error messages may be displayed:
	
	MS-DOS clients (all versions) and Mail Administrator program version 2.1:
	
	  Could not find mail system database.
	
	Mail Administrator program version 3.0:
	
	  Could not find mail system data files on drive 'M:'
	
	Windows client version 3.0:
	
	  Mail could not connect to your Mail server. The Mail server path in your
	  MSMAIL.INI file is missing or invalid.
	
	Windows client version 2.1:
	
	  The mail database cannot be reached. The server that contains the database
	  needs to be running, and you need to either connect to it on drive M: or
	  state its location in the WIN.INI. Please see your network administrator if
	  you need assistance.
	
	CAUSE
	=====
	
	The above error messages indicate that the mail program cannot read the database
	files. Typically, this occurs because of one or more of the following five
	reasons:
	
	1. A previously installed security feature is overriding other, more current
	  settings, or the MAIL.DAT file is not in the WINDOWS\SYSTEM directory.
	
	2. The mail program is looking for the files in the wrong location.
	
	3. The drive where the mail program is looking does not exist because it has not
	  been mapped or mounted.
	
	4. The person trying to access the postoffice database does not have sufficient
	  rights or privileges to the MAILDATA directories.
	
	5. The MASTER.GLB file does not exist, is hidden, or is locked open.
	
	RESOLUTION
	==========
	
	Following are resolutions for each of the five above causes:
	
	1. Check for the existence of a MAIL.DAT file on both the server and the
	  workstation. If you find any occurrences, delete them or rename them to
	  MAILDAT.OLD. If any MAIL.DAT files exist, they can override all other
	  settings pointing to the postoffice database.
	
	  To locate any copies of MAIL.DAT from within Windows, use File Manager and
	  choose Search from the File menu.
	
	  To locate any copies of MAIL.DAT from the MS-DOS prompt, run the following
	  command from the root directory:
	
	  attrib mail.dat /s
	
	  NOTE: For more information on advanced security and the MAIL.DAT file, see the
	  "Microsoft Mail 3.0 Administrator's Guide," pages 14-17, and 51.
	
	  To re-enable Advanced Security, either rerun setup for that workstation and
	  select Advanced Security, or if it had been previously renamed (to disable
	  AS), rename the file to MAIL.DAT in the WINDOWS\SYSTEM directory.
	
	2. 
	  a. Unless told otherwise, the ADMIN.EXE and MAIL.EXE programs for MS-DOS
	     assume that the current directory of drive M is the root of the database
	     (..\MAILDATA). If the database resides on another drive, add the -Dm
	     switch to the command line (where M is the alternative drive letter).
	
	     For example, use the following command if the current directory of drive R
	     is the root of the database:
	
	  admin -dr
	
	     Note: The current directory of the drive letter used must be the root of
	     the database (for example, ..\MAILDATA).
	
	     For example, in the list below, if the directory on the left is the current
	     directory when you run a Mail program, the Mail program will give you the
	     error message shown on the right:
	
	   Current Directory        Error Message
	   -----------------------------------------------------------------
	   M:\APPS\MAIL             Could not find mail system database
	   M:\APPS\MAIL\EXE         Could not find mail system database
	   M:\APPS\MAIL\DATA\LOG    Could not find mail system database
	   M:\APPS\MAIL\DATA        (Correct directory -- no error message)
	
	     You can verify that the root of the postoffice database is in the current
	     directory of the drive by changing to that drive and running the MS-DOS
	     DIR command. If the Mail database is there, you will see directories named
	     ATT, GLB, MBG, and so forth.
	
	     Following are examples of the commands used to map to the root of the
	     postoffice database for Novell and LAN Manager networks:
	
	   Novell
	   ------
	   map m:=<servername>/sys:apps\mail\data
	   map root r:=<Server>/vol1:maildata
	
	   LAN Manager
	   -----------
	   net use m: \\<servername>\maildata
	
	  b. The Windows workstation software also assumes the database is in the
	     current directory of drive M unless told otherwise. It does not require
	     that the directory be the current directory, but it does require that you
	     specify the full path to the postoffice database. In Mail for Windows,
	     version 3.0, this is done in the MSMAIL.INI file. In Mail for Window,
	     version 2.1, the setting is in the WIN.INI file. Usually, you can find
	     MSMAIL.INI and WIN.INI in your WINDOWS directory.
	
	     To specify the path to the postoffice database for Mail for Windows,
	     version 3.0, include a "ServerPath=" line in the [Microsoft Mail] section
	     of MSMAIL.INI. To do the same for Mail for Windows, version 2.1, include a
	     "Path=" line in the [Mail] section of WIN.INI. Following is an example of
	     each type of entry:
	
	   MSMAIL.INI (Mail for Windows, Version 3.0)
	   ------------------------------------------
	      [Microsoft Mail]
	      ServerPath=m:\apps\mail\data
	
	   WIN.INI (Mail for Windows, Version 2.1)
	   ---------------------------------------
	      [Mail]
	      Path=m:\apps\mail\data
	
	     Note: The system administrator can simplify Windows workstation
	     installations by using drive M as everyone's database mapping or by
	     editing the MSMAIL.INI file (Mail 3.0) located in the MAILEXE directory on
	     the server to include a standard "ServerPath=" line. Mail 2.1
	     administrators can create a WINMAIL.INI file containing a "Path=" line
	     (see the "Microsoft Mail 2.1 Administrator's Guide," pages 183-187).
	
	3. The settings in an INI file may appear correct, but the drive may not exist.
	  It may not have been mapped or mounted, or it may have been disconnected.
	  Verify that the drive and path is valid by using the MS-DOS DIR command.
	
	4. Following are examples of the rights needed on different file servers.
	
	  The rights needed for a Novell 3.11 server are as follows:
	
	      Rights       Directory
	      ------------------------------------------------------------------
	
	      [ RWCEM  ]   ..\MAILDATA directory
	      [ RWCEMF ]   ..\MAILDATA\KEY, \MAILDATA\FOLDERS, and
	                     \MAILDATA\CAL directories
	      [ R    F ]   ..\MAILEXE directory
	
	      R Read (Open and read files)
	      W Write (Open and write to the file)
	      C Create (Create a directory)
	      E Erase (Delete a directory or file)
	      M Modify (Change attributes or rename directory or file)
	      F File Scan (See the filename when viewing directory)
	
	  Note: Macintosh and OS/2 clients need File Scan (F) rights to the entire
	  database (..\MAILDATA).
	
	  The rights needed for a Novell 2.15 server are as follows:
	
	      Rights        Directory
	      ------------------------------------------------------------------
	
	      [ RWOCDM  ]   ..\MAILDATA directory
	      [ RW0CDMS ]   ..\MAILDATA\KEY & \MAILDATA\FOLDERS directories
	      [ R O   S ]   ..\MAILEXE directory
	
	      R Read
	      W Write
	      O Open
	      C Create
	      D Delete
	      M Modify
	      S Search
	
	  You can set up a Microsoft LAN Manager server with share level security or
	  user level security with the following permissions:
	
	      Rights        Directory
	      ------------------------------------------------------------------
	
	      RWCDA         ..\MAILDATA directory
	      R             ..\MAILEXE directory
	
	      R Read
	      W Write
	      C Create
	      D Delete
	      A Attribute
	
	5. If the MAILDATA\GLB\MASTER.GLB file does not exist, restore it from the
	  latest backup.
	
	  If it is hidden, make it viewable it by changing to the MAILDATA\GLB directory
	  and typing the following MS-DOS 5.0 command:
	
	  " attrib -h master.glb /s" (without the quotation marks)
	
	  If the file is locked open, close the file using whatever tools are available
	  on your network. The following are Novell and LAN Manager examples:
	
	  Novell
	
	  Console => Monitor => File Locking => Directory => File LAN
	  Manager
	
	  Net Admin => Status => Open Files => Select File => Close
	
	Additional query words: 2.10 3.00 permission Mail cannot connect to your server
	
	======================================================================
	Keywords          :  
	Technology        : kbMailSearch kbZNotKeyword3 kbMailPCN300 kbMailPCN210
	Version           : WINDOWS:2.1,3.0
	
	=============================================================================
	

{% endraw %}
