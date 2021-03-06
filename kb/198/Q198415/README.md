---
layout: page
title: "Q198415: XFOR: Disable 8-BIT MIME Support on NT Option Pack SMTP Service"
permalink: /kb/198/Q198415/
---

## Q198415: XFOR: Disable 8-BIT MIME Support on NT Option Pack SMTP Service

{% raw %}

	Article: Q198415
	Product(s): Microsoft Exchange
	Version(s): winnt:4.0,5.0,5.5
	Operating System(s): 
	Keyword(s): exc4 exc5 exc55
	Last Modified: 06-AUG-2002
	
	-------------------------------------------------------------------------------
	The information in this article applies to:
	
	- Microsoft Exchange Server, versions 4.0, 5.0, 5.5 
	-------------------------------------------------------------------------------
	
	SUMMARY
	=======
	
	Exchange Server administrators may notice the following error message:
	
	  500 Host does not support 8bitmime
	
	This may be a result of a mail host attempting to send 8-bit MIME messages to the
	Exchange Server computer. The Microsoft Windows NT Option Pack comes with an
	SMTP service that can be used as a relay host between the Internet and Exchange
	Server. By default, this SMTP service advertises and allows 8- bit MIME messages
	to be relayed. This article describes how to prevent outside mail hosts from
	sending in 8-bit MIME messages by disabling the advertisement of 8BITMIME.
	
	MORE INFORMATION
	================
	
	To make the Windows NT 4.0 SMTP service stop advertising 8BITMIME, you need to
	alter the metabase key that tells it to advertise 8BITMIME. Use the Mdutil.exe
	utility that is included on the Windows NT Option Pack CD.
	
	NOTE: The Mdutil.exe utility is not installed with the Option Pack by default.
	
	To turn the 8BITMIME advertising off, set the advertisement of 8BITMIME to 0 by
	typing the following command at a command prompt:
	
	  mdutil.exe set -path:smtpsvc -prop:36865 -utype:UT_SERVER -dtype:DWORD -
	  attrib:INHERIT -value:0
	
	NOTE: The above command is shown on two lines for convenience, but it should be
	typed as one continuous command. You may need to stop and restart the SMTPSVC
	for this option to take effect. To verify that disabling or enabling 8BITMIME
	has taken effect, do the following:
	
	1. From a command prompt, type the following command:
	
	  telnet localhost 25
	
	  After it connects, you should see a banner response with "ESMTP spoken here."
	
	2. On the Terminal menu, click Preferences, verify that the Local Echo check box
	  is selected, and then click OK.
	
	3. In the Telnet window type the following command:
	
	  EHLO <yourdomain.com>
	
	  Where <yourdomain.com> is your e-mail domain, and then press the ENTER
	  key. You should then receive a response of 250- and various options. If you
	  disabled the 8BITMIME, it should no longer be listed.
	
	4. Type "quit" (without the quotation marks) in the Telnet window to close the
	  session, and then close the Telnet window.
	
	The response should be:
	
	  36865                         : [IS]    (DWORD)  0x0={0}
	
	The number at the beginning of the returned line, 36865, is the property ID
	number for 8BITMIME. The hexadecimal value (0x0)={0} means that 8BITMIME
	advertising is turned off.
	
	To turn MIME broadcasting back on, execute the above command after replacing
	"-value:0" (without the quotation marks) with "-value:1" (without the quotation
	marks). This sets the parameter value to 1, which turns MIME broadcasting on.
	
	Additional query words: 8bit 7bit eight bit
	
	======================================================================
	Keywords          : exc4 exc5 exc55 
	Technology        : kbExchangeSearch kbExchange500 kbExchange550 kbExchange400 kbZNotKeyword2
	Version           : winnt:4.0,5.0,5.5
	Issue type        : kbhowto
	
	=============================================================================
	

{% endraw %}
