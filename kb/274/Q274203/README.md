---
layout: page
title: "Q274203: PRB: Cannot Shift Focus from ATL Composite Control on Web Page"
permalink: /kb/274/Q274203/
---

## Q274203: PRB: Cannot Shift Focus from ATL Composite Control on Web Page

{% raw %}

	Article: Q274203
	Product(s): Microsoft C Compiler
	Version(s): 3.0,4.x,5,5.01,5.01 SP1,5.5
	Operating System(s): 
	Keyword(s): kbCtrl kbIE400 kbie401 kbATL300 kbSBNWorkshop kbGrpDSInet kbie500 kbDSupport kbie550
	Last Modified: 13-SEP-2001
	
	-------------------------------------------------------------------------------
	The information in this article applies to:
	
	- The Microsoft Active Template Library (ATL) 3.0 
	- Microsoft Internet Explorer (Programming) versions 4.0, 4.01, 4.01 SP1, 4.01 SP2, 5, 5.01, 5.01 SP1, 5.5 
	-------------------------------------------------------------------------------
	
	SYMPTOMS
	========
	
	When you use an ATL composite control on a Web page, the user may not be able to
	shift focus from the control to other elements on the page.
	
	CAUSE
	=====
	
	When you create the control, this problem occurs if you add support for the
	VALID stock property (DISPID_VALID) and fail to initialize it.
	
	RESOLUTION
	==========
	
	To resolve this problem, in the control class constructor, initialize the
	m_bValid variable of DISPID_VALID to 1.
	
	MORE INFORMATION
	================
	
	The problem is not reproducible if you run the debug version, or if you run the
	release version under the debugger. This is because you are not using the
	debugger; in most cases, the default values for uninitialized values are 0
	(zero). When you use the debugger, the default values are set to 0xCDCD (in
	other words, TRUE).
	
	When the m_bValid variable that is used to store this stock property value is 0
	(zero), it implies that the control's data is not in a valid state. When
	Internet Explorer tries to set focus to a new element and to set its site
	correctly, it checks whether the control is ready to give up focus by verifying
	its state. Since this value is 0 (zero) in release builds of the control, the
	focus is not shifted (killed).
	
	Steps to Reproduce Behavior
	---------------------------
	
	1. Use the Microsoft Visual C++ AppWizard to create an ATL Component Object
	  Model (COM) dynamic-link library (DLL) application.
	
	2. On the Insert menu, click ATL Object. In the Category list, click Controls.
	  In the Objects list, click Composite Control. Name the composite control.
	
	3. On the Stock Properties tab, click Valid, and click the greater than (>)
	  button to add the VALID stock property to the Supported list.
	
	4. In the resource editor, open the composite control dialog template, and add a
	  text box to the control. Build any release version of the control (Win32
	  Release MinSize, Win32 Release MinDependency, and so on).
	
	5. Open the HTML page that was created by the wizard in the source folder, and
	  add an INPUT text element.
	
	6. In Internet Explorer, open the HTML file, and set focus to the textbox in the
	  control. Press TAB to try to shift focus away from the control.
	
	Notice that you cannot shift focus to other elements on the page.
	
	REFERENCES
	==========
	
	For more information on developing Web-based solutions for Internet Explorer,
	please see the following Web sites:
	
	  http://msdn.microsoft.com/workshop/entry.asp
	
	  http://msdn.microsoft.com/ie/
	
	  http://support.microsoft.com/highlights/iep.asp?FR=0&SD=MSDN
	
	(c) Microsoft Corporation 2000, All Rights Reserved. Contributions by Kusuma
	Vellanki, Microsoft Corporation.
	
	
	Additional query words: kill
	
	======================================================================
	Keywords          : kbCtrl kbIE400 kbie401 kbATL300 kbSBNWorkshop kbGrpDSInet kbie500 kbDSupport kbie550 
	Technology        : kbVCsearch kbIEsearch kbAudDeveloper kbSDKIESearch kbATLsearch kbATL300 kbIE500Search kbSDKIE400 kbSDKIE401 kbSDKIE401SP1 kbSDKIE401SP2 kbSDKIE501SP1 kbSDKIE500 kbSDKIE501 kbSDKIE550 kbIE550Search
	Version           : :3.0,4.x,5,5.01,5.01 SP1,5.5
	Issue type        : kbprb
	
	=============================================================================
	

{% endraw %}
