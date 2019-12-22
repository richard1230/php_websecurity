[TOC]

## 定义

![]((29)CSRF攻击介绍与实施_files/7f43d040-0133-4046-b956-1d035b4f853d.jpg)
1.登录正常网站A
2.通过登录验证,在用户C的本地产生正常网站A的Cookie;
此时再去访问网站B(被黑客控制的);黑客通过这个网站向用户C发出了一个请求,这个请求是 访问网站A(让用户C访问A,用户自己是不知道的,而A则认为这是C的正常请求,比如我要转账,我要消费,它一看会话建立了,身份通过验证了;而且就是从用户C这里发出的，而后就执行操作;)

用户C带着 B网站发出的请求带着A网站的cookie访问A;A就认为这是一个正常的请求;A就根据用户的权限处理由B网站发出的请求;黑客句实现了会话劫持的目的;
这个过程里面网站A是有CSRF的漏洞的;
有些网站后台 具有创建管理员账号(或者修改管理员密码这样的功能)这样的功能，要想访问这个页面,得有管理员权限才可以,现在黑客他就想创建管理员 账号,可以通过CSRF让管理员(如果他正在登录网站管理后台)，管理员访问了黑客网站,黑客网站通过管理员发出一个请求,让其创建一个管理员账号;或者说把管理员账号改了,这个请求通过管理员登录后台！

## 实战
![]((29)CSRF攻击介绍与实施_files/f2fabe5f-a247-40c7-9993-39cb8fd814d0.jpg)

![]((29)CSRF攻击介绍与实施_files/1a43e3f0-75c5-4aca-83f9-181a4d91dc48.png)

![]((29)CSRF攻击介绍与实施_files/75c7a3e3-a776-482c-83ee-157a74bddcc5.png)

![]((29)CSRF攻击介绍与实施_files/4c2b15f6-c63f-4138-84b6-a49363d7ea13.png)
可以看到其密码用md5加密了!
下面修改密码:(为123)
![]((29)CSRF攻击介绍与实施_files/7bd9ffc6-ad6a-4088-866d-b7e47685044d.png)

发现其已经改了:
![]((29)CSRF攻击介绍与实施_files/5f631fff-4de5-480a-be43-aecdfb813c40.png)


这里CSRF的攻击目的就是更改dvwa的密码;
这里将其url复制下来:
```
http://192.168.2.59/dvwa/vulnerabilities/csrf/?password_new=123&password_conf=123&Change=Change#
```
这里用的是get方法传密的;
`password_new`和`password_conf`(这是确认confirm)
其实这里可以直接把这个url修改也可以，把123对应的几个数字改一波即可！！！
先以管理员权限登录,
![]((29)CSRF攻击介绍与实施_files/c47da062-6e46-4e60-b76b-69e92aa08f28.png)

下面将这个链接直接发给管理员让其点击:
```
http://192.168.2.59/dvwa/vulnerabilities/csrf/?password_new=abcd&password_conf=abcd&Change=Change#
```

![]((29)CSRF攻击介绍与实施_files/1ac469d6-9ce5-4357-89f0-d4237e3f8232.png)

![]((29)CSRF攻击介绍与实施_files/bc624cb7-ceb1-4c62-9cd9-866c414af095.png)
发现密码改了,这就是一个典型的csrf攻击！
前提:
1.受害者确实已经登录网址A，并与之建立会话
2.A有这个漏洞
3.受害用户访问这个链接
![]((29)CSRF攻击介绍与实施_files/4fd4c527-2128-43df-ae18-4170d84699dd.jpg)


![]((29)CSRF攻击介绍与实施_files/2e7104cb-2f90-47e4-beae-2cf06b78a89e.jpg)

![]((29)CSRF攻击介绍与实施_files/7ac0205a-97df-44e3-aaec-6f9fdb110fd1.jpg)
```
<script src="xxx" >

        </script>

```
这是调用外部 js链接；
XSS与CSRF结合其实就是将xss里面的恶意js设置为修改你的登录密码等恶意行为！(这个方法有一个好处：会神不知鬼不觉改你的密码)
如下:
```
<script
src = "http://192.168.2.59/dvwa/vulnerabilities/csrf/?password_new=123456&password_conf=123456&Change=Change#"
></script>
```

![]((29)CSRF攻击介绍与实施_files/661a0d7b-aa42-4539-93a8-333cbc8b06d5.png)

![]((29)CSRF攻击介绍与实施_files/122ae3e7-5eb2-4524-9cc7-d5a76f9d68f5.png)

![]((29)CSRF攻击介绍与实施_files/d913104c-8523-444e-8cf5-c2e96cd3a2a3.png)

![]((29)CSRF攻击介绍与实施_files/77020dc1-d093-4319-918a-68b644df1dad.png)
而后提交;
![]((29)CSRF攻击介绍与实施_files/d8db5442-e329-4a7e-b8a5-625f6ae99087.png)

重新打开一个页面；
![]((29)CSRF攻击介绍与实施_files/a090de36-37e6-4ba3-819c-7607cf196f97.png)
发现其密码是改变了的！
![]((29)CSRF攻击介绍与实施_files/94d75210-1a7b-461c-972f-a739d318fc94.png)


