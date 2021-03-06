---
layout: page
title: "Q104860: FORTRAN PowerStation README.TXT: Installing and Using FL32"
permalink: /kb/104/Q104860/
---

## Q104860: FORTRAN PowerStation README.TXT: Installing and Using FL32

{% raw %}

	Article: Q104860
	Product(s): Microsoft Fortran Compiler
	Version(s): 1.0,1.0a
	Operating System(s): 
	Keyword(s): 
	Last Modified: 02-NOV-1999
	
	-------------------------------------------------------------------------------
	The information in this article applies to:
	
	- Microsoft FORTRAN PowerStation for MS-DOS, versions 1.0, 1.0a 
	-------------------------------------------------------------------------------
	
	SUMMARY
	=======
	
	The following information is from parts 1 and 2 of the Microsoft FORTRAN
	PowerStation README.TXT file located in the \F32\README\ directory.
	
	  Part 1: Installing
	  Part 2: Using the FL32 Compiler
	
	MORE INFORMATION
	================
	
	Part 1: Installing
	------------------
	
	Using SHARE
	-----------
	
	If you are going to use Windows 3.1, you must start the share utility
	prior to starting Windows in order to use the Browser. This is not
	necessary if you will be using Windows for Workgroups (WFW), because
	WFW has its own internal version of SHARE.
	
	Modifications to SYSTEM.INI
	---------------------------
	
	Setup modifies the SYSTEM.INI file in your Windows directory. It adds
	the following information in the [386ENH] section:
	
	  device=c:\f32\bin\dosxnt.386
	  device=c:\f32\bin\mmd.386
	
	Without these device drivers installed, FORTRAN PowerStation will not
	work from within Windows. The original SYSTEM.INI is renamed
	SYSTEM.BK_
	
	Running Setup from MS-DOS or Windows
	------------------------------------
	
	The DOSSETUP program installs all of the files necessary to run
	Microsoft FORTRAN PowerStation under MS-DOS. To use the product,
	however, you need to ensure that your environment variables in your
	AUTOEXEC.BAT file are set to run the product correctly.
	
	DOSSETUP has created a file called F32ENV.BAT. This file sets the
	current environment of your MS-DOS session to the necessary values. If
	you want Microsoft FORTRAN PowerStation to be configured when your
	machine starts, you need to copy the lines from F32ENV.BAT to the end
	of your AUTOEXEC.BAT.
	
	If you want to use the Integrated Debugging Environment, you need to
	run the SETUP.EXE program from the Program Manager in Microsoft
	Windows (version 3.1 or later). Running the Microsoft Windows Setup
	program will not affect your ability to run in the MS-DOS environment;
	it merely installs extra files used in the Microsoft Windows
	environment. Although it is possible to run the browser tools
	(SBRPACK.EXE and BSCMAKE.EXE) from the MS-DOS command line, these
	tools are not installed by DOSSETUP.
	
	Libraries Replaced by Setup
	---------------------------
	
	If you have older versions of the LIBC.LIB, KERNEL32.LIB, FP.LIB, or
	NTDLL.LIB libraries in your installation directory, Setup replaces
	them only if the ones on the distribution disk are newer than the ones
	on your hard disk. The only library that Setup always replaces is
	LIBF.LIB.
	
	Running Setup from Windows for Workgroups (WFW)
	-----------------------------------------------
	
	If you install FORTRAN PowerStation from a PC running Windows for
	Workgroups, you may get a warning message from Windows when you allow
	Setup to restart Windows. If another user is connected to your PC, you
	should make certain that restarting Windows on your PC does not cause
	him or her to lose data before proceeding. Some network connections
	may have to be re-established manually after Windows has restarted.
	
	Using a Video Seven Graphics Card
	---------------------------------
	
	Video Seven provides a utility called V7VGA to enable extended
	resolutions of their card. These extended capabilities are enabled by
	default in MS-DOS, but are disabled by default in a Windows MS-DOS
	session.
	
	To use VESA modes in Windows, you must first run the command line
	"V7VESA /1" using the utility supplied with FORTRAN PowerStation. You
	can put this in your AUTOEXEC.BAT file, or run it in a Windows MS-DOS
	session. In addition to running this program in a Windows MS-DOS
	session, you must give the command line "V7VGA pure:off" inside the
	Windows MS-DOS session. This enables the extended capabilities used by
	VESA. V7VGA.EXE is provided on the utilities disk with the Video 7
	card. V7VESA.COM is also provided. Microsoft provides V7VESA.COM, but
	not V7VGA.EXE.
	
	Problems Using 256-Color VESA Modes
	-----------------------------------
	
	Some video adapters do not execute a FLOODFILL correctly if they are
	running in 256-color VESA modes. Instead of filling polygons
	completely with the specified color, these adapters fill only the
	lower half of the polygon. (You can check how your video adapter
	executes FLOODFILL by running the GRDEMO project in the
	..F32\SAMPLES\DEMO directory.
	
	Possible MS-DOS Extender Conflicts
	----------------------------------
	
	Several Microsoft language products provide 32-bit MS-DOS-extended
	tools that use the Microsoft DOSXNT MS-DOS Extender. The version of
	DOSXNT used by Microsoft FORTRAN PowerStation version 1.0 is not
	compatible with the version used by Microsoft MASM version 6.1.
	
	To ensure that all MS-DOS-extended tools run successfully, it is
	recommended that you install each language product in a separate
	directory and that you leave each version of DOSXNT.EXE in the
	subdirectory that contains the tools it supports. This allows each
	MS-DOS-extended tool to locate the appropriate version of DOSXNT.EXE.
	Make sure that the PATH environment variable specifies the directory
	in which you installed FORTRAN PowerStation version 1.0 before the
	directory that contains MASM 6.1. This ensures that you can run the
	latest versions of tools that are in common to both products.
	
	If you install both FORTRAN PowerStation 1.0 and MASM 6.1 in one
	directory, you will not be able to run MASM.EXE and ML.EXE from the
	command line. However, you will be able to run these tools as commands
	executed by NMAKE.
	
	The DOS extender used by Version 1.0a of FORTRAN PowerStation
	is compatable with MASM Version 6.11, Visual C++ 32-bit Edition
	Version 1.0, and Visual C++ 16-bit Edition Version 1.5.
	
	Part 2: Using the FL32 Compiler
	-------------------------------
	
	Temporary Files Created by FL32
	-------------------------------
	
	The FORTRAN PowerStation compiler creates temporary files during
	compilation. These files are normally stored in a directory identified
	by the TMP environment variable. (If a TMP environment variable has
	not been set, these temporary files are stored in the directory where
	FORTRAN PowerStation was installed.) If the directory identified by
	the TMP environment variable does not exist, or there is not enough
	space to create the temporary files, compilation will fail with the
	message "F1914: cannot open internal files."
	
	To check the location of the TMP environment variable, type SET at the
	MS-DOS prompt. All currently set environment variables are listed. You
	can use the Windows File Manager to locate the directory specified in
	the TMP environment variable.
	
	Using Assumed-size Arrays of Structures
	---------------------------------------
	
	Writing an assumed-size array without specifying element indices
	should produce an error, but does not if the array is an array of
	structures.
	
	    subroutine sub(s)
	    structure /struc/ 
	      real r
	    end structure
	    record /struc/ s(*)
	
	C  The following line is incorrect, but will not produce an error:
	
	     write(*,*) s(i).r
	
	C  Instead, a write statement such as the following should be used:
	
	     write(*,*) (s(i).r, i=1,10)
	
	Loop Counter Limitation
	-----------------------
	
	The largest number of iterations that a loop can perform is
	2,147,483,647. This is because the tripcounter is an Integer*4
	variable; the compiler does not check for overflow as a means of
	increasing execution speed.
	
	Notes on the Random Number Generator
	------------------------------------
	
	The random number generator provided with FORTRAN PowerStation is
	different from the one provided with the 16-bit FORTRAN 5.1. The
	sequence of numbers produced by RANDOM is different from that produced
	by the same seed in the FORTRAN 5.1 random number generator.
	
	The value -1 is an exception to the rule that a given seed always
	produces the same sequence of values from RANDOM. Instead, -1 is
	equivalent to RND$TIMESEED, which produces a different sequence each
	time it is used.
	
	Differences in Substring/Concatenation Operations
	-------------------------------------------------
	
	There is a difference in how FORTRAN 5.1 and FORTRAN PowerStation
	handle substring/concatenation operations. FORTRAN PowerStation
	produces the same results that VAX FORTRAN produces if the VAX
	extensions (-4Yv) are enabled. If the VAX extensions are not enabled,
	these operations are handled in the same way that FORTRAN 5.1 does.
	For example, if you define
	
	         CHARACTER*10    BUFFER1
	         CHARACTER*11    BUFFER2, BUFFER3
	         CHARACTER*1     CHAR1
	         BUFFER1 = '0123456789'
	         BUFFER2 = '0123456789 '
	         BUFFER3 = '0123456789 '
	         CHAR1 = 'X'
	
	The statement
	
	  BUFFER1 = BUFFER1(6:10)//BUFFER1(1:5)
	
	produces "5678901234:with VAX extensions enabled and "5678956789" with
	VAX extensions disabled.
	
	The statement
	
	  BUFFER2 = CHAR1//BUFFER2
	
	produces "X0123456789" with VAX extensions enabled and "XX113355779"
	with VAX extensions disabled.
	
	The Statement
	
	  BUFFER3 = BUFFER3(1:10)//CHAR1
	
	produces "0123456789X" with either switch setting.
	
	The assignment statements for BUFFER1 and BUFFER2 violate the ANSI
	Standard. Section 10.4 of the Standard says that for a Character
	Assignment Statement of the form
	
	  v = e
	
	"none of the character positions being defined in 'v' may be
	referenced in 'e'." The FORTRAN PowerStation "Language Guide" does not
	mention this and no run-time error is generated, even when /4Yb is
	used.
	
	Handling Mismatched Type and Length Warnings
	--------------------------------------------
	
	The FL32 compiler generates a mismatched type warning (F2606) if the
	type of a formal argument is different from the type of the actual
	argument used in the subprogram call. Under most conditions, this
	situation will not prevent a program from executing, but certain
	automatic type conversions, such as between REAL*4 and REAL*8, can
	cause the program to crash. It is good practice to resolve mismatched
	type warnings prior to running a program.
	
	Additional query words: 1.00 1.00a
	
	======================================================================
	Keywords          :  
	Technology        : kbAudDeveloper kbFortranSearch kbZNotKeyword3 kbFORTRANPower100DOS kbFORTRANPower100aDOS
	Version           : :1.0,1.0a
	
	=============================================================================
	

{% endraw %}
