 [TOC]

[1 前言](#user-content-1-前言)
 
[2 代码风格](#user-content-2-代码风格)
 
　　[2.1 文件](#user-content-21-文件)

　　[2.2 结构](#user-content-22-结构)
 
　　　　[2.2.1 缩进](#user-content-221-缩进)
 
　　　　[2.2.2 空格](#user-content-222-空格)
 
　　　　[2.2.3 空行](#user-content-223-空行)
 
　　　　[2.2.4 换行](#user-content-224-换行)

　　　　[2.2.5 顺序](#user-content-225-顺序)
 
　　[2.3 命名](#user-content-23-命名)
 
　　[2.4 注释](#user-content-24-注释)
 
[3 语言特性](#user-content-3-语言特性)
 
　　[3.1 选择器](#user-content-31-选择器)
 
　　[3.2 声明](#user-content-32-声明)

　　[3.3 属性](#user-content-33-属性)
 
[4 其他](#user-content-4-其他)

　　[4.1 代码有效性](#user-content-41-代码有效性)

# CSS编程规范

## 1 前言

这份规范是针对CSS的，对CSS预处理语言（SASS、LESS 和 Scss）也有一定的参考价值。要求CSS预处理语言编译后生成的CSS代码也必须符合这份规范。


## 2 代码风格

### 2.1 文件

##### [建议] 文件里面没必要指定编码

文件里面没必要指定编码（`@charset "utf-8";`），因为默认就是UTF-8。 

##### [强制] 文件名由小写字母、数字、连字符（-）组成 

```
common.css
index.css
```
##### [强制] 禁止在 CSS 中使用 `@import`

> `@import` 引用的文件只有在引用它的那个css文件被下载、解析之后，才开始下载，这导致css解析、页面渲染延迟，可能导致页面长时间空白。

##### [建议] 单个 CSS 文件避免过大

建议少于 300 行。
 
### 2.2 结构

#### 2.2.1 缩进

##### [强制] 所有代码块（“{}”之间）必须缩进

```
@media only screen and (max-width: 400px) {
	.foo{
		width: 100%;
	}
}
```

#### 2.2.2 空格

##### [强制] 表示块的左大括号之前加一个空格

在每个声明块的左花括号前添加一个空格。

```
/* good */
.foo {
}

media (max-width: 300px) {

}

/* bad */
.foo{
}
```

##### [强制] 属性名后面的冒号和值之间加一个空格

注意属性名和冒号之间不能加空格。

```
/* good */
.foo {
    color: #f00;
}

/* bad */
.foo {
    color:#f00;
}
.foo {
	color : #fff;
}
```

##### [强制] 当一个属性有多个值的时候， `,` 后面必须跟一个空格

```
/* good */
.foo {
    font-family: "楷体", "微软雅黑";
}

/* bad */
.foo {
    font-family: "楷体","微软雅黑";
}
```

##### [强制] `>`、`+`、`~` 选择器的两边各保留一个空格

```
/* good */
ul > li {
}

/* bad */
ul>li {
}
```

#### 2.2.3 空行

##### [可选] 两个规则之间隔一行，注释与规则之间不隔行

```
/* good */
.foo {
}

.foo2 {
}

/* bad */
.foo {
}
.foo2 {
}
```


#### 2.2.4 换行

##### [强制] 每个选择器独立一行

```
/* good */
.foo,
.foo2 {
}

/* bad */
.foo, .foo2 {
}
```

##### [强制] 每个声明独立一行

除了可读性外，还可以获得更准确的错误报告。

```
/* good */
.foo {
	color: #f00;
	font-size: 18px;
}

/* bad */
.foo {
	color: #f00; font-size: 18px;
}
```

##### [强制] 声明块的右花括号应当单独成行

```
/* good */
.foo {
	color: #fff;
}

/* bad */
.foo {
	color: #fff; }
```

#### 2.2.5 顺序

##### [建议] 规则按元素在页面的顺序书写（针对某个页面）

从上到下，从左到右，从外到内。

同一功能模块的规则应该写在一起。


```
.header {
}
.content {
}
.content-left {
}
.content-left .in {
}
.content-right {
}
.footer {
}
```

##### [建议] 声明按照功能排序

相关的属性声明应当归为一组，便于阅读和维护。

> 由于定位（positioning）可以从正常的文档流中移除元素，并且还能覆盖盒模型（box model）相关的样式，因此排在首位。盒模型排在第二位，因为它决定了组件的尺寸和位置。 
> 其他属性只是影响组件的内部（inside）或者是不影响前两组属性，因此排在后面。
 
声明顺序：
1. 位置属性

```
position
top
right
bottom
left
z-index
```

2. 盒模型

```
display
float
width
height
padding
margin
```

3. 文字样式

```
font
line-height
letter-spacing
color
text-align
...
```

4. 背景边框

```
background
border
```

5. 其他

```
animation
transition

opacity
...
```

忽略浏览器的特定前缀排序，但多浏览器特定的某个CSS属性前缀应相对保持排序（例如-moz前缀在-webkit前面）。

针对特殊浏览器的属性，应写在标准属性之前。

```
background: fuchsia;
border: 1px solid;
-webkit-border-radius: 4px;
   -moz-border-radius: 4px;
        border-radius: 4px;
color: black;
text-align: center;
text-indent: 2em;
```

##### [强制] 媒体查询尽可能放在相关规则的附近

不应该把所有的媒体查询（Media query）放在一个单一样式文件中或者放在文档底部。

```
.element { ... }
.element-avatar { ... }
.element-selected { ... }
 
@media (min-width: 480px) {
  .element { ...}
  .element-avatar { ... }
  .element-selected { ... }
}
```

### 2.3 命名

### 2.4 注释

##### [建议] 按功能模块写注释

如果可以，按照功能的类别来对一组样式表写统一注释。独立成行。

```
/* Header */
 
#adw-header {}
 
/* Footer */
 
#adw-footer {}
 
/* Gallery */
 
.adw-gallery {}
```

##### [强制] css代码里面不能出现 `<!-- -->`

这种注释这会导致紧接着注释后面的规则不起作用，而且Dreamweaver编辑器不报错，新手容易被坑！


## 3 语言特性

###  3.1 选择器

#### 3.1.1 高效率、可维护选择器

##### [建议] 尽可能避免使用效率低的选择器

选择器的效率从高到低排序：

* id选择器（#myid）
* 类选择器（.myclassname）
* 标签选择器（div,h1,p）
* 相邻选择器（h1+p）
* 子选择器（ul < li）
* 后代选择器（li a）
* 通配符选择器（*）
* 属性选择器（a[rel="external"]）
* 伪类选择器（a:hover,li:nth-child）

##### [建议] 减少CSS的层级

尽可能控制在二级，避免超过三级。

```
/* good */
.person-info-name {}

/* bad */
.person .info .name {}
```

##### [建议] 避免样式污染

层级为 1 的选择器容易造成样式污染，使用时需谨慎。

一般使用两个层级的选择器，前一个选择器名是页面唯一的模块名，后一个只要保证在模块内唯一就可以了。

```
/* good */
.header .username {
}

/* bad */
.username {
}
```

##### [建议] 避免使用类型选择器

```
/* good */
.foo .head-image {
}

/* bad */
.foo img {
}
.foo div {
}
```

##### [建议] 避免在选择器的右边使用效率低的选择器


##### [强制] ID选择不要与其他选择器一起用

ID 在页面已经是唯一的了，没这个必要。

```
/* good */
#name {}

/* bad */
.info #name {}
```

##### [建议] 非必要的情况下不要使用元素标签名和 class 进行组合

```
/* good */
.error {
}

/* bad */
div .error {}
```

##### [建议] 不滥用 ID 选择器

虽然 ID 选择器效率最高，但应该优先考虑使用类选择器而不是 ID 选择器。

而且，ID 选择器无法复用。

强烈建议不用 ID 选择器来添加样式。

##### [建议] 性能与可维护性之间合理取舍

这点性能的差异，在小网站上是体现不出来的。小网站的优化，不要在这方面钻牛角尖。

当然，作为前端开发者，养成良好的规范是必须的。

对于大型网站，这样做是必须的，但上面的建议往往会牺牲了一定的可维护性（比如减少层级的使用）。如何在性能和可维护性之间取舍，自己看着办吧。



##### [建议] 合理地使用继承，减少重复的代码，提供可维护性。

#### 3.1.2 ID和class的命名

##### [强制] ID名称必须在页面唯一

##### [建议] ID和class的名称应尽量简短且有意义。

##### [强制] ID 和 class 的名称必须满足 `[a-z0-9_-]+`

不允许使用无意义的数字，且必须以字母开头。

以数字开始的类名仅在IE6(Q)/IE7(Q)/IE8(Q)下被识别，而其它浏览器下则不识别（忽略该规则）


```
/* good */
.user-info {
}

/* bad */
.userInfo {
}
.info2 {
}
._foo {
}
```

##### [建议] 单词之间用短破折号“-”分开，不推荐用下划线“_”。

应该优先虑以这元素具体目来进行命名，这样他就最容易理解，减少更新。

通用名称可以加在兄弟元素都不特殊或没有个别意义的元素上，可以起名类似“helpers”这样的泛。

使用功能性或通用的名字会减少不必要的文档或模板修改。
```css
/* 不推荐: 无意义 不易理解 */
#yee-1901 {}
 
/* 不推荐: 表达不具体 */
.button-green {}
.clear {}
/* 推荐: 明确详细 */
#gallery {}
#login {}
.video {}
 
/* 推荐: 通用 */
.aux {}
.alt {}

/* 不推荐，不够简短 */
#navigation {}


/* 推荐 */
#nav {}

/* bad */
.f60 { 
    color: #f60; 
}
.ff8600 { 
    color: #ff8600; 
}
.font12px { 
    font-size: 12px; 
}
.left { float:left; }
```

##### [可选] class 选择器前面加上模块的前缀

大型项目中最好在ID或class名字前加上这种标识性前缀（命名空间）

使用命名空间可以防止命名冲突，方便维护，比如在搜索和替换操作上。

```
.adw-help {} /* AdWords */
#maia-note {} /* Maia */
```

### 3.2 声明


##### [强制] 所有声明都要用分号结尾

尤其是最后一条声明语句后面的分号，如果不写，你的代码可能更易出错。

```
/* good */
.foo {
    color: #f00;
}

/* bad */
.foo {
    color: #f00
}
.foo {
	color: #fff;
	font-size: 18px
}
```


###  3.3 属性

##### [建议] 合理地使用属性缩写

如果需要设置所有值，应当尽量使用简写形式的属性声明。

避免为了简写滥用简写属性声明。

```
/* good */
.foo {
    padding: 20px 10px;
}

/* bad */
.foo {
    padding-top: 20px;
    padding-right: 10px;
    padding-bottom: 20px;
    padding-left: 10px;
}
```

```
/* good */
.foo {
	margin-bottom: 10px;
	background-color: red;
	background-image: url(image.jpg);
	border-top-left-radius: 3px;
	border-top-right-radius: 3px;
}

/* bad */
.foo {
	margin: 0 0 10px 0;
	background: red;
	background: url(image.jpg);
	border-radius: 3px 3px 0 0;
}
```

##### [强制] 0 后面不用加单位。

示例：

```
/* good */
padding: 0;

/* bad */
padding: 0px;
```

##### [强制] 值在-1与1之间的小数，小数前的 0 忽略不写。


```
/* good */
font-size: .8em;
padding-left: -0.5px;

/* bad */
font-size: 0.8em;
padding-left: -.5px;
```

##### [建议] 十六进制尽可能使用3个字符。

```
/* good */
color: #ffffff;

/* bad */
color: fff;
```

##### [强制] 十六进制值应该全部小写

```
/* good */
color: #fc0;

/* bad */
color: #FC0;
color: #Fc0;
```

##### [建议] 尽可能避免使用hacks。

##### [强制] url 函数中的路径不加引号

```css
background: url(bg.png);

@import url(//www.google.com/css/go.css);
```

##### [强制] 属性值由多个单词组成的，用双引号包围

不允许使用单引号，不允许不加引号

```
/* good */
.foo {
    font-family: "微软雅黑", "Hoefler Text", serif;
}

/* bad */
.foo {
    font-family: 微软雅黑, Hoefler Text, serif;
}
```
##### [强制] 颜色采用 16 进制代码而不是颜色的名称

```
/* good */
.foo {
    color: #f00;
}

/* bad */
.foo {
    color: red;
}
```

##### [强制] `font-family` 必须有多个属性值

必须保证总有一个字体会被选中。

```
/* good */
.foo {
    font-family: 幼圆, 宋体, 微软雅黑;
}

/* bad */
.foo {
    font-family: 幼圆;
}
```

## 4 其他

### 4.1 代码有效性

##### [建议] 尽量使用有效的CSS代码

使用有效的CSS代码，除非是处理CSS校验器程序错误或者需要专有语法。

用类似 [W3C CSS validator](http://jigsaw.w3.org/css-validator/)这样的工具来进行有效性的测试。

使用有效的CSS是重要的质量衡量标准，如果发现有的CSS代码没有任何效果的可以删除，确保CSS用法适当。

##### [强制] 禁止使用 Expression

效率原因。

##### [建议] 慎用 `!important`

滥用 `!important` 使代码不易维护。代码中用了很多 importent 说明css的结构肯定有问题。