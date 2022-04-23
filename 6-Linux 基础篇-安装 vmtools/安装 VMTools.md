## 安装 VMTools

### 一、介绍

1. vmtools 安装后，可以在 windows 下更好的管理 vm 虚拟机
2. 可以设置 windows 和 centos 的共享文件夹

![1650697747677](E:\code\linux\6-Linux 基础篇-安装 vmtools\安装 VMTools.assets\1650697747677.png)

### 二、步骤

1. 进入 centos

2. 点击 vm 菜单的 -> install vmware tools

3. centos 会出现一个 vm 的安装包

   ![1650698217431](E:\code\linux\6-Linux 基础篇-安装 vmtools\安装 VMTools.assets\1650698217431.png)

4. 拷贝到 /opt

   ![1650698299128](E:\code\linux\6-Linux 基础篇-安装 vmtools\安装 VMTools.assets\1650698299128.png)

5. 使用解压命令 tar, 得到一个安装文件

   ```bash
   # 进入到 opt 目录
   cd /opt/ 
   # 解压
   tar -zxvf VMwareTools-10.3.23-17030940.tar.gz 
   ```

   

6. 进入该 vm 解压的目录 , /opt 目录下

   ```bash
   # 进入 vm 解压的目录
   cd vmware-tools-distrib/
   ```

   

7. 安装

   ```bash
   # 安装
   ./vmware-install.pl 
   ```

   

8. 全部使用默认设置即可, 就可以安装成

9. 注意：安装 vmtools 需要有 ==gcc== 

   ```bash
   # 检查是否安装 gcc
   gcc -v
   ```

   

### 三、设置共享文件夹

1. 设置一个共享文件夹，比如 D:\VMware\myshare

2. 虚拟机设置里添加共享文件夹

   ![1650699197333](E:\code\linux\6-Linux 基础篇-安装 vmtools\安装 VMTools.assets\1650699197333.png)

3. 共享文件夹在 centos 的 /mnt/hgfs/ 下

4. 通过 vmtools，windows 和 centos 可以共享文件了，但是在实际开发中，文件的上传下载是需要使用 远程方式完成的