---
layout: page
title: "Q171668: FIX: Shared Table in DBC Remains Locked After Table Update"
permalink: /kb/171/Q171668/
---

## Q171668: FIX: Shared Table in DBC Remains Locked After Table Update

{% raw %}

	Article: Q171668
	Product(s): Microsoft FoxPro
	Version(s): WINDOWS:5.0,5.0a
	Operating System(s): 
	Keyword(s): kbvfp kbvfp600fix
	Last Modified: 24-MAR-2000
	
	-------------------------------------------------------------------------------
	The information in this article applies to:
	
	- Microsoft Visual FoxPro for Windows, versions 5.0, 5.0a 
	-------------------------------------------------------------------------------
	
	SYMPTOMS
	========
	
	When using optimistic table buffering on a table inside a database container
	(DBC), a shared table remains locked after a table update that occurs within a
	transaction. This situation prevents other users from updating the table. The
	behavior occurs when the table is in a DBC, the table update is within a
	transaction and the buffer mode is optimistic table. The behavior does not
	happen when the table is free.
	
	RESOLUTION
	==========
	
	One resolution is to use free tables instead of tables within a database.
	
	Another option is to check, within the transaction, whether the table is locked
	(ISFLOCKED() returns True) and if the table is locked, use the UNLOCK command to
	unlock the table.
	
	A third resolution to perform a REPLACE on more than one record is to put the
	REPLACE statement within a loop so that the scope of the REPLACE statement
	affects only a single record.
	
	STATUS
	======
	
	Microsoft has confirmed this to be a bug in the Microsoft products listed at the
	beginning of this article. This has been corrected in Visual FoxPro 6.0.
	
	MORE INFORMATION
	================
	
	NOTE: This problem occurs only when the scope of records affected by the REPLACE
	function is more than one.
	
	Steps to Reproduce Behavior
	---------------------------
	
	The following code will demonstrate the behavior:
	
	     * Start of the Code
	       CLEAR
	       CLOSE DATABASES ALL
	       SET MULTILOCKS ON
	       SET SAFETY OFF
	       SET TALK OFF
	
	     * Create the database and table
	
	     *********************************************************************
	     * NOTE: If the table is not in a database the problem does not occur.
	     *       The following line can be removed to verify this behavior.
	     *********************************************************************
	       CREATE DATABASE test
	
	       CREATE TABLE test (CTest C(10) , NTest I)
	
	       INSERT INTO Test VALUES ( "one", 1)
	       INSERT INTO Test VALUES ( "two", 2)
	       INSERT INTO Test VALUES ( "three", 3)
	       INSERT INTO Test VALUES ( "four", 4)
	
	       CLOSE DATABASES ALL
	
	       USE Test SHARED
	       =CURSORSETPROP( "buffering", 5) && Optimistic Table Buffering
	
	       REPLACE NEXT 2 cTest WITH "test"
	
	       BEGIN TRAN
	          IF NOT TABLEUPDATE( 2, .F., "Test")
	             ? "Failed."
	          ELSE
	             ? "Committed."
	          ENDIF
	       END TRAN
	
	       IF ISFLOCKED( "Test")
	        * UNLOCK in test && Uncomment this line to test the UNLOCK command
	          ? "The table is still locked."
	       ELSE
	          ? "The table is not locked."
	       ENDIF
	       ?ISFLOCKED()
	     * End of the Code
	
	Additional query words:
	
	======================================================================
	Keywords          : kbvfp kbvfp600fix 
	Technology        : kbVFPsearch kbAudDeveloper kbVFP500 kbVFP500a
	Version           : WINDOWS:5.0,5.0a
	Issue type        : kbbug kbprb
	Solution Type     : kbfix
	
	=============================================================================
	

{% endraw %}
