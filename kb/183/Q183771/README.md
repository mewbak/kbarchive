---
layout: page
title: "Q183771: INFO: Registry Entries Made by an ActiveX Component"
permalink: /kb/183/Q183771/
---

## Q183771: INFO: Registry Entries Made by an ActiveX Component

{% raw %}

	Article: Q183771
	Product(s): Microsoft Visual Basic for Windows
	Version(s): 5.0,6.0,97
	Operating System(s): 
	Keyword(s): kbActiveX kbAPI kbRegistry kbVBp kbVBp500 kbVBp600 kbVC500 kbVS97 kbOSWin95 kbOSWin98 k
	Last Modified: 18-JUN-2001
	
	-------------------------------------------------------------------------------
	The information in this article applies to:
	
	- Microsoft Visual Basic Learning Edition for Windows, version 6.0 
	- Microsoft Visual Basic Professional Edition for Windows, versions 6.0, 5.0 
	- Microsoft Visual Basic Enterprise Edition for Windows, versions 6.0, 5.0 
	- Microsoft Visual Basic Control Creation Edition for Windows, version 5.0 
	- Microsoft Visual C++, 32-bit Enterprise Edition, version 5.0 
	-------------------------------------------------------------------------------
	
	SUMMARY
	=======
	
	An ActiveX component can be either an in-process or out-of-process (local or
	remote) server. When registering an ActiveX component on a Windows 95, Windows
	98, Windows Me, Windows NT 4.0 or Windows 2000 machine, specific entries are
	made in the Windows Registry that allow the components to be accessed by client
	applications. An ActiveX control is an example of an in-process server that is
	registered in the Windows Registry. The purpose of this article is to outline
	some of the Registry entries for an ActiveX component in order to assist in
	troubleshooting registry issues that may arise.
	
	MORE INFORMATION
	================
	
	An in-process component can be registered by using a utility such as
	Regsvr32.exe. The utility makes a call to the component's DllRegisterServer
	method. At this point, a series of entries is made in the Windows Registry. The
	method for registering out-of-process servers can vary.
	
	The scope of this article will only refer to one branch of the Registry:
	HKEY_CLASSES_ROOT. This same information can also be found in
	HKEY_LOCAL_MACHINE/Software/Classes. For troubleshooting and removal purposes,
	you only need to focus on HKEY_CLASSES_ROOT.
	
	In the HKEY_CLASSES_ROOT branch, you will initially find a list of file
	extensions. Following the file extensions are a combination of Programmatic
	Identifiers (ProgIDs) along with special keys that will be discussed shortly.
	
	ProgIDs are typically friendly names that refer directly to a component's
	ClassID. The typical format for a ProgID is
	<Application>.<Class>.<Version>. However, this format is not
	strictly enforced and often times the version portion is ignored. Examples of
	ProgIDs are "Word.Application.8" and "Excel.Chart."
	
	Each ProgID refers to a ClassID. The ClassID (or CLSID)is formatted as
	{xxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxx}.
	
	Along with ProgIDs, special keys such as AppID, CLSID, Component Categories,
	Interface, Licenses, and TypeLib are found directly below HKEY_CLASSES_ROOT.
	Information regarding your ActiveX component can be entered in any of these
	special keys. The focus of this article is only on the CLSID, TypeLib, and
	Interface special keys. For more information concerning these and other special
	keys, refer to the resources listed in the REFERENCES section of this article.
	
	IMPORTANT: This article contains information about editing the registry. Before
	you edit the registry, make sure you understand how to restore it if a problem
	occurs. For information about how to restore the registry, refer to the Help
	files in the Registry Editor (Regedit.exe).
	
	You can use this information to remove all references of a given component from
	the registry or to troubleshoot a possible registry problem.
	
	The following steps illustrate how you can step through the registry and find
	references to an ActiveX component:
	
	1. Run the Registry Editor (Regedit.exe).
	
	2. The first step is to find the Programmatic Identifier (ProgID). This can be
	  found directly under the HKEY_CLASSES_ROOT branch. Again the typical format
	  is <Application>.<Class>.<Version>. For example:
	  MSComDlg.CommonDialog.1.
	
	3. Once you have found the ProgID for a given component, expand it and select
	  the CLSID subkey.
	
	4. In the right pane, you will see the ClassID that this ProgID is associated
	  with. For example: {F9043C85-F6F2-101A-A3C9-08002B2F49FB}
	
	5. Copy this ClassID by double-clicking the Default string icon and copying the
	  value from the Dialog window that appears.
	
	6. Select and expand the subkey HKEY_CLASSES_ROOT\CLSID. Note that the subkeys
	  are ClassIDs.
	
	7. Click the Edit menu and choose Find. Paste the ClassID value that you copied
	  from the ProgID. Click the Find Next button to locate the value under
	  HKEY_CLASSES_ROOT\CLSID.
	
	8. Once you find the subkey, expand it. Note that there are several subkeys,
	  including InprocServer32, ProgID, TypeLib, and Version.
	
	9. Select the TypeLib subkey and copy this TypeLibID by double-clicking the
	  Default string icon in the right pane and copying the value from the Dialog
	  window that appears.
	
	10. Select and expand the subkey HKEY_CLASSES_ROOT\TypeLib.
	
	11. Click Find on the Edit menu. Paste the TypeLibID value that you copied from
	  the ClassID and then click Find Next. The registry subkey that is found
	  contains information about your component's Type Library.
	
	12. Select and expand the subkey HKEY_CLASSES_ROOT\Interface.
	
	13. Click Find on the Edit menu. Paste the TypeLibID value that you copied from
	  the ClassID and then click Find Next.
	
	14. Unlike the other searches you have completed, the search under the
	  Interfaces subkey results in a one-to-many relationship between the
	  TypeLibID and the InterfaceIDs associated with that TypeLibID. To find all
	  the InterfaceIDs, click Find Next from the Edit Menu or press the F3 key.
	
	REFERENCES
	==========
	
	"Inside COM" by Dale Rogerson, Microsoft Press (ISBN 1-57231-349-8)
	
	For a list of additional resources regarding the Windows 95, Windows 98, or
	Windows NT registry, please see the following article in the Microsoft Knowledge
	Base:
	
	  Q173014 : INFO: Windows Registry Resources
	
	Additional query words:
	
	======================================================================
	Keywords          : kbActiveX kbAPI kbRegistry kbVBp kbVBp500 kbVBp600 kbVC500 kbVS97 kbOSWin95 kbOSWin98 kbGrpDSVB _IK kbOSWinME 
	Technology        : kbVCsearch kbVBSearch kbAudDeveloper kbZNotKeyword6 kbZNotKeyword2 kbVB500Search kbVB600Search kbVBA500Search kbVB500 kbVB600 kbZNotKeyword3 kbVC500 kbVC32bitSearch kbVC500Search
	Version           : :5.0,6.0,97
	Issue type        : kbinfo
	
	=============================================================================
	

{% endraw %}
