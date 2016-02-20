 [TOC]

# REST 规范

## 前言

REST 风格的 Web API 接口须遵守 REST 规范。

## 路径规范

##### [强制] URI 中不能包含动词

REST是面向资源的，每一个URI对应一种资源，设计时应该全部使用名词。

```
// good
GET  https://api.example.com/v1/products

// bad
GET  https://api.example.com/v1/get/products
```

##### [强制] 使用名词复数形式而不是单数形式。

资源都是每一类信息的集合，采用复数的形式更符合实际，更规范。

##### [建议] API 应该满足 HATEOAS 约束

HATEOAS（Hypermedia as the Engine of Application State，超媒体作为应用状态的引擎）

例子：[api.github.com](https://api.github.com/)

```
{
  "id": 711,
  "manufacturer": "bmw",
  "model": "X5",
  "seats": 5,
  "drivers": [
   {
    "id": "23",
    "name": "Stefan Jauker",
    "links": [
     {
     "rel": "self",
     "href": "/api/v1/drivers/23"
    }
   ]
  }
]
}
```

## 使用标准方法

仅使用以下四个请求方法：

* GET：获取资源
* PUT：创建资源
* POST：更新资源
* DELETE：删除资源

需要注意的是，Get方法和查询参数不应该涉及状态改变，即GET方法仅仅是获取数据，不会对数据内容产生影响。

```
// good
GET  http://api.example.com/v1/products ---------------获取所有产品的信息
 
GET  http://api.example.com/v1/products/1 ---------------获取ID为1的产品的信息

// bad

DELETE  http://api.example.com/v1/products/1 -------删除ID为1的产品的信息
```

##### [建议] 还有一点，建议使用子资源表达关系

如果一个资源与另外一个资源有关系，使用子资源：

``` 
// good
GET /zoos/1/pandas
GET /zoos/1/pandas/1

// bad
GET /zoos/1/pandas?id=1
```



## 条件查询

##### [建议] 根据业务，为集合提供过滤、排序、选择和分页等功能

由于这些条件限制不属于资源，这些参数必须写在 URI 的问号后面

```
// good
GET /cars?color=red
GET /cars?seats<=2

// bad
GET /cars/red
GET /cars/seats/2
```



### 排序

##### [建议] 统一使用 sort 作为参数名。

##### [建议] 需要对多个字段进行排序时，字段之间用英文逗号分隔（,）。

多个字段排序时，先按第一个字段进行排序，再按第二个字段进行排序，依次进行。

字段默认按升序排序，降序则在字段名前面加 `-`。

``` 
GET /cars?sort=color,-price
```

### 分页

##### [建议] 使用 limit 和 offset 做为参数名。

```
GET /cars?offset=2&limit=30
```

##### [建议] limit 和 offset 应该有默认值。

通常默认 limit=20，offset=0。这样的话，如果没有指明 limit 和 offset 参数，返回符合条件的前 20 条数据。

### 字段

允许获取目标资源的部分字段。降低网络流量，提高API可用性。

* 使用 fields 作为参数名，表示需要哪些字段。
* 使用 filter 作为参数名，表示不需要哪些字段。

字段之间用英文逗号分隔（,）。

```
GET /cars?fields=id,name,price,description
GET /cars?filter=description
```


##### [强制] 无状态通讯

服务器不保存客户端的转态。每次请求必须包含应用中所有的状态信息。

这样设计的好处是： 
1. 不同的服务器的处理一系列请求中的不同请求，提高服务器的扩展性。
2. 由于是无状态通讯，相同的请求返回的结果总是一样的，可以利用缓存来提高响应速度。

##### [强制] 在 URI 中加入版本信息

API的设计必须考虑版本，否则后期的升级和维护是个灾难性的问题。

版本信息显式地写在 URI 中而不是将版本号放在 HTTP 头信息中。

这种做法的好处是，方便、直观。

采用 v + 整数的版本号，避免小数点。

```
// good
https://api.example.com/v1/books

// bad
https://api.example.com/version1/books
https://api.example.com/v1.1/books
https://api.example.com/books?v=1
https://api.example.com/books?version=1
``` 


## 资源的表现形式

##### [建议] 除非特殊情况，API 返回 json 格式的数据而非 XML

一个资源可以有多种形式的表示，例如json、xml、rss等。

关于使用json还是xml，网上颇有争议。个人建议使用json，其优点就不多说了。当然，有些特殊情况还是xml更具优势。

如果需要返回多种资源，在HTTP-Header中指定。

Content-Type 定义请求格式。

Accept 定义系列可接受的响应格式。

## 错误处理

##### [强制] 当请求失败时，系统必须返回相关的错误提示信息

##### [强制] 错误信息必须和成功返回时的数据相同的表现形式

比如响应成功返回的数据是 json 格式的，那么错误信息应该也是 json 格式的。

禁止返回 404、500 之类的错误页面或是返回跳转后的其他页面。

##### [建议] 错误信息应该返回状态码和详细的错误描述

可以采用 HTTP 协议的状态码，也可以采用自定义的状态码。

400系列的表示客户端错误，500系列的表示服务端错误，通常用大于 1000 数表示自定义的错误码。

```json
{
    "code": 404,
    "message": "resource is not found",
    "description": "More details about the error here"
}
```

常见 HTTP 状态码：

* 200 ok - 成功返回状态，对应，GET,PUT,PATCH,DELETE
* 201 created - 成功创建新的资源。
* 304 not modified - HTTP缓存有效，客户端使用缓存数据。
* 400 bad request - 请求无效。
* 401 unauthorized - 未授权。
* 403 forbidden - 服务器已经理解了请求，但是拒绝服务或这种请求的访问是不允许的。
* 404 not found - 请求的资源不存在
* 405 method not allowed - 该http方法不被允许。
* 410 gone - 这个url对应的资源现在不可用。
* 415 unsupported media type - 请求类型错误。
* 422 unprocessable entity - 只有服务器不能处理实体时使用，比如图像不能被格式化，或者重要字段丢失。
* 429 too many request - 请求过多
* 500 API开发者应该避免这种错误。

```

```



##### [建议] 错误信息与响应成功时返回的数据应该保持相同的格式

这样做方便客户端解析处理。

比如请求成功时

```
{
    "code": 200,
    "message": "",
    "data": {...}
}
```

请求错误时

```
{
    "code": 404,
    "message": "resource is not found",
    "data": null
}
```

## 安全性

##### [建议] 推荐使用 OAuth 2.0 进行权限控制
 
##### [可选] API 采用 HTTPs 协议而不是 HTTP 协议

居于安全性考虑。
