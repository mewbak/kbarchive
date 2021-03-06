---
layout: page
title: "Q217192: PRB: ODBCDirect Cursor Not Valid After Transaction Commits"
permalink: /kb/217/Q217192/
---

## Q217192: PRB: ODBCDirect Cursor Not Valid After Transaction Commits

{% raw %}

	Article: Q217192
	Product(s): Microsoft Visual Basic for Windows
	Version(s): 5.0,6.0
	Operating System(s): 
	Keyword(s): kbDAO350 kbVBp500 kbVBp600
	Last Modified: 11-JAN-2001
	
	-------------------------------------------------------------------------------
	The information in this article applies to:
	
	- Microsoft Visual Basic Learning Edition for Windows, versions 5.0, 6.0 
	- Microsoft Visual Basic Professional Edition for Windows, versions 5.0, 6.0 
	- Microsoft Visual Basic Enterprise Edition for Windows, versions 5.0, 6.0 
	-------------------------------------------------------------------------------
	
	SYMPTOMS
	========
	
	When you use ODBCDirect with Visual Basic, you receive the following error on
	accessing a recordset object that was created inside of a transaction that has
	been committed or rolled back:
	
	  3670 Cursor is not valid
	
	CAUSE
	=====
	
	This error occurs because you are using server-side cursors on your connection
	and the cursor is being closed when the transaction is committed or rolled back.
	Whether a server-side cursor is closed on a transaction commit or rollback
	depends on the database driver that you are using. For the SQL Server driver,
	the default is to close the server-side cursor on the commit or rollback of a
	transaction.
	
	RESOLUTION
	==========
	
	When you use ODBCDirect, the only two workarounds are the following:
	
	1. Use client side cursors. (This only works with commit. Rollback will still
	  cause the same error.)
	
	2. Requery the information (rs.requery) after a commit or rollback. NOTE: For
	  this workaround to work, MSDTC must not be running.
	
	
	  With some other data access APIs, such as RDO, you can manually set an option
	  to preserve server-side cursors. You set this option using either the
	  SQLSetConnectOption or the SQLSetConnectAttr ODBC API functions. These
	  options must be set after the connection handle is allocated but before the
	  connection has been made. With ODBCDirect it is not possible to have access
	  to the connection handle before the connection has been established, so it is
	  not possible to set the option.
	
	STATUS
	======
	
	This behavior is by design.
	
	MORE INFORMATION
	================
	
	Steps to Reproduce Behavior
	---------------------------
	
	1. Create a new Visual Basic Standard EXE program. Form1 is created by default.
	
	2. Create a reference to the Microsoft DAO 3.50 or 3.51 Object Library.
	
	3. Place a CommandButton on the default form.
	
	4. Add the following code to the CommandButton Click event.
	
	  NOTE: You will need to modify the query and connection string so that it will
	  use your database:
	
	      On Error GoTo errhandler
	      
	      Dim wrkODBC As dao.Workspace
	      Dim cn As dao.Connection
	      Dim rs As dao.Recordset
	      Dim szConnect As String
	     
	      szConnect = "ODBC;Driver={SQL Server};Server=(local);Database=pubs;uid=sa;pwd="
	      
	      Set wrkODBC = CreateWorkspace("", "admin", "", dbUseODBC)
	      wrkODBC.DefaultCursorDriver = dbUseServerCursor
	      
	      'You can work around this problem by uncommenting this next line.
	      'The client batch cursor will preserve the cursor after the
	      'transaction commits.
	      'wrkODBC.DefaultCursorDriver = dbUseClientBatchCursor
	      Set cn = wrkODBC.OpenConnection("", dbDriverNoPrompt, False, szConnect)
	         
	      wrkODBC.BeginTrans
	          Set rs = cn.OpenRecordset("SELECT * FROM AUTHORS")
	          Debug.Print "Recordset Returned: " & rs(0).Value
	      wrkODBC.CommitTrans
	      
	      ' If using server-side cursors, (dbUseServerCursor) this line
	      '  can be uncommented to requery the data after the transaction.
	      ' NOTE: If MSDTC is running, this workaround will fail.
	      '  With MSDTC running you will need to close and then
	      '  reopen the connection before issuing the requery.
	      'rs.Requery
	      Debug.Print rs(0).Value   '<<Invalid Cursor Error Occurs here
	      
	      rs.Close
	      cn.Close
	      Set rs = Nothing
	      Set cn = Nothing
	
	      Exit Sub
	      
	  errhandler:
	
	      'Iterate through the Errors collection to get detailed error information.
	      '-----------------------------------------------------------------------
	      Dim MyErr As Error
	      For Each MyErr In DBEngine.Errors
	          Debug.Print MyErr.Number & " -- " & MyErr.Description
	      Next MyErr
	
	5. Run the code and note that the error occurs when you try to access the
	  recordset after the transaction has been committed. Uncomment the appropriate
	  lines to see the workaround mentioned above.
	
	REFERENCES
	==========
	
	SQL Server 6.5/7.0 Books Online
	
	For additional information, click the article numbers below to view the articles
	in the Microsoft Knowledge Base:
	
	  Q190109 HOWTO: Keep RDO Cursor Open After Transaction
	
	
	Additional query words:
	
	======================================================================
	Keywords          : kbDAO350 kbVBp500 kbVBp600 
	Technology        : kbVBSearch kbAudDeveloper kbZNotKeyword6 kbZNotKeyword2 kbVB500Search kbVB600Search kbVBA500 kbVBA600 kbVB500 kbVB600
	Version           : :5.0,6.0
	Issue type        : kbprb
	
	=============================================================================
	

{% endraw %}
