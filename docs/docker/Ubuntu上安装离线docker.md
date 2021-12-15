系统Ubuntu18.04

1. docker安装

```
docker-ce_17.12.1_ce-0_ubuntu_amd64.deb
libltdl7_2.4.6-0.1_amd64.deb
sudo dpkg -i XXX

```

2. 解决如下错误：

```
[root@localhost laradock]# systemctl enable docker  && systemctl start docker
A dependency job for docker.service failed. See 'journalctl -xe' for details.
```

如下 命令可用： 

```
[root@localhost laradock]# chattr -i /etc/group
[root@localhost laradock]# groupadd docker
[root@localhost laradock]# systemctl enable docker  && systemctl start docker
```

https://blog.csdn.net/leng_yan/article/details/87208363

