---
layout: page
title: "Q138649: How to Use OLE to Edit General Fields in Visual FoxPro"
permalink: /kb/138/Q138649/
---

## Q138649: How to Use OLE to Edit General Fields in Visual FoxPro

{% raw %}

	Article: Q138649
	Product(s): Microsoft FoxPro
	Version(s): 
	Operating System(s): 
	Keyword(s): 
	Last Modified: 26-AUG-1999
	
	-------------------------------------------------------------------------------
	The information in this article applies to:
	
	- Microsoft Visual FoxPro for Windows, version 3.0 
	-------------------------------------------------------------------------------
	
	SUMMARY
	=======
	
	Editing general fields is much easier in Visual FoxPro. A new control called the
	OLE Bound Control is used to select general fields in the Form Builder and allow
	editing of a general field when the form is running. The application used to
	place the data into the general field when it was created is the application
	that will appear on the screen when the form is running and you click the
	general field to edit it.
	
	For example, if you placed data into the general field by clicking Insert Object
	on the Edit menu and then clicking Paintbrush, Paintbrush will appear when you
	click the general field object of the form. Some applications that are OLE 2.0
	aware, such as Microsoft Word or Microsoft Excel, will add their functionality
	to the FoxPro menu, so you need only click the menu to change the data in the
	general field object of the form.
	
	MORE INFORMATION
	================
	
	Step-by-Step Example
	--------------------
	
	1. Create a table with a general field in it, and save the table.
	
	2. When prompted to Input Data Records Now, click Yes. Double-click the general
	  field to open it. On the Edit menu, click Insert Object. In the Object Type
	  list, scroll down to the Paintbrush Picture item and select it. When
	  Paintbrush appears, draw something in the paintbrush window. On the File menu
	  in Paintbrush, click Exit to Return to <tablename.fieldname>. Click Yes
	  in the window that appears to update the general field.
	
	3. Close the general field by pressing CTRL+W. Add another record to the table
	  and repeat step 2. This time select another application in the Object Type
	  box. If the application is OLE 2 aware, editing will take place in the
	  general field itself. Close the general field to save the data placed into
	  it.
	
	4. Close the Browse window of the table, and create a form. Choose the OLE Bound
	  Control from the Forms Control toolbar, and place it on the form.
	
	5. In the Properties sheet, type the name of the general field in the
	  ControlSource property of the OLE Bound control.
	
	6. To allow all of the data from the general field to fit into the OLE object of
	  the form, select 1 or 2 in the Stretch property.
	
	7. Place a command button on the form, and type the following code into its
	  Click event:
	
	     SKIP
	     THISFORM.REFRESH
	
	8. Run the form, and double-click the general field. Note that Paintbrush
	  appears allowing the picture to be edited. Make changes to the paintbrush
	  picture, and close it. Click the command button, and then double-click the
	  general field again. Note that the application used to place the data into
	  the general field earlier appears again.
	
	Additional query words: VFoxWin
	
	======================================================================
	Keywords          :  
	Technology        : kbVFPsearch kbAudDeveloper kbVFP300
	
	=============================================================================
	

{% endraw %}
