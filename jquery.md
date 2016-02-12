[TOC]

# JQuery 编码规范

## 前言

JQuery 编程（JQuery插件开发等）必须遵守[Javascript 编码规范](javascript.md)和本编码规范。

## 使用规范

##### [建议] 合理选择版本

v1.13 后的 1.x版本中不再支持IE6和IE7

v2.x 版本不再支持 IE6/7/8

## 插件开发


##### [建议] JQuery 插件代码文件的推荐命名方法为：jquery.插件名.js

```
jquery.lazyload.js

jquery.posfixed.js
```

##### [建议] 针对新的JQuery版本开发



##### [强制] 使用闭包

这是 jQuery 官方的插件开发规范要求，这样做的好处：
* 避免全局依赖。
* 避免第三方破坏。
* 兼容 jQuery 操作符 `$` 和 `jQuery`

```
// good
(function($) {
	$.fn.beautify = function() {
		$(this).css('color', '#f00');
		return this;	
	}
})(jQuery);

// bad
$.fn.beautify = function() {
	$(this).css('color', '#f00');
	return this;	
};
```

##### [强制] 插件应该返回一个JQuery对象，以便保证插件的可链式操作


```
// good
$.fn.beautify = function() {
	$(this).css('color', '#f00');
	return this; // impotent
};

$('#foo').beautify().show();

// bad
$.fn.beautify = function() {
	$(this).css('color', '#f00');
};

$('#foo').beautify().show(); // 出错

```

##### [建议] 接受options参数，以便控制插件的行为

```
$.fn.beautify = function(options) {
	var defaults = { 
		color: '#f00'
	}; 
	var opts = $.extend(defaults, options); 
	
	$(this).css('color', opts.color);
	return this;
};

$('#foo').beautify();
$('#foo').beautify({color: '#ff0'});
```

##### [建议] 暴露插件的默认设置 ，以便外面可以访问

```
(function($){

	$.fn.beautify = function(options) {
		var opts = $.extend({}, $.fn.beautify.defaults, options); 
		
		$(this).css('color', opts.color);
		return this;
	};

	$.fn.beautify.defaults = { 
		color: '#f00'
	}; 
	
})(jQuery);
```

##### [建议] 不要将 CSS 与 Javascript 代码杂揉

```
// bad
$('#foo').css({'color':red, 'font-weight':'bold'});

// good
.error {
	color: red;
	font-weight: bold;
}
$('#foo').addClass('error'); 
```

2. 扩展
 
> jQuery提供了2个供用户扩展的‘基类’ - $.extend和$.fn.extend.
> $.extend 用于扩展自身方法，如$.ajax, $.getJSON等，$.fn.extend则是用于扩展jQuery类，包括方法和对jQuery对象的操作。为了保持jQuery的完整性，我比较 趋向于使用$.fn.extend进行插件开发而尽量少使用$.extend.


示例：

```
(function ($) {
	//默认参数 (放在插件外面，避免每次调用插件都调用一次，节省内存)
	var defaults = {
		color: '红色'
	};

	//扩展
	$.fn.extend({
	//插件名称
	height: function (options) {
	//覆盖默认参数
	var opts = $.extend(defaults, options);
	//主函数
	return this.each(function () {
	//激活事件
	var obj = $(this);
	obj.click(function () {
	alert(opts.color);
	});
	});
	}
	})
	})(jQuery);
	$(function () {
	$("p").height({ color: 'black' });
});
``` 
 
##### [建议] 开发效率与执行效率的合理选择

##### [建议] 使用对象来传递参数

```
// bad
$myLink.attr("href", "#").attr("title", "my link").attr("rel", "external");

// good
$myLink.attr({
    href: "#",
    title: "my link",
    rel: "external"
});
```

##### [建议] 使用 on() 方法绑定事件

官方推荐这么做

##### [建议] 使用 CDN

Microsoft CDN：
http://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.1.0.min.js

百度 CDN：
http://libs.baidu.com/jquery/2.0.3/jquery.min.js


提示：使用谷歌或微软的 jQuery，有一个很大的优势：
许多用户在访问其他站点时，已经从谷歌或微软加载过 jQuery。所有结果是，当他们访问您的站点时，会从缓存中加载 jQuery，这样可以减少加载时间。同时，大多数 CDN 都可以确保当用户向其请求文件时，会从离用户最近的服务器上返回响应，这样也可以提高加载速度。


为了保险起见，当无法从CDN服务器上获取jQuery时，则使用本地jQuery

<script type="text/javascript">window.jQuery||document.write('<scriptsrc="//localhost/jQuery/jquery-2.1.0.min.js"><\/script>');</script>
在Wordpress主题中使用的方法为
1

<script type="text/javascript">window.jQuery||document.write('<scripttype="text/javascript"src="<?phpechoget_template_directory_uri();?>/jquery.min.js">\x3C/script>')</script>

6、推荐使用国内CDN公共库，速度更快，稳定性更高。