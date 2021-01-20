# lsf

LSF (Lion's Sectioned Format) is a plain-text container format.

It features:
* header & content sections
* titles for all sections (except the header)
* tags for all sections
* body text for each section

LSF files are always UTF-8 encoded.

## An example LSF File

    title: My Blog
    tags: blog
    
    This is my blog.
    
    == 2021-01-20 ==
    tags: blogpost datepage github
    date: 2021-01-20
    
    Today I uploaded my lsf module to PyPI.
    
    == 2021-01-18 ==
    tags: blogpost datepage holiday
    date: 2021-02-10
    
    Today was Martin Luther King Day.

This file has a header section, and two content sections (2021-01-20, 2021-01-18).  All sections have tags and body text content.


# lsf-lions-own-sectioned-format

The "lsf-lions-own-sectioned-format" distribution package contains lsf.py, which reads and write LSF files.

## Example of Use

Here's reading an LSF file:

    import lsf
    
    L = lsf.loadfile("basic_blog.lsf")
    
    for section in L:
        print(section[lsf.TITLE])
        print("  " + section[lsf.KEYS].get("tags"))

And adding a section:

    lsf.append(L, "A Title", {"date": "2021-01-19", "tags": "test"}, "This is a new entry.")

And saving to the file:

    lsf.savefile(L, "basic_blog.lsf")


## Section Dictionaries

Each section has a dictionary of the form:

    {TITLE: "...a title...",
     KEYS: {"key1": "value 1", "key2": "value 2", ...},
     BODY: "Central\nBody\nText\n"}

...which corresponds to section:

    == ...a title... ==
    key1: value 1
    key2: value 2
    ...
    
    Central
    Body
    Text
    

It's safe to manipulate data in place.
