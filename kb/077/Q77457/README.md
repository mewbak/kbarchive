---
layout: page
title: "Q77457: Accepting Keyboard Input in Batch Files"
permalink: /kb/077/Q77457/
---

## Q77457: Accepting Keyboard Input in Batch Files

{% raw %}

	Article: Q77457
	Product(s): Microsoft Disk Operating System
	Version(s): MS-DOS:3.x,4.x,5.x,6.0,6.2,6.21,6.22
	Operating System(s): 
	Keyword(s): 
	Last Modified: 17-DEC-2000
	
	-------------------------------------------------------------------------------
	The information in this article applies to:
	
	- Microsoft MS-DOS operating system versions 3.1, 3.2, 3.21, 3.3, 3.3a, 4.0, 4.01, 5.0, 5.0a, 6.0, 6.2, 6.21, 6.22 
	-------------------------------------------------------------------------------
	
	SUMMARY
	=======
	
	The MS-DOS batch language facility does not provide a means for you to provide
	input to control program flow. All information input from you must be entered
	from the command line.
	
	By using a short program created with the MS-DOS Debug utility, you can provide
	information at the time of batch file execution.
	
	NOTE: Although the Debug program works with MS-DOS 6.0 or 6.2, it is not
	required. If you are using MS-DOS 6.0 or 6.2, type "help choice" (without the
	quotation marks) at the MS-DOS command prompt for more information.
	
	MORE INFORMATION
	================
	
	The Debug program at the end of this article will wait for you to input a
	character from the keyboard and set the value of "errorlevel" equal to the ASCII
	code value of the character entered. For a list of ASCII characters and their
	associated values, see the ANSI.SYS section in your MS-DOS manual.
	
	Most keyboard characters are represented by only one code. However, the functions
	and ALT key combinations send two codes: a zero, followed by another code. The
	REPLY.COM program will set "errorlevel" equal to the second code passed. For
	example, the F8 key sends a zero followed by the value 66. This will be
	interpreted by REPLY.COM as the character "B," which has an ASCII value of 66.
	
	REPLY.COM can be used within batch files to allow user input to control the flow
	of the program. For example, the following AUTOEXEC.BAT file allows you to
	determine whether or not to install a mouse driver during startup:
	
	  @Echo off
	  path=C:\DOS
	  :Ask
	  Echo Install Mouse Driver (y/n)?
	  Reply
	  If errorlevel 121 if not errorlevel 122 goto install
	  If errorlevel 89 if not errorlevel 90 goto install
	  If errorlevel 110 if not errorlevel 111 goto NoMouse
	  If errorlevel 78 if not errorlevel 79 goto NoMouse
	  goto ask
	  :install
	  c:\mouse\mouse
	  :NoMouse
	  cls
	  ver
	
	For more information about using the "errorlevel" environment variable, query on
	the following word in the Microsoft Knowledge Base:
	
	  " errorlevel " (without the quotation marks)
	
	REPLY.COM
	---------
	
	To create REPLY.COM, enter the text listed in the Instruction column. Press ENTER
	after each instruction. Do not enter the text listed in the Comment column; it
	is for your reference.
	
	          Instruction     Comment
	          -----------     -------
	
	           DEBUG       Executes MS-DOS DEBUG utility
	-A 100                  Begin assembling instructions at memory location
	100
	xxxx:0100   MOV AH,08   Get character input without echo
	xxxx:0102   INT 21      Perform MS-DOS service
	xxxx:0104   CMP AL,0    Compare AL with zero
	xxxx:0106   JNZ 010A    If lead zero, get second code of character
	xxxx:0108   INT 21      Perform MS-DOS service
	xxxx:010A   MOV AH,4C   Terminate process with return code
	xxxx:010C   INT 21      Perform MS-DOS service
	xxxx:010E   <ENTER>
	-rcx
	CX 0000
	:e
	-n REPLY.COM
	-w
	Writing 000E bytes
	-q
	
	REFERENCES
	==========
	
	"Supercharging MS-DOS," pages 97-98, by Van Wolverton, Microsoft Press, 1989,
	1991 (Updated for Version 4).
	
	Additional query words: 6.22 3.20 3.30 3.30a 4.00 4.00a 5.00 5.00a 6.00 6.20
	
	======================================================================
	Keywords          :  
	Technology        : kbMSDOSSearch kbMSDOS321 kbMSDOS400 kbMSDOS320 kbMSDOS330a kbMSDOS621 kbMSDOS622 kbMSDOS620 kbMSDOS600 kbMSDOS310 kbMSDOS500 kbMSDOS330 kbMSDOS401 kbMSDOS500a
	Version           : MS-DOS:3.x,4.x,5.x,6.0,6.2,6.21,6.22
	
	=============================================================================
	

{% endraw %}
