---
layout: page
title: "Q188856: XCLN: Names of Mailbox Folders Appear in Different Languages"
permalink: /kb/188/Q188856/
---

## Q188856: XCLN: Names of Mailbox Folders Appear in Different Languages

{% raw %}

	Article: Q188856
	Product(s): Microsoft Exchange
	Version(s): 4.0,5.0,5.5
	Operating System(s): 
	Keyword(s): 
	Last Modified: 13-JUN-2002
	
	-------------------------------------------------------------------------------
	The information in this article applies to:
	
	- Microsoft Exchange Server, versions 4.0, 5.0, 5.5 
	-------------------------------------------------------------------------------
	
	SYMPTOMS
	========
	
	Names of standard folders in an Exchange mailbox, such as the Inbox, Sent Items,
	Public Folders, and so on, appear in different languages when seen from the
	client program.
	
	CAUSE
	=====
	
	Most of the standard folders seen from the client are stored on the server, but
	they are initially created and named by the first client to access the
	corresponding mailbox after it is created. Thus, if the first client you use to
	access a new mailbox is a French client, standard folders like the Inbox or Sent
	Items are given French names. After a folder is named, it retains that name
	unless you explicitly change it from the client. So if a client in a different
	language subsequently is used to access the mailbox, these standard folders
	still retain names in the language used by the client that created them. This
	does not affect functionality, but it may be somewhat confusing in appearance.
	
	Additionally, some folders are on the server (for example, all of the server
	mailbox folders). Others may be in a local .pst file, and still others are
	"virtual" folders that have no real existence (such as the Public Folders
	folder, which simply serves as a tree node for the public- folder tree of the
	organization). The server folders have names in the language of the client that
	first created them. Similarly, the .pst folders have names in the language of
	the client that created them (which may have been a different client from the
	one that created the server folders). Finally, the virtual folders always have
	names in the language of the client that is currently displaying them (because
	they have no existence independent of the client program). The net result is
	that you may see standard folders with names in a variety of languages, if
	clients in different languages have been used to access the mailbox or any
	.psts.
	
	Again, none of this affects functionality, and you may change the names of the
	folders at any time. The problem is only aesthetic.
	
	
	WORKAROUND
	==========
	
	The names of the folders can be changed at any time, at your discretion, from
	your client program.
	
	Some clients (for example, Outlook 2000 or older) do not allow the names of
	certain standard folders (for example, the Inbox) to be changed, but this is a
	client restriction and not an intrinsic limitation of Exchange. In these cases,
	you must use a different client (such as the older Exchange client) to modify
	the folder names.
	
	Outlook 2002 clients can run a command line switch to rename the default folders
	to the language of the client. To do this, click Start, click Run, and then type
	"Outlook.exe /resetfoldernames" (without the quotation marks). Outlook will
	start normally and the default folder names will be in the language of the
	client.
	
	With Outlook 2002 and the CIW or CMW you might want to reset folder names for all
	users when you deploy Outlook to synchronize users' folder names to the User
	Interface Language of their version of Outlook. This could be useful, for
	example, if a corporate-wide process has initialized new mailboxes before new
	users have started Outlook for the first time. In this case, the mailboxes will
	end up with default folders in the language of the server. (Note that users can,
	instead, specify the /resetfoldernames option on the Outlook.exe command line to
	synchronize the folder names on their computer.)
	
	To reset folder names when deploying Outlook, perform the following steps:
	
	1. In the Custom Installation Wizard, go to the "Add/Remove Registry Entries"
	  page.
	
	2. Click Add to add a registry entry for ResetFolderNames.
	
	3. On the "Add/Modify Registry Entry" page, select or type the following:
	
	  a. Under Root:, click to select HKEY_CURRENT_USER.
	
	  b. Under Data type:, click to select Dword.
	
	  c. In the Key: field, type "Software/Microsoft/Office/10.0/Outlook/Setup"
	     (without the quotation marks).
	
	  d. In the "Value name:" field, type "ResetFolderNames" (without the quotation
	     marks).
	
	  e. In the "Value data:" field, type "1" (without the quotation marks).
	
	  Any non-zero value will cause Outlook to synchronize the user's folder names
	  to the User Interface Language of Outlook.
	
	4. Click OK to save the entry.
	
	STATUS
	
	This behavior is by design.
	
	MORE INFORMATION
	================
	
	If you are administering a multilingual user community, you may want to suggest
	to users that they use a client in their preferred language to access their
	mailbox for the first time, so that the folders are created in the language they
	prefer. Note that only the language of the client matters; the settings of the
	OS and the server are not important.
	
	In the case of mixed wide-character (DBCS/Unicode) clients and other clients,
	folders named in a wide-character client may have names that look like garbage
	characters when seen from other clients that do not support wide-character
	strings. This has no effect on functionality, but it can mislead users into
	thinking that the system is "broken." Wide-character names display correctly
	only with clients and operating systems that can handle wide-character strings
	(such as Japanese or Chinese versions of such products).
	
	NOTE: References to the client software in this article are generic and refer to
	any program that can create or modify folders. This includes not only
	traditional e-mail client programs but also administrative migration or support
	utilities that access stores to perform various functions unrelated to normal
	sending and receiving of e-mail. These latter programs often create folders
	also, and when they do, generally they create the folders in the language of the
	program. This is an important consideration when using utilities like ExMerge
	(BackOffice Resource Kit III). The language version of these utilities should be
	carefully chosen when they are used by administrators.
	
	
	Additional query words: outlook determine
	
	======================================================================
	Keywords          :  
	Technology        : kbExchangeSearch kbExchange500 kbExchange550 kbExchange400 kbZNotKeyword2
	Version           : :4.0,5.0,5.5
	Issue type        : kbprb
	
	=============================================================================
	

{% endraw %}
