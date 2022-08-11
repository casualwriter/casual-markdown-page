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

[casual-markdown]({{github}}) is a super lightweight RegExp-based markdown parser, with TOC and scrollspy support

It revises from simple-markdown-parser of [Powerpage Markdown Document](https://github.com/casualwriter/powerpage-md-document) 
for the following features

* simple, super lightweight (less than 180 lines)
* vanilla javascript, no dependance
* support all browsers (IE9+, Chrome, Firfox, Brave, etc..)
* straight-forward coding style, hopefully readable.
* support [basic syntax](https://casualwriter.github.io/casual-markdown/casual-markdown-syntax.html) according [Basic Markdown Syntax (markdownguide.org)](https://www.markdownguide.org/basic-syntax/)  
* support subset of [extended-syntax](https://casualwrit=
* extendable (by override md.before, md.after, md.formatCode)


### Usage Guide

just simply include [casual-markdown.js](https://github.com/casualwriter/casual-markdown/blob/main/source/casual-markdown.js) in web page, (from local or CDN).  

~~~ 
<link rel="stylesheet" href="casual-markdown.css">
<script src="casual-markdown.js"></script>
~~~

or CDN

~~~ 
<link rel="stylesheet" href="https://cdn.jsdelivr.net/gh/casualwriter/casual-markdown/dist/casual-markdown.css">
<script src="https://cdn.jsdelivr.net/gh/casualwriter/casual-markdown/dist/casual-markdown.js"></script>
~~~ 

or github-page (with version)

~~~ 
<link rel="stylesheet" href="https://casualwriter.github.io/dist/casual-markdown@0.82.css">
<script src="https://casualwriter.github.io/dist/casual-markdown@0.82.js"></script>
~~~ 


#### Usage

Once include the javascript library, markdown parser object `md` is available with below functions.

* `md.html(mdString)` - convert markdown string into html
* `md.toc( mdElement, tocElement, options)` - generate TOC html to tocElement
* default TOC option := { title:'Table of Contents', css:'h1,h2,h3,h4', scrollspy:null }

for example

~~~
// get markdown source from element
var mdText = document.getElementById('source').innerHTML

// parse markdown, and render content
document.getElementById('content').innerHTML = md.html( mdText )

// render TOC, add scrollspy to document.body
md.toc( 'content', 'toc', { css:'h2,h3,h4', title:'Table of Contents', scrollspy:'body' } )

// render TOC, title=Index, add scrollspy to <div id=content>
md.toc( 'content', 'toc', { title:'Index', scrollspy:'content' } )
~~~


#### Advanced Usage

**Code-block formatter**

code-block keywords are hard-code in function md.formatCode(). 
If do want to highlight different keywords, please override original function md.formatCode() showing below. 

~~~
//===== format code-block, highlight remarks/keywords for code/sql
md.formatCode = function (match, title, block) {
  // convert tag <> to &lt; &gt; tab to 3 space, support mark code using ^^^
  block = block.replace(/</g,'&lt;').replace(/\>/g,'&gt;')
  block = block.replace(/\t/g,'   ').replace(/\^\^\^(.+?)\^\^\^/g, '<mark>$1</mark>')
  
  // highlight comment and keyword based on title := none | sql | code
  if (title.toLowerCase(title) == 'sql') {
    block = block.replace(/^\-\-(.*)/gm,'<rem>--$1</rem>').replace(/\s\-\-(.*)/gm,' <rem>--$1</rem>')   
    block = block.replace(/(\s)(function|procedure|return|if|then|else|end|loop|while|or|and|case|when)(\s)/gim,'$1<b>$2</b>$3')
    block = block.replace(/(\s)(select|update|delete|insert|create|from|where|group by|having|set)(\s)/gim,'$1<b>$2</b>$3')
  } else if ((title||'none')!=='none') {
    block = block.replace(/^\/\/(.*)/gm,'<rem>//$1</rem>').replace(/\s\/\/(.*)/gm,' <rem>//$1</rem>')   
    block = block.replace(/(\s)(function|procedure|return|if|then|else|end|loop|while|or|and|case|when)(\s)/gim,'$1<b>$2</b>$3')
    block = block.replace(/(\s)(var|let|const|for|next|do|while|loop|continue|break|switch|try|catch|finally)(\s)/gim,'$1<b>$2</b>$3')
  }
  return '<pre title="' + title + '"><code>'  + block + '</code></pre>'
}
~~~

**Extend Parser for enhanced syntax**

to parse every markdown-block, dummy function md.before() and md.after() will be called 
(i.e. ``md.after( md.parser( md.before(mdText) ) )``). They can be re-defined for enhanced syntax

~~~
// original code
var md = { before: function (str) {return str}, after: function (str) {return str} }

// re-define for extend syntax. e.g. $text$  => <strong>text</strong>
md.before = function (str) { 
   return mdstr = mdstr.replace(/\$(\w.*?[^\\])\$/gm, '<strong>$1</strong>')
}   

// re-define for extend syntax. e.g. $$text$$  => <b>text</b>
md.after = function (str) { 
   return mdstr = mdstr.replace(/\$\$(\w.*?[^\\])\$\$/gm, '<b>$1</b>')
}   
~~~


### Applications

* casual-md-page.html?file={md-file}  // show markdown as web-page
* casual-md-blog.html  // blogging by markdown
* casual-md-doc.js     // document by markdown


### Modification History

* 2022/07/19, v0.80, initial release.
* 2022/07/22, v0.85, refine toc/scrollspy, extend function, and simple yaml
* 2022/07/31, v0.90, refine frontmatter for indent yaml; code casual-md-page.html
 