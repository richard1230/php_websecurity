[TOC]

## 定义

![]((19)javacript语言基础_files/7b413451-b3d7-4556-922e-66d4aceb32a9.jpg)
javascript就是对html在功能上的扩展;
XSS攻击的对象是客户端;
![]((19)javacript语言基础_files/4fbf9dc3-b4a6-41e0-96d6-375103a0884c.jpg)

- 所有的javascript语句必须包含在`<script>...</script>`标签中;
- 每行javascript语句必须以";"表示结束(其实也可以不加,不像php);(html没有必要)
- document是一个对象,指的是当前网页,write是其动作；
- document.write就是让当前的网页执行write动作;将()里面的内容写入到页面当中去;
## 例1


```
<html>
<head>
<title>
JavaScript Test
</title>
</head>

<body>
<script>
document.write("Hello,WOrld");
</script>
</body>
</html>
```
![]((19)javacript语言基础_files/d02e330d-0603-4c4b-8df0-bca4c33ec205.jpg)

![]((19)javacript语言基础_files/d95caad5-2cf2-4f97-a24b-a638b7ad9490.png)

![]((19)javacript语言基础_files/73a2544d-0a13-4344-ae94-7aaabe284a55.jpg)

javascript里面不能对变量直接赋值;
```
<html>
<head>
<title>
JavaScript Test
</title>
</head>

<body>
<script>
var hack = "hack";
document.write("<h1>hello,"+name+"</h1>");
</script>
</body>
</html>
```
- php里面是可以直接赋值给变量的；而js里面是不可以的;
- 输出的内容如果在双引号里面就原样输出;
- js里面的`+`为连接符号;(php里面为`.`)
- //表示单行注释,多行注释为:`/*......*/`


![]((19)javacript语言基础_files/c35dacc9-c761-40bb-80fc-5345c1af1522.jpg)

![]((19)javacript语言基础_files/ed30a58b-4f0d-4f30-b819-d56307fd672a.png)


## 对某事件作出反应

![]((19)javacript语言基础_files/df586756-b2e9-4b29-bc1d-4561e7bd67b9.jpg)
用js对某个事件作出反应:
![]((19)javacript语言基础_files/c4720ef9-1467-489f-be2f-131324fc0b19.png)
(注意:这里没有把form放在script里面)
![]((19)javacript语言基础_files/6b552ef8-da58-493e-993d-23e26835828b.png)
## 常见事件
![]((19)javacript语言基础_files/96693fd0-9468-47d1-800a-69638dd718bb.jpg)

| 事件处理程序  | html标签  |  触发时机 |
| ------------ | ------------ | ------------ |
| onClick  |all元素   |   当用户点击里类似按钮这样的窗体元素后触发|
| onError  |` <img>`  |  加载图像过程中发生错误时触发 |
| onLoad  | `<body><img><object>`  | 文档,图像或对象完成加载是发生  |
| onSubmit  | ` <form>` |  用户 提交窗体时触发 |

### onError

正常 情况下:
![]((19)javacript语言基础_files/1619ef09-b821-4da6-8240-cb283382f7fe.jpg)

![]((19)javacript语言基础_files/9fe6398c-2400-49e7-90f3-c7adce2b58ef.jpg)

非正常情况下:
```
<html>
<head>
<title>
JavaScript Test
</title>
</head>

<body>

<img src=aaa onError="alert('helloworld')">

</body>
</html>
```
![]((19)javacript语言基础_files/69b55523-2c70-4c95-84b6-7cddca2062fd.png)

```
<html>
<head>
<title>
JavaScript Test
</title>
</head>

<body onLoad ="alert ('hello')">
<!--
<img src=aaa onError="alert('helloworld')">
-->

</body>
</html>
```
![]((19)javacript语言基础_files/1d55efb5-dfc5-4c99-9358-411459419f50.png)
只要网页以加载完毕,就弹框!

### 加载外部js
![]((19)javacript语言基础_files/af508ae5-d81f-481f-a468-687f0f1b3125.jpg)

如果代码比较多可以单独将其放在一个js文件里面;
有利于反复调用！
#### 例子
![]((19)javacript语言基础_files/e66f145b-f13e-4b86-9bc4-c4b747794c85.jpg)


![]((19)javacript语言基础_files/820a2be7-ff3f-4b02-bdad-b8c803652ae5.jpg)

```
<html>
<head>
<title>
JavaScript Test
</title>
</head>

<body >
<!--
<img src=aaa onError="alert('helloworld')">
-->
<script src="/js/test.js">

</script>

</body>
</html>
```

![]((19)javacript语言基础_files/42bbb475-ffeb-41d0-b82a-a1dc0cfd6be9.png)

还可以加载另外一个服务器上面的js文件
