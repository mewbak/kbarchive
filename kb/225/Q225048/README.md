---
layout: page
title: "Q225048: INFO: Issues Migrating from DAO/Jet to ADO/Jet"
permalink: /kb/225/Q225048/
---

## Q225048: INFO: Issues Migrating from DAO/Jet to ADO/Jet

{% raw %}

	Article: Q225048
	Product(s): Microsoft Visual Basic for Windows
	Version(s): 2.0,2.01,2.1,2.5,2.6,5.0,6.0
	Operating System(s): 
	Keyword(s): kbADO kbDAOsearch kbDatabase kbIISAM kbJET kbOLEDB kbVBp kbVBp500 kbVBp600 kbvfp kbGrpD
	Last Modified: 11-JAN-2001
	
	-------------------------------------------------------------------------------
	The information in this article applies to:
	
	- Microsoft Visual Basic Professional Edition for Windows, versions 5.0, 6.0 
	- Microsoft Visual Basic Enterprise Edition for Windows, versions 5.0, 6.0 
	- ActiveX Data Objects (ADO), versions 2.0, 2.01, 2.1, 2.5, 2.6 
	-------------------------------------------------------------------------------
	
	SUMMARY
	=======
	
	When migrating an application from using DAO and the Jet database engine to
	using ADO and the Jet database engine, there are a number of issues that need to
	be taken into account before determining the feasibility of such a transition.
	
	MORE INFORMATION
	================
	
	DAO and ADO were designed to solve two different problems. As such, they expose
	two different object models and different methods of manipulating the underlying
	data engines. These differences could mean that you have to make some extensive
	changes when migrating your application from DAO to ADO.
	
	The DAO object model is designed specifically for the Microsoft Jet database
	engine. Jet itself incorporates ISAM and ODBC connectivity and makes the
	back-end providers look as much like the native Jet engine as possible, though
	this comes at the expense of performance. DAO also has an ODBCDirect mode that
	allows it to host RDO objects and access ODBC datasources in a very efficient
	manner.
	
	The ADO object model was designed for OLE DB providers and is a much simpler and
	more flexible object model than DAO. However, its architectural design poses
	some problems when using the Microsoft Jet OLE DB provider, and it is more
	limited than DAO in Jet functionality it supports.
	
	This article outlines several issues you need to consider when making the
	decision whether to migrate your applications from DAO to ADO.
	
	Provider: OLE DB Provider for Jet 3.51 vs 4.0
	---------------------------------------------
	
	The first decision is which OLE DB provider to use. The OLE DB provider for Jet
	3.51 uses the same version of Jet as Access 97 and Visual Basic 5.0 and 6.0, but
	it has limited functionality. The OLE DB provider for Jet 4.0 has more
	functionality, but its native database format is incompatible with Access 97,
	though it can read and write to older database formats through an ISAM driver.
	
	Cursors: Client-Side vs Server-Side
	-----------------------------------
	
	The next decision you have to make in ADO, as in ODBC and RDO, is whether to use
	client-side cursors or server-side cursors.
	
	If you choose client-side cursors, the Client Cursor engine requests the records
	from Microsoft Jet and buffers them in a temporary file on your local machine.
	This will allow your application to have standard ADO functionality, such as
	disconnected and/or saved recordsets and batch updates. However, you will not be
	able to see new records added to any table using an Autonumber column as the
	Primary key unless you Requery the records. You will also not be able to see
	changes other users make until you requery the recordset.
	
	For more information about this topic, please see the following article in the
	Microsoft Knowledge Base:
	
	  Q190370 PRB: AutoNumber Field Is Not Incremented When Using ADO
	
	The OLE DB Provider for Microsoft Jet 3.51 does not return enough schema
	information for some recordsets to be updated when using client-side cursors.
	
	For more information about this topic, please see the following article in the
	Microsoft Knowledge Base:
	
	  Q190108 PRB: Error Updating adUseClient Cursor Based on MDB Query
	
	When using server-side cursors that are provided by the Microsoft Jet OLE DB
	provider and Rowset Helper, functionality will be more limited. However,
	performance of certain operations, such as scrolling through records in a
	recordset, will be faster, and you will be able to see records added to tables
	that contain Autonumber fields without having to requery the recordset.
	
	Multiple Providers
	------------------
	
	As stated at the beginning of the article, DAO and Jet try to make all providers
	appear the same to the programmer. The drawback is performance. The benefit is
	fewer special case decisions in code. ADO, however, exposes the native
	functionality of each provider. This can mean more efficient programs if they
	are coded against a single provider, but if writing code to access multiple
	providers, then you will have to use client-side cursors to minimize differences
	between them, or you will have to devote more of your application to special
	case scenarios where two or more providers expose different functionality.
	
	Limited Functionality of ADO and the OLE DB Provider for Jet
	------------------------------------------------------------
	
	The OLE DB Provider for Jet 3.51 is a limited provider. It was intended to
	provide a thread-safe method of using Microsoft Jet with Microsoft's Internet
	Information Server.
	
	For more information about this topic, please see the following article in the
	Microsoft Knowledge Base:
	
	  Q222135 INFO: Using Microsoft Jet with IIS
	
	It does not expose the full capabilities of the Microsoft Jet database engine. It
	provides the ability to open recordsets against tables, non-parameterized
	queries, and parameterized or non-parameterized SELECT statements. It also
	allows the execution of SQL commands, but not stored Microsoft Jet action
	queries. It does not allow access to ISAM data sources.
	
	The OLE DB Provider for Jet 4.0 exposes most of the Microsoft Jet functionality,
	but not all of it. In addition to the ADO type library, you must include
	references in your project to the ADOX and Jet and Replication Objects type
	libraries to take advantage of functionality outside the core ADO objects. This
	mainly falls into the category of manipulating Access-specific objects and some
	of the other issues noted below.
	
	Limited Functionality of DAO
	----------------------------
	
	- DAO 3.51 cannot use the Microsoft Jet 4.0 database engine, but it does have
	  full control over the Microsoft Jet 3.51 database engine.
	
	- DAO 3.6 provides DAO 3.51 level of control over Microsoft Jet 4.0, but does
	  not expose any new functionality available in Microsoft Jet 4.0.
	
	Performance
	-----------
	
	DAO makes much more efficient use to the Microsoft Jet database engine than ADO
	and many operations are faster under DAO, sometimes up to 5 or 10 times faster,
	such as use of Batch updates. Another issue is that the calls made to retrieve
	schema information are inefficient when applied against Jet. This results in
	queries and updates against tables with a large number of columns being 30
	percent to 80 percent slower than the equivalent query using DAO. One example of
	inefficient usage of Jet by ADO is illustrated in the next section on Connection
	Issues.
	
	
	Connection Issues
	-----------------
	
	Microsoft Jet can host multiple independent sessions within the same process.
	Each session has overhead and a separate read cache. A session in DAO is
	represented by the DBEngine object. By default, all DAO objects you create and
	all DAO Data controls in Visual Basic use the same Jet session.
	
	In OLE DB, a Jet session is represented by the Data Source object. Multiple
	connections can be opened against a single Data Source object.
	
	In ADO, the OLE DB object model is somewhat simplified: An ADO Connection object
	consists of an OLE DB Data Source object and an OLE DB Connection object. This
	means that in ADO, every Connection object and ADO Data control use a separate
	Jet session.
	
	This has important ramifications when migrating your application from DAO to ADO.
	First, Microsoft Jet can only handle a limited number of sessions. If your
	application uses a large number of ADO Data controls, Jet may run out of
	resources. In addition, Jet's read buffer has a five-second time-out, so changes
	made on one connection will not be visible on another for five seconds. In DAO,
	this was not an issue, because all objects were using the same buffer. The
	following Knowledge Base article provides more information on this topic, and
	how to share connections between data controls to eliminate the problems caused
	by multiple Jet sessions:
	
	  Q216925 PRB: Single-User Concurrency Problems With ADO and Jet
	
	A second method of improving concurrency is to use the RefreshCache method of
	JetEngine object. This object is exposed via the Microsoft Jet and Replication
	Objects 2.1 Library, available starting with ADO 2.1 Sp1 GA. ADO is downloadable
	from:
	
	http://www.microsoft.com/data
	
	Redistribution
	--------------
	
	When using DAO, you have a much smaller number of files that you must install on
	the client machine. The Visual Basic Setup Wizard (Visual Basic 5.0 and earlier)
	or the Package and Deployment Wizard (Visual Basic 6.0) handles this for you.
	With ADO, you have to redistribute all of ADO and OLE DB, including ODBC, and
	some default drivers other than Microsoft Jet.
	
	Wild Card Characters
	--------------------
	
	The query wild-card characters are different in DAO than in ADO. DAO exposes the
	following characters for use with the SQL LIKE operator:
	
	+---------------------------------------------------+
	| Character | Function                              | 
	+---------------------------------------------------+
	| *         | Match any string                      | 
	+---------------------------------------------------+
	| ?         | Match any character                   | 
	+---------------------------------------------------+
	| #         | Match any digit                       | 
	+---------------------------------------------------+
	| [a-cf]    | Match any of 'a' through 'c' or 'f'   | 
	+---------------------------------------------------+
	| [~a-c]    | Match anything but of 'a' through 'c' | 
	+---------------------------------------------------+
	
	ADO exposes the following ANSI wildcard characters:
	
	+---------------------------------+
	| Character | Function            | 
	+---------------------------------+
	| %         | Match any string    | 
	+---------------------------------+
	| _         | Match any character | 
	+---------------------------------+
	
	Wildcards and Stored Queries
	----------------------------
	
	If you have a stored QueryDef in an MDB file, created through Access or DAO, that
	uses wildcard characters, it will not return any records if run under ADO. The
	OLEDB provider for Jet recompiles the SQL and tells the query engine to use the
	ANSI wildcard characters (see table above).
	
	If you create a QueryDef in a Jet 4.0 database using the ADO CREATE PROCEDURE or
	CREATE VIEW statements and ANSI wildcards, the queries will not run correctly
	under DAO 3.6. More information on ANSI query issues is in the "Access 2000 and
	Legacy Application Compatibility" section later in this article.
	
	Find vs FindFirst
	-----------------
	
	In ADO, the Find method has a couple of limitations:
	
	- Neither the 3.51 nor 4.0 versions of the OLE DB provider for Microsoft Jet
	  implement the Find method natively, so the Rowset Helper is used. The Rowset
	  Helper implements the Find method by stepping through the records
	  sequentially. To avoid this performance penalty, you should use a SELECT
	  statement with a WHERE condition to return just the record(s) you need and,
	  if this is not feasible, then use client-side cursors and the Filter method.
	- Unlike FindFirst or the ADO Filter method, which allow complex search
	  criteria, the Find method allows only a single comparison with limited
	  syntax:
	
	  fieldname operator literal
	
	OLE Container Control
	---------------------
	
	Many databases, including the SQL Server 7 Northwind database, contain pictures
	and other objects saved by Microsoft Access. In Visual Basic, you can see the
	pictures by binding the OLE Container control to the DAO Data control. However,
	the OLE Container control is not compatible with the ADO Data control and there
	is no way to access these pictures and display them using ADO. The OLE Container
	control cannot be used unbound because GetChunk does not retrieve the data in a
	format compatible with the ReadFromFile method.
	
	Security
	--------
	
	When using ADOX to create users in a secure Jet environment, you cannot specify
	the PID. This means that if the SYSTEM.MDW file is deleted you will not be able
	to recreate the accounts from scratch, but must rely on a backup SYSTEM.MDW
	file.
	
	Access 2000 and Legacy Application Compatibility
	------------------------------------------------
	
	There are three main compatibility issues:
	
	- The first is that using the Jet 4.0 database format means that legacy
	  applications, such as Access 95 and Access 97, and Visual Basic 4.0, 5.0, and
	  6.0 applications that use the DAO Data control, are all hard-coded to use the
	  Jet 3.x database format will not be able read Jet 4.0 data.
	
	- The second issue is that stored queries created by ADO are not visible to
	  Access 2000. The reason for this is a change in the Jet 4.0 query processor
	  to make it more ANSI compliant, including adding new SQL commands. Access
	  2000 does not even display these queries in order to avoid confusing users.
	  However, they can be seen and executed via DAO and ADO. They can also be
	  referenced in Form and Report RecordSource properties and in SQL statements;
	  you will have to type the name in manually as the builder will not display
	  the name. The Microsoft OLE DB provider for Jet 4.0 always sets the ANSI flag
	  to a non-NULL value. DAO always sets this flag to NULL.
	
	- The third issue is that Jet 4.0 drops support for the FoxPro IISAM. Any
	  FoxPro tables must be accessed through the FoxPro ODBC driver. If your Jet
	  database uses linked FoxPro tables, and you convert to Jet 4.0, you will have
	  to re-link them to use the FoxPro ODBC driver instead.
	
	(c) Microsoft Corporation 1999, All Rights Reserved.
	Contributions by Malcolm Stewart, Microsoft Corporation
	
	
	Additional query words:
	
	======================================================================
	Keywords          : kbADO kbDAOsearch kbDatabase kbIISAM kbJET kbOLEDB kbVBp kbVBp500 kbVBp600 kbvfp kbGrpDSVBDB kbMDAC250 kbADO250 kbMDAC260 kbADO260 
	Component         : dao JET
	Technology        : kbVBSearch kbAudDeveloper kbADOsearch kbADO210 kbADO201 kbADO200 kbADO250 kbADO260 kbZNotKeyword6 kbZNotKeyword2 kbVB500Search kbVB600Search kbVBA500 kbVBA600 kbVB500 kbVB600
	Version           : :2.0,2.01,2.1,2.5,2.6,5.0,6.0
	Issue type        : kbinfo
	
	=============================================================================
	

{% endraw %}
