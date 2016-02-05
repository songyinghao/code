[TOC]

# Android编程规范

## 前言

Android 是用 Java 开发的，Java 的编程规范同样对 Android 有效。

关于Java的编程规范，请参考[Java 编程规范](java.md)，这里不再赘述。

 
### 包命名规范
 
安卓常用的模块名：
activity：存放所有Activity类 
adapter：存放所有的适配器类 
service：存放所有Service类 
view：存放自定义控件 
util：存放工具类 
 
### 统一的命名
 
每个Activity命名：XxxActivity.java
 
Activity对应的布局文件：activity_xxx.xml
 
布局文件里面的控件ID：xxx_ + 控件前缀 + 控件名
 
例子1：设置界面
 
SettingActivity.java
 
activity_setting.xml
 
保存按钮：setting_btnSave
 
例子2：个人信息修改界面
 
InfoModifyActivity.java
 
activity_info_modify.xml
 
姓名输入框：info_mofidy_txtName
 
保存按钮：info_mofidy_brnSave
 
 
 
我常用的控件前缀：
 
Button：btn
 
EditText：txt
 
TextView：tv
 
ImageView：iv
 
ListView：lv
 
GridView：gv
 
应用图标icon的大小
drawable-ldpi：32*32
drawable-mdpi：48*48
drawable-hdpi：72*72
drawable-xhdpi：96*96
drawable-xxhdpi：144*144
 
### xml布局文件
 
**单位使用规范** 
在使用单位时，如果没有特殊情况，一律采用dip和sp（字体大小单位）这两个单位。因为这两个单位是与设备分辨率无关的，能够解决在不同分辨率的设备上显示效果不同的问题。
 
### 文件命名规范
 
res/layout目录下文件：
 
统一用小写和下划线"_"组合命名，建议xml文件加个前缀以便区分，如对话框的xml配置文件:dlg_name.xml；
 
res/drawable目录下文件：
 
统一用小写加下划线“_”组合命名，同上，每个资源文件最好加个前缀以便区分，如：btn_submit_default.png，btn_ submit _pressed.png，btn_ submit.xml;