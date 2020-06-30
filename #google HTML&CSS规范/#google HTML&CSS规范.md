# google HTML&CSS规范指南

>  翻译自[原文](https://google.github.io/styleguide/htmlcssguide.html#Parting_Words)

[TOC]









## 1. 背景

本文档定义了HTML和CSS的样式以及格式规则，旨在提高协同合作，代码质量，基础架构支持。本规则应用于基于HTML和CSS为源代码的项目。只要保持常规代码的质量，工具就可以自由地进行混淆、压缩和编译。

## 2. 通用

###  2.1 通用样式规则

#### 2.1.1 **协议**

**在可能的情况下，尽可能的使用HTTPS来嵌入内容资源**

始终使用HTTPS(`https:`)来引用图像和其它的媒体文件，css样式表，以及js脚本。除非没有对应的通过HTTPS提供的资源。

```html
<!-- 不推荐: 省略协议规则 -->
<script src="//ajax.googleapis.com/ajax/libs/jquery/3.4.0/jquery.min.js"></script>

<!-- 不推荐: 使用 HTTP -->
<script src="http://ajax.googleapis.com/ajax/libs/jquery/3.4.0/jquery.min.js"></script>
```

```html
<!-- 推荐 -->
<script src="https://ajax.googleapis.com/ajax/libs/jquery/3.4.0/jquery.min.js"></script>
```

```css
/* 不推荐: 省略协议 */
@import '//fonts.googleapis.com/css?family=Open+Sans';

/* 不推荐: 使用 HTTP */
@import 'http://fonts.googleapis.com/css?family=Open+Sans';
```

```css
/* 推荐 */
@import 'https://fonts.googleapis.com/css?family=Open+Sans';
```



### 2.2 通用格式规则

#### 2.2.1 缩进

**一个缩进等同于两个空格，不要使用多个tabs或者混用tabs和空格来缩进**

```html
<ul>
  <li>Fantastic
  <li>Great
</ul>
```

```css
.example {
  color: blue;
}
```

### 2.3 通用元规则

#### 2.3.1 编码

**使用UTF-8**

确保你的编辑器使用了UTF-8字符编码，没有字节顺序标记。

通过`<meta charset="utf-8">`来指定HTML模版和文档编码。

不要为样式表指定字符集，因为样式表默认是UTF-8字符编码。

（更多编码以及何如指定他们，参考[LINK](https://www.w3.org/International/tutorials/tutorial-char-enc/)）

#### 2.3.2 注释

**在可能的时候，为必要的代码注释。**

#### 2.3.3 操作项

**使用`TODO`来标记代办事项和操作项**

高亮的显示待办事项，仅使用`TODO`，不要使用其它的常见格式，例如`@@`。

在括号中去缀加用户名或者邮箱列表之类的联系方式，如`TODO(联系方式)`。

在冒号后面缀加操作项，如`TODO:操作项`。

```html
{# TODO(john.doe): revisit centering #}
<center>Test</center>
```

```html
<!-- TODO: remove optional tags -->
<ul>
  <li>Apples</li>
  <li>Oranges</li>
</ul>
```



## 3. HTML

### 3.1 HTML样式规则

#### 3.1.1 文档类型

**使用HTML5**

HTML5 标记`<!DOCTYPE html>`是所有HTML文档的首选。

（建议使用HTML，即`text/html`，不要使用XHTML，即`application/xhtml+xml`，因为缺少浏览器和基础架构支持，并且比HTML提供更少的优化空间。）

不要关闭void元素（非文字内容元素，也叫空元素），例如使用`<br>`而不是`</br>`。

#### 3.1.2 HMTL有效性

**尽可能使用有效的HTML，除非由于文件大小的其他无法达到的性能目标而无法这样做。**

可以使用像[W3C HTML validator](https://validator.w3.org/nu/)这样的工具去检测。
使用有效的HTML是一个可测量的基本质量指标，有效的HTML代码有助于了解技术要求和约束，并且确保正确的使用HTML。

```html
<!-- 不推荐 -->
<title>Test</title>
<article>This is only a test.
```

```html
<!-- 推荐 -->
<!DOCTYPE html>
<meta charset="utf-8">
<title>Test</title>
<article>This is only a test.</article>
```

#### 3.1.3 语义化

**根据不同的目的去使用不同的HTML标签**

根据目的去使用合适的HTML标签，对于html文档的可访问性，复用，以及代码效率等原因都起着重要的作用。

```html
<!-- 不推荐 -->
<div onclick="goToRecommendations();">All recommendations</div>
```

```html
<!-- 推荐 -->
<a href="recommendations/">All recommendations</a>
```

#### 3.1.4 为多媒体内容留下挽救方案

**为多媒体替代的内容**

对于对媒体资源，像图片，视频，使用canvas实现的动画对象，要确保提供可替代的内容，对于图片而言，应该指定有意义的替代文本（`alt`属性），对于音视频，如果可能的情况下，应当提供对应的文本和字幕。

提供可替代的内容对提高可访问性而言是很重要的，如果没有`alt`属性，盲人用户几乎无法知道图片是关于什么，而其它用户也有可能没办法理解音视频是什么内容。

```html
<!-- 不推荐 -->
<img src="spreadsheet.png">
```

```html
<!-- 推荐 -->
<img src="spreadsheet.png" alt="Spreadsheet screenshot.">
```

（对于图像而言，`alt`属性有时候也会造成冗余，例如，对于用于装饰用的图片，不具备实际含义，就不应当指定`alt`属性，即`alt=""`。）

#### 3.1.5 业务分离

**应当把文档结构、表现样式、和行为分开。**

严格的保持文档结构（markup），表现样式（styling）和行为（scripting）分离，并且应该尽量的让这三部分相互影响达到最小。

为了实现这一目的，要确保文档和模版只含有HTML代码，且HTML代码仅用于提供布局结构的作用，把所有的样式都放在样式表中，把所有的行为全都放在脚本中。

另外，通过从文档和模板中链接尽可能少的样式表和脚本，使联系区域尽可能小。

项目的可维护性，分离结构和样式以及行为是十分必要的。从样式表和脚本文件中去修改相应逻辑远比直接在html中去修改代价小。

```html
<!-- 不推荐 -->
<!DOCTYPE html>
<title>HTML sucks</title>
<link rel="stylesheet" href="base.css" media="screen">
<link rel="stylesheet" href="grid.css" media="screen">
<link rel="stylesheet" href="print.css" media="print">
<h1 style="font-size: 1em;">HTML sucks</h1>
<p>I’ve read about this on a few sites but now I’m sure:
  <u>HTML is stupid!!1</u>
<center>I can’t believe there’s no way to control the styling of
  my website without doing everything all over again!</center>
```

```html
<!-- 推荐 -->
<!DOCTYPE html>
<title>My first CSS-only redesign</title>
<link rel="stylesheet" href="default.css">
<h1>My first CSS-only redesign</h1>
<p>I’ve read about this on a few sites but today I’m actually
  doing it: separating concerns and avoiding anything in the HTML of
  my website that is presentational.
<p>It’s awesome!
```

#### 3.1.6 实体引用

**不要使用实体引用**

假设文件和编辑器以及团队之间使用相同的编码(UTF-8)，就没有必要使用实体引用，例如 `&mdash;`,`&rdquo;`,`&#x263a;`。

唯一的例外就是当在HTML中表示特殊含义字符的时候，起到类似转义的作用，（例如`<`和`&`）,以及一些不可见的字符（例如不间断空格）。

```html
<!-- 不推荐 -->
The currency symbol for the Euro is &ldquo;&eur;&rdquo;.
```

```html
<!-- 推荐 -->
The currency symbol for the Euro is “€”.
```

#### 3.1.7 可选的标签

**省略可选的标签**

为了优化文件大小和便于扫面，请考虑省略可选的标记，HTML5规范（[HTML5 specification](https://html.spec.whatwg.org/multipage/syntax.html#syntax-tag-omission) ）定义了那些标记可以被省略。

(这种方法可能需要一段宽限期来作为更广泛的指导原则，因为它与web开发人员通常被教导的内容有很大的不同。出于一致性和简单性的原因，最好忽略所有可选标记，而不仅仅是一个选项。)

```html
<!-- 不推荐 -->
<!DOCTYPE html>
<html>
  <head>
    <title>Spending money, spending bytes</title>
  </head>
  <body>
    <p>Sic.</p>
  </body>
</html>
```

```html
<!-- 推荐 -->
<!DOCTYPE html>
<title>Saving money, saving bytes</title>
<p>Qed.
```

#### 3.1.8 `type`属性

**为样式表和脚本省略`type`属性**

不要使用`type`属性为样式表和脚本指明文件类型，除非用的不是css和javascript。

因为HTML5默认指定了`type`为`text/css`以及`text/javascript`,所以在文档中再去使用`type`属性明确文件类型是不必要的。

```html
<!-- 不推荐 -->
<link rel="stylesheet" href="https://www.google.com/css/maia.css" type="text/css">
```

```html
<!-- 推荐 -->
<link rel="stylesheet" href="https://www.google.com/css/maia.css">
```

```html
<!-- 不推荐 0-->
<script src="https://www.google.com/js/gweb/analytics/autotrack.js" type="text/javascript"></script>
```

```html
<!-- 推荐 -->
<script src="https://www.google.com/js/gweb/analytics/autotrack.js"></script>
```



### 3.2 HTML格式规则

#### 3.2.1 通用格式

每一个块区、列表或者表格都应该在新的一行中开始，并且，缩进每个子元素。

(如果您遇到列表项之间存在空格的问题，可以将所有li元素放在一行中。鼓励linter抛出警告而不是错误。)

```html
<blockquote>
  <p><em>Space</em>, the final frontier.</p>
</blockquote>
```

```html
<ul>
  <li>Moe
  <li>Larry
  <li>Curly
</ul>
```

```html
<table>
  <thead>
    <tr>
      <th scope="col">Income
      <th scope="col">Taxes
  <tbody>
    <tr>
      <td>$ 5.00
      <td>$ 4.50
</table>
```

#### 3.2.2 HTML 换行

**断开长行（可选的）**

虽然对于HTML没有限制列的建议，但是如果可以显著提高可读性，可以考虑换行。

当换行之后，每一个衔接行都应该至少额外多缩紧4个空格。

```html
<md-progress-circular md-mode="indeterminate" class="md-accent"
    ng-show="ctrl.loading" md-diameter="35">
</md-progress-circular>
```

```html
<md-progress-circular
    md-mode="indeterminate"
    class="md-accent"
    ng-show="ctrl.loading"
    md-diameter="35">
</md-progress-circular>
```

```html
<md-progress-circular md-mode="indeterminate"
                      class="md-accent"
                      ng-show="ctrl.loading"
                      md-diameter="35">
</md-progress-circular>
```

#### 3.2.3 HTML 引号

**当引用属性值的时候，使用双引号**

使用双引号（`""`）和不是单引号去包裹属性值。.

```html
<!-- 不推荐 -->
<a class='maia-button maia-button-secondary'>Sign in</a>
```

```html
<!-- 推荐 -->
<a class="maia-button maia-button-secondary">Sign in</a>
```









## 4. CSS

### 4.1 CSS样式规则

#### 4.1.1 CSS 有效性

使用有效的CSS

#### 4.1.2 ID和Class命名

**使用有含义的或者通用的ID和Class名。**

避免使用描述性的或者晦涩难懂的命名，始终使用反映了元素目的或功能的ID和类名，或者通用的名称。

特定的且反映目的功能的命名应该尽可能的易于理解且最小的被再次修改的可能性。

通用名称只是与它们的兄弟姐妹没有特殊或没有意义的元素的后备。 通常需要它们作为“帮助者”。

使用功能名称或通用名称可以减少不必要的文档或模板更改的可能性

```css
/* 不推荐: meaningless */
#yee-1901 {}

/* 不推荐: presentational */
.button-green {}
.clear {}
```

```css
/* 推荐: specific */
#gallery {}
#login {}
.video {}

/* 推荐: generic */
.aux {}
.alt {}
```

#### 4.1.3 ID 和 Class 命名样式

使用尽可能短但必要的ID和类名。

尽量简短地传达ID或类的含义。

以这种方式使用ID和类名有助于提高可接受的可理解性和代码效率。

```css
/* 不推荐 */
#navigation {}
.atr {}
```

```css
/* 推荐 */
#nav {}
.author {}
```

#### 4.1.4  类型选择器（Type Selectors）

避免使用类型选择器来限定ID和类名。

除非必要(例如使用helper类)，否则不要将元素名与id或类结合使用。

避免不必要的祖先选择器有助于提高性能([performance reasons](http://www.stevesouders.com/blog/2009/06/18/simplifying-css-selectors/))。

```css
/* 不推荐 */
ul#example {}
div.error {}
```

```css
/* 推荐 */
#example {}
.error {}
```

#### 4.1.5 简写属性

**尽可能的使用简写属性**

CSS提供了很多的简写属性，例如`font`，我们应当尽可能的使用简写属性，即便只有一个需要被显示设定的属性值。

使用简写属性有助于我们理解代码，且有助于代码效率。

```css
/* 不推荐 */
border-top-style: none;
font-family: palatino, georgia, serif;
font-size: 100%;
line-height: 1.6;
padding-bottom: 2em;
padding-left: 1em;
padding-right: 1em;
padding-top: 0;
```

```css
/* 推荐 */
border-top: 0;
font: 100%/1.6 palatino, georgia, serif;
padding: 0 1em 2em;
```

#### 4.1.6 0 和 单位

**如非必要，我们应该总是省略属性值为0时的单位，例如0px。**

```css
flex: 0px; /* This flex-basis component requires a unit. */
flex: 1 1 0px; /* Not ambiguous without the unit, but needed in IE11. */
margin: 0;
padding: 0;
```

#### 4.1.7 前置 0

**省略属性值中的前置0**

不要在值或者长度介于-1到1之间的值中使用0. 

```css
font-size: .8em;
```

#### 4.1.8 十六进制表示法

**如非必要，尽可能的使用三位十六进制表示法**

对于允许的颜色值，三个字符的十六进制表示法更短，更简洁。

```css
/* 不推荐 */
color: #eebbcc;
```

```css
/* 推荐 */
color: #ebc;
```

#### 4.1.9 前缀

在大型项目以及嵌入到其他项目或外部站点中的代码中，请使用前缀（作为名称空间）作为ID和类名。 使用简短的唯一标识符，后接破折号。、

使用名称空间有助于防止命名冲突，并可以简化维护，例如在搜索和替换操作中。

```css
.adw-help {} /* AdWords */
#maia-note {} /* Maia */
```

#### 4.1.10 ID 和 Class 名称分隔符

**在ID或者Class名称中，使用连接符分开多个单词**

为了提高理解和可扫描性 ，在选择器中，除了连字符以外，不要用任何字符连接单词和缩写(不包括任何字符)。

```css
/* 不推荐: 不分开单词 “demo”和 “image” */
.demoimage {}

/*  不推荐: 使用下划线而不是连接符 */
.error_status {}
```

```css
/* 推荐 */
#video-id {}
.ads-sample {}
```

#### 4.1.11 黑客

避免用户代理检测和CSS"黑客攻击"，首先尝试其他方法。

通过用户代理检测或特殊的CSS过滤器、变通方法和hack来解决样式差异是很诱人的。这两种方法都应该作为最后的手段，以实现和维护一个有效的、可管理的代码库。换句话说，从长远来看，给检测和黑客提供免费通行证将损害项目，因为项目往往会采取阻力最小的方式。也就是说，允许并简化检测和破解意味着更频繁地使用检测和破解太频繁了。



### 4.2 CSS格式规则

#### 4.2.1 声明顺序

**按照字母顺序进行声明**

将声明按照字母顺序进行排列，以便以一种易于记忆和维护的方式实现一致性的代码。

忽略供应商特定的前缀以进行排序。然而，针对某个CSS属性的多个供应商特定的前缀

应该保持排序。

```html
background: fuchsia;
border: 1px solid;
-moz-border-radius: 4px;
-webkit-border-radius: 4px;
border-radius: 4px;
color: black;
text-align: center;
text-indent: 2em;
```

#### 4.2.2 块中内容缩进

**缩进所有的块级内容**

这是规则以及声明中的规则，以便反映层次结构并增进理解。

```css
@media screen, projection {

  html {
    background: #fff;
    color: #444;
  }

}
```



#### 4.2.3 声明终止

**使用分号以结束每行声明**

出于一致性和可扩展性的原因，每个声明都以分号结尾。

```css
/* 不推荐 */
.test {
  display: block;
  height: 100px
}
```

```css
/* 推荐 */
.test {
  display: block;
  height: 100px;
}
```



#### 4.2.4 属性名终止

**在每个属性名的冒号后，属性值之前，用一个空格隔开**

始终在最后一个选择器之后，和开括号之前用一个空格隔开

开括号应该和最后一个选择器始终在同一行

```css
/* 不推荐: 缺失空格 */
#video{
  margin-top: 1em;
}

/* 不推荐: 不必要的折行 */
#video
{
  margin-top: 1em;
}
```

```css
/* 推荐 */
#video {
  margin-top: 1em;
}
```

#### 4.2.6 选择器和声明分离

通过折行来分割不同的选择器和声明

每一个选择器始终从新的一行开始

```css
/* 不推荐 */
a:focus, a:active {
  position: relative; top: 1px;
}
```

```css
/* 推荐 */
h1,
h2,
h3 {
  font-weight: normal;
  line-height: 1.2;
}
```

#### 4.2.7 分割样式规则

**始终通过新的空行来分离不同的样式规则**

```css
html {
  background: #fff;
}

body {
  margin: auto;
  width: 50%;
}
```

#### 4.2.8 CSS 引号使用规则

为属性选择器和属性值应用单引号（`''`），而不是双引号（""）

URL 值不要使用引号

例外：除非你使用 `@charset` 规则, 才会用到双引号—[single quotation marks are not permitted](https://www.w3.org/TR/CSS21/syndata.html#charset).

```css
/* 不推荐 */
@import url("https://www.google.com/css/maia.css");

html {
  font-family: "open sans", arial, sans-serif;
}
```

```css
/* 推荐 */
@import url(https://www.google.com/css/maia.css);

html {
  font-family: 'open sans', arial, sans-serif;
}
```



### 4.3 CSS元规则

#### 4.3.1 节注释

**通过注释对节进行分组（可选的）**

尽可能的使用注释对不同的节进行分组，不同的分组间用红白行来分隔。

```css
/* Header */

#adw-header {}

/* Footer */

#adw-footer {}

/* Gallery */

.adw-gallery {}
```

## 最后的话

**始终保持前后一致**

如果您正在编辑代码，请花几分钟时间查看您周围的代码并确定其样式。 如果他们在所

有算术运算符周围使用空格，您也应该这样做。 如果他们的注释周围有小方框，则使您

的注释周围也有小方框。

制定样式指南的目的是拥有通用的编码词汇，以便人们可以专注于您在说的而不是在怎么

说。 我们在这里介绍全局样式规则，以便人们了解词汇表，但是局部样式也很重要。 如

果您添加到文件中的代码看起来与周围的现有代码完全不同，则当读者阅读文件时，会使

他们的节奏变慢。 避免这种情况。



>  翻译自[原文](https://google.github.io/styleguide/htmlcssguide.html#Parting_Words)
