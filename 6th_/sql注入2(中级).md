[TOC]

![](sql注入2(中级)_files/24b05cc9-8e0b-46c8-9a96-947aba718748.jpg)

怎样防护SQL注入,用户的一切输入都是有害的----》过滤:
低等级下:
![](sql注入2(中级)_files/89e01389-5c21-45a1-b108-c8f4a3e2b78f.png)
调整为中级之后 就不行了:
查看源代码:
view source:
再次点击 compare：
低级:
```
<?php    

if(isset($_GET['Submit'])){
    
    // Retrieve data
    
    $id = $_GET['id'];

    $getid = "SELECT first_name, last_name FROM users WHERE user_id = '$id'";
    $result = mysql_query($getid) or die('<pre>' . mysql_error() . '</pre>' );

    $num = mysql_numrows($result);

    $i = 0;

    while ($i < $num) {

        $first = mysql_result($result,$i,"first_name");
        $last = mysql_result($result,$i,"last_name");
        
        echo '<pre>';
        echo 'ID: ' . $id . '<br>First name: ' . $first . '<br>Surname: ' . $last;
        echo '</pre>';

        $i++;
    }
}
?>
```

中级:
```
<?php

if (isset($_GET['Submit'])) {

    // Retrieve data

    $id = $_GET['id'];
    $id = mysql_real_escape_string($id);

    $getid = "SELECT first_name, last_name FROM users WHERE user_id = $id";

    $result = mysql_query($getid) or die('<pre>' . mysql_error() . '</pre>' );
    
    $num = mysql_numrows($result);

    $i=0;

    while ($i < $num) {

        $first = mysql_result($result,$i,"first_name");
        $last = mysql_result($result,$i,"last_name");
        
        echo '<pre>';
        echo 'ID: ' . $id . '<br>First name: ' . $first . '<br>Surname: ' . $last;
        echo '</pre>';

        $i++;
    }
}
?>
```

高级:
```
<?php    

if (isset($_GET['Submit'])) {

    // Retrieve data

    $id = $_GET['id'];
    $id = stripslashes($id);
    $id = mysql_real_escape_string($id);

    if (is_numeric($id)){

        $getid = "SELECT first_name, last_name FROM users WHERE user_id = '$id'";
        $result = mysql_query($getid) or die('<pre>' . mysql_error() . '</pre>' );

        $num = mysql_numrows($result);

        $i=0;

        while ($i < $num) {

            $first = mysql_result($result,$i,"first_name");
            $last = mysql_result($result,$i,"last_name");
            
            echo '<pre>';
            echo 'ID: ' . $id . '<br>First name: ' . $first . '<br>Surname: ' . $last;
            echo '</pre>';

            $i++;
        }
    }
}
?>
```

对比低级和中级的,发现其 区别:
中级里面多了下面一句:
```
$id = mysql_real_escape_string($id);

```
低级里面直接获取id,而后可以构造查询语句,赋给 $getid变量,下面主要讲上面一句:
```
$id = mysql_real_escape_string($id);

```
![](sql注入2(中级)_files/0156b76b-dbb5-4ed6-9010-10bdb7cb00be.jpg)

`mysql_real_escape_string`主要对用户输入的数据进行转义,（一般有单引号,双引号,【\】；【null】），一般转义的话就是在这些符号前面加一个【\】符号;举个例子:
原来有个用户名字就叫
```
adm`in
```
在输入用户名的时候不能直接输入
```
adm`in
```
 因为他会把这里的单引号和查询语句里面的单引号构成一对闭合了,所以要在这个单引号之前加一个反斜杠符号【\】进行转义,转义就是你这个单引号不要和其他的单引号组成一对进行闭合,它就是被看成一个字符功能,它就是一个单引号!
 举例:
 在mysql里面输入:
 1.show databases;
 2.create table hack
 ![](sql注入2(中级)_files/1d197ac2-597a-4712-9061-290cb0483ac3.png)
 3.show tables;
 ![](sql注入2(中级)_files/360c7380-fae1-4c50-a6fa-2dd42c822743.png)
 4_. insert into hack values(1,"adm'in","123");
 ![](sql注入2(中级)_files/bfd0c59b-cc97-4b2d-a77c-8c8e1c14a0e9.png)
 5.select * from hack;
 ![](sql注入2(中级)_files/487d8518-99a5-4ff5-b2fc-9ae383b826bb.png)
 
 而后输入：
 select * from hack where username ='admin';
 这样是不行的!
 ![](sql注入2(中级)_files/479bd535-8794-4cf8-ba02-aca8fa997d10.png)
  select * from hack where username ='ad\'min';
  ![](sql注入2(中级)_files/c42c1fa3-9fcd-4115-88f6-edf93fd4ee88.png)
  
  只要你输入的语句里面有这些四个符号的话(（一般有单引号,双引号,【\】；【null】),只要在其前面加一个【\】,就可以转义了!还有一个函数的功能和mysql_real_escape_string差不多！是addslashes()【slash就是反斜杠的意思】
  
  还有一个区别:
  ![](sql注入2(中级)_files/5b5eb834-5a13-4fd6-8cc7-70590fe5bfe8.png)
  
  ![](sql注入2(中级)_files/85dc9a6f-6423-4eb4-a046-5522923dea42.png)
  
  看中级里面这句话:
  `$getid = "SELECT first_name, last_name FROM users WHERE user_id = $id";`
  这里有一个数字型注入,`$id`没有放在单引号里面，这里就不用考虑单引号问题，如下图
  ![](sql注入2(中级)_files/78b33518-b6b8-4270-840c-de09ed120a74.png)