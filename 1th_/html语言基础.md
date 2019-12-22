[TOC]

```
<html>
<head>

<title>测试网页</title>

</head>
<body>
这是我的第一个html网页
</body>


</html>

```
另存为html格式;
![](html语言基础_files/ada6c98e-7a9e-4048-9377-cd43c33b8a5c.png)


![](html语言基础_files/6323d8f1-c0bc-457b-89df-2a9d95273c16.png)

右击查看源代码:
![](html语言基础_files/c8a885c2-b18e-4f1b-be78-2cc9ea0c8fc0.png)

![](html语言基础_files/9797ed6c-4276-40bf-9d30-ea63438d80e9.jpg)

下面讲body里面的:
![](html语言基础_files/86d73d4c-4f95-4d93-b7aa-f769fd99f2e9.jpg)

![](html语言基础_files/a03a4db7-9f6b-497e-81e8-0dcb254949c0.jpg)

![](html语言基础_files/9817342e-dbb2-42e1-8d3d-77a22da1b592.jpg)
## 分段:（两段之间有空行）
![](html语言基础_files/2268d8ae-44dc-4eab-b175-15795ab66eee.jpg)

![](html语言基础_files/1f9183c0-4fdc-4462-a096-0e538012e0ba.png)

## 换行标签:(两行之间没有空行)
![](html语言基础_files/134731ed-62f3-40f6-9195-bc6b8d305199.jpg)

![](html语言基础_files/25d11fff-dd64-4a77-b4fc-d98b16ccbb1b.jpg)

![](html语言基础_files/c3fa29e2-a36b-431f-baac-0528eef3edea.png)
## 原样输出标签:
![](html语言基础_files/241f353e-fd34-4f64-a53d-a42db769c7d5.jpg)

![](html语言基础_files/47b25d9a-2868-4214-8e22-923320c2bd29.jpg)

![](html语言基础_files/fc94a881-8b8d-42ad-a2ab-79e571eea5cf.png)

## 注释:
![](html语言基础_files/bd1d1e4c-ccdb-4f7f-a7fd-bfbf1119141b.jpg)

![](html语言基础_files/a2a1d897-8e8e-4b96-bcaf-0b6c5bd3c62d.jpg)
![](html语言基础_files/c642c361-46bc-4b39-a4bb-9d7d9110d099.jpg)

## 图片:
![](html语言基础_files/717a3f52-3f96-4c70-98bd-766225f83843.jpg)

![](html语言基础_files/bda82b35-035b-4039-b641-9022622c7e31.png)
![](html语言基础_files/09dc9dea-bc88-44bd-a8c5-eecc60225307.png)

![](html语言基础_files/0cd7f00a-d102-494d-bee1-b515437e0447.jpg)
```
<img src="/image/1.jpg" alt="测试图片">
```
这里面表示了一个相对路径`/image/1.jpg`表示根目录(这里指的是www这个文件夹)下面的image文件夹下面的1.jpg这个图片
![](html语言基础_files/a0dee3dd-8efe-4db9-8e75-c1002021c012.jpg)

![](html语言基础_files/4c79ef33-73fc-4e30-8380-fb3c0d1e5b69.jpg)
![](html语言基础_files/5d170d9f-93dc-4eed-8275-f1236d5e77a2.png)
![](html语言基础_files/3f58154e-1f3d-40b0-bac9-b4e4745f1f87.jpg)

## 超链接
![](html语言基础_files/03713431-9702-407a-81e8-35c8e617c20d.jpg)
href属性指定url；
以上面图里面的例子为例:将文字描述这4个字嵌入网页里面,一点这四个字,就跳转至url所指定的页面;
![](html语言基础_files/61718666-29f1-4c2b-8015-198f3e7b411d.jpg)
图像超链接:
![](html语言基础_files/2dde6542-d223-4d6e-b863-1f5fe757a9af.jpg)
![](html语言基础_files/5fb8e3a4-5a9f-4cfb-be27-4c7f6416a3b1.png)

![](html语言基础_files/8af966d1-4edd-476b-b876-4a2ab3ad1a4c.jpg)
## 表单
场景:登录界面
![](html语言基础_files/0e06678b-3836-4b00-98ff-7992cacdd3ff.jpg)

![](html语言基础_files/eb3ad946-3aeb-4514-98b9-a3cd37850ddd.jpg)
表单用于接收用户输入的数据,再将其发送给服务器,表单包括文本框和按钮;表单有一些子标签（最常用的是input标签）,每个子标签 又能实现一些功能;
action属性后面跟一个页面,“UserLogin.php”，这个页面的作用是接收通过表单传给服务器的数据,（表单作用是接收数据传给服务器),数据传给服务器以后谁来处理这些数据,所以这里定义了一个动态的 php页面,由这个页面来验证用户名和密码是否正确(一般需要用户名和密码的,用户名和密码在服务端那边判断是否正确);

method是方法,你要通过什么方法把表单的数据传给服务器,客户端传数据给服务端的方法一般有两种, get和post(传输数据量大用post，一般表单用post),一般传给服务器的数据在url显示出来的是get(会有 一个？,比如？username=...),而post传出的数据是在地址栏里面看不到的(5")
![](html语言基础_files/0b82905c-1d80-4775-b787-4c466eac3170.jpg)
(表单主要是一些文本框和按钮)

input标签可以用来实现文本框,也可以实现按钮,是什么类型的需要看后面的type,text类型的是一个文本框,username是给用户名冒号后面的文本框定义的一个名字;why?我们输入的信息都需要传给UserLogin.php这个网页页面去处理(在这个例子里面);UserLogin.php这个网在一上来就要接受通过表单传给它的数据,接受的时候怎么知道那个数据是用户名,密码,那么从name是username文本框传过来的数据就是用户名,从名字是password的文本框传过来的数据就是密码;所以必须给每个文本框起个名字,这样接收方在服务器那儿接受的时候就能区分!
第三行是一个提交的按钮,一点这个按钮,数据就传出去了,这里提交按钮的名字叫submit,名字可以随便起,但是类型的确定的(这里有text，password,submit三种类型)!
submit显示出来的文字就是value的值:(value后面是什么,后面按钮上面就显示什么)
![](html语言基础_files/9fe1cd26-b127-42da-9e5a-4d01a6509a91.jpg)

![](html语言基础_files/205dd2f5-4628-4e70-81ba-f18784b820cd.jpg)

&nbsp 代表一个空格:
下图表示两个按钮之间有三个空格;
![](html语言基础_files/4ade42ff-3ec0-4eeb-bfd0-a6d4c7ce4215.jpg)
![](html语言基础_files/8a32678d-c391-41d2-9f13-8f15b6e72aba.png)
重置按钮功能是把名字和密码清0,服务器那里不接受他的数据,所以这里的名字有没有无所谓的!但是value必须有！
## 浮动框架
可以在一个页面里面显示其他网页的内容!
![](html语言基础_files/49c536a7-9190-40ed-81a4-fcab3cdc2dcc.jpg)

![](html语言基础_files/39ebc85e-9075-4cf6-b4c4-2e9da0df970a.jpg)

![](html语言基础_files/2b143e22-9360-4399-9c90-99ef106ac0dd.png)
这里面的宽度和高度是自己定义的;
这种方式可以网页挂马,可以把木马放在服务器上,src后面的url可以是木马的地址;把木马的地址以iframe的方式插入到正常的网页里面;人家一访问这个网页,就会主动访问木马网页,把木马页面设置一下，让其一访问就自动下载木马,可以将其高度和宽度设置为0,在设置frameborder=0即边线为0


