# linux-05

今天是学习linux的第5天，从4.4开始看～

## 4.4 帮助命令

**帮助命令： man**  

info 也是类似的功能

命令名称：man

命令英文原意：manual

命令所在路径： /usr/bin/man

执行权限： 所有用户

语法： man 【命令或配置文件】

功能描述： 获得帮助信息

范例： man ls

​		查看ls命令的帮助信息

​			man services

​		查看配置文件services的帮助信息

/ 查找 ，n - next下一个

1 命令 5 配置文件的帮助

**查看简短信息：**

**whatis 命令 	apropos 配置文件**

--help 很方便，可以中文显示哦～



`补充一下zsh的优点： 1.完全兼容bash 2.更强大的tab补全，cd + 2下tab可以列出当前目录下面的所有目录，并且可以使用键盘上下左右键来选择要进入的目录 3.更智能的切换目录`



## 4.5 用户管理命令

**用户管理命令： useradd**

命令名称： useradd

命令所在路径：/usr/sbin/useradd

执行权限： root

语法： useradd 用户名

功能描述： 添加新用户

范例： useradd yang



**用户管理命令： passwd**

命令名称： passwd

命令所在路径： /usr/bin/passwd

执行权限： 所有用户

语法： passwd 用户名

功能描述： 设置用户米阿们

范例： passwd yangmi



**用户管理命令： who**

命令名称： who

命令所在路径： /usr/bin/who

执行权限： 所有用户

语法： who

功能描述： 查看登陆用户信息

范例： who

![image-20210314225302852](linux-images/image-20210314225302852.png)

登陆信息：

登陆用户名

登陆终端  tty ： 本地终端 pts:远程终端

登陆时间

IP地址

## 4.6 解压缩命令
```yml
.gz gzip gunzip -d 

.tar	tar -cf    tar -xf

.tar.gz		tar -zcf -zxf

.zip	zip  -r unzip

.bz2		bzip2 bunzip2

.tar.bz2 	tar -jcf	-jxf
```


**zxf zcf**

**压缩解压命令：gzip**

**只能压缩文件，并不保存原文件**

命令名称： gzip

命令英文原意： GNU zip

命令所在路径： /bin/gzip

执行权限： 所有用户

语法： gzip 【文件】

功能描述：压缩文件

压缩后文件格式： .gz

-d : decompress = gunzip



**压缩解压命令： tar**

命令名称： tar

命令所在路径： /bin/tar

执行权限： 所有用户

语法： tar 选项【-zcf】 【压缩后文件名】 【目录】

​		-c 打包 create a new archive 创建一个新的归档

​		-x 解包 extract files from an archive

​		-v 显示详细信息 verbosely list files processed

​		-f 指定文件名  use archive file

​		-z 打包同时压缩 filter the archive from gzip

​		 -j filter the archive from bzip2

功能描述：打包目录

压缩后文件格式： .tar.gz

`f 一定要放在最后否则会将f后的参数判定为打包文件名`

范例： tar -zcf Japan.tar.gz Japn

​			 tar -zcf etc.tar.gz /etc 

​			tar -zxvf Janpan.tar.gz



**压缩解压命令： zip**

命令名称： zip

命令所在路径： /usr/bin/zip

执行权限：所有用户

语法：

zip 选项【-r】 【压缩后文件名】【文件或目录】

​			-r 压缩目录

功能描述：压缩文件或目录

压缩后文件格式：.zip

范例： zip buduo.zip boduo

​			zip -r Janpan.zip	Japan

 **压缩解压命令： unzip**

命令名称： unzip

命令所在路径： /usr/bin/unzip

执行权限：所有用户

语法：unzip 【压缩文件】

功能描述： 解压.zip的压缩文件

范例： unzip test.zip

**压缩解压缩命令：bzip2**

命令名称：bzip2

命令所在路径：/usr/bin/bzip2

执行权限：所有用户

语法：bzip2

命令所在路径：/usr/bin/bzip2

执行权限：所有用户

语法：bzip2  选项 【-k】【文件】

​					-k 产生压缩文件后保留原文件

功能描述：压缩文件

压缩后文件格式：.bz2

范例：bzip2 -k boduo

​		  tar -jcf Janpan.tar.bz2 Japan

**压缩解压命令： bunzip2**

命令名称：bunzip2

命令所在路径：/usr/bin/bunzip2

执行权限：所有用户

语法： bunzip2 选项【-k】【压缩文件】

​							-k 解压缩后保留原文件

功能描述： 解压缩

范例： bunzip2 -k boduo.bz2

​			tar -jvxf Janpan.tar.bz2



