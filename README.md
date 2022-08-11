## casual-markdown-page

[Casual-Markdown-Page](https://github.com/casualwriter/casual-markdown-page) directly use markdown files as web page or web site.

It is a single file [index.html](source/inde.html) which load markdown file into web page by the syntax of `index.html?file={markdown-file.md}`


### Usage Guide

1. copy index.html to web server
2. copy index.md and other files (*.md) to the folder

that's it!

### Sample Site

* self-host:   
* github page: https://casualwriter.github.io/casual-markdown
* github page: https://casualwriter.github.io/powerpage

## Markdown Page

markdown page use below frontmatter to setup web page component

~~~
-----------------------------------------------------------------------------
title   : Casual-Markdown 
menu    :    
  Home            : index.md
  Supported Syntax: md-syntax.md
  md-as-Doc       : md-as-doc.md
  md-as-Page      : md-as-page.md
  md-as-Blog      : md-as-blog.md
  [DarkMode]      : javascript:darkmode()
-----------------------------------------------------------------------------

## {{ title }} 

[casual-markdown]({{github}}) is a super lightweight RegExp-based markdown parser, with TOC and scrollspy support
~~~


### Modification History

* 2022/08/??, initial release.
 
