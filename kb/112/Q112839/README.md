---
layout: page
title: "Q112839: How to Index on Numbers in a Character Field"
permalink: /kb/112/Q112839/
---

## Q112839: How to Index on Numbers in a Character Field

{% raw %}

	Article: Q112839
	Product(s): Microsoft FoxPro
	Version(s): MACINTOSH:2.5b; MS-DOS:2.0,2.5,2.5a,2.5b; WINDOWS:2.5,2.5a,2.5b,3.0
	Operating System(s): 
	Keyword(s): 
	Last Modified: 08-FEB-2000
	
	-------------------------------------------------------------------------------
	The information in this article applies to:
	
	- Microsoft Visual FoxPro for Windows, version 3.0 
	- Microsoft FoxPro for Windows, versions 2.5, 2.5a, 2.5b 
	- Microsoft FoxPro for MS-DOS, versions 2.0, 2.5, 2.5a, 2.5b 
	- Microsoft FoxPro for Macintosh, version 2.5b 
	-------------------------------------------------------------------------------
	
	SYMPTOMS
	========
	
	If a character field is made up of numbers and the database is indexed on this
	field, the numbers are not in the expected order.
	
	NOTE: This article assumes that all numbers must be positive.
	
	CAUSE
	=====
	
	In character fields, each character is evaluated one at a time from left to
	right. Therefore, the order may not match that of a numeric field.
	
	RESOLUTION
	==========
	
	To get the character field in numerical order, you must create an index key
	using the PADL() function. The PADL() function will put a character to the left
	of the character expression in order to make the digits right aligned.
	
	Example
	-------
	
	1. In your database, create a character field called IDNUM that has a width of
	  10 and is composed entirely of numbers.
	
	2. In the Command window, type:
	
	        INDEX ON PADL(ALLTRIM(IDNUM),10,"0") TAG IDSORT
	
	  This command will create a tag call IDSORT that will shift all the characters
	  to the right as far as the length of the field.
	
	3. In the Command window, issue the following command in order to index the
	  database on the IDSORT tag:
	
	        SET ORDER TO TAG IDSORT
	
	The order of IDNUM will now emulate that of a numeric field.
	
	MORE INFORMATION
	================
	
	To illustrate the behavior described in the "Symptoms" section above, suppose
	you have a character field called IDNUM that has a width of 10 and is made up of
	all numbers. The following table shows how the numbers will be ordered.
	
	  IDNUM order      IDNUM order when table
	  on input         is indexed on IDNUM
	  ---------------------------------------
	       2                    1
	       30                   10
	       1                    12
	       10                   122
	       12                   2
	       200                  200
	       122                  30
	
	The numbers that begin with "1" will come first, then the numbers that begin with
	"2", and so on because the index expression is evaluated based on one character
	at a time rather than on the whole numeric expression.
	
	Additional query words: VFoxWin FoxMac FoxDos FoxWin 1.02
	
	======================================================================
	Keywords          :  
	Technology        : kbHWMAC kbOSMAC kbVFPsearch kbAudDeveloper kbFoxproSearch kbZNotKeyword3 kbFoxPro250bMac kbFoxPro200DOS kbFoxPro250DOS kbFoxPro250aDOS kbFoxPro250bDOS kbFoxPro250 kbFoxPro250a kbFoxPro250b kbVFP300
	Version           : MACINTOSH:2.5b; MS-DOS:2.0,2.5,2.5a,2.5b; WINDOWS:2.5,2.5a,2.5b,3.0
	
	=============================================================================
	

{% endraw %}
