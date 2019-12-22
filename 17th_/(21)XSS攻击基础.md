[TOC]

## firefox浏览器的设置

![]((21)XSS攻击基础_files/020ecb43-a11b-47c4-a399-54dae5b06fcc.png)

![]((21)XSS攻击基础_files/81bcd193-d18e-47d7-8594-fc6b40443176.png)

![]((21)XSS攻击基础_files/9249733d-ae49-47e8-934b-82e0fa594bc8.png)

![]((21)XSS攻击基础_files/ba71e827-2c23-4b43-84c5-73cea4ac9270.png)
## 定义

![]((21)XSS攻击基础_files/af935d63-c8e7-4344-aa0c-ccc729811249.jpg)
攻击者在被攻击的web服务器网页里面嵌入 恶意脚本,通常是用Javascript编写的恶意代码,当用户使用浏览器访问被嵌入的恶意代码的网页的时候,恶意代码将会在用户的浏览器上去执行;

Xss属于针对客户端的攻击,受害者最终是用户;网站管理人员也是用户之一,攻击者可以通过XSS假冒管理员身份对网站实施攻击;

![]((21)XSS攻击基础_files/debab41e-ce48-4bdc-aa88-8872e2e05595.jpg)
上图里面的留言板里面就是一个有xss的漏洞的钓鱼;只要一查看这个留言的链接,恶意代码就会在这个人的浏览器里面执行了;
而后可以获取他的信息进而把其信息发送给 攻击者(一般是cookie);而后可以假冒他的身份去登录；

## 危害


![]((21)XSS攻击基础_files/c28161aa-aac5-4b8e-a952-dc48fccd91ee.jpg)


## 环境
![]((21)XSS攻击基础_files/548c4c43-efeb-4bff-91e1-9469b68af5d7.jpg)

不要和那个appserve安装在一台机器上面!!!
![]((21)XSS攻击基础_files/249b04e2-882a-4370-aeeb-521c1037e19d.png)

## 反射型XSS
![]((21)XSS攻击基础_files/9a1d6e2f-9868-491d-8166-1d6490d93618.jpg)
先安装一下NPMserv;
这个需要放于根目录下面,不要放于桌面！

![]((21)XSS攻击基础_files/b4590c99-a22a-4070-8229-240746375d05.jpg)
```
<form name="inout" action ="xss1.php" method="post">  //将表单提交给xss1.php这个页面;方法是post方法
<p>请输入姓名: <input type="text" name = "uname"></p>
//文本框名字叫uname
<p><input type = "submit" value="提交"></p>//提交按钮
</form>
```
![]((21)XSS攻击基础_files/d188e78e-bef0-48e5-9336-613388372dcb.jpg)
```
<?php
$username = $_POST['uname']; //接收数据
echo <p>你好，".$username."</p>//注意这里的.(点),一个都不能少！！！还有分号！一定要是英文状态下的,中文会出错！！
?>
```
![]((21)XSS攻击基础_files/66918597-b050-4798-bc61-0b491bff774b.png)
![]((21)XSS攻击基础_files/d238eefd-bc26-415c-9049-89bdc7bcda8a.png)

这里提交数据之后，不是去数据库里面做查询;
**XSS攻击必须得有用户输入的地方**,才可能有跨站漏洞！
在这里输入一段javascript代码,看能不能被执行,可以执行的话就是XSS攻击！

![]((21)XSS攻击基础_files/871ec668-b0dc-4a41-8d15-e12fca8de465.png)

![]((21)XSS攻击基础_files/fbcc089c-99ee-46eb-b4ce-55cec7834e1e.png)
方框里面代码:
```
<script>alert("hi")</script>
```
这里是有漏洞的,为什么有漏洞 ,查看源代码:
![]((21)XSS攻击基础_files/16a936c8-49e6-41b8-ad66-082591a557b6.png)
**刚才提交的代码直接被带入浏览器执行了**！
黑客输入的数据又在浏览器上执行了,这叫跨站!
### 例2
![]((21)XSS攻击基础_files/4781a97e-86a0-48e5-abc7-799fde6549b7.jpg)
```
<form action="" method= "get"> //action后面的空白表示提交给当前页面
        <input type="text" name="uname"><br />
        <input type="submit" value="ok">
</form>
<hr/>    //表示水平分割线
<?php
    $username = $_GET['uname'];//这里是中括号,别写错了！！！
    echo "<p>hello ." .$username."</p>"

?>
```

![]((21)XSS攻击基础_files/ef9a1559-0712-4fc8-a674-af6d04deafe6.jpg)


![]((21)XSS攻击基础_files/b24c4879-8ff8-4bd3-a3fe-9d155730bbf7.jpg)

![]((21)XSS攻击基础_files/a3974b61-660f-48b9-b7a2-03c97bdf26dd.jpg)

![]((21)XSS攻击基础_files/cd35e107-fb56-4c90-8230-6ec36d392f73.png)

![]((21)XSS攻击基础_files/47795896-53e9-41ed-8ff7-c9524bf0d54e.jpg)
方框里面:
```
<script>alert("hi!!!")</script>
```
(12'39")

![]((21)XSS攻击基础_files/2a7fa0a9-458e-4f1e-b0e1-8c5debe8d2d0.png)

这个url可以发送给其他人,其他人点击这个url之后 也会实现这个效果！！
这里这个url=`http://192.168.0.104/xss2.php?uname=%3Cscript%3Ealert%28%22hi%21%21%21%22%29%3C%2Fscript%3E`（13‘30“）(ip可能会有所变化)
![]((21)XSS攻击基础_files/c36008d5-afe6-4b70-bd03-961cdc9e9fb4.jpg)
反射型XSS只是对当前URL有限;(它不持久),很难利用
## 存储型XSS
把你提交的代码直接提交至数据库里面去了;只要有用户它正好看的页面就从数据库里面把你那些代码调出来;你这些代码就会在页面上执行！攻击威力大,访问这个页面的人都有效!
![]((21)XSS攻击基础_files/39ac5c11-9478-4779-98c4-48ffc6f96bba.jpg)

![]((21)XSS攻击基础_files/3f76dfeb-72be-4eaa-8f93-dae287af3dd6.jpg)
