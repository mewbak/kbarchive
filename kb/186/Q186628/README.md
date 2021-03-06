---
layout: page
title: "Q186628: Performance Tuning CPU Use for 16, 32-bit Windows Applications"
permalink: /kb/186/Q186628/
---

## Q186628: Performance Tuning CPU Use for 16, 32-bit Windows Applications

{% raw %}

	Article: Q186628
	Product(s): Microsoft Windows NT
	Version(s): 4.0
	Operating System(s): 
	Keyword(s): 
	Last Modified: 11-DEC-2001
	
	-------------------------------------------------------------------------------
	The information in this article applies to:
	
	- Microsoft Windows NT Server version 4.0, Terminal Server Edition 
	-------------------------------------------------------------------------------
	
	IMPORTANT: This article contains information about editing the registry.
	Before you edit the registry, make sure you understand how to restore it if
	a problem occurs. For information about how to do this, view the "Restoring
	Registry Key" Help topic in Regedit.exe or the "Restoring a Registry Key"
	Help topic in Regedt32.exe.
	
	SUMMARY
	=======
	
	Windows 16-bit or 32-bit applications may use too much CPU time, even when they
	are idle (no keyboard or mouse events). Terminal Server's registry can be
	modified to detect this behavior, suspending application execution and allowing
	other applications to use the CPU, making multitasking much more efficient.
	
	MORE INFORMATION
	================
	
	WARNING: Using Registry Editor incorrectly can cause serious problems that may
	require you to reinstall your operating system. Microsoft cannot guarantee that
	problems resulting from the incorrect use of Registry Editor can be solved. Use
	Registry Editor at your own risk.
	
	For information about how to edit the registry, view the "Changing Keys And
	Values" Help topic in Registry Editor (Regedit.exe) or the "Add and Delete
	Information in the Registry" and "Edit Registry Data" Help topics in
	Regedt32.exe. Note that you should back up the registry before you edit it. If
	you are running Windows NT, you should also update your Emergency Repair Disk
	(ERD).
	
	To modify the registry, perform the following steps:
	
	1. Run Regedt32.exe and locate the following key:
	
	  HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows
	  NT\CurrentVersion\TerminalServer\Compatibility\Applications
	
	NOTE: The above registry key is one path; it has been wrapped for readability.
	
	2. Double-click the Applications subkey to reveal several pre-defined settings.
	  Select SETUP under the Applications subkey. The following values are
	  displayed on the right side of the Registry Editor window:
	
	FirstCountMsgQPeeksSleepBadApp:REG_DWORD:0xf
	
	Flags:REG_DWORD:0x8
	MsgQBadAppSleepTimeInMillisec:REG_DWORD:0
	NthCountMsgQPeeksSleepBadApp:REG_DWORD:0x5
	
	3. With the Setup subkey highlighted, click to select Save Key from the Registry
	  pull-down menu. The filename can be anything, such as Setup.reg. When the
	  setup values are saved, create a subkey for your application.
	
	4. With the Applications subkey highlighted, click to select Add Key on the Edit
	  pull-down menu. Set the Key Name field to the name of the executable in
	  question, minus the extension. For example, for the application Myapp.exe,
	  type "MYAPP" (without the quotation marks) in the Key Name field. Leave the
	  Class field blank. Click OK.
	
	5. To copy the values from the Setup subkey, click to select your new subkey
	  (for example, MYAPP) and click to select Restore from the Registry pull-down
	  menu. Click to choose the filename you created in Step 3. Click Yes when the
	  warning dialog box displays. Your new application subkey now has the same
	  values as the Setup subkey.
	
	6. You must now fine-tune the values for your application. The values are
	  described in the following sections:
	
	Bad Application Registry Values
	-------------------------------
	
	The default values for the bad application settings are:
	
	FirstCountMsgQPeeksSleepBadApp = 0xf
	MsgQBadAppSleepTimeInMillisec = 0x1
	NthCountMsgQPeeksSleepBadApp = 0x5
	Flags: 0x8
	
	FirstCountMsgQPeeksSleepBadApp is the number of times the application must query
	the message queue before Terminal Server decides that it is ill-behaved.
	Decrease this value to put the application to sleep more often, so it uses less
	CPU time.
	
	MsgQBadAppSleepTimeInMillisec is the number of milliseconds the application is
	suspended when Terminal Server has decided that it is ill-behaved. Increase this
	value to use less CPU time. If this value is zero, polling detection is
	disabled.
	
	NthCountMsgQPeeksSleepBadApp - After the application is determined to be "bad,"
	this setting is the number of times the application must query the message queue
	before it is suspended again. Decrease this value to use less CPU time.
	
	Flags is set to a value corresponding to the type of Windows application. Valid
	values are:
	
	0x4 for Win16 applications only
	0x8 for Win32 applications only
	0xC for either Win16 or Win32 applications
	
	Bad Application Settings
	------------------------
	
	All values are expressed in hexadecimal numbers. When changing the values, first
	click the Decimal button and input the decimal value. For instance, if you want
	the MsgQBadAppSleepTimeInMillisec value to be set to 200 milliseconds, perform
	the following steps:
	
	1. Double-click MsgQBadAppSleepTimeInMillisec.
	
	2. Click the Decimal radio button.
	
	3. Enter "200" (without the quotation marks) in the Data field.
	
	4. Click OK.
	
	The value is now converted to 0xc8, the hexadecimal equivalent of 200 decimal.
	NOTES:
	
	- To modify polling detection for MS-DOS applications, use the DOSKBD utility.
	
	For additional information, click the article number below to view the article in
	the Microsoft Knowledge Base:
	
	  Q186560 Modifying DOS Application Keyboard Polling Detection
	
	- When tuning these parameters, make sure Performance Monitor is running. These
	  parameters will affect the amount of CPU used by an application. These
	  parameters usually trade off CPU usage versus application responsiveness.
	
	
	Additional query words:
	
	======================================================================
	Keywords          :  
	Technology        : kbWinNTsearch kbWinNT400search kbWinNTSsearch kbWinNTS400search kbNTTermServ400 kbNTTermServSearch
	Version           : :4.0
	Issue type        : kbinfo
	
	=============================================================================
	

{% endraw %}
