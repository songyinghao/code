[TOC]

# Javascript 编码规范

## 前言

Javascript 编程必须遵守[通用编程规范](common.md)和本编程规范。

## 1 代码风格

### 1.1 文件

##### [推荐] Javascript文件使用无 BOM 的 UTF-8 编码

##### [建议] Javascript文件格式 `.js`，压缩文件格式 `.min.js`

```
jquery.js
jquery.min.js
```

### 1.2 结构

#### 1.2.1 缩进

#### 1.2.2 空格

#### 1.2.3 换行

#### 1.2.4 语句

### 1.3 命名

### 1.4 注释

## 2 语言特性

### 2.1 变量

##### [强制] 变量在使用前必须先定义

不通过 var 定义变量将导致变量污染全局环境。

```
// good
var foo = 1;

// bad
foo = 1;
```

##### [强制] 每条语句必须以分号结尾

```
var funcName = function () {
};
```

##### [强制] 函数定义结束不允许添加分号

```
// good
function funcName() {
}

// bad
function funcName() {
};

// 如果是函数表达式，分号是不允许省略的。
var funcName = function () {
};
```

##### [强制] 没必要的逗号要删除

```
// bad
{
    name: 'foo',
    age: 14,
}

// good
{
    name: 'foo',
    age: 14
}
```

##### [建议] 谨慎使用全局变量。

##### [建议] 使用 `===` 而不是 `==` 判断是否相等

##### [强制] 字符串使用单引号

除非特殊情况不能使用单引号，否则使用单引号

```
// good
var name = 'MyName';

// bad
var name = "MyName";
```

##### [强制] 一个函数应该返回统一的数据类型。


##### [建议] 不需要所有的东西都用jQuery实现。也不必为了效率放弃JQuery，应该合理地选择。

##### [建议] 慎用闭包。

不要使用 with() 语句。

最好在函数的顶端把需要使用的变量首先声明一遍。

**大文件可以压缩处理**

[在线JS/CSS/HTML压缩](http://tool.oschina.net/jscompress)
(采用YUI Compressor实现)

##### [建议] setTimeout() 第一个参数不建议使用字符串

为了安全

```
function foo {...}

// good
setTimeout(foo, 1000);

// bad
setTimeout('foo()', 1000);
```

##### [可选] 适当情况下使用 `&&` 使代码简洁

```
// good
if (something()) { 
	other();
}

// good
something() && other();
```

## AMD 规范