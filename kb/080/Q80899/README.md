---
layout: page
title: "Q80899: Windows 3.1 Application Compatibility (part 4 of 7)"
permalink: /kb/080/Q80899/
---

## Q80899: Windows 3.1 Application Compatibility (part 4 of 7)

{% raw %}

	Article: Q80899
	Product(s): Microsoft Windows Software Development Kit
	Version(s): WINDOWS:3.1
	Operating System(s): 
	Keyword(s): kb16bitonly
	Last Modified: 06-NOV-1999
	
	-------------------------------------------------------------------------------
	The information in this article applies to:
	
	- Microsoft Windows Software Development Kit (SDK) 3.1 
	-------------------------------------------------------------------------------
	
	SUMMARY
	=======
	
	Application Compatibility Document for Windows 3.1
	--------------------------------------------------
	
	Due to the amount of information in this document, it has been broken into seven
	pieces. To find all seven pieces of this document and the Windows 3.1
	Compatibility Test checklist, query this knowledge base on the words:
	
	  " prod(winsdk) and 31compattest " (without the quotation marks)
	
	PARAMETER VALIDATION
	--------------------
	
	Windows strictly checks parameters passed to its functions before using them. In
	a Windows version 3.0 application, Windows works around many validation errors
	and lets the function or application continue to function. In a Windows version
	3.1 application, many of these errors cause the functions to fail, and the
	developer must ensure that structures and parameters are passed correctly.
	
	For example, in Windows version 3.0, if an application passes NULL as the
	hInstance parameter to CreateWindowEx, Windows maps the handle to the stack
	segment. In Windows version 3.1, the function returns an error value.
	
	The SDK release notes describe this in more detail. In some cases, the system may
	reject valid parameters incorrectly and cause applications to misbehave.
	Microsoft plans to correct any such occurrences.
	
	UNDELETED OBJECT NOTIFICATIONS
	------------------------------
	
	In Windows version 3.1, any GDI or USER object left allocated when an application
	terminates results in a warning to the debug terminal. Windows version 3.1 does
	not automatically free these objects; the application must free them. These
	warnings usually imply a memory leakage; running and terminating an offending
	application eventually uses up all available memory.
	
	In some cases applications (and DLLs) allocate objects that are intended to stay
	around longer than the application that created them. This occurs frequently in
	shared DLLs that share GDI objects such as bitmaps and brushes among their many
	clients. In such cases, ignore the warnings at the debug terminal.
	
	Potential Problem
	-----------------
	
	Applications can eventually use up available memory, which seriously degrades
	system performance.
	
	Test
	----
	
	Use the Program Manager to check memory usage before and after running your
	application. Follow these steps:
	
	1. Choose the About command in Program Manager's Help menu. Record the amount of
	  available memory and resources.
	
	2. Run your application and carry out enough tasks to ensure that one or more
	  objects are created. Terminate your application.
	
	3. Choose the About command again and compare available memory and resources. Be
	  sure these values have not dropped.
	
	4. Repeat this procedure several times, and check available memory and resources
	  each time.
	
	MENU IMPLEMENTATION
	-------------------
	
	Windows version 3.1 has enhanced menu management. In particular, the
	TrackPopupMenu function allows additional parameters, and Windows stores
	application menu data in a separate heap, expanding the number of windows that
	may exist.
	
	In Windows version 3.0 applications, Windows sends a WM_COMMAND message using the
	SendMessage function. In Windows version 3.1 applications, Windows sends the
	message using the PostMessage function, preventing the potential for overflowing
	a stack when dealing with pop-up menus.
	
	REGISTERCLASS
	-------------
	
	In Windows version 3.0, Windows fails to free the window-class background brush
	properly when deleting the class. In Windows version 3.1, Windows frees the
	brush when either a Windows version 3.0 or 3.1 application terminates.
	
	Potential Problem
	-----------------
	
	A multiple-instance application that deletes the background brush may
	unintentionally delete a brush when other instances of the application are
	running.
	
	TOPMOST WINDOW
	--------------
	
	A new window attribute allows a window to be placed on top of all other windows,
	even when the owning application is not active. If multiple applications have
	topmost windows, the topmost window is ordered the same as owning applications.
	
	Also, a topmost window, its owners, and all windows it owns stay together as
	windows are moved around. Thus, if you bring an owned dialog window to the top,
	its owner is also brought forward so that it stays immediately below the dialog
	box.
	
	Potential Problem
	-----------------
	
	Applications that depend on being able to have windows of other applications
	between their main window and a dialog box may encounter problems. For example,
	a Setup program that starts Notepad and then brings up a dialog box causes
	Notepad to be positioned behind the dialog box owner. The solution is to create
	the dialog box without an owner (a window may not be owned by a window of
	another application).
	
	Potential Problem
	-----------------
	
	Any application that relies on having an unobstructed client area when active may
	encounter problems because the active window cannot be guaranteed to be on top.
	Thus, the active window may not have a rectangular clipping region because a
	topmost window may be on top of it. Calling BitBlt with a window or screen DC as
	the source (which is not recommended in any case) may copy bits belonging to the
	topmost window.
	
	Tests
	-----
	
	1. Examine your application code, and be sure there are no dependencies on
	  client area visibility when your application is active.
	
	2. Start the clock, and set it to be the topmost window. Run your application
	  and several others. Use ALT+TAB to switch between applications, and be sure
	  your application repaints correctly.
	
	Additional query words: 3.10 no32bit
	
	======================================================================
	Keywords          : kb16bitonly 
	Technology        : kbAudDeveloper kbWin3xSearch kbSDKSearch kbWinSDKSearch kbWinSDK310
	Version           : WINDOWS:3.1
	
	=============================================================================
	

{% endraw %}
