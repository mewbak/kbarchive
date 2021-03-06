---
layout: page
title: "Q151585: HOWTO: Use _crtBreakAlloc to Debug a Memory Allocation"
permalink: /kb/151/Q151585/
---

## Q151585: HOWTO: Use _crtBreakAlloc to Debug a Memory Allocation

{% raw %}

	Article: Q151585
	Product(s): Microsoft C Compiler
	Version(s): WINNT:4.0,4.1,4.2,5.0;
	Operating System(s): 
	Keyword(s): kbCRT kbDebug kbide kbVC kbVC400 kbVC410 kbVC420 kbVC500 kbVC600
	Last Modified: 31-JUL-2001
	
	-------------------------------------------------------------------------------
	The information in this article applies to:
	
	- The Integrated Debugger, included with:
	   - Microsoft Visual C++, 32-bit Editions, versions 4.0, 4.1 
	   - Microsoft Visual C++, 32-bit Enterprise Edition, version 4.2 
	   - Microsoft Visual C++, 32-bit Professional Edition, version 4.2 
	   - Microsoft Visual C++, 32-bit Enterprise Edition, version 5.0 
	   - Microsoft Visual C++, 32-bit Professional Edition, version 5.0 
	   - Microsoft Visual C++, 32-bit Enterprise Edition, version 6.0 
	   - Microsoft Visual C++, 32-bit Professional Edition, version 6.0 
	   - Microsoft Visual C++, 32-bit Learning Edition, version 6.0 
	-------------------------------------------------------------------------------
	
	SUMMARY
	=======
	
	When tracking down memory leaks using the debug C-Runtime (CRT), it is often
	useful to set a breakpoint immediately before allocating the memory that causes
	the leak. By setting _crtBreakAlloc at either compile time or run-time, you can
	cause a user-defined breakpoint at a specific point of memory allocation.
	
	MORE INFORMATION
	================
	
	When tracking memory leaks with Debug-CRT functions, such as
	_CrtDumpMemoryLeaks, an allocation number enclosed in braces ({}) often appears.
	For example, the following is a memory leak at allocation number 18:
	
	  
	
	  Detected memory leaks!
	  Dumping objects ->
	  {18} normal block at 0x00660BE4, 10 bytes long
	  Data: <          > CD CD CD CD CD CD CD CD CD CD
	  Object dump complete.
	
	It is useful to set a breakpoint right before this memory gets allocated so you
	can step through the callstack and see what functions are causing this memory to
	get allocated. The Debug-CRT function _CrtSetBreakAlloc that allows you to
	specify an allocation number at which to break. This method requires that you
	recompile your program every time you want to set a allocation breakpoint. An
	alternative method is to use the Watch window and set the allocation breakpoint
	dynamically. This method has the advantage of not requiring any source code
	changes or recompiling.
	
	If you are statically linking to the C Run-time, the variable you want to change
	is called _crtBreakAlloc. If you are dynamically linking to the C Run-time, the
	variable you want to change in the Watch window is
	{,,msvcr40d.dll}*__p__crtBreakAlloc()if you are using Visual C++ 4.0 or 4.1. The
	variable you want to change in the Watch window should be
	{,,msvcrtd.dll}*__p__crtBreakAlloc() if you are using Visual C++ 4.2 or later.
	
	To determine which version of the CRT you are compiling with:
	
	1. From the Build menu, choose Settings.
	
	2. In the Settings for: pane, select the configuration you are building for.
	  Choose the C/C++ tab, and then select the Code Generation category.
	
	The Use run-time library dialog should appear displaying the version of the CRT
	you are using. (If this setting is blank, make sure you have only selected one
	configuration on the Settings for: pane.)
	
	To set a allocation breakpoint dynamically, perform the following steps:
	
	1. Start your debugging session. From the Build menu, choose Debug ->
	  Step-Into. If you are using the "Debug Single-Threaded" or "Debug Multi-
	  Threaded CRT", follow step 1a. Otherwise, follow step 1b.
	
	  a. Type _crtBreakAlloc in the Watch window. This shows the current allocation
	     number at which your program will stop. This allocation number should be
	     -1 when your program first starts.
	
	  b. Type {,,msvcr40d.dll}*__p__crtBreakAlloc() in the Watch window if you are
	     using Visual C++ 4.0 or 4.1. Type {,,msvcrtd.dll}*__p__crtBreakAlloc() if
	     you are using Visual C++ 4.2 or later. This shows the current allocation
	     number at which your program will stop. This allocation number should be
	     -1 when your program first starts.
	
	2. Double click on the -1 value, and enter the new allocation number that causes
	  a user-defined breakpoint.
	
	3. From the Debug menu, choose Debug -> Go.
	
	For more information about _crtBreakAlloc, please see "Tracking Heap Allocation
	Requests" in the Online Help.
	
	======================================================================
	Keywords          : kbCRT kbDebug kbide kbVC kbVC400 kbVC410 kbVC420 kbVC500 kbVC600 
	Technology        : kbVCsearch kbAudDeveloper kbIntegratedDebugger
	Version           : WINNT:4.0,4.1,4.2,5.0;
	Issue type        : kbhowto
	
	=============================================================================
	

{% endraw %}
