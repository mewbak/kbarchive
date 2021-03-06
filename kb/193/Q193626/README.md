---
layout: page
title: "Q193626: HOWTO: Overriding Default Right-Click Behavior in Editor Window"
permalink: /kb/193/Q193626/
---

## Q193626: HOWTO: Overriding Default Right-Click Behavior in Editor Window

{% raw %}

	Article: Q193626
	Product(s): Microsoft FoxPro
	Version(s): WINDOWS:5.0,5.0a,6.0
	Operating System(s): 
	Keyword(s): 
	Last Modified: 13-AUG-1999
	
	-------------------------------------------------------------------------------
	The information in this article applies to:
	
	- Microsoft Visual FoxPro for Windows, versions 5.0, 5.0a, 6.0 
	-------------------------------------------------------------------------------
	
	SUMMARY
	=======
	
	If you open an Editor window in Visual FoxPro 5.0 or later, right-clicking in
	the Editor window displays a context menu. You may choose to use the Editor
	window in a run-time application and you may want to override the default menu
	to either not display a menu or to display a custom menu.
	
	MORE INFORMATION
	================
	
	The editor is normally invoked with the MODIFY COMMAND <filename>, MODIFY
	FILE <filename>, or MODIFY MEMO <memo fieldname> command. In a
	run-time application, you are most likely to use MODIFY FILE or MODIFY MEMO.
	
	The way to override the default right-click behavior involves associating a
	command or procedure with an ON KEY LABEL RIGHTCLICK, and issuing a WAIT command
	to remove the right-click and cause the default menu not to display.
	
	Overriding the Default Menu with No Menu
	----------------------------------------
	
	The following code sample demonstrates how to make no menu appear with the
	right-click:
	
	     LOCAL lcFileName
	
	     * Name a temporary text file.
	     lcFileName = SYS(3)+'.txt'
	
	     * Store its contents to the clipboard.
	     _CLIPTEXT = "Line 1"+CHR(13)+"Line 2"+CHR(13)
	     KEYBOARD '{ctrl+v}{ctrl+w}'
	
	     * Paste the contents into the file, then save and close the file.
	     MODIFY FILE (lcFileName)
	
	     * Set the RIGHTMOUSE behavior to the WAIT command to remove right-click.
	     ON KEY LABEL RIGHTMOUSE WAIT ""
	     MODIFY FILE (lcFileName)
	     DELETE FILE (lcFileName)
	
	     * Reset the default RIGHTMOUSE behavior
	     ON KEY LABEL RIGHTMOUSE
	
	Overriding Default Menu With A Custom Menu
	------------------------------------------
	
	The following code sample demonstrates how to make a custom menu appear with the
	right-click. The custom menu contains the normal edit menu functionality of
	Undo, Redo, Copy, Paste, Cut, and Select All.
	
	     LOCAL lcFileName
	
	     * Name a temporary text file.
	     lcFileName = SYS(3)+'.txt'
	
	     * Store its contents to the clipboard.
	     _CLIPTEXT = "Line 1"+CHR(13)+"Line 2"+CHR(13)
	     KEYB '{ctrl+v}{ctrl+w}'
	
	     * Paste the contents into the file, then save and close it.
	     MODIFY FILE (lcFileName)
	
	     * Set the RIGHTMOUSE behavior.
	     ON KEY LABEL RIGHTMOUSE MenuFunction()
	     MODIFY FILE (lcFileName)
	     DELETE FILE (lcFileName)
	
	     * Reset the default RIGHTMOUSE behavior.
	     ON KEY LABEL RIGHTMOUSE
	
	     FUNCTION MenuFunction()
	        WAIT ""  && This removes the right-click.
	        IF POPUP('shortcut')
	           * Let's make sure we don't display the menu twice.
	           DEACTIVATE POPUP shortcut
	        ELSE
	           DEFINE POPUP shortcut shortcut RELATIVE
	           DEFINE BAR _MED_UNDO OF shortcut PROMPT "\<Undo" ;
	              MESSAGE "Undoes the last command or action"
	           DEFINE BAR _MED_REDO OF shortcut PROMPT "Re\<do" ;
	              MESSAGE "Repeats the last command or action"
	           DEFINE BAR 3 OF shortcut PROMPT "\-"
	           DEFINE BAR _MED_COPY OF shortcut PROMPT "\<Copy" ;
	              MESSAGE "Copies the selection onto the Clipboard"
	           DEFINE BAR _MED_PASTE OF shortcut PROMPT "\<Paste" ;
	              MESSAGE "Pastes the contents of the Clipboard"
	           DEFINE BAR _MED_CUT OF shortcut PROMPT "Cu\<t" ;
	              MESSAGE "Removes the selection and places it on the Clipboard"
	           DEFINE BAR _MED_SLCTA OF shortcut PROMPT "Se\<lect All" ;
	              MESSAGE "Selects all text or items in the current window"
	        ENDIF
	        * Activate it where we clicked.
	        ACTIVATE POPUP shortcut AT MROW(),MCOL()
	        * Deactivate it after we click outside of the menu.
	        DEACTIVATE POPUP shortcut
	        RETURN
	     ENDFUNC
	
	REFERENCES
	==========
	
	(c) Microsoft Corporation 1998. All Rights Reserved. Contributions by Jim
	Saunders, Microsoft Corporation
	
	
	Additional query words: kbvfp500 kbvfp500a kbvfp600
	
	======================================================================
	Keywords          :  
	Technology        : kbVFPsearch kbAudDeveloper kbVFP500 kbVFP600 kbVFP500a
	Version           : WINDOWS:5.0,5.0a,6.0
	Issue type        : kbhowto
	
	=============================================================================
	

{% endraw %}
