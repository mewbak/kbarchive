---
layout: page
title: "Q233059: Error Message When Attempting to Create a Folder NTFS Partition"
permalink: /kb/233/Q233059/
---

## Q233059: Error Message When Attempting to Create a Folder NTFS Partition

{% raw %}

	Article: Q233059
	Product(s): Microsoft Windows NT
	Version(s): winnt:4.0
	Operating System(s): 
	Keyword(s): 
	Last Modified: 06-AUG-2002
	
	-------------------------------------------------------------------------------
	The information in this article applies to:
	
	- Microsoft Windows NT Server version 4.0, Terminal Server Edition 
	- Microsoft Windows NT Server version 4.0 
	- Microsoft Windows NT Server, Enterprise Edition version 4.0 
	- Microsoft Windows NT Workstation version 4.0 
	-------------------------------------------------------------------------------
	
	SYMPTOMS
	========
	
	When you attempt to create a folder or subfolder on an NTFS partition or volume,
	the following error message may be displayed:
	
	  Unable to create the folder <New Folder>. The inherited access control
	  list (ACL) or the access control entry (ACE) could not be built.
	
	CAUSE
	=====
	
	This behavior occurs because the buffer size on an access control list (ACL) may
	be exceeded.
	
	The maximum size of an ACL is 64 KB. An ACL contains access control entries
	(ACEs), which also vary in size, so the total number of ACEs that can be placed
	in an ACL varies. A container object contains two sets of ACEs. One is for the
	container itself, and the other is for the inheritable ACEs. This is because of
	the way ACLs are inherited, and cannot be changed.
	
	The creation algorithm checks to see if the size of the parent's ACL is larger
	than 32 KB. If so, the buffer is exceeded and the child container object cannot
	be created.
	
	WORKAROUND
	==========
	
	To work around this issue, use either of the following methods.
	
	Method 1: Remove the ACEs from the ACL on the parent container.
	
	1. In Windows NT Explorer, right-click the folder, and then click Properties.
	
	2. Click the Security tab.
	
	3. Click Permissions. At this point, you are viewing the ACEs of the ACL.
	
	4. Click the users and groups in the list that you want to remove, and then
	  click Remove.
	
	5. After you remove enough ACEs from the ACL, you can create the subfolder.
	
	Method 2: Create a child folder that does not inherit the parent's ACE list.
	
	1. On the same partition on which the parent folder is located, create a new
	  folder (for example, if the parent folder is on drive C, create the new
	  folder somewhere on drive C).
	
	2. Move the new folder into the appropriate parent folder.
	
	3. Set the permissions you want on the new subfolder.
	
	Method 2 works because moving files and folders within the same partition allows
	the object to retain its own permissions, and not inherit the parents.
	Therefore, the new subfolder does not have the same permissions as the parent.
	
	STATUS
	======
	
	This behavior is by design.
	
	A few hundred objects (ACEs) in an ACL is more than enough to successfully manage
	permissions on that object. An excessive amount of ACEs in an ACL uses many
	resources and is not within the boundaries of the Windows NT security model. In
	fact, enumerating such an ACL is often the most costly transaction when you open
	a file.
	
	The Windows NT security model relies on the use of nesting global groups within
	local groups. If you have more than a few hundred ACEs assigned in an ACL, you
	may want to reassess how permissions are assigned. In addition, a large number
	of ACEs in an ACL makes it difficult to determine the actual access level of a
	specific user.
	
	MORE INFORMATION
	================
	
	Access Control List
	-------------------
	
	This is the part of a security descriptor that enumerates the protections applied
	to an object. The owner of an object has discretionary access control of the
	object and can change the object's ACL to allow or disallow others' access to
	the object. ACLs are made up of access control entries.
	
	Access Control Entry
	--------------------
	
	This is an entry in an ACL. The entry contains a security ID (SID) and a set of
	access rights. A process with a matching security ID is allowed access rights,
	denied rights, or allowed rights with auditing.
	
	Using NTFS, you can add a user to an ACL. The ACL lets the user gain access to a
	file, and can at the same time prevent the user from copying or running a file.
	Each ACL is made up of ACEs, which specify access or auditing permissions to
	that object for one user or group.
	
	There are three ACE types; two for discretionary access control and one for
	system security. The discretionary ACEs are AccessAllowed and AccessDenied.
	These explicitly grant and deny access to a user or group of users. The first
	AccessDenied ACE denies the user access to the resource, and no further
	processing of ACEs occurs.
	
	NOTE: There is an important distinction between a discretionary ACL that is empty
	(one that contains no ACEs) and an object without any discretionary ACL. In the
	case of an empty discretionary ACL, no access is explicitly granted, so access
	is implicitly denied. For an object without an ACL, there is no protection
	assigned to the object, so any access request is granted.
	
	SystemAudit is a system security ACE that is used to keep a log of security
	events (such as who uses which files) and to generate and log security audit
	messages.
	
	
	
	Additional query words:
	
	======================================================================
	Keywords          :  
	Technology        : kbWinNTsearch kbWinNTWsearch kbWinNTW400 kbWinNTW400search kbWinNT400search kbWinNTSsearch kbWinNTSEntSearch kbWinNTSEnt400 kbWinNTS400search kbWinNTS400 kbNTTermServ400 kbNTTermServSearch
	Version           : winnt:4.0
	Issue type        : kbprb
	
	=============================================================================
	

{% endraw %}
