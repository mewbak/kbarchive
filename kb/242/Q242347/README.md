---
layout: page
title: "Q242347: PRB: Error Message &quot;Invalid Procedure Call or Argument&quot;"
permalink: /kb/242/Q242347/
---

## Q242347: PRB: Error Message &quot;Invalid Procedure Call or Argument&quot;

{% raw %}

	Article: Q242347
	Product(s): Microsoft Visual Basic for Windows
	Version(s): WINDOWS:4.0,5.0,6.0
	Operating System(s): 
	Keyword(s): kbVBp kbVBp400 kbVBp500 kbVBp600 kbGrpDSVB kbDSupport
	Last Modified: 11-JAN-2001
	
	-------------------------------------------------------------------------------
	The information in this article applies to:
	
	- Microsoft Visual Basic Learning Edition for Windows, versions 5.0, 6.0 
	- Microsoft Visual Basic Professional Edition for Windows, versions 5.0, 6.0 
	- Microsoft Visual Basic Enterprise Edition for Windows, versions 5.0, 6.0 
	- Microsoft Visual Basic Standard Edition, 32-bit, for Windows, version 4.0 
	- Microsoft Visual Basic Enterprise Edition, 32-bit, for Windows, version 4.0 
	-------------------------------------------------------------------------------
	
	SYMPTOMS
	========
	
	If a modal dialog or form is programmatically shown in code, other executing
	code in the same process that calls SetFocus on a control on a dialog or form
	other than the one currently modal raises the following:
	
	  Run-time Error '5'
	  Invalid Procedure Call or Argument
	
	This only occurs when running the application as a compiled EXE. This does not
	occur in the Visual Basic IDE.
	
	CAUSE
	=====
	
	In the case of the SetFocus call, when a modal dialog, such as a messagebox or a
	modal Visual Basic form is shown, any other forms and their controls are
	disabled. Calling SetFocus on a disabled control always generates an error of
	this type.
	
	RESOLUTION
	==========
	
	There are several workarounds that can be used:
	
	The most elegant workaround is to first check to see if the target of the
	SetFocus is Enabled.
	
	The problem can be avoided by changing the repro sample code in the Timer event
	from this:
	
	  Private Sub Timer1_Timer()
	          Command2.SetFocus
	  End Sub
	
	to this:
	
	  Private Sub Timer1_Timer()
	          If Command2.Enabled = True Then
	               Command2.SetFocus
	          Else
	               Beep
	          End If
	  End Sub
	
	This works because whenever a modal dialog or form is shown, the controls on
	non-modal forms in that process become disabled.
	
	Other ways that can work around this problem include:
	
	- Trapping the Error 5 within the procedure that actually calls the SetFocus.
	
	- Setting a global flag that becomes True when a call to MsgBox is made and
	  check it before you make a call to SetFocus.
	
	STATUS
	======
	
	This behavior is by design.
	
	MORE INFORMATION
	================
	
	Steps to Reproduce Behavior
	---------------------------
	
	1. Start a new Standard EXE project in Visual Basic. Form1 is created by
	  default.
	
	2. Add two Command Buttons, Command1 and Command2, and a Timer control, Timer1,
	  to Form1.
	
	3. Add the following code to Form1:
	
	  Private Sub Command1_Click()
	      MsgBox "Wait until the timer control fires"
	  End Sub
	
	  Private Sub Timer1_Timer()
	          Command2.SetFocus
	  End Sub
	
	4. Set the Timer1.Interval property to 3000 for a three-second delay.
	
	5. Compile the project and run the newly-compiled EXE file.
	
	6. Immediately after starting the application, click Command1 and wait for the
	  Timer control to fire its Timer Event. When the event fires, you receive the
	  error dialog described in the SYMPTOMS section above. After dismissing this
	  dialog and the message box, your application terminates.
	
	Additional query words: modally
	
	======================================================================
	Keywords          : kbVBp kbVBp400 kbVBp500 kbVBp600 kbGrpDSVB kbDSupport 
	Technology        : kbVBSearch kbAudDeveloper kbZNotKeyword6 kbZNotKeyword2 kbVB500Search kbVB600Search kbVBA500 kbVBA600 kbVB500 kbVB600 kbVB400Search kbVB400
	Version           : WINDOWS:4.0,5.0,6.0
	Issue type        : kbprb
	
	=============================================================================
	

{% endraw %}
