# git常用命令大全

> git的使用对于一个程序员来说很重要。配合github不仅仅在工作中，日常记笔记这里也是一个很好的地方。这里整理了git的命令大全，帮助你更好的运用这款工具。



#### 1.本地的工作区

查看状态信息：git status （查看工作区、暂存区状态）

添加到暂存区：git add [file name]（将工作区的“新建修改”添加到暂存区）

提交：git commit -m "commit message" [file name]（将暂存区的内容提交到本地库）



#### 2.查看历史记录

git log --pretty=oneline（查看一行记录）

git log --oneline（查看一行记录）

git reflog（查看全部的记录）

- git reflog还能多屏显示控制：

						    1.空格向下翻页
    
	    					2.b向上翻页
    
	    					3.q退出



#### 3.git进行版本回滚

git reset --hard [索引值]  （既能前进又能后退）

git reset --hard ^				（只能后退）

git reset --hard ~10          	（只能后退）

reset命令的三个参数对比

--soft

	仅仅在本地库移动HEAD指针

--mixed

	在本地库移动HEAD指针并重置暂存区

--hard

	在本地库移动HEAD指针，并重置暂存区和工作区



#### 4.比较

git diff [file name]					将工作区和暂存区进行比较

git diff HEAD [file name]  	   将工作区和本地库进行·比较

git diff HEAD^ [file name]	    将工作区和本地库的上一个版本进行比较

注：如果不加文件名则是比较多个文件



#### 5.分支管理

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200723205941736.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2xpMjY0MjUzMDk3OQ==,size_16,color_FFFFFF,t_70)


分支的好处：

- 同时并行推进多个功能的开发，提高开发效率。
- 各个分支在开发过程中，如果一个分支开发失败不会对其他分支造成影响，把失败的分支删除即可。

分支的使用：

git brach -v 						查看分支

git branch 分支名 			创建分支

git checkout 分支名		 切换分支

合并分支：

第一步：切换到接收修改的分支上面。

第二步：执行merge（git merge fix_hot)。

#### 6.解决冲突

第一步：编辑文件删除特殊符号

第二步：把文件修改成满意的程度，保存退出

第三步：git add [文件名]

第四步：git commit -m '日志信息'（注意：这步命令的后面不要加文件名）

#### 7.git关联远程仓库

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200723210037223.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2xpMjY0MjUzMDk3OQ==,size_16,color_FFFFFF,t_70)


git remote add origin [git地址]  把本地仓库与远程仓库进行连接（origin：别名，代表远程仓库）

git remote -v 								查看origin

git clone [git clone地址]			 克隆

克隆的三个效果：

- 完整地把远程仓库下载到本地
- 创建origin远程仓库地址别名
- 初始化本地仓库

pull:

git fetch origin master + git merge origin/master 或者 git pull origin master

push:

git push origin master

出现推送失败的原因：

- 如果不是基于github远程仓库的最新版所做的修改，不能推送，必须先拉取。
- 拉取下来如果进入冲突状态，则按照“分支冲突解决”操作即可。

#### 8.SSH登录（只能设置一个用户）

1.进入当前用户家目录

```
cd ~
```

2.删除.ssh目录

```
rm -rf .ssh
```

3.运行命令生成ssh秘钥目录

```
ssh -keygen -t -rsa -C '注册邮箱'	（获取秘钥）
```

4.进入.ssh目录查看文件列表

```
cd .ssh
ls -IF
```

5.查看id_rsa.pub文件内容

```
cat id_rsa.pub
```

6.复制id_rsa.pub文件内容复制到远程仓库。登录github点击头像>settings>ssh and GPG key>new SSH key,输入复制的的秘钥信息。

7.回到<kbd>git bash</kbd>创建远程ssh地址别名

```
git remote add origin_ssh [ssh地址]
```

现在就可以推送文件了，不再需要输入密码。

#### 9.团队合作
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200723210017159.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2xpMjY0MjUzMDk3OQ==,size_16,color_FFFFFF,t_70)
#### 10.Git基本原理

1.1 哈希

哈希是一个系列的加密算法，各个不同的哈希算法虽然加密强度不同，但是有以下几个共同点：

- 不管输入的数据量有多大，使用同一个哈希算法得到的加密结果长度固定。
- 哈希算法确定，输入数据确定，输出数据能够保证长度。
- 哈希算法确定，输入数据有变化，输出数据一定有变化，而且变化很大。
- 哈希算法不可逆。

git底层采用是sha-1算法；哈希算法用来验证文件。