-----------------------------------------------------------------------------
title   : Markdown-as-Blog
style   : #header { background: linear-gradient(to bottom right, #06c, #fc0); }
menu    :    
  Supported Syntax: md-syntax.md
  md-as-Doc       : md-as-doc.md
  md-as-Page      : md-as-page.md
  <img src='sunset.svg' width=16>  : javascript:darkmode()
  <img src='home.svg' width=16>    : index.md
  <img src='github.svg' width=16>  : https://github.com/casualwriter/casual-markdown-blog
-----------------------------------------------------------------------------
<style>
  .markdown   { max-width:900px; margin:auto }
  #header     { background: linear-gradient(to bottom right, #06c, #fc0) } 
  #left-panel { background: linear-gradient(to bottom right, #eee, #888) }  
  h1, h2      { border-bottom:1px solid grey }
  h2, h3, h4  { color:#06c }  
</style>

## casual-markdown-blog

Build blog site by markdown files and single [index.html](source/index.html). 

What we need is config home page at [index.md](https://raw.githubusercontent.com/casualwriter/casual-markdown-blog/main/source/index.md), then start write post in markdown!

It is very handy to build simple blog-site from markdown files, and host on static web hosting. For example, 

* Self-host on github: https://raw.githack.com/casualwriter/casual-markdown-blog/main/source/index.html
* Casual-Markdown's Blog: https://casualwriter.github.io/casual-markdown/blog
* Dark theme: https://casualwriter.github.io/casual-markdown/blog?theme=dark
* Dark (always): https://casualwriter.github.io/casual-markdown/blog?home=index-dark.md
* Nav at right-side: https://casualwriter.github.io/casual-markdown/blog?home=index-right.md 

### Features

* single html
* no dependence in vanilla javascript
* support all browser
* dark mode or dark theme
* responsive, support mobile
* customized theme (by css style)

### Usage Guide

simply copy [index.html](https://github.com/casualwriter/casual-markdown-page/blob/main/source/index.html) to web server, or fork this repo. 

* config site at index.md (title, subtitle, header-color, navigation, etc..)
* start to write blog post using markdown
* to publish, just add the post in index.md by syntax 

~~~
* yyyy/mm/dd: [post-title](md-file) { #tags }
~~~

index.md is also shown as HOME page of blog site. 

below is sample setup from [Sample Blog: index.md](https://raw.githubusercontent.com/casualwriter/casual-markdown-blog/main/source/index.md)

~~~  
--------------------------------------------------------------------------
title      : Casual-Markdown's Blog 
subtitle   : Simple is the best
nav-group  : featured, new-3, tags, months
nav-width  : 320px
css-header : background:linear-gradient(to bottom right, #06c, #fc0); color:white
menu       : 
   Home    : ?
   Github  : https://github.com/casualwriter/casual-markdown-blog
   Dark    : javascript:darkmode()
   About   : ?page=about.md
--------------------------------------------------------------------------

<style comment="additional style">
......
</style>

<div id="md-post">

home page in markdown syntax...

## Archive

* yyyy/mm/dd: [Post Title](md file)  { #tag1, #tag2 }
* yyyy/mm/dd: [Post Title](md file)  { #tag1, #tag2 }
...
* yyyy/mm/dd: [Post Title](md file)  { #tag1, #tag2 }

</div>
~~~ 

### frontmatter for blog setup

* `title` := blog title
* `subtitle` := subtitle
* `nav-group` := featured // show blogs tagged by `featured`
* `nav-group` := new-n    // show new posts (n=number of new post)
* `nav-group` := tags     // show tags list
* `nav-group` := months   // show archive by month
* `nav-width` := 320px    // width of nav-panel
* `css-header` := background:green   // css style for header
* `theme` := dark        // show by dark theme (only dark theme available now)
* `menu` :=  ...         // top-menu 

### URL Parameters

* `index.html?post={md-post.md}`  show post of md-post.md 
* `index.html?tag={tag-name}`  list posts for specified tag
* `index.html?month=2022-08`  list posts for specified month
* `index.html?theme=dark`  show in dark theme
* `index.html?home=index-dark.md`  show blog site using index-dark.md as home/index
* `index.html?home=my-blog.md&theme=dark&pos=post01.md` show post01.md using my-blog.md in dark mode.

### Notes

* [alt-k] to toggle dark mode
* [alt-s] to view in html code (for developer)
* [ctrl-p] to print post
* in mobile mode (width<900), click on title to toggle nav panel

### History

* 2022/08/24: 0.60, first release
* to-do, more themes
