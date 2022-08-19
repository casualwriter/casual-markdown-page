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

Build blog site by markdown files. 

1. write blog by markdown (e.g. 20220728-use-markdown-for-blog.md)
2. config site at index.md (title, logo, menu, category, style)
3. update blog index at index.md

### Sample Site 

* [Casual-Markdown Sample Blog](https://casualwriter.github.io/casual-markdown/blog)
* [Casualwriter's Blog](https://casualwriter.github.io/blog)

### Usage Guide

simply put copy [index.html](https://github.com/casualwriter/casual-markdown-page/blob/main/source/index.html) 
or all-in-one version [index-one.html](https://github.com/casualwriter/casual-markdown-page/blob/main/source/index-one.html) 
to web server. 

* config site at index.md (title, logo, menu, category, style)
* update blog index at index.md, 
* start write post in markdown. (e.g. 20220818-all-you-need-is-markdown.md)
                                          
below is index.md for [Casual-Markdown Sample Blog](./blog)
 
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
   
### Aug 2022
                    
* 2022/08/19: [markdown is all you need for blogging](20220819-markdown-is-all-need.md) { @image.jpg, #markdown, #blog }
* 2022/08/10: [is regexp readable?](20220810-is-regexp-readable.md) { @image.jpg, #regexp, #web-dev }
* 2022/08/03: [my dream web browser](20220803-my-dream-web-browser.md) { @image.jpg, #web, #dev }

### July 2022
                    
* 2022/07/30: [frontmatter for simple YAML](20220730-frontmatter.md) { @pp-web-crawler.jpg, #markdown, #regexp }
* 2022/07/22: [release casual-markdown v0.85](20220722-casual-markdown-v0.85.md) {#on-top, #markdown, #regexp, @pp-web-crawler.jpg }

### Oct 2021

* 2021/10/20: [code a markdown editor within 80 lines](20211020-code-markdown-editor.md) { #powerpage, #markdown }
* 2021/07/20: [crawl web page by powerpage-web-crawler](20210720-powerpage-web-crawler.md) { #powerpage, @image.jpg }
* 2021/06/18: [develop html/css/jsavscript application by PowerPage](20210618-html-app-by-powerpage.md) { #on-top, #powerpage, @image.jpg }

~~~ 


### To-Do

* todo: code casual-markdown-blog.html for basic blogs site
* todo: more customized options
 
