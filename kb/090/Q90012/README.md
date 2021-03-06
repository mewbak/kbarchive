---
layout: page
title: "Q90012: BUG: Friction and Factor PWB Switches do not work"
permalink: /kb/090/Q90012/
---

## Q90012: BUG: Friction and Factor PWB Switches do not work

{% raw %}

	Article: Q90012
	Product(s): Microsoft Programming Utilities
	Version(s): MS-DOS:2.1.49
	Operating System(s): 
	Keyword(s): kb16bitonly
	Last Modified: 23-DEC-1999
	
	-------------------------------------------------------------------------------
	The information in this article applies to:
	
	- Microsoft Programmer's Workbench for MS-DOS, version 2.1.49 
	-------------------------------------------------------------------------------
	
	SYMPTOMS
	========
	
	The Friction and Factor switches do not work in Programmer's WorkBench (PWB)
	version 2.1.49.
	
	RESOLUTION
	==========
	
	The Friction switch, together with the Factor switch, control how quickly PWB
	executes a fast function (see the "Environment and Tools" manual for information
	on the Fastfunc switch). A fast function is a PWB function whose action repeats
	rapidly when you hold down the associated key.
	
	On many computers, the keyboard repeat rate is much too fast by default. The
	intention of the Friction and Factor switches is to slow the keyboard repeat
	rate. These switches do not work in PWB 2.1.49.
	
	To adjust the keyboard rate, do the following:
	
	1. From the Options menu, choose Editor Settings.
	
	2. In the Editor Settings box, select the "text" option.
	
	3. Turn off all the Fastfunc settings in the Switch List box by toggling "on" to
	  "off." For example, you should see the editor setting:
	
	  Fastfunc: emacscdel on
	
	  This statement would normally allow the Friction and Factor switches to
	  control the speed of the BACKSPACE key assigned to the Emacscdel function.
	  Change this to:
	
	  " Fastfunc: emacscdel off" (without the quotation marks)
	
	By turning off Fastfunc settings, you will enable Windows or MS-DOS to set the
	key repeat rate.
	
	In Windows, you can adjust the key repeat rate with the keyboard icon in the
	control panel. This will affect all applications that run within Windows.
	
	If you are running MS-DOS outside of Windows, you can adjust the key repeat rate
	(also known as the typematic rate) by using the MODE command. For example, the
	MS-DOS command
	
	  mode con rate=1 delay=4
	
	specifies a rate of approximately two characters a second after a delay of 1
	second.
	
	STATUS
	======
	
	Microsoft has confirmed this to be a problem in Programmer's WorkBench version
	2.1.49.
	
	MORE INFORMATION
	================
	
	More information about setting keyboard repeat rates can be found in your MS-DOS
	manual (see MODE command) and in the "Microsoft Windows User's Guide" (see
	Control Panel).
	
	For more information about the Friction, Factor, and Fastfunc editor settings,
	see the "Environment and Tools" manual.
	
	Additional query words: 2.1.49 patch buglist2.1.49 cursor speed MASM C7
	
	======================================================================
	Keywords          : kb16bitonly 
	Technology        : kbAudDeveloper kbPWBSearch kbZNotKeyword3 kbPWB2149DOS
	Version           : MS-DOS:2.1.49
	
	=============================================================================
	

{% endraw %}
