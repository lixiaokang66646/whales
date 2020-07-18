# Ant+Jmeter+Jenkins做接口持续化集成

测试完成后，jmeter接口导出脚本用Ant运行，利用jenkins持续集成，达到监控接口的目的

优点：不需要懂代码，接口测试通过后即可导出测试脚本并持续集成

缺点：不能很好地支持 动态参数 的接口

Jmeter 的安装和使用在这里就不详细介绍了。具体操作见章节接口测试

## 一、Ant 简介

Apache Ant是一个将软件编译，测试，部署等步骤联系在一起的一个工具。一般用于java环境中的软件开发。

**下载地址**：<https://ant.apache.org/bindownload.cgi>

下载之后解压到任意文件路径下。

**配置环境变量**：

-   ANT_HOME：解压的路径

-   Path：%ANT_HOME%\\bin

-   CLASSPATH：%ANT_HOME%\\lib

检测是否安装成功

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200717211414202.png)

注：如果出现ant不是内部或者外部命令，表示环境变量配置有误

## 二、Ant+jmeter搭建：

(1) 首先创建一个文件夹，例如dome（文件名称不要用下划线，空格等特殊字符），将jmeter保存的测试脚本放在该文件夹中。

(2) 将Jmeter extras文件中的ant-jmeter-1.1.1.jar放到Ant中的lib文件夹中。

(3) 将Jmeter extras文件中的jmeter-results-detail-report_21.xsl、build.xml、collapse.png、expand.png放到ant目录中的bin目录下面。

(4) 创建一个build.xml文件，修改此文件：[build.xml](../jmeter_test/dome/build.xml)

(5) 进入Jmeter的bin目录，找到jmeter.properties文件打开，然后将一下代码取消注释并改为true
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200717212400945.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2xpMjY0MjUzMDk3OQ==,size_16,color_FFFFFF,t_70)




(6) 把需要测试的jmx文件和build.xml文件放在同一个目录下

(7) 打开cmd, 运行ant run 运行

## 三、Jenkins配置

1、安装jenkins（jenkins-2.107.1，windows版本），安装完成后在浏览器中输入：http://localhost:8080/jenkins,默认端口为8080

2、安装插件

系统管理-\>插件管理，安装Ant Plugin、Email Extension Plugin、Email Extension Plugin

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200717212433716.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2xpMjY0MjUzMDk3OQ==,size_16,color_FFFFFF,t_70)

3、Jenkins全局工具配置-JDK

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200717212507337.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2xpMjY0MjUzMDk3OQ==,size_16,color_FFFFFF,t_70)



4、Jenkins全局工具配置-ANT

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200717212518365.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2xpMjY0MjUzMDk3OQ==,size_16,color_FFFFFF,t_70)


5. 创建自由风格的任务

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200717212541827.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2xpMjY0MjUzMDk3OQ==,size_16,color_FFFFFF,t_70)

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200717212621576.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2xpMjY0MjUzMDk3OQ==,size_16,color_FFFFFF,t_70)


![在这里插入图片描述](https://img-blog.csdnimg.cn/20200717212714249.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2xpMjY0MjUzMDk3OQ==,size_16,color_FFFFFF,t_70)
注：HTML directory to archive：存放html报告的路径，也可填写相对路径

6\. 立即构建

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200717212806140.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2xpMjY0MjUzMDk3OQ==,size_16,color_FFFFFF,t_70)



![在这里插入图片描述](https://img-blog.csdnimg.cn/20200717212819944.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2xpMjY0MjUzMDk3OQ==,size_16,color_FFFFFF,t_70)


构建成功后点击HTML report，显示生成的结果，到此结束；