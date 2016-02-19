[TOC]

# Android编程规范

## 1 前言

Android 是用 Java 开发的，Java 的编程规范同样对 Android 有效。

关于Java的编程规范，请参考[Java 编程规范](java.md)，这里不再赘述。

## 2 代码风格

### 2.1 文件

### 2.2 结构

### 2.3 命名

#### 包命名规范
 
安卓常用的模块名：

* activity：存放所有Activity类 
* adapter：存放所有的适配器类 
* base：基类，如BaseActivity、BaseFragment等等。
* broadcast：Broadcast服务类
* common：全局常量，应用配置信息。
* db：数据库操作
* fragment
* model：实体类（bean、domain均可，个人喜好）
* service：存放所有Service类 
* util：存放工具类 
* view：（或者.ui）存放自定义控件 


```
SplashActivity // 闪屏界面
MainActivity // 主界面
```

#### 类命名规范

Application类：XxxApplication

Activity类：XxxActivity
闪屏页面类：SplashActivity


解析类：XxxHandler


公共方法类：
XxxUtils或XxxManager
线程池管理类：ThreadPoolManager
日志工具类：LogUtils

数据库类

以DBHelper后缀标识
MySQLiteDBHelper

Service类
以Service为后缀标识
播放服务：PlayService

BroadcastReceiver类
以Broadcast为后缀标识
时间通知：
TimeBroadcast

ContentProvider类
以Provider为后缀标识
单词内容提供者：DictProvider

直接写的共享基础类
以Base为前缀
BaseActivity,
BaseFragment



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
 




### 控件变量的命名，控件的ID命名：

建议：xml布局文件中的控件的id的命名与*.java的代码文件中的控件对象的命名一致。

```
TextView txtUserName = (TextView) findViewById(R.id.main_txtUserName);
Button btnClose = (Button) findViewById(R.id.main_btnClose);
```


 
常用的控件前缀：采用控件名称的各单词首字母
如：
```
TextView tv
ImageView iv
RelativeLayout rl
```

例外：
``` 
Button btn
ImageButton imgBtn

```
 
##### [建议] 应用图标的大小要合理

* drawable-ldpi：32*32
* drawable-mdpi：48*48
* drawable-hdpi：72*72
* drawable-xhdpi：96*96
* drawable-xxhdpi：144*144
 
#### xml布局文件

##### [强制] 单位使用要规范
 
字体大小采用sp，其他的全部使用dp。

dp 和 sp 这两个单位是与设备分辨率无关的，能够解决在不同分辨率的设备上显示效果不同的问题。
 
### 文件命名规范
 
res/layout目录下文件：
 
统一用小写和下划线"_"组合命名，建议xml文件加个前缀以便区分，如对话框的xml配置文件:dlg_name.xml；
 
res/drawable目录下文件：
 
统一用小写加下划线“_”组合命名，同上，每个资源文件最好加个前缀以便区分，如：btn_submit_default.png，btn_ submit _pressed.png，btn_ submit.xml;



## 调试

##### [建议] 在运行慢的手机上测试
 
你将在运行慢的手机上发现很多问题

## API

##### [建议] ListView的优化
 
如果列表的列表项太多，可以使用ViewHolder对Adapter的getView方法进行优化



##### [建议] 尽量减少 XML 布局层次
 
更多的层次意味着系统将为解析你的代码付出更多的工作，这将会让图像渲染的更慢。

熟悉RelativeLayouot可以帮你减少布局层次。

### string.xml

##### [建议] 如果是控件上面显示的文本，放在strings.xml资源文件中

##### [建议] 除了注释外，Java 代码中不出现中文

### color.xml

颜色值的命名：  color_description  以color为前缀，全部小写，下划线分隔。description既可以是该颜色值使用的功能描述，也可以是该颜色值的英文描述，也可以是具体的颜色值，例如：

```
<color name="color_white">#ffffff</color>
<color name="color_grey_ccc">#cccccc</color>
<color name="color_grey_ddd">#dddddd</color>
```
因为grey可能有很多等级，有时候需要不同等级的灰色，没有那么多英文名可以区分，所以名字中可以直接使用颜色值
<color name=”color_button_pressed”>#4c4c4c</color> 根据功能定义description，表示该颜色用于按钮被按下

### styles.xml

将layout中不断重现的style提炼出通用的style通用组件，放到styles.xml中


### 动画文件

动画文件（anim文件夹下）：

全部小写，采用下划线命名法，加前缀区分。

//前面为动画的类型，后面为方向

```
fade_in // 淡入
fade_out // 淡出
push_down_in // 从下方推入
push_down_out // 从下方推出
push_left // 推向左方
slide_in_from_top // 从头部滑动进入
zoom_enter // 变形进入
slide_in // 滑动进入
shrink_to_middle // 中间缩小
```

### 常用的常量

##### [建议] Activity 之间传递参数的 key 值采用 `EXTRA_`。

这些常量定义在被启动的 Activity 中。

```
intent.putExtra(EXTRA_USER_ID, "123");
startActivity(intent);
```

##### [建议] SharedPreferences 中的 key 采用 `SP_` 前缀

这些常量定义在公共类中。

```
sharedPreferences.getString(Constant.SP_PASSWORD, "");
```

##### [建议] Message 的 ID 采用 `MSG_` 前缀

```
private static final String MSG_SUCCESS = "message_success"; // 获取数据成功
private static final String MSG_FAILURE = "message_failure"; // 获取数据失败

Message msg = handler.obtainMessage();
msg.what = MSG_SUCCESS;
```  

##### [建议] onActivityResult 中的 requestCode 和 resultCode 分别采用 `REQUEST_` 和 `RESULT_` 后缀

```
private static final int RESULT_SUCCESS = 0;
private static final int RESULT_NO_DATA = 1;
private static final int RESULT_NETWORK_EXCEPTION = 2;
private static final int RESULT_PARSE_JSON_EXCEPTION = 3;

startActivityForResult(intent, REQUEST_QRCODE);

@Override
protected void onActivityResult(int requestCode, int resultCode, Intent data) {
    if (requestCode == REQUEST_QRCODE){
        if (resultCode == BeCalledActivity.RESULT_SUCCESS) {
            // ...
        }
    }
    // ...
}
```

### AndroidManifest.xml

##### [建议] activity 按照字典序排序
## API

### Handler