---
layout: page
title: "Q189735: BUG: Removing Collection Elements Takes Longer Than Expected"
permalink: /kb/189/Q189735/
---

## Q189735: BUG: Removing Collection Elements Takes Longer Than Expected

{% raw %}

	Article: Q189735
	Product(s): Microsoft Visual Basic for Windows
	Version(s): 
	Operating System(s): 
	Keyword(s): kbGrpDSVB
	Last Modified: 11-JAN-2001
	
	-------------------------------------------------------------------------------
	The information in this article applies to:
	
	- Microsoft Visual Basic Learning Edition for Windows, version 6.0 
	- Microsoft Visual Basic Professional Edition for Windows, version 6.0 
	- Microsoft Visual Basic Enterprise Edition for Windows, version 6.0 
	-------------------------------------------------------------------------------
	
	SYMPTOMS
	========
	
	In Visual Basic 6.0, removing elements from the end of a collection takes longer
	than removing elements from the beginning.
	
	CAUSE
	=====
	
	When removing an element from a collection, Visual Basic 6.0 begins at the
	beginning of the collection and traverses the collection until the desired
	element is reached, then that element is removed.
	
	RESOLUTION
	==========
	
	Remove elements from the beginning of the collection rather than the end.
	
	STATUS
	======
	
	Microsoft has confirmed this to be a bug in the Microsoft products listed at the
	beginning of this article. We are researching this bug and will post new
	information here in the Microsoft Knowledge Base as it becomes available.
	
	MORE INFORMATION
	================
	
	Steps to Reproduce Behavior
	---------------------------
	
	1. Create a new Standard EXE project in Visual Basic. Form1 is created by
	  default.
	
	2. Select Add Module from the Project menu. This will create Module1.
	
	3. Select Project1 Properties from the Project menu. Change the Startup Object
	  to Sub Main.
	
	4. Copy and paste the following code into Module1:
	
	        Sub Main()
	
	           Dim c As New Collection
	           Dim a As Long
	
	           Set c = New Collection
	
	           'Add elements to collection
	           For a = 1 To 10000
	              c.Add "Thank you sir, may I have another."
	           Next a
	           MsgBox "Done adding elements"
	
	           'Remove elements from end, this takes long time
	           For a = 10000 To 1 Step -1
	              c.Remove a
	           Next a
	           MsgBox "Done removing elements from end"
	
	           'Add elements to collection again
	           For a = 1 To 10000
	              c.Add "Thank you sir, may I have another."
	           Next a
	           MsgBox "Done adding elements"
	
	           'Remove elements from beginning, this is much quicker
	           For a = 1 To 10000
	              c.Remove 1
	           Next a
	           MsgBox "Done removing elements from end"
	         End Sub
	
	5. Press the F5 key to run the project. Note the time difference between the two
	  methods of deleting elements from a collection.
	
	Additional query words: kbDSupport kbVBp600bug kbVBp kbdss kbNoKeyWord
	
	======================================================================
	Keywords          : kbGrpDSVB 
	Technology        : kbVBSearch kbAudDeveloper kbZNotKeyword6 kbZNotKeyword2 kbVB600Search kbVBA600 kbVB600
	Issue type        : kbbug
	
	=============================================================================
	

{% endraw %}
