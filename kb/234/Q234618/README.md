---
layout: page
title: "Q234618: BUG: MDAC 2.1 GA - ODBC Jet / ISAM Driver Cannot Open Excel 4.0"
permalink: /kb/234/Q234618/
---

## Q234618: BUG: MDAC 2.1 GA - ODBC Jet / ISAM Driver Cannot Open Excel 4.0

{% raw %}

	Article: Q234618
	Product(s): Open Database Connectivity (ODBC)
	Version(s): WINDOWS:2.5,3.51
	Operating System(s): 
	Keyword(s): kbODBC kbMDAC250
	Last Modified: 21-APR-2000
	
	-------------------------------------------------------------------------------
	The information in this article applies to:
	
	- Microsoft Open Database Connectivity, version 3.51 
	- Microsoft Data Access Components version 2.5 
	-------------------------------------------------------------------------------
	
	SYMPTOMS
	========
	
	When using Jet 3.51 or Jet 4.0 with ODBC, a data source name (DSN) that is set
	to Excel version 4.0 creates the following error when you try to open the DSN:
	
	  [Microsoft][ODBC Excel Driver] The Microsoft Jet database engine could not
	  find the object 'somefile.xls'. Make sure the object exists and that you
	  spell its name and the path name correctly.
	
	CAUSE
	=====
	
	Jet 4.0 is not handling the Excel 4.0 file correctly.
	
	RESOLUTION
	==========
	
	As a workaround set the DSN to use version Excel 5.0 with Excel 4.0 .xls files.
	ODBC and Jet will be able to open and query the .xls files and will not produce
	the error message.
	
	STATUS
	======
	
	Microsoft has confirmed this to be a bug in the Microsoft products listed at the
	beginning of this article.
	
	Additional query words:
	
	======================================================================
	Keywords          : kbODBC kbMDAC250 
	Technology        : kbAudDeveloper kbODBCSearch kbMDACSearch kbMDAC250 kbODBC351
	Version           : WINDOWS:2.5,3.51
	Issue type        : kbbug
	Solution Type     : kbpending
	
	=============================================================================
	

{% endraw %}
