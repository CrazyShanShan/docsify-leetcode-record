## docker 安装sql-server2019并挂载数据

---

## **步骤：**

这个版本是可以的。

```
账号 sa
密码 SA_PASSWORD=Mypass!1
```



1. 拉取镜像

```
   docker pull datagrip/mssql-server-linux
```

2. 创建挂载目录

```
/Users/crazys/docker_mapping/docker-sqlserver


```

3. 运行命令

```
docker run -e ‘ACCEPT_EULA=Y’ -e ‘SA_PAS’ -p 0.0.0.0:1403:1433 -v /E/sqlserverdata:/var/opt/mssql/data --name sqlserver19 -d mcr.microsoft.com/mssql/server:2019-CU2-ubuntu-16.04

macos
docker run -e 'ACCEPT_EULA=Y' -e 'SA_PASSWORD=Mypass!1' -p 1433:1433 -v /Users/crazys/docker_mapping/docker-sqlserver/data:/var/opt/mssql/data --name sqlserver19-server -d datagrip/mssql-server-linux


docker run -e 'ACCEPT_EULA=Y' -e 'SA_PASSWORD=Mypass!1' -p 1433:1433 -v /home/lab1204/RiskEvent/docker_mapping/docker-sqlserver/data:/var/opt/mssql/data -v /home/lab1204/RiskEvent/docker_mapping/docker-sqlserver/log:/var/opt/mssql/log  --name sqlserver19-server -d datagrip/mssql-server-linux


sudo docker run -e 'ACCEPT_EULA=Y' -e 'SA_PASSWORD=Mypass!1' -p 1433:1433 -v /home/myuser/Projects/RiskEvent/docker_mapping/docker-sqlserver/data:/var/opt/mssql/data -v //home/myuser/Projects/RiskEvent/docker_mapping/docker-sqlserver/log:/var/opt/mssql/log  --name sqlserver19-server -d datagrip/mssql-server-linux

```

4. docker 镜像的导入导出

   ```
   > 
   <
   ```

