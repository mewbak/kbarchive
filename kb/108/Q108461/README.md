---
layout: page
title: "Q108461: FIX: DO Loop/Computed GOTO Errors with /Ox and /4Yb"
permalink: /kb/108/Q108461/
---

## Q108461: FIX: DO Loop/Computed GOTO Errors with /Ox and /4Yb

{% raw %}

	Article: Q108461
	Product(s): Microsoft Fortran Compiler
	Version(s): 1.0
	Operating System(s): 
	Keyword(s): 
	Last Modified: 24-MAR-2000
	
	-------------------------------------------------------------------------------
	The information in this article applies to:
	
	- Microsoft Fortran Powerstation 32 for Windows NT, version 1.0 
	-------------------------------------------------------------------------------
	
	SYMPTOMS
	========
	
	DO loops may not function properly when compiled with both optimization for time
	(/Ox) and extended error handling (/4Yb or $DEBUG). A similar problem exists
	using computed GOTO statements.
	
	RESOLUTION
	==========
	
	Do not compile with /Ox and /4Yb at the same time. Use the Visual Workbench
	debugger to track down run-time errors that occur when using /Ox.
	
	STATUS
	======
	
	Microsoft has confirmed this to be a problem in Microsoft FORTRAN PowerStation
	32 for Windows NT, version 1.0. This problem was fixed in FORTRAN PowerStation,
	version 4.0.
	
	MORE INFORMATION
	================
	
	The following code illustrates the DO loop problem when compiling with /Ox and
	/4Yb:
	
	Sample Code #1
	--------------
	
	  c FORTRAN Compile options needed: /Ox /4Yb
	        ieof = 0
	        DO i = 1, 4
	          IF ( i .EQ. 4 )  ieof = 999
	          i1 = i + 1
	          WRITE (*,1000) i, i1, ieof
	        ENDDO
	  1000  FORMAT (3i6)
	        END
	
	Output
	------
	
	Expected results:
	
	  1     2     0
	  2     3     0
	  3     4     0
	  4     5   999
	
	Results with -Ox -4Yb:
	
	  1     2     0
	  1     2     0
	  2     3     0
	  3     4     0
	
	The sample program below executes in an infinite loop when compiling with /Ox and
	/4Yb:
	
	Sample Code #2
	--------------
	
	  c FORTRAN Compile options needed: /Ox /4Yb
	        J = 0
	      1 CONTINUE
	        WRITE(*,*) 'Label 1'
	        WRITE(*,*) 'J = ', J
	
	        J = J + 1
	        IF (J.EQ.2) THEN
	       K = 1
	        ELSE
	       K = 1
	        ENDIF
	
	        WRITE(*,*) 'J = ', J
	        GOTO(1,2), J        ! Computed GOTO always branches to label 1
	
	      2 CONTINUE
	        WRITE(*,*) 'Label 2'
	        END
	
	Additional query words: 1.00
	
	======================================================================
	Keywords          :  
	Technology        : kbAudDeveloper kbFortranSearch kbZNotKeyword2 kbFORTRANPower32100NT
	Version           : :1.0
	Issue type        : kbbug
	Solution Type     : kbfix
	
	=============================================================================
	

{% endraw %}
