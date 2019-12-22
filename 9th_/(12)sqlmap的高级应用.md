[TOC]

![]((12)sqlmap的高级应用_files/e07e0331-d812-41ef-bbd2-b60767bfb164.png)
传递参数了:
![]((12)sqlmap的高级应用_files/cc2a19f4-0301-4fd2-b79b-a260d5c38969.png)


![]((12)sqlmap的高级应用_files/1076dca6-d5bb-49a9-a7ac-3981cd56fa9d.jpg)

登录一个网站,会把我的用户名和密码存于cookie里面;通过cookie确认身份;
只要获得admin这个用户名的cookie，再把它给sqlmap，就同样地获得了admin用户的身份;zenme 获得当前用户的身份,用burp suite!

## BurpSuite相关的
![]((12)sqlmap的高级应用_files/4f9be2c8-de07-4c64-92d0-989f87010254.jpg)

![]((12)sqlmap的高级应用_files/2849946e-8f98-417b-835d-9555f675bbe7.jpg)

![]((12)sqlmap的高级应用_files/f2d304e9-d67c-4c55-a3a9-6425aa253d64.png)

![]((12)sqlmap的高级应用_files/8007bf44-20b4-4a56-ba47-e23751a602c6.png)

先不抓包,像127.X...这样的回环地址的包burpsuite是抓不到的;
![]((12)sqlmap的高级应用_files/861c4721-3358-4a87-98e6-c8f33485798b.png)

![]((12)sqlmap的高级应用_files/f519c203-bd47-47b7-b9df-11bbd1aecb1f.jpg)

![]((12)sqlmap的高级应用_files/f3137f51-13ca-45c2-8ae2-4a9766db02c0.png)

admin,password
![]((12)sqlmap的高级应用_files/6629ce5e-3ce6-4074-ae57-3cebaa2cf449.png)

![]((12)sqlmap的高级应用_files/b45b9c74-b9d6-4765-a88b-b6d08f28a4ab.png)

![]((12)sqlmap的高级应用_files/37610cb7-e1bd-44dc-a9d0-bd0d19e56f9e.png)

获取其cookie：
![]((12)sqlmap的高级应用_files/72d864fc-1221-418a-a786-4ccac621c52e.jpg)

![]((12)sqlmap的高级应用_files/84bcc681-d561-481d-abfe-2590087c882e.jpg)

利用sqlmap进行post注入

![]((12)sqlmap的高级应用_files/4ba5a6b5-9200-433a-990c-29b4c7887ba8.jpg)

12'50"

![]((12)sqlmap的高级应用_files/ffcbc103-d00b-4252-865e-0fda4d225e60.jpg)

![]((12)sqlmap的高级应用_files/e083d50e-a51b-4119-9ecb-6aebcb18a6a5.jpg)

![]((12)sqlmap的高级应用_files/b4717f01-c52f-45c5-b059-86819f5780fe.jpg)

![]((12)sqlmap的高级应用_files/1733047a-c909-449a-8930-31538f653f77.jpg)

![]((12)sqlmap的高级应用_files/476c5b22-1d6c-469e-92bb-b71f13dbfdfa.jpg)


![]((12)sqlmap的高级应用_files/a7df99e0-de3c-42b6-a0a3-f15120452001.jpg)


