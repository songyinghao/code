[TOC]

# PHP 编码规范

## 1 前言

阅读本规范需结合[通用编码规范](common.md)，里面讲到的规范这里不再赘述，此外，PHP代码里面出现的HTML编码需遵守[HTML 编码规范](html.md)。

## 2 代码风格

### 2.1 文件

##### [强制] 对于只含有 php 代码的文件，文件结尾处忽略掉 `?>`

防止多余的空格或者其它字符影响到代码。

##### [强制] 不使用 php 短标签

php 标签采用完整的形式 `<?php … ?>`，不使用短标签 `<? … ?>`，且保证在关闭标签后不要有任何空格。

### 2.2 结构

### 2.3 命名

##### [强制] 大小写不敏感的标识符，当做大小写敏感来使用

所有标识符都当做是大小写敏感的，严格按照通用编程规范来定义，使用时使用与定义相同的名字。

##### [强制] 常量默认大小写敏感，按照规范，禁止开启大小写不敏感

常量默认大小写敏感，也可以定义成不敏感，但不允许这么做。

```
```

##### [强制] 魔术常量统一大写

包括：__LINE__、__FILE__、__DIR__、__FUNCTION__、__CLASS__、__METHOD__、__NAMESPACE__。

```
// good
echo __LINE__;

// bad
echo __line__;
```

##### [强制] null、true、false 统一小写

```
// good
$foo = null;
$foo = true;
$foo = false;

// bad
$foo = NULL;
$foo = TRUE;
$foo = FALSE;
```

##### [强制] 类型强制转换统一小写

包括：

* (int)，(integer) – 转换成整型
* (bool)，(boolean) – 转换成布尔型
* (float)，(double)，(real) – 转换成浮点型
* (string) – 转换成字符串
* (array) – 转换成数组
* (object) – 转换成对象

```
// good
$foo = (string) 1;

// bad 
$foo = (STRING) 1;
```

### 2.4 注释

## 3 语言特性

### 3.1 字符串

##### [强制] 字符串使用单引号

除非字符串里面有变量或者其他特殊情况不能使用单引号，否则使用单引号

为了统一和效率。

```
// good
$name = 'MyName';

// bad
$name = "MyName";
```

### 3.2 条件

##### [建议] 使用 `else...if` 而不是 `elseif`

没为什么，仅仅是为了统一而已。

### 3.3 类、属性和方法

##### [强制] 所有的属性和方法必须有可见性(public, protected, private)

* abstract和final声明必须在可见性之前；
* static声明必须在可见性之后。

### 3.4 其他

##### [强制] 源文件只能使用 <?php 这种标签

```
// good
<?php echo $name; ?>

// bad
<?= $name; ?>
```


##### [强制] PHP5.3之后的代码必须使用正式的命名空间

```
namespace Vendor\Model;

class Foo {
}
```

##### [强制] 命名空间(namespace)的声明后面必须有一行空行

##### [强制] 所有的导入(use)声明必须放在命名空间(namespace)声明的下面

##### [强制] 一句声明中，必须只有一个导入(use)关键字

##### [强制] 在导入(use)声明代码块后面必须有一行空行。

```
namespace Vendor\Package;

use FooClass;
use BarClass as Bar;
use OtherVendor\OtherPackage\BazClass;

// ...
```