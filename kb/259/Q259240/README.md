---
layout: page
title: "Q259240: XWEB: Configure OWA to Connect to Exchange Through a Firewall"
permalink: /kb/259/Q259240/
---

## Q259240: XWEB: Configure OWA to Connect to Exchange Through a Firewall

{% raw %}

	Article: Q259240
	Product(s): Microsoft Exchange
	Version(s): 5.5
	Operating System(s): 
	Keyword(s): 
	Last Modified: 06-AUG-2002
	
	-------------------------------------------------------------------------------
	The information in this article applies to:
	
	- Microsoft Outlook Web Access, version 5.5 
	- Microsoft Exchange Server, version 5.5 
	-------------------------------------------------------------------------------
	
	IMPORTANT: This article contains information about modifying the registry. Before you 
	modify the registry, make sure to back it up and make sure that you understand how to restore 
	the registry if a problem occurs. For information about how to back up, restore, and edit the 
	registry, click the following article number to view the article in the Microsoft Knowledge Base:
	
	  Q256986 Description of the Microsoft Windows Registry
	
	SUMMARY
	=======
	
	This article describes how to set up Microsoft Outlook Web Access (OWA) to
	connect to Microsoft Exchange Server through a firewall. This configuration
	assumes that there is a firewall between OWA and the Exchange Server computer.
	There are three ports that need to be opened on the firewall in this
	configuration. On the Exchange Server computer, two ports need to be statically
	mapped. To do this, the ports must be opened by editing the registry.
	
	NOTE: The third port, port 135, must be opened on the firewall.
	
	MORE INFORMATION
	================
	
	Follow the steps in this section to statically map the two ports on the Exchange
	Server computer. The Exchange Server computer that OWA points to must have these
	ports mapped.
	
	NOTE: One port must be mapped for the information store, and one port must be
	mapped for the directory.
	
	For additional information about configuring Exchange Server services for
	Internet firewalls, click the article number below to view the article in the
	Microsoft Knowledge Base:
	
	  Q155831 XADM: Setting TCP/IP for Exchange and Outlook Client Connects Through
	  a Firewall
	
	WARNING: If you use Registry Editor incorrectly, you may cause serious problems
	that may require you to reinstall your operating system. Microsoft cannot
	guarantee that you can solve problems that result from using Registry Editor
	incorrectly. Use Registry Editor at your own risk.
	
	1. Start Registry Editor (Regedt32.exe).
	
	2. Locate the following key in the registry:
	
	  HKEY_LOCAL_MACHINE\System\CurrentControlSet\Services\MSExchangeDS\Parameters
	
	3. Add the following entry for the Microsoft Exchange Directory service:
	
	  Entry: TCP/IP port
	  Type: REG_DWORD
	  Data: <port number to assign>
	
	  NOTE: Do not assign ports immediately above the 1023 range. This may cause
	  other problems on the Exchange Server.
	
	  For example:
	
	  "TCP/IP Port"=dword:000004C9(1225)
	
	4. Locate the following key in the registry:
	
	  HKEY_LOCAL_MACHINE\System\CurrentControlSet\Services\MSExchangeIS\ParametersSystem
	
	5. Add the following entry for the Exchange Server information store:
	
	  Entry: TCP/IP port
	  Type: REG_DWORD
	  Data: <port number to assign>
	
	  NOTE: Do not assign ports immediately above the 1023 range. This may cause
	  other problems on the Exchange Server computer.
	
	  For example:
	
	  "TCP/IP Port"=dword:000004CA(1226)
	
	6. Quit Registry Editor.
	
	7. Restart your computer for the changes to take effect.
	
	8. On the firewall, open the ports that you assigned to the directory, the
	  information store, and port 135 for the endpoint mapper.
	
	  NOTE: For the Exchange Server to communicate back through the firewall to the
	  OWA server it is also necessary to have the ephemeral ports 1024 through
	  65535 configured for outbound communications from the Exchange server to the
	  OWA server. Although you can specify what ports Exchange listens on for RPC
	  traffic, you can not specify what RPC ports the OWA application uses for RPC
	  communications.
	
	NOTE: The OWA server must also be a member of the domain where the mailboxes
	reside. For additional information about how to configure that access, click the
	article number below to view the article in the Microsoft Knowledge Base:
	
	  Q179442 How to Configure a Firewall for Domains and Trusts
	
	Additional query words: XMRP
	
	======================================================================
	Keywords          :  
	Technology        : kbOutlookSearch kbExchangeSearch kbExchange550 kbZNotKeyword2 kbOWASearch kbOWA550
	Version           : :5.5
	Issue type        : kbhowto
	
	=============================================================================
	

{% endraw %}
