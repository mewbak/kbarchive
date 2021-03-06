---
layout: page
title: "Q98642: Multimedia Err Msg: The Specified Device Is Not Open ..."
permalink: /kb/098/Q98642/
---

## Q98642: Multimedia Err Msg: The Specified Device Is Not Open ...

{% raw %}

	Article: Q98642
	Product(s): Microsoft Home Multimedia Titles
	Version(s): 1.0
	Operating System(s): 
	Keyword(s): 
	Last Modified: 08-NOV-2001
	
	-------------------------------------------------------------------------------
	The information in this article applies to:
	
	- Microsoft SoundBits 
	- Microsoft Bookshelf for Windows, 1991, 1992, 1993, 1994, 1995 editions 
	- Microsoft Bookshelf 1996-97 for Windows 
	- Microsoft Cinemania for Windows, 1992, 1993, 1994, 1995, 1996, 1997 editions 
	- Microsoft Encarta 1994 The Complete Multimedia Encyclopedia 
	- Microsoft Encarta 95 The Complete Interactive Multimedia Encyclopedia 
	- Microsoft Multimedia Stravinsky for Windows, version 1.0 
	-------------------------------------------------------------------------------
	
	SYMPTOMS
	========
	
	When you start one of the programs listed at the top of the article, you may
	receive the message:
	
	  The specified device is not open or is not recognized by MCI.
	
	If you choose Yes, SoundBits will continue to play sounds when you select .WAV
	files. These error messages will occur when you choose the SoundBits Browser
	icon or when you choose the Play Sound button in the Media Browser screen.
	
	When you try to play a sound in Encarta, Bookshelf, or Stravinsky, or play an
	animation that uses an .AVI file, you may receive one of the following
	messages:
	
	  Multimedia Viewer MCI
	  The specified device is not open or is not recognized by MCI.
	  device: WaveAudio
	
	-or-
	
	  File Name extension of the specified multimedia file is not associated with
	  any installed MCI device.
	
	If you choose Yes, the program will continue without sound capabilities.
	
	CAUSE
	=====
	
	These messages occur when the Windows [MCI] Sound driver is not installed or the
	WIN.INI [MCI Extensions] section is incorrect.
	
	RESOLUTION
	==========
	
	Verify that the Drivers option in Control Panel lists the [MCI] Sound driver. If
	the [MCI] Sound driver is listed, refer to the instructions, "To Verify the
	WIN.INI [MCI Extensions] Section." Otherwise, use the steps listed below, "To
	Install the MCI Sound Driver."
	
	How to Install the MCI Sound Driver
	-----------------------------------
	
	1. Choose the Drivers icon in Windows Control Panel.
	
	2. Choose the Add button.
	
	3. From the list of drivers that is displayed, select [MCI] Sound.
	
	4. Choose the OK button.
	
	[MCI] Sound should now be installed and listed in the Installed Drivers box.
	
	How to Verify the WIN.INI [MCI Extensions] Section
	--------------------------------------------------
	
	1. From the File menu in Program Manager, choose Run.
	
	2. Type WIN.INI.
	
	3. Choose the OK button.
	
	4. Select the Search menu.
	
	5. Choose Find.
	
	6. Type [mci extensions] and select Find Next.
	
	7. Choose Cancel on the Find dialog.
	
	8. Scroll down to view the [MCI Extensions] section and verify that the
	  following lines exist:
	
	     wav=Waveaudio
	     mid=Sequencer
	     avi=AVIVideo
	
	
	Additional query words: 1.00 multimedia multi media multi-media .wav wav wave start run open kbmm dev/drv sound wfw 3.10 3.11
	
	======================================================================
	Keywords          :  
	Technology        : kbHomeProdSearch kbHomeMMsearch kbEncartaSearch kbZNotKeyword kbBookshelfSearch kbSoundBitsSearch kbEncartaEncycSearch kbCineManiaSearch kbMMStravinsky kbBookShelf1996 kbBookShelf1997 kbSoundBits kbEncarta1995 kbEncartaEnCyc1994
	Version           : :1.0
	
	=============================================================================
	

{% endraw %}
