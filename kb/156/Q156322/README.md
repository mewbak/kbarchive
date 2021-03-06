---
layout: page
title: "Q156322: FIX: RETURN TO Procedurename Command Doesn't Work in Forms"
permalink: /kb/156/Q156322/
---

## Q156322: FIX: RETURN TO Procedurename Command Doesn't Work in Forms

{% raw %}

	Article: Q156322
	Product(s): Microsoft FoxPro
	Version(s): 3.0 5.0
	Operating System(s): 
	Keyword(s): kbvfp kbVS97sp2fix
	Last Modified: 21-AUG-1999
	
	-------------------------------------------------------------------------------
	The information in this article applies to:
	
	- Microsoft Visual FoxPro for Windows, versions 3.0, 3.0b, 5.0, 5.0a 
	-------------------------------------------------------------------------------
	
	SUMMARY
	=======
	
	This article pertains to the use of the Error event of a control and the RETURN
	TO command when trying to return to a method or event of a form or class that is
	different from where the Error event was generated. When using the RETURN TO
	command in a form or class, it will only return to the method or event on some
	of FoxPro's error messages.
	
	STATUS
	======
	
	Microsoft has confirmed this to be a bug in the Microsoft products listed at the
	beginning of this article. This bug has been fixed in Visual Studio 97 Service
	Pack 2.
	
	For more information on the Visual Studio 97 Service Pack 2, please see the
	following article in the Microsoft Knowledge Base:
	
	  Q170365 INFO: Visual Studio 97 Service Packs - What, Where, and Why
	
	MORE INFORMATION
	================
	
	The RETURN TO command is useful when the execution of code needs to be
	redirected to a method or event further up in the call stack. One reason for
	wanting to return to some method or event different from the calling method or
	event would be when trying to bypass the remainder of code in the event or
	method that is after the line of code that caused the error. For example, a
	Click event of the command button might call a method that executes some code.
	If this code causes an error, the Error event of the command button could handle
	the error and then a RETURN TO command could be used to return to the Click
	event of the command button without executing the rest of the code in the method
	that it called.
	
	The problem is that this works with only some of the FoxPro commands. For
	example, if the line of code that causes the error is "SET FILTER TO 10," the
	RETURN TO command does not work correctly. If the line of code is "WAIT WINDOW
	10," the RETURN TO command works correctly. Both are syntax errors, but one
	works and the other does not.
	
	Steps to Reproduce Behavior
	---------------------------
	
	1. Create a form with the form designer and add a command button.
	
	2. Place the following code in the Click event of the command button.
	
	        THISFORM.TriggerError
	        ? "After calling the Triggererror method in the command button."
	
	3. In the Error event of the command button, place the following code:
	
	        ? "In the Error event of the command button."
	        RETURN TO click
	
	4. Add a custom method to the form call TriggerError.
	
	5. Add the following code to the method TriggerError.
	
	        USE HOME()+"samples\data\customer"
	        SET FILTER TO 10
	        *WAIT WINDOW 10
	        ? "*** After the error code."
	
	6. Run the form and click on the command button.
	
	  Note that the "*** After the error code." message is displayed when the SET
	  FILTER TO 10 command triggers an error. Now comment the SET FILTER command
	  and uncomment the WAIT WINDOW 10 command. The "*** After the error code."
	  message doesn't appear now because execution is returned directly to the
	  Click event of the command button.
	
	  Another thing to be aware of is that if there is code in the Error event of
	  the form, control will not be returned to the method or event that is
	  identified in the RETURN TO command.
	
	Additional query words:
	
	======================================================================
	Keywords          : kbvfp kbVS97sp2fix 
	Technology        : kbVFPsearch kbAudDeveloper kbVFP300 kbVFP300b kbVFP500 kbVFP500a
	Version           : 3.0 5.0
	Issue type        : kbbug
	Solution Type     : kbfix
	
	=============================================================================
	

{% endraw %}
