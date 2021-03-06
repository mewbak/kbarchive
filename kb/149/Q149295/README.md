---
layout: page
title: "Q149295: Win 95 SNA Client May Hang on Startup with Anti-cmos Virus"
permalink: /kb/149/Q149295/
---

## Q149295: Win 95 SNA Client May Hang on Startup with Anti-cmos Virus

{% raw %}

	Article: Q149295
	Product(s): Microsoft SNA Server
	Version(s): WINDOWS:2.1,2.11,3.0,4.0
	Operating System(s): 
	Keyword(s): kbusage
	Last Modified: 13-JUN-2001
	
	-------------------------------------------------------------------------------
	The information in this article applies to:
	
	- Microsoft SNA Server, versions 2.1, 2.11, 3.0, 4.0, on platform(s):
	   - the operating system: Microsoft Windows NT 
	-------------------------------------------------------------------------------
	
	SYMPTOMS
	========
	
	Infection by the anti-cmos virus can cause the Microsoft Windows 95 SNA client
	to hang or return the following error message:
	
	  No SNA server found in domain.
	
	CAUSE
	=====
	
	You will get the above error when you start the SNA Server Windows 95 client
	SNABASE process when it is configured for named pipes over the NetBEUI transport
	only, though may occur over other named pipes transports.
	
	WORKAROUND
	==========
	
	Remove the virus from the client computer to resolve this problem.
	
	MORE INFORMATION
	================
	
	The SNA Server client internal traces and network captures show two behaviors
	when you use named pipes over NetBEUI.
	
	- The client makes an IPC$ connection to the SNA Server; it posts a Server
	  Message Block (SMB) Read Request, and then hangs.
	
	  Sample Network Capture
	  ----------------------
	
	  Frame   Time    Src MAC Addr Dst MAC Addr   Protocol  Description
	
	  1       6.010   CLIENT       SERVER         NETBIOS   Session Alive (0x1F)
	  2       6.210   SERVER       CLIENT          LLC       RR DSAP=0xF0
	  SSAP=0xF1 R N(R) = 0x25
	  3       19.440  CLIENT       *NETBIOS Multi  BROWSER   Host Announcement
	  [0x01] CLIENT
	  4       23.794  SERVER       CLIENT          LLC       RR DSAP=0xF0
	  SSAP=0xF0 C N(R) = 0x25 POLL
	  5       23.794  CLIENT       SERVER          LLC       RR DSAP=0xF0
	  SSAP=0xF1 R N(R) = 0x1C FINAL
	  6       48.279  CLIENT       *NETBIOS Multi  SMB       C transact, File =
	  \MAILSLOT\SNADMOD
	  7       48.280  CLIENT       *NETBIOS Multi  SMB       C transact, File =
	  \MAILSLOT\SNADMOD
	  8       48.500  CLIENT       SERVER          SMB       C tree connect & X,
	  Share = \\SERVER\IPC$
	  9       48.501  SERVER       CLIENT          SMB       R tree connect & X,
	  Type = IPC
	  10      48.502  CLIENT       SERVER          SMB       C open & X, File =
	  \PIPE\COMNAP (RW -Share Deny None)
	  11      48.504  SERVER       CLIENT          SMB       R open & X, FID =
	  0x1812
	  12      48.504  CLIENT       SERVER          SMB       C transact
	  SetNmPHandState, FID = 0x1812
	  13      48.506  SERVER       CLIENT          SMB       R transact
	  14      48.510  CLIENT       SERVER          SMB       C write & X, FID =
	  0x1812, Write 0xb4 at 0x00000000
	  15      48.511  SERVER       CLIENT          SMB       R write & X, Wrote
	  0xb4
	  16      48.512  CLIENT       SERVER          SMB       C read & X, FID =
	  0x1812, Read 0x800 at 0x00000000
	  17      48.547  SERVER       CLIENT          NETBIOS   Data Ack (0x14): LSN
	  = 0x17, RSN = 0x09
	  18      48.896  CLIENT       SERVER          LLC       RR DSAP=0xF0
	  SSAP=0xF1 R N(R) = 0x21
	  19      56.504  CLIENT       SERVER          NETBIOS   Session Alive (0x1F)
	  20      56.668  SERVER       CLIENT          LLC       RR DSAP=0xF0
	  SSAP=0xF1 R N(R) = 0x2B
	  21      79.869  SERVER       CLIENT          LLC       RR DSAP=0xF0
	  SSAP=0xF0 C N(R) = 0x2B POLL
	  22      79.870  CLIENT       SERVER          LLC       RR DSAP=0xF0
	  SSAP=0xF1 R N(R) = 0x21 FINAL
	  23      108.001 CLIENT       SERVER          NETBIOS   Session Alive (0x1F)
	  24      108.197 SERVER       CLIENT          LLC       RR DSAP=0xF0
	  SSAP=0xF1 R N(R) = 0x2C
	  25      111.912 SERVER       CLIENT          LLC       RR DSAP=0xF0
	  SSAP=0xF0 C N(R) = 0x2C POLL
	  26      111.912 CLIENT       SERVER          LLC       RR DSAP=0xF0
	  SSAP=0xF1 R N(R) = 0x21 FINAL
	  27      143.956 SERVER       CLIENT          LLC       RR DSAP=0xF0
	  SSAP=0xF0 C N(R) = 0x2C POLL
	  28      143.956 CLIENT       SERVER          LLC       RR DSAP=0xF0
	  SSAP=0xF1 R N(R) = 0x21 FINAL
	  29      159.484 CLIENT       SERVER          NETBIOS   Session Alive (0x1F)
	
	- If the Local Domain option is selected, the SNA client repeats the mailslot
	  broadcast, but does not appear to see the SNA Server's response.
	
	Sample Network Capture
	----------------------
	
	Frame   Time    Src MAC Addr   Dst MAC Addr   Protocol  Description
	
	1       2.750   CLIENT       SERVER          NETBIOS   Session Alive (0x1F)
	2       2.943   SERVER       CLIENT          LLC       RR DSAP=0xF0
	SSAP=0xF1 R N(R) = 0x33
	3       24.311  SERVER       CLIENT          LLC       RR DSAP=0xF0
	SSAP=0xF0 C N(R) = 0x33 POLL
	4       24.311  CLIENT       SERVER          LLC       RR DSAP=0xF0
	SSAP=0xF1 R N(R) = 0x27 FINAL
	5       53.876  CLIENT       SERVER          NETBIOS   Session Alive (0x1F)
	6       54.071  SERVER       CLIENT          LLC       RR DSAP=0xF0
	SSAP=0xF1 R N(R) = 0x34
	7       56.354  SERVER       CLIENT          LLC       RR DSAP=0xF0
	SSAP=0xF0 C N(R) = 0x34 POLL
	8       56.355  CLIENT       SERVER          LLC       RR DSAP=0xF0
	SSAP=0xF1 R N(R) = 0x27 FINAL
	9       63.122  CLIENT       *NETBIOS Multi  SMB       C transact, File =
	\MAILSLOT\SNADMOD
	10      63.123  CLIENT       *NETBIOS Multi  SMB       C transact, File =
	\MAILSLOT\SNADMOD
	11      68.392  CLIENT       *NETBIOS Multi  SMB       C transact, File =
	\MAILSLOT\SNADMOD
	12      68.393  CLIENT       *NETBIOS Multi  SMB       C transact, File =
	\MAILSLOT\SNADMOD
	13      73.666  CLIENT       *NETBIOS Multi  SMB       C transact, File =
	\MAILSLOT\SNADMOD
	14      73.667  CLIENT       *NETBIOS Multi  SMB       C transact, File =
	\MAILSLOT\SNADMOD
	15      78.939  CLIENT       *NETBIOS Multi  SMB       C transact, File =
	\MAILSLOT\SNADMOD
	16      78.940  CLIENT       *NETBIOS Multi  SMB       C transact, File =
	\MAILSLOT\SNADMOD
	17      84.212  CLIENT       *NETBIOS Multi  SMB       C transact, File =
	\MAILSLOT\SNADMOD
	18      84.213  CLIENT       *NETBIOS Multi  SMB       C transact, File =
	\MAILSLOT\SNADMOD
	19      88.397  SERVER       CLIENT          LLC       RR DSAP=0xF0
	SSAP=0xF0 C N(R) = 0x34 POLL
	20      88.397  CLIENT       SERVER          LLC       RR DSAP=0xF0
	SSAP=0xF1 R N(R) = 0x27 FINAL
	21      89.485  CLIENT       *NETBIOS Multi  SMB       C transact, File =
	\MAILSLOT\SNADMOD
	22      89.486  CLIENT       *NETBIOS Multi  SMB       C transact, File =
	\MAILSLOT\SNADMOD
	23      105.331 CLIENT       SERVER          NETBIOS   Session Alive (0x1F)
	24      105.530 SERVER       CLIENT          LLC       RR DSAP=0xF0
	SSAP=0xF1 R N(R) = 0x35
	
	The client's other network connections are unaffected. The anti-cmos virus is a
	boot sector virus. Because of the nature of viruses, it is not possible to know
	with any accuracy what part of the system this virus affects or the true
	identity of the virus.
	
	It has also been reported that the FORM_A virus may cause the same results as
	listed above. In each case, running a virus program will resolve the problem.
	
	Additional query words: prodsna win95
	
	======================================================================
	Keywords          : kbusage 
	Technology        : kbAudDeveloper kbSNAServSearch
	Version           : WINDOWS:2.1,2.11,3.0,4.0
	
	=============================================================================
	

{% endraw %}
