---
layout: page
title: "Q302669: XADM: Error Updating Meeting Requests After Mailbox ExMerge"
permalink: /kb/302/Q302669/
---

## Q302669: XADM: Error Updating Meeting Requests After Mailbox ExMerge

{% raw %}

	Article: Q302669
	Product(s): Microsoft Exchange
	Version(s): 5.5,5.5 SP1,5.5 SP2,5.5 SP3,5.5 SP4
	Operating System(s): 
	Keyword(s): kbExchange550preSP5fix
	Last Modified: 13-JUN-2002
	
	-------------------------------------------------------------------------------
	The information in this article applies to:
	
	- Microsoft Exchange Server, versions 5.5, 5.5 SP1, 5.5 SP2, 5.5 SP3, 5.5 SP4 
	-------------------------------------------------------------------------------
	
	
	IMPORTANT: This article contains information about modifying the registry. Before you modify the registry, make sure to back it up and make sure that you understand how to restore the registry if a problem occurs. For information about how to back up, restore, and edit the registry, click the following article number to view the article in the Microsoft Knowledge Base:
	
	  Q256986 Description of the Microsoft Windows Registry
	
	SYMPTOMS
	========
	
	After you use the ExMerge resource kit utility (or other unsupported means) to
	move mailbox data between Exchange Server 5.5 sites, organizations, or between
	recipients containers within the same site, when a user tries to use a client to
	modify and resend an appointment with invitees, or to resend a message from the
	sent items folder, the user may receive the following error message:
	
	  You do not have the permission to send the message on behalf of the specified
	  user.
	
	CAUSE
	=====
	
	To resolve this problem, this fix adds a registry value that you can use to make
	the information store look up X.500 proxy addresses even if the Move Server
	Wizard was never run. Code is added to the information store to handle cases in
	which ExMerge was used to move mailboxes between Exchange 5.5 sites or
	organizations. To enable the new functionality, first edit the registry to add
	the AlwaysLookupX500Proxy value using the procedure outlined below, then apply
	the fix that is described in the "Resolution" section of this article to the
	affected Exchange Server 5.5 SP4 computer."
	
	ExMerge does not update the distinguished names of the message sender. When a
	user whose mailbox has been moved attempts to resend one of the messages, the
	information store does not perform lookups of X.500 proxy addresses by default.
	This causes the permissions error message that is described in the "Symptoms"
	section of this article. If you use the Move Server Wizard, the information
	store can perform lookups of X.500 proxies.
	
	ExMerge is a BackOffice Resource Kit utility, and therefore falls under the
	BackOffice Resource Kit utilities support boundaries. For additional
	information, click the article number below to view the article in the Microsoft
	Knowledge Base:
	
	  Q303056 XADM: BackOffice Resource Kit Utility Support Boundaries
	
	RESOLUTION
	==========
	
	A supported fix is now available from Microsoft, but it is only intended to
	correct the problem described in this article and should be applied only to
	systems experiencing this specific problem. This fix may receive additional
	testing at a later time, to further ensure product quality. Therefore, if you
	are not severely affected by this problem, Microsoft recommends that you wait
	for the next Microsoft Exchange Server 5.5 service pack that contains this fix.
	
	To resolve this problem immediately, contact Microsoft Product Support Services
	to obtain the fix. For a complete list of Microsoft Product Support Services
	phone numbers and information about support costs, please go to the following
	address on the World Wide Web:
	
	  http://support.microsoft.com/default.aspx?scid=fh;EN-US;CNTACTMS
	
	NOTE: In special cases, charges that are normally incurred for support calls may
	be canceled, if a Microsoft Support Professional determines that a specific
	update will resolve your problem. Normal support costs will apply to additional
	support questions and issues that do not qualify for the specific update in
	question.
	
	The English version of this fix should have the following file attributes or
	later:
	
	Component: Information store
	
	+-------------------------+
	| File name | Version     | 
	+-------------------------+
	| Store.exe | 5.5.2655.20 | 
	+-------------------------+
	
	NOTE: Because of file dependencies, this fix requires Microsoft Exchange Server
	version 5.5 Service Pack 4.
	
	
	
	STATUS
	======
	
	Microsoft has confirmed this to be a problem in Microsoft Exchange Server
	version 5.5.
	
	MORE INFORMATION
	================
	
	WARNING: If you use Registry Editor incorrectly, you may cause serious problems
	that may require you to reinstall your operating system. Microsoft cannot
	guarantee that you can solve problems that result from using Registry Editor
	incorrectly. Use Registry Editor at your own risk.
	To resolve this problem, this fix adds a registry value that you can use to make
	the information store look up X.500 proxy addresses even if the Move Server
	Wizard was never run. Code is added to the information store to handle cases in
	which ExMerge was used to move mailboxes between Exchange Server 5.5 sites or
	organizations. To enable the new functionality, apply the fix that is described
	in the "Resolution" section of this article to the affected Exchange Server 5.5
	SP4 computer, and then edit the registry to add the AlwaysLookupX500Proxy
	value.
	
	To add the AlwaysLookupX500Proxy value:
	
	1. Start Registry Editor (Regedt32.exe).
	
	2. Locate and click the following key in the registry:
	
	  HKEY_LOCAL_MACHINE\CurrentControlSet\Services\MSExchangeIS\ParametersSystem
	
	3. On the Edit menu, click Add Value, and then add the following registry value:
	
	  Value name: AlwaysLookupX500Proxy
	  Data type: REG_DWORD
	  Radix: Decimal
	  Value data: 1
	
	4. Quit Registry Editor.
	
	You must stop and restart the Exchange Server Information Store service for the
	change to take effect.
	
	To turn off this functionality, change the preceding value data to 0, and then
	restart the Exchange Server Information Store service.
	
	You also need to add an X.500 proxy address that points back to the old
	Obj-Dist-Name to each mailbox that has been moved. For example, if a mailbox in
	the source site or organization had the following Obj-Dist-Name
	
	  /o=Organization/ou=Site/cn=Recipients/cn=Mailbox
	
	you need to create an X.500 proxy address for the mailbox in the destination
	organization or site as follows:
	
	  E-mail address: /o=Organization/ou=Site/cn=Recipients/cn=Mailbox
	  E-mail type: X500
	
	Additional query words: reskit bork
	
	======================================================================
	Keywords          : kbExchange550preSP5fix 
	Technology        : kbExchangeSearch kbExchange550 kbZNotKeyword2 kbExchange550SP1 kbExchange550SP2 kbExchange550SP3 kbExchange550SP4
	Version           : :5.5,5.5 SP1,5.5 SP2,5.5 SP3,5.5 SP4
	Issue type        : kbbug
	Solution Type     : kbfix
	
	=============================================================================
	

{% endraw %}
