---
layout: page
title: "Q174167: XFOR: Forum Password Security Lost After Collabra Migration"
permalink: /kb/174/Q174167/
---

## Q174167: XFOR: Forum Password Security Lost After Collabra Migration

{% raw %}

	Article: Q174167
	Product(s): Microsoft Exchange
	Version(s): winnt:5.5
	Operating System(s): 
	Keyword(s): kb3rdparty kbusage
	Last Modified: 17-DEC-1999
	
	-------------------------------------------------------------------------------
	The information in this article applies to:
	
	- Microsoft Exchange Server, version 5.5 
	-------------------------------------------------------------------------------
	
	SUMMARY
	=======
	
	
	Collabra Share has the ability to set access passwords on individual forums. When
	these forums are migrated into Microsoft Exchange Server, these access passwords
	are not preserved.
	
	MORE INFORMATION
	================
	
	The Migration Wizard imports Collabra Share forums as public folders into
	Microsoft Exchange Server. Exchange does not set any type of access password on
	a public folder. Exchange sets access permissions. During the migration phase,
	the access permissions will be set for all folders based on the rights of the
	logged-on Windows NT account when migration is performed.
	
	You will be presented with the access permissions that will be used for all the
	public folders that will be created. The Migration Wizard has no method of
	setting access permissions on a single folder basis. However, you can set access
	permissions on individual folders using the Exchange Administrator program after
	migration is complete.
	
	This behavior is by product design.
	
	Additional query words:
	
	======================================================================
	Keywords          : kb3rdparty kbusage 
	Technology        : kbExchangeSearch kbExchange550 kbZNotKeyword2
	Version           : winnt:5.5
	Issue type        : kbinfo
	
	=============================================================================
	

{% endraw %}
