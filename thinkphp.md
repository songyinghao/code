# thinkphp 编码规范

## 1 前言

鉴于公司多数项目采用 ThinkPHP 框架，本规范对 ThinkPHP 的使用作出部分限制。php 项目开发需遵守本规范和 [PHP编码规范](php.md)


原则上，所有ThinkPHP框架硬性规定的Model、Controller以外，所有的文件在命名上均应该使用小写（包括后缀名），在任何时候都严禁大小写混编。一般来说，建议的格式为：

## 2 代码风格

### 2.1 文件


### 2.2 命名

##### [强制] 控制器采用 XxxController 的命名方式，文件名格式为 XxxController.class.php

```
ArticleController.class.php
```

### 2.3 注释

##### 文档注释


@author

## 3 语言特征


##### [强制] 项目采用 MVC 的方式开发

```
dep/
	jquery/
	bootstrap/
	foo/
```

##### [建议] 避免在View层处理业务逻辑。

* 尽可能减少 view 层 php 代码。
* 尽可能使用模板引擎。

```
// good
<if condition='foo'>
    {$article.title}								
</if>

// bad
<?php
if (foo) {
    echo $article.title;
}
?>
```

##### [建议] 尽可能使用简短的 url

ThinkPHP 支持多台路由，尽可能配置简短的 url。url 的设计可参照 REST。

```
// good
foo.com/about
foo.com/category/48

// bad
foo.com/index.php/Home/Category/category/id/48
```