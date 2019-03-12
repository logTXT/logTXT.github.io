---
title: Manjaro安装手册
categories:
  - Manjaro
  - 安装
tags:
  - linux
  - Manjaro
  - install
abbrlink: f61d
date: 2019-03-09 17:16:37
---

### 获取Manjaro镜像

#### 进入[Manjaro](https://manjaro.org)官网

1. 下载Manjaro的时候不需要去各种镜像网站下载，Manjaro官网会在你开始下载前自动匹配合适的镜像网站
2. 不要使用旧版本的Manjaro安装，旧版本在系统升级时很可能会出现依赖问题导致无法升级或者安装应用，虽然有办法解决，但是为啥非要折腾自己呢？

<!-- more --> 

#### 选择桌面环境

Manjaro支持很多种桌面环境，选择前建议勾选上Beginner-friendly，然后选择一个发行版就可以开始下载了


### 制作Manjaro启动盘

参考自[Manjaro User Guide ](https://manjaro.org/support/userguide/)

#### 在Windows下制作

推荐使用[rufus](http://rufus.ie/)大小只有1M，可以[Rufus 3.4 Portable](https://github.com/pbatard/rufus/releases/download/v3.4/rufus-3.4p.exe) （便携版）无需安装直接使用

软件截图如下

![rufus截图](https://i.loli.net/2019/03/12/5c868e05c545a.png)

1. 设备选项选择你插入的U盘
2. ISO选择刚刚下载的Manjaro安装镜像
3. 其他保持默认点击开始
4. 在弹出的窗口中选择DD模式写入（第二个选项），不要使用默认的ISO模式
5. 等待程序运行完毕

#### 在Linux下制作

1. 插入U盘，打开终端进入镜像文件所在目录

2. 使用fdisk命令查看设备信息，记录下你的U盘编号（格式就像：/dev/sdb）

   ```bash
   sudo fdisk -l
   ```

3. 使用DD命令写入磁盘 `if`后面接ISO文件名可以使用tab自动补全 `of`是你的U盘编号 

   ```bash
   sudo dd if=manjaro-xfce-18.0-stable-x86_64.iso of=/dev/(上面的U盘编号) bs=4M
   ```

   我的U盘是/dev/sdb，所以我的命令应该改成

   ```bash
   sudo dd if=manjaro-xfce-18.0-stable-x86_64.iso of=/dev/sdb bs=4M 
   ```

   #### 命令最后可以加上` status=progress`显示dd制作的进度

4. 一段时间的等待

### 开始安装Manjaro

电脑关机，插入制作好的启动盘 ，进入欢迎界面，如下图所示

![welcome to Manjaro](https://i.loli.net/2019/03/12/5c868da08465e.png)

> 进入安装界面有一个前提，需要进入电脑的BIOS系统中调整启动顺序，将你的启动盘放到最上面。电脑进入启动盘的方式一般是开机时按F2或F12，如果不行请自行百度相应电脑型号如何进入BIOS

#### 启动测试环境

时区改为Asia/Shanghai

语言改为中文

然后选择Boot那一项就可以启动Manjaro的测试环境

你可以在这里试用Manjaro系统，在试用过程中进行的设置操作均不会保存

觉得不错就可以准备安装了系统会弹出一个hello程序，找到Installer选项（或者直接点击桌面上的Installer文件

#### 进入装机程序

1. 选择语言为简体中文
2. 选择时区为Asia、Shanghai
3. 选择分区方案：可以选择一个空的磁盘或者自己手动分区

下面是Manjaro中文社区中关于磁盘分区的部分讨论，这里可以做一个参考。

> **必须**准备一个256mb，格式fat32的分区，挂载点/boot/efi，设置成esp。（安装过程中会提示，当然256mb是非常绰绰有余了，我看到过别人说只设置100mb，这个你自行尝试）
>
> 关于分几个区，有些人会建议 / 一个分区， /home一个分区，然而/home中会有很多配置文件，如果新系统有洁癖的小伙伴，这么做会不大爽，
>
> 我个人的建议是 / 一个分区，然后/home/下载 挂载一个分区（不见得把自己下载的数据每次都格式化掉对吧），然后这个分区里设置一个譬如Document的目录，新系统安装好后把这个文件夹ln -s到/home/文档，这样就行了。
>
> 关于swap分区嘛，以前的人都会分，但现在的内存都很大，所以我觉得可以不要分，但安装完系统可以：
> dd if=/dev/zero of=/swapfile bs=1024M count=2 （这里是分了2G的swap，dd命令可以自行搜索）
> mkswap /swapfile
> swapon /swapfile
> 然后写进fstab：
> /swapfile swap swap defaults,noatime 0 2
>
> 总结：3个分区一个/swapfile，一个是fat32的挂载/boot/efi（强制），另一个是 / （ext4），第三个是 /home/下载（ext4）。
> 我自己的硬盘是512G的，我给 / 分了50G，swapfile暂时给了1G不够再换个大点的文件。（内存4g的老笔记本）

4. 配置用户名称、电脑名称、用户密码，以及管理员密码
5. 预览安装配置信息
6. 开始安装

### 安装结束

等到安装结束之后，就可以关闭电脑、拔出U盘、开机开始Manjaro的体验之旅



TodoList

- [ ] 一篇关于Manjaro配置方面的笔记
