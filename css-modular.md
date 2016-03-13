[TOC]

# CSS 模块化


## 前言

## 命名

### 基本原则

以 eui 为命名空间（其他的也可以）。

命名空间尽可能简短（2-3个字符）。

## 模块化编写实践

* **语义化的模块名**，通过模块名应该能一眼就看出模块的是干什么的。
* **模块内部的类名继承自父级**。

模块采用 `{命名空间}-{模块名}` 的命名方式。

```
<div class="eui-box"></div>

<nav class="eui-menu"></div>
```

子模块采用 `{命名空间}-{模块名}` 的命名方式。

常用模块名有：header, body，footer, content，text，img，title，item，cell 等， 词义表达组件要实现的功能。

```
<div class="eui-box">
	<div class="eui-box-header">
		<h2>标题</h2>
	</div>
	<div class="eui-box-body">
		<p>内容</p>	
	</div>
	<div class="eui-box-footer">
	</div>
</div>
```

模块状态采用 `{命名空间}-{模块名}-{状态描述}` 的命名方式。

常用状态有：hover, current, selected, disabled, focus, blur, checked, success, error 等

与 JS 交互时，在模块 HTML 结构的最外一层添加状态，而非给模块每个子元素单独添加元素。给最外层添加状态类以后，整个模块的样式都能控制，减少操作，提高性能。
比如，可以这样写：

```
<div class="am-box am-box-active">
   <h3 class="am-box-title"></h3>
   <p class="am-box-content"></p>
</div>
```

但不要这样写（效率更低）：

```
<div class="am-box">
   <h3 class="am-box-title am-box-title-active"></h3>
   <p class="am-box-content am-box-content-active"></p>
</div>
```