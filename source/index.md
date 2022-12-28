-----------------------------------------------------------------------------
github  : https://github.com/casualwriter/casual-markdown 
title   : Casual-Markdown 
menu    :    
  Supported Syntax: md-syntax.md
  md-as-Doc       : md-as-doc.md
  md-as-Page      : md-as-page.md
  md-as-Blog      : md-as-blog.md
  <img src='sunset.svg' width=16>  : javascript:darkmode()
  <img src='home.svg' width=16>    : index.md
-----------------------------------------------------------------------------
<style>
  .markdown   { max-width:900px; margin:auto }
  #header     { background: linear-gradient(to bottom right, #06c, #fc0) } 
  #left-panel { background: linear-gradient(to bottom right, #eee, #888) }  
  h1, h2      { border-bottom:1px solid grey }
  h2, h3, h4  { color:#06c }  
</style>

## {{ title }} 

[casual-markdown]({{github}}) is lightweight RegExp-based markdown parser, with TOC, scroll spy and front-matter support.

It revises from simple-markdown-parser of [Powerpage Markdown Document](https://github.com/casualwriter/powerpage-md-document) 
for the following features

* simple, super lightweight (less than 190 lines)
* vanilla javascript, no dependence
* all browsers supported (IE9+, Chrome, Firfox, Brave, etc..)
* straight-forward coding style, hopefully readable.
* support [basic+enhanced syntax](https://casualwriter.github.io/casual-markdown/casual-markdown-syntax.html) according [Basic Markdown Syntax (markdownguide.org)](https://www.markdownguide.org/basic-syntax/)  
* TOC and scroll-spy support
* highlight comments/keywords in code-block
* front-matter for simple YAML
* extendable (by override md.before, md.after, md.formatCode, md.formatYAML)


### Usage Guide

just simply include [casual-markdown.js](https://github.com/casualwriter/casual-markdown/blob/main/source/casual-markdown.js) from CDN or local.  

~~~ 
<link rel="stylesheet" href="https://cdn.jsdelivr.net/gh/casualwriter/casual-markdown/dist/casual-markdown.css">
<script src="https://cdn.jsdelivr.net/gh/casualwriter/casual-markdown/dist/casual-markdown.js"></script>
~~~ 

or github-page (may specify version no)

~~~ 
<link rel="stylesheet" href="https://casualwriter.github.io/dist/casual-markdown@0.90.css">
<script src="https://casualwriter.github.io/dist/casual-markdown@0.90.js"></script>
~~~ 

or may download `casual-markdown.js, casual-markdown.css` and include them locally.


### Basic Usage

Once include the javascript library, casual-markdown object `md` is available with below functions.

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


### Advanced Usage

#### TOC from special elements

TOC may retrieve heading from special TAG elements. ``e.g. tag <section>``. 

md.toc() retrieve content from selected tags, using tag name as className. So remember provide additional #toc class to show it nice in TOC dialog.

~~~
// render TOC from tag:section, and H3, H4
md.toc( 'content', 'toc', { css: 'section,h3,h4' } )

// remember provide style class for TOC tag, normally set position for left margin
var style = document.createElement('style');
style.innerHTML = '#toc .SECTION { margin-left:2em }
document.head.appendChild(style);
~~~

#### Activate scrollspy feature

To activate the scrollspy feature, just pass element-ID of scroll content as below.

~~~
// activate scrollspy. normally is same as md-content, but sometime is document body.
md.toc( 'content', 'toc', { css: 'h2,h3,h4', scrollspy:'content' } )

// sometimes scroll content is document body.
md.toc( 'content', 'toc', { css: 'h3,h4,h5', scrollspy:'body' } )
~~~

#### Code-block formatter

Code-block keywords will be highlighted, they are hard-code in function md.formatCode(). 
If do want to highlight different keywords, please revise or override original function md.formatCode(). 

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

#### Extend Parser for enhanced syntax

to parse every markdown-block, dummy function md.before() and md.after() will be called 
(i.e. ``md.after( md.parser( md.before(mdText) ) )``). 

They can be re-defined for enhanced syntax. for example,

~~~
// original code in casual-markdown.js
var md = { before: function (str) {return str}, after: function (str) {return str} }

// re-define for extend syntax. e.g. $text$  => <strong>text</strong>
md.before = function (str) { 
   return mdstr = mdstr.replace(/\$(\w.*?[^\\])\$/gm, '<strong>$1</strong>')
}   

// re-define for extend syntax. e.g. $$text$$  => <b>text</b>
md.after = function (str) { 
   return mdstr = mdstr.replace(/\$\$(\w.*?[^\\])\$\$/gm, '<b>$1</b>')
}   

document.getElementById('content').innerHTML = md.html()
~~~

### Frontmatter for simple YAML

Support front-matter for simple YAML, only support string value (with 2 level ) meanwhile.

Front-matter start with `---` (at least three) in first line of markdown document, for example

```
-----------------------------------------------------------------------------
title   : Markdown-as-Page
style   : #header { background: RoyalBlue }
menu    :    
  Home            : index.md
  Supported Syntax: md-syntax.md
  md-as-Doc       : md-as-doc.md
  md-as-Page      : md-as-page.md
  md-as-Blog      : md-as-blog.md
  [DarkMode]      : javascript:darkmode() 
-----------------------------------------------------------------------------

## {{ title }}  

....
```

After called md.html(), js program may refer these values by `md.yaml[name]` (i.e. md.yaml = { title:'Markdown-as-Page', .... }) 
and html string with ``{{ name }}`` will be replaced with related values
                                               

### Applications

* Markdown-as-Document: https://github.com/casualwriter/casual-markdown-doc 
* Markdown-as-WebPage: https://github.com/casualwriter/casual-markdown-page   
* Markdown-as-Blog: https://github.com/casualwriter/casual-markdown-blog (not ready yet!)


### Update History

* 2022/07/19, v0.80, initial release.
* 2022/07/21, v0.82, refine toc/scrollspy, add dummy function for extension
* 2022/07/22, v0.85, front-matter for simple YAML
* 2022/07/31, v0.90, refine front-matter. code casual-markdown-doc.js, casual-markdown-page.html

<noscript>casual-markdown, casualwriter, javascript, html, regexp</noscript>

