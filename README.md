# lsf: Lion's Sectioned Format

LSF (Lion's Sectioned Format) is a plain-text container format.

## Installing on Python

    pip install lsf-lions-sectioned-format

## An Example LSF File

    title: My Blog
    date: 2021-01-20
    tags: blog
    
    This file contains all blog entries for my blog.
    Each section after the header section
    
    == 2021-01-17 ==
    tags: blogpost datepage github
    date: 2021-01-17
    
    Today, I put LSF on github.
    
    == 2021-01-06 ==
    tags: blogpost datepage news
    date: 2021-01-17
    
    Oh wow.

Logically, this document has three sections:
* a header section, with keys "`title`" and "`tags`", and containing body text "`This is my blog.`"
* a section titled "`2021-01-17`", also with keys and body.
* a section titled "`2021-01-06`", also with keys and body.

A blank space always segregates keys (which are optional) from body text (which is also optional).

The title line is always of the form "`== (title here) ==`", and is not optional for a section.

A header section is not required; If the first line matches the title pattern, there is no header section.


## Slightly More Formal Specification

    Document = Section? Titled-Section*
    
    Titled-Section = Title-Line Section
    
    Section = Keys-Block Empty-Line Body-Block
    
    Keys-Block = Key-Value-Line*
    
    Body-Block = Content-Line*
    
    Title-Line = "== " title " ==" (newline)
    
    Key-Value-Line = key ": " value (newline)
    
    Empty-Line = (newline)
    
    Content-Line = (any printable character)* (newline)
      (important: Content-Line may NOT be a Title-Line)


## Round-Tripping

LSF is intended to be for human-readable, human-editable text files.
Human-editable text files are often diff'ed before submission.

Therefore, it's important that when a computer program modifies an LSF document, that it introduces no changes further than what it needs to.
For this reason, I recommend that LSF parsers support round-tripping, if they are made to save LSF-structured data that originally was read from an LSF-structured document.
This way, only the required changes are made, and there is minimal disruption to (A) the user's chosen formatting, and (B) diff processing.

