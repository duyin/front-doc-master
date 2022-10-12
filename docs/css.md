# CSS 规范

## 命名规范

命名规则规范问题，使用`BEM`命名规则，避免使用如：（.t-c 这种无意义命名）[参考URL](http://getbem.com/)

### 什么是 BEM 命名规范
Bem 是块（block）、元素（element）、修饰符（modifier）的简写，由 Yandex 团队提出的一种前端 CSS 命名方法论。

::: warning
- `-` 中划线 ：仅作为连字符使用，表示某个块或者某个子元素的多单词之间的连接记号。
- `__` 双下划线：双下划线用来连接块和块的子元素
- `_` 单下划线：单下划线用来描述一个块或者块的子元素的一种状态
:::

BEM 是一个简单又非常有用的命名约定。让你的前端代码更容易阅读和理解，更容易协作，更容易控制，更加健壮和明确，而且更加严密。

### BEM 命名约定的模式是
```css
.block {}

.block__element {}

.block--modifier {}
```
- 每一个块(`block`)名应该有一个命名空间（前缀）
  - `block` 代表了更高级别的抽象或组件。
  - `block__element` 代表 `.block` 的后代，用于形成一个完整的 `.block` 的整体。
  - `block--modifier` 代表 `.block` 的不同状态或不同版本。

使用两个连字符和下划线而不是一个，是为了让你自己的块可以用单个连字符来界定。如：
```css
.sub-block__element {}

.sub-block--modifier {}
```

### BEM 命名法的好处
BEM的关键是，可以获得更多的描述和更加清晰的结构，从其名字可以知道某个标记的含义。于是，通过查看 HTML 代码中的 class 属性，就能知道元素之间的关联。


## 代码风格
### 行长度 - 每行不得超过 120 个字符，除非单行不可分割。
常见不可分割的场景为URL超长。

[建议] 对于超长的样式，在样式值的 空格 处或 , 后换行，建议按逻辑分组。
```css
/* 不同属性值按逻辑分组 */
background:
  transparent url(aVeryVeryVeryLongUrlIsPlacedHere)
  no-repeat 0 0;

/* 可重复多次的属性，每次重复一行 */
background-image:
  url(aVeryVeryVeryLongUrlIsPlacedHere)
  url(anotherVeryVeryVeryLongUrlIsPlacedHere);

/* 类似函数的属性值可以根据函数调用的缩进进行 */
background-image: -webkit-gradient(
  linear,
  left bottom,
  left top,
  color-stop(0.04, rgb(88,94,124)),
  color-stop(0.52, rgb(115,123,162))
);
```

### 使用 2 个空格做为一个缩进层级

```css
.selector {
  margin: 0;
  padding: 0;
}
```

### 空格

#### 选择器 与 { 之间必须包含空格
```css
.selector {

}
```

#### 属性名 与之后的 : 之间不允许包含空格， : 与 属性值 之间必须包含空格。
```css
margin: 0;
```

#### 列表型属性值 书写在单行时，, 后必须跟一个空格。
```css
font-family: Arial, sans-serif;
```

### 代码大小写
样式选择器，属性名，属性值关键字全部使用小写字母书写，属性字符串允许使用大小写。
```css
/* good */
.black {
  display: block;
  color: #90ee90;
}

/* bad */
.BLACK {
	DISPLAY: BLOCK;
  color: #90EE90;
}
```

### 当一个 rule 包含多个 selector 时，每个选择器声明必须独占一行。
```css
/* good */
.nav, 
.nav_logo, 
.nav_head {
  color: #ff0;
}

.nav {
  color: #fff;
}

/* bad */
.nav,.nav_logo,.nav_head {
  color: #ff0;
}.nav {
  color: #fff;
}
```

### >、+、~ 选择器的两边各保留一个空格。
```css
/* good */
main > nav {
  padding: 10px;
}

label + input {
  margin-left: 5px;
}

input:checked ~ button {
  background-color: #69C;
}

/* bad */
main>nav {
  padding: 10px;
}

label+input {
  margin-left: 5px;
}

input:checked~button {
  background-color: #69C;
}
```

### 颜色值 rgb() rgba() hsl() hsla() rect() 中不需有空格，且取值不要带有不必要的 0 
```css
/* good */
.red {
  color: rgba(255,255,255,.5);
}

/* bad */
.red {
  color: rgba( 255, 255, 255, 0.5 );
}
```

### 属性值十六进制数值能用简写的尽量用简写

```css
/* good */
.white {
  color: #fff;
}

/* bad */
.white {
  color: #ffffff;
}
```

### 不要为 0 指明单位
```css
/* good */
.margin {
  margin: 0 10px;
}

/* bad */
.margin {
  margin: 0 10px;
}
```

### 选择器的嵌套层级应不大于 3 级，位置靠后的限定条件应尽可能精确
```css
/* good */
#username input {}
.comment .avatar {}

/* bad */
.page .header .login #username input {}
.comment div * {}
```

## 属性规范

###  属性定义后必须以分号结尾。
```css
/* good */
.selector {
  margin: 0;
}

/* bad */
.selector {
  margin: 0
}
```

### 属性定义必须另起一行。
```css
/* good */
.selector {
  margin: 0;
  padding: 0;
}

/* bad */
.selector { margin: 0; padding: 0; }
```

### 属性选择器中的值必须用双引号包围。
```css
/* good */
article[character="juliet"] {
  voice-family: "Vivien Leigh", victoria, female;
}

/* bad */
article[character='juliet'] {
  voice-family: "Vivien Leigh", victoria, female;
}
```

### 属性书写顺序
同一 rule set 下的属性在书写时，应按功能进行分组，并以 Formatting Model（布局方式、位置） > Box Model（尺寸） > Typographic（文本相关） > Visual（视觉效果） 的顺序书写，以提高代码的可读性。

::: warning
建议遵循以下顺序：
- 布局定位属性：position / top / right / bottom / left / float / display / overflow 等
- 自身属性：width / height / margin / padding / border / background
- 文本属性：color / font / text-decoration / text-align / vertical-align / white- space / break-word
- 其他属性（CSS3）：content / cursor / border-radius / box-shadow / text-shadow / background:linear-gradient …

另外，如果包含 content 属性，应放在最前面。
:::

```css
.sidebar {
  /* formatting model: positioning schemes / offsets / z-indexes / display / ...  */
  position: absolute;
  top: 50px;
  left: 0;
  overflow-x: hidden;

  /* box model: sizes / margins / paddings / borders / ...  */
  width: 200px;
  padding: 5px;
  border: 1px solid #ddd;

  /* typographic: font / aligns / text styles / ... */
  font-size: 14px;
  line-height: 20px;

  /* visual: colors / shadows / gradients / ... */
  background: #f5f5f5;
  color: #333;
  -webkit-transition: color 1s;
  -moz-transition: color 1s;
  transition: color 1s;
}
```
[mozilla官方属性顺序推荐](https://www.mozilla.org/en-US/css/base/content.css)


### CSS3浏览器私有前缀写法
CSS3 浏览器私有前缀在前，标准前缀在后


```css
.black {
  -webkit-border-radius: 10px;
  -moz-border-radius: 10px;
  -o-border-radius: 10px;
  -ms-border-radius: 10px;
  border-radius: 10px;
}
```
更多关于浏览器私有前辍写法：[Vendor-specific extensions](https://www.w3.org/TR/2011/REC-CSS2-20110607/syndata.html#vendor-keywords)

## 文本编排

### font-family 属性中的字体族名称应使用字体的英文 Family Name，其中如有空格，须放置在引号中。
所谓英文 Family Name，为字体文件的一个元数据，常见名称如下：
| 字体        | 操作系统                            | Family Name          |
| :----------- | :------------------------------------- |  :-------------- |
| 宋体 (中易宋体)	 | Windows | 	SimSun |
| 黑体 (中易黑体)	 | Windows | 	SimHei |
| 微软雅黑	 | Windows | 	Microsoft YaHei |
| 微软正黑	 | Windows | 	Microsoft JhengHei |
| 华文黑体	 | Mac/iOS | 	STHeiti |
| 冬青黑体	 | Mac/iOS | 	Hiragino Sans GB |
| 文泉驿正黑	 | Linux | 	WenQuanYi Zen Hei |
| 文泉驿微米黑	 | Linux | 	WenQuanYi Micro Hei |
```css
h1 {
  font-family: "Microsoft YaHei";
}
```

### font-family 按「西文字体在前、中文字体在后」、「效果佳 (质量高/更能满足需求) 的字体在前、效果一般的字体在后」的顺序编写，最后必须指定一个通用字体族( serif / sans-serif )。
```css
/* Display according to platform */
.article {
  font-family: Arial, sans-serif;
}

/* Specific for most platforms */
h1 {
  font-family: "Helvetica Neue", Arial, "Hiragino Sans GB", "WenQuanYi Micro Hei", "Microsoft YaHei", sans-serif;
}
```
更详细说明可参考[本文](https://www.zhihu.com/question/19911793/answer/13329819)。

### font-family 不区分大小写，但在同一个项目中，同样的 Family Name 大小写必须统一。
```css
/* good */
body {
  font-family: Arial, sans-serif;
}

h1 {
  font-family: Arial, "Microsoft YaHei", sans-serif;
}

/* bad */
body {
  font-family: arial, sans-serif;
}

h1 {
  font-family: Arial, "Microsoft YaHei", sans-serif;
}
```

### 需要在 Windows 平台显示的中文内容，其字号应不小于 12px。
由于 Windows 的字体渲染机制，小于 12px 的文字显示效果极差、难以辨认。

### font-weight 属性必须使用数值方式描述。
- CSS 的字重分 `100 – 900` 共九档，但目前受字体本身质量和浏览器的限制，实际上支持 `400` 和 `700` 两档，分别等价于关键词 `normal` 和 `bold。`
- 浏览器本身使用一系列启发式规则来进行匹配，在 `<700` 时一般匹配字体的 `Regular` 字重，`>=700 `时匹配 Bold 字重。
- 但已有浏览器开始支持 `=600` 时匹配 `Semibold` 字重 (见此表)，故使用数值描述增加了灵活性，也更简短。

```css
/* good */
h1 {
  font-weight: 700;
}

/* bad */
h1 {
  font-weight: bold;
}
```

### 行高 - line-height 在定义文本段落时，应使用数值。
将 `line-height` 设置为数值，浏览器会基于当前元素设置的 `font-size` 进行再次计算。在不同字号的文本段落组合中，能达到较为舒适的行间间隔效果，避免在每个设置了 font-size 都需要设置 `line-height`。

当 `line-height` 用于控制垂直居中时，还是应该设置成与容器高度一致。

```css
.container {
  line-height: 1.5;
}
```

## 变换与动画

### 使用 transition 时应指定 transition-property。
```css
/* good */
.box {
  transition: color 1s, border-color 1s;
}

/* bad */
.box {
  transition: all 1s;
}
```

### 尽可能在浏览器能高效实现的属性上添加过渡和动画。
见[本文](http://www.html5rocks.com/en/tutorials/speed/high-performance-animations/)，在可能的情况下应选择这样四种变换：

- transform: translate(npx, npx);
- transform: scale(n);
- transform: rotate(ndeg);
- opacity: 0..1;
典型的，可以使用 translate 来代替 left 作为动画属性。

```css
/* good */
.box {
  transition: transform 1s;
}
.box:hover {
  transform: translate(20px); /* move right for 20px */
}

/* bad */
.box {
  left: 0;
  transition: left 1s;
}
.box:hover {
  left: 20px; /* move right for 20px */
}
```

## 响应式

### Media Query 不得单独编排，必须与相关的规则一起定义。
```css
/* Good */
/* header styles */
@media (...) {
  /* header styles */
}

/* main styles */
@media (...) {
  /* main styles */
}

/* footer styles */
@media (...) {
  /* footer styles */
}


/* Bad */
/* header styles */
/* main styles */
/* footer styles */

@media (...) {
  /* header styles */
  /* main styles */
  /* footer styles */
}
```

### Media Query 如果有多个逗号分隔的条件时，应将每个条件放在单独一行中。
```css
@media
(-webkit-min-device-pixel-ratio: 2), /* Webkit-based browsers */
(min--moz-device-pixel-ratio: 2),    /* Older Firefox browsers (prior to Firefox 16) */
(min-resolution: 2dppx),             /* The standard way */
(min-resolution: 192dpi) {           /* dppx fallback */
  /* Retina-specific stuff here */
}
```
尽可能给出在高分辨率设备 (Retina) 下效果更佳的样式。


## 兼容性

### 属性前缀 - 带私有前缀的属性由长到短排列，按冒号位置对齐。
标准属性放在最后，按冒号对齐方便阅读，也便于在编辑器内进行多行编辑。

```css
.box {
  -webkit-box-sizing: border-box;
  -moz-box-sizing: border-box;
  box-sizing: border-box;
}
```

### 需要添加 hack 时应尽可能考虑是否可以采用其他方式解决。
如果能通过合理的 HTML 结构或使用其他的 CSS 定义达到理想的样式，则不应该使用 hack 手段解决问题。通常 hack 会导致维护成本的增加。

[建议] 尽量使用 选择器 hack 处理兼容性，而非 属性 hack。

尽量使用符合 CSS 语法的 selector hack，可以避免一些第三方库无法识别 hack 语法的问题。

```css
/* IE 7 */
*:first-child + html #header {
  margin-top: 3px;
  padding: 5px;
}

/* IE 6 */
* html #header {
  margin-top: 5px;
  padding: 4px;
}
```

### 尽量使用简单的 属性 hack。
```css
.box {
  _display: inline; /* fix double margin */
  float: left;
  margin-left: 20px;
}

.container {
  overflow: hidden;
  *zoom: 1; /* triggering hasLayout */
}
```

## 代码注释
