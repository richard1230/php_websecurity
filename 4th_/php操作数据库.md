[TOC]

![](php操作数据库_files/456f2979-2f33-4577-845b-9fac1ea9dd78.jpg)
```
mysql_connect("localhost","root","123");    //通过php连接上Mysql,Mysql和网站在同一台服务器上，这里可以直接连接服务器自己;
Mysql_select_db("test")//打开了这个数据库之后,选择要操作的数据库(就是选择要操作mysql里面的那个数据库);
mysql_query("set name utf8")//设置客户端和连接字符集；
通过数据库进行增删改查
mysql_close($conn);//释放连接资源

```
![](php操作数据库_files/11befc75-cbc5-40ca-89f0-08c867833a6b.png)
常见的一些命令如上;
![](php操作数据库_files/716fa285-0206-4f26-9fca-9d4ee7834018.png)

创建一个表:
![](php操作数据库_files/20caabf7-c2e1-439e-87c8-26683351dbc8.jpg)
![](php操作数据库_files/d1de1632-0616-495a-b93b-1a5b14346322.png)
## 建表
建立一个表的一般步骤:
```
1.use 数据库名
2.create table 表名
```
## 增数据
往表格里面添加数据:
![](php操作数据库_files/c4cdca7f-6ffd-4914-a416-1e1413396d90.png)
![](php操作数据库_files/ad5aa359-22d2-4d94-bc71-911eb0c5d96d.png)
## 查数据
查询数据:
![](php操作数据库_files/14098eb9-a65a-4552-93f6-77d189215d6a.png)

现在正确的用户名和密码就两个(存于数据库里面)
而后 通过php动态网页来接收你的用户名和密码而后在数据库里面再判断你的这个用户名和密码对不对,这就是一个完整的程序.

![](php操作数据库_files/31e6f67a-129b-42b4-ac60-8a75d2e426a1.jpg)

```

$username = $_POST['username'];//这里是接收数据
    $password = $_POST['password'];
    
    $conn = mysql_connect("127.0.0.1","root","123"); //连接Mysql，并把连接的结果赋值给一个变量conn
    mysql_select_db("test");//选择打开test这个数据库
    mysql_query("set names utf8");//设置字符集
    
    $sql = "select * from hack where username='$username' and password='$password'";//在hack表里面查询符合这两个内容的:1.username='$username'，2.password='$password',由于单引号里面的数据是在双引号里面的，所以这里单引号里面的数据会被解析，他们都是文本型数据,到这里只是把查询的语句复制给这个变量，何时调用这个变量才执行这个语句;这里其实就是把要执行的语句复制给一个变量！！！
    $res = mysql_query($sql，$conn);//mysql_query这个函数式专门执行sql语句的,这句话的意思是执行存放于$sql这个变量里面的这个sql语句,并把执行的结果存于$res这个变量，$conn表示在哪个数据库连接里面执行sql语句,$res表示result，右边返回的结果是0行,1行,2行等等,通过mysql_query函数来执行上面这个语句,并把结果赋给左边这个变量``

    if (mysql_num_rows($res)!=0){
    echo "登录成功";
    }else{
    echo "登录失败";
    
    }//row:列;如果$res里面存放了不是0行,那么就证明查到结果了,这只是判断方法之一
mysql_close($conn);
```