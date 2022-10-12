# HTML 规范

## DOCTYPE 声明

一个DOCTYPE必须包含以下部分，并严格按照顺序出现：

```
A string that is an ASCII case-insensitive match for the string <!DOCTYPE.
One or more space characters.
A string that is an ASCII case-insensitive match for the string html.
Optionally, a DOCTYPE legacy string or an obsolete permitted DOCTYPE string (defined below).
Zero or more space characters.
A > (U+003E) character.
```

- 一个ASCII字符串 `<!DOCTYPE` ，大小写不敏感
- 一个或多个空白字符
- 一个ASCII字符串`html`，大小写不敏感
- 一个可选的历史遗留的`DOCTYPE`字符串 （`DOCTYPE legacy string`），或者一个可选的已过时但被允许的`DOCTYPE`字符串 （`obsolete permitted DOCTYPE string`） 字符串
- 一个或多个空白字符
- 一个编码为 U+003E 的字符 `>`

#### 团队约定

HTML文件必须加上 DOCTYPE 声明，并统一使用 HTML5 的文档声明：

```html
<!DOCTYPE html>
```

启用 IE Edge 模式。

```html
<meta http-equiv="X-UA-Compatible" content="IE=Edge">
```

更多关于 DOCTYPE声明
[The DOCTYPE](https://www.w3.org/TR/2014/REC-html5-20141028/syntax.html#the-doctype)


## 页面语言LANG

Lang属性的取值应该遵循互联网工程任务组–IETF（The Internet Engineering Task Force）制定的关于语言标签的文档 [BCP 47 - Tags for Identifying Languages](http://tools.ietf.org/html/bcp47)

推荐使用属性值 cmn-Hans-CN（简体, 中国大陆），但是考虑浏览器和操作系统的兼容性，目前仍然使用 zh-CN 属性值

```html
<html lang="zh-CN">
```

更多地区语言参考：

```html
zh-SG 中文 (简体, 新加坡)   对应 cmn-Hans-SG 普通话 (简体, 新加坡)
zh-HK 中文 (繁体, 香港)     对应 cmn-Hant-HK 普通话 (繁体, 香港)
zh-MO 中文 (繁体, 澳门)     对应 cmn-Hant-MO 普通话 (繁体, 澳门)
zh-TW 中文 (繁体, 台湾)     对应 cmn-Hant-TW 普通话 (繁体, 台湾)
```

已废弃不推荐使用的 Languages Tags

以下写法已于 2009 年废弃，请勿使用（cmn、wuu、yue、gan 等已由 2005 年的 extlang 升级到 2009 年的 language）：

```html
zh-cmn, zh-cmn-Hans, zh-cmn-Hant, zh-wuu, zh-yue, zh-gan
```

以下写法已于 2009 年废弃，不推荐使用：

```html
zh-Hans, zh-Hans-CN, zh-Hans-SG, zh-Hans-HK, zh-Hans-MO, zh-Hans-TW, 
zh-Hant, zh-Hant-CN, zh-Hant-SG, zh-Hant-HK, zh-Hant-MO, zh-Hant-TW
```

更多已废弃 Languages Tags 参考 [IANA Language Subtag Registry](http://www.iana.org/assignments/language-subtag-registry/language-subtag-registry) 里面的 “Type: redundant“”

更多关于 Languages Tags ：
[W3C Language tags in HTML and XML](https://www.w3.org/International/articles/language-tags/)

[网页头部的声明应该是用 lang=”zh” 还是 lang=”zh-cn”？](https://www.zhihu.com/question/20797118?utm_source=weibo&utm_medium=weibo_share&utm_content=share_question&utm_campaign=share_sidebar)


## 页面编码

```html
Because the character sets in ISO-8859 was limited in size, and not compatible in multilingual environments, the Unicode Consortium developed the Unicode Standard.

The Unicode Standard covers (almost) all the characters, punctuations, and symbols in the world.

Unicode enables processing, storage, and transport of text independent of platform and language.

The default character encoding in HTML-5 is UTF-8.
```

因为 ISO-8859 中字符集大小是有限的，且在多语言环境中不兼容，所以 Unicode 联盟开发了 Unicode 标准。

Unicode 标准覆盖了（几乎）所有的字符、标点符号和符号。

Unicode 使文本的处理、存储和运输，独立于平台和语言。

HTML-5 中默认的字符编码是 UTF-8

参阅 [HTML Unicode (UTF-8) Reference](http://www.w3schools.com/charsets/ref_html_utf8.asp)

一般情况下统一使用 “UTF-8” 编码
```html
<meta charset="UTF-8">
```

由于历史原因，有些业务可能会使用 “GBK” 编码

```html
<meta charset="UTF-8">
```

请尽量统一写成标准的 “UTF-8”，不要写成 “utf-8” 或 “utf8” 或 “UTF8”。根据 IETF对UTF-8的定义，其编码标准的写法是 “UTF-8”；而 UTF8 或 utf8 的写法只是出现在某些编程系统中，如 .NET framework 的类 System.Text.Encoding 中的一个属性名就叫 UTF8。

更多关于

UTF-8写法: [UTF8 or UTF-8?](https://stackoverflow.com/questions/809620/utf8-or-utf-8)

GBK：[Application of IANA Charset Registration for GBK](http://www.ietf.org/assignments/charset-reg/GBK)

Charset：[character-encoding-declaration](http://www.w3.org/TR/html5/document-metadata.html#character-encoding-declaration)


## 元素及标签闭合

HTML元素共有以下5种：

- 空元素：`area`、`base`、`br`、`col`、`command`、`embed`、`hr`、`img`、`input`、`keygen`、`link`、`meta`、`param`、`source`、`track`、`wbr`
- 原始文本元素：`script`、`style`
- RCDATA元素：`textarea`、`title`
- 外来元素：来自`MathML`命名空间和`SVG`命名空间的元素。
- 常规元素：其他`HTML`允许的元素都称为常规元素。

元素标签的闭合应遵循以下原则：

```html
Tags are used to delimit the start and end of elements in the markup. 
Raw text, escapable raw text, and normal elements have a start tag to indicate where they begin, and an end tag to indicate where they end. 
The start and end tags of certain normal elements can be omitted, as described below in the section on optional tags. 
Those that cannot be omitted must not be omitted. Void elements only have a start tag; end tags must not be specified for void elements.
Foreign elements must either have a start tag and an end tag,
or a start tag that is marked as self-closing, in which case they must not have an end tag.
```

- 原始文本元素、`RCDATA元素`以及常规元素都有一个开始标签来表示开始，一个结束标签来表示结束。
- 某些元素的开始和结束标签是可以省略的，如果规定标签不能被省略，那么就绝对不能省略它。
- 空元素只有一个开始标签，且不能为空元素设置结束标签。
- 外来元素可以有一个开始标签和配对的结束标签，或者只有一个自闭合的开始标签，且后者情况下该元素不能有结束标签。

- 标签必须合法且闭合、嵌套正确，标签名需小写
- 标签语法无错误，需要符合语义化
- 标签的自定义属性以data-开头，如：`<a href="#" data-num='18'></a>`
- 除非有特定的功能、组件要求等，禁止随意使用id来定义元素样式

为了能让浏览器更好的解析代码以及能让代码具有更好的可读性，有如下约定：


#### 强制 - HTML标签名、类名、标签属性和大部分属性值统一用小写

```html
<!-- good -->
<div class="demo"></div>

<!-- bad -->
<div class="DEMO"></div>
<DIV CLASS="DEMO"></DIV>

```

#### 对于无需自闭合的标签，不允许自闭合。
常见无需自闭合标签有 input、br、img、hr 等。

```html
<!-- good -->
<input type="text" name="title">

<!-- bad -->
<input type="text" name="title" />
```

#### 对 `HTML5` 中规定允许省略的闭合标签，不允许省略闭合标签。

对代码体积要求非常严苛的场景，可以例外。比如：第三方页面使用的投放系统。

```html
<!-- good -->
<ul>
    <li>first</li>
    <li>second</li>
</ul>

<!-- bad -->
<ul>
    <li>first
    <li>second
</ul>
```

#### 标签使用必须符合标签嵌套规则。

比如 div 不得置于 p 中，tbody 必须置于 table 中。

详细的标签嵌套规则参见[HTML DTD](http://www.cs.tut.fi/~jkorpela/html5.dtd)中的 Elements 定义部分。

[建议] HTML 标签的使用应该遵循标签的语义。

#### HTML 标签的使用应该遵循标签的语义。

下面是常见标签语义

- p - 段落
- h1, h2, h3, h4, h5, h6 - 层级标题
- strong,em - 强调
- ins - 插入
- del - 删除
- abbr - 缩写
- code - 代码标识
- cite - 引述来源作品的标题
- q - 引用
- blockquote - 一段或长篇引用
- ul - 无序列表
- ol - 有序列表
- dl, dt, dd - 定义列表

```html
<!-- good -->
<p>Esprima serves as an important <strong>building block</strong> for some JavaScript language tools.</p>

<!-- bad -->
<div>Esprima serves as an important <span class="strong">building block</span> for some JavaScript language tools.</div>
```

#### 在 CSS 可以实现相同需求的情况下不得使用表格进行布局。
在兼容性允许的情况下应尽量保持语义正确性。对网格对齐和拉伸性有严格要求的场景允许例外，如多列复杂表单。
[建议] 标签的使用应尽量简洁，减少不必要的标签。

```html
<!-- good -->
<img class="avatar" src="image.png">

<!-- bad -->
<span class="avatar">
  <img src="image.png">
</span>
```

#### 属性
[强制] 属性名必须使用小写字母。
```html
<!-- good -->
<table cellspacing="0">...</table>

<!-- bad -->
<table cellSpacing="0">...</table>
```

### 自定义属性建议以 xxx- 为前缀，推荐使用 data-。
使用前缀有助于区分自定义属性和标准定义的属性。

```html
<!-- good -->
<a href="#" data-num='18'></a>

<!-- bad -->
<a href="#" num='18'></a>
```

#### 属性值必须用双引号包围。

不允许使用单引号，不允许不使用引号。

```html
<!-- good -->
<script src="esl.js"></script>

<!-- bad -->
<script src='esl.js'></script>
<script src=esl.js></script>
```

### 布尔类型的属性，建议不添加属性值。

```html
<input type="text" disabled>
<input type="checkbox" value="1" checked>
```
所有具有开始标签和结束标签的元素都要写上起止标签，某些允许省略开始标签或和束标签的元素亦都要写上。
空元素标签都不加 `/` 字符

```html
<!-- good -->
<div>
  <h1>我是h1标题</h1>
  <p>我是一段文字，我有始有终，浏览器能正确解析</p>
</div>
	
<br>

<!-- bad -->
<div>
  <h1>我是h1标题</h1>
  <p>我是一段文字，我有始无终，浏览器亦能正确解析
</div>

<br/>
```
更多关于元素及标签关闭：[Elements](http://www.w3.org/TR/html5/syntax.html#elements-0)

## 特殊字符引用
```html
In certain cases described in other sections, 
text may be mixed with character references. 
These can be used to escape characters that couldn’t otherwise legally be included in text.
```

文本可以和字符引用混合出现。这种方法可以用来转义在文本中不能合法出现的字符。
在 HTML 中不能使用小于号 `<` 和大于号 `>` 特殊字符，浏览器会将它们作为标签解析，若要正确显示，在 HTML 源代码中使用字符实体

```html
<!-- good -->
<a href="#">more&gt;&gt;</a>

<!-- bad -->
<a href="#">more>></a>
```
更多关于符号引用：[Character references](https://html.spec.whatwg.org/multipage/syntax.html#character-references)


## 链接
- 给 `<a>` 标签加上title属性
- `<a>`标签的href属性必须写上链接地址，暂无的加上`javascript:alert('敬请期待！')`
- 非本专题的页面间跳转，采用打开新窗口模式：`target="_blank"`

## https协议自适应

将调用静态域名 `www.eq.cn` 以及 `i.eq.cn` 的外部请求，写法上一律去掉协议`http: | https:`部分，采用自适应的写法。具体方法如下：
```html
<style>
//CSS背景图片 
.bg{background: url(//www.eq.cn/images/cf/hd.jpg) no-repeat;}
</style>
//链接URL
<a href="//www.eq.cn/main.shtml">进入官网</a>
//图片SRC
<img src="//i.eq.cn/images/cf/web201610/logo.png">
//JS链接
<script src="//i.eq.cn/images/js/title.js"></script>
```

## title

页面必须包含 `title` 标签声明标题
`title` 必须作为 head 的直接子元素，并紧随 charset 声明之后
`title` 中如果包含 ASCII 之外的字符，浏览器需要知道字符编码类型才能进行解码，否则可能导致乱码。

```html
<head>
    <meta charset="UTF-8">
    <title>页面标题</title>
</head>
```

## favicon
保证 favicon 可访问

在未指定 favicon 时，大多数浏览器会请求 Web Server 根目录下的 favicon.ico 。为了保证 favicon 可访问，避免 404，必须遵循以下两种方法之一：

- 在 Web Server 根目录放置 favicon.ico 文件。
- 使用 link 指定 favicon。

```html
<link rel="shortcut icon" href="path/to/favicon.ico">
```

## viewport
若页面欲对移动设备友好，需指定页面的 `viewport`。

`viewport meta tag` 可以设置可视区域的宽度和初始缩放大小，避免在移动设备上出现页面展示不正常。

比如，在页面宽度小于 `980px` 时，若需 iOS 设备友好，应当设置 `viewport` 的 width 值来适应你的页面宽度。同时因为不同移动设备分辨率不同，在设置时，应当使用 device-width 和 device-height 变量。

另外，为了使 `viewport` 正常工作，在页面内容样式布局设计上也要做相应调整，如避免绝对定位等。关于 `viewport` 的更多介绍，可以参见 [Safari Web Content Guide的介绍](https://developer.apple.com/library/mac/documentation/AppleApplications/Reference/SafariWebContent/UsingtheViewport/UsingtheViewport.html#//apple_ref/doc/uid/TP40006509-SW26)


## keywords

Keywords为产品名、专题名、专题相关名词，之间用英文半角逗号隔开

```html
 <meta name="keywords" content="遛遛科技系统" />
```

## description

不超过150个字符，描述内容要和页面内容相关。

```html
<meta name="description" content="遛遛科技系统" />
```

## meta

PC端Meta：

```html
<meta charset="gbk" /> 
<meta http-equiv="X-UA-Compatible" content="IE=edge,chrome=1">
<meta name="robots" content="all">
<meta name="author" content="epp" />
<meta name="Copyright" content="epp" />
<meta name="Description" content="页面的描述内容" />
<meta name="Keywords" content="页面关键字" />
```

移动端Meta：

```html
<meta charset="gbk" /> 
<meta name="viewport" content="width=device-width,initial-scale=1,minimum-scale=1,maximum-scale=1,user-scalable=no">
<!-- 为了防止页面数字被识别为电话号码，可根据实际需要添加： -->
<meta name="format-detection" content="telephone=no"> 
<!-- 让添加到主屏幕的网页再次打开时全屏展示，可添加：   -->
<meta content="yes" name="mobile-web-app-capable">
<meta content="yes" name="apple-mobile-web-app-capable">
<meta name="robots" content="all">
<meta name="author" content="epp" />
<meta name="Copyright" content="epp" />
<meta name="Description" content="页面的描述内容" />
<meta name="Keywords" content="页面关键字" />
```

## 注释规范

HTML注释规范写法应该遵循以下标准：

- 必须以4个有序字符开始：编码为 U+003C LESS-THAN SIGN 的小于号, 编码为 U+0021 EXCLAMATION MARK 的感叹号, 编码为 U+002D HYPHEN-MINUS 横线, 编码为 U+002D HYPHEN-MINUS横线 ，即 `<!–`
- 在此之后是注释内容，注释的内容有以下限制：
- 不能以单个 `>` (U+003E) 字符开始
- 不能以由 `-`（U+002D HYPHEN-MINUS）和 `>` (U+003E) 组合的字符开始，即 `->`
- 不能包含两个连续的 U+002D HYPHEN-MINUS 字符，即 `–`
- 不能以一个 U+002D HYPHEN-MINUS 字符结束，即 `-`
- 必须以3个有序字符结束：U+002D HYPHEN-MINUS, U+002D HYPHEN-MINUS, U+003E GREATER-THAN SIGN，即 `–>`

good:

```html
<!--Comment Text-->
```

bad: 
```html
<!-->The Wrong Comment Text-->

<!--->The Wrong Comment Text-->

<!--The--Wrong--Comment Text-->

<!--The Wrong Comment Text--->
```

参考 [www.w3.org](https://www.w3.org/) [#Comments](https://www.w3.org/TR/2014/REC-html5-20141028/syntax.html#comments)


### 单行注释
一般用于简单的描述，如某些状态描述、属性描述等
注释内容前后各一个空格字符，注释位于要注释代码的上面，单独占一行

```html
<!-- good -->
<!-- Comment Text -->
<div>...</div>

<!-- bad -->
<div>...</div><!-- Comment Text -->	
<div><!-- Comment Text -->
    ...
</div>
```

### 模块注释
一般用于描述模块的名称以及模块开始与结束的位置

注释内容前后各一个空格字符，<!-- S Comment Text --> 表示模块开始，<!-- E Comment Text --> 表示模块结束，模块与模块之间相隔一行

good:
```html
<!-- S Comment Text A -->	
<div class="mod_a">
    ...
</div>
<!-- E Comment Text A -->
	
<!-- S Comment Text B -->	
<div class="mod_b">
    ...
</div>
<!-- E Comment Text B -->
```

bad:
```html
<!-- S Comment Text A -->
<div class="mod_a">
    ...
</div>
<!-- E Comment Text A -->
<!-- S Comment Text B -->	
<div class="mod_b">
    ...
</div>
<!-- E Comment Text B -->
```

### 嵌套模块注释
当模块注释内再出现模块注释的时候，为了突出主要模块，嵌套模块不再使用
```html
<!-- good -->
<!-- /Comment Text -->


<!-- bad -->
<!-- S Comment Text -->
<!-- E Comment Text -->
```

注释写在模块结尾标签底部，单独一行。
```html
<!-- S Comment Text A -->
<div class="mod_a">
		
    <div class="mod_b">
        ...
    </div>
    <!-- /mod_b -->
    	
    <div class="mod_c">
    	...
    </div>
    <!-- /mod_c -->
		
</div>
<!-- E Comment Text A -->
```

## 文件模板
HTML模版指的是团队使用的初始化HTML文件，里面会根据不同平台而采用不一样的设置，一般主要不同的设置就是 `mata` 标签的设置，以下是 `PC` 和移动端的 `HTML` 模版。

### HTML5标准模版 - 默认

```html
<!DOCTYPE html>
<html lang="zh-CN">
<head>
<meta charset="UTF-8">
<title>HTML5标准模版</title>
</head>
<body>
	
</body>
</html>
```

### 移动端 - 标准模板
```html
<!DOCTYPE html>
<html lang="zh-CN">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no, shrink-to-fit=no" >
<meta name="format-detection" content="telephone=no" >
<title>移动端HTML模版</title>
	
<!-- S DNS预解析 -->
<link rel="dns-prefetch" href="">
<!-- E DNS预解析 --> 

<!-- S 线上样式页面片，开发请直接取消注释引用 -->
<!-- #include virtual="" -->
<!-- E 线上样式页面片 -->

<!-- S 本地调试，根据开发模式选择调试方式，请开发删除 --> 
<link rel="stylesheet" href="css/index.css" >
<!-- /本地调试方式 -->

<link rel="stylesheet" href="http://srcPath/index.css" >
<!-- /开发机调试方式 -->
<!-- E 本地调试 -->

</head>
<body>

</body>
</html>
```
### PC端 - 标准模板
```html
<!DOCTYPE html>
<html lang="zh-CN">
<head>
<meta charset="UTF-8">
<meta name="keywords" content="your keywords">
<meta name="description" content="your description">
<meta name="author" content="author,email address">
<meta name="robots" content="index,follow">
<meta http-equiv="X-UA-Compatible" content="IE=Edge,chrome=1">
<meta name="renderer" content="ie-stand">
<title>PC端HTML模版</title>

<!-- S DNS预解析 --> 
<link rel="dns-prefetch" href="">
<!-- E DNS预解析 --> 

<!-- S 线上样式页面片，开发请直接取消注释引用 -->
<!-- #include virtual="" -->
<!-- E 线上样式页面片 -->

<!-- S 本地调试，根据开发模式选择调试方式，请开发删除 --> 
<link rel="stylesheet" href="css/index.css" >
<!-- /本地调试方式 -->

<link rel="stylesheet" href="http://srcPath/index.css" >
<!-- /开发机调试方式 -->
<!-- E 本地调试 -->

</head>
<body>

</body>
</html>
```

## WebApp Meta

WebApp目的在于使其界面和行为在某种程度上类似于原生APP应用。例如，WebApp 可以在 iOS 设备上通过缩放去适配设备屏幕。当用户将WebApp程序添加到主屏幕后，会使得它看上去像原生APP一样，以此，你可以进一步为 Safari 定制自己的 WebApp，而使用某些专为 iOS 平台设定的设置就可以做到。

WebApp可以通过设置 meta 标签来改变页面的一些表现，有些 meta 设置在 Safari 应用或原生 App 的内嵌网页中都可以生效，而有些设置侧需要将应用添加到主屏幕的时候才会生效。


### Viewport Meta Tag
```html
<meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
```

- width – viewport的宽度
- height – viewport的高度
- initial-scale – 初始的缩放比例
- minimum-scale – 允许用户缩放到的最小比例
- maximum-scale – 允许用户缩放到的最大比例
- user-scalable – 是否允许用户缩放