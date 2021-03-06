---
layout: page
title: "Q218430: XCLN: Client SMTP Connectivity Using Secure Socket Layer"
permalink: /kb/218/Q218430/
---

## Q218430: XCLN: Client SMTP Connectivity Using Secure Socket Layer

{% raw %}

	Article: Q218430
	Product(s): Microsoft Exchange
	Version(s): 4.0,5.0,5.5,8.0,8.01,8.02,8.03
	Operating System(s): 
	Keyword(s): 
	Last Modified: 15-OCT-2001
	
	-------------------------------------------------------------------------------
	The information in this article applies to:
	
	- Microsoft Exchange Server, version 5.5 
	- Microsoft Outlook 97, versions 8.0, 8.01, 8.02, 8.03 
	- Microsoft Outlook 98 
	- Microsoft Exchange Windows 95/98 client, versions 4.0, 5.0 
	- Microsoft Exchange Windows NT client, versions 4.0, 5.0 
	-------------------------------------------------------------------------------
	
	SYMPTOMS
	========
	
	When you send SMTP messages from an Internet Mail Service-enabled client to an
	Exchange Server computer, you may want these documents sent in a secure fashion.
	When you configure an e-mail client, for example Outlook Express, to communicate
	by means of Secure Socket Layer (SSL) for this reason, you may receive the
	following error message:
	
	  The connection to the server has failed. Account: 'Account name', Server:
	  'Server name',
	  Protocol: SMTP, Port 465, Secure (SSL): Yes, Socket Error: 10061, Error
	  Number:
	  0x800CCC0E
	
	This indicates that the client was unable to connect to the server.
	
	There will not be any event logged on the Exchange Server computer.
	
	CAUSE
	=====
	
	Microsoft clients configured to send SMTP message by means of SSL are not able
	to communicate correctly with the Exchange Server computer. When SSL is enabled
	on an e-mail client, the communication port defaults to port 465, defined by
	Netscape. When the client issues an SMTP command to send a message, the Internet
	Mail Service does not receive the communication because it is monitoring port
	25.
	
	If you change the port within the client to use port 25, and you try to resend
	the message, Exchange Server still will not respond because the client is
	issuing SSL commands to the server, while the server only understands Transport
	Layer Security (TLS) command sets. Because the two computers are speaking a
	different security protocol, they will not be able to negotiate a session.
	
	RESOLUTION
	==========
	
	At this time, SSL-enabled Microsoft Internet mail clients send security command
	requests (SSL) that are incompatible with the Exchange Server Internet Mail
	Service security command set (TLS). Consequently, there is no way of using this
	configuration for sending SMTP secure mail. Outlook Express 5, as well as
	Outlook 2000, will include support for TLS over port 25. Both of these products
	will support the TLS command set.
	
	WORKAROUND
	==========
	
	There are a two workarounds that will work until the Outlook Express 5 and
	Outlook 2000 products are released.
	
	- Communicate with your Exchange Server computer through Point-To-Point
	  Tunneling Protocol (PPTP), which will encapsulate all messages sent to or
	  received from the server.
	
	For additional information, please see the following article in the Microsoft
	Knowledge Base:
	
	  Q180979 OL97: Using Outlook with a PPTP Connection
	
	-or-
	
	- Use message encryption by means of certificates to send and receive messages
	  securely and discretely.
	
	MORE INFORMATION
	================
	
	Additional information on the following subjects can be found at the following
	locations:
	
	TLS
	---
	
	  ftp://ftp.isi.edu/in-notes/rfc2246.txt
	
	Message Encryption
	------------------
	
	  Q197974 XCLN: How to Send Encrypted Mail to a User in Another Organization
	
	Additional query words: 8.0 8.01 8.02 8.03 8.5
	
	======================================================================
	Keywords          :  
	Technology        : kbOutlookSearch kbExchangeSearch kbExchange550 kbExchangeClientSearch kbZNotKeyword kbOutlook97 kbZNotKeyword2 kbOutlook97Search kbOutlook98Search kbZNotKeyword3 kbOutlook801 kbOutlook802 kbOutlook803 kbExchange400NT kbExchange500NT kbExchange400Win95 kbExchange500Win95
	Version           : :4.0,5.0,5.5,8.0,8.01,8.02,8.03
	Issue type        : kbprb
	
	=============================================================================
	

{% endraw %}
