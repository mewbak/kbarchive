---
layout: page
title: "Q231923: HOWTO: Distribute the Microsoft Data Engine (MSDE) With the PDW"
permalink: /kb/231/Q231923/
---

## Q231923: HOWTO: Distribute the Microsoft Data Engine (MSDE) With the PDW

{% raw %}

	Article: Q231923
	Product(s): Microsoft Visual Basic for Windows
	Version(s): 1.0,6.0
	Operating System(s): 
	Keyword(s): kbwizard kbAppSetup kbDatabase kbVBp kbVBp600 kbGrpDSVBDB kbDSupport kbMSDE100
	Last Modified: 01-MAR-2002
	
	-------------------------------------------------------------------------------
	The information in this article applies to:
	
	- Microsoft Visual Basic Professional Edition for Windows, version 6.0 
	- Microsoft Visual Basic Enterprise Edition for Windows, version 6.0 
	- Microsoft Data Engine (MSDE), version 1.0 
	-------------------------------------------------------------------------------
	
	SUMMARY
	=======
	
	This article shows how to package and distribute MSDE for Visual Studio using
	the Package and Deployment Wizard (PDW) tool that ships with Visual Basic 6.0.
	There are two main steps to perform:
	
	1. Create a Standard Setup Package that redistributes necessary MSDE files to
	  target machines along with your Visual Basic application. The MSDE files will
	  be used on target machines to set up MSDE. This could be done in two ways
	  with the PDW:
	
	   - MSDE manual setup
	
	   - MSDE automatic setup via a Window's Program group icon
	
	2. Use a custom database with MSDE on the target machine.
	
	MORE INFORMATION
	================
	
	The following procedure assumes that you have downloaded the MSDE for Visual
	Studio redistribution package (Msdex86_pkg.exe) and have extracted the
	redistribution file (Msdex86.exe). The MSDE for Visual Studio CD also has the
	redistribution files in the MSDE folder.
	
	Step 1: Create the Redistribution Package
	-----------------------------------------
	
	Manual Setup:
	
	In this approach, MSDE setup must be launched manually after redistributing MSDE
	files to the target machine. This can be accomplished from either the MS-DOS
	command line or from the Start/Run menu.
	
	1. On the original development machine, start the Package and Deployment Wizard.
	  Choose a Visual Basic project and click the Package icon.
	
	2. In the Package and Deployment Wizard - Package Type dialog box, click
	  Standard Setup Package.
	
	3. Click Next; leave the default settings.
	
	4. Click Next. In the Package and Deployment Wizard - Included Files dialog box,
	  click Add. Include the following files within the setup wizard:
	
	   - Readme.txt
	
	   - Msdex86.exe
	
	   - Unattend.iss
	
	   - License.txt
	
	   - Any custom database (.mdf file) that needs to be used with MSDE on the
	     target machine
	
	5. Click Next. In the Package and Deployment Wizard - Cab Options dialog box,
	  choose one of the following two options:
	
	   - Single Cab: This option is useful when distributing the Package on a large
	     media such as a CD-ROM. This option packages all of the files into a
	     single CAB file.
	
	   - Multiple Cab: This option is useful when distributing the package on
	     disks. Choosing this option packages the files into multiple CAB files.
	
	6. Click Next. In the Package and Deployment Wizard - Installation Title dialog
	  box, choose a setup screen title.
	
	7. Continue through the wizard, selecting the default settings, until you reach
	  the Package and Deployment Wizard - Shared Files dialog box. In this dialog
	  box, mark the components you want shared.
	
	8. Continue through the wizard; click Finish. The package is now complete and
	  can be installed onto target machines.
	
	9. Run the setup program on the target machine.
	
	10. From the Start menu, point to Run (or from the MS-DOS command prompt), type
	  the following, "AppPath\msdex86.exe -s -a -f1 "AppPath\unattend.iss""
	  (without the quotation marks) where AppPath is the application directory
	  specified by the user, or the default directory specified in the Setup
	  section. This launches the MSDE setup program.
	
	Automatic Setup via Window's Program Group:
	
	This allows the creation of a program group that appears under the Start/Programs
	menu on Window's desktop. Once clicked, this program group automatically
	launches the MSDE setup process on the target machine.
	
	1. On the original development machine, start the Package and Deployment Wizard
	  and repeat steps 1 through 6 in the "Manual Setup" process above.
	
	2. In the Package and Deployment Wizard - Start Menu Items dialog box, click New
	  Item. Then, do the following:
	
	  a. In the Name box, type "Start MSDE Setup" (without the quotation marks).
	
	  b. In the Target box, type the following:
	
	     "msdex86.exe -s -a -f1 "$(AppPath)\unattend.iss"" (without the quotation
	     marks)
	
	  c. In the Start In box, leave the default macro: $(AppPath).
	
	3. Repeat steps 7 and 8 above. The package is now complete and can be installed
	  onto target machines.
	
	Step 2: Using a Custom Database with MSDE
	-----------------------------------------
	
	When MSDE setup is completed successfully on target machines, only the following
	databases will be available with MSDE:
	
	- master
	
	- model
	
	- msdb
	
	- tempdb
	
	Once you have redistributed the custom database (.mdf) file onto the target
	machine as shown in step 4 of the "Manual Setup" section above, you can then
	apply any of the following approaches:
	
	- Run the stored procedure "sp_attach_db" to attach your database to MSDE as
	  follows:
	
	  EXEC sp_attach_db @dbname = N'dbname', @filename = N'filepath\filename.mdf'
	  	
	  EXEC sp_attach_db 'Test', 'c:\Mssql7\Data\Test.mdf'
	
	- Use the Microsoft OLEDB Provider for SQL Server to attach the .mdf database
	  file and connect to the database directly. In this case, the connection
	  string should resemble the following:
	
	  "Provider = SQLOLEDB.1; User ID = your_user_id; Password = your_password;Initial Catalog = db_name; Data Source = server_name;
	  Initial File Name = db_file_path\db_file_name.mdf"
	
	- Use the Microsoft OLEDB Provider for SQL Server to point to the local MSDE.
	  In this case, the connection string should resemble the following:
	
	  "Provider = SQLOLEDB.1; User ID = your_user_id; Password = your_password;
	   Initial Catalog = db_name; Data Source = (local)"
	
	- Use the Microsoft OLEDB Provider for ODBC drivers (MSDASQL) to connect to
	  MSDE. You can create a DSN on each target machine or use a DSN-less
	  connection
	
	  NOTE: The third and fourth approaches above require attaching the database
	  prior to using the connection string(s).
	
	- You can optionally use SQL-DMO to start MSDE, attach or/and detach your
	  custom database to MSDE.
	
	REFERENCES
	==========
	
	Resources for developers building applications with MSDE, including whitepapers,
	general additional FAQS, and sample code can be found at:
	
	  http://msdn.microsoft.com/vstudio/msde
	
	For additional information on the process of installing a user-database on MSDE,
	click the article number below to view the article in the Microsoft Knowledge
	Base:
	
	  Q224071 INF: Moving SQL Server Databases to a New Location
	
	For additional information on automating the MSDE setup with the PDW, click the
	article number below to view the article in the Microsoft Knowledge Base:
	
	  Q234626 SAMPLE: Setup1.exe Fully Automating MSDE Setup with the Package and
	  Deployment Wizard (PDW)
	
	For additional information on the Package and Deployment Wizard, please refer to
	the Visual Basic documentation.
	
	(c) Microsoft Corporation 1999, All Rights Reserved.
	Contributions by Ammar Abuthuraya, Microsoft Corporation
	
	
	Additional query words:
	
	======================================================================
	Keywords          : kbwizard kbAppSetup kbDatabase kbVBp kbVBp600 kbGrpDSVBDB kbDSupport kbMSDE100 
	Technology        : kbVBSearch kbAudDeveloper _IKkbbogus kbZNotKeyword6 kbZNotKeyword2 kbVB600Search kbVB600 kbMSDE
	Version           : :1.0,6.0
	Issue type        : kbhowto
	
	=============================================================================
	

{% endraw %}
