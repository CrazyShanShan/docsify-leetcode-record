参考URL：https://blog.csdn.net/qq_44695727/article/details/108978183

## 步骤：

1. 拉取镜像

```
docker pull redis:latest
```

2. 创建需要挂载的文件目录

```
/Users/crazys/docker_mapping/docker-redis/conf
/Users/crazys/docker_mapping/docker-redis/data
```

3. 在conf文件夹下创建redis.conf

如果bind设置为127.0.0.1，则只能本机访问

```sh
bind 0.0.0.0
protected-mode yes
port 6379
tcp-backlog 511
timeout 0
tcp-keepalive 0
loglevel notice
logfile ""
databases 16
save 900 1
save 300 10
save 60 10000
stop-writes-on-bgsave-error yes
rdbcompression yes
rdbchecksum yes
dbfilename dump.rdb
dir ./
slave-serve-stale-data yes
slave-read-only yes
repl-diskless-sync no
repl-diskless-sync-delay 5
repl-disable-tcp-nodelay no
slave-priority 100
appendonly no
appendfilename "appendonly.aof"
appendfsync everysec
no-appendfsync-on-rewrite no
auto-aof-rewrite-percentage 100
auto-aof-rewrite-min-size 64mb
aof-load-truncated yes
lua-time-limit 5000
slowlog-log-slower-than 10000
slowlog-max-len 128
latency-monitor-threshold 0
notify-keyspace-events ""
hash-max-ziplist-entries 512
hash-max-ziplist-value 64
list-max-ziplist-size -2
list-compress-depth 0
set-max-intset-entries 512
zset-max-ziplist-entries 128
zset-max-ziplist-value 64
hll-sparse-max-bytes 3000
activerehashing yes
client-output-buffer-limit normal 0 0 0
client-output-buffer-limit slave 256mb 64mb 60
client-output-buffer-limit pubsub 32mb 8mb 60
hz 10
aof-rewrite-incremental-fsync yes
```

4. 新建并启动容器

```shell
docker run -d --privileged=true -p 6379:6379 -v /docker/redis/conf/redis.conf:/D/home/redis/conf.conf -v /docker/redis/data:/D/home/redis/data --name redis6379 redis:latest redis-server /D/home/redis/conf.conf  --appendonly yes

docker run -d --privileged=true -p 6379:6379 -v /Users/crazys/docker_mapping/docker-redis/data:/etc/redis/redis.conf -v /Users/crazys/docker_mapping/docker-redis/data:/data --name redis-server redis:latest redis-server /etc/redis/redis.conf   --appendonly yes

```

5. 命令解析

```shell
docker run 

-d  后台运行容器，并返回容器ID；
--privileged=true 容器内的root拥有真正root权限，否则容器内root只是外部普通用户权限
-p 6379:6379 指定端口映射,格式：主机(宿主)端口:容器端口
-v /docker/redis/conf/redis.conf:/D/home/redis/conf.conf  映射配置文件
-v /docker/redis/data:/D/home/redis/data  映射数据目录
--name redis6379 指定一个名称
redis:latest redis-server /D/home/redis/conf.conf  指定配置文件启动redis-server进程，latest镜像版本，docker images查看
--appendonly yes 开启数据持久化
--requirepass '123456’设置密码
```

