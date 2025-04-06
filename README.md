# 基于ABHPC系统的SCOW用户手册 <!-- omit in toc -->

[简体中文](README.md)|[English](README.en.md)

本教程适用于在ABHPC操作系统上配置了SCOW的超算平台用户，管理员另见[管理员手册](ADMIN.md)。

## 目录 <!-- omit in toc -->

- [1 用户初始化](#1-用户初始化)
  - [1.1 超算平台和管理系统界面切换](#11-超算平台和管理系统界面切换)
  - [1.2 文件系统初始化](#12-文件系统初始化)
  - [1.3 修改密码](#13-修改密码)
- [2 登录方式](#2-登录方式)
  - [2.1 Web登录](#21-web登录)
  - [2.2 SSH登录](#22-ssh登录)
  - [2.3 NX登录](#23-nx登录)
- [3 数据上传与下载](#3-数据上传与下载)
  - [3.1 Web文件管理(适合在线查看文件)](#31-web文件管理适合在线查看文件)
  - [3.2 sftp客户端文件传输(适合批量传输文件)](#32-sftp客户端文件传输适合批量传输文件)
- [4 命令行作业](#4-命令行作业)
  - [4.1 slmscript拷贝脚本模板](#41-slmscript拷贝脚本模板)
  - [4.2 提交作业](#42-提交作业)
  - [4.3 查看作业](#43-查看作业)
  - [4.4 终止作业](#44-终止作业)
- [5 图形化作业](#5-图形化作业)
- [6 账单查询](#6-账单查询)

## 1 用户初始化

### 1.1 超算平台和管理系统界面切换

用户有两个界面可切换：超算平台和管理系统。其中超算平台界面是用户的全部作业操作，而管理系统是用户管理自己的密码、费用和权限等操作。所有用户的超算界面相同，但不同权限的用户（普通用户、租户管理员、平台管理员、财务人员）的管理系统界面内容有差异。

用户登录进系统后，注意看**右上角**的面板切换图标，如果显示 ``管理系统``，则说明现在处于**超算平台**，点击 ``管理系统``可以进入**管理系统**界面，反之点击该按钮也可实现界面切换：

<div  align="center">  
<img src="image/README/1743867063380.png" width = "250" align=center />
</div>

如无特别强调，下述用户操作都是在**超算平台**界面上。

### 1.2 文件系统初始化

点击 ``桌面——>新建桌面``，然后选择 ``MATE``桌面，选择登录节点后，点确定按钮，即可完成用户初始化。

<div  align="center">  
<img src="image/README/1743867848645.png" width = "1200" align=center />
</div>

**Rocky Linux 8系统注意事项：** 由于Rocky Linux 8.10默认无MATE桌面，因此用户需要打开一个文件浏览器，然后选择 ``Edit——>Preferences——>Extensions``，然后选中 ``Open terminal``，点击 ``Configure Extension``按钮，将原来的 ``mate-terminal``修改为 ``xfce4-terminal``(如下图所示)。否则在文件夹中打开终端不会跟随当前目录，永远是打开 ``$HOME``目录。

<div  align="center">  
<img src="image/README/1743868191524.png" width = "1200" align=center />
</div>

### 1.3 修改密码

在**系统管理**界面，点击右上角的用户名，然后点击个人信息(如下图所示)，可以修改用户的密码和邮箱：

<div  align="center">  
<img src="image/README/1743868588249.png" width = "300" align=center />
</div>

## 2 登录方式

目前ABHPC系统提供三种登录方式：Web、SSH和NX。

### 2.1 Web登录

在浏览器中打开集群SCOW地址，输入用户名和密码登录即可。

### 2.2 SSH登录

SSH推荐使用客户端登录，跨平台的推荐[FinalShell](https://www.hostbuf.com)(付费高级版仅35元)，包含了ssh和sftp功能。ABHPC全系采用RSA密钥登录，首先下载私钥到本地，在文件管理系统打开 ``显示隐藏的项目``，然后打开 ``.ssh``文件夹，下载文件 ``id_rsa``（`<font color=red>`**注意：该文件非常重要，请妥善保管**`</font>`）：

<div  align="center">  
<img src="image/README/image.png" width = "1200" align=center />
</div>

在Finalshell中新建连接，导入下载的 ``id_rsa``文件即可：

<div  align="center">  
<img src="image/README/id_rsa.png" width = "400" align=center />
</div>

**小建议：** 如果你有多个主机的私钥，保管的时候，最好命名为 ``<username>@<hostname>.id_rsa``以免混淆。

### 2.3 NX登录

ABHPC提供基于Docker的NX远程桌面，可使用Nomachine客户端进行连接。每个用户的NX端口号不同，事前需要管理员提供用户唯一的NX端口号。

Nomachine客户端[下载地址](https://downloads.nomachine.com/download-enterprise/#NoMachine-Enterprise-Client)。

新建连接后，输入连接名、主机地址和端口号，登录即可：

<div  align="center">  
<img src="image/README/1743899795526.png" width = "600" align=center />
</div>

## 3 数据上传与下载

### 3.1 Web文件管理(适合在线查看文件)

<font color=red>**注意：** 由于web协议的限制，下载文件时，只能下载单个文件，且无法下载文件夹，该方法适合在线看文件，不适合批量下载文件。</font>

在用户界面的标签栏中点击“文件管理”，即可打开用户主目录，可进行文件的上传、下载、删除、移动、复制等操作。

<div  align="center">  
<img src="image/README/1743869232887.png" width = "1200" align=center />
</div>

### 3.2 sftp客户端文件传输(适合批量传输文件)

使用Finalshell登录后，可以在下方的sftp进行文件和文件夹的上传和下载操作：

<div  align="center">  
<img src="image/README/1743901390533.png" width = "600" align=center />
</div>

## 4 命令行作业

### 4.1 slmscript拷贝脚本模板
```slmscript```的使用详细见[slmscript命令](https://github.com/abhpc/slmscript)：
```bash
slmscript cp <job.slm>
```
### 4.2 提交作业
```bash
sbatch <job.slm>
```
### 4.3 查看作业
```bash
squeue
```
### 4.4 终止作业
```bash
scancel <job id>
```

## 5 图形化作业
网页登录页面后，打开```交互式作业——>创建应用```，选取所需的应用程序后，设置好资源，提交作业即可：
<div  align="center">  
<img src="image/README/1743907617927.png" width = "600" align=center />
</div>

## 6 账单查询

在**管理系统**页面首页可查看自己账户的余额和未结束作业信息：

<div  align="center">  
<img src="image/README/1743908020965.png" width = "1200" align=center />
</div>

进入```用户空间——>已结束的作业```可以查看自己的作业账单(只有作业结束了才完成计费)：

<div  align="center">  
<img src="image/README/1743907855289.png" width = "1200" align=center />
</div>