---
layout: page
title: "Q303739: Firewall Prevents Access from Receiving Updates to Network Map"
permalink: /kb/303/Q303739/
---

## Q303739: Firewall Prevents Access from Receiving Updates to Network Map

{% raw %}

	Article: Q303739
	Product(s): Microsoft Developer Network
	Version(s): 1.3,1.4,1.99
	Operating System(s): 
	Keyword(s): 
	Last Modified: 27-AUG-2001
	
	-------------------------------------------------------------------------------
	The information in this article applies to:
	
	- Microsoft Passport, versions 1.3, 1.4, 1.99 
	-------------------------------------------------------------------------------
	
	SUMMARY
	=======
	
	If your computer resides behind a firewall, you must take steps to ensure that
	your Network Map (Partner.xml) is updated regularly and successfully. The steps
	that you take depend on which version of the Passport Software Development Kit
	(SDK) you are using.
	
	MORE INFORMATION
	================
	
	If you are using Passport SDK version 1.4.1 or later, first make sure that the
	Passport SDK is installed. For more information about installing the Passport
	SDK, see the following Passport SDK Web site:
	
	  Installing the SDK
	  http://www.passport.com/devinfo/setup_sdk.asp
	
	After the Passport SDK is installed, adjust your registry so that your proxy
	settings are available to the system process that obtains Partner.xml. To do
	this, copy the contents of the following registry key
	
	  HKEY_CURRENT_USER\Software\Microsoft\Windows\CurrentVersion\ Internet
	  Settings
	
	to the following key:
	
	  HKEY_USERS\.DEFAULT\Software\Microsoft\Windows\CurrentVersion\ Internet
	  Settings
	
	If you are using Passport SDK version 1.4 or earlier, you can add a Network Map
	refresh page to your site. To create a Network Map refresh page, use the
	following code:
	
	  <% Dim pmadmin, success
	
	  Set pmadmin = Server.CreateObject("Passport.Admin.1")
	  success = pmadmin.Refresh(true)
	
	  %>
	  <HTML>
	  <HEAD>
	  <TITLE>Client Test Pages<%=strPageHeading%></TITLE>
	  </HEAD>
	  <BODY border=0 topmargin=0 rightmargin=0 leftmargin=0
	  text="<%=strPgeTextCol%>" bgcolor="<%=strPgeBackCol%>">
	
	  <%
	  Response.write("Refresh occurred? ")
	  Response.write(success)
	  %>
	
	  </FORM>
	  </BODY>
	  </HTML>
	
	For more information about Network Map refresh, see the following Passport SDK
	Web site:
	
	  Nexus Information
	  http://www.passport.com/devinfo/Other_Nexus.asp
	
	Additional query words: ccd, configuration, control, document,partner, partner.xml
	
	======================================================================
	Keywords          :  
	Technology        : kbMSNSearch kbPassport140 kbPassport130 kbPassport199 kbPassportSearch
	Version           : :1.3,1.4,1.99
	Issue type        : kbinfo
	
	=============================================================================
	

{% endraw %}
