### Docker简介

开源的应用容器化引擎，通俗讲，将安装好的软件打包成一个镜像

- docker支持将软件编译成一个镜像

##### 核心概念

1. docker主机（Host）:安装了docket程序的机器（安装在windows系统上）
2. docker客户单（client)：连接docket主机进操作
3. docker仓库(Registry):用于保持各种打包好的软件镜像
4. docker镜像(Images):软件打包好的镜像，放在docker仓库中
5. docker容器(Container)：镜像启动后的实例（一个或一组）

##### 使用docker的步骤：

1. 安装docker
2. 去docker仓库找软件对于镜像
3. 使用docker运行镜像，生产一个docker容器
4. 对容器的启动停止就是对软件的启动停止

```
1.检查内核版本，必须3.10以上
uname -r
2.安装docker
yum install docker
https://www.cnblogs.com/ding2016/p/11592999.html

3.输入y,确认安装
4.启动docker
systemctl start docker
5.设置开机启动
systemctl enable docker
6.停止docker
stop docker
```

##### 常用命令

docker search mysql  检索mysql镜像

docker pull  mysq 拉取-默认最新版本 docker pull mysql:5.5

docker images 查看本地所有镜像

docker rmi 镜像id 删除容器

docker run --name mytomcat -d tomcat:latest      -d ：后台运行 -p：将主机端口映射到容器端口

docker ps 查看运行中的容器

docker start |stop 镜像id 启动|停止

service firewalld status

service firewalld stop

docker logs container-name/container-id

https://hub.docker.com/

