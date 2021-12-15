需要先去cp /etc/nginx/nginx.conf 文件和 /etc/nginx/conf.d/default.conf两个文件

```sh
docker run -d --name nginx -p80:80 -p 8847:8847 -v /Users/crazys/docker_mapping/docker-nginx/logs:/var/log/nginx -v /Users/crazys/docker_mapping/docker-nginx/html:/usr/share/nginx/html -v /Users/crazys/docker_mapping/docker-nginx/conf:/etc/nginx/conf.d -v /Users/crazys/docker_mapping/docker-nginx/nginx.conf:/etc/nginx/nginx.conf --privileged=true nginx
```

