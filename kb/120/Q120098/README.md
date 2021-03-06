---
layout: page
title: "Q120098: INFO: Two Ways to Search &amp; Remove Characters from a Text String"
permalink: /kb/120/Q120098/
---

## Q120098: INFO: Two Ways to Search &amp; Remove Characters from a Text String

{% raw %}

	Article: Q120098
	Product(s): Microsoft FoxPro
	Version(s): MACINTOSH:2.5b,2.5c,2.6a; MS-DOS:2.5,2.5a,2.5b,2.6,2.6a; UNIX:2.6; WINDOWS:2.5,2.5a,2.5
	Operating System(s): 
	Keyword(s): kbcode
	Last Modified: 30-DEC-1999
	
	-------------------------------------------------------------------------------
	The information in this article applies to:
	
	- Microsoft Visual FoxPro for Windows, versions 3.0, 5.0, 6.0 
	- Microsoft FoxPro for Windows, versions 2.5, 2.5a, 2.5b, 2.6, 2.6a 
	- Microsoft FoxPro for MS-DOS, versions 2.5, 2.5a, 2.5b, 2.6, 2.6a 
	- Microsoft FoxPro for Macintosh, versions 2.5b, 2.5c, 2.6a 
	- Microsoft FoxPro for UNIX, version 2.6 
	-------------------------------------------------------------------------------
	
	SUMMARY
	=======
	
	You can delete characters from a text string in a memory variable or database
	field. You can use the FoxPro SUBSTR(), ATC(), and STRTRAN() functions to search
	a text string for a particular value and replace it with another.
	
	MORE INFORMATION
	================
	
	Method One: Use SUBSTR() and ATC() Functions
	--------------------------------------------
	
	You can use the ATC() and SUBSTR() functions to eliminate unwanted characters
	from database fields and memory variables.
	
	For example, look at the following code:
	
	  a="123.45"
	  y=SUBSTR(a,1,ATC(".",a)-1)+SUBSTR(a,ATC(".",a)+1)
	  b="123 45"
	  y=SUBSTR(b,1,ATC(" ",b)-1)+SUBSTR(b,ATC(" ",b)+1)
	
	The variables a and b contain the text strings "123.45" and "123 45"
	respectively. The code removes the period (.) and the blank space from the
	variables.
	
	The SUBSTR() function parses the variable into separate pieces based on the value
	returned by the ATC() function. The ATC() function searches for a string in a
	variable or field and returns the numeric position of the first character in the
	string if it is found. If the ATC() function can't locate the string, it returns
	zero (0).
	
	By combining the SUBSTR() and ATC() functions, you can construct complex
	statements to alter data in numerous ways.
	
	Method Two: Use STRTRAN() Function
	----------------------------------
	
	You can use the STRTRAN() function to search and replace characters within a text
	string using a single command. The following example code shows you how to use
	STRTRAN() to remove an unwanted period (.) from a text string:
	
	  x="123.4567"
	  y=strtran(x,".","")
	  ? y  && The variable y now contains "1234567" as a text string.
	
	By default, STRTRAN() looks for all occurrences of the second parameter listed in
	the function. By adding a numeric value in the third parameter, you can force
	the function to ignore earlier instances of a character. By adding a fourth
	numeric parameter, you can control the number of occurrences the function
	replaces.
	
	The following example code shows you how to remove the second period from a text
	string while preserving the first occurrence:
	
	  x="123.4567.8910"
	  y=strtran(x,".","",2)
	  ? y
	
	The variable y returns "123.45678910" as a text string.
	
	REFERENCES
	==========
	
	Microsoft FoxPro Commands & Functions 1.02 pp. C4-17; C4-191; C4-189
	Microsoft FoxPro Commands & Functions 2.00 pp. C3-156; C3-870; C3-866
	Microsoft FoxPro Language Reference 2.5x and 2.60 pp. L3-218; L3-1059; L3-1055
	
	Additional query words: VFoxWin FoxUnix FoxMac FoxDos FoxWin
	
	======================================================================
	Keywords          : kbcode 
	Technology        : kbHWMAC kbOSMAC kbVFPsearch kbAudDeveloper kbFoxproSearch kbZNotKeyword3 kbFoxPro250bMac kbFoxPro260aMac kbFoxPro250cMac kbFoxPro250DOS kbFoxPro250aDOS kbFoxPro250bDOS kbFoxPro260DOS kbFoxPro260aDOS kbFoxPro260UNIX kbFoxPro260 kbFoxPro250 kbFoxPro250a kbFoxPro250b kbFoxPro260a kbVFP300 kbVFP500 kbVFP600
	Version           : MACINTOSH:2.5b,2.5c,2.6a; MS-DOS:2.5,2.5a,2.5b,2.6,2.6a; UNIX:2.6; WINDOWS:2.5,2.5a,2.5b,2.6,2.6a,3.0,5.0,6.0
	Issue type        : kbinfo
	
	=============================================================================
	

{% endraw %}
