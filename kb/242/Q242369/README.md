---
layout: page
title: "Q242369: HOWTO: Distribute an MMC SnapIn Project With the PDW"
permalink: /kb/242/Q242369/
---

## Q242369: HOWTO: Distribute an MMC SnapIn Project With the PDW

{% raw %}

	Article: Q242369
	Product(s): Microsoft Visual Basic for Windows
	Version(s): 1.1,1.2,6.0
	Operating System(s): 
	Keyword(s): kbMMC kbVBp600 kbGrpDSPlatform kbDSupport kbSnapIn
	Last Modified: 11-JAN-2001
	
	-------------------------------------------------------------------------------
	The information in this article applies to:
	
	- Microsoft Management Console, versions 1.1, 1.2 
	- Microsoft Visual Basic Professional Edition for Windows, version 6.0 
	- Microsoft Visual Basic Enterprise Edition for Windows, version 6.0 
	-------------------------------------------------------------------------------
	
	SUMMARY
	=======
	
	This article outlines the basic steps to follow when building a distribution for
	a SnapIn project developed with the MMC SnapIn Designer for Visual Basic using
	the Package and Deployment Wizard (PDW). There is an assumption that a SnapIn
	project has already been developed and built properly. For more information on
	how to build a SnapIn project, please refer to the "References" section below.
	
	MORE INFORMATION
	================
	
	Steps To Package a SnapIn Project
	---------------------------------
	
	1. Start the Package and Deployment Wizard.
	
	2. When the PDW loads, click Browse and locate the SnapIn project file on the
	  system (VBP file).
	
	3. When the proper project has been located, click Package.
	
	4. The PDW presents the Package Type dialog box. For this example select the
	  Standard Setup Package option and click Next .
	
	5. The PDW presents the Package Folder dialog box. This option specifies where
	  the finished package will reside. By default, the PDW creates a package
	  folder under the project folder. In this example accept the default and click
	  Next. The PDW prompts about creating a Folder that does not exist. This
	  behavior is by design.
	
	6. The PDW might display the following dialog box next:
	
	  If this control will be used within a design environment other than Visual
	  Basic, you will need to distribute the Property Page DLL. Do you want to
	  include this file in your package?
	
	  A SnapIn project is compiled as an .ocx file, and the PDW thinks the project
	  is an ActiveX UserControl project. Select No to this question.
	
	7. The PDW displays the Included Files dialog box. The Mssnaor.dll component
	  should be included. If it is not, browse for the component and add it to the
	  list. If there are additional files (readme file, etc) which need to be
	  distributed this is where they are added to the package. Notice that the
	  Msstkprp.dll should not be selected. When everything is set, click Next.
	
	8. The PDW display the Cab Options dialog box. For this example, accept the
	  default Single Cab option and click Next button.
	
	9. The PDW displays the Installation Title dialog box. For this example, accept
	  the default title and click Next.
	
	10. The PDW displays the Start Menu Items dialog box. A SnapIn project should
	  not add itself to the Start Menu unless there are additional files which
	  ship (such as a readme file). When everything has been set, click Next.
	
	11. The PDW displays the Install Location dialog box. The list shows where
	  important components are installed on the target machine. Make sure that the
	  Mssnapr.dll component is installed in the Program Files\Common
	  Files\Microsoft Shared\SnapInDesigner folder. When everything is set, click
	  Next.
	
	12. The PDW displays the Shared Files dialog box. For this example simply click
	  Next.
	
	13. The PDW displays the Finished! dialog box. The option to save all the above
	  taken options in a script file is presented. Click Finish and the PDW builds
	  the distribution package.
	
	Notes
	-----
	
	  1. A SnapIn developed with the MMC SnapIn Designer For Visual Basic requires
	     the Visual Basic runtime files as well as the SnapIn runtime component
	     (Mssnapr.dll). The PDW automatically includes these components in the
	     distribution package.
	
	  2. If the SnapIn project uses any ActiveX controls, confirm they are included
	     with the distribution package. The PDW picks these dependencies up.
	
	  3. The PDW does not pick up on implicit dependencies (late bound objects)
	     which can cause problems when the SnapIn is executed on the target
	     computer. For example, late binding to the File System Object, which is
	     contained in the Scrrun.dll. The SnapIn project file (VBP) does not
	     contain a reference to the component, and the Scripting Runtime is not
	     included in the distribution package. If the Scripting Runtime is not
	     installed on the target computer a 429 error occurs when the SnapIn tried
	     to create the File System Object.
	
	REFERENCES
	==========
	
	Refer to the following topic(s) in the MMC SnapIn Designer for Visual Basic
	documentation:
	
	- Common Development Tasks
	
	Additional query words:
	
	======================================================================
	Keywords          : kbMMC kbVBp600 kbGrpDSPlatform kbDSupport kbSnapIn 
	Technology        : kbVBSearch kbAudDeveloper kbZNotKeyword6 kbZNotKeyword2 kbVB600Search kbVBA600 kbVB600 kbMMCSearch kbMMC110 kbMMC120
	Version           : :1.1,1.2,6.0
	Issue type        : kbhowto
	
	=============================================================================
	

{% endraw %}
