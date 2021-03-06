---
layout: page
title: "Q155199: WD97: How to Create Two-Page Numbering Schemes in One Document"
permalink: /kb/155/Q155199/
---

## Q155199: WD97: How to Create Two-Page Numbering Schemes in One Document

{% raw %}

	Article: Q155199
	Product(s): Word 97 for Windows
	Version(s): WINDOWS:97
	Operating System(s): 
	Keyword(s): kbprint kbfield word97 kbPrinting
	Last Modified: 07-SEP-2001
	
	-------------------------------------------------------------------------------
	The information in this article applies to:
	
	- Microsoft Word 97 for Windows 
	-------------------------------------------------------------------------------
	
	
	SUMMARY
	=======
	
	Word does not provide a built-in method for applying two different page
	numbering schemes in one document. This article describes how to create one page
	numbering scheme for the entire document and another scheme for each section of
	the document.
	
	For example, a 10-page document has three sections with the following number of
	pages in each section:
	
	4 pages in section 1 (physical pages 1-4)
	2 pages in section 2 (physical pages 5-6)
	4 pages in section 3 (physical pages 7-10)
	
	Using the method below, you can create two-page numbering schemes to look like
	the following:
	
	The header will display the numbering scheme of:
	
	  <Page Number> of <Total Number of Pages in Section>
	
	The footer will display the numbering scheme of:
	
	  <total number of pages in the document>
	
	So, on page 3 of section 1 (the third physical page of the total document), the
	header will display Page 3 of 4 and the footer will display 3. On page 2 of
	section 3 (the eighth physical page of the total document), the header will
	display Page 2 of 4 and the footer will display 8.
	
	MORE INFORMATION
	================
	
	NOTE: This process assumes that you have a document with multiple sections, and
	that you are familiar with inserting field codes.
	
	To create a numbering scheme that uses consecutive numbering throughout the
	document and a second numbering scheme that numbers each section beginning at 1,
	use either method below:
	
	Method 1: Use SEQ Fields
	------------------------
	
	1. Place the following two field codes on the first page of the document:
	
	  {SEQ variable1 \h \r {SectionPages} }
	
	  {SEQ variable2 \h \r0}
	
	  NOTE: the \r is followed by the number zero, not the letter "O".
	
	2. Place the following field codes at the beginning of each section after the
	  first section:
	
	  {SEQ variable2 \h \r {={SEQ variable1 \c} } }
	
	  {SEQ variable1 \h \r {={SectionPages}+{SEQ variable2 \c} } }
	
	3. Position your insertion point at the top of the document and on the View
	  menu, click Header And Footer.
	
	4. In the Header, position your insertion point where you want the page number,
	  type the word "Page" (without the quotation marks) and a space, and then
	  click the Insert Page Number button on the Header And Footer toolbar.
	
	5. On the Insert menu, click Page Numbers, and then click Format.
	
	6. Under Page Numbering, click Start At (1 should appear in the Start At box),
	  and then click OK twice.
	
	7. Position the insertion point after the Page field, type " of " (without the
	  quotation marks, and including the spaces before and after the word "of"),
	  and on the Insert menu, click Field. Under Categories, click (All). Under
	  Field Names, click SectionPages, and then click OK.
	
	8. Click Show Next on the Header and Footer toolbar. (Note: you should see
	  Header-Section 2 in the header area of the document.) On the Insert menu,
	  click Page Numbers, and then click Format. Under Page Numbering, click Start
	  At (1 should appear in the Start At box), and then click OK twice.
	
	9. Repeat step 8 for each section of your document.
	
	10. Click Show Previous on the Header And Footer toolbar until it displays
	  Header-Section 1 in the Header section of the document. Click the Switch
	  Between Header and Footer icon on the Header and Footer toolbar. (Note: You
	  should see Footer Section 1 in the footer area of your document.)
	
	11. Place the following field code in the footer to show the page number of the
	  total number of pages in the document:
	
	  {={SEQ variable2 \c}+{Page} }
	
	12. Click Close on the Header and Footer toolbar.
	
	The sequence fields include the \h switch which formats the fields as hidden.
	Although you can display hidden text by clicking the Show/Hide button on the
	Standard toolbar, you should turn hidden text off before you print because
	hidden text affects page breaks and can result in incorrect page numbering.
	
	Method 2: Use PAGEREF Fields
	----------------------------
	
	To create the Header section numbering scheme, follow these steps:
	
	Page numbering starts at 1 for each section, and the PAGEREF field yields the
	number of pages in each section. Page numbering appears as "Page X of Y" on each
	page, where X is the current page in the current section, and Y is the number of
	pages in the current section. To do this, follow these steps:
	
	1. On the View menu, click Header and Footer.
	
	2. In Section 1, position your insertion point where you want the page number
	  and then click the Insert Page Number icon on the Header and Footer toolbar.
	
	3. On the Insert menu, click Page Numbers, and then click Format.
	
	4. Under Page Numbering, click Start At (1 should appear in the Start At box),
	  and then click OK twice, and then click Close on the Header and Footer
	  toolbar.
	
	5. Repeat the following instructions in each section of your document to insert
	  a bookmark at the end of the section:
	
	  a. Select some text at the end of the last page of the section.
	
	  b. On the Insert menu, click Bookmark.
	
	  c. Type a Bookmark Name, such as Sec1 for Section 1, and then click Add.
	
	6. On the View menu, click Header and Footer, and then follow these steps:
	
	  a. Starting at Section 1 of your document, position the insertion point after
	     the Page field that you inserted in step 2, and then type " of " (without
	     the quotation marks, and including the spaces before and after the word
	     "of")
	
	  b. On the Insert menu, click Field. Under Categories, click (All). Under
	     Field Names, click PAGEREF, click Options, click the Bookmarks tab, select
	     the name of the bookmark you inserted to mark the end of the current
	     section, and then click Add To Field.
	
	  c. Click OK twice.
	
	  d. Click Show Next on the Header and Footer toolbar. (Note: you should see
	     Header-Section 2 in the header area of the document.) If Same As Previous
	     is turned on (you will see the words Same As Previous on the right side of
	     the dotted line surrounding the header or footer), click the Same As
	     Previous button on the Header and Footer toolbar. The words Same As
	     Previous will disappear from the right side of the dotted line surrounding
	     the header or footer. Also, on the Insert menu, click Page Numbers, and
	     then click Format. Under Page Numbering, click Start At (1 should appear
	     in the Start At box), and then click OK twice.
	
	  e. If your field codes are not turned on, press ALT+F9 to turn then on. With
	     field codes turned on, the following code will appear:
	
	  {PAGE} of {PAGEREF BookmarkName \* MERGEFORMAT}
	
	     where BookmarkName is the name of the bookmark you inserted in step 5.
	
	  f. Change the BookmarkName within the PAGEREF field to the name of the
	     bookmark for the respective Section.
	
	  g. Repeat steps d and f for each section of your document.
	
	  h. Click Close on the Header and Footer toolbar.
	
	  Note: you may need to update the field (press F9) for it to appear correctly.
	
	To create the Footer numbering scheme, do the following:
	
	1. Position your insertion point at the top of the document and on the View
	  menu, click Header And Footer. Click the Switch Between Header and Footer
	  icon on the Header and Footer toolbar.
	
	2. In Section 1, click the Insert Page Number icon on the Header and Footer
	  toolbar.
	
	3. Click Show Next on the Header and Footer toolbar. (Note: you should see
	  Header-Section 2 in the header area of the document.) If Same As Previous is
	  turned on (you will see the words Same As Previous on the right side of the
	  dotted line surrounding the header or footer), click the Same As Previous
	  button on the Header and Footer toolbar. The words Same As Previous will
	  disappear from the right side of the dotted line surrounding the header or
	  footer.
	
	4. If your field codes are not turned on, press ALT+F9 to turn then on. With
	  field codes turned on, delete any {PAGE} field in the footer.
	
	5. Enter the following field into the Footer of Section 2:
	
	  {={PAGE} + {PAGEREF BookmarkName (section 1)}}
	
	  Note: The BookmarkName should be the PREVIOUS Section's BookmarkName.
	
	6. Click the Show Next button on the Header and Footer toolbar and then follow
	  these steps:
	
	  a. You should see Header-Section 3 in the header area of the document. If
	     Same As Previous is turned on (you will see the words Same As Previous on
	     the right side of the dotted line surrounding the header or footer), click
	     the Same As Previous button on the Header and Footer toolbar. The words
	     Same As Previous will disappear from the right side of the dotted line
	     surrounding the header or footer.
	
	  b. If your field codes are not turned on, press ALT+F9 to turn then on.
	
	  c. With field codes turned on, change the field to the following:
	
	  {={PAGE} + {PAGEREF BookmarkName (section 1)}
	  + {PAGEREF BookmarkName (section 2)}}
	
	7. Repeat step 6 for each section of your document.
	
	  Note: You will need to edit the field placed into the footer for each
	  additional section by adding the following to the end of the existing field
	  code between the two end braces ({}):
	
	  + {PAGEREF BookmarkName (previous section x)}
	
	  Note: x represents the PREVIOUS section number.
	
	  For example, Section 4 of our example would be:
	
	  {={PAGE} + {PAGEREF BookmarkName (section 1)}
	  + {PAGEREF BookmarkName (section 2)}
	  + {PAGEREF BookmarkName (section 3)}}
	
	8. Click Close on the Header and Footer toolbar.
	
	Additional query words: page number numbering two dual pattern different differing dissimilar multiple
	
	======================================================================
	Keywords          : kbprint kbfield word97 kbPrinting 
	Technology        : kbWordSearch kbWord97 kbWord97Search kbZNotKeyword2
	Version           : WINDOWS:97
	Issue type        : kbhowto kbinfo
	
	=============================================================================
	

{% endraw %}
