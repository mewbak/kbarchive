---
layout: page
title: "Q188659: HOWTO: Use a Satellite DLL for Localization Purposes"
permalink: /kb/188/Q188659/
---

## Q188659: HOWTO: Use a Satellite DLL for Localization Purposes

{% raw %}

	Article: Q188659
	Product(s): Microsoft Visual Basic for Windows
	Version(s): WINDOWS:6.0
	Operating System(s): 
	Keyword(s): kbnokeyword kbVBp kbVBp600 kbGrpDSVB kbDSupport
	Last Modified: 11-JAN-2001
	
	-------------------------------------------------------------------------------
	The information in this article applies to:
	
	- Microsoft Visual Basic Professional Edition for Windows, version 6.0 
	- Microsoft Visual Basic Enterprise Edition for Windows, version 6.0 
	-------------------------------------------------------------------------------
	
	SUMMARY
	=======
	
	This article demonstrates how to use a satellite DLL to provide dynamic
	localization for a Visual Basic 6.0 application.
	
	MORE INFORMATION
	================
	
	Visual Basic allows you to use resource files to help you localize an
	application. Localization is the process of adapting a program for a specific
	international market, which includes customizing the user interface and features
	of the application. While it is possible to use separate resource files within
	an application, it is not recommended because resource files are compiled into
	an application and you will need to create and redistribute a new executable
	with each change to the resource file.
	
	With the use of a satellite DLL, an application can easily target many languages.
	For this to occur, you need to place all resources that are unique to the
	language into a separate DLL. When the application is started, the application
	will detect which regional setting is currently being used by the computer and
	will then load the appropriate DLL. By simply compiling and distributing an
	additional DLL, which contains its own unique resource file, it is much easier
	to support additional languages.
	
	How a Satellite DLL Works
	-------------------------
	
	To make a satellite DLL work properly, the application must determine the locale
	(regional setting) of the computer that it is running on. When the application
	first starts, it determines the locale ID from the operating system by calling
	GetUserDefaultLCID. The application uses this locale ID to load a DLL that
	contains the specific locale ID number as part of its name. If the application
	locates the DLL, the application will use the resources contained within the
	DLL. If the application does not find the DLL, the application defaults to
	whatever language it was compiled with.
	
	The difference between the DLLs is in the unique resource files that are used for
	the specific language being targeted. By containing the same code and the same
	basic interface, the main application can use any of the DLLs. Each satellite
	DLL should be named in a similar and standard way. For the sample below,
	"TestSat" + LocaleID of the region is used, where two LocaleID's are shown as
	follows:
	
	  409 : LocaleID for English (United States)
	  40C : LocaleID for French (Standard)
	
	The English Satellite DLL in the sample below will be named "TestSat409.DLL", and
	the French Satellite DLL will be named "TestSat40C.DLL". The test application
	contains the necessary code to determine which locale it is running in and how
	to load the appropriate satellite DLL.
	
	The sample steps below show how to create a simple satellite DLL, how to
	determine which locale an application is running in, and how to create and load
	the proper resources.
	
	Steps to Create the Test Application
	------------------------------------
	
	1. Create a new Standard EXE project in Visual basic 6.0. Form1 is created by
	  default.
	
	2. Add a Standard Module to the project by selecting Add Module from the Project
	  menu.
	
	3. Add a Command Button to Form1.
	
	4. Add the following code to the Declarations section of Form1:
	
	        Private Sub Command1_Click()
	           MsgBox "Command Button was Clicked", vbOKOnly, "Satellite Test"
	        End Sub
	
	        Private Sub Form_Load()
	
	        ' When this application launches, the code attempts
	        ' to find a local satellite DLL that will contain all the
	        ' resources.
	
	           If (LoadLocalizedResources) Then
	
	              ' Pull a string resource out of a local resource
	              ' object for demonstration purposes.
	              Command1.Caption = GetString(101)
	           End If
	       End Sub
	
	5. Add the following code to Module1:
	
	        Option Explicit
	
	        ' This module contains all the code necessary for the application
	        ' to use a satellite DLL for localization purposes.
	
	        ' Please refer to the MSDN for more information regarding the APIs
	        ' used in this example.
	
	        Public Declare Function GetUserDefaultLCID Lib "kernel32" () As Long
	
	        ' Object reference to the DLL that contains the resources
	        ' to be loaded.
	        Private clsSatellite As Object
	
	        Public Function LoadLocalizedResources() As Boolean
	           Dim lLocalID As String
	
	           ' Find the LocalID.
	           lLocalID = Hex(GetUserDefaultLCID)
	
	           ' Load the Satellite DLL that contains the local
	           ' resource object to be used. If CreateObject
	           ' fails, there is no local version of the
	           ' resources.
	
	           On Error GoTo NoLocalResource
	
	           ' Create a local object containing resources.
	           Set clsSatellite = CreateObject("TestSat" & lLocalID & _
	              ".clsResources")
	
	           ' Return true, then read local resources.
	           LoadLocalizedResources = True
	        Exit Function
	
	        NoLocalResource:
	
	           ' There is no local satellite DLL. As a result, false is returned.
	
	           LoadLocalizedResources = False
	
	        End Function
	
	        ' GetString will access the object and return the string
	        ' resources specific to the region. For this example, only
	        ' basic error handling is implemented.
	
	        Public Function GetString(StringIndex As Long) As String
	
	         ' Make sure there is a resource object.
	           If Not (clsSatellite Is Nothing) Then
	              ' Get the resource from the resource object.
	              GetString = clsSatellite.GetResourceString(StringIndex)
	           Else
	             ' For this example, if there is no resource
	             ' object something is still returned.
	             GetString = "Error : No Local Data"
	           End If
	        End Function
	
	6. Save and compile the project (Project1.Exe).
	
	Steps to Create Satellite DLLs
	------------------------------
	
	1. Create a new ActiveX DLL project in Visual Basic 6.0. Class1 is created by
	  default.
	
	2. From the Project menu, select Project1 Properties. Set the Project Name to
	  "TestSat409."
	
	3. Rename Class1 to clsResources.
	
	4. Paste the following code into clsResources:
	
	        Public Function GetResourceString(ResourceIndex As Long) As String
	           GetResourceString = LoadResData(ResourceIndex, 6)
	        End Function
	
	5. Start the Visual Basic 6.0 Resource Editor Add-In.
	
	6. In the Resource Editor, select "Edit String Tables."
	
	7. A new string table will be created, with a blank resource (101). Enter some
	  sample text into the resource (for example, "English Language").
	
	8. Close the String editor, and save the resource file as "TestSat409.Res".
	
	9. Save the Project, and make the ActiveX DLL.
	
	10. Perform Steps 1-9 again, but this time change the project name to
	  "TestSat40C", save the resource file as "TestSat40C.Res", and modify the
	  string contained in Step 7 to "French Language". For this particular test,
	  keep each satellite DLL in its own folder by placing the ActiveX DLL and
	  resource file into its own folder.
	
	Steps To Test Satellite DLLs
	----------------------------
	
	1. From the Windows Control Panel, select Regional Settings.
	
	2. Select "English (United States)." The system might prompt you to reboot if
	  another region was originally selected.
	
	3. Run the test project (Project1.exe). The command button caption should have
	  the "English" resource string you used for the first ActiveX DLL.
	
	4. From the Windows Control Panel, select Regional Settings again.
	
	5. Select French (Standard). If you are using Windows 95 or Windows 98 you have
	  to reboot.
	
	6. Run the test project (Project1.exe). The command button caption should have
	  the "French" resource string you used for the second ActiveX DLL.
	
	7. For testing purposes, rename the Test40C.dll. Re-run the test project
	  (Project1.Exe). The command button should have the default caption
	  "Command1". This is the case because the application could not find a
	  localized satellite DLL to use. As a result, the application used the default
	  caption of the command button.
	
	Additional query words:
	
	======================================================================
	Keywords          : kbnokeyword kbVBp kbVBp600 kbGrpDSVB kbDSupport 
	Technology        : kbVBSearch kbAudDeveloper kbZNotKeyword6 kbZNotKeyword2 kbVB600Search kbVBA600 kbVB600
	Version           : WINDOWS:6.0
	Issue type        : kbhowto
	
	=============================================================================
	

{% endraw %}
