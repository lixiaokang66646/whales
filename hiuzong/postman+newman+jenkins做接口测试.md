# postman+newman+jenkins做接口测试



### windows上：

1.安装Jenkins集成环境

2.安装newman

- 安装node.js（参考[菜鸟教程node.js安装配置](https://www.runoob.com/nodejs/nodejs-install-setup.html)）

- 安装npm

  如果是Windows是随着node.js一块安装了，无需额为安装。

- 安装newman（cmd命令行中）

  > 安装时自动配置环境变量
  > 命令行检查：node -v
  > 安装newman
  > 命令行输入：npm install -g newman
  >
  > 命令行检查：newman -v

2.3对Jenkins进行配置，使postman+newman+jenkins关联在一起（参考[这里](http://www.baidu.com)）

Jenkins环境变量配置

- 点击首页的设置

  <img src="C:\Users\k\Desktop\测试\002.png" alt="002" style="zoom:70%;" />

- 进入配置选项

  <img src="C:\Users\k\Desktop\测试\003.png" alt="003" style="zoom:70%;" />

- 配置node.js和npm的全局变量

<img src="C:\Users\k\Desktop\测试\001.png" alt="001" style="zoom:70%;" />

- 配置jdk的全局变量

  <img src="C:\Users\k\Desktop\测试\004.png" alt="004" style="zoom:70%;" />