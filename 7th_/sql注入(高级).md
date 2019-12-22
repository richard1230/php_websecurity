[TOC]

![](sql注入(高级)_files/51c2c463-a4a0-442d-9d14-f9c9775cb1e0.jpg)

开启魔术引导(一般不建议采用,可能会造成可移植方面的 问题)之后，可以对所有的GET,POST和COOKIE传值的数据自动运行addslashes()函数;

关闭魔术引导:
![](sql注入(高级)_files/66a57b0c-e72e-4db8-a1af-1bbb26a140ec.jpg)

![](sql注入(高级)_files/eb32bb2a-4bdd-4141-a731-0a9f4d1fbe82.png)

high级别下的防御措施:

![](sql注入(高级)_files/82d27cef-a619-4202-8b55-0980a59769d2.jpg)

2利用is_numeric()函数判断你输入的 是不是 数字，如果输入的不是字符就不会往下执行!
3.把你输入的数据放于单引号内,作为一个字符型
![](sql注入(高级)_files/395bcee8-e7a2-4566-840d-911218639a26.jpg)


如何防御:

![](sql注入(高级)_files/b8558318-8c3b-47a9-a5cf-754dbcc28d65.jpg)
字符型注入里面最关键的就是单引号,怎么闭合单引号,你把单引号转义了,字符型注入就不存在了;

![](sql注入(高级)_files/cb313206-be94-4ce0-9adb-1955deac3435.jpg)
在WAF里面主要做过滤!云端防护也一样的原理！

