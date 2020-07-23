# jenkins简介

## 1.1 是什么

Jenkins是一款Java平台的开源持续集成（Continuous Integration，CI）引擎。 简称：CI
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200718111306256.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2xpMjY0MjUzMDk3OQ==,size_16,color_FFFFFF,t_70)

## 1.2 作用

1、持续、自动地构建/测试 软件项目。 
2、监控软件开放流程，快速问题定位及处理，提高开发效率。

## 1.3 持续化集成（ci）

持续集成指的是，频繁地(一天多次)将代码集成到主干。

它的好处主要有两个：

● 快速发现错误。每完成一点更新，就集成到主干，可以快速发现错误，定位错误也比较容易。

● 防止分支大幅偏离主干。如果不是经常集成，主干又在不断更新，会导致以后集成的难度变大，甚至难以集成。

持续集成的目的，就是让产品可以快速迭代，同时还能保持高质量。

可以进行持续化集成工具有：

-   Jenkins

-   Travis

-   Codeship

-   Strider

## 1.4 组成

1.源码仓库：git、svn、gitlab等

2.自动化测试脚本（app，web，接口，单元测试）

3.持续化工具：jenkins

## 1.5 流程

1.5.1 提交

开发向源码仓库提交代码

1.5.2 测试（第一轮）

持续集成工具对源码仓库配置了监控，只要提交代码，就会执行自动化测试

第一轮至少执行单元测试

1.5.3 构建

只有通过第一轮测试，才会将代码合并进主干，合并后就可以进行构建活动，构建指的是：将源代码转化为可以运行的实际代码，比如安装依赖、配置资源等

1.5.4 测试（第二轮）

第二轮执行的是全面测试，新版本的更新点都要测试到

1.5.5 部署

将新版本打包存档，发送到生产服务器

1.5.6 回滚

如果新版本发现问题，就回滚到上一个版本的结果

# Gitlab注册文档

第一：打开浏览器进入192.168.10.138:10808，跳转至Gitlab首页；

第二：点击project，跳转至登录/注册界面；

第三：填写昵称、邮箱、密码；单击注册

![\[外链图片转存失败,源站可能有防盗链机制,建议将图片保存下来直接上传(img-hLxQR4My-1594990276521)(media/image1.png)\]{width="5.768055555555556in" height="2.959722222222222in"}](https://img-blog.csdnimg.cn/20200717205345483.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2xpMjY0MjUzMDk3OQ==,size_16,color_FFFFFF,t_70)


第四：创建项目，单击New project，跳转至如下图

![\[外链图片转存失败,源站可能有防盗链机制,建议将图片保存下来直接上传(img-Th3FTwsC-1594990276526)(media/image2.png)\]{width="5.768055555555556in" height="3.0208333333333335in"}](https://img-blog.csdnimg.cn/20200717205410608.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2xpMjY0MjUzMDk3OQ==,size_16,color_FFFFFF,t_70)


第五：单击create project保存；项目创建成功后，把clone\-\--http的网址复制到pycharm的地址栏中，Git globle setup下的复制到Git命令行中执行（如下图）；
![在这里插入图片描述](https://img-blog.csdnimg.cn/2020071720543315.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2xpMjY0MjUzMDk3OQ==,size_16,color_FFFFFF,t_70)
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200717205449328.png)




# 项目构建

## 创建一个自由风格的项目

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200717205516563.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2xpMjY0MjUzMDk3OQ==,size_16,color_FFFFFF,t_70)


##  设置工作区（可以是本地空目录）

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200717205532134.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2xpMjY0MjUzMDk3OQ==,size_16,color_FFFFFF,t_70)


##  设置源码仓库

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200717205549779.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2xpMjY0MjUzMDk3OQ==,size_16,color_FFFFFF,t_70)


##  设置构建条件

![在这里插入图片描述](https://img-blog.csdnimg.cn/202007172056202.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2xpMjY0MjUzMDk3OQ==,size_16,color_FFFFFF,t_70)

>
>一、定时构建：不管SVN或Git中数据有无变化，均执行定时化的构建任务 ；
>
>二、轮询SCM：只要SVN或Git中数据有更新，则执行构建任务；
>
>三、构建语法说明：
>
>1.首先格式为：\* \* \* \* \*（五个星）；
>
>2.第一个\*表示分钟，取值0\~59
>
>第二个\*表示小时，取值0\~23
>
>第三个\*表示一个月的第几天，取值1\~31
>
>第四个\*表示第几月，取值1\~12
>
>第五个\*表示一周中的第几天，取值0\~7，其中0和7代表的都是周日

![\[外链图片转存失败,源站可能有防盗链机制,建议将图片保存下来直接上传(img-UcxOLtjE-1594990276574)(media/image9.jpeg)\]{width="3.6875in" height="4.083333333333333in"}](https://img-blog.csdnimg.cn/20200717205637316.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2xpMjY0MjUzMDk3OQ==,size_16,color_FFFFFF,t_70)


##  构建编译环境

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200717205709163.png)



## 构建活动时执行
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200717205725177.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2xpMjY0MjUzMDk3OQ==,size_16,color_FFFFFF,t_70)

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200717205736859.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2xpMjY0MjUzMDk3OQ==,size_16,color_FFFFFF,t_70)


##  构建活动后执行

![> \[外链图片转存失败,源站可能有防盗链机制,建议将图片保存下来直接上传(img-qifQkXQT-1594990276609)(media/image13.png)\]{width="3.4583333333333335in" height="3.25in"}](https://img-blog.csdnimg.cn/20200717205753104.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2xpMjY0MjUzMDk3OQ==,size_16,color_FFFFFF,t_70)


一般用于构建成功之后发送邮件