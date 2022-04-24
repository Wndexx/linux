## 远程登录到 Linux 服务器

### 一、 为什么需要远程登录 Linux

公司开发时候， 具体的应用场景是这样的

- linux 服务器是开发小组共享

- 正式上线的项目是运行在公网

- 因此程序员需要远程登录到 Linux 进行项目管理或者开发

  

### 二、远程登录 Linux-Xshell

#### 2.1 介绍

- Xshell是目前最好的远程登录到 Linux 操作的软件，流畅的速度并且完美解决了中文乱码的问题， 是目前程序员首选的软件
- Xshell 是一个强大的安全终端模拟软件，它支持 SSH1, SSH2, 以及 Microsoft Windows 平台的 TELNET 协议
- Xshell 可以在 Windows 界面下用来访问远端不同系统下的服务器，从而比较好的达到远程控制终端的目的

#### 2.2 下载

下载 free-for-home-school 版本

地址: https://www.netsarang.com/en/free-for-home-school/

#### 2.3 使用

1. 查看 linux 系统网络接口配置信息

   ```bash
   ifconfig
   ```

2. 查看主机和虚拟系统是否网络通畅

   ```bash
   ping + 虚拟系统网络ip
   ```

3. 配置 Xshell

   ![1650761090642](E:\code\linux\8-Linux 实操篇-远程登录到 Linux 服务器\远程登录到 Linux 服务器.assets\1650761090642.png)

   

### 三、远程登录 Linux-Xftp

#### 3.1 介绍

Xftp 是一个基于 windows 平台的功能强大的 SFTP、FTP 文件传输软件。使用了 Xftp 以后，windows 用户能安全地在 UNIX/Linux 和 Windows PC 之间传输文件

#### 3.2 配置和使用

![1650761469178](E:\code\linux\8-Linux 实操篇-远程登录到 Linux 服务器\远程登录到 Linux 服务器.assets\1650761469178.png)

#### 3.3 乱码配置

![1650761575000](E:\code\linux\8-Linux 实操篇-远程登录到 Linux 服务器\远程登录到 Linux 服务器.assets\1650761575000.png)



