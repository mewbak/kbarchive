---
layout: page
title: "Q155831: XADM: Set TCP/IP for Exchange/Outlook Client Through Firewall"
permalink: /kb/155/Q155831/
---

## Q155831: XADM: Set TCP/IP for Exchange/Outlook Client Through Firewall

{% raw %}

	Article: Q155831
	Product(s): Microsoft Exchange
	Version(s): 4.0,5.0,5.5
	Operating System(s): 
	Keyword(s): exc4 exc5 exc55
	Last Modified: 06-AUG-2002
	
	-------------------------------------------------------------------------------
	The information in this article applies to:
	
	- Microsoft Exchange Server, versions 5.5, 4.0, 5.0 
	-------------------------------------------------------------------------------
	
	IMPORTANT: This article contains information about modifying the registry. Before you 
	modify the registry, make sure to back it up and make sure that you understand how to restore 
	the registry if a problem occurs. For information about how to back up, restore, and edit the 
	registry, click the following article number to view the article in the Microsoft Knowledge Base:
	
	  Q256986 Description of the Microsoft Windows Registry
	
	SUMMARY
	=======
	
	This article tells you how to allow the Microsoft Exchange Client to connect to
	Microsoft Exchange Server over an existing connection to the Internet and
	through a firewall. In order to do this, make the ports assigned to these
	connections static. This requires you to add entries to the registry.
	
	For additional information about configuring Exchange Server services for
	Internet firewalls, please click the article number below to view the article in
	the Microsoft Knowledge Base:
	
	  Q148732 XADM: Setting TCP/IP Port Numbers for Internet Firewalls
	
	MORE INFORMATION
	================
	
	WARNING: If you use Registry Editor incorrectly, you may cause serious problems
	that may require you to reinstall your operating system. Microsoft cannot
	guarantee that you can solve problems that result from using Registry Editor
	incorrectly. Use Registry Editor at your own risk.
	
	You must restart the computer for these changes to take effect.
	
	To make the ports static:
	
	1. Start Registry Editor (Regedt32.exe).
	
	2. Under the HKEY_LOCAL_MACHINE subtree, go to the following subkey:
	
	  System\CurrentControlSet\Services\MSExchangeDS\Parameters
	
	3. Add the following entry for the Microsoft Exchange Directory service:
	
	  TCP/IP port REG_DWORD
	  DATA: <port number to assign>
	
	  NOTE: Microsoft recommends that you assign ports from the 5000 - 65535
	  (decimal) range. For additional information about the guidelines for static
	  port assignment of Exchange Server services, please see the Microsoft
	  Knowledge Base article in the "More Information" section.
	
	  EXAMPLE: "TCP/IP Port"=dword:00001388(5000)
	
	  The decimal number 5000 was used for the DS, 1388 in hexadecimal format.
	
	4. Locate the following subkey:
	
	  System\CurrentControlSet\Services\MSExchangeIS\ParametersSystem
	
	5. Add the following entry for the Information Store:
	
	  TCP/IP port REG_DWORD
	  DATA: <port number to assign>
	
	  NOTE: Microsoft recommends that you assign ports from the 5000 - 65535
	  (decimal) range. For additional information about the guidelines for static
	  port assignment of Exchange Server services, please see the Microsoft
	  Knowledge Base article in the More Information section.
	
	  EXAMPLE: "TCP/IP Port"=dword:00001389(5001)
	
	  The decimal number 5001 was used for the IS, 1389 in hexadecimal format.
	
	6. Quit Registry Editor.
	
	After this, you must configure the packet filter (or firewall) to allow
	Transmission Control Protocol (TCP) connections to be made to these ports as
	well as to port 135.
	
	Further Explanation
	-------------------
	
	A packet filter (or firewall) denies connection attempts made to any port for
	which you have not explicitly allowed connections. Microsoft Exchange Server
	does use a well-known static port (port 135) to listen for client connects to
	the Remote Procedure Call (RPC) Endpoint Mapper Service. However, after the
	client connects to this socket, Microsoft Exchange Server then re-assigns the
	client two random ports to use when communicating with the directory and the
	information store. This makes it impossible to allow these through the firewall
	without forcing them to be statically assigned.
	
	References
	----------
	
	For additional information, please refer to the Readme.wri file on the Microsoft
	Exchange Server compact disc.
	
	For additional information about port selection for Exchange, click the article
	number below to view the article in the Microsoft Knowledge Base:
	
	  Q194952 XADM: Statically Mapped Port Limitations for Exchange Server
	
	
	Additional query words: static mapped ports
	
	======================================================================
	Keywords          : exc4 exc5 exc55 
	Technology        : kbExchangeSearch kbExchange500 kbExchange550 kbExchange400 kbZNotKeyword2
	Version           : :4.0,5.0,5.5
	Issue type        : kbhowto
	
	=============================================================================
	

{% endraw %}
