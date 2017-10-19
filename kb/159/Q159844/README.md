---
layout: page
title: "Q159844: XADM: Setup Editor Cannot Create Some Services in Default.prf"
permalink: /kb/159/Q159844/
---

## Q159844: XADM: Setup Editor Cannot Create Some Services in Default.prf

	Article: Q159844
	Product(s): Microsoft Exchange
	Version(s): winnt:4.0,5.0
	Operating System(s): 
	Keyword(s): kbsetup kbusage
	Last Modified: 11-APR-1999
	
	-------------------------------------------------------------------------------
	The information in this article applies to:
	
	- Microsoft Exchange Server, versions 4.0, 5.0 
	-------------------------------------------------------------------------------
	
	SYMPTOMS
	========
	
	An administrator uses Microsoft Exchange Setup Editor to select the following
	information services:
	
	  Microsoft Exchange Server
	  Personal Address Book
	  Personal Folders
	  Microsoft Mail
	
	However, after users install Microsoft Exchange clients by running Setup.exe at
	the client installation point, the automatically generated default Microsoft
	Exchange profile has only the following information services:
	
	  Microsoft Exchange Server
	  Personal Address Book
	
	CAUSE
	=====
	
	The [Service List] section in the Default.prf file generated by the Setup Editor
	contains only the following services:
	
	  Service1=Microsoft Exchange Client
	  Service2=Microsoft Exchange Server
	  Service3=Personal Address Book
	
	WORKAROUND
	==========
	
	Before users install the Microsoft Exchange clients, the Default.prf at the
	client installation point has to be manually modified using a text editor. The
	following is a sample of the modified Default.prf file. (Section 4 is omitted
	here for simplicity.)
	
	; Sample PRF file
	; ---------------
	; Copyright (C), Microsoft Corporation, 1996.
	;
	; The following PRF file is included as an example of how to create a PRF
	; file for creating a profile.  Sections 1, 2, and 3 can be modified. DO
	; NOT MODIFY SECTION 4. It will most likely cause Microsoft Exchange
	; services to stop responding. Be very careful when editing to ensure
	; property values match their property types.
	;
	; Section 1 - Profile defaults
	
	[General]
	ProfileName=Default Exchange Profile
	DefaultProfile=Yes
	OverwriteProfile=No
	DefaultStore=Service2
	
	; ************************************************************************
	; ************************************************************************
	; ************************************************************************
	; Section 2 - Services in profile.
	
	[Service List]
	Service1=Microsoft Exchange Client
	Service2=Microsoft Exchange Server
	Service3=Personal Address Book
	Service4=Microsoft Mail
	Service5=Personal Folders
	
	; ************************************************************************
	; ************************************************************************
	; ************************************************************************
	; Section 3 - Default values for each service.
	
	[Service1]
	NotifyPlaySound=TRUE
	NotifyChangeCursor=TRUE
	NotifyShowPopup=FALSE
	WarnOnDelete=TRUE
	EmptyWastebasket=TRUE
	ShowTooltips=TRUE
	SelectEntireWord=TRUE
	AfterMoveMessage=2
	IncludeMessageText=TRUE
	IndentMessageText=TRUE
	CloseOriginalMessage=TRUE
	GenReadReceipt=FALSE
	GenDeliveryReceipt=FALSE
	DefaultSensitivity=0
	DefaultPriority=1
	SaveSentMail=TRUE
	SpellAlwaysSuggest=FALSE
	CheckSpelling=FALSE
	SpellIgnoreUpper=FALSE
	SpellIgnoreNumbers=FALSE
	SpellIgnoreOriginal=FALSE
	
	[Service2]
	ConversionProhibited=TRUE
	HomeServer=server1
	ExchangeConfigFlags=4
	
	[Service3]
	PathToPersonalAddressBook=c:\exchange\mailbox.pab
	ViewOrder=1
	
	[Service4]
	ServerPath=\\server2\maildata
	
	[Service5]
	PathToPersonalFolders=c:\exchange\mailbox.pst
	EncryptionType=0x40000000
	
	; ************************************************************************
	; ************************************************************************
	; ************************************************************************
	; Section 4 - Mapping for profile properties.
	
	;
	
	Additional query words:
	
	======================================================================
	Keywords          : kbsetup kbusage 
	Technology        : kbExchangeSearch kbExchange500 kbExchange400 kbZNotKeyword2
	Version           : winnt:4.0,5.0
	
	=============================================================================
	