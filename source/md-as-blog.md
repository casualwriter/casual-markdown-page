-----------------------------------------------------------------------------
github  : https://github.com/casualwriter/casual-markdown 
title   : Markdown-as-Blog
style   : #header { background: linear-gradient(to bottom right, #06c, #fc0); }
menu    :    
  Home            : index.md
  Supported Syntax: md-syntax.md
  md-as-Doc       : md-as-doc.md
  md-as-Page      : md-as-page.md
  md-as-Blog      : md-as-blog.md
  [DarkMode]      : javascript:darkmode() 
-----------------------------------------------------------------------------

## {{ title }} (to-be-released..)

Casual-Markdown provide a simple solution to build blog site by markdown files.

1. write blog by markdown (e.g. 20220720-use-markdown-for-blog.md)
2. config site at index.md (title, logo, menu, category, style)
3. update blog index at index.md

### Sample Site 

* [Casual-Markdown Sample Blog](./blog)
* [Casualwriter's Blog](../blog)

### Usage Guide

simply put [casual-md-blog.html](https://github.com/casualwriter/casual-markdown/blob/main/source/casual-md-blog.html) 
in web server (sometimes, rename to `index.html` if like) 

* config site at index.md (title, logo, menu, category, style)
* update blog index at index.md
                                          
belwo is index.md for [Casual-Markdown Sample Blog](./blog)
 
~~~  
-----------------------------------------------------------------------------
github  : https://github.com/casualwriter/casual-markdown 
title   : Casual-Markdown Sample Blogs 
style   : #header { background: linear-gradient(to bottom right, #06c, #fc0); }
menu    : 
  Search  : .
  List    : .
  About   : about.md
-----------------------------------------------------------------------------
   
## Highlight

- 2021/10/20: [simple markdown parser](20211020-simple-markdown-parser.md) ![](pp-web-crawler.jpg)
- 2022/07/30: [frontmatter for simple YAML](20220730-frontmatter.md)

### July 2022
                    
* 2022/07/30: [frontmatter for simple YAML](20220730-frontmatter.md) {#markdown,#regexp,@pp-web-crawler.jpg}
* 2022/07/22: [release casual-markdown v0.85](20220722-casual-markdown-v0.85.md) {#markdown,#regexp,@pp-web-crawler.jpg}
* 2022/07/19: [about table-of-content](20220719-table-of-content.md) {#markdown,#regexp,@pp-web-crawler.jpg}

### Oct 2021

* 2021/10/20: [simple markdown parser](20211020-simple-markdown-parser.md) {#markdown,#regexp,@image.jpg}

~~~ 


### Modification History

* todo: code casual-md-blog.html for basic blogs site
* todo: more customized options
 