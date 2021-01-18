# lsf: Lion's Sectioned Format

LSF (Lion's Sectioned Format) is a plain-text container format.

It features:
* a header section,
* unlimited content sections,
* titles for content sections,
* tags for all sections,
* body text for each section,
* UTF-8 encoding.


## Example LSF File

> title: My Blog
> tags: blog
> 
> This is my blog.
>
> == 2021-01-17 ==
> tags: blogpost datepage github
> date: 2021-01-17
>
> Today, I put LSF on github.
>
> == 2021-01-06 ==
> tags: blogpost datepage news
> date: 2021-01-17
>
> Oh wow.

Logically, this document has three sections:
* a header section, tagged with keys "title" and "tags", and containing body text "This is my blog."
* a section titled "2021-01-17", also with tags and body.
* a section titled "2021-01-06", also with tags and body.

A blank space always segregates tags from body text, or, alternatively, the title line of the next section.

The title line is always of the form "== (title here) ==".

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
> (important: Content-Line may NOT be a Title-Line)


## Round-Tripping

LSF is intended to be for human-readable, human-editable text files.
Human-editable text files are often diff'ed before submission.

Therefore, it's important that when a computer program modifies an LSF document, that it introduces no changes further than what it needs to.
For this reason, I recommend that LSF parsers support round-tripping, if they are made to save LSF-structured data that originally was read from an LSF-structured document.
This way, only the required changes are made, and there is minimal disruption to (A) the user's chosen formatting, and (B) diff processing.

