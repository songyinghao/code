# URL 设计规范

## 前言

写给后台开发人员参考。

## 规范

### 设计规范

##### [强制] URL 必须符合标准

##### [建议] URL 尽可能简短

##### [强制] URL统一小写字母加下划线的命名方式

所有参数命名也统一小写字母加下划线的命名方式。

```
foo.com/say_hello.html?user_id=123
```

##### [建议] 尽可能采用与技术无关的 URL

应使用技术无关的URI，即 URL 中不应该出现跟技术有关的单词（如 php、sevelet、cgi-bin 等等）。

原因：

1. 这些信息对用户来说是没有意义的（不提供有用的信息）。
2. 安全性。
2. 可维护。URI 不暴露服务器端使用的脚本语言，平台引擎，而这些语言，平台，引擎的变化也不会导致 URI 的变更。

提供静态内容服务时，应当隐去文件的扩展名。

```
// good
foo.com/topic
foo.com/topic.html
.do .action .jsp

// bad
foo.com/topic.jsp
foo.com/topic.do
foo.com/topic.action
```

##### [建议] 尽可能采用类似 REST 风格的 URL

```
foo.com/topic/1/answer
```

##### [建议] 网站的目录结构应该规范

小网站的目录结构示例：

```
{root}/
    asset/
        css/
        lib/
            /jquery
                jquery.min.js
            /bootstrap
                bootstrap.min.css
                bootstrap.min.js
        img/
        js/
    upload/
    ...
```


##### [建议] URL 应该对 SEO 友好

比如：

```
foo.com/article/how_to_study_seo
foo.com/article/35675424
```

上面的 URL 比下面的 URL 更利于 SEO 优化。

考虑到实现技术等各种原因，不做严格要求。