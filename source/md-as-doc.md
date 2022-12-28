-----------------------------------------------------------------------------
title   : Markdown-as-Document
menu    :    
  Supported Syntax: md-syntax.md
  md-as-Page      : md-as-page.md
  md-as-Blog      : md-as-blog.md
  <img src='sunset.svg' width=16>  : javascript:darkmode()
  <img src='home.svg' width=16>    : index.md
  <img src='github.svg' width=16>  : https://github.com/casualwriter/casual-markdown-doc
-----------------------------------------------------------------------------
<style>
  .markdown   { max-width:900px; margin:auto }
  #header     { background: linear-gradient(to bottom right, #06c, #fc0) } 
  #left-panel { background: linear-gradient(to bottom right, #eee, #888) }  
  h1, h2      { border-bottom:1px solid grey }
  h2, h3, h4  { color:#06c }  
</style>

## {{ title }} 

[Casual-Markdown-Doc](https://github.com/casualwriter/casual-markdown-doc) is a handy solution to use markdown as document.

just add below 4 lines in the beginning of html file, then start write document in markdown format!

~~~
<!DOCTYPE html>
<link  href="https://casualwriter.github.io/dist/casual-markdown-doc.css" rel="stylesheet">
<script src="https://casualwriter.github.io/dist/casual-markdown-doc.js"></script>
<body title="Supported Syntax of Casual-Markdown">

start write document in markdown format!
~~~

check the sample document at https://casualwriter.github.io/casual-markdown/casual-markdown-syntax.html

### Credit

This project based on the design idea of [Strapdown.js](https://strapdownjs.com/). 
but use [casual-markdown](https://github.com/casualwriter/casual-markdown) parser, 
build-in css, vanilla javascript without any dependence. (support all browsers include IE9) 

### Usage Guide

1. create document in html format. e.g. `casual-markdown-syntax.html` 
2. use below first 4 line as header, and start draft content in markdown format
3. at line 4, revise title to your document title
4. start draft document in markdown format

~~~
<!DOCTYPE html>
<link  href="https://casualwriter.github.io/dist/casual-markdown-doc.css" rel="stylesheet">
<script src="https://casualwriter.github.io/dist/casual-markdown-doc.js"></script>
<body title="Supported Syntax of Casual-Markdown">

## Heading

content in markdown format

~~~

or include `casual-markdown-doc.js` from local

~~~
<!DOCTYPE html>
<link  href="casual-markdown-doc.css" rel="stylesheet">
<script src="casual-markdown-doc.js"></script>
<body title="Supported Syntax of Casual-Markdown">

## Heading

content in markdown format
~~~

### Table of Content 

* table-of-content will be auto-generated from markdown heading
* hotkey [alt-t] to toggle table-of-content popup-box
* hotkey [ctrl-p] to print document, table-of-content will be inserted as first page automatically.
* if do not want table-of-content printout. please close TOC box first, then print document.

### How it works

The main program is very simple by doing the following steps.

1. read markdown content from ``<body>``
1. update document title 
2. call casual-markdown parse, convert to html and update to content area.
3. generate table-of-content with scrollspy feature.

~~~
//=============================================================================
// 20220719, convert markdown-document in <body> tag into HTML document
//=============================================================================
window.onload = function () {

  var html = '<div class="container" style="margin:auto; max-width:1024px; padding:4px;">'
  html += '<header id=heading>' + (document.body.title||document.title) + '</header>'
  html += '\n<div id=tocbox><button style="float:right" onclick="this.parentElement.style.display=\'none\'">'
  html += 'X</button><div id="toc"></div></div>' 
  html += '\n<div id=content>' + md.html(document.body.innerHTML.replace(/\&gt;/g,'>')) + '</div></div>'; 

  document.body.innerHTML = html
  document.body.style.display = 'block';

  md.toc( 'content', 'toc', { scrollspy:'body' } )
  
}
~~~


### Modification History

* 2022/08/02, v0.70, initial release.
 