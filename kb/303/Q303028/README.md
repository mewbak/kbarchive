---
layout: page
title: "Q303028: Error Message When You Modify otherMailbox or Mail"
permalink: /kb/303/Q303028/
---

## Q303028: Error Message When You Modify otherMailbox or Mail

{% raw %}

	Article: Q303028
	Product(s): Windows for Workgroups and Windows NT Networking Issues
	Version(s): 2.2 SP1,5.5
	Operating System(s): 
	Keyword(s): kbenv kberrmsg kbtool
	Last Modified: 28-AUG-2001
	
	-------------------------------------------------------------------------------
	The information in this article applies to:
	
	- Microsoft Metadirectory Services 2.2 SP1 
	- Microsoft Exchange Server, version 5.5 
	-------------------------------------------------------------------------------
	
	SYMPTOMS
	========
	
	When you use the Exchange LDAP MA to apply modifications, some transactions may
	generate an "Invalid modification response 20" error message, even though you
	can successfully make the same modifications through the Exchange Administration
	tool. This behavior may occur during an InterOrg synchronization with Microsoft
	Metadirectory Services (MMS).
	
	CAUSE
	=====
	
	This issue can occur after you initially add the custom recipients. On a
	subsequent pass containing modifications, some records will generate this error.
	Examination of the data reveals that the error occurs on those records where
	either the primary SMTP reply or an SMTP proxy address have changed places.
	
	Consider the following custom recipient example, where SMTP denotes the primary
	reply address, and SMTP indicates a proxy address:
	
	  SMTP: John.Doe@company.com
	  smtp: johnd@company.com
	
	If a new primary SMTP address is assigned and the old one is moved into the proxy
	addresses, the error occurs:
	
	  SMTP: JDoe@company.com
	  smtp: John.Doe@company.com
	  smtp: johnd@company.com
	
	An error entry that is similar to the following entry appears in your Zscript.log
	file:
	
	  ******************************************************************
	  Updating the Connected Directory's Foreign Users
	  ******************************************************************
	  Start of the LDAP update process
	  Invalid modification response 20 - ATTRIBUTE OR VALUE EXISTS for object
	  CN=SmallmouthB(Freshwater),CN=Foreign,OU=Harbor,O=Saltwater
	  Update directory completed: 6 objects processed
	  ******************************************************************
	  Successful update of Connected Directory's Foreign Users
	  ******************************************************************
	
	The reason for this error is that the updates to the object are evaluated as a
	whole by LDAP. Either all fields succeed or the record fails. When the values
	are checked for otherMailbox against the existing record, the current primary
	SMTP address will match the value that is destined for otherMailbox and the
	error occurs.
	
	WORKAROUND
	==========
	
	To work around the issue, use one or more of the following methods:
	
	- Make the address change over two synchronization cycles to eliminate any
	  conflict. To do this, change the primary SMTP address during one cycle, and
	  then change the otherMailbox during the next cycle.
	
	- Edit the custom recipient through the Exchange Administrator tool.
	
	- Delete and then recreate the problem custom recipient through MMS. This means
	  that all Custom Recipients (Foreign Users) will be deleted by the Management
	  Agent and then re-added. To delete and then recreate the problem custom
	  recipient through MMS:
	
	  1. Back up your Management Agent templates before you proceed, because the
	     following steps require you to make a parsing template modification that
	     you will want to undo after you have processed the foreign user deletion.
	
	For additional information about recording management agent templates in
	Microsoft Metadirectory, click the article number below to view the article in
	the Microsoft Knowledge Base:
	
	  Q250479 Recording Management Agent Templates in Microsoft Metadirectory
	
	  2. WARNING: You must first delete all of the custom recipients that are
	     created by this Management Agent. Because this could place a high load on
	     your Exchange server if you have thousands of CRs, you must proceed with
	     caution.
	
	  3. Open Design MA\Connected Directory Foreign Entries\Foreign Entries Output
	     Templates\Add, and then change the following entries from this
	
	  A $v_dn
	  (-objectClass: $v_oc)
	  ($v_oc1)
	  ($v_rdn)
	  ($v_containerinfo)
	  (-cn: $v_AccountName)
	  (-Admin-Description: $v_description)
	  (-Admin-Display-Name: $v_AdminDisplayNameRdn)
	  (-co: $v_co)
	  (-Company: $v_company)
	  (-Target-Address: $v_targetaddress)
	  (-mail: $v_mail)
	  (-sn: $v_sn)
	  (-givenName: $v_givenName)
	  (-homePhone: $v_homePhone)
	  (-initials: $v_initials)
	  (-info: $v_comment)
	  (-MAPI-Recipient: $v_MapiRecipient)
	  (-mobile: $v_mobile)
	  (-pager: $v_pager)
	  (-uid: $v_AliasName)
	  (-telephoneNumber: $v_telephoneNumber)
	  (-textEncodedORAddress: $v_textEncodedORAddress)
	  (-facsimileTelephoneNumber: $v_facsimileTelephoneNumber)
	  (-st: $v_st)
	  (-postalCode: $v_postalCode)
	  (-attributeCertificate;base64: $md.attributeCertificate;base64)
	  ($multi_valued("0",$userCertificate;base64,"-userCertificate;base64: "))
	  (-cACertificate;base64: $md.cACertificate;base64)
	  #(-thumbnailLogo;base64: $md.thumbnailLogo;base64)
	  #(-thumbnailPhoto;base64: $md.thumbnailPhoto;base64)
	  #(-jpegPhoto;base64: $md.thumbnailPhoto;base64)
	  ---
	
	     to this:
	
	  D $v_dn
	  ---
	
	     Click OK.
	
	  4. Open Operate MA\Operational Settings\Delta Operations, and then click to
	     clear the Use Metadirectory Deltas to Update Foreign Users check box.
	
	  5. Open Operate MA\Operational Settings\When Running the Management Agent.
	     Set the Tasks to Run to Update Microsoft Exchange, and then set the Types
	     of Object to Process to Process Custom Recipients.
	
	  6. Run the Management Agent to delete all of the custom recipients that were
	     created in Exchange, and note that this could take some time.
	
	  7. After the custom recipients are deleted, you can restore your templates.
	
	For additional information about how to do so, click the article number below to
	view the article in the Microsoft Knowledge Base:
	
	  Q255796 Updating a Management Agent's Templates from Its Working Folder
	
	  8. Run the Management Agent again to re-populate the custom recipients in
	     Exchange. At this point all of your custom recipients are back in Exchange
	     with the correct addresses.
	
	MORE INFORMATION
	================
	
	This behaviour only occurs for values in the otherMailbox attribute within a
	user object. LDAP does not run any uniqueness checks against SMTP addresses in
	the targetAddress or mail attributes of other objects in the directory. This
	occasionally results in duplicate SMTP addresses. For additional information
	about how to resolve this problem, click the article number below to view the
	article in the Microsoft Knowledge Base:
	
	  Q302757 Duplicate SMTP Addresses through the Exchange LDAP MA
	
	Additional query words: kbmmssearch mms metadirectory zoomit
	
	======================================================================
	Keywords          : kbenv kberrmsg kbtool 
	Technology        : kbExchangeSearch kbExchange550 kbZNotKeyword2 kbMMSSearch kbMMS220SP1
	Version           : :2.2 SP1,5.5
	Issue type        : kbprb
	
	=============================================================================
	

{% endraw %}
