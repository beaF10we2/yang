java-web-security

提示：java.io.FileNotFoundException:{help.docx}

这里对WEB-INF进行一个简单的了解。

WEB-INF是java的WEB应用的安全目录。

1.WEB-INF/web.xml

web应用程序配置文件，描述了servlet和其他的应用组件配置及命名规则。

2.WEB-INF/classes

包含了站点所有用的class文件，包括servlet class和非servlet class

3.WEB-INF/lib

存放web应用需要的JAR文件

4.WEB-INF/src

源码目录，按照包名结构放置各个java文件

5.WEB-INF/database.properties

数据库配置文件

6.WEB-INF/tags

存放了自定义标签文件

7.WEB-INF/jsp

jsp 1.2 一下版本的文件存放位置。

8.WEB-INF/jsp2

存放jsp2.0以下版本的文件。

9.META-INF

相当于一个信息包。

漏洞形成原因：

Tomcat的WEB-INF目录，每个j2ee的web应用部署文件默认包含这个目录。

Nginx在映射静态文件时，把WEB-INF目录映射进去，而又没有做Nginx的相关安全配置（或Nginx自身一些缺陷影响）。从而导致通过Nginx访问到Tomcat的WEB-INF目录（请注意这里，是通过Nginx，而不是Tomcat访问到的，因为上面已经说到，Tomcat是禁止访问这个目录的。）。

漏洞利用方式：

直接在域名后面加上WEB-INF/web.xml就可以了。
根据web.xml配置文件路径或通常开发时常用框架命名习惯，找到其他配置文件或类文件路径。
dump class文件进行反编译。

简单来说：通过找到web.xml文件，推断class文件的路径，最后直接class文件，在通过反编译class文件，得到网站源码。

payload:

Download?filename=/WEB-INF/classes/com/wm/ctf/FlagController.class

**将get改为post**

