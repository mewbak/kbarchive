---
layout: page
title: "Q169326: Does InterNIC Think Your DNS Servers Are Working?"
permalink: /kb/169/Q169326/
---

## Q169326: Does InterNIC Think Your DNS Servers Are Working?

{% raw %}

	Article: Q169326
	Product(s): Microsoft Windows NT
	Version(s): WinNT:4.0
	Operating System(s): 
	Keyword(s): kbnetwork kbusage
	Last Modified: 10-AUG-2001
	
	-------------------------------------------------------------------------------
	The information in this article applies to:
	
	- Microsoft Windows NT Server version 4.0 
	-------------------------------------------------------------------------------
	
	SUMMARY
	=======
	
	Although InterNIC has required a primary and secondary name server in the past,
	it did not always fully verify their functionality. InterNIC is now consistently
	verifying whether the servers you have specified are lame. Lame, as defined by
	InterNIC, is "the condition whereby a name-space is delegated to an entity but
	that entity will not answer to that name". If the nslookup utility returns an
	authoritative answer (when queried for a Status Of Authority [SOA] resource
	record) for your domain name, then your servers are not considered lame.
	
	See the following on the InterNIC server for more information:
	
	InterNIC Lame Delegation Policy:
	
	  ftp://rs.internic.net/policy/internic/internic-domain-5.txt
	
	InterNIC Web site:
	
	  http://rs.internic.net
	
	MORE INFORMATION
	================
	
	How to Test Your DNS Server
	---------------------------
	
	In this article, you will be using the NSLOOKUP command-line utility provided
	with Windows NT Server. Type NSLOOKUP at an MS-DOS command prompt, then press
	Enter. This will start NSLOOKUP in interactive mode (as opposed to line mode).
	You will now see that the prompt is a greater than (>) sign. Type a question
	mark "?" without the quotes, and then press enter. This will give you the
	commands available for use in NSLOOKUP. Also, to quit gracefully from the
	NSLOOKUP utility, type "exit" and press enter.
	
	There are three commands you can use to test our name servers: SERVER, SET, and
	`NAME'. `NAME' is not actually a command, it is just the fully qualified domain
	name as specified in the WHOIS record. The WHOIS database is maintained by
	InterNIC and contains information for all domain names registered to it.
	
	For additional information, please see the following article in the Microsoft
	Knowledge Base:
	
	  Q169213 How to Verify Internet Domain Registration Info with InterNIC
	
	A sample WHOIS record for the Test.net domain:
	
	The whois client utility is not available with Windows NT. You can access this
	information through the World Wide Web at:
	
	  http://rs.internic.net/cgi-bin/whois
	
	-or-
	
	By telnet 198.41.0.5.
	
	Below is a what you would see using telnet:
	
	In Windows NT 4.0, click the Start button, click Run, and type "TELNET
	198.41.0.5" (without the quotation marks)
	
	You will see the following on your screen. Comments are preceded by *****
	
	Trying 198.41.0.5 port 23...
	Connected to 198.41.0.5.
	
	
	***************************************************************************
	* -- InterNIC Registration Services Center  --
	*
	* For wais, type:                    WAIS <search string> <return>
	* For the *original* whois type:     WHOIS [search string] <return>
	* For referral whois type:           RWHOIS [search string] <return>
	*
	* For user assistance call (703) 742-4777
	* Questions/Updates on the whois database to HOSTMASTER@internic.net
	* Please report system problems to ACTION@internic.net
	***************************************************************************
	Please be advised that use constitutes consent to monitoring
	(Elec Comm Priv Act, 18 USC 2701-2711)
	
	6/1/94
	We are offering an experimental distributed whois service called referral
	whois (RWhois). To find out more, look for RWhois documents, a sample
	client and server under:
	gopher: (rs.internic.net) InterNIC Registration Services ->
	       InterNIC Registration Archives -> pub -> rwhois
	       anonymous ftp: (rs.internic.net) /pub/rwhois
	Cmdinter Ver 1.3 Thu May 29 14:42:50 1997 EST
	[ansi] InterNIC >
	[ansi] InterNIC > whois TEST.NET
	Connecting to the rs Database . . . . . .
	Connected to the rs Database
	Test Communications (TEST3-DOM)
	  734 Crater Street
	  Charlotte, NC 28205
	  US
	
	  Domain Name: TEST.NET
	
	  Administrative Contact:
	     Administrator  (ADM214-ORG)  administrator@TEST.NET
	     704-342-4664 (FAX) 704-342-1144
	  Technical Contact, Zone Contact:
	     Test, Russ  (RO553)  russ@TEST.NET
	     704-342-4664 (FAX) 704-342-1144
	  Billing Contact:
	     Test, Lisa  (LL1079)  lisa@TEST.NET
	     704-342-4664 (FAX) 704-342-1144
	
	  Record last updated on 19-Dec-96.
	  Record created on 19-Dec-96.
	  Database last updated on 20-May-97 05:00:33 EDT.
	
	  Domain servers in listed order:
	
	  NS1.TEST.NET              123.123.123.253
	  HARRIS2.DIABLO1.COM  200.200.200.1
	
	Type a handle, name, mailbox, or other field, optionally preceded
	 by a keyword, like "host diis". Type "?" for short, 2-page
	 details, "HELP" for full documentation, or hit RETURN to exit.
	---> Do ^E to show search progress, ^G to abort a search or output <---
	Whois:
	
	Press ENTER to exit Whois.
	
	[ansi] InterNIC >
	
	*****Record the Domain servers listed in the WHOIS record and their ip
	*****addresses.
	
	[ansi] InterNIC > logout
	
	*****This is what you would expect from a properly configured name server
	*****and WHOIS record:
	
	*****(Remember, these are examples, please replace all mentions of
	*****ns1.test.net   with your primary DNS servers hostname and
	*****harris2.diablo1.com     with your secondary DNS servers hostname.)
	
	>
	>NSLOOKUP
	Default Server:  ntw.test.net
	Address:  200.200.200.5
	
	>SERVER ns1.test.net
	Default Server:  ns1.test.net
	Address:   123.123.123.253
	
	>SET TYPE=ANY
	>test.net
	Server:  ns1.test.net
	Address:  123.123.123.253
	
	Test.net  nameserver = ns1.test.net
	Test.net  nameserver = harris2.diablo1.com
	Test.net
	  Primary name server = ns1.test.net
	  Responsible mail addr = Administrator.test.net
	  Serial = 5
	  Refresh = 3600 (1 hour)
	  Retry    = 600 (10 mins)
	  Expire   = 86400 (1 day)
	  Default TTL = 3600 (1 hour)
	ns1.test.net internet address = 123.123.123.253
	harris2.diablo1.com internet address = 200.200.200.1
	>
	
	*****The above is an example of an "authoritative answer." The name server,
	*****NS1.TEST.NET, returned the SOA (Status of Authority) record for the
	*****domain TEST.NET.
	
	*****This is what to expect from a lame server. HARRIS2.DIABLO1.COM is
	*****listed as TEST.NETs secondary name server and is required to be
	*****authoritative for the TEST.NET domain:
	
	>
	>NSLOOKUP
	Default Server:  ntw.test.net
	Address:  200.200.200.5
	
	>SERVER harris2.diablo1.com
	Default Server:  harris2.diablo1.com
	Address:   200.200.200.1
	
	>SET TYPE=ANY
	>test.net
	Server: harris2.diablo1.com
	Address: 200.200.200.1
	
	Non-authoritative answer:
	test.net     nameserver = ns1.test.net
	test.net     nameserver = harris2.diablo1.com
	
	Authoritative answers can be found from:
	test.net     nameserver = ns1.test.net
	test.net     nameserver = ns2.test.netn
	ns1.test.NET          internet address = 123.123.123.253
	harris2.diablo1.com      internet address = 200.200.200.1
	
	*****The above is returning a non-authoritative answer and is telling us
	*****where to get an authoritative answer from. Note that it is telling us
	*****that an authoritative answer can be obtained from ourselves!
	
	>NSLOOKUP
	Default Server:  wow.diablo1.com
	Address:  200.200.200.199
	
	>SERVER harris2.diablo1.com
	Default Server:  harris2.diablo1.com
	Address:   200.200.200.1
	
	>SET TYPE=ANY
	>test.net
	Server: harris2.diablo1.com
	Address: 200.200.200.1
	
	DNS request timed out.
	        Timeout was 2 seconds.
	DNS request timed out.
	        Timeout was 4 seconds.
	DNS request timed out.
	        Timeout was 8 seconds.
	*** Request to harris2.diablo1.com timed-out
	
	(OR)
	
	*** harris2.diablo1.com can't find test.net.: No response from server
	
	*****The above is considered a lame server as well. This server isn't even
	*****listening for DNS queries or doesn't even exist!
	
	For additional information, please see the following article in the Microsoft
	Knowledge Base:
	
	  Q171789 PTR Record for DNS Server is not Automatically Created
	
	
	Additional query words: soa start of authority ntdns Status of Authority Domain Name System
	======================================================================
	Keywords          : kbnetwork kbusage 
	Technology        : kbWinNTsearch kbWinNT400search kbWinNTSsearch kbWinNTS400search kbWinNTS400
	Version           : WinNT:4.0
	Issue type        : kbinfo
	
	=============================================================================
	

{% endraw %}
