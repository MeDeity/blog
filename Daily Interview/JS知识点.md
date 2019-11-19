#### 常见的HTTP状态码
>HTTP状态码的英文为HTTP Status Code,状态码由3个10进制数组成,第一个10进制数代表状态码的类型,后两个数字代表详细的状态信息.

|分类|分类描述|
|-|-|
|1**|信息，服务器收到请求，需要请求者继续执行操作|
|2**|成功，操作被成功接收并处理|
|3**|重定向，需要进一步的操作以完成请求|
|4**|客户端错误，请求包含语法错误或无法完成请求|
|5**|服务器错误，服务器在处理请求的过程中发生了错误|


|状态码|状态码英文名称|中文描述|
|-|-|-|
|200|OK|请求成功。一般用于GET与POST请求|
|400|Bad Request|客户端请求的语法错误，服务器无法理解|
|401|Unauthorized|请求要求用户的身份认证|
|403|Forbidden|服务器理解请求客户端的请求，但是拒绝执行此请求|
|404|Not Found|服务器无法根据客户端的请求找到资源（网页）。通过此代码，网站设计人员可设置"您所请求的资源无法找到"的个性页面|
|405|Method Not Allowed|客户端请求中的方法被禁止|
|500|Internal Server Error|服务器内部错误，无法完成请求|
|502|Bad Gateway|作为网关或者代理工作的服务器尝试执行请求时，从远程服务器接收到了一个无效的响应|
|503|Service Unavailable|由于超载或系统维护，服务器暂时的无法处理客户端的请求。延时的长度可包含在服务器的Retry-After头信息中|


#### 是什么IE盒子模型、W3C盒子模型,他们有什么区别
![IE盒子模型以及W3C盒子模型](../screenshots/DailyInterview/20191119/box_model.png)
> 可以看到唯一的区别width的计算方式不一样,避免触发IE盒模型的方法是使用<!DOCTYPE html>声明，告诉IE采用W3C盒子模型即可



#### 以下JS定义中,哪个是立即执行函数 -5
```
A.function methodName(){
    console.log("methodName");
}

B.var methodName = function(){
    console.log("methodName");
}

C.function(){
    console.log("methodName");
}

D.(function(){
    console.log("methodName");
})()
```
> 以上从A到D 分别是函数声明、函数表达式、匿名函数、立即函数


#### 以下代码执行结果会输出什么内容-5
```
for (var i = 0; i < 5; i++) {
  console.log(i);
}
```
> 0 1 2 3 4 (基础)

##### 以下代码执行结果会输出什么内容-10
```
for (var i = 0; i < 5; i++) {
  setTimeout(function() {
    console.log(i);
  }, 1000 * i);
}
```
> 由于setTimeout会延迟执行,而此时for循环已经执行到5,因此输出为 5个5

#### 以下代码执行结果会输出什么内容-10
```
for (var i = 0; i < 5; i++) {
  setTimeout((function(i) {
    console.log(i);
  })(i), i * 1000);
}
```
> 由于setTimeOut(function,value),而即使运行函数不是function,因此相当于setTimeout(undefine, i * 1000);但是立即函数会立刻执行.因此会瞬间输出0~4.

##### 以下代码执行结果会输出什么内容-15
```
for (var i = 0; i < 5; i++) {
  (function(i) {
    setTimeout(function() {
      console.log(i);
    }, i * 1000);
  })(i);
}
```
> 以上涉及闭包知识,会输出0~4

##### 以下代码执行结果会输出什么内容-15
```
for (var i = 0; i < 5; i++) {
  (function() {
    setTimeout(function() {
      console.log(i);
    }, i * 1000);
  })(i);
}
```
> 由于闭包内没有对i保持引用,会输出5个5

##### Promise是什么东西?

#### CSS相关
##### CSS中 display 有哪些属性值,他们的作用是什么
|属性|备注|
|-|-|
|inline|默认。此元素会被显示为内联元素，元素前后没有换行符|
|block|此元素将显示为块级元素，此元素前后会带有换行符。|
|none|此元素不会被显示（隐藏）|
|inline-block|行内块元素。（CSS2.1 新增的值）|
|list-item|此元素会作为列表显示|
|table|此元素会作为块级表格来显示（类似table），表格前后带有换行符|

##### display:none 与 visibility:hidden 的区别是什么？
>display : none 隐藏对应的元素，在文档布局中不再分配空间
visibility:hideen 隐藏对应的元素，在文档布局中仍保留原来的空间

##### 如何水平并且垂直居中一张背景图
> 设置 background-position:center;


#### 框架相关


扩展链接(以上内容来源于)
[最佳实践-Liril-Excuse me？这个前端面试在搞事!](https://zhuanlan.zhihu.com/p/25407758)
[CSS经典面试题](https://juejin.im/post/5cc59e41e51d456e62545b66)
[前端面试整理](https://www.one-tab.com/page/DUzvPkoFTy67kYevpvS2WQ)