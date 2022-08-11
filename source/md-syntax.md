-----------------------------------------------------------------------------
github  : https://github.com/casualwriter/casual-markdown 
title   : Supported Syntax of Casual-Markdown 
menu    :    
  Home            : index.md
  Supported Syntax: md-syntax.md
  md-as-Doc       : md-as-doc.md
  md-as-Page      : md-as-page.md
  md-as-Blog      : md-as-blog.md
  [DarkMode]      : javascript:darkmode()
-----------------------------------------------------------------------------

## Introduction

[Casual Markdown](https://github.com/casualwriter/casual-markdown) is a super lightweight RegExp-based markdown parser, 
with TOC and scrollspy features

It revises from simple-markdown-parser of [Powerpage Markdown Document](https://github.com/casualwriter/powerpage-md-document) 
for the following features

* simple, super lightweight (less than 180 lines)
* vanilla javascript, no dependance
* support all browsers (IE9+, Chrome, Firefox, Brave, etc..)
* straight-forward coding style, hopefully readable.
* support [basic syntax](#markdown-syntax) according [Basic Markdown Syntax (markdownguide.org)](https://www.markdownguide.org/basic-syntax/)  
* support subset of [extended-syntax](#enhanced-syntax)
* table-of-content (TOC) and scrollspy support
* auto highlight comment and keyword in code-block
* extendable (by override md.before, md.after, md.formatCode)
* frontmatter for simple YAML

### Usage

just simply include [casual-markdown.js](https://github.com/casualwriter/casual-markdown/blob/main/source/casual-markdown.js) 
 from local or CDN.  


CDN, jsdelivr

~~~ 
<link rel="stylesheet" href="https://cdn.jsdelivr.net/gh/casualwriter/casual-markdown/dist/casual-markdown.css">
<script src="https://cdn.jsdelivr.net/gh/casualwriter/casual-markdown/dist/casual-markdown.js"></script>
~~~ 

or github-page (may specify version no)

~~~ 
<link rel="stylesheet" href="https://casualwriter.github.io/dist/casual-markdown@0.85.css">
<script src="https://casualwriter.github.io/dist/casual-markdown@0.85.js"></script>
~~~

Then may call markdown-parser by md.html(), or TOC by md.toc()

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



## Supported Markdown Syntax {markdown-syntax} 
 
[casual-markdown](https://github.com/casualwriter/casual-markdown) parser support 
[Basic Markdown Syntax](https://www.markdownguide.org/basic-syntax/ "new") with some advanced featurens. 

Please refer the following samples.  

### Heading 

<table border=1><tr><th width=30%>Markdown<th width=35%>HTML<th width=35%>Rendered Layout</tr>
<tr><td>
~~~
may add multiple # in right side.  
following with {id} to specify id

# heading 1 {no-toc-1}
## heading 2 {no-toc-2} ##
### heading 3 {no-toc-3} ####
#### heading 4  {no-toc-4} #######
##### heading 5 {id=five}
~~~
<td><xmp>
# heading 1 {no-toc-1}
## heading 2 {no-toc-2} ##
### heading 3 {no-toc-3} ####
#### heading 4  {no-toc-4} #######
##### heading 5 {id=five}
</xmp>
<td>
# heading 1 {no-toc-1}
## heading 2 {no-toc-2} ##
### heading 3 {no-toc-3} ####
#### heading 4  {no-toc-4} #######
##### heading 5 {id=five}
</td></tr></table>
 
### Text Decoratoin (Bold/Italic)

<table border=1><tr><th width=30%>Markdown<th width=35%>HTML<th width=35%>Rendered Layout</tr>
<tr><td>
~~~
**basic decoration**

this is ***bold+italic*** sample  
this is **bold** sample  
this is *italic* sample  
this is ___bold+italic___ sample  
this is __underline__ sample  
  
**enhance syntax**  
* ~~Strikethrough~~ sample
* ~~delete~~ then ^^insert^^
* ^^^mark text^^^

**disable decoration**
* disable \*\*bold\*\* by esc\  
* disable \*italic\* by esc\  
* disable by following ** with space*  
* not support _italic_ !!
~~~
<td><xmp>
**basic decoration**

this is ***bold+italic*** sample  
this is **bold** sample  
this is *italic* sample  
this is ___bold+italic___ sample  
this is __underline__ sample  
  
**enhance syntax**  
* ~~Strikethrough~~ sample
* ~~delete~~ then ^^insert^^
* ^^^mark text^^^

**disable decoration**
* disable \*\*bold\*\* by esc\  
* disable \*italic\* by esc\  
* disable by following ** with space*  
* not support _italic_ !!
</xmp>
<td>
**basic decoration**

this is ***bold+italic*** sample  
this is **bold** sample  
this is *italic* sample  
this is ___bold+italic___ sample  
this is __underline__ sample  
  
**enhance syntax**  
* ~~Strikethrough~~ sample
* ~~delete~~ then ^^insert^^
* ^^^mark text^^^

**disable decoration**
* disable \*\*bold\*\* by esc\  
* disable \*italic\* by esc\  
* disable by following ** with space*  
* not support _italic_ !!
</td></tr></table>


### Paragraph, Line Breaks and HR

<table border=1><tr><th width=35%>Markdown<th width=40%>HTML<th>Rendered Layout</tr>
<tr><td>
~~~
Empty will be considered as paragraph.

Don't put tabs or spaces in front of your paragraphs.

Line break will be added     
if line wne with 2+ space  
~~~
<td><xmp>
Empty will be considered as paragraph.

Don't put tabs or spaces in front of your paragraphs.

Line break will be added     
if line wne with 2+ space  
</xmp>
<td>
Empty will be considered as paragraph.

Don't put tabs or spaces in front of your paragraphs.

Line break will be added     
if line wne with 2+ space  
</td></tr><tr><td>
~~~
Use - or _ or * for horizontal rule.

--------
________
********
~~~
<td><xmp>
Use - or _ or * for horizontal rule.

--------
________
********
</xmp>
<td>
Use - or _ or * for horizontal rule.

--------
________
********
</td>
</tr></table>
 
### Blockquote and Code (same line)

<table border=1><tr><th>Markdown<th>HTML<th>Rendered Layout</tr>
<tr><td>
~~~
> blockquote line1
> blockquote line2
>> blockquote line3
>> blockquote line4
> Below is empty line
>         
> line 5

single quote in same line may allow `<b>decoration</b> text` 
  
double quote in same line will show ``RAW `<u>text</u>`` include single quote
~~~
<td><xmp>
> blockquote line1
> blockquote line2
>> blockquote line3
>> blockquote line4
> Below is empty line
>         
> line 5

single quote in same line may allow `<b>decoration</b> text` 
  
double quote in same line will show ``RAW `<u>text</u>`` include single quote
</xmp>
<td>
> blockquote line1
> blockquote line2
>> blockquote line3
>> blockquote line4
> Below is empty line
>         
> line 5

single quote in same line may allow `<b>decoration</b> text` 
  
double quote in same line will show ``RAW `<u>text</u>`` include single quote
</td></tr></table>


### Code-Block  (Multiple lines)

* use **three** ``\~ or \` `` to define code-block.
* may define language or title using ``\~\~\~ {language or title}``
* ``comment and keyword`` will be highlighted in code-block if language is specified.

~~~ javascript
  //===== format code-block, highlight remarks/keywords for code/sql
  md.formatCode = function (match, title, block) {
    // convert tag <> to &lt; &gt;
    block = block.replace(/</g,'&lt;').replace(/\>/g,'&gt;').replace(/\t/g,'   ')
    
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


* will highlight SQL keyword if language=sql

~~~ sql
-- show department staffs
select dept_code, grade, staff_id, staff_name
 from dept
 where dept_code = 'IT'
~~~

 
 



### Lists (Ordered and unordered)

<table border=1><tr><th>Markdown<th>HTML<th>Rendered Layout</tr>
<tr><td>
~~~
use *|+|- for unorder list

* item 1
* item 2
* item 3
~~~
<td><xmp>
use *|+|- for unorder list

* item 1
* item 2
* item 3
</xmp><td>
use *|+|- for unorder list

* item 1
* item 2
* item 3
</td></tr>
<tr><td>
~~~
use number [0-9] with dot for ordered list.

1. one 
1. two
0. three
4. Four
~~~
<td><xmp>
use number [0-9] with dot for ordered list.

1. one 
1. two
0. three
4. Four
</xmp>
<td>
use number [0-9] with dot for ordered list.

1. one 
1. two
0. three
4. Four
</td></tr>
<tr><td>
~~~
indent for nested list, 
max 2 level, level 1 
should be unordered list

* colors
  + red
  + green
  + blue
* numbers
  1. one
  2. two
  
* languages
  0. javascript
  0. python
  0. c, c++
* OS
  - Windows
  - Linux
  - macOS
~~~
<td><xmp>
indent for nested list, 
max 2 level, level 1 
should be unordered list

* colors
  + red
  + green
  + blue
* numbers
  1. one
  2. two
  
* languages
  0. javascript
  0. python
  0. c, c++
* OS
  - Windows
  - Linux
  - macOS
</xmp>
<td>
indent for nested list, 
max 2 level, level 1 
should be unordered list

* colors
  + red
  + green
  + blue
* numbers
  1. one
  2. two
  
* languages
  0. javascript
  0. python
  0. c, c++
* OS
  - Windows
  - Linux
  - macOS
</td></tr>
</table>

 
### Links and Images

<table border=1 width=980px><tr><th>Markdown<th>HTML</tr>
<tr><td>
~~~
* Link to [google](https://google.com)
* Link with title [youtube](https://youtube.com "google")
* Link in new tab [google](https://google.com "new")
* quick link: <https://youtube.com> 
* direct link: https://youtube.com   
* link as text [https://youtube.com]() 

* Show Image 
  ![Powerpage Document](pp-web-crawler.jpg)
       
* Show Image with options (width=380px or style="width:70%")

  ![Powerpage Document](powerpage.gif "width=500px")
       
  ![Powerpage Document](pp-md-editor.jpg "style='width:75%;border:1px solid red'")     
~~~

<td><xmp>
* Link to [google](https://google.com)
* Link with title [youtube](https://youtube.com "google")
* Link in new tab [google](https://google.com "new")
* quick link: <https://youtube.com> 
* direct link: https://youtube.com   
* link as text [https://youtube.com]() 

* Show Image 
  ![Powerpage Document](pp-web-crawler.jpg)
       
* Show Image with options (width=380px or style="width:70%")

  ![Powerpage Document](powerpage.gif "width=500px")
       
  ![Powerpage Document](pp-md-editor.jpg "style='width:75%;border:1px solid red'")     
</xmp></td>
</tr></table>

 **Rendered Layout**

* Link to [google](https://google.com)
* Link with title [youtube](https://youtube.com "google")
* Link in new tab [google](https://google.com "new")
* quick link: <https://youtube.com> 
* direct link: https://youtube.com   
* link as text [https://youtube.com]() 

* Show Image 
  ![Powerpage Document](pp-web-crawler.jpg)
       
* Show Image with options (width=380px or style="width:70%")

  ![Powerpage Document](powerpage.gif "width=500px")
       
  ![Powerpage Document](pp-md-editor.jpg "style='width:75%;border:1px solid red'")     
  
   
### Escaping Characters


<table border=1><tr><th>Markdown<th>HTML<th>Rendered Layout</tr>
<tr><td>
~~~
\` \~ \_ \* \+ \- \. \^   
\\ \< \> \( \) \[ \]  
~~~
<td><xmp>
\` \~ \_ \* \+ \- \. \^   
\\ \< \> \( \) \[ \]  
</xmp>
<td>
\` \~ \_ \* \+ \- \. \^   
\\ \< \> \( \) \[ \]  
</td>
</tr></table>
 

### Tables

below is a typical table 

~~~
 header1 | Header2 | Header3 
---------|---------|--------
 row1,c1 | row1, c2 | row1, c3 
 r2,col1 | r2,col2 | r2,col3 
 row3,col1 | row3,col2 | row3,col3 
| row4,col1 | row4,col2 | row4,col3 |
| row5,col1 | row5,col2 | also ok  
 also ok  | row6,col2 | row6,col3 |
~~~

the render output like below

 header1 | Header2 | Header3 
---------|---------|--------
 row1,c1 | row1, c2 | row1, c3 
 r2,col1 | r2,col2 | r2,col3 
 row3,col1 | row3,col2 | row3,col3 
| row4,col1 | row4,col2 | row4,col3 |
| row5,col1 | row5,col2 | also ok  
 also ok  | row6,col2 | row6,col3 |

### Enhanced Syntax  {enhanced-syntax}

The following enhanced syntax are support by the [casual-markdown](https://github.com/casualwriter/casual-markdown) parser.

however, be aware compatibility issue if document will be parsed by other parser (e.g. github)

* Specify ID for Header. ie. ``\n## header {id} [#*]`` => ``<h2 id={id}>header</h2>``
* Specify title for Code-Block. ie. ``\n~\~\~ {title}\n{code-block}\n~\~\~`` => ``<pre title={title}><code\>{code-block}</code\></pre>``
* Highlight keyword within code-block based on title. ie. ``\n~\~\~ sql\n{sql scripts}\n~\~\~`` to highlight keyword of SQL

* link as text. ie. `[link]\()` => ``<a href={link}>{link}</a>``
* text as link for url. ie. ``<https://{url}>`` => ``<a href="https://{url}">https://{url}</a>``   
* Open link in new page. i.e.  ``[text]\(url "new")`` => ``<a href="url" target=_new>text</a>`` 
* Specify title for Link i.e.  ``[text]\(url "title")`` => ``<a href="url" title="title">text</a>``  
* Specify property for image. ie. `![title]\(image "{width=400px,etc..}")`
* table support (if second line likes `\-\-|\-\-`)

* __Underline__ by `_\_Underline_\_` => `<u>text</u>`  
* ~~Strikethrough~~ by `~\~Strikethrough~\~` => ``<del>text</del>`
* ^^highlight^^ by `^\^highlight^\^` => ``<ins>text</ins>``
* ^^^mark text^^^ by `^\^\^highlight^\^\^` => ``<mark>text</mark>``, ^^^supported within code-block^^^
* Escaping Characters `` \` \~ \_ \* \+ \- \. \^ \\ &lt; &gt; \( \) \[ \] ``
    
### Frontmatter for simple YAML

Support frontmatter for simple YAML, only support string value at first level (i.e. key = value) 

Frontmatter start with `---` (at least three) in first line of markdown document, for example

```
-----------------------------------------------------------------------------
github  : https://github.com/casualwriter/casual-markdown 
title   : Casual-Markdown 
toc     : leftspy
menu    :    
  Syntax       : cmd-syntax.md
  cmd-Document : cmd-document.md
  cmd-Blog     : cmd-blog.md
-----------------------------------------------------------------------------

## ^^^{{ title }}^^^

[casual-markdown](^^^{{github}}^^^) is a super lightweight RegExp-based markdown parser, with TOC and scrollspy support

```

After called md.html(), js program may refer these values by `md.yaml[name]` (i.e. md.yaml = { title:'Casual Markdown', toc:'leftspy', .... }) 
and html string with ``{{ name }}`` will be replaced with related values

    
## Notes

### Modification History

* 2021/10/06, v0.50, initial version
* 2021/10/09, v0.60, add scrollspy feature
* 2021/10/11, v0.63, rewrite code-block, highlight remarks and keywords 
* 2021/10/12, v0.64, support table syntax 
* 2021/10/20, v0.66, minor fixes. support nested unordered list. 
* 2022/07/18, v0.70, refine table syntax
* 2022/07/19, v0.80, toc support with scrollspy
* 2022/07/21, v0.82, refine toc/scrollspy, add md.before(), md.after()
* 2022/07/22, v0.85, frontmatter for simple YAML
* 2022/07/31, v0.90, support indent YAML, use md file for https://casualwriter.github.io/casual-markdown/
 
### To-Do

- [v] some enhance synatx (underline,Strikethrough,highlight)
- [v] some enhance synatx (link as tex, header id, image property)
- [v] enhance code-block
- [v] support table syntax
- [v] toc with scrollspy support
- [v] simple frontmatter :=  ---\n Name: value \n--- 
- [.] use Frontmatter for markdown-document
- [.] use Frontmatter for markdown-blog-site 
- [ ] use Frontmatter for markdown-application 
