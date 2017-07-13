---
layout: page
title: Contribute - Customize the web page
nav: false
---

In order to edit the web page, you need [Jekyll](https://jekyllrb.com/) next to the associated [source code](TODO). The source files you want to edit are all written in Markdown (you can find a tutorial [here](https://github.com/adam-p/markdown-here/wiki/Markdown-Cheatsheet)). If you want functionality that goes beyond that, you'll need to use HTML code.  
If you want to add new pictures, please put them in the folder *pictures*.

Please keep in mind to always <span style="color:red">save the files in UTF8 format!</span>

## Edit the Developer Documentation
The developer documentation files are all located in the *developerdocumentation* folder. The only exception is the introduction file, which is located on the first level (*developerdocumentation.md*).

### Adapt existing documentation
If, for example, you want to edit the documentation for "Dummy-Seite 1", you open the corresponding file. You can find the exact filename (and path) in the address line of your browser - provided you are currently on the corresponding page (replace .html by .md). The corresponding file is in this case *dummy1.md*.

The file is structured as follows:

**Header** -- Don't touch. 
```
---
layout: page
title: Developer-Documentation
nav: false
---
```

**Sub-Navigation** -- Don't touch. 
```
---
[Introduction](/developerdocumentation.html) &nbsp;&nbsp; Dummy-Seite 1 &nbsp;&nbsp; [Dummy-Seite 2](dummy2.html) 

---
&nbsp;

```

**Content** -- This is the part you want to edit.
```
## Dummy-Seite 1

TODO [in english]
```
You might notice that the first heading is formatted as h2 (##). This is because of Jekyll -- h1 (#) is provided for the page title (defined in the header), and is not defined. You can use it anyway, but h1 headings appear like h3.


### Create new documentation
To create a new documentation page, create a new file. Please choose a concise, speaking name - all lower case - because the file name will be part of the link. Please save this file in the *developerdocumentation* folder. We now set "Dummy-Seite 3" (*dummy3.md*).

**Header** -- For a new developer documentation sub-page, please take the following:
```
---
layout: page
title: Developer-Documentation
nav: false
---
```
`---` is the delimiter of the header.  
`layout` is the layout of the page. Please always use "page" to keep the layout uniform.  
`title` is the title of the page. (We have decided to give sub-pages the title of the parent page.)  
`nav` determines whether the page should appear in the general navigation bar. Sub-pages should NEVER appear in the general navigation bar.

**Sub-Navigation** -- To switch between the sub-pages.  
The three hyphens in the first and second-to-last line produce continous lines. The blank line above the second line is mandatory. Otherwise, three dashes appear on the web page instead of a line. The code snippet in the last line is a protected space (HTML). Followed by an empty line (don't forget it!), it provides enough space between the sub-navigation and the following content.  
The sub-navigation itself consists of a link to the introduction, followed by the juxtaposed links to the different sub-pages. The individual links are separated by two protected spaces. The link to the page to which the current file belongs is replaced by a plain text.

Copy the sub-navigation from any other sub-page of the Developer documentation and edit it. Our new sub-navigation looks as follows:
```
---
[Introduction](/developerdocumentation.html) &nbsp;&nbsp; [Dummy-Seite 1](dummy1.html) &nbsp;&nbsp; [Dummy-Seite 2](dummy2.html) &nbsp;&nbsp; Dummy-Seite 3

---
&nbsp;

```
The entry to "Dummy-Seite 1" has changed (from plaintext to link) and the entry to "Dummy-Seite 3" (plaintext) has been added. The link to "Dummy-Seite 3" must be added in the in the sub-navigation of EVERY other sub-page AND the introduction page.

**Content** -- Here comes your content.
```
## Dummy-Seite 3

TODO [in english]
```
We remind you that the first heading must be formatted as h2 (##). In Jekyll, h1 (#) is provided for the page title (defined in the header), and is not defined. You can use it anyway, but h1 headings appear like h3.

## Edit / Create other content
The customization of other parts of the web page is similar to that of the developer documentation, with the restriction that these are to be written in **German**. 

### Editing (Sub) Pages:
* Please note new features on the start page (*index.md*).
* Customize the tutorials if the current ones don't work any more (because of changes to the program code). Try to keep them simple.
* Helpful or interesting links to the *Links* page.
* TODO Credits

### Creating New (Sub) Pages:
* If you want to submit sub-pages to a page that does not already have any, please create a subnavigation. 
* If the new page is to appear in the general navigation bar:
```
---
layout: page
title: New_Title
nav: true
order: 7
---
```
Set `nav` to `true` and add `order` at the end of the header, to specify at which point the page should appear (first = 1, second = 2, ...). If the new page should be inserted between already existing ones in the general navigation bar, adjust the counter for all those who are to follow it!
* New tutorials as sub-page of *Tutorials*; a brief description on the introductory page (*tutorials.md*).  
&nbsp;  
&nbsp;


---

&nbsp;

*Note: The files in the _layout folder should be .txt files. This is NOT a mistake, it is a bug. The format provided by Jekyll for the files in this folder (.hmtl) does not work! (At least at the time of construction of the website.)*
