git常用命令大全

查看状态信息：git status （查看工作区、暂存区状态）

添加到暂存区：git add [file name]（将工作区的“新建修改”添加到暂存区）

提交：git commit -m "commit message" [file name]（将暂存区的内容提交到本地库）



查看历史记录

git log --pretty=oneline（查看一行记录）

git log --oneline（查看一行记录）

git reflog（查看全部的记录）

​					多屏显示控制：

​						    1.空格向下翻页

​							2.b向上翻页

​							3.q退出



版本回滚

git reset --hard [索引值]  （既能前进又能后退）

git reset --hard ^				（只能后退）

git reset --hard ~10          	（只能后退）

reset命令的三个参数对比

--soft

​	仅仅在本地库移动HEAD指针

--mixed

​	在本地库移动HEAD指针并重置暂存区

--hard

​	在本地库移动HEAD指针，并重置暂存区和工作区

分支：

![img](https://gitee.com/lixiaokang66646/whales_photo/raw/master/img/QQ%E5%9B%BE%E7%89%8720200709095955.jpg)