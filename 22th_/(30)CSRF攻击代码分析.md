[TOC]

## 源码

### 低级

```
 <?php
                
    if (isset($_GET['Change'])) {
    
        // Turn requests into variables
        $pass_new = $_GET['password_new'];
        $pass_conf = $_GET['password_conf'];


        if (($pass_new == $pass_conf)){
            $pass_new = mysql_real_escape_string($pass_new);//防止sql注入的，这是！！
            $pass_new = md5($pass_new);//用MD5加密

            $insert="UPDATE `users` SET password = '$pass_new' WHERE user = 'admin';";//用update更新
            $result=mysql_query($insert) or die('<pre>' . mysql_error() . '</pre>' );
                        
            echo "<pre> Password Changed </pre>";        
            mysql_close();
        }
    
        else{        
            echo "<pre> Passwords did not match. </pre>";            
        }

    }
?> 
```
### 中级
```
 <?php
            
    if (isset($_GET['Change'])) {//$_POST和$_GET皆为接收用户的数据的
    
        // Checks the http referer header
        if ( eregi ( "127.0.0.1", $_SERVER['HTTP_REFERER'] ) ){        //$_POST和$_GET皆为接收用户的数据的,这里的$_SERVER也是接收用户提交的服务器(http协议也好,服务器也好相关的信息，比如说客户端的ip 是什么,就是通过这个函数)的信息的！！！$_SERVER函数的作用就是从接收的一堆信息里面把HTTP_REFERER这个信息找出来，再和前面这个信息比较一下看是不是"127.0.0.1",用于判断用户提交密码那个页面的HTTP_REFERER这个字段的信息是不是"127.0.0.1"
    
            // Turn requests into variables
            $pass_new = $_GET['password_new'];
            $pass_conf = $_GET['password_conf'];

            if ($pass_new == $pass_conf){
                $pass_new = mysql_real_escape_string($pass_new);
                $pass_new = md5($pass_new);

                $insert="UPDATE `users` SET password = '$pass_new' WHERE user = 'admin';";
                $result=mysql_query($insert) or die('<pre>' . mysql_error() . '</pre>' );
                        
                echo "<pre> Password Changed </pre>";        
                mysql_close();
            }
    
            else{        
                echo "<pre> Passwords did not match. </pre>";            
            }    

        }
        
    }
?> 
```
![]((30)CSRF攻击代码分析_files/c58b41a6-4f7d-4f7c-9eb8-167525d15b4b.jpg)

可以设置代理:
![]((30)CSRF攻击代码分析_files/b91bc0a0-845f-4ea4-9634-92d046d349f6.png)

![]((30)CSRF攻击代码分析_files/ee935593-5eab-4a15-afeb-54c848ba72f8.png)

打开burp suite:

![]((30)CSRF攻击代码分析_files/c0114555-c528-4acc-a934-c955ce1fe90d.jpg)

点击一个链接:
![]((30)CSRF攻击代码分析_files/58387cc2-26b3-4d79-89ba-b659a2267494.png)
再来看一下burpsuite:
![]((30)CSRF攻击代码分析_files/d8351f54-41b0-45fe-baec-fb64455bac6b.jpg)
http协议头的信息:
![]((30)CSRF攻击代码分析_files/a0352800-f500-43b3-b9fa-051a130ddb63.jpg)
这是用用get方法传递的消息;
![]((30)CSRF攻击代码分析_files/a9c178ba-b2f7-4464-9f42-9dcdfbe48d0b.jpg)
host是目标网站;
User-agent:这是客户端的浏览器的信息;
Accept:访问的网页类型;
Accept-Language:访问的网页的语言！
refer，有的还有cookie;
再次访问的时候就有了:
![]((30)CSRF攻击代码分析_files/479cae63-896a-4e9a-84f1-4dff1480846b.jpg)
你要 访问host这个 目标网站,你是从哪个网站开启 访问的;你访问目标网站之前,你是从哪个网站过去的,访问之前的那个页面就叫做referer；
```
https://www.baidu.com/baidu.php?sc.060000jZYuibWkd0MGd2jocqvfOtTjn-VKC31uhCI2QHbvPUfGm08jtg8p9LJStX-Ira97TAMermA3e3q-4Hl5rqYChgWT8mOVoDpD_3IzH_0r-wG65PT5kykTDqCUtmHJe6NYOhJxeXWXubLIGtt2goutMxjeIVotJCLxrg9TpWJz25N6.7Y_iF8sXyl8A64DD2mJauCrKrNdtZGY8C5I7KVe3LkmvgJN9h9mzyUVqp6.U1Yk0ZDqPH7WIAt0TA-W5H00IjYdnyPYUsKGUHYznWR0u1dBugK1nfKdpHdBmy-bIfKspyfqn6KWpyfqPj030AdY5Hnkn1uxnH0kPdtknjD4g1csPWFxn1msnfKopHYs0ZFY5HD4n6K-pyfqnWmdnWNxnHf1P7tznHDsnNtkrjRvn7tzPWndn7tznWDdr0KBpHYznjf0UynqnHRvg1T3PWm1nHcYrNtknj0kg1DLnWcdnWD3nHFxn0KkTA-b5H00TyPGujYs0ZFMIA7M5H00mycqn7ts0ANzu1Ys0ZKs5H00UMus5H08nj0snj0snj00Ugws5H00uAwETjYs0ZFJ5H00uANv5gKW0AuY5H00TA6qn0KET1Ys0AFL5HT0UMfqn0K1XWY0IZN15HbYrHcdrjR1PWnzPjTvrjmzPj00ThNkIjYkPHnLPjcYnWbLPjnv0ZPGujdbnHR3njwWn10snjm4rHP90AP1UHYkfHTdPWFjnRwjfRmdPHT30A7W5HD0TA3qn0KkUgfqn0KkUgnqn0KlIjYs0AdWgvuzUvYqn7tsg1Kxn7ts0Aw9UMNBuNqsUA78pyw15HKxn7tsg1Kxn0Ksmgwxuhk9u1Ys0AwWpyfqnWm3PjndPjRv0ANYpyfqQHD0mgPsmvnqn0KdTA-8mvnqn0KkUymqnHm0uhPdIjYs0AulpjYs0Au9IjYs0ZGsUZN15H00mywhUA7M5HD0UAuW5H00mLFW5HmznjTs&ck=7951.3.218.433.151.243.140.578&shh=www.baidu.com&sht=baidu&us=1.0.1.0.1.305.0&ie=utf-8&f=8&tn=baidu&wd=51cto&oq=51cto&rqlang=cn&inputT=3480&bc=110101
```
referer就指明了你在访问某一个网站的时候是从哪一个网站过去的;
![]((30)CSRF攻击代码分析_files/54c9be32-cca7-4118-bed3-bdce931fab4e.jpg)

![]((30)CSRF攻击代码分析_files/8058b6ae-b91d-4dce-a8ee-d2d7180534a5.jpg)

验证其referer值即可！
其实referer也是可以伪造的！！这是一个缺陷！！
另外,有的单位他不用referer，因为他怕泄露内部信息！！

## High CSRF Source
二次验证即可！

![]((30)CSRF攻击代码分析_files/ef9b97b0-9fbd-4c17-82bc-1b3d7ea0604d.jpg)
```
 <?php
            
    if (isset($_GET['Change'])) {
    
        // Turn requests into variables
        $pass_curr = $_GET['password_current'];
        $pass_new = $_GET['password_new'];
        $pass_conf = $_GET['password_conf'];

        // Sanitise current password input
        $pass_curr = stripslashes( $pass_curr );
        $pass_curr = mysql_real_escape_string( $pass_curr );
        $pass_curr = md5( $pass_curr );
        
        // Check that the current password is correct
        $qry = "SELECT password FROM `users` WHERE user='admin' AND password='$pass_curr';";
        $result = mysql_query($qry) or die('<pre>' . mysql_error() . '</pre>' );

        if (($pass_new == $pass_conf) && ( $result && mysql_num_rows( $result ) == 1 )){
            $pass_new = mysql_real_escape_string($pass_new);
            $pass_new = md5($pass_new);

            $insert="UPDATE `users` SET password = '$pass_new' WHERE user = 'admin';";
            $result=mysql_query($insert) or die('<pre>' . mysql_error() . '</pre>' );
                        
            echo "<pre> Password Changed </pre>";        
            mysql_close();
        }
    
        else{        
            echo "<pre> Passwords did not match or current password incorrect. </pre>";            
        }

    }
?> 
```