---
layout: page
title: "Q296093: FILE: PrepWebLog Utility Prepares IIS Logs for SQL Bulk Insert"
permalink: /kb/296/Q296093/
---

## Q296093: FILE: PrepWebLog Utility Prepares IIS Logs for SQL Bulk Insert

{% raw %}

	Article: Q296093
	Product(s): Internet Information Server
	Version(s): 3.0,4.0,5.0
	Operating System(s): 
	Keyword(s): kbfile kbGrpDSSIE tslic_tslic
	Last Modified: 27-FEB-2002
	
	-------------------------------------------------------------------------------
	The information in this article applies to:
	
	- Microsoft Internet Information Server versions 3.0, 4.0 
	- Microsoft Internet Information Services version 5.0 
	-------------------------------------------------------------------------------
	
	SUMMARY
	=======
	
	Microsoft Knowledge Base article
	
	  Q296085 HOWTO: Analyzing Web Logs with SQL
	
	describes a utility that you can use to strip the header lines from an Internet
	Information Server/Services (IIS) log for bulk insert to Microsoft SQL Server.
	This article provides that utility as well as the source code.
	
	The Prewebplog.exe utility takes the path and file name of an IIS log file,
	removes the lines that start with "#" (these are the header lines in Web logs)
	and outputs the file to STDOUT.
	
	MORE INFORMATION
	================
	
	The following file is available for download from the Microsoft Download
	Center:
	
	  PrepWebLog.exe
	  (http://download.microsoft.com/download/iis50/utility4/1.0/WIN98MeXP/EN-US/PrepWebLog.exe)
	
	Release Date: JUN-21-2001
	
	For additional information about how to download Microsoft Support files, click
	the article number below to view the article in the Microsoft Knowledge Base:
	
	  Q119591 How to Obtain Microsoft Support Files from Online Services
	
	Microsoft used the most current virus detection software available on the date of
	posting to scan this file for viruses. Once posted, the file is housed on secure
	servers that prevent any unauthorized changes to the file.
	
	The PrepWebLog.exe file contains the following files:
	
	+----------------------------+
	| File name   | Size (bytes) | 
	+----------------------------+
	| Preplog.opt | 48,640       | 
	+----------------------------+
	| Preplog.cpp | 1,274        | 
	+----------------------------+
	| Preplog.plg | 16,779       | 
	+----------------------------+
	| Preplog.exe | 45,056       | 
	+----------------------------+
	| Preplog.obj | 1,883        | 
	+----------------------------+
	| Vc60.idb    | 41,984       | 
	+----------------------------+
	| Preplog.pch | 3,655,472    | 
	+----------------------------+
	| Preplog.dsp | 3,413        | 
	+----------------------------+
	| Preplog.dsw | 537          | 
	+----------------------------+
	| Readme.txt  | 203          | 
	+----------------------------+
	To run the utility, use the following command:
	
	  "D:\>preplog.exe [name of web log]" (without the quotation marks)
	
	The output will go automatically go to STDOUT. Add a file name to direct to a
	specific output file:
	
	  " D:\>preplog.exe [name of web log] > [name of output file]" (without
	  the quotation marks)
	
	  For example, to send the output to a file called "C:\Out.log":
	
	  "D:\>preplog.exe c:\blah.log > out.log" (without the quotation marks)
	
	Additional query words: PrepWebLog
	
	======================================================================
	Keywords          : kbfile kbGrpDSSIE tslic_tslic 
	Technology        : kbiisSearch kbiis500 kbiis400 kbiis300
	Version           : :3.0,4.0,5.0
	
	=============================================================================
	

{% endraw %}
