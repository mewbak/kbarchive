---
layout: page
title: "Q126226: Writer: TrueType Fonts Not Showing Under Letterizer Tool"
permalink: /kb/126/Q126226/
---

## Q126226: Writer: TrueType Fonts Not Showing Under Letterizer Tool

{% raw %}

	Article: Q126226
	Product(s): Microsoft Home Kids Products
	Version(s): WINDOWS:1.0,1.1,1.1a
	Operating System(s): 
	Keyword(s): 
	Last Modified: 29-NOV-1999
	
	-------------------------------------------------------------------------------
	The information in this article applies to:
	
	- Microsoft Creative Writer for Windows, versions 1.0, 1.1, 1.1a 
	-------------------------------------------------------------------------------
	
	SYMPTOMS
	========
	
	When you choose the Letterizer Tool in Creative Writer, only Impact, Lucida
	Sans, Lucida Handwriting, Lucida Blackletter, and Stencil are listed. Any other
	Windows TrueType fonts installed on the computer are not displayed in the
	Creative Writer font list.
	
	RESOLUTION
	==========
	
	To resolve the problem in Windows 3.x, use the following steps:
	
	1. In Program Manager, run Control Panel from the Main group.
	
	2. Double-click the Fonts icon.
	
	3. Select the TrueType fonts. Choose the Remove button.
	
	4. You receive a dialog box that says
	
	  Are you sure you want to remove the <name> (TrueType) font?
	
	  where <name> is the name of the TrueType font.
	
	  Make sure that the Delete Font File From Disk check box is not selected.
	  Choose the Yes To All button.
	
	5. Choose the Add button in the Fonts dialog box. You receive an Add Fonts
	  dialog box that by default selects your Windows directory.
	
	6. In the Windows directory, select the SYSTEM subdirectory (font files are
	  stored in the SYSTEM subdirectory). Choose the Select All button, then choose
	  OK. After the fonts are installed, close Control Panel.
	
	7. In the Main group in Program Manager, open File Manager.
	
	8. Locate the MSKIDS\SHARED directory. Select the MSKIDS.INF file, and delete
	  it. When you run Creative Writer again, it re-creates the MSKIDS.INF file.
	
	After following these steps, all Windows TrueType fonts should appear in Creative
	Writer when you choose the Letterizer Tool.
	
	
	Additional query words: kids fonts mskids mczee win wm_writer missing display true type empty blank appear max tt 1.10a
	
	======================================================================
	Keywords          :  
	Technology        : kbHomeProdSearch kbCreativeWriter100 kbCreativeWriter110 kbCreativeWriter110a
	Version           : WINDOWS:1.0,1.1,1.1a
	
	=============================================================================
	

{% endraw %}
