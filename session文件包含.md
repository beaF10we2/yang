session文件包含

session文件包含，一般利用GET传参将我们构造好的恶意代码传入session中的，但没有 GET 传参还能往 session 中写入代码吗？当然可以，php 5.4后添加了 session.upload_progress 功能，这个功能开启意味着当浏览器向服务器上传一个文件时，php将会把此次文件上传的详细信息(如上传时间、上传进度等)存储在session当中，利用这个特性可以将恶意语句写入session文件。

访问/?mode=eval查看 phpinfo 内容，定位到 session 相关的信息，标注箭头处是比较关键的信息


那么讲解一下关键选项

session.auto_start：如果 session.auto_start=On ，则PHP在接收请求的时候会自动初始化 Session，不再需要执行session_start()。但默认情况下，这个选项都是关闭的。但session还有一个默认选项，session.use_strict_mode默认值为 off。此时用户是可以自己定义 Session ID 的。比如，我们在 Cookie 里设置 PHPSESSID=ph0ebus ，PHP 将会在服务器上创建一个文件：/tmp/sess_ph0ebus”。即使此时用户没有初始化Session，PHP也会自动初始化Session。 并产生一个键值，这个键值有ini.get(“session.upload_progress.prefix”)+由我们构造的 session.upload_progress.name 值组成，最后被写入 sess_ 文件里。

session.save_path：负责 session 文件的存放位置，后面文件包含的时候需要知道恶意文件的位置，如果没有配置则不会生成session文件

·session.upload_progress_enabled：当这个配置为 On 时，代表 session.upload_progress 功能开始，如果这个选项关闭，则这个方法用不了

session.upload_progress_cleanup：这个选项默认也是 On，也就是说当文件上传结束时，session 文件中有关上传进度的信息立马就会被删除掉；这里就给我们的操作造成了很大的困难，我们就只能使用条件竞争(Race Condition)的方式不停的发包，争取在它被删除掉之前就成功利用

session.upload_progress_name：当它出现在表单中，php将会报告上传进度，最大的好处是，它的值可控

session.upload_progress_prefix：它＋session.upload_progress_name 将表示为 session 中的键名



综上所述，这种利用方式需要满足下面几个条件：

目标环境开启了session.upload_progress.enable选项
发送一个文件上传请求，其中包含一个文件表单和一个名字是PHP_SESSION_UPLOAD_PROGRESS的字段
请求的Cookie中包含Session ID
注意的是，如果我们只上传一个文件，这里也是不会遗留下Session文件的，所以表单里必须有两个以上的文件上传。

有脚本。

ctfshow    easy_include

[发布成功 (csdn.net)](https://mp.csdn.net/mp_blog/creation/success/135431426)

[pearcmd.php文件包含妙用_pearcmd文件包含-CSDN博客](https://blog.csdn.net/qq_61839115/article/details/131906758?ops_request_misc=%7B%22request%5Fid%22%3A%22170453010416800215037003%22%2C%22scm%22%3A%2220140713.130102334..%22%7D&request_id=170453010416800215037003&biz_id=0&utm_medium=distribute.pc_search_result.none-task-blog-2~all~sobaiduend~default-4-131906758-null-null.142^v99^pc_search_result_base1&utm_term= pearcmd.php本地文件包含&spm=1018.2226.3001.4187)

[Docker PHP裸文件本地包含综述 | 离别歌 (leavesongs.com)](https://www.leavesongs.com/PENETRATION/docker-php-include-getshell.html)

[[ctfshow 2023元旦水友赛\]web题解-CSDN博客](https://blog.csdn.net/m0_73512445/article/details/135410969?ops_request_misc=%7B%22request%5Fid%22%3A%22170452906416800215040561%22%2C%22scm%22%3A%2220140713.130102334.pc%5Fall.%22%7D&request_id=170452906416800215040561&biz_id=0&utm_medium=distribute.pc_search_result.none-task-blog-2~all~first_rank_ecpm_v1~rank_v31_ecpm-6-135410969-null-null.142^v99^pc_search_result_base1&utm_term=ctfshow元旦水友赛&spm=1018.2226.3001.4187)

[【Web】CTFSHOW元旦水友赛部分wp_ctfshow 元旦水友赛 wp-CSDN博客](https://blog.csdn.net/uuzeray/article/details/135333972?ops_request_misc=%7B%22request%5Fid%22%3A%22170452906416800197075086%22%2C%22scm%22%3A%2220140713.130102334..%22%7D&request_id=170452906416800197075086&biz_id=0&utm_medium=distribute.pc_search_result.none-task-blog-2~all~sobaiduend~default-1-135333972-null-null.142^v99^pc_search_result_base1&utm_term=ctfshow元旦水友赛&spm=1018.2226.3001.4187)

[PHP session相关知识详解_phpsessid是什么-CSDN博客](https://blog.csdn.net/weixin_40228200/article/details/128310809)