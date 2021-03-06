---
layout: page
title: "Q286189: HOWTO: Invoke OLE DB Data Link Properties Dialog Box in VB Code"
permalink: /kb/286/Q286189/
---

## Q286189: HOWTO: Invoke OLE DB Data Link Properties Dialog Box in VB Code

{% raw %}

	Article: Q286189
	Product(s): Microsoft Visual Basic for Windows
	Version(s): 2.0,2.01,2.1,2.1 SP1,2.1 SP2,2.5,2.6,5.0,6.0,6.0 SP3,6.0 SP4
	Operating System(s): 
	Keyword(s): kbOLEDB kbVBp kbVBp500 kbVBp600 kbGrpDSVBDB kbDSupport kbADOsearch kbATM kbmdac270 kbad
	Last Modified: 23-AUG-2001
	
	-------------------------------------------------------------------------------
	The information in this article applies to:
	
	- Microsoft Visual Basic Enterprise Edition for Windows, versions 5.0, 6.0, 6.0 SP3, 6.0 SP4 
	- Microsoft Visual Basic Professional Edition for Windows, versions 5.0, 6.0 
	- Microsoft OLE DB, versions 2.0, 2.1, 2.5, 2.6 
	- ActiveX Data Objects (ADO), versions 2.0, 2.01, 2.1, 2.1 SP1, 2.1 SP2, 2.5, 2.6, 2.7 
	-------------------------------------------------------------------------------
	
	SUMMARY
	=======
	
	The OLE DB Data link properties dialog box is commonly used to define or edit
	ActiveX Data Object (ADO) connection string attributes for ADO Data controls,
	Visual Basic 6.0 DataEnvironment connection objects, and Universal Data Link
	(UDL) files. This article documents a code sample that demonstrates how to
	programmatically invoke and use this dialog box in a Visual Basic application to
	construct the connection string for an ADO Connection object at run time by
	using a graphical user interface (GUI) driver interface. This is a useful
	feature to implement in applications and tools that might require users to
	specify an ADO connection string at run time.
	
	MORE INFORMATION
	================
	
	The OLE DB Service Component 1.0 Type Library (oledb32.dll) that is installed by
	Microsoft Data Access Components (MDAC) implements an object named DataLinks
	whose PromptEdit and PromptNew methods can invoke and use the OLE DB Data Link
	properties dialog box to define or edit ADO connection strings.
	
	The following steps set up a Visual Basic sample that demonstrates how to use the
	DataLinks object of the OLE DB Service Component 1.0 Type Library to edit the
	connection string properties of an ADO connection object:
	
	1. Open a new Standard EXE project in Visual Basic. Form1 is created by default.
	
	2. On the Project menu, set references to the Microsoft ActiveX Data Objects 2.x
	  Library and the OLE DB Service Component 1.0 Type Library.
	
	3. Drag-and-drop a CommandButton on Form1 and make the caption Define
	  Connection.
	
	4. Copy and paste the following code into Form1's code module:
	
	  Dim cn As ADODB.Connection
	
	  Private Sub Command1_Click()
	
	  Dim MSDASCObj As MSDASC.DataLinks
	  Set MSDASCObj = New MSDASC.DataLinks
	
	  Set cn = New ADODB.Connection
	  MSDASCObj.PromptEdit cn
	
	  cn.Open
	  MsgBox "Connection opened successfully"
	  cn.Close
	  End Sub
	
	5. Save the project and run it.
	
	6. Click Define Connection, and note that the code in the Click event procedure
	  of the CommandButton creates an instance of the MSDASC.DataLinks object and
	  executes its PromptEdit method to display the OLE DB Data Link Properties
	  dialog box. This dialog box is displayed as a modal window. As a result,
	  subsequent code that follows the call to the PromptEdit method is not
	  executed until the Data link properties dialog box is dismissed.
	
	7. Select a suitable OLEDB provider in the Providers tab, and then specify the
	  other connection attributes to establish a connection to one of your
	  databases (Access, SQL Server, Oracle, and so forth).
	
	8. Click Test Connection in the Data link properties dialog box to test the
	  connection. Note that you receive a Test Connection succeeded message box if
	  the connection is successful. Dismiss the dialog box by clicking OK.
	
	The remaining code in the Click event procedure of the CommandButton is now
	executed. The ConnectionString property of the ADO Connection object that was
	passed as a parameter to the PromptEdit method is initialized based on the
	settings that you selected in the Data link properties dialog box.
	
	The statements that follow the call to the PromptEdit method of the
	MSDASC.DataLinks object open and close an ADO Connection by using the ADO
	Connection object that is initialized by the call to the PromptEdit method. This
	verifies that the ADO Connection object's ConnectionString property was set
	correctly according to the options that are selected in the Data Link properties
	dialog box. If you click Cancel in the Data Link properties dialog box, the
	cn.Open statement in the Visual Basic code generates a run-time error to
	indicate that it could not establish a connection by using the uninitialized
	ConnectionString.
	
	NOTE: You can check the connection's ConnectionString to see if it is empty ("")
	and catch the Cancel before the connection.open statement.
	
	Additional query words: PromptEdit MSDASC Data Link
	
	======================================================================
	Keywords          : kbOLEDB kbVBp kbVBp500 kbVBp600 kbGrpDSVBDB kbDSupport kbADOsearch kbATM kbmdac270 kbado270 
	Technology        : kbVBSearch kbAudDeveloper kbADOsearch kbADO210 kbADO201 kbADO200 kbADO210sp1 kbADO210sp2 kbADO250 kbADO260 kbZNotKeyword6 kbZNotKeyword2 kbVB500Search kbVB600Search kbVB500 kbVB600 kbOLEDBSearch kbOLEDB200 kbOLEDB210 kbOLEDB250 kbOLEDB260 kbVB600SP3 kbVB600SP4 kbADO270
	Version           : :2.0,2.01,2.1,2.1 SP1,2.1 SP2,2.5,2.6,5.0,6.0,6.0 SP3,6.0 SP4
	Issue type        : kbhowto
	
	=============================================================================
	

{% endraw %}
