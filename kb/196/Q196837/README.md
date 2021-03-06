---
layout: page
title: "Q196837: BUG: Compile Errors Result for Certain ATL Method Parameters"
permalink: /kb/196/Q196837/
---

## Q196837: BUG: Compile Errors Result for Certain ATL Method Parameters

{% raw %}

	Article: Q196837
	Product(s): Microsoft C Compiler
	Version(s): winnt:5.0
	Operating System(s): 
	Keyword(s): kbwizard kbATL200bug kbAutomation kbCOMt kbVC500bug kbGrpDSMFCATL kbCollectionClass
	Last Modified: 07-MAY-2001
	
	-------------------------------------------------------------------------------
	The information in this article applies to:
	
	- Microsoft Visual C++, 32-bit Enterprise Edition, version 5.0 
	- Microsoft Visual C++, 32-bit Professional Edition, version 5.0 
	-------------------------------------------------------------------------------
	
	SYMPTOMS
	========
	
	Using the ATL Interface Wizard from Visual C++ 5.0 to add a method to an
	interface, you will get compilation errors C2061 if you specified any of the
	following for parameters in the dialog box:
	
	     SAFEARRAY(type) pSA
	     SAFEARRAY(type) *ppSA
	
	CAUSE
	=====
	
	This problem is caused by a limitation in the ATL COM Interface Wizard.
	
	RESOLUTION
	==========
	
	To cause the ATL code to compile, you must make modifications to the method that
	was added with the ATL COM Interface wizard in the .h and .cpp files.
	
	The correct declarations and definitions that must be used for each of the known
	data types that cause the problems are shown below (assume that the interface is
	IATLObj and the ATL class that is implementing the interface is CATLObj):
	
	For instance, the following are wizard-generated function prototypes in the .h
	file:
	
	     STDMETHOD(Test)(SAFEARRAY(BSTR) *ppArrayBstr);
	     STDMETHOD(Test2)(SAFEARRAY(BSTR) pArrayBstr);
	
	The correct declarations for header file should be:
	
	     STDMETHOD(Test)(SAFEARRAY **ppArrayBstr);
	     STDMETHOD(Test2)(SAFEARRAY *pArrayBstr);
	
	The correct definitions for source file should be:
	
	     STDMETHODIMP CATLObj::Test(SAFEARRAY **ppArrayBstr)
	     {
	        return S_OK;
	     }
	
	     STDMETHODIMP CATLObj::Test2(SAFEARRAY *pArrayBstr)
	     {
	        return S_OK;
	     }
	
	You will notice that if you use the above method, the Class view information in
	the Tree view may look different for CATLObj. Test and Test2 will not be in the
	IATLObj interface section in Class view for CATLObj as they were before. They
	are now in the member function section. You can correct this behavior by not
	making the changes above; and instead, using a macro. To do this, make the
	following modifications to the header file before the class definition:
	
	     #define SAFEARRAY(X) SAFEARRAY*
	
	Class view will now properly display the new methods under the interface section
	instead of under the member function section.
	
	STATUS
	======
	
	Microsoft has confirmed this to be a bug in the Microsoft products listed at the
	beginning of this article.
	
	MORE INFORMATION
	================
	
	Steps to Reproduce Behavior
	---------------------------
	
	1. Create a new ATL/COM Application Wizard Project.
	
	2. Insert a new ATL COM Object with the default settings.
	
	3. Add a new method with the ATL COM Object Wizard by right-clicking the
	  interface to add the method and selecting "Add Method."
	
	4. Give the method a name.
	
	5. Add one parameter with SAFEARRAY(BSTR)* as the type. For example:
	
	        [out] SAFEARRAY(BSTR) *pArrayBSTR
	
	6. Build the project.
	
	You will receive Compiler Error C2061 due to the incorrect syntax for the
	parameter in the header and source files.
	
	
	Additional query words:
	
	======================================================================
	Keywords          : kbwizard kbATL200bug kbAutomation kbCOMt kbVC500bug kbGrpDSMFCATL kbCollectionClass 
	Technology        : kbVCsearch kbAudDeveloper kbVC500 kbVC32bitSearch kbVC500Search
	Version           : winnt:5.0
	Issue type        : kbbug
	
	=============================================================================
	

{% endraw %}
