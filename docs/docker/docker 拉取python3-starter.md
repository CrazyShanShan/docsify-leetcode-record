**拉取python3-starter镜像，并使用jupter功能**

1. 拉取镜像

   ```
   docker pull dataquestio/python3-starter
   ```

2. 创建文件夹

   ```
   /Users/crazys/docker_mapping/docker-python3starter/notebooks
   ```

   

3. 运行镜像

   ```
   docker run -d -p 8888:8888 -v /Users/crazys/docker_mapping/docker-python3starter/notebooks:/home/ds/notebooks  --memory-swap 4096M --name python3-starter   dataquestio/python3-starter
   docker run -d -p 8888:8888 --name python3-starter   dataquestio/python3-starter
   ```

4. 可以使用了哦

   ```
   http://localhost:8888/tree#
   ```

   

