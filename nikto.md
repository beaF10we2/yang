## tools

工具

[TOC]

#### nikto

在kali中。

Nikto是一款开源的（GPL）网页服务器扫描器，它可以对网页服务器进行全面的多种扫描

```
nikto -host http://172.168.1.105
简单来说就是查找网页隐藏的目录。
```

[Web漏洞扫描神器Nikto使用指南_nikto扫描-CSDN博客](https://blog.csdn.net/liver100day/article/details/121392509?ops_request_misc=%7B%22request%5Fid%22%3A%22171038098916800215074924%22%2C%22scm%22%3A%2220140713.130102334..%22%7D&request_id=171038098916800215074924&biz_id=0&utm_medium=distribute.pc_search_result.none-task-blog-2~all~top_positive~default-1-121392509-null-null.142^v99^pc_search_result_base1&utm_term=nikto&spm=1018.2226.3001.4187)

#### enum4linux

在kali中

Enum4linux是用于枚举windows和Linux系统上的SMB服务的工具。可以轻松的从与**SMB服务**有关的目标中快速提取信息

```
enum4linux -a -o ip
简单来说就是看到开启了SMB服务就扫一扫。

1.LDAP信息探测
 通过LDAP 389 / TCP获取一些（有限的）信息（仅适用于DN）
enum4linux -l ip   

 2.获取操作系统信息
enum4linux -o ip  

3.通过RID循环枚举用户
enum4linux -r ip  
```

#### Hydra

​		hydra（九头蛇）是著名黑客组织thc的一款开源的暴力破解密码工具，功能非常强大，kali下是默认安装的，几乎支持所有协议的在线破解。密码能否破解，在于字典是否强大。

```
使用语法：hydra 参数 IP地址 服务名
帮助命令：hydra -h
常用命令：hydra [-l 用户名|–L 用户名文件路径] [-p 密码|–P 密码文件路径] [-t 线程数] [–vV 显示详细信息] [–o 输出文件路径] [–f 找到密码就停止] [–e ns 空密码和指定密码试探] [ip|-M ip列表文件路径]

```

用户名文件和密码文件需要自己指定/

不需要密码。

hydra -L user.txt -e nsr 192.168.47.142 ftp

例子

ssh

```
不知账号命令：hydra -L user.txt -P passwd.txt -t 2 -vV -e ns 192.168.10.30 ssh

知道账号命令：hydra -l root -P passwd.txt -t 2 -vV -e ns 192.168.10.30 ssh 

```

ftp

```
不知账号命令：hydra -L user.txt -P passwd.txt -t 2 -vV -e ns 192.168.10.30 ftp 
知道账号命令：hydra -l root -P passwd.txt -t 2 -vV -e ns 192.168.10.30 ftp

```

#### hash-identifier

查是哪种hash加密。

直接进入。

#### john 

john --wordlist=/usr/share/wordlists/rockyou.txt sql1.txt

#### nmap

```
查询支持的方法
nmap --script http-methods --script-args http-methods.url-path='/test' 192.168.137.136

```

#### oneforall

路径

![1710729992320](C:\Users\86176\AppData\Roaming\Typora\typora-user-images\1710729992320.png)

https://github.com/shmilylty/OneForAll?tab=readme-ov-file

```
python oneforall.py --target sujiaofei.com run

python oneforall.py --target example.com run
python oneforall.py --targets ./example.txt run
```

[OneForAll的使用 - 灰心爷爷 - 博客园 (cnblogs.com)](https://www.cnblogs.com/blackclouds2810/p/16828889.html)

#### axel/wget/aria2

下载工具/kali

```
axel url
```

#### 自动化的测目录

![1710902074745](C:\Users\86176\AppData\Roaming\Typora\typora-user-images\1710902074745.png)

这是目录，我们要将他与主域名拼接，访问，看看哪些能访问。

#### sed

![1710902219131](C:\Users\86176\AppData\Roaming\Typora\typora-user-images\1710902219131.png)

^代表从头开始，将http://。。。插入到secret.txt中。、

![1710902290365](C:\Users\86176\AppData\Roaming\Typora\typora-user-images\1710902290365.png)

![1710902351903](C:\Users\86176\AppData\Roaming\Typora\typora-user-images\1710902351903.png)

将secret.txt中的内容保存到secret_ext.txt中。

![1710902435509](C:\Users\86176\AppData\Roaming\Typora\typora-user-images\1710902435509.png)

因为我们不清楚在哪层目录下，所以要都试试。

```
sed 's|^|http://192.168.137.137/DRAGON%20BALL|' secret.txt | tee -a secret_ext.txt
```

这句比上面那句多了-a 这个意思是将这次拼接的内容加到secret_ext.txt文件中。如果不写-a，原文件中的内容会被覆盖掉。

那么接下来是访问这些URL

```
while read -r url;do curl "$url";done< secret_ext.txt
将secret.txt中的文件按行赋值给url,然后访问。
-r,是将url中的反斜杠按普通字符处理。
```

```
while IFS= read -r url;do curl -o /dev/null -s -w "%{url_effective} http status: %{http_code}\n" "$url";done< secret_ext.txt


这段命令对先前的命令进行了几个重要的改进：
IFS=：IFS（Internal Field Separator）是 Bash 中用于分隔字段的变量。默认情况下，它包含空格、制表符和换行符。当将 IFS 设置为空时（即 IFS=），read 命令将只按换行符分割输入，这确保了即使 URL 中包含空格或其他空白字符，也能被正确地读取。

curl -o /dev/null -s -w "%{url_effective} http status: %{http_code}\n"：这个 curl 命令的选项和参数做了以下事情：
-o /dev/null：将 curl 的输出（即所请求的网页内容）重定向到 /dev/null，这意味着你不会在终端中看到这些输出。这对于只关心 HTTP 响应状态码而不关心实际内容的场景很有用。
-s 或 --silent：这个选项让 curl 在运行时保持静默，不显示进度表或错误消息。
-w "%{url_effective} http status: %{http_code}\n"：这个选项用于在 curl 命令完成后输出格式化的字符串。%{url_effective} 会被替换为实际请求的 URL（考虑到重定向的情况），而 %{http_code} 会被替换为 HTTP 响应的状态码。\n 是一个换行符，确保每个 URL 的输出都在新的一行。
"$url"：这是从 secret_ext.txt 文件中读取的每一行内容，即每个 URL。

整个命令的作用是：从 secret_ext.txt 文件中读取每一行的 URL，使用 curl 访问这些 URL，并输出每个 URL 的有效 URL（考虑到任何重定向）和相应的 HTTP 状态码，而不显示任何实际的网页内容。

这个命令在处理包含空格或其他特殊字符的 URL 时更加健壮，并且它提供了关于 HTTP 请求状态的更多信息。此外，通过重定向输出到 /dev/null，它减少了不必要的输出，使得结果更加清晰。
```

![1710904419552](C:\Users\86176\AppData\Roaming\Typora\typora-user-images\1710904419552.png)

#### urlfinder

在本文件夹下打开cmd

```
URLFinder.exe -u http://www.baidu.com -s all -m 3
```

