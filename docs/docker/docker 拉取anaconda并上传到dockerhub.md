1. docker search anaconda

2. docker pull continuumio/anaconda3

3. docker run -i -t -p 12345:8888 continuumio/anaconda3 /bin/bash

   ```
   -i: 是  以交互模式运行容器，通常与 -t 同时使用；
   
   -t: 为容器重新分配一个伪输入终端，通常与 -i 同时使用；
   
   -p: 指定端口映射，格式为：主机(宿主)端口:容器端口
   ```

4. 安装xgboost 

   pip install -i https://pypi.tuna.tsinghua.edu.cn/simple xgboost 

5. 可以给镜像改名字

   docker rename cc432d1f6b13 AnacondaEnvironment

6. docker start -i AnacondaEnvironment 重新运行

7. 在容器中运行jupyter notebook:

   ```
   jupyter notebook --port 8888 --ip 0.0.0.0 --allow-root
   ```

   然后复制http://127.0.0.1:8888/?token=a6b3189e8f96802b6d193475f0e30908c3a2e16816e1a444

把前面的ip换为宿主的ip，把端口号换为12345，在本地浏览器中就可以直接访问啦。

8. 想把当前容器状态打包为新的镜像，然后可以就可以部署到其他地方了，而不用再安装xgboost等。

   可以采用docker commit或者DockerFile进行打包，这里采用的是docker commit进行打包。

   ```
   docker commit -a "crazyshanshan" -m "my first image" 08e new_anaconda_xgboost
   ```

   ```
   -a 是作者， -m 是描述， 后面一个是cd，一个是镜像名字
   ```

9. 给这个镜像打上tag

   ```
   docker tag new_anaconda_xgboost:latest crazyshanshan/machine_learning:v0.1
   ```

10. 最后可以推送到自己的dockerHub上面去：

    ```
    docker push crazyshanshan/machine_learning:v0.1
    ```

    然后再进行拉取即可，真方便啊。

