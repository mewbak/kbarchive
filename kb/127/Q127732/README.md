---
layout: page
title: "Q127732: SMTP: Configuring LAN Manager 2.2c MS-DOS Client w/ TCP/IP"
permalink: /kb/127/Q127732/
---

## Q127732: SMTP: Configuring LAN Manager 2.2c MS-DOS Client w/ TCP/IP

{% raw %}

	Article: Q127732
	Product(s): Microsoft Mail For PC Networks
	Version(s): MS-DOS:3.0
	Operating System(s): 
	Keyword(s): 
	Last Modified: 29-OCT-1999
	
	-------------------------------------------------------------------------------
	The information in this article applies to:
	
	- Microsoft Mail Gateway to SMTP, version 3.0 
	-------------------------------------------------------------------------------
	
	SUMMARY
	=======
	
	The Microsoft Mail Gateway to SMTP computer requires TCP/IP to be loaded (refer
	to page 2 of the "Administrator's Guide"). However, it is not required to load
	any other protocols on the dedicated workstation. Below are the configuration
	files for a properly configured Microsoft LAN Manager MS-DOS client using only
	TCP/IP.
	
	Boot files
	----------
	
	CONFIG.SYS:
	
	  DEVICE=C:\DOS\Himem.sys
	  DEVICE=C:\DOS\EMM386.EXE NOEMS
	  Buffers=15,0
	  Files=40
	  DOS=UMB
	  LASTDRIVE=Z
	  DOS=HIGH
	  DEVICE=C:\LM\DRIVERS\PROTMAN\PROTMAN.DOS /i:C:\LM
	  DEVICEHIGH /L:1,10000 =C:\LM\DRIVERS\ETHERNET\EXP16\DEPCA.DOS
	  DEVICEHIGH /L:1,4176 =C:\LM\DRIVERS\PROTOCOL\TCPIP\TCPDRV.DOS /I:C:\LM
	  DEVICEHIGH /L:2,2624 =C:\LM\DRIVERS\PROTOCOL\TCPIP\NEMM.DOS
	
	AUTOEXEC.BAT:
	
	  Prompt=$p$g
	  @REM ==== LANMAN 2.2 =======
	  SET PATH=C:\LM\NETPROG;c:\;c:\dos;%PATH%
	  LH C:\LM\DRIVERS\PROTOCOL\tcpip\umb.com
	  NET START WORKSTATION
	  LOAD TCPIP
	  NET LOGON
	  @REM ==== LANMAN 2.2 =======
	
	LAN Manager Files Found in C:\LM\*.INI
	--------------------------------------
	
	PROTOCOL.INI:
	
	  [PROTMAN]
	  DRIVERNAME = PROTMAN$
	  DYNAMIC = YES
	  PRIORITY = TCPIP
	
	  [TCPIP_XIF]
	  DRIVERNAME      = TCPIP$
	  IPADDRESS0  = 22 100 49 117
	  SUBNETMASK0    = 255 255 0 0
	  DEFAULTGATEWAY0 = 22 100 0 1
	  NBSESSIONS  = 2
	  ; the following two parameters added after documentation was completed
	  TCPSEGMENTSIZE  = 1450
	  TCPWINDOWSIZE   = 1450
	  LOAD            = tcptsr[c],tinyrfc[c],emsbfr[cr]
	  UNLOAD          = "unloadt /notsr[dc]"
	  BINDINGS    = "DEPCA_NIF"
	  LANABASE    = 0
	  FORCEPUSHBIT= 1
	
	  [DEPCA_NIF]
	  ; protocol.ini section for the DEC EtherWORKS (MC, LC, Turbo & DEPCA)
	  ; Adapters
	
	     DriverName     = DEPCA$
	     MaxMulticast   = 12
	     MaxTransmits   = 32
	     AdapterName    = DE200
	     RamAddress     = 0xD000
	     :Interrupt     = 3
	
	  Interupt        = 5               ; for turbo board
	  TCPUTILS.INI
	  [TCPGLOBAL]
	  DRIVERNAME      = GLOBAL$
	  HOSTNAME        = LMUSER
	
	  [SOCKETS]
	  DRIVERNAME      = SOCKETS$
	  BINDINGS        = TCPIP_XIF
	  ; the following value changed from 8 to 4 (after documentation was
	  ; complete)
	  NUMSOCKETS  = 4
	  NUMTHREADS      = 32
	  POOLSIZE        = 3200
	  MAXSENDSIZE     = 1024
	  [TELNET]
	  DRIVERNAME      = TELNET$
	  BINDINGS        = TCPIP_XIF
	  NSESSIONS   = 2
	  MAX_OUT_SENDS   = 0
	
	LANMAN.INI:
	
	  ;*****************************************************************;
	  ;**                  Microsoft LAN Manager                      **;
	  ;**            Copyright(c) Microsoft Corp., 1992               **;
	  ;*****************************************************************;
	  [networks]
	  netservices = chknet, minses
	  [workstation]
	  wrkservices = encrypt,messenger
	  computername = Mrgateway
	  domain = mydomain
	  othdomains =
	  numdgrambuf = 3
	  lanroot = C:\LM
	  [netshell]
	  username = SMTPGATE
	  [version]
	  lan_manager = 2.2.c
	  [messenger]
	
	  [services]
	  chknet        = netprog\chknet.exe
	  minses        = netprog\minses.exe /n
	  workstation   = netprog\netwksta.exe
	  messenger     = services\msrv.exe
	  encrypt       = services\encrypt.exe
	
	Additional query words: MSClient
	
	======================================================================
	Keywords          :  
	Technology        : kbMailSearch kbMailGateSearch kbZNotKeyword3 kbMailGateSMTP300
	Version           : MS-DOS:3.0
	
	=============================================================================
	

{% endraw %}
