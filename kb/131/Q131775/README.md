---
layout: page
title: "Q131775: HOWTO: Access Child Process Exit Code from 32-Bit Parent Proc."
permalink: /kb/131/Q131775/
---

## Q131775: HOWTO: Access Child Process Exit Code from 32-Bit Parent Proc.

{% raw %}

	Article: Q131775
	Product(s): Microsoft C Compiler
	Version(s): WINNT: 2.0,2.1,4.0,5.0;
	Operating System(s): 
	Keyword(s): kbcode kbCRT kbVC200 kbVC210 kbVC400 kbVC500 kbVC600
	Last Modified: 28-JAN-2002
	
	-------------------------------------------------------------------------------
	The information in this article applies to:
	
	- The C Run-Time (CRT), included with:
	   - Microsoft Visual C++, 32-bit Editions, versions 2.0, 2.1, 4.0 
	   - Microsoft Visual C++, 32-bit Enterprise Edition, version 5.0 
	   - Microsoft Visual C++, 32-bit Professional Edition, version 5.0 
	   - Microsoft Visual C++, 32-bit Enterprise Edition, version 6.0 
	   - Microsoft Visual C++, 32-bit Professional Edition, version 6.0 
	   - Microsoft Visual C++, 32-bit Learning Edition, version 6.0 
	-------------------------------------------------------------------------------
	
	SUMMARY
	=======
	
	In the Microsoft products listed at the beginning of this article, there is no C
	run-time function that will return the system exit code from a child process.
	However, the Win32 GetExitCodeProcess() API function can retrieve this
	information. This article shows how to use it.
	
	MORE INFORMATION
	================
	
	Under Win32, the GetExitCodeProcess() function retrieves the exit status of the
	child process. In fact, GetExitCodeProcess() can retrieve the exit status of any
	process given the correct process handle. The process handle itself must have
	PROCESS_QUERY_INFORMATION access before it can be used.
	
	If the specified process has not terminated, STILL_ACTIVE is returned as the exit
	status. If the process has terminated, the exit status returned is one of
	these:
	
	- The exit value specified in the ExitProcess or TerminateProcess function.
	
	-or-
	
	- The return value from the main or WinMain function of the process.
	
	-or-
	
	- The exception value for an unhandled exception that caused the process to
	  terminate.
	
	Sample Code
	-----------
	
	  /* Compile options needed: none
	  */ 
	
	  #include <windows.h>
	  #include <stdio.h>
	
	  void main(void)
	  {
	     PROCESS_INFORMATION pInfo;
	     STARTUPINFO         sInfo;
	     DWORD               exitCode;
	
	     sInfo.cb              = sizeof(STARTUPINFO);
	     sInfo.lpReserved      = NULL;
	     sInfo.lpReserved2     = NULL;
	     sInfo.cbReserved2     = 0;
	     sInfo.lpDesktop       = NULL;
	     sInfo.lpTitle         = NULL;
	     sInfo.dwFlags         = 0;
	     sInfo.dwX             = 0;
	     sInfo.dwY             = 0;
	     sInfo.dwFillAttribute = 0;
	     sInfo.wShowWindow     = SW_SHOW;
	
	     if (!CreateProcess(NULL,
	                  "command.com /c dir c:\\*.bat",
	                        NULL,
	                        NULL,
	                        FALSE,
	                        0,
	                        NULL,
	                        NULL,
	                        &sInfo,
	                        &pInfo)) {
	        printf("ERROR: Cannot launch child process\n");
	        exit(1);
	     }
	
	     // Give the process time to execute and finish
	     WaitForSingleObject(pInfo.hProcess, 5000L);
	
	     if (GetExitCodeProcess(pInfo.hProcess, &exitCode))
	     {
	        switch(exitCode)
	        {
	           case STILL_ACTIVE: printf("Process is still active\n");
	                              break;
	           default:           printf("Exit code = %d\n", exitCode);
	                              break;
	        }
	     }
	     else {
	        printf("GetExitCodeProcess() failed\n");
	     }
	  }
	
	REFERENCES
	==========
	
	Books Online documentation for the Win32 GetExitCodeProcess() function.
	
	For information about 16-bit Windows-based programs, please see the following
	article in the Microsoft Knowledge Base:
	
	  Q83301 Retrieving Application Exit Code in MS-DOS Window
	
	Additional query words: 9.00 9.0 9.1 9.10
	
	======================================================================
	Keywords          : kbcode kbCRT kbVC200 kbVC210 kbVC400 kbVC500 kbVC600 
	Technology        : kbVCsearch kbAudDeveloper kbCRT
	Version           : WINNT: 2.0,2.1,4.0,5.0;
	Issue type        : kbhowto
	
	=============================================================================
	

{% endraw %}
