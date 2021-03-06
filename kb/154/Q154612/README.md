---
layout: page
title: "Q154612: Installing Windows NT 4.0 Printer Drivers on a 3.51 Server"
permalink: /kb/154/Q154612/
---

## Q154612: Installing Windows NT 4.0 Printer Drivers on a 3.51 Server

{% raw %}

	Article: Q154612
	Product(s): Microsoft Windows NT
	Version(s): 2000,3.51,4.0
	Operating System(s): 
	Keyword(s): kbnetwork
	Last Modified: 08-AUG-2001
	
	-------------------------------------------------------------------------------
	The information in this article applies to:
	
	- Microsoft Windows NT Server versions 3.51, 4.0 
	- Microsoft Windows NT Workstation version 4.0 
	- Microsoft Windows 95 
	- Microsoft Windows 2000 Professional 
	-------------------------------------------------------------------------------
	
	SUMMARY
	=======
	
	To allow Windows NT 4.0 clients to connect to printers on a Windows NT 3.51
	server and have the driver reside on the server, it is necessary to install the
	4.0 drivers on the 3.51 server.
	
	NOTE: Windows 95 point and print drivers cannot be installed on a Windows NT 3.51
	server. Attempts to do so results in the following error message:
	
	  Alternate drivers cannot be installed
	
	MORE INFORMATION
	================
	
	If the printer already exists on the Windows NT 3.51 Server, use the following
	steps to add a 4.0 driver for use by Windows NT 4.0 clients:
	
	1. Log on to the Windows NT 4.0 workstation using an account that has
	  administrator privileges on the server you will be installing the drivers on.
	
	2. From the Start menu, choose Run.
	
	3. In the Open box, type \\<servername>, where <servername> is the
	  name of the 3.51 server.
	
	4. Open the Printers Folder on the server.
	
	5. Select the printer you wish to add a 4.0 driver for.
	
	6. Select File/Properties, install the driver when prompted, then choose the
	  Sharing tab.
	
	7. Select the alternate drivers you wish to install, then select OK.
	
	If you are creating a new printer on a Windows NT 3.51 Server, use the following
	steps to install a Windows NT 4.0 driver on a 3.51 Server for use by 4.0
	clients:
	
	1. Log on to the Windows NT 4.0 workstation using an account that has
	  administrator privileges on the server you will be installing the drivers on.
	
	2. From the Start menu, choose Run.
	
	3. In the Open box, type \\<servername> where <servername> is the
	  name of the Windows NT 3.51 Server.
	
	4. Open the Printers Folder on the server.
	
	5. Select Add Printer.
	
	6. Select Remote print server \\<servername>, then select Next.
	
	7. Choose the port the printer will use, then select Next
	
	  NOTE: If the port does not already exist on the server, you will need to go to
	  the server to create the port. This cannot be done remotely.
	
	8. Choose the printer make and model, then select Next.
	
	9. Type a printer name, then Select Next.
	
	10. Choose Shared, enter a Share name, then select all operating systems that
	  will be connecting to the Windows NT 3.51 Server.
	
	11. You will be prompted for the source media for Windows NT 3.51 and any other
	  operating systems selected in step 10.
	
	
	Installing Microsoft Windows 2000 drivers on a Windows NT 4.0 server for Windows 2000 clients
	---------------------------------------------------------------------------------------------
	
	To allow Windows 2000 clients to connect to printers on a Windows NT 4.0 server
	and have the driver reside on the server, it is necessary to install the 2000
	drivers on the 4.0 server.
	
	If the printer already exists on the Windows NT 4.0 Server, use the following
	steps to add a Windows 2000 driver for use by Windows 2000 clients:
	
	   - Log on to the Windows 2000 workstation using an account that has
	  administrator privileges on the server you will be installing the drivers on.
	
	- From the Start menu, choose Run.
	
	- In the Open box, type \\servername, where servername is the name of the 4.0
	  server.
	
	- Open the Printers Folder on the server.
	
	- Select the printer in which you wish to add a Windows 2000 driver.
	
	- Select File/Properties, install the driver when prompted, then choose the
	  Sharing tab.
	
	- Select the alternate drivers you wish to install, then select OK.
	
	If you are creating a new printer on a Windows NT 4.0 Server, use the following
	steps to install a Windows 2000 driver on a 4.0 Server for use by Windows 2000
	clients:
	
	   - Log on to the Windows 2000 workstation using an account that has
	  administrator privileges on the server you will be installing the drivers on.
	
	- From the Start menu, choose Run.
	
	- In the Open box, type \\servername where servername is the name of the
	  Windows NT 4.0 Server.
	
	- Open the Printers Folder on the server.
	
	- Select Add Printer.
	
	- Select Remote print server \\servername, then select Next.
	
	- Choose the port which the printer will use, then select Next.
	
	  NOTE: If the port does not already exist on the server, you will need to go to
	  the server to create the port. This cannot be done remotely.
	
	- Choose the printer make and model, then select Next.
	
	- Type a printer name, then Select Next.
	
	- Choose Shared, enter a Share name, then select all operating systems that
	  will be connecting to the Windows NT 4.0 Server.
	
	You will be prompted for the source media for Windows NT 4.0 and any other
	operating systems selected in step 10.
	
	Additional query words: prodnt mips alpha win95
	
	======================================================================
	Keywords          : kbnetwork 
	Technology        : kbWinNTsearch kbWinNTWsearch kbWinNTW400 kbWinNTW400search kbWinNT351search kbWinNT400search kbWinNTSsearch kbWinNTS400search kbWinNTS400 kbWinNTS351 kbwin2000Search kbwin2000ProSearch kbwin2000Pro kbWinNTS351search kbWin95search kbZNotKeyword3
	Version           : :2000,3.51,4.0
	
	=============================================================================
	

{% endraw %}
