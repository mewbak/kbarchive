---
layout: page
title: "Q247732: Age of Empires II: Game Slows Down or Becomes Choppy"
permalink: /kb/247/Q247732/
---

## Q247732: Age of Empires II: Game Slows Down or Becomes Choppy

{% raw %}

	Article: Q247732
	Product(s): Microsoft Home Games
	Version(s): WINDOWS:2.0
	Operating System(s): 
	Keyword(s): kbenv kbui aoe kbimu msgame
	Last Modified: 06-AUG-2002
	
	-------------------------------------------------------------------------------
	The information in this article applies to:
	
	- Microsoft Age of Empires II: The Age of Kings, version 2.0 
	-------------------------------------------------------------------------------
	
	SYMPTOMS
	========
	
	While you play a random map game or a scenario in a campaign in Microsoft Age of
	Empires II: The Age of Kings, the game may slow down or become extremely choppy
	after you play for a few minutes.
	
	RESOLUTION
	==========
	
	To resolve this issue, install the latest update for Age of Empires II: Age of
	Kings. The latest update, Microsoft Age of Empires II: The Age of Kings 2.0a
	Update, includes performance enhancements that are designed to make the game run
	faster.
	
	To download the Age of Kings 2.0a Update, visit the following Microsoft Web
	site:
	
	  http://www.microsoft.com/games/age2/downloads.htm
	
	If the issue continues to occur:
	
	1. Quit all programs that are running on your computer.
	
	2. Click Start, point to Settings, and then click Control Panel.
	
	3. Double-click Add/Remove Programs.
	
	4. On the Install/Uninstall tab, click Microsoft Age of Empires II, and then
	  click Add/Remove.
	
	5. Follow the instructions on the screen to remove Age of Empires II.
	
	6. Empty the Temp folder. To do this, use the appropriate method for your
	  version of Microsoft Windows.
	
	Microsoft Windows 95:
	
	  a. Click Start, point to Programs, and then click MS-DOS Prompt.
	
	  b. At the command prompt, type "set" (without the quotation marks), and then
	     press ENTER.
	
	  c. Note the path on the "TEMP=" line.
	
	     By default, the path on the "TEMP=" line points to the following folder
	
	  <drive>:\Windows\Temp
	
	     where <drive> is the drive letter of the hard disk on which Windows
	     95 is installed.
	
	  d. At the command prompt, type the following lines, pressing ENTER after you
	     type each line
	
	  <drive>:
	  cd \<path>
	
	     where <drive> is the drive letter from the path you noted on the
	     "TEMP=" line, and <path> is the path you noted on the "TEMP=" line.
	
	  e. If the Temp folder exists, proceed to the next step.
	
	     If the Temp folder does not exist, type the following lines at the command
	     prompt, pressing ENTER after you type each line:
	
	  md \<path>
	  cd \<path>
	
	     where <path> is the path you noted on the "TEMP=" line.
	
	  f. At the command prompt, type "del *.tmp" (without the quotation marks), and
	     then press ENTER. If you are prompted to confirm the file deletion, press
	     Y.
	
	  g. At the command prompt, type "exit" (without the quotation marks), and then
	     press ENTER.
	
	Microsoft Windows 98:
	
	  a. Click Start, point to Programs, point to Accessories, point to System
	     Tools, and then click Disk Cleanup.
	
	  b. In the Drives box, click the hard disk on which Windows 98 is installed,
	     and then click OK.
	
	  c. In the "Files to delete" box, click to select the "Temporary files" check
	     box.
	
	     NOTE: Click to clear the check boxes for files that you do not want to
	     delete.
	
	  d. Click OK, and then click Yes.
	
	7. Click Start, point to Programs, point to Accessories, point to System Tools,
	  and then click ScanDisk.
	
	8. In the "Select the drive(s) you want to check for errors" box, click
	  <drive> (C:), where <drive> is the volume name of the hard disk.
	
	  If multiple hard disks are installed in your computer, press and hold down the
	  SHIFT key as you click to highlight all hard disks in the list.
	
	9. Click to select the "Automatically fix errors" check box.
	
	10. Click Standard, and then click Start.
	
	11. When ScanDisk is finished, click Close.
	
	12. Click Start, point to Programs, point to Accessories, point to System Tools,
	  and then click Disk Defragmenter.
	
	13. In the "Which drive do you want to defragment?" box, click Drive C, and then
	  click OK.
	
	  Repeat this step for all other hard disks in the list.
	
	14. Reinstall Age of Empires II.
	
	
	STATUS
	======
	
	Microsoft has confirmed that this is a problem in Microsoft Age of Empires II:
	The Age of Kings, version 2.0.
	
	Additional query words: 2.00 msgame aok aoe aoe2 aoeii hang lock freeze drag
	
	======================================================================
	Keywords          : kbenv kbui aoe kbimu msgame 
	Technology        : kbHomeProdSearch kbGamesSearch kbAOESearch kbAOE2Kings
	Version           : WINDOWS:2.0
	Issue type        : kbbug
	Solution Type     : kbpending
	
	=============================================================================
	

{% endraw %}
