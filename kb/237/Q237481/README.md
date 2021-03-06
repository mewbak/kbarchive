---
layout: page
title: "Q237481: XADM: Event 1023 Using Mailbox Manager w. Clean Remote Mailbox"
permalink: /kb/237/Q237481/
---

## Q237481: XADM: Event 1023 Using Mailbox Manager w. Clean Remote Mailbox

{% raw %}

	Article: Q237481
	Product(s): Microsoft Exchange
	Version(s): winnt:5.5,5.5 SP1,5.5 SP2,5.5 SP3
	Operating System(s): 
	Keyword(s): exc55 exc55sp1 exc55sp2 exc55sp3
	Last Modified: 26-MAR-2000
	
	-------------------------------------------------------------------------------
	The information in this article applies to:
	
	- Microsoft Exchange Server, versions 5.5, 5.5 SP1, 5.5 SP2, 5.5 SP3 
	-------------------------------------------------------------------------------
	
	
	SYMPTOMS
	========
	
	If you install Mailbox Manager on one server in a site and use it to clean
	mailboxes on another server in the site, the following error message is logged
	in the application event log:
	
	  Event ID: 1023
	  Source: MSExchangeIS Private
	  Type: Failure Audit
	  Category: Logons
	  Description:
	  Domain\ServiceAccount was validated as
	  /o=Organization/ou=Site/cn=Configuration/cn=Add-Ins/cn= MCAServerName but was
	  unable to log on to /o=Organization/ou=Site/cn=Recipients/cn=userA1.
	
	Even though the 1023 error message indicates that the Mailbox Manager was unable
	to log on to the remote mailbox, the remote mailbox is cleaned. Note that a 1023
	error message is logged for each remote mailbox that you clean.
	
	STATUS
	======
	
	Microsoft has confirmed this to be a problem in the Microsoft products that are
	listed at the beginning of this article.
	
	
	Additional query words: MSExchangeIS Private
	
	======================================================================
	Keywords          : exc55 exc55sp1 exc55sp2 exc55sp3 
	Technology        : kbExchangeSearch kbExchange550 kbZNotKeyword2 kbExchange550SP1 kbExchange550SP2 kbExchange550SP3
	Version           : winnt:5.5,5.5 SP1,5.5 SP2,5.5 SP3
	Issue type        : kbbug
	Solution Type     : kbnofix
	
	=============================================================================
	

{% endraw %}
