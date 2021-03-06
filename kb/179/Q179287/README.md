---
layout: page
title: "Q179287: FIX: Insufficient Memory in Visual FoxPro on Fast Computers"
permalink: /kb/179/Q179287/
---

## Q179287: FIX: Insufficient Memory in Visual FoxPro on Fast Computers

{% raw %}

	Article: Q179287
	Product(s): Microsoft FoxPro
	Version(s): WINDOWS:3.0,3.0b
	Operating System(s): 
	Keyword(s): kbvfp kbvfp300 kbvfp300b
	Last Modified: 24-MAR-2000
	
	-------------------------------------------------------------------------------
	The information in this article applies to:
	
	- Microsoft Visual FoxPro for Windows, versions 3.0, 3.0b 
	-------------------------------------------------------------------------------
	
	SYMPTOMS
	========
	
	When using a large table, cursor, or array (over 275 records) as the row source
	of a combo box, you may see the following error message:
	
	  There is not enough memory to complete this operation.
	
	RESOLUTION
	==========
	
	Here are four workarounds for this problem:
	
	- Upgrade to Visual FoxPro version 5.0.
	
	  -or-
	
	- Use a grid control.
	
	  -or-
	
	- Use a list box control.
	
	  -or-
	
	- Limit the size of the underlying table, cursor, or array to 275 records or
	  less.
	
	The following code snippets illustrate implementation of the grid and list box
	workarounds based on the code example provided in the MORE INFORMATION section.
	
	To use a grid instead of a combo box, replace the cbocombo class definition with
	the following code:
	
	     DEFINE CLASS cboCombo AS GRID
	        LEFT = 10
	        TOP = 25
	        WIDTH=140
	        HEIGHT=100
	        VISIBLE=.T.
	        RECORDSOURCETYPE=1
	        RECORDSOURCE="Customer"
	     ENDDEFINE
	
	To use a list box instead of a combo box, replace the cbocombo class definition
	with the following code:
	
	     DEFINE CLASS cboCombo AS LISTBOX
	        LEFT = 10
	        TOP = 25
	        WIDTH=140
	        HEIGHT=100
	        VISIBLE=.T.
	        ROWSOURCETYPE=6
	        ROWSOURCE="Customer.cust_id"
	     ENDDEFINE
	
	STATUS
	======
	
	Microsoft has confirmed this to be a problem in the Microsoft products listed at
	the beginning of this article. This has been corrected in Visual FoxPro 6.0.
	
	MORE INFORMATION
	================
	
	This behavior does not occur in Visual FoxPro 5.0 or 5.0a nor does this behavior
	occur with Visual FoxPro 3.0 when either of the following conditions is true:
	
	- The combo box Style property is set to 0 - Dropdown Combo.
	
	  -or-
	
	- The combo box has been opened using the mouse.
	
	The problem does occur under the following conditions:
	
	- The Combo box Style property is set to 2 - Dropdown List.
	
	  -or-
	
	- The Combo box RowSourceType property is set to one of the following:
	
	     2 - Alias
	     3 - SQL Statement
	     4 - Query (.qpr)
	     5 - Array
	     6 [ASCII 150] Fields
	
	  -or-
	
	- The Combo box is being navigated using the keyboard.
	
	  -or-
	
	- Visual FoxPro 3.0 is being run on a computers with a clock speeds of 166 MHz
	  or greater.
	
	Steps to Reproduce Behavior
	---------------------------
	
	1. Create a program called FrmCombo.prg using the following code:
	
	  
	
	        ofrmcombo = CREATEOBJECT("frmcombo")
	        ofrmcombo.VISIBLE = .T.
	        ofrmcombo.ADDOBJECT("cboCombo1","cbocombo")
	        ofrmcombo.ADDOBJECT("btnExit","cmdExit")
	
	        READ EVENTS
	
	        DEFINE CLASS frmcombo AS FORM
	           CAPTION="Combo Form"
	           TOP=0
	           LEFT=0
	           HEIGHT=150
	           WIDTH=225
	           PROCEDURE LOAD
	              CREATE CURSOR customer (cust_id c(10))
	              FOR i=1 TO 350
	                 INSERT INTO customer (cust_id) VALUES (SYS(2015))
	              NEXT
	              GO TOP
	           ENDPROC
	           PROCEDURE ACTIVATE
	              THISFORM.REFRESH
	           ENDPROC
	        ENDDEFINE
	
	        DEFINE CLASS cbocombo AS COMBOBOX
	           LEFT = 10
	           TOP = 25
	           WIDTH = 140
	           HEIGHT = 25
	           VISIBLE = .T.
	           INCREMENTALSEARCH=.F.
	           CONTROLSOURCE="Customer.cust_id"
	           ROWSOURCETYPE=6
	           ROWSOURCE="Customer.cust_id"
	           STYLE=2
	        ENDDEFINE
	
	        DEFINE CLASS cmdexit AS COMMANDBUTTON
	           CAPTION = "Exit"
	           LEFT = 155
	           TOP = 25
	           WIDTH = 50
	           HEIGHT = 25
	           VISIBLE = .T.
	           PROCEDURE CLICK
	              THISFORM.RELEASE
	              CLEAR EVENTS
	           ENDPROC
	        ENDDEFINE
	
	2. Run the program. Once the form appears, move through the data in the combo
	  box by holding down the DOWN ARROW key. The data appears to scroll through
	  the combo box. At some point, the error occurs.
	
	Additional query words:
	
	======================================================================
	Keywords          : kbvfp kbvfp300 kbvfp300b 
	Technology        : kbVFPsearch kbAudDeveloper kbVFP300 kbVFP300b
	Version           : WINDOWS:3.0,3.0b
	Issue type        : kbbug kbprb
	Solution Type     : kbfix
	
	=============================================================================
	

{% endraw %}
