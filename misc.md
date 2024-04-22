misc

文件分离

binwalk----formost----dd

![image-20230607203041994](C:\Users\86176\AppData\Roaming\Typora\typora-user-images\image-20230607203041994.png)

binwalk -e misc10.png --run-as=root

binwalk -e misc14.jpg --run-as=root -D=jpeg提取图片

zsteg -E 'extradata:0' misc17.png > data这种方法提取出的data不含图片本身的正常数据，但同样可以binwalk得到结果。

apng可用gif一帧一帧查看，by honeyview

//----------用exiftool查看图片exif信息，有如下提示：

Thumbnail Image : (Binary data 18195 bytes, use -b option to extract)

用-b参数以二进制形式提取缩略图信息，并写入文件

root@kali:~/Desktop# exiftool -ThumbnailImage -b misc22.jpg > tn.jpg---------//



![image-20230610092137725](C:\Users\86176\AppData\Roaming\Typora\typora-user-images\image-20230610092137725.png)

文件压缩

![image-20230608144023381](C:\Users\86176\AppData\Roaming\Typora\typora-user-images\image-20230608144023381.png)

压缩包加密

​	1.暴力破解

​	windows:ARCHPR

​	LINUX:fcrackzip

流量包流量分析

![image-20230608150633178](C:\Users\86176\AppData\Roaming\Typora\typora-user-images\image-20230608150633178.png)