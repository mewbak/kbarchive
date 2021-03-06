---
layout: page
title: "Q138752: FIX: C4114 Warning When Using Templates and Const Keyword"
permalink: /kb/138/Q138752/
---

## Q138752: FIX: C4114 Warning When Using Templates and Const Keyword

{% raw %}

	Article: Q138752
	Product(s): Microsoft C Compiler
	Version(s): 2.x4.0,4.1,4.2
	Operating System(s): 
	Keyword(s): kbCompiler kbCPPonly kbVC kbVC500fix
	Last Modified: 30-JUL-2001
	
	-------------------------------------------------------------------------------
	The information in this article applies to:
	
	- Microsoft C/C++ Compiler (CL.EXE), used with:
	   - *EDITOR Please do not choose this product*Microsoft Visual C++ 32-bit Edition* use 241, 265, 225, versions 2.x4.0, 4.1, 4.2 
	-------------------------------------------------------------------------------
	
	SYMPTOMS
	========
	
	Using a class or function template may incorrectly generate a C4114 warning. The
	sample code in this article demonstrates a case where this occurs.
	
	CAUSE
	=====
	
	The compiler incorrectly expands the type of the function parameter to const T
	as it expands a template with type const T when the definition of a function or
	member function template has a parameter that takes a const T.
	
	The Help file gives the following information for C4114:
	
	- Same type qualifier used more than once.
	
	- A type qualifier (const, volatile, signed, or unsigned) was used more than
	  once in the same type declaration or definition. The second occurrence of the
	  qualifier was ignored. This is a warning when Microsoft extensions are
	  enabled (/Ze) and an error when extensions are disabled (/Za).
	
	- The following is an example of this warning:
	
	  
	
	  volatile volatile int i;   // warning
	
	RESOLUTION
	==========
	
	This warning can be safely ignored. To disable all occurrences of this warning,
	use the #pragma warning preprocessor directive. The Help file demonstrates how
	to use this pragma.
	
	STATUS
	======
	
	Microsoft has confirmed this to be a bug in the Microsoft products listed at the
	beginning of this article. This bug was corrected in Visual C++ version 5.0.
	
	MORE INFORMATION
	================
	
	Sample Code to Reproduce Problem
	--------------------------------
	
	     // test.cpp
	     // Compile options needed - none
	     template <class T>
	     struct f
	     {
	       void goo( const T & r){ T t=r;};
	     };
	
	     void main()
	     {
	         f<const int> h;
	
	         // the following line of code causes
	         // goo( const const int ) to be expanded
	         h.goo( 2 );
	     }
	
	Additional query words: kbVC400bug 2.00 2.10 2.20 9.00 9.10 10.00 10.10 10.20
	
	======================================================================
	Keywords          : kbCompiler kbCPPonly kbVC kbVC500fix 
	Technology        : kbVCsearch kbAudDeveloper kbCVCComp
	Version           : :2.x4.0,4.1,4.2
	Issue type        : kbbug
	Solution Type     : kbfix
	
	=============================================================================
	

{% endraw %}
