## docker的安装和使用  :page_facing_up:

> 有没有小伙伴有这样的问题？刚学了docker后，各种命令背的很熟，然而工作后有些命令用的少了就忘了。但是突然有一天发现需要使用这个命令，却死活想不起来。百度也是给出都是自己背住的常用命令，这个“不常用”的怎么也找不到。遇到这种问题早早做好笔记，哪天需要了就翻开笔记看看就行了。

## 一、docker的安装

> docker安装也是很简单的，以下是它的安装方法。

- 在Ubuntu上安装Docker Engine

  要在Ubuntu上开始使用Docker Engine，请确保您 [满足前提条件](https://docs.docker.com/engine/install/ubuntu/#prerequisites)，然后 [安装Docker](https://docs.docker.com/engine/install/ubuntu/#installation-methods)。

#### 前提条件:

#### 1.操作系统要求

要安装Docker Engine，您需要以下Ubuntu版本之一的64位版本：

- Ubuntu Focal 20.04（LTS）
- Ubuntu Eoan 19.10
- Ubuntu Bionic 18.04（LTS）
- Ubuntu Xenial 16.04（LTS）

Docker Engine在`x86_64`（或`amd64`）`armhf`，和`arm64`体系结构上受支持。

#### 2.卸载旧版本

旧版本docker被称为`docker`，`docker.io`或`docker-engine`。如果已安装这些，请卸载它们：

```
$ sudo apt-get remove docker docker-engine docker.io containerd runc
```

如果`apt-get`报告未安装这些软件包，则可以进行安装。

这些内容（`/var/lib/docker/`包括图像，容器，卷和网络）将被保留。Docker Engine软件包现在称为`docker-ce`。

#### 3.支持的存储驱动程序

docker引擎在Ubuntu的支持`overlay2`，`aufs`和`btrfs`存储驱动程序。

Docker Engine `overlay2`默认使用存储驱动程序。如果需要使用 `aufs`，则需要手动配置。请参阅[使用AUFS存储驱动程序](https://docs.docker.com/storage/storagedriver/aufs-driver/)

#### 安装方法:

您可以根据需要以不同的方式安装Docker Engine：

- 大多数用户会 [设置Docker的存储库](https://docs.docker.com/engine/install/ubuntu/#install-using-the-repository)并从中进行安装，以简化安装和升级任务。这是推荐的方法。
- 一些用户下载并[手动安装](https://docs.docker.com/engine/install/ubuntu/#install-from-a-package) DEB软件包， 并完全手动管理升级。这在诸如在无法访问互联网的空白系统上安装Docker的情况下很有用。
- 在测试和开发环境中，一些用户选择使用自动 [便利脚本](https://docs.docker.com/engine/install/ubuntu/#install-using-the-convenience-script)来安装Docker。

> 使用存储库安装

在新主机上首次安装Docker Engine之前，需要设置Docker存储库。之后，您可以从存储库安装和更新Docker。

#### 1.设置存储库

1. 更新`apt`软件包索引并安装软件包以允许`apt`通过HTTPS使用存储库：

   ```
   $ sudo apt-get update
   
   $ sudo apt-get install \
       apt-transport-https \
       ca-certificates \
       curl \
       gnupg-agent \
       software-properties-common
   ```

2. 添加Docker的官方GPG密钥：

   ```
   $ curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
   ```

   `9DC8 5822 9FC7 DD38 854A E2D8 8D81 803C 0EBF CD88`通过搜索指纹的后8个字符，验证您现在是否拥有带有指纹的密钥 。

   ```
   $ sudo apt-key fingerprint 0EBFCD88
   
   pub   rsa4096 2017-02-22 [SCEA]
         9DC8 5822 9FC7 DD38 854A  E2D8 8D81 803C 0EBF CD88
   uid           [ unknown] Docker Release (CE deb) <docker@docker.com>
   sub   rsa4096 2017-02-22 [S]
   ```

3. 使用以下命令来设置**稳定的**存储库。要添加 **夜间**或**测试**存储库，请在以下命令中的单词后面添加`nightly`或`test`（或两者）`stable`。[了解**每晚**和**测试**频道](https://docs.docker.com/engine/install/)。

   > **注意**：下面的`lsb_release -cs`子命令返回Ubuntu发行版的名称，例如`xenial`。有时，在Linux Mint等发行版中，您可能需要更改`$(lsb_release -cs)` 为父Ubuntu发行版。例如，如果您使用 `Linux Mint Tessa`，则可以使用`bionic`。Docker对未经测试和不受支持的Ubuntu发行版不提供任何保证。

   - x86_64 / amd64

   ```
   $ sudo add-apt-repository \
      "deb [arch=amd64] https://download.docker.com/linux/ubuntu \
      $(lsb_release -cs) \
      stable"
   ```

   

#### 2.安装DOCKER引擎

1. 更新`apt`程序包索引，并安装*最新版本*的Docker Engine和容器，或转到下一步以安装特定版本：

   ```
    $ sudo apt-get update
    $ sudo apt-get install docker-ce docker-ce-cli containerd.io
   ```

   > 有多个Docker存储库吗？
   >
   > 如果您启用了多个Docker存储库，则在未在`apt-get install`or `apt-get update`命令中指定版本的情况下进行安装或更新将始终安装可能的最高版本，这可能不适合您的稳定性需求。

2. 要安装*特定版本*的Docker Engine，请在存储库中列出可用版本，然后选择并安装：

   一个。列出您的仓库中可用的版本：

   ```
   $ apt-cache madison docker-ce
   
     docker-ce | 5:18.09.1~3-0~ubuntu-xenial | https://download.docker.com/linux/ubuntu  xenial/stable amd64 Packages
     docker-ce | 5:18.09.0~3-0~ubuntu-xenial | https://download.docker.com/linux/ubuntu  xenial/stable amd64 Packages
     docker-ce | 18.06.1~ce~3-0~ubuntu       | https://download.docker.com/linux/ubuntu  xenial/stable amd64 Packages
     docker-ce | 18.06.0~ce~3-0~ubuntu       | https://download.docker.com/linux/ubuntu  xenial/stable amd64 Packages
     ...
   ```

   b。使用第二列中的版本字符串安装特定版本，例如`5:18.09.1~3-0~ubuntu-xenial`。

   ```
   $ sudo apt-get install docker-ce=<VERSION_STRING> docker-ce-cli=<VERSION_STRING> containerd.io
   ```

3. 通过运行`hello-world` 映像来验证是否正确安装了Docker Engine 。

   ```
   $ sudo docker run hello-world
   ```

   此命令下载测试图像并在容器中运行。容器运行时，它会打印参考消息并退出。

Docker Engine已安装并正在运行。该`docker`组已创建，但未添加任何用户。您需要使用`sudo`来运行Docker命令。继续进行[Linux后安装，](https://docs.docker.com/engine/install/linux-postinstall/)以允许非特权用户运行Docker命令以及其他可选配置步骤。

---



## 二、docker命令

### 1.docker镜像命令

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

  

### 2.docker 容器命令

> 容器是docker 镜像的运行时实例



创建容器 

docker run 参数 --name=容器名称 镜像名称 /bin/bash(根进程)

-i:交互式

-t:终端

-d:守护进程

--name=容器名称:给创建的容器命名



进入容器 

docker attach 容器名称/id(exit会关闭容器)

docker exec -it 容器名称/id /bin/bash(exit不会关闭容器)



查看容器

docker ps 查看当前运行容器

docker ps -a 查看所有容器(包括历史创建容器)



1.停止/启动容器

docker stop 容器名称/id 关闭容器

docker start 容器名称/id 运行容器



2.获取容器/镜像的元数据

docker inspect 容器名称/id



3.删除容器(无法删除正在运行的容器)

docker rm 容器名称1/id1 [容器名称2/id2…]:删除多个容器

docker rm ‘docker ps -a -q’:删除所有容器



4.查看容器日志（只能用attach进入）

docker logs 容器名称/id



5.文件拷贝

docker cp 宿主机文件 容器名称:容器文件 	 将宿主机文件拷贝到容器上

docker cp 容器名称:容器文件 宿主机文件	 将容器文件拷贝到宿主机上



6.目录挂载（只能创建时就进行挂载）



docker  run  -id  --name=c4  -v  /opt/:/usr/local/myhtml  镜像名



就是在创建容器`docker run 参数 --name=容器名称 镜像名称`命令的 基础加上` -v  /opt/:/usr/local/myhtml`



这条命令的意思是把Linux下的<kbd>/opt目录</kbd>与docker容器下的<kbd>/usr/local/myhtml</kbd>目录进行关联。这就是挂载，当你再需要往docker<kbd>/usr/local/myhtml</kbd>目录传文件时，只需要往<kbd>/opt目录</kbd>下传送即可。它会自动复制一份到<kbd>/usr/local/myhtml</kbd>目录下。



可能出现的问题：如果你共享的是多级的目录，可能会出现权限不足的提示“Permission denied”。

这是因为CentOS7中的安全模块selinux把权限禁掉了，我们需要添加参数 `--privileged=true` 来解决挂载的目录没有权限的问题：



docker  run  -id  --privileged=true  --name=c4  -v  /opt/:/usr/local/myhtml 镜像名

### 3.docker镜像制作

1.拉取一个基础镜像（其始就是OS）
docker pull centos

2.创建一个容器
docker run ‐it ‐‐name=mycentos centos:latest

3.软件上传：将宿主机Tomact上传到容器中
docker cp apache‐tomcat‐7.0.47.tar.gz mycentos:/root/

4.在容器中安装jdk（需要进入容器）  
yum -y install java-1.8.0-openjdk*

5.在容器中安装tomcat
tar ‐zxvf apache‐tomcat‐7.0.47.tar.gz ‐C /usr/local/

6.将正在运行的容器提交为一个新的镜像（exit退出容器）
docker commit  mytomcat

7.容器运行：

1.端口映射&目录挂载

docker run -itd --name=t1 ‐p 8888:8080 -v  /opt/test:/usr/local/apache‐tomcat‐7.0.47/webapps/test mytomcat

2.将war包或者html文件放到宿主机/opt/test文件下

3.运行tomcat
docker exec t1 /usr/local/apache‐tomcat‐7.0.47/bin/startup.sh
4.访问资源:http://宿主机地址:8888/test/资源（用来验证Tomcat）

### 4.容器/镜像打包

​	镜像打包： 

1.	镜像打包：
   docker save ‐o /root/tomcat7.tar mytomcat
2.	将打包的镜像上传到其他服务器
   scp tomcat7.tar 其他服务器ip:/root
3.	导入镜像
   docker load ‐i /root/tomcat7.tar
   容器打包：
4.	容器打包
   docker export ‐o /root/t1.tar t1
5.	导入容器
   docker import t1.tar mytomcat:latest

### 5.docker 网络管理

查看docker网络：docker network ls
Docker中默认的三种网络分别为bridge、host和none，其中名为bridge的网络就是默认的bridge驱动网络，也是容器创建时默认的网络管理方式，配置后可以与宿主机通信从而实现与互联网通信功能，而host和none属于无网络，容器添加到这两个网络时不能与外界网络通信