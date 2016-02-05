[TOC]

# HTML编程规范

## 前言

## 样式规则

### 协议

嵌入式资源书写省略协议头
省略图像、媒体文件、样式表和脚本等URL协议头部声明 ( http: , https: )。如果不是这两个声明的URL则不省略。
 
省略协议声明，使URL成相对地址，防止内容混淆问题和导致小文件重复下载。
```html
<!-- 不推荐 -->
<script src="http://www.google.com/js/gweb/analytics/autotrack.js"></script>
<!-- 推荐 -->
<script src="//www.google.com/js/gweb/analytics/autotrack.js"></script>
/* 不推荐 */
.example {
  background: url(http://www.google.com/images/example);
}
/* 推荐 */
.example {
  background: url(//www.google.com/images/example);
}
```
## 排版规则
 
### 缩进

#### [强制] 每次缩进 4 个空格，不允许使用 2 个空格过 tab 字符
 
### 换行

#### [建议] 每行代码不超过 120 个字符



### 大小写
所有的代码都用小写字母：适用于元素名，属性，属性值（除了文本和 CDATA ）， 选择器，特性，特性值（除了字符串）。
 
 
##  元数据规则
 
###  编码

#### [建议] 用不带BOM头的 UTF-8编码。
让你的编辑器用没有字节顺序标记的UTF-8编码格式进行编写。
 
在HTML模板和文件中指定编码 `<meta charset="utf-8"> `. 不需要制定样式表的编码，它默认为UTF-8.
 
（更多有关于编码的信息和怎样指定它，请查看 [Character Sets & Encodings in XHTML, HTML and CSS](http://www.w3.org/International/tutorials/tutorial-char-enc/en/all.html)。）
 
 
###  注释
必要的注释

我常常这么做：
```html
<!-- XX模块开始 -->

<!-- XX模块结束 -->
```

### TODO
 
#### [建议] 用 TODO 标记代办事项和正活动的条目

说明：
只用 TODO 来强调代办事项， 不要用其他的常见格式，例如 @@ 。
 
附加联系人（用户名或电子邮件列表），用括号括起来，例如 TODO(contact) 。
 
可在冒号之后附加活动条目说明等，例如 TODO: 活动条目说明 。
 
```html
{# TODO(cha.jn): 重新置中 #}
<center>Test</center>
<!-- TODO: 删除可选元素 -->
<ul>
  <li>Apples</li>
  <li>Oranges</li>
</ul>
```
 
## HTML代码风格规则
 
### DOCTYPE


##### [强制] 使用HTML5标准： `<!DOCTYPE html>`，且DOCTYPE大写
 
###  HTML代码有效性
 
尽量使用有效的HTML代码。比如元素的闭合、必要的元素等等。
编写有效的HTML代码，否则很难达到性能上的提升。
 
用类似这样的工具 W3C HTML validator 来进行测试。
 
HTML代码有效性是重要的质量衡量标准，并可确保HTML代码可以正确使用。
 
 
###  语义

#### [建议] 使用语义标签而不是清一色的div
  
 
###  多媒体后备方案
为多媒体提供备选内容。
对于多媒体，如图像，视频，通过 canvas 读取的动画元素，确保提供备选方案。 对于图像使用有意义的备选文案（ alt ） 对于视频和音频使用有效的副本和文案说明。
 
提供备选内容是很重要的，原因：给盲人用户以一些提示性的文字，用 @alt 告诉他这图像是关于什么的，给可能没理解视频或音频的内容的用户以提示。
 
（图像的 alt 属性会产生冗余，如果使用图像只是为了不能立即用CSS而装饰的 ，就不需要用备选文案了，可以写 alt="" 。）
 
 
###  关注点分离
将表现和行为分开。
严格保持结构 （标记），表现 （样式），和行为 （脚本）分离, 并尽量让这三者之间的交互保持最低限度。
 
确保文档和模板只包含HTML结构， 把所有表现都放到样式表里，把所有行为都放到脚本里。
 
此外，尽量使脚本和样式表在文档与模板中有最小接触面积，即减少外链。
 
将表现和行为分开维护是很重要滴，因为更改HTML文档结构和模板会比更新样式表和脚本更花费成本。
 
不使用样式有关的元素，如center u。
 
 
### 实体引用
不要用实体引用。
不需要使用类似 &mdash; 、 &rdquo; 和 &#x263a; 等的实体引用, 假定团队之间所用的文件和编辑器是同一编码（UTF-8）。
 
在HTML文档中具有特殊含义的字符（例如 < 和 & )为例外， 噢对了，还有 “不可见” 字符 （例如no-break空格）。
 
<!-- 不推荐 -->
欧元货币符号是 `&ldquo;&eur;&rdquo;`。
<!-- 推荐 -->
欧元货币符号是 “€”。
 
### 可选标签
省略可选标签（可选）。
出于优化文件大小和校验， 可以考虑省略可选标签，哪些是可选标签可以参考[ HTML5 specification](http://www.whatwg.org/specs/web-apps/current-work/multipage/syntax.html#syntax-tag-omission)。
 
（这种方法可能需要更精准的规范来制定，众多的开发者对此的观点也都不同。考虑到一致性和简洁的原因，省略所有可选标记是有必要的。）
 
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
<!-- 推荐 -->
<!DOCTYPE html>
<title>Saving money, saving bytes</title>
<p>Qed.
```
 
###  type属性
 
在样式表（除非不用 CSS）和脚本（除非不用 JavaScript）的标签中 不写 type 属性。
 
HTML5默认 type 为 text/css 和 text/javascript 类型，所以没必要指定。即便是老浏览器也是支持的。

## head



## HTML代码格式规则
 
###  格式
每个块元素、列表元素或表格元素都独占一行，每个子元素都相对于父元素进行缩进。
独立元素的样式（as CSS allows elements to assume a different role per display property), 将块元素、列表元素或表格元素都放在新行。
 
另外，需要缩进块元素、列表元素或表格元素的子元素。
 
（如果出现了列表项左右空文本节点问题，可以试着将所有的 li 元素都放在一行。 A linter is encouraged to throw a warning instead of an error.)
 
```html
<blockquote>
  <p><em>Space</em>, the final frontier.</p>
</blockquote>
<ul>
  <li>Moe
  <li>Larry
  <li>Curly
</ul>
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
 

## 未整理


 
不使用样式有关的元素，如center u
 