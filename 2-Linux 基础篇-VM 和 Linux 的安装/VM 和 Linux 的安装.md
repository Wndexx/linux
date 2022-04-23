## VM 和 Linux 的安装

### 一、VM 和 Linux 的关系

![1650692807688](E:\code\linux\2-Linux 基础篇-VM 和 Linux 的安装\VM 和 Linux 的安装.assets\1650692807688.png)



### 二、安装 VM

- 下载地址：<https://www.vmware.com/cn.html>
- 安装步骤
  - 在BIOS 开启 CPU 虚拟化支持
  - 按照安装步骤安装 VM

  

### 三、安装 CentOS 7.6

- 下载地址

  - CentOS 7.6 DVD 版 4G (目前主流的生产环境)
    - <http://mirrors.163.com/centos/7.6.1810/isos/x86_64/CentOS-7-x86_64-DVD-1810.iso>
  - CentOS 8.1 DVD 版 8G (未来的主流)
    - <https://mirrors.aliyun.com/centos/8.1.1911/isos/x86_64/CentOS-8.1.1911-x86_64-dvd1.iso>

- 安装步骤

  - 创建虚拟机

    - 指定磁盘容量：所分配的磁盘大小并不立即占有，而是随着系统资源的增大而增加，最大磁盘大小即为指定的磁盘容量

    - 网络连接的三种方式

      - 桥接模式：虚拟系统可以和外部系统通讯，但是容易造成IP冲突

      -  NAT模式：网络地址转换模式，虚拟系统可以和外部系统通讯，不造成IP冲突

      - 主机模式：独立的系统

        ![1650692912648](E:\code\linux\2-Linux 基础篇-VM 和 Linux 的安装\VM 和 Linux 的安装.assets\1650692912648.png)

  - Cent OS 7.6 配置

    - 软件选择（开发工具包含 gcc、jdk、mysql）

      ![1650693057597](E:\code\linux\2-Linux 基础篇-VM 和 Linux 的安装\VM 和 Linux 的安装.assets\1650693057597.png)

    - 安装目标位置

      ![1650693123294](E:\code\linux\2-Linux 基础篇-VM 和 Linux 的安装\VM 和 Linux 的安装.assets\1650693123294.png)

    -  手动分区

      ![1650693177968](E:\code\linux\2-Linux 基础篇-VM 和 Linux 的安装\VM 和 Linux 的安装.assets\1650693177968.png)

      ![1650693188715](E:\code\linux\2-Linux 基础篇-VM 和 Linux 的安装\VM 和 Linux 的安装.assets\1650693188715.png)![1650693290668](E:\code\linux\2-Linux 基础篇-VM 和 Linux 的安装\VM 和 Linux 的安装.assets\1650693290668.png)

      ![1650693229077](E:\code\linux\2-Linux 基础篇-VM 和 Linux 的安装\VM 和 Linux 的安装.assets\1650693229077.png)

      ![1650693239279](E:\code\linux\2-Linux 基础篇-VM 和 Linux 的安装\VM 和 Linux 的安装.assets\1650693239279.png)































