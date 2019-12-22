[TOC]

## document 对象的常用属性
- document.cookie,显示当前页面的cookie(访问当前页面的cookie)
```
<script>alert(document.cookie);
    </script>
```
- document.location,显示当前页面的URL

```
<script>alert(document.location);
    </script>
```

这里由于没有登录所以没有显示cookie!
![]((20)javascript语言基础_files/327beaa9-2046-4a63-89dc-75720c27a3ee.jpg)
![]((20)javascript语言基础_files/5bef941f-5e6d-4e60-8ca1-5af208e9686d.png)



![]((20)javascript语言基础_files/65a3c4ab-dfdf-4c97-9c53-74b7716e103c.png)
```
<script>alert(document.cookie)</script>
```
![]((20)javascript语言基础_files/ead61ee5-a561-4568-aba9-e2d2337b96cb.png)

![]((20)javascript语言基础_files/3e4f3036-94a5-4a83-ad32-a7c611188956.jpg)

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
<script>
document.write(document.cookie);

</script>

</body>
</html>

```

## locatio.href实现页面跳转
- 当页面整体跳转至另外一个页面上去


```
<script>
alert(document.location);
location.href = "www.51cto.com";
</script>

```

location.href可以简写成location


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
<script>
document.write(document.location)
location.href = "http://www.51cto.com";

</script>

</body>
</html>

```
![]((20)javascript语言基础_files/fa464d17-a9ae-4d02-91fc-004134d88734.jpg)

![]((20)javascript语言基础_files/177ab570-8855-414d-9493-d2acac8addbe.png)


![]((20)javascript语言基础_files/3daa3604-d767-4023-ae2f-6b6c39294778.png)

![]((20)javascript语言基础_files/6a1e7a44-7cfc-4210-a0b9-758c83cbb022.jpg)


## confirm语句
- 显示确认选择对话框,返回true或者false

```
<script>
    if(confirm("3>2？")==true)
    {
    document.write("正确");
    }
    else
    {
        document.write("错误");
    }
</script>

```

![]((20)javascript语言基础_files/53e1e343-b4f7-4749-9c09-46ba0f42e8a6.jpg)
![]((20)javascript语言基础_files/cd37662b-fcc2-4e8c-a6bd-fb2508137985.png)

![]((20)javascript语言基础_files/282a8cd1-aff7-4950-8429-7b011a3c6a1d.png)

