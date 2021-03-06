---
layout: page
title: "Q67805: LAN Manager 2.0 Named Pipe Performance Information"
permalink: /kb/067/Q67805/
---

## Q67805: LAN Manager 2.0 Named Pipe Performance Information

{% raw %}

	Article: Q67805
	Product(s): Microsoft LAN Manager
	Version(s): 
	Operating System(s): 
	Keyword(s): 
	Last Modified: 30-JUL-2001
	
	SUMMARY
	=======
	
	The following questions address performance related issues involving the use of
	named pipes in Microsoft OS/2 LAN Manager version 2.x.
	
	1. Q. I have heard that OS/2 LAN Manager version 2.x uses a "sliding window"
	  algorithm to help manage its network performance. Is this related to the
	  protocol that I am using?
	
	  A. Sliding window algorithms are not limited to OS/2 LAN Manager. OS/2 LAN
	  Manager improves upon the basic algorithm by making it more sensitive to
	  network load and other factors. Whether OS/2 LAN Manager uses the sliding
	  window algorithm is protocol dependent. This algorithm is a part of the
	  NetBEUI protocol stack that is shipped with OS/2 LAN Manager version 2.x.
	
	2. Q. Does OS/2 LAN Manager take advantage of intelligent network cards? If not,
	  are there plans to add this functionality in the future?
	
	  A. Currently, OS/2 LAN Manager does not utilize intelligent network cards, nor
	  are there any plans to do so in the future. This is because intelligent
	  network cards (NICs) generally lag behind other cards and are usually
	  designed to the lowest common denominator of the PCs they must work with.
	  What often happens is that the INC becomes a bottleneck rather then a help
	  (especially with faster CPUs).
	
	3. Q. If there are several named pipe connections between a client and a server
	  machine, will OS/2 LAN Manager package together data from all the pipes
	  before sending them across to the target machine?
	
	  A. No. The underlying Server Message Block (SMB) protocol used by OS/2 LAN
	  Manager does not support this type of functionality. Also, please note that
	  pipes are a server resource and live on an OS/2 LAN Manager server. Whenever
	  data is written by a client, it is immediately (with the normal OS/2 LAN
	  Manager buffering) transmitted to the server that owns the pipe. However,
	  whenever data is written by the server, it remains on the machine until it is
	  requested by the client. When data is requested, the same is true. The server
	  retrieves it out of the local pipe buffers, and the client generates a
	  network request to the server for the data. Because pipes live on servers,
	  any client request will generate network traffic [even a DosPeekNmPipe()
	  call].
	
	4. Q. Since pipes live on the server, does OS/2 LAN Manager do anything to speed
	  up the usage of remote named pipes? In other words, what kind of buffering
	  strategy does an OS/2 LAN Manager server use for named pipes?
	
	  A. With the exception of reads and writes, most pipe requests are some sort of
	  a transaction and can be processed with a single network request. For reads
	  and writes, there are several internal protocols that can be used, depending
	  upon the availability of server resources, the mode of the pipe, and the size
	  of the request. Listed below are the different types of protocols:
	
	   - RAW protocol
	
	     This protocol is used to transfer large amounts of data (up to 64K) when
	     possible, and is only used for pipes when they are in nonblocking mode.
	     Data sent in RAW mode is sent in a series of NCBs (network control
	     blocks), each containing a portion of the data, until all of the data has
	     been sent. Then, a single acknowledgment is returned by the target.
	
	   - MPX protocol
	
	     This is similar to the RAW protocol, except the server and client negotiate
	     a maximum packet size that the data will be broken into. As with RAW, only
	     a single acknowledgment is sent after the data is all transferred. MPX is
	     not supported by the DOS redirector (and therefore will never be used by
	     DOS clients).
	
	   - Standard protocol
	
	     This protocol divides the data into several packets for network transfer,
	     and receives an acknowledgment for each packet sent. This protocol is used
	     whenever the data will fit into the normal packet size. The server may
	     request that a client use standard (or MPX), depending on the amount of
	     resources it has, and other factors.
	
	   - Generic transact protocol
	
	     This protocol is used for APIs that do not involve read or write
	     functionality, and is also used with the DosTransactNmPipe() API. It is
	     similar to the MPX protocol except that it assumes 0-64K packet sizes (on
	     both the send and receive ends). For example, this protocol allows the
	     client [via the DosTransactNmPipe() API] to complete a relatively small
	     write followed by a small read with half the number of packets normally
	     required. If the amount of data to transfer is larger then the negotiated
	     buffer size in use by the client and server, it will be divided into
	     packets of the negotiated size (as with the MPX protocol).
	
	  Beyond the various protocols that OS/2 LAN Manager may use internally, the
	  server end that owns the pipe also includes some enhancements (which are part
	  of the HPFS386 IFS shipped with OS/2 LAN Manager version 2.x). Essentially,
	  for remote pipes with HPFS386.IFS installed, OS/2 LAN Manager is able to
	  bypass the OS/2 kernel in many cases, thus saving unnecessary ring
	  transitions and movement of the data.
	
	  In the normal case (without HPFS386), data is transferred from the network
	  into OS/2 owned pipe buffers, and then finally to the application's buffers.
	  With HPFS386 installed, OS/2 LAN Manager will attempt to copy the data
	  directly to the application's buffers. It will always be able to do this if a
	  read is outstanding when the data arrives (this is the advantage of
	  dedicating a thread to reading a blocking-mode named pipe). If no read is
	  outstanding, OS/2 LAN Manager will hold the data in its own internal buffers
	  as long as it can (waiting for a read to be issued).
	
	  Additionally, with DosTransactNmPipe() calls, the data written in response can
	  be taken directly from the application's buffers, thus bypassing (again) the
	  OS/2 internal pipe buffers.
	
	  An application will get the best pipe response time by dedicating a thread to
	  the pipe and blocking on reads. This will be faster than either using a
	  semaphore or polling. Additional optimizations for named pipes exist in the
	  NetBEUI protocol stack. For example, some requests may even be handled at
	  interrupt time.
	
	5. Q. What can an application do to obtain the best possible named pipe
	  performance?
	
	  Foremost, the server should be using HPFS386 so that OS/2 LAN Manager can
	  bypass as much of the OS/2 kernel as possible. Also, as noted, if resources
	  allow it, an application will get the best possible performance by dedicating
	  a thread to a pipe so that when the data arrives it can be transferred
	  immediately.
	
	  If the amount of the data to be transferred is small, an application may want
	  to consider using the DosTransactNmPipe() call (to minimize network traffic).
	  On the server, for small data I/O requests, the number of request buffers
	  specified is important. Always ensure that NUMREQBUF is set with the
	  following formula as a minimum, to a maximum of 300:
	
	           (3 * <number of clients>) + (2 * <number of named-pipes>)
	
	  For large data transfers, MPX is normally used with OS/2 clients and RAW for
	  DOS clients. For MPX, it is important to have as many request buffers as
	  necessary to hold a 64K write (using the default, this is 16 request
	  buffers). To support RAW mode transfers, the server needs big-buffers; the
	  number of these that exist is controlled by the NUMBIGBUF keyword (at a
	  minimum, three should be specified if DOS clients exist on the network, even
	  if HPFS386 is being used).
	
	Additional query words: 2.00 2.10 2.10a 2.20
	
	======================================================================
	Keywords          :  
	
	=============================================================================
	

{% endraw %}
