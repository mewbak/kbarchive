---
layout: page
title: "Q235856: HOWTO: Read IBM 370 Data from a Binary File"
permalink: /kb/235/Q235856/
---

## Q235856: HOWTO: Read IBM 370 Data from a Binary File

{% raw %}

	Article: Q235856
	Product(s): Microsoft Visual Basic for Windows
	Version(s): 1.0,1.1,2.0,4.0,5.0,6.0,7.0
	Operating System(s): 
	Keyword(s): kbAccess kbDatabase KbVBA kbVBp400 kbVBp500 kbVBp600 kbGrpDSVBDB
	Last Modified: 05-JUN-2001
	
	-------------------------------------------------------------------------------
	The information in this article applies to:
	
	- Microsoft Visual Basic Standard Edition, 32-bit, for Windows, version 4.0 
	- Microsoft Visual Basic Professional Edition, 16-bit, for Windows, version 4.0 
	- Microsoft Visual Basic Professional Edition, 32-bit, for Windows, version 4.0 
	- Microsoft Visual Basic Enterprise Edition, 16-bit, for Windows, version 4.0 
	- Microsoft Visual Basic Enterprise Edition, 32-bit, for Windows, version 4.0 
	- Microsoft Visual Basic Learning Edition for Windows, versions 5.0, 6.0 
	- Microsoft Visual Basic Professional Edition for Windows, versions 5.0, 6.0 
	- Microsoft Visual Basic Enterprise Edition for Windows, versions 5.0, 6.0 
	- Microsoft Visual Basic for Applications versions 5.0, 6.0 
	-------------------------------------------------------------------------------
	
	SUMMARY
	=======
	
	When you use the VBA Get statement to read binary data generated on an IBM 370
	(or compatible) mainframe into a structure, the data comes out garbled. There
	are three problems:
	
	1. The text is in EBCDIC encoding.
	
	2. The 2-byte and 4-byte integers have the order of their bytes reversed.
	3. The 4-byte and 8-byte floating point numbers not only have their bytes
	  reversed, but also have a different internal structure.
	
	This article addresses the second and third issues. For EBCDIC to ASCII text
	translation, please see the following Microsoft Knowledge Base article:
	
	  Q216399 HOWTO: Convert Between ASCII and EBCDIC Character Codes
	
	Other binary or BCD numeric formats are not addressed.
	
	MORE INFORMATION
	================
	
	Integer Conversions
	-------------------
	
	The 2-byte and 4-byte integer format is identical to the Integer and Long data
	types in Visual Basic except that the order of the bytes is reversed. Thus, an
	integer with the hexadecimal value of A47C in Visual Basic would be stored as
	7CA4. The following routines swap the order of bytes in a 2-byte and 4-byte
	integer. These routines take advantage of the LSet statement, which allows
	assignment of data between different structures as long as the sizes are
	identical:
	
	  Private Type MungeInteger
	    Value As Integer
	  End Type
	
	  Private Type MungeLong
	    Value As Long
	  End Type
	
	  Private Type Munge2Bytes
	    Bytes(0 To 1) As Byte
	  End Type
	
	  Private Type Munge4Bytes
	    Bytes(0 To 3) As Byte
	  End Type
	
	  Private Sub SwapBytes(B() As Byte)
	  '
	  ' Reverses the order of the bytes in the array.
	  '
	  Dim I As Long, Temp As Byte, Offset As Long
	    Offset = LBound(B) + UBound(B)
	    For I = LBound(B) To UBound(B) \ 2
	      Temp = B(I)
	      B(I) = B(Offset - I)
	      B(Offset - I) = Temp
	    Next I
	  End Sub
	
	  Public Function IBMToVBAInteger(ByVal IBM_Value As Integer) As Integer
	  '
	  ' Converts an Integer in IBM 370 format to IEEE format
	  ' by reversing the order of the bytes.
	  '
	  Dim iTemp As MungeInteger, bTemp As Munge2Bytes
	    iTemp.Value = IBM_Value
	    LSet bTemp = iTemp
	    SwapBytes bTemp.Bytes
	    LSet iTemp = bTemp
	    IBMToVBAInteger = iTemp.Value
	  End Function
	
	  Public Function IBMToVBALong(ByVal IBM_Value As Long) As Long
	  '
	  ' Converts a Long in IBM 370 format to IEEE format
	  ' by reversing the order of the bytes.
	  '
	  Dim lTemp As MungeLong, bTemp As Munge4Bytes
	    lTemp.Value = IBM_Value
	    LSet bTemp = lTemp
	    SwapBytes bTemp.Bytes
	    LSet lTemp = bTemp
	    IBMToVBALong = lTemp.Value
	  End Function
	
	After you get your data, you can pass the fields through the IBMToVBAInteger and
	IBMToVBALong functions to perform the conversions.
	
	IBM 370 and IEEE Floating Point Formats
	---------------------------------------
	
	The IBM 4-byte and 8-byte floating point formats are identical except that the
	8-byte floating point number has an additional 32 bits in the mantissa. For this
	reason, the 4-byte floating point format is sometimes referred to as a truncated
	floating point number. The IBM 370 floating point format is as follows:
	
	+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
	| Bits                                    | Description                                                                                                                                                                                  | 
	+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
	| 0                                       | The Sign bit. 0 for positive numbers; 1 for negative numbers.                                                                                                                                | 
	+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
	| 1-7                                     | The Exponent. This is stored in excess 64 format, which means the number range 0-127 means an exponent value of -64 to +63. The exponent is base 16.                                         | 
	+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
	| 8-31 (4-byte) or
	       8-63 (8-byte). | The Mantissa. This is a fractional value between 0.0625 and 0.999..., which is multiplied by 16^Exponent to give the value of the number. If all 32 or 64 bits are zero, the number is zero. | 
	+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
	
	The IEEE floating point is as follows:
	
	+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
	| Bits                                     | Description                                                                                                                                                                                                                                                                    | 
	+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
	| 0                                        | The Sign bit. 0 for positive numbers; 1 for negative numbers.                                                                                                                                                                                                                  | 
	+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
	| 1-8 (4-byte) or
	       1-11 (8-byte)    | The Exponent. This is stored in excess 127 format (4-byte) or excess 1023 format(8-byte), which means the number range 0-255 (or 0-2047) means an exponent value of -127 to +128 (or -1023 to +1024). The exponent is base 2.                                                  | 
	+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
	| 9-31 (4-byte) or
	       12-63 (8-byte). | The Mantissa. This is a fractional value between 0.0 and 0.999... The number 1 is added to this fraction, giving a value in the range 1.0 to 1.999..., which is multiplied by 2^Exponent to give the value of the number. If all 32 or 64 bits are 0, then the number is zero. | 
	+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
	
	Floating Point Conversion
	-------------------------
	
	The conversion routine for floating point numbers involves the following steps:
	
	1. Extract the value of the Sign bit and the Exponent bits.
	2. Convert the Exponent value from IBM format to IEEE format:
	  1. Subtract 64 to remove the "Excess 64" offset.
	  2. Multiply by 4 since it is base 16 and IEEE numbers use base 2.
	  3. Subtract 1 because IEEE mantissa is in the range 1 to 2 rather than 0.5 to
	     1.
	
	3. Because the exponent is base 16 in the IBM format, the mantissa may have high
	  order bits with a value of 0. The IEEE format does not allow for this in
	  normalized numbers, so you have to shift the mantissa left and decrement the
	  exponent until the highest bit is a 1. Low order bits are filled with 0.
	4. Add 127 or 1023 to 4-byte and 8-byte Exponent values respectively to add the
	  IEEE offset.
	5. Place the Sign and Exponent bits back in the number.
	6. Reverse the order of the bytes.
	
	The following routines build on the code for swapping bytes given earlier in the
	article:
	
	  Private Type MungeSingle
	    A As Single
	  End Type
	
	  Private Type MungeDouble
	    A As Double
	  End Type
	
	  Private Type Munge8Bytes
	    B(0 To 7) As Byte
	  End Type
	
	  Public Function IBMToVBASingle(ByVal IBM_Value As Single) As Single
	  '
	  ' Converts a Single in IBM 370 format to IEEE format.
	  '
	  Dim sTemp As MungeSingle, bTemp As Munge4Bytes
	    sTemp.Value = IBM_Value
	    LSet bTemp = sTemp
	    IBM370_To_IEEE bTemp.Bytes
	    SwapBytes bTemp.Bytes
	    LSet sTemp = bTemp
	    IBMToVBASingle = sTemp.Value
	  End Function
	
	  Public Function IBMToVBADouble(ByVal IBM_Value As Double) As Double
	  '
	  ' Converts a Double in IBM 370 format to IEEE format
	  '
	  Dim dTemp As MungeDouble, bTemp As Munge8Bytes
	    dTemp.Value = IBM_Value
	    LSet bTemp = dTemp
	    IBM370_To_IEEE bTemp.Bytes
	    SwapBytes bTemp.Bytes
	    LSet dTemp = bTemp
	    IBMToVBADouble = dTemp.Value
	  End Function
	
	  Private Sub ShiftLeft(B() As Byte)
	  '
	  ' Shifts all bits in the array 1 to the Left.
	  ' Doesn't shift B(0) because it doesn't contain the mantissa.
	  '
	  Dim I As Long, MaxItem As Long, NewCarry As Long, OldCarry As Long
	    MaxItem = UBound(B)
	    For I = MaxItem To 1 Step -1
	      NewCarry = B(I) And &H80
	      B(I) = (B(I) And &H7F) * 2 + IIf(OldCarry, 1, 0)
	      OldCarry = NewCarry
	    Next I
	  End Sub
	
	  Private Sub ShiftRight(B() As Byte)
	  '
	  ' Shifts all bits in the array 1 to the Right.
	  ' Doesn't shift B(0) because it doesn't contain the mantissa.
	  '
	  Dim I As Long, MaxItem As Long, NewCarry As Long, OldCarry As Long
	    MaxItem = UBound(B)
	    For I = 1 To MaxItem
	      NewCarry = B(I) And 1
	      B(I) = (B(I) And &HFE) \ 2 + IIf(OldCarry, &H80, 0)
	      OldCarry = NewCarry
	    Next I
	  End Sub
	
	  Private Sub IBM370_To_IEEE(B() As Byte)
	  '
	  ' This routine is the heart of the conversion.
	  '
	  Dim Sign As Long, Exponent As Long, I As Long, Temp As Long
	  '
	  ' Extract sign.
	  '
	    Sign = B(0) And &H80
	  '
	  ' Extract exponent.
	  '
	    Exponent = ((B(0) And &H7F) - 64) * 4 - 1
	  '
	  ' Normalize the mantissa.
	  '
	    Do While (B(1) And &H80) = 0 And I < 4  ' 4 since 4 bits per hex digit
	      ShiftLeft B
	      I = I + 1
	      Exponent = Exponent - 1
	    Loop
	  '
	  ' Zero check.
	  '
	    If I = 4 Then
	      B(0) = 0      ' rest of bytes are 0 so output -> 0.0
	  '
	  ' Put sign and exponent back in 4-byte number.
	  '
	    ElseIf UBound(B) = 3 Then
	      Exponent = Exponent + 127     ' Excess 127 offset
	      If (Exponent And 1) = 1 Then  ' low bit goes into B(1)
	        B(1) = B(1) Or &H80
	      Else
	        B(1) = B(1) And &H7F
	      End If
	      B(0) = Sign Or ((Exponent \ 2) And &H7F)
	    Else
	  '
	  ' Put sign and mantissa back in 8-byte number.
	  '
	      ShiftRight B                  ' make room for longer exponent
	      ShiftRight B
	      ShiftRight B
	      Exponent = Exponent + 1023    ' Excess 1023 format
	      Temp = Exponent And &HF       ' Low 4 bits go into B(1)
	      B(1) = (B(1) And &HF) Or Temp * 16
	      B(0) = Sign Or ((Exponent \ 16) And &H7F)
	    End If
	  End Sub
	
	Additional query words:
	
	======================================================================
	Keywords          : kbAccess kbDatabase KbVBA kbVBp400 kbVBp500 kbVBp600 kbGrpDSVBDB 
	Technology        : kbVBSearch kbAudDeveloper kbZNotKeyword6 kbZNotKeyword2 kbVB500Search kbVB600Search kbVBA600Search kbVBA500 kbVBA600 kbVB500 kbVB600 kbVB400Search kbVB400 kbVBASearch kbZNotKeyword3 kbVB16bitSearch
	Version           : :1.0,1.1,2.0,4.0,5.0,6.0,7.0
	Issue type        : kbhowto
	
	=============================================================================
	

{% endraw %}
