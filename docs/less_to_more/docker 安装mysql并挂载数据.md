参考URL：https://blog.csdn.net/qq_40618319/article/details/111935444?utm_medium=distribute.pc_relevant_t0.none-task-blog-2%7Edefault%7EBlogCommendFromMachineLearnPai2%7Edefault-1.control&depth_1-utm_source=distribute.pc_relevant_t0.none-task-blog-2%7Edefault%7EBlogCommendFromMachineLearnPai2%7Edefault-1.control



## 步骤：

1. 拉取镜像

   ```
   docker pull mysql:5.7
   ```

   

2. 创建临时容器

```
docker run  -p 3306:3306 --name mysql-server  -e MYSQL_ROOT_PASSWORD=123456 -d mysql:5.7

```

3. 复制容器配置文件

```
docker cp  mysql-server:/etc/mysql /opt/docker-mysql/conf
docker cp  mysql-server:/etc/mysql /Users/crazys/docker_mapping/docker-mysql/conf 

```

4. 创建容器(需要先把之前的容器删除)

```
docker run  -p 3306:3306 --name mysql-server -v /opt/docker-mysql/conf:/etc/mysql -v /opt/docker-mysql/logs:/var/log/mysql -v /opt/docker-mysql/data:/var/lib/mysql -e MYSQL_ROOT_PASSWORD=123456 -d mysql:5.7

docker run  -p 3306:3306 --name mysql-server -v /Users/crazys/docker_mapping/docker-mysql/conf:/etc/mysql -v /Users/crazys/docker_mapping/docker-mysql/logs:/var/log/mysql -v /Users/crazys/docker_mapping/docker-mysql/data:/var/lib/mysql -e MYSQL_ROOT_PASSWORD=123456 -d mysql:5.7.22

```

5. 开启远程连接

```
进入容器：
docker exec -it mysql-server bash
连接mysql
mysql -uroot  -p
授权
grant all on *.* to root@'%' identified by '123456';
flush privileges;

```

