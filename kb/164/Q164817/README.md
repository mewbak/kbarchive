---
layout: page
title: "Q164817: WD97: Bad Parameter Error with the AddPicture Method"
permalink: /kb/164/Q164817/
---

## Q164817: WD97: Bad Parameter Error with the AddPicture Method

{% raw %}

	Article: Q164817
	Product(s): Word 97 for Windows
	Version(s): WINDOWS:97
	Operating System(s): 
	Keyword(s): kbgraphic kbProgramming kbdta word8 kbwordvba word97
	Last Modified: 13-MAY-2002
	
	-------------------------------------------------------------------------------
	The information in this article applies to:
	
	- Microsoft Word 97 for Windows 
	-------------------------------------------------------------------------------
	
	
	SYMPTOMS
	========
	
	When you attempt to set both of the AddPicture properties--LinkToFile and
	SaveWithDocument--to False, the following error message appears:
	
	  Run time error 4120 - Bad Parameter
	
	CAUSE
	=====
	
	You cannot set both LinkToFile and SaveWithDocument to False.
	
	The following example Visual Basic for Applications command causes the error
	described in the "Symptoms" section of this article to occur:
	
	     ChangeFileOpenDirectory _
	        "C:\MyPics\"
	     Selection.InlineShapes.AddPicture FileName:= _
	        "My Picture.Gif", LinkToFile:=False, _
	           SaveWithDocument:=False
	
	WORKAROUND
	==========
	
	Microsoft provides programming examples for illustration only, without warranty
	either expressed or implied, including, but not limited to, the implied
	warranties of merchantability and/or fitness for a particular purpose. This
	article assumes that you are familiar with the programming language being
	demonstrated and the tools used to create and debug procedures. Microsoft
	support professionals can help explain the functionality of a particular
	procedure, but they will not modify these examples to provide added
	functionality or construct procedures to meet your specific needs. If you have
	limited programming experience, you may want to contact a Microsoft Certified
	Partner or the Microsoft fee-based consulting line at (800) 936-5200. For more
	information about Microsoft Certified Partners, please visit the following
	Microsoft Web site:
	
	  http://www.microsoft.com/partner/referral/
	
	For more information about the support options that are available and about how
	to contact Microsoft, visit the following Microsoft Web site:
	
	  http://support.microsoft.com/default.aspx?scid=fh;EN-US;CNTACTMS
	
	To work around this problem, set LinkToFile equal to False, or set
	SaveWithDocument equal to False, but not both. For example:
	
	To link to the picture file:
	
	     ChangeFileOpenDirectory _
	        "C:\MyPics\"
	     Selection.InlineShapes.AddPicture FileName:= _
	        "My Picture.Gif", LinkToFile:=True, _
	           SaveWithDocument:=False
	
	To save the picture file with the document:
	
	     ChangeFileOpenDirectory _
	        "C:\MyPics\"
	     Selection.InlineShapes.AddPicture FileName:= _
	        "My Picture.Gif", LinkToFile:=False, _
	           SaveWithDocument:=True
	
	STATUS
	======
	
	Microsoft has confirmed this to be a problem in the Microsoft products that are
	listed at the beginning of this article.
	
	MORE INFORMATION
	================
	
	For additional information, please see the following article in the Microsoft
	Knowledge Base:
	
	  Q173707 OFF97: How to Run Sample Code from Knowledge Base Articles
	
	
	REFERENCES
	==========
	
	For more information about getting help with Visual Basic for Applications,
	please see the following article in the Microsoft Knowledge Base:
	
	  Q163435 VBA: Programming Resources for Visual Basic for Applications
	
	Additional query words: wordcon vb vbe vba
	
	======================================================================
	Keywords          : kbgraphic kbProgramming kbdta word8 kbwordvba word97 
	Technology        : kbWordSearch kbWord97 kbWord97Search kbZNotKeyword2
	Version           : WINDOWS:97
	Issue type        : kbbug
	Solution Type     : kbpending
	
	=============================================================================
	

{% endraw %}
