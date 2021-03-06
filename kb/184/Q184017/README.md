---
layout: page
title: "Q184017: Administrators Can Display Contents of Service Account Passwords"
permalink: /kb/184/Q184017/
---

## Q184017: Administrators Can Display Contents of Service Account Passwords

{% raw %}

	Article: Q184017
	Product(s): Microsoft Windows NT
	Version(s): winnt:3.51,4.0
	Operating System(s): 
	Keyword(s): kbWinNT400sp4fix
	Last Modified: 10-AUG-2001
	
	-------------------------------------------------------------------------------
	The information in this article applies to:
	
	- Microsoft Windows NT Workstation versions 3.51, 4.0 
	- Microsoft Windows NT Server versions 3.51, 4.0 
	- Microsoft Windows NT Server, Enterprise Edition version 4.0 
	- Microsoft BackOffice Small Business Server version 4.0 
	- Microsoft Windows NT Server version 4.0, Terminal Server Edition 
	-------------------------------------------------------------------------------
	
	
	SYMPTOMS
	========
	
	A program is available on the Internet that allows a local Administrator, with
	full control of a Windows NT system, to use APIs published in the Win32 software
	development kit (SDK) for Windows NT to display the contents of security
	information stored by the Local Security Authority (LSA) in a form called LSA
	Secrets. LSA Secrets are used to store information such as the passwords for
	service accounts used to start services under an account other than local
	System.
	
	CAUSE
	=====
	
	This is by design. Members of the local Administrators groups are trusted users
	that have the ability to access any information that can also be accessed by the
	operating system itself.
	
	
	RESOLUTION
	==========
	
	Note that the fix listed below does not change the behavior in which LSA secrets
	are available to local administrators. Administrators have access to data
	including LSA secrets. This fix provides improved protection for LSA secrets
	against attacks noted below that do not involve accounts with administrative
	priviledges.
	
	To resolve this problem, obtain the latest service pack for Windows NT 4.0 or
	Windows NT Server 4.0, Terminal Server Edition. For additional information,
	please see the following article in the Microsoft Knowledge Base:
	
	  Q152734 How to Obtain the Latest Windows NT 4.0 Service Pack
	
	
	The updates in this Windows NT 4.0 hotfix provide the following additional
	protection for the LSA Secret data:
	
	- Additional encryption for the LSA Secrets, which provides protection for this
	  information when stored on backup tapes, the Emergency Repair Disk, or other
	  registry backups. For maximum protection, you should also enable the System
	  Key option. For information on System Key (Syskey.exe) functionality, please
	  refer to the following article in the Microsoft Knowledge Base:
	
	  ARTICLE-ID: Q143475
	  TITLE : Windows NT System Key Permits Strong Encryption of the SAM
	
	- The value of the LSA private data is not returned to remote clients over the
	  network.
	
	- Calls to the Win32 APIs will not return LSA private data used for service
	  accounts and other system components to unauthorized applications (non-system
	  components).
	
	- This update includes a change to the privilege needed to open the Security
	  Event log. Applications that open this log on systems running with this
	  update installed fail unless the security privilege (SE_SECURITY_NAME) is
	  enabled.
	
	For more information on this change, please see the following article in the
	Microsoft Knowledge Base:
	
	  ARTICLE-ID: Q188855
	  TITLE : Security Privilege Must be Enabled to View Security Event Log
	
	Before You Apply The Hotfix
	---------------------------
	
	Because this hotfix makes a modification to the on-disk storage of the LSA data
	information, Microsoft does not recommend that it be uninstalled. Perform the
	following steps to ease the transition back to a pre-LSA2-fix configuration in
	case you experience problems with the hotfix:
	
	1. Perform a Full System Backup.
	
	2. Run Rdisk /s. Using the /s command-line switch with Rdisk.exe causes the
	  Sam._ and Security._ databases to be copied to the %Systemroot%\Repair
	  folder.
	
	3. Create a temporary folder under the %Systemroot% folder called Lsabackout.
	
	4. Copy the following files from the %Systemroot\System32 folder to the
	  %Systemroot%\Lsabackout folder as they are updated by LSA2-fix:
	
	  Eventlog.dll
	  Lsasrv.dll
	  Msaudite.dll
	  Msv1_0.dll
	  Netcfg.dll
	  Samlib.dll
	  Samsrv.dll
	  Services.exe
	  Srvmgr.exe
	  Xactsrv.dll
	
	5. Create an updated Emergency Repair Disk (ERD) which updates the on-disk SAM
	  and Registry information in the %Systemroot%\System32\Config folder.
	
	NOTE: This hotfix supersedes the fix referred to in the following articles in the
	Microsoft Knowledge Base:
	
	  ARTICLE-ID: Q154087
	  TITLE : Access Violation in LSASS.EXE Due to Incorrect Buffer Size
	
	  ARTICLE-ID: Q174205
	  TITLE : LSASS May Use a Large Amount of Memory on a Domain Controller
	
	  ARTICLE-ID: Q129457
	  TITLE : Anonymous Connections May Be Able to Obtain the Password Policy
	
	This hotfix has been posted as Lsa2fixi.exe (x86) and Lsa2fixa.exe (Alpha).For
	your convenience, the English version of this post-SP3 hotfix has been posted to
	the following Internet location. However, Microsoft recommends that you install
	Windows NT 4.0 Service Pack 4 to correct this problem.
	
	NOTE: An updated version of this hotfix was posted on July 20, 1998 and provides
	an additional security level to systems running Windows NT 4.0 Service Pack 3.
	
	  ftp://ftp.microsoft.com/bussys/winnt/winnt-public/fixes/usa/NT40/hotfixes-postSP3/lsa2-fix/
	
	NOTE: The above link is one path; it has been wrapped for readability.
	
	If you run Systems Management Server on systems where this hotfix is applied, the
	SNMP Event Log Extension Agent (Snmpelea) generates the following Event ID 3007
	error:
	
	  Error opening event log file Security.
	  Log will not be processed.
	  Return code from OpenEventLog is 1314.
	
	The SNMP Event Log Extension Agent requires an update to manage the security
	event log. To resolve the SNMP Event Log Extension Agent problem, please see the
	following article in the Microsoft Knowledge Base:
	
	  ARTICLE-ID: Q183770
	  TITLE : SMS: Snmpelea Unable to Open Security Event Log
	
	
	Windows NT 3.51
	---------------
	
	A hotfix for Windows NT 3.51 is not available at this time.
	
	MORE INFORMATION
	================
	
	If you experience problems with this hotfix, perform the following steps to
	restore the system to its original configuration before applying the hotfix:
	
	1. Perform a full system backup including the registry. This backup set should
	  only be necessary if the following steps fail.
	
	2. Rename the following files the %Systemroot%\System32 folder that were
	  replaced by the hotfix:
	
	  Eventlog.dll
	  Lsasrv.dll
	  Msaudite.dll
	  Msv1_0.dll
	  Netcfg.dll
	  Samlib.dll
	  Samsrv.dll
	  Services.exe
	  Srvmgr.exe
	  Xactsrv.dll
	
	3. Copy the original versions of these system files from the
	  \%Systemroot%\Lsabackout folder to the %Systemroot%\System32 folder.
	
	4. Restart the computer using the installation disks and select the option to
	  repair the system.
	
	5. Deselect all options except Inspect Registry Files and then continue.
	
	6. Press the ESC key to indicate you wish to use the on-disk repair information.
	
	7. Press ENTER to repair.
	
	8. Click only Security (security policy) and SAM (user accounts database).
	
	WARNING: Using Registry Editor incorrectly can cause serious problems that may
	require you to reinstall your operating system. Microsoft cannot guarantee that
	problems resulting from the incorrect use of Registry Editor can be solved. Use
	Registry Editor at your own risk.
	
	For information about how to edit the registry, view the "Changing Keys And
	Values" Help topic in Registry Editor (Regedit.exe) or the "Add and Delete
	Information in the Registry" and "Edit Registry Data" Help topics in
	Regedt32.exe. Note that you should back up the registry before you edit it.
	
	1. Start Registry Editor (Regedt32.exe) and delete the key from:
	
	  HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows NT
	  \CurrentVersion\Hotfix
	
	  NOTE: The above registry key is one path; it has been wrapped for readability.
	
	
	STATUS
	======
	
	Microsoft has confirmed this to be a problem in Windows NT 4.0 and Windows NT
	Server 4.0, Terminal Server Edition. This problem was first corrected in Windows
	NT 4.0 Service Pack 4.0 and Windows NT Server 4.0, Terminal Server Edition
	Service Pack 4.
	
	Additional query words: 3.51 4.00
	
	======================================================================
	Keywords          : kbWinNT400sp4fix 
	Technology        : kbWinNTsearch kbWinNTWsearch kbWinNTW400 kbWinNTW400search kbWinNT351search kbWinNT400search kbWinNTW351search kbWinNTW351 kbWinNTSsearch kbWinNTSEntSearch kbWinNTSEnt400 kbWinNTS400search kbWinNTS400 kbWinNTS351 kbNTTermServ400 kbNTTermServSearch kbWinNTS351search kbAudDeveloper kbSBServSearch kbSBServ400
	Version           : winnt:3.51,4.0
	Hardware          : ALPHA x86
	Issue type        : kbbug
	Solution Type     : kbfix
	
	=============================================================================
	

{% endraw %}
