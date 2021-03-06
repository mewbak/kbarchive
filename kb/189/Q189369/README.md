---
layout: page
title: "Q189369: Using CD-ROM Drive at MS-DOS Prompt to Reinstall Windows 95"
permalink: /kb/189/Q189369/
---

## Q189369: Using CD-ROM Drive at MS-DOS Prompt to Reinstall Windows 95

{% raw %}

	Article: Q189369
	Product(s): Microsoft Windows 95.x Retail Product
	Version(s): WINDOWS:95
	Operating System(s): 
	Keyword(s): kbenv kbhw kbsetup win95 kbHardware
	Last Modified: 27-JUL-2001
	
	-------------------------------------------------------------------------------
	The information in this article applies to:
	
	- Microsoft Windows 95 
	-------------------------------------------------------------------------------
	
	SUMMARY
	=======
	
	This article describes how to gain access to your CD-ROM drive at an MS-DOS
	prompt so you can copy the Windows 95 Setup files from the CD-ROM drive to a
	hard disk and then reinstall Windows 95. You may need to do this if:
	
	- You are unable to start Windows 95 in normal mode.
	
	- You do not have access to real-mode CD-ROM drivers.
	
	- Your CD-ROM drive was functional using protected-mode drivers before you
	  became unable to start Windows 95 in normal mode.
	
	- You want to reinstall Windows 95.
	
	MORE INFORMATION
	================
	
	To gain access to your CD-ROM drive, copy the Windows 95 Setup files from this
	CD-ROM drive to a hard disk, and then reinstall Windows 95, use the following
	steps:
	
	1. Restart the computer. When you see the "Starting Windows 95" message, press
	  F8, and then choose Safe Mode Command Prompt Only on the Startup menu.
	
	2. At the command prompt, type the following lines, pressing ENTER after each
	  line:
	
	  "cd windows
	  edit system.ini" (without the quotation marks)
	
	3. Locate the "shell=explorer" line in the [Boot] section of the System.ini
	  file.
	
	4. Change the line to read "shell=command.com" (without the quotation marks).
	
	5. Press ALT+F, and then press S. Press ALT+F, and then press X.
	
	6. Restart the computer.
	
	  NOTE: After your computer restarts, it should operate in an MS-DOS virtual
	  machine with access to the CD-ROM drive, but this may not work correctly. If
	  you are unable to access the CD-ROM drive, you may need to enable the
	  Mscdex.exe line in the Autoexec.bat file or you may need to install real-mode
	  drivers. To enable the Mscdex.exe line, use any text editor (such as Edit) to
	  open the Autoexec.bat file in the root folder of drive C. Look for a line
	  containing "Mscdex.exe," and then remove the "REM" statement at the beginning
	  of the line. Save the changes, quit the text editor, and then restart your
	  computer. For information about how to install real-mode drivers for your
	  CD-ROM drive, contact the manufacturer of your CD-ROM drive or computer, or
	  view the documentation included with your CD-ROM drive or computer.
	
	7. At the command prompt, type the following commands, pressing ENTER after each
	  command:
	
	  "md flat
	  <CD-ROM drive letter>:
	  cd win95
	  copy *.* c:\flat" (without the quotation marks)
	
	8. At the command prompt, type the following commands, pressing ENTER after each
	  command:
	
	  "c:
	  cd windows
	  edit system.ini" (without the quotation marks)
	
	9. Locate the "shell=command.com" line in the [Boot] section of the System.ini
	  file.
	
	10. Change the line to read "shell=explorer.exe" (without the quotation marks).
	
	11. Press ALT+F, and then press S. Press ALT+F, and then press X.
	
	12. Press CTRL+ALT+DELETE, and then click Shut Down.
	
	13. Restart your computer, press the F8 key at the "Starting Windows 95"
	  message, and then choose "Safe Mode Command Prompt Only".
	
	14. At the command prompt, type the following commands, pressing ENTER after
	  each command:
	
	  "cd\
	  cd flat
	  setup" (without the quotation marks)
	
	15. Follow the instructions on the screen to finish installing Windows 95.
	
	======================================================================
	Keywords          : kbenv kbhw kbsetup win95 kbHardware 
	Technology        : kbWin95search kbZNotKeyword3
	Version           : WINDOWS:95
	Issue type        : kbhowto
	
	=============================================================================
	

{% endraw %}
