---
layout: page
title: "Q166875: 5250 Emulator Won't Connect Even Though Sessions Are Available"
permalink: /kb/166/Q166875/
---

## Q166875: 5250 Emulator Won't Connect Even Though Sessions Are Available

{% raw %}

	Article: Q166875
	Product(s): Microsoft SNA Server
	Version(s): WINDOWS:2.11,3.0
	Operating System(s): 
	Keyword(s): kbnetwork
	Last Modified: 11-JUN-2002
	
	-------------------------------------------------------------------------------
	The information in this article applies to:
	
	- Microsoft SNA Server, versions 2.11, 3.0 
	-------------------------------------------------------------------------------
	
	
	IMPORTANT: This article contains information about modifying the registry. Before you modify the registry, make sure to back it up and make sure that you understand how to restore the registry if a problem occurs. For information about how to back up, restore, and edit the registry, click the following article number to view the article in the Microsoft Knowledge Base:
	
	  Q256986 Description of the Microsoft Windows Registry
	
	SYMPTOMS
	========
	
	When connecting to an AS/400, the 5250 applet shows Not Connected in the lower
	left corner. SNA Server shows that there are sessions available for the LU-LU
	pair the 5250 applet is attempting to use. However, some of these LUs on the
	AS/400 are in an Active - Detached state, thereby preventing the request for
	conversation from succeeding. The same thing will happen with other 5250
	emulators. However, the message displayed in the emulator may be different.
	
	NOTE: There are various situations in which you might see a Not Connected 5250
	status. This article documents one possible situation. For other possible
	situations, see the following Microsoft Knowledge Base article:
	
	  Q150796 5250 Emulator Displays a BlackScreen Then Disconnects
	
	CAUSE
	=====
	
	The exact cause of why the AS/400 sometimes shows sessions in an Active -
	Detached state is unknown.
	
	WORKAROUND
	==========
	
	To work around this problem, apply the fix referenced below, and then edit the
	registry as follows.
	
	NOTE: You must first apply the fix referenced below before editing the registry.
	
	WARNING: Using Registry Editor incorrectly can cause serious, system-wide
	problems that may require you to reinstall Windows NT to correct them. Microsoft
	cannot guarantee that any problems resulting from the use of Registry Editor can
	be solved. Use this tool at your own risk.
	
	1. Start Registry Editor (Regedt32.exe or Regedit.exe, as appropriate for your
	  version of Windows NT).
	
	2. Go to the following key in the registry:
	
	HKEY_LOCAL_ MACHINE\SYSTEM\CurrentControlSet\Services\SnaServr\ 
	  Parameters
	
	3. On the Edit menu, click Add Value and use the following entry:
	
	  Value Name: SessionLimitMargin
	  Data Type: REG_SZ
	
	  This registry entry artificially lowers the number of post cnos negotiation by
	  the value specified. Therefore, if the negotiated session limit for an
	  LU-LU-MODE triplet is 8 and SessionLimitMargin is 2, the SNA Server service
	  node will only start 6 sessions on the triplet.
	
	4. Exit Registry Editor.
	
	This will work around the problem where SNA Server thinks it has sessions
	available and the AS/400 does not.
	
	STATUS
	======
	
	Microsoft has confirmed this to be a problem in SNA Server versions 2.11 and
	3.0. This problem was corrected in the latest SNA Server version 3.0 U.S.
	Service Pack. For information on obtaining this Service Pack, query on the
	following word in the Microsoft Knowledge Base (without the spaces):
	
	  S E R V P A C K
	
	
	MORE INFORMATION
	================
	
	The following will be seen in an SNA Server DLC trace:
	
	The SNA Server service, thinking it has sessions available for a conversation
	request, sends an Attach (02ff) for conversation to the AS/400:
	
	  DLC    ---------------------------------------------- 22:00:54.97
	  DLC    01020601->04160005 DLC DATA
	  DLC                       DAF:36 OAF:01 ODAI:off Normal
	  DLC                       RQE FMD FI BC EC DR1 PI CD
	  DLC
	  DLC    ---- Header  at address 00CC45EC, 1 elements ----
	  DLC    0B05537E 324F2C00 36010001 01001121     <..S~2O,.6......!>
	  DLC
	  DLC    ---- Element at address 011C68C8, start 10, end 233 ----
	  DLC    0B91203F 0502FF18 03D00040 0430F0F0     <.j ?.......@.000>
	  DLC    F50F0402 D7C3E209 014AB1D6 5ACABB72     <5...PCS..J.OZ..r>
	  DLC    8A160DC1 D7D7D54B D4E2E2D5 C1E2F1F6     <...APPNKMSSNAS16>
	  DLC    54310016 0A040001 00080000 00000000     <T1..............>
	  DLC    0001009E 12F5009A 12E20096 12A02000     <.....5...S.o.. .>
	  DLC    05100100 000023D9 E8C1D5C1 D7D7C1F1     <......#RYANAPPA1>
	  DLC    40F3F1F9 F74040C3 F2404040 40000000     <@3197@@C2@@@@...>
	  DLC    00000000 00000000 000026C4 E4E2C200     <..........&DUSB.>
	  DLC    F6F9F740 F0F3F740 40404040 40404040     <697@037@@@@@@@@@>
	  DLC    40404040 40404040 40E7F900 00000000     <@@@@@@@@@X9.....>
	  DLC    41C10000 00004040 40404040 4040D7C3     <AA....@@@@@@@@PC>
	  DLC    E2404040 40404040 D7C3E240 40404040     <S@@@@@@@PCS@@@@@>
	  DLC    40402040 40404040 40404040 40404040     <@@ @@@@@@@@@@@@@>
	  DLC    40404040 40404040 40404040 40404040     <@@@@@@@@@@@@@@@@>
	
	The AS/400 rejects the Attach with a 0846 0000 sense code promising the SNA
	Server the real error in a following message:
	
	  
	
	  DLC    ---------------------------------------------- 22:00:56.66
	  DLC    04160005->01020601 DLC DATA
	  DLC                       DAF:01 OAF:36 ODAI:off Normal
	  DLC                       -RSP FMD SD BC EC DR1
	  DLC
	  DLC    ---- Header  at address 00CC6AE4, 1 elements ----
	  DLC    0B05537E 324F2C00 01368000 0100BB00     <..S~2O,..6......>
	  DLC
	  DLC    ---- Element at address 011C68C8, start 10, end 16 ----
	  DLC    87900008 460000                         <g...F..         >
	
	Here is the actual error from the AS/400:
	
	  
	
	  DLC    ---------------------------------------------- 22:00:56.87
	  DLC    04160005->01020601 DLC DATA
	  DLC                       DAF:01 OAF:36 ODAI:off Normal
	  DLC                       RQE FMD FI BC EC DR1 PI CEB
	  DLC
	  DLC    ---- Header  at address 00CC5FEC, 1 elements ----
	  DLC    0B05537E 324F2C00 01360001 0100BB00     <..S~2O,..6......>
	  DLC
	  DLC    ---- Element at address 011C5440, start 10, end 19 ----
	  DLC    0B910107 07084B60 3100                  <.j....K`1.      >
	
	  Primary Sense:   084B - Requested Resources Not Available
	  Secondary Sense: 6031 - Transaction Program Not Available - Retry
	  Available.
	
	See SNA Formats Guide for the full text message.
	
	The third-party products discussed here are manufactured by vendors independent
	of Microsoft; we make no warranty, implied or otherwise, regarding these
	products' performance or reliability.
	
	Additional query words:
	
	======================================================================
	Keywords          : kbnetwork 
	Technology        : kbAudDeveloper kbSNAServSearch kbSNAServ300 kbSNAServ211
	Version           : WINDOWS:2.11,3.0
	Issue type        : kbbug
	Solution Type     : kbfix
	
	=============================================================================
	

{% endraw %}
