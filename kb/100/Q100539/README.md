---
layout: page
title: "Q100539: FIX: No C4051 Warnings Compiling .CPP or .CXX Files"
permalink: /kb/100/Q100539/
---

## Q100539: FIX: No C4051 Warnings Compiling .CPP or .CXX Files

{% raw %}

	Article: Q100539
	Product(s): Microsoft C Compiler
	Version(s): 7.00 | 1.00 1.50 | 1.00
	Operating System(s): 
	Keyword(s): kbCompiler kbCPPonly kbVCkbbuglist kbfixlist
	Last Modified: 26-JUL-2001
	
	-------------------------------------------------------------------------------
	The information in this article applies to:
	
	- The C/C++ Compiler (CL.EXE), included with:
	   - Microsoft C/C++ for MS-DOS, version 7.0 
	   - Microsoft Visual C++ for Windows, 16-bit edition, versions 1.0, 1.5 
	   - Microsoft Visual C++, 32-bit Editions, version 1.0 
	-------------------------------------------------------------------------------
	
	SYMPTOMS
	========
	
	When Microsoft C/C++ compiles a source code file that has the .CPP or .CXX
	filename extension, the compiler does not generate any C4051 warning messages.
	However, when Microsoft C/C++ compiles a source code file that contains similar
	code but that has the .C filename extension, the compiler correctly generates
	C4051 warning messages as follows:
	
	  C4051: type conversion; possible loss of data
	
	STATUS
	======
	
	Microsoft has confirmed this to be a bug in the Microsoft products listed at the
	beginning of this article. This problem was corrected in Visual C++ 32-bit
	Edition version 2.0.
	
	MORE INFORMATION
	================
	
	According to the online help, the C4051 warning indicates that two data items in
	an expression have different base types. In the process of converting one of the
	items, it was truncated. To avoid this warning, cast the data item to an
	appropriate data type.
	
	The following code example demonstrates this problem.
	
	Sample Code
	-----------
	
	  /*
	   * Compile options needed: /W4
	   */ 
	
	  void main()
	  {
	     int i;
	
	     i = 66.66 * 55.55;
	  }
	
	Additional query words: 1.00 1.50 7.00 8.00 8.00c
	
	======================================================================
	Keywords          : kbCompiler kbCPPonly kbVC kbbuglist kbfixlist
	Technology        : kbVCsearch kbAudDeveloper kbCVCComp
	Version           : 7.00 | 1.00 1.50 | 1.00
	Issue type        : kbbug
	Solution Type     : kbfix
	
	=============================================================================
	

{% endraw %}
