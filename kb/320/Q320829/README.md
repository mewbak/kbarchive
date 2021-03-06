---
layout: page
title: "Q320829: HOW TO: Modify the Default SizReqBuf Value in Windows 2000"
permalink: /kb/320/Q320829/
---

## Q320829: HOW TO: Modify the Default SizReqBuf Value in Windows 2000

{% raw %}

	Article: Q320829
	Product(s): Microsoft Windows NT
	Version(s): 
	Operating System(s): 
	Keyword(s): kbAudITPro kbHOWTOmaster
	Last Modified: 11-JUN-2002
	
	IMPORTANT: This article contains information about modifying the registry. Before you modify the registry, make sure to back it up and make sure that you understand how to restore the registry if a problem occurs. For information about how to back up, restore, and edit the registry, click the following article number to view the article in the Microsoft Knowledge Base:
	
	  Q256986 Description of the Microsoft Windows Registry
	
	IN THIS TASK
	------------
	
	- SUMMARY
	
	   - How to Increase the SizReqBuf Value
	
	SUMMARY
	=======
	
	This article describes how to modify the size of the SizReqBuf value. In File
	and Printer Sharing for Microsoft Networks, the SizReqBuf value determines how
	much data is buffered at one time to send to a client. The default values in
	Windows 2000 provide acceptable levels of performance in typical scenarios.
	However, on a high-latency connection, you may want to use an increased
	SizReqBuf value.
	
	By default, all Windows 2000 installations use a SizReqBuf value of 16,644
	bytes.
	
	How to Increase the SizReqBuf Value
	-----------------------------------
	
	WARNING: If you use Registry Editor incorrectly, you may cause serious problems
	that may require you to reinstall your operating system. Microsoft cannot
	guarantee that you can solve problems that result from using Registry Editor
	incorrectly. Use Registry Editor at your own risk.
	
	The SizReqBuf value is stored in the registry under the following registry key:
	
	  HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\LanmanServer\Parameters
	
	The SizReqBuf value is a REG_DWORD value, with a range of from 512 to 65536.
	
	NOTE: Increasing the SizReqBuf value can increase performance significantly in a
	high-latency environment. However, note that increasing the SizReqBuf value also
	increases the non-paged pool memory that is used by the LanManServer service. If
	you increase the SizReqBuf value, make sure to monitor non-paged pool to make
	sure that the change does not affect the performance of the file server.
	
	Increasing the SizReqBuf value also proportionately increases the risk that a
	malicious user might use up non-paged pool on the file server.
	
	Additional query words:
	
	======================================================================
	Keywords          : kbAudITPro kbHOWTOmaster 
	Technology        : kbOSWin2000 kbOSWinSearch
	Issue type        : kbhowto
	
	=============================================================================
	

{% endraw %}
