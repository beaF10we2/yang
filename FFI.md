FFI

[[RCTF 2019\]nextphp | NSSCTF](https://www.nssctf.cn/problem/33)

[opcache.preload](https://www.php.net/manual/en/opcache.configuration.php#ini.opcache.preload) 是 **PHP7.4** 中新加入的功能。如果设置了 [opcache.preload](https://www.php.net/manual/en/opcache.configuration.php#ini.opcache.preload) ，那么在所有Web应用程序运行之前，服务会先将设定的 **preload** 文件加载进内存中，使这些 **preload** 文件中的内容对之后的请求均可用。更多细节可以阅读：<https://wiki.php.net/rfc/preload> ，在这篇文档尾巴可以看到如下描述：