# Linux-03

从4.3.1开始学。



## 4.3 搜索命令

### 4.3.1 文件搜索命令find

find -name -iname * ? -size + - -user -group

​	-amin -cmin -mmin -type f d l   -inum

​	-a -o				-exec/-ok {} \;

少用搜索命令， 会占用资源

**文件搜索命令： find**

命令名称: find

命令所在路径： /bin/find

执行权限： 所有用户

语法：find 【搜索范围】【匹配条件】

功能描述： 文件搜索

范例：

**根据名字搜索,精准搜索**

find /etc **-name** init

在目录/etc中查找文件init

**-iname 不区分大小写**

`*匹配任意字符 ？匹配当个字符`



**1数据块 512字节。0.5K**

**100MB = 102400B = 204800**

find / **-size** + 204800

在根目录下查找大于100MB的文件

**+n大于 -n小于 n等于**



**查找user和group**

find /home **-use**r shenchao

在home目录下查找所有者为shenchao的文件

-group 根据所属组查找



**查找文件内容修改**

find /etc **-cmin** -5

在/etc下查找5分钟内被修改过属性的文件和目录

-amin 访问时间 access

-cmin 文件属性 change

-mmin 文件内容	modify



**and or**

find /etc -size +163840 **-a** -size -204800

在/etc下查找大于80M小于100MB的文件

**-a 两个条件同时满足**

**-o 两个条件满足任意一个即可**



-type 根据文件类型查找

​	**f 文件 d目录 l软链接文件**



Find /etc -name initiab **-exec** ls -l {} \;

在/etc下查找inittab并显示其详细信息

**-exec/-ok 命令 {} \ ;**对搜索结果执行操作

find /etc -name init* -a -type f -exec ls -l {} \;

- -exec :
- -ok: 进行询问，确认 



**-inum 根据i节点查找**

ls -i 查看 i节点

find . -inum 31513 -exec rm {} \; 

查找31513节点并删除