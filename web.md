[TOC]

# 前端开发规范

## 前言

前端开发需遵守 [html 编码规范](html.md)、[css 编码规范](css.md)、 [javascript 编码规范](javascript.md) 和本规范。

## 规范说明约定

1. `${root}` 表示项目的根目录

 
## 项目结构

### 目录命名

1. 简洁。有习惯性缩写的单词 *必须(MUST)* 采用容易理解的缩写。如：源代码目录使用`src`，不使用`source`。下面是更多例子：
    1. `img`: 图片。 *不允许(MUST NOT)* 使用`image`、`images`、`imgs`等。
    2. `js`: javascript脚本。 *不允许(MUST NOT)* 使用`script`、`scripts`等。
    3. `css`: 样式表。 *不允许(MUST NOT)* 使用`style`、`styles`等。
    4. `swf`: flash。 *不允许(MUST NOT)* 使用`flash`等。
    5. `src`: 源文件目录。 *不允许(MUST NOT)* 使用`source`等。
    6. `dep`: 引入的第三方依赖包目录。 *不允许(MUST NOT)* 使用`lib`、`library`、`dependency`等。
2.  *不允许(MUST NOT)* 使用复数形式。如：`imgs`、`docs`是不被允许的。

### 目录划分

在 {root} 下，目录结构按功能划分。

不允许(MUST NOT)* 将`资源类型`或`业务逻辑`划分的目录直接置于 ${root}下。

```
{root}/
	dist/
	src/
	test/
	doc/
	dep/
```

* dist：项目发布目录。
* src：项目相关的源文件。
* test：测试文件。
* dep：引入的第三方依赖包目录。

业务相关的文件置于 src 目录下

如果业务相关的文件太多，应该划分成多个子业务。

src 目录下只允许以业务命名的文件夹和 common 文件夹，不允许以资源类型命名的文件夹。

```
src/
	common/
	music/
	movie/
		action-movie/
		romanti-movie/
```

小型网站允许按照资源来划分目录结构

```
{root}
	css/
	font/
	img/
	js/
	index.html
	...
```

业务目录的划分

## 常用目录

### src

存放开发时的源文件。

### dep

存放项目依赖的第三方包。一般情况下不修改 dep 目录下的第三方包。

所有的第三方库必须(MUST)置于改目录下，且每一个库都在该文件夹下创建一个相应的文件夹而不是把资源文件直接放在该目录下。

```
dep/
	jquery/
	bootstrap/
	foo/
```

### tool

存放开发或构建阶段使用的工具。

### test

存放测试用例
### doc

存放项目文档。

### asset

存放用于线上访问线上访问的静态资源。

通常构建工具会对 src 和 dep 目录下的资源进行分析、合并与压缩等，生成到 asset 目录下。所以该目录尽量避免手工管理。

```
asset/
	js/
		loader.js
		build.js
	css/
		common.js
		img/
	tpl/
		build.tpl.html
	img/
```

### js

用于存放脚本资源文件。通常文件后缀是 .js 或 .coffee。

### css

用于存放样式文件，包括 less、sass 等 CSS 预处理语言。通常文件后缀是 .css 、.less 或 .sass 等。

### img

用于存放图片资源文件（png、jpg、gif、svg 等）。

### tpl

用于存放模板（template）资源文件。通常文件后缀是 .tpl 或 .html。

### font

用于存放字体资源文件。通常文件后缀是 .tff 、.woff 或 .svg 等。

### swf

用于存放 flash 资源文件。

### common

公共业务目录

### 文件命名

项目名、HTML 文件名、CSS文件名，LESS 文件名、JavaScript 文件名全部采用小写方式，以中划线分隔。 


## 优化

##### [建议] 减少网页大文件的加载

* CSS文件和JS文件压缩。
* 尽量减小图片的大小。

##### [建议] 通过资源合并减小网络请求次数

* 把多个小的CSS/JS文件合并成大文件。
* css sprites：把一堆小的图片整合到一张大的图片上。

##### [建议] 访问量大时可以使用 CDN 托管

选择稳定、速度快的CDN，推荐国内的CDN。

##### [建议] 合理使用缓存

##### [建议] 引用css和js文件时，在url加上版本号

避免因为浏览器缓存的原因，导致页面排版出错。

```

```

##### [建议] 不滥用 Web 字体

Web字体需要下载，解析，重绘当前页面，尽量减少使用。

##### [强制] 避免仅仅为了显示几个特殊字体而引入整个字体文件

字体文件（.ttf）一般体积很大，请用图片代替文字。

##### [建议] 兼容性需慎重考虑

兼容性伴随着开发、维护的工作量增大。

有时候没必要考虑兼容性。


##### [建议] css 元素放在头部，script 元素放在 `</script>` 之前。