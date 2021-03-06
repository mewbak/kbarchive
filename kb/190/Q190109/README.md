---
layout: page
title: "Q190109: HOWTO: Keep RDO Cursor Open After Transaction"
permalink: /kb/190/Q190109/
---

## Q190109: HOWTO: Keep RDO Cursor Open After Transaction

{% raw %}

	Article: Q190109
	Product(s): Microsoft Visual Basic for Windows
	Version(s): WINDOWS:4.0,5.0,6.0
	Operating System(s): 
	Keyword(s): kbGrpDSVBDB
	Last Modified: 09-JAN-2000
	
	-------------------------------------------------------------------------------
	The information in this article applies to:
	
	- Microsoft Visual Basic Enterprise Edition for Windows, versions 4.0, 5.0, 6.0 
	-------------------------------------------------------------------------------
	
	SUMMARY
	=======
	
	By default, the SQL Server ODBC driver automatically closes cursor after a call
	to commit or rollback. If you reference the RDO resultset afterwards, for
	example, rs.MoveNext, Debug.Print rs(0), the following error occurs:
	
	  Run-time error '40088':
	  No open cursor or cursor closed.
	
	This article demonstrates, in Visual Basic 6.0, how you can keep the cursor open
	by setting a driver-specific statement option, using the SQLSetConnectOption API
	before establishing the connection. This option is documented in the SQL Server
	ODBC Driver Help file, which you can also obtain when installing the SQL Server
	Books Online.
	
	However, this approach does not work in Visual Basic 5.0 using RDO (Msrdo20.dll
	version 5.xx.xxxx) due to a known RDO bug. To reference the resultset after the
	transaction, you must either Requery the resultset or use the Server-side cursor
	driver and the rdExecDirect option of the connection object.
	
	In Visual Basic 4.0, the resultset remains open after transaction.
	
	MORE INFORMATION
	================
	
	Visual Basic 6.0 Step-by-Step Example
	-------------------------------------
	
	1. Start a new project in Visual Basic and choose "Standard EXE." Form1 is
	  created by default.
	
	2. On the Project menu, click References, and then select Microsoft Remote Data
	  Object 2.0.
	
	3. Add a CommandButton to Form1.
	
	4. Paste the following code in the General Declaration section of Form1:
	
	        Option Explicit
	
	        Const SQL_PRESERVE_CURSORS As Long = 1204
	        Const SQL_PC_ON As Long = 1
	
	        Private Declare Function SQLSetConnectOption Lib "odbc32.dll" (ByVal
	           hdbc&, ByVal fOption%, ByVal vParam As Any) As Integer
	        Dim WithEvents cn As rdoConnection
	        Dim rs As rdoResultset
	
	        Private Sub cn_BeforeConnect(ConnectString As String, Prompt As
	          Variant)
	           Dim intRet As Integer
	           intRet = SQLSetConnectOption(cn.hdbc, SQL_PRESERVE_CURSORS,
	            SQL_PC_ON)
	        End Sub
	
	        Private Sub Command1_Click()
	           Dim strConnect As String
	           Set cn = New rdoConnection
	           strConnect = "DRIVER={SQL
	             Server};SERVER=MyServer;DATABASE=pubs;UID=sa;PWD="
	           cn.Connect = strConnect
	           cn.EstablishConnection
	           Set rs = cn.OpenResultset("SELECT * FROM authors", rdOpenKeyset,
	             rdConcurValues)
	
	           cn.BeginTrans
	           rs.Edit
	           rs(1) = "Vermont"
	           rs.Update
	           cn.CommitTrans
	           Debug.Print rs(1)
	        End Sub
	
	Visual Basic 5.0 Step-by-Step Example
	-------------------------------------
	
	1. Start a new project in Visual Basic and choose "Standard EXE." Form1 is
	  created by default.
	
	2. On the Project menu, click References, and then select Microsoft Remote Data
	  Object 2.0.
	
	3. Add a CommandButton to Form1.
	
	4. Paste the following code in the General Declaration section of Form1:
	
	        Option Explicit
	
	        Dim cn As rdoConnection
	        Dim rs As rdoResultset
	
	        Private Sub Command1_Click()
	           Dim strConnect As String
	           Set cn = New rdoConnection
	           strConnect = "Driver={SQL
	             Server};Server=yourserver;Database=Pubs;Uid=sa;Pwd=;"
	           With cn
	             .CursorDriver = rdUseServer
	             .Connect = strConnect
	             .EstablishConnection
	           End With
	           Set rs = cn.OpenResultset("Select * from Authors", rdOpenKeyset, _
	              rdConcurValues)
	
	           cn.Execute "Begin Transaction", rdExecDirect
	           Debug.Print rs(1)
	           rs.Edit
	           rs(1) = "Vermont"
	           rs.Update
	           cn.Execute "Commit Transaction", rdExecDirect
	           Debug.Print rs(1)
	        End Sub
	
	Note that Authors table in SQL Server Pubs database is used here for testing
	purposes. You must change your Server, Uid, and Pwd parameters in the connect
	string.
	
	Additional query words: kbvbp600 kbvbp400 kbvbp500 kbDatabase kbRDO200bug kbRDO
	
	======================================================================
	Keywords          : kbGrpDSVBDB 
	Technology        : kbVBSearch kbAudDeveloper kbZNotKeyword6 kbZNotKeyword2 kbVB500Search kbVB600Search kbVB500 kbVB600 kbVB400Search kbVB400
	Version           : WINDOWS:4.0,5.0,6.0
	Issue type        : kbhowto
	
	=============================================================================
	

{% endraw %}
