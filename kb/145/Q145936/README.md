---
layout: page
title: "Q145936: HOWTO: Insert Existing Projects as Sub-Projects"
permalink: /kb/145/Q145936/
---

## Q145936: HOWTO: Insert Existing Projects as Sub-Projects

	Article: Q145936
	Product(s): Microsoft C Compiler
	Version(s): WINNT:4.0,5.0,6.0;
	Operating System(s): 
	Keyword(s): kbide kbVC kbVC400 kbVC500 kbVC600 kbGrpDSTools
	Last Modified: 31-JUL-2001
	
	-------------------------------------------------------------------------------
	The information in this article applies to:
	
	- Microsoft Visual C++, 32-bit Editions, version 4.0 
	- Microsoft Visual C++, 32-bit Enterprise Edition, version 5.0 
	- Microsoft Visual C++, 32-bit Professional Edition, version 5.0 
	- Microsoft Visual C++, 32-bit Enterprise Edition, version 6.0 
	- Microsoft Visual C++, 32-bit Professional Edition, version 6.0 
	- Microsoft Visual C++, 32-bit Learning Edition, version 6.0 
	-------------------------------------------------------------------------------
	
	SUMMARY
	=======
	
	There is no way to insert an existing project as a project or subproject of the
	current workspace in Visual C++, version 4.0. The Insert menu has a Projects
	command that you can use to create new projects and sub-projects for the
	workspace, but you can't use it to insert projects into the workspace.
	
	However, you can create a new sub-project of type makefile and insert a link from
	it to an existing project's makefile. This provides one of the major benefits of
	a sub-project; when the main project is building, it will do a 'make' of the
	linked project.
	
	If you have a project that creates a library, and in another workspace you have a
	project to create an .exe file that uses the library, you can create a makefile
	sub-project in the .exe project that contains commands to build a library
	project. When building the main (.exe) project, if a dependent file of the
	linked (library) project is out of date, the file and the library will be
	re-built, and the changes will be incorporated into the main project.
	
	Because the project is not truly inserted into the workspace, the project
	workspace window will not be able to display class, file, or resource
	information about the linked project.
	
	This limitation has been removed in Visual C++, versions 5.0 and 6.0. Click the
	workspace name in the File View. On the Project menu, click Insert Project into
	Workspace.
	
	MORE INFORMATION
	================
	
	Step-by-Step Procedure
	----------------------
	
	From a project workspace, to create a sub-project link to an existing separate
	project, follow these steps:
	
	1. On the Insert menu, click Projects. This will bring up the Insert Project
	  dialog box that can create (but not insert existing) projects. To get here
	  another way, you can on Build menu, click Subprojects, and then click New.
	
	2. From the Insert Project dialog box, select a Project of type Makefile.
	  Specify a project name and whether or not it is to be a subproject of an
	  existing project.
	
	3. Click Create, and then click Yes. This takes you directly to the Project
	  Settings dialog box for this new project.
	
	4. In the Settings For list, select a configuration of the new makefile
	  sub-project that matches one of the configurations of the main project. For
	  example, select the Win32 Debug configuration. This is important because when
	  you build a main project, Developer's Studio will look for the matching
	  sub-project configuration and build that. If there is no matching sub-project
	  configuration, the sub-project will be ignored.
	
	5. Click the General tab, remove the NMAKE command from the build command line,
	  and instead invoke a batch file to run NMAKE on the existing project
	  makefile. A batch file is required because project makefiles use relative
	  paths, and the current directory must be set to the directory of the project
	  makefile - something you can do in a batch file. For example, the command for
	  the Win32 Debug configuration should look something like this one:
	
	     c:\MyOldProject\MyOldProject.bat "MyOldProject - Win32 Debug"
	
	  If the old project was created by Visual C++ 2.0, the string would be "Win32
	  Debug" - look in the makefile to be sure.
	
	  If you always want the sub-project built the same way for all configurations,
	  just have the same batch command for each configuration.
	
	  In this sample, the batch file is in main directory of the old existing
	  project. It works well there because that makes it easy to include the
	  project in the sub-projects of any other new projects you might create.
	
	6. Note the Rebuild all option. When you use the Rebuild all option on the main
	  project, this option will be passed as a parameter to your batch file. This
	  is best left "/a".
	
	7. Change the Output file name to the actual library or .exe file that will be
	  created, and be sure to specify the full path.
	
	8. Do steps 4-5 for each configuration you will use.
	
	9. Write the batch file to change the working directory to that of the original
	  project directory, and then invoke NMAKE on the project's .mak file. The
	  batch file can also pass along the arguments for rebuild all and the
	  configuration specifier. For example:
	
	     cd c:\MyOldProject
	     nmake %2 -f MyOldProject.mak CFG=%1
	
	  Given the build command listed in step 5, %1 will contain the configuration
	  string and %2 will contain the rebuild all option (which will be blank for
	  normal builds).
	
	  NOTE: the batch file must not contain any commands for user interaction such
	  as PAUSE. The output of the batch file is sent to the debug window, which is
	  display only. Developer's Studio will hang waiting for input from the user in
	  a window that does not allow input.
	
	Additional query words:
	
	======================================================================
	Keywords          : kbide kbVC kbVC400 kbVC500 kbVC600 kbGrpDSTools 
	Technology        : kbVCsearch kbVC400 kbAudDeveloper kbVC500 kbVC600 kbVC32bitSearch kbVC500Search
	Version           : WINNT:4.0,5.0,6.0;
	Issue type        : kbhowto
	
	=============================================================================
	