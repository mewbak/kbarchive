---
layout: page
title: "Q299520: How to Determine the Cipher Suite for the Server and Client"
permalink: /kb/299/Q299520/
---

## Q299520: How to Determine the Cipher Suite for the Server and Client

{% raw %}

	Article: Q299520
	Product(s): Internet Information Server
	Version(s): 5.0
	Operating System(s): 
	Keyword(s): kbgrpdsvckbfaq
	Last Modified: 28-JUN-2001
	
	-------------------------------------------------------------------------------
	The information in this article applies to:
	
	- Microsoft Internet Information Services version 5.0 
	-------------------------------------------------------------------------------
	
	SUMMARY
	=======
	
	This article helps you to determine which cipher suite is negotiated during a
	secure channel (https) connection between a client and a Web server. "Cipher
	suite" is the technical protocol term that describes the type, size, and methods
	that are used when data (plaintext) is turned into "cipher text", or encrypted
	data.
	
	MORE INFORMATION
	================
	
	To determine the cipher suite the server and client agree on, you need to be
	familiar with the Secure Sockets Layer (SSL) 2.0 and 3.0 specifications and the
	Transport Layer Security (TLS) 1.0 protocol. TLS 1.0 is basically the latest
	version of SSL 3.0 and is discussed in this article. For more details on SSL
	2.0, SSL 3.0 and additional details on TLS 1.0, see the "References" section.
	
	The following sample trace, taken from a Network Monitor trace, is used to
	demonstrate how to determine the ciphersuite that is being used in a secure
	communication.
	
	TCP: Data: Number of data bytes remaining = 1456 (0x05B0)
	00000030                    16 03 00 12 F5 02 00 00 46 03       ........F.
	00000040  00 B1 4F 08 36 74 E4 77 3A C9 8C 0C AA 71 48 0F ..O.6t.w:....qH.
	00000050  49 0B 58 5A 79 53 49 31 6E 00 42 8C E9 EF 06 C4 I.XZySI1n.B.....
	00000060  0D 20 03 00 00 00 1B EB EE 0C 7D 21 65 FA EA 27 ..........}!e..'
	00000070  51 EA 1D A3 5A BB 00 E9 42 AF 30 2B E3 1A 23 8F Q...Z...B.0+..#.
	00000080  89 CC 00 64 00 0B 00 06 4B 00 06 48 00 06 45 30 ...d....K..H..E0
	
	Use 0x16 03 00 as the start of a TLS handshake record. The rest of the analysis
	is as follows:
	
	Starting offset 0x36
	
	- 16 - This suggests that this is an SSL handshake record.
	- 03 00 - This is the protocol version. This example shows SSL 3.0. (NOTE: TLS
	  1.0 is 03 01)
	- 12 f5 - This is the length of this handshake record.
	- 02 - This indicates that this is a server hello message.
	- 00 00 46 - This is the length of this server hello message.
	- 03 00 - This is the protocol version again.
	- The next 0x20 bytes are called the "server random".
	- 20 - This is the length of session id.
	- The next 0x20 bytes contain the session ID.
	- 00 64 - This identifies the cipher suite that you are attempting to identify.
	  After you have this value, you can compare it with the table below. For
	  example, 0x0064 = TLS_RSA_EXPORT1024_WITH_RC4_56_SHA.
	
	The following is a list of the most common cipher suites used by TLS 1.0:
	
	NOTE: For common cipher suites used by SSL 2.0 and 3.0, see the "References"
	section.
	
	TLS_NULL_WITH_NULL_NULL = { 0x00,0x00 }
	
	NOTE: TLS_NULL_WITH_NULL_NULL is specified and is the initial state of a TLS
	connection during the first handshake on that channel, but must not be
	negotiated, because it provides no more protection than an unsecured
	connection.
	
	TLS_RSA_WITH_NULL_MD5 = { 0x00,0x01 }
	TLS_RSA_WITH_NULL_SHA = { 0x00,0x02 }
	TLS_RSA_EXPORT_WITH_RC4_40_MD5 = { 0x00,0x03 }
	TLS_RSA_WITH_RC4_128_MD5 = { 0x00,0x04 }
	TLS_RSA_WITH_RC4_128_SHA = { 0x00,0x05 }
	TLS_RSA_EXPORT_WITH_RC2_CBC_40_MD5 = { 0x00,0x06 }
	TLS_RSA_WITH_IDEA_CBC_SHA = { 0x00,0x07 }
	TLS_RSA_EXPORT_WITH_DES40_CBC_SHA = { 0x00,0x08 }
	TLS_RSA_WITH_DES_CBC_SHA = { 0x00,0x09 }
	TLS_RSA_WITH_3DES_EDE_CBC_SHA = { 0x00,0x0A }
	TLS_RSA_EXPORT1024_WITH_DES_CBC_SHA = { 0x00,0x62 }
	TLS_RSA_EXPORT1024_WITH_RC4_56_SHA = { 0x00,0x64 }
	
	TLS_DH_DSS_EXPORT_WITH_DES40_CBC_SHA = { 0x00,0x0B }
	TLS_DH_DSS_WITH_DES_CBC_SHA = { 0x00,0x0C }
	TLS_DH_DSS_WITH_3DES_EDE_CBC_SHA = { 0x00,0x0D }
	TLS_DH_RSA_EXPORT_WITH_DES40_CBC_SHA = { 0x00,0x0E }
	TLS_DH_RSA_WITH_DES_CBC_SHA = { 0x00,0x0F }
	TLS_DH_RSA_WITH_3DES_EDE_CBC_SHA = { 0x00,0x10 }
	TLS_DHE_DSS_EXPORT_WITH_DES40_CBC_SHA = { 0x00,0x11 }
	TLS_DHE_DSS_WITH_DES_CBC_SHA = { 0x00,0x12 }
	TLS_DHE_DSS_WITH_3DES_EDE_CBC_SHA = { 0x00,0x13 }
	TLS_DHE_RSA_EXPORT_WITH_DES40_CBC_SHA = { 0x00,0x14 }
	TLS_DHE_RSA_WITH_DES_CBC_SHA = { 0x00,0x15 }
	TLS_DHE_RSA_WITH_3DES_EDE_CBC_SHA = { 0x00,0x16 }
	TLS_DHE_DSS_EXPORT1024_WITH_DES_CBC_SHA= { 0x00,0x63 }
	TLS_DHE_DSS_EXPORT1024_WITH_RC4_56_SHA = { 0x00,0x65 }
	TLS_DHE_DSS_WITH_RC4_128_SHA = { 0x00,0x66 }
	TLS_DHE_DSS_WITH_NULL_SHA = { 0x00,0x67 }
	
	TLS_DH_anon_EXPORT_WITH_RC4_40_MD5 = { 0x00,0x17 }
	TLS_DH_anon_WITH_RC4_128_MD5 = { 0x00,0x18 }
	TLS_DH_anon_EXPORT_WITH_DES40_CBC_SHA = { 0x00,0x19 }
	TLS_DH_anon_WITH_DES_CBC_SHA = { 0x00,0x1A }
	TLS_DH_anon_WITH_3DES_EDE_CBC_SHA = { 0x00,0x1B }
	
	NOTE: All cipher suites whose first byte is 0xFF are considered private and can
	be used for defining local and experimental algorithms. Interoperability of such
	types is a local matter.
	
	REFERENCES
	==========
	
	For more information on the TLS specification, see the following Web site:
	
	  http://www.ietf.org/rfc/rfc2246.txt
	
	NOTE: See Appendex A.5 for cipher suite descriptions.
	
	For more information on the SSL2 specification, see the following Web site:
	
	  http://home.netscape.com/eng/security/SSL_2.html
	
	NOTE: See Appendix C for cipher suite descriptions.
	
	For more information on the SSL 3.0 specification, see the following Web site:
	
	  http://home.netscape.com/eng/ssl3/draft302.txt
	
	NOTE: See Appendix A.6 for cipher suite descriptions.
	
	Additional query words:
	
	======================================================================
	Keywords          : kbgrpdsvc kbfaq
	Technology        : kbiisSearch kbiis500
	Version           : :5.0
	
	=============================================================================
	

{% endraw %}
