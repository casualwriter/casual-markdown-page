## casual-markdown-page

[Casual-Markdown-Page](https://github.com/casualwriter/casual-markdown-page) directly use markdown files as web page or web site.

Just a html file [index.html](source/inde.html) to load markdown file into web page by the syntax of `index.html?file={markdown-file.md}`

It is very handy to build simple web-site from markdown files, for example, 

* self-host:   https://raw.githack.com/casualwriter/casual-markdown-page/main/source
* github page: https://casualwriter.github.io/casual-markdown
* github page: https://casualwriter.github.io/powerpage


### Usage Guide

1. copy index.html to web server
2. copy index.md and other files (*.md) to the folder

**that's it!**

* by default, it will load `index.md` as home page.
* hotkey [alt-s] to show markdown html for developer
* hotkey [alt-k] to showpage in dark mode
* use frontmatter for page configuration (title, menu, navigation), for example

~~~
-----------------------------------------------------------------------------
github  : https://github.com/casualwriter/casual-markdown 
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

[casual-markdown]({{github}}) is a super lightweight RegExp-based markdown parser, 
with TOC and scrollspy support
~~~ 


### Modification History

* 2022/08/11, v0.60, initial release.
 