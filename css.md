[TOC]

# CSS编程规范

## 前言

这份规范是针对CSS的，对CSS预处理语言（SASS、LESS 和 Scss）也有一定的参考价值。要求CSS预处理语言编译后生成的CSS代码也必须符合这份规范。


## 基本准则
 
**坚持一致原则**

维护别人写的代码，应当遵守一致原则。即修改后的代码的编程风格应该与之前的代码一致。
 

## 代码风格

### 文件

##### [建议] CSS 文件采用无 BOM 的 utf-8 编码

### 缩进

##### [强制] 采用 4 个空格缩进而不是 2 个空格或 tab 字符
 
###  CSS代码有效性
尽量使用有效的CSS代码。
使用有效的CSS代码，除非是处理CSS校验器程序错误或者需要专有语法。
 
用类似 [W3C CSS validator](http://jigsaw.w3.org/css-validator/)这样的工具来进行有效性的测试。
 
使用有效的CSS是重要的质量衡量标准，如果发现有的CSS代码没有任何效果的可以删除，确保CSS用法适当。

###  规则

##### [建议] 两个规则之间隔一行

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

###  选择器

##### [强制] 选择器和左大括号之间隔一个空格

```
/* good */
.foo {
}

/* bad */
.foo{
}
```

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

##### [强制] `>`、`+`、`~` 选择器的两边各保留一个空格

```
/* good */
ul > li {
}

/* bad */
ul>li {
}
```

###  ID和class的命名

##### [强制] ID名称必须在页面唯一

##### [建议] ID和class的名称应尽量简短且有意义。

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
.atr {}

/* 推荐 */
#nav {}
.author {}
```
###  类型选择器
避免使用CSS类型选择器。
非必要的情况下不要使用元素标签名和ID或class进行组合。
 
出于性能上的考虑避免使用父辈节点做选择器 performance reasons.
```
/* 不推荐 */
ul#example {}
div.error {}
/* 推荐 */
#example {}
.error {}
```


###  属性

##### [强制] 属性名后面的冒号和值之间加一个空格（属性名和冒号之间不能加空格）

```
/* good */
.foo {
	color: #f00;
}

/* bad */
.foo {
	color:#f00;
}
```

##### [建议] 属性尽量使用缩写

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


### 属性值

##### [强制] 当一个熟悉有多个值的时候，`,` 后面必须跟一个空格

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

/* bad */
font-size: 0.8em;
```

##### [建议] 十六进制尽可能使用3个字符。

```
color: #ebc;
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
	font-family:Cambria, "Hoefler Text", serif;
}

/* bad */
.foo {
	font-family:Cambria, Hoefler Text, serif;
}
```
 

###  前缀
选择器前面加上特殊应用标识的前缀（可选）。
大型项目中最好在ID或class名字前加上这种标识性前缀（命名空间），使用短破折号链接。
 
使用命名空间可以防止命名冲突，方便维护，比如在搜索和替换操作上。
```
.adw-help {} /* AdWords */
#maia-note {} /* Maia */
```
 
 


 
##  CSS代码格式规则


### 声明

##### [强制] 每个声明独立一行

```
/* good */
.foo,
.foo2 {
}

/* bad */
.foo, foo2 {
}
```

##### [强制] 所有声明都要用分号结尾

```
/* good */
.foo {
	color: #f00;
}

/* bad */
.foo {
	color: #f00
}
```

###  声明顺序

谷歌推荐依字母顺序进行声明，很容易记住和维护。
忽略浏览器的特定前缀排序，但多浏览器特定的某个CSS属性前缀应相对保持排序（例如-moz前缀在-webkit前面）。
```
background: fuchsia;
border: 1px solid;
-moz-border-radius: 4px;
-webkit-border-radius: 4px;
border-radius: 4px;
color: black;
text-align: center;
text-indent: 2em;
```

而我是这么做的：
1.位置属性(position, top, right, z-index, display, float等)
2.大小(width, height, padding, margin)
3.文字系列(font, line-height, letter-spacing, color- text-align等)
4.背景(background, border等)
5.其他(animation, transition等)


###  代码块内容缩进
缩进所有代码块（“{}”之间）内容。
缩进所有代码块的内容，它能够提高层次结构的清晰度。
```
@media screen, projection {
 
  html {
    background: #fff;
    color: #444;
  }
 
}
```

 

 


## 注释

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

css代码里面不能出现`<!-- -->`这种注释，这会导致注释后面的样式不起作用，而且Dreamweaver编辑器不报错，新手容易被坑！
 

### 继承

##### [建议] 合理地使用继承，减少重复的代码，提供可维护性。

