## docker命令大全  :page_facing_up:

> 有没有小伙伴有这样的问题？刚学了docker后，各种命令背的很熟，然而工作后有些命令用的少了就忘了。但是突然有一天发现需要使用这个命令，却死活想不起来。百度也是给出都是自己背住的常用命令，这个“不常用”的怎么也找不到。遇到这种问题早早做好笔记，哪天需要了就翻开笔记看看就行了。



### docker镜像命令



1. 列出镜像docker images

   REPOSITORY：表示镜像的仓库源TAG：镜像的标签（版本），同一仓库源可以有多个 TAG，代表这个仓库源的不同个版本，如ubuntu仓库源里，有15.10、14.04等多个不同的版本。

   字段解释： IMAGE ID：镜像ID；CREATED：镜像创建时间；SIZE：镜像大小。

   

2. 查找镜像

    docker search 镜像名称

    

3. 拉取镜像

   docker pull 镜像名称

   

4. 删除镜像 (没办法删除正在使用的镜像)

   docker rmi 镜像名称或id号[镜像名称2/id2…] 删除一个或多个

   docker rmi 'docker image -q' 删除所有  -q:显示所有id    

   

   **配置加速器，可以更快的下载（拉取镜像）**

   - 配置加速器(阿里巴巴)

     sudo vim /etc/docker/daemon.json

     { "registry-mirrors": ["https://cs913o6k.mirror.aliyuncs.com"]  }

   - 重新启动进程

     sudo systemctl daemon-reload

   - 重新启动服务

     sudo systemctl restart docker
     
     

### docker 容器命令

> 容器是docker 镜像的运行时实例



1. 创建容器 

   docker run 参数 --name=容器名称 镜像名称 /bin/bash(根进程)

   -i:交互式

   -t:终端

   -d:守护进程

   --name=容器名称:给创建的容器命名

   

2. 进入容器 

   docker attach 容器名称/id(exit会关闭容器)

   docker exec -it 容器名称/id /bin/bash(exit不会关闭容器)

   

3. 查看容器

   docker ps 查看当前运行容器

   docker ps -a 查看所有容器(包括历史创建容器)

   

4. 停止/启动容器

   docker stop 容器名称/id 关闭容器

   docker start 容器名称/id 运行容器

   

5. 获取容器/镜像的元数据

   docker inspect 容器名称/id

   

6. 删除容器(无法删除正在运行的容器)

   docker rm 容器名称1/id1 [容器名称2/id2…]:删除多个容器

   docker rm ‘docker ps -a -q’:删除所有容器

   

7. 查看容器日志（只能用attach进入）

   docker logs 容器名称/id

   

8. 文件拷贝

   docker cp 宿主机文件 容器名称:容器文件  将宿主机文件拷贝到容器上

   docker cp 容器名称:容器文件 宿主机文件 将容器文件拷贝到宿主机上

   

9. 目录挂载（只能创建时就进行挂载）

   

   docker  run  -id  --name=c4  -v  /opt/:/usr/local/myhtml  镜像名

   

   就是在创建容器`docker run 参数 --name=容器名称 镜像名称`命令的 基础加上` -v  /opt/:/usr/local/myhtml`

   

   这条命令的意思是把Linux下的<kbd>/opt目录</kbd>与docker容器下的<kbd>/usr/local/myhtml</kbd>目录进行关联。这就是挂载，当你再需要往docker<kbd>/usr/local/myhtml</kbd>目录传文件时，只需要往<kbd>/opt目录</kbd>下传送即可。它会自动复制一份到<kbd>/usr/local/myhtml</kbd>目录下。

   

   可能出现的问题：如果你共享的是多级的目录，可能会出现权限不足的提示“Permission denied”。

   这是因为CentOS7中的安全模块selinux把权限禁掉了，我们需要添加参数 `--privileged=true` 来解决挂载的目录没有权限的问题：

   

   docker  run  -id  --privileged=true  --name=c4  -v  /opt/:/usr/local/myhtml 镜像名

### docker镜像制作

1. 拉取一个基础镜像（其始就是OS）
   docker pull centos

2. 创建一个交互式容器
   docker run ‐it ‐‐name=mycentos centos:latest

3. 软件上传：将宿主机Tomact上传到容器中
   docker cp apache‐tomcat‐7.0.47.tar.gz mycentos:/root/

4. 在容器中安装jdk  
   yum -y install java-1.8.0-openjdk*

5. 在容器中安装tomcat
   tar ‐zxvf apache‐tomcat‐7.0.47.tar.gz ‐C /usr/local/

6. 将正在运行的容器提交为一个新的镜像
   docker commit  mytomcat

7. 容器运行：
   1.端口映射&目录挂载

   docker run -itd --name=t1 ‐p 8888:8080 -v  /opt/test:/usr/local/apache‐tomcat‐7.0.47/webapps/test mytomcat

   2.将war包或者html文件放到宿主机/opt/test文件下

   3.运行tomcat
   docker exec t1 /usr/local/apache‐tomcat‐7.0.47/bin/startup.sh
   4.访问资源:http://宿主机地址:8888/test/资源

### 容器/镜像打包
​	镜像打包： 

1.	镜像打包：
docker save ‐o /root/tomcat7.tar mytomcat
2.	将打包的镜像上传到其他服务器
scp tomcat7.tar 其他服务器ip:/root
3.	导入镜像
docker load ‐i /root/tomcat7.tar
容器打包：
1.	容器打包
docker export ‐o /root/t1.tar t1
2.	导入容器
docker import t1.tar mytomcat:latest

### docker 网络管理

查看docker网络：docker network ls
Docker中默认的三种网络分别为bridge、host和none，其中名为bridge的网络就是默认的bridge驱动网络，也是容器创建时默认的网络管理方式，配置后可以与宿主机通信从而实现与互联网通信功能，而host和none属于无网络，容器添加到这两个网络时不能与外界网络通信