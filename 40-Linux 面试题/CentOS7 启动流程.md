## CentOS 7 启动流程

### 第一阶段：硬件启动阶段

这一阶段与 CentOS 6 类似



### 第二阶段：GRUB2 引导阶段

从这一步开始，CentOS6 和 CentOS7 的启动流程区别开始展现出来了

CentOS7的主引导程序使用的是 grub2，CentOS6 的主引导程序使用的是 grub

这一步的流程：

- 加载两个镜像 

  ```bash
  [root@wndexx boot]# ls
  config-3.10.0-1160.62.1.el7.x86_64
  config-3.10.0-957.el7.x86_64
  efi
  grub
  grub2
  initramfs-0-rescue-532787cee8ce4249a6c7c4c5ac01d6dd.img
  initramfs-3.10.0-1160.62.1.el7.x86_64.img
  ### initramfs-3.10.0-957.el7.x86_64.img
  lost+found
  symvers-3.10.0-1160.62.1.el7.x86_64.gz
  symvers-3.10.0-957.el7.x86_64.gz
  System.map-3.10.0-1160.62.1.el7.x86_64
  System.map-3.10.0-957.el7.x86_64
  vmlinuz-0-rescue-532787cee8ce4249a6c7c4c5ac01d6dd
  vmlinuz-3.10.0-1160.62.1.el7.x86_64
  ### vmlinuz-3.10.0-957.el7.x86_64
  
  ```

  

- 再加载 MOD 模块文件

- 把 grub2 程序加载执行

- 接着解析配置文件 /boot/grub2/grub.cfg

- 根据配置文件加载内核镜像到内存

- 之后构建虚拟根文件系统

- 最后转到内核

在这里 grub.cfg 配置文件已经比较复杂了，但并不用担心，到了 CentOS7 中一般是使用命令进行配置，而不直接去修改配置文件了。不过可以看到 grub.cfg 配置文件开头注释部分说明了由 /etc/grub.d/ 目录下文件和 /etc/default/grub 文件组成。

 一般修改好配置后都需要使用命令`grub2-mkconfig -o /boot/grub2/grub.cfg`，将配置文件重新生成



### 第三阶段：内核引导阶段

这一步与 CentOS6 也差不多，加载驱动，切换到真正的根文件系统，唯一不同的是执行的初始化程序变成了 /usr/lib/systemd/systemd



### 第四阶段：systemed 初始化阶段（又叫系统初始化阶段）

CentOS7 的初始化进程变为了 systemd

- 执行默认 target 配置文件 /etc/systemd/system/default.target（这是一个软链接，与默认运行级别有关）。
- 然后执行 sysinit.target 来初始化系统和 basic.target 来准备操作系统。
- 接着启动 multi-user.target 下的本机与服务器服务，并检查 /etc/rc.d/rc.local 文件是否有用户自定义脚本需要启动。
- 最后执行 multi-user 下的 getty.target 及登录服务，检查 default.target 是否有其他的服务需要启动

注意：

/etc/systemd/system/default.target 指向了 /lib/systemd/system/ 目录下的 graphical.target 或multiuser.target。

而 graphical.target 依赖 multiuser.target ，multiuser.target 依赖 basic.target，basic.target 依赖 sysinit.target，所以倒过来执行。



System概述（了解）：systemd 即为 system daemon，是 Linux 下的一种 init 软件，开发目标是提供更优秀的框架以表示系统服务间的依赖关系，并依此实现系统初始化时服务的并行启动，同时达到降低Shell系统开销的效果，最终代替现在常用的 System V 与 BSD 风格的 init 程序。

与多数发行版使用的 System V 风格的 init 相比，systemd 采用了以下的新技术：

- 采用 Socket 激活式与总线激活式服务，以提高相互依赖的各服务的并行运行性能
- 用 Cgroup 代替 PID 来追踪进程，即使是两次 fork 之后生成的守护进程也不会脱离 systemd 的控制

unit 对象：unit 表示不同类型的 systemd 对象，通过配置文件进行标识和配置；文件中主要包含了系统服务、监听 socket、保存的系统快照以及其它与 init 相关的信息。（也就是CentOS6中的服务器启动脚本）



> /etc/systemd/system/default.target

这是一个软链接，和默认运行级别相关

```bash
[root@wndexx ~]# ll /etc/systemd/system/default.target
lrwxrwxrwx. 1 root root 40 4月  29 18:02 /etc/systemd/system/default.target -> /usr/lib/systemd/system/graphical.target

[root@wndexx system]# cd /usr/lib/systemd/system/
[root@wndexx system]# ls *.target
anaconda.target            poweroff.target
basic.target               printer.target
bluetooth.target           rdma-hw.target
cryptsetup-pre.target      reboot.target
cryptsetup.target          remote-cryptsetup.target
ctrl-alt-del.target        remote-fs-pre.target
default.target             remote-fs.target
emergency.target           rescue.target
final.target               rpcbind.target
getty-pre.target           rpc_pipefs.target
getty.target               runlevel0.target
graphical.target           runlevel1.target
halt.target                runlevel2.target
hibernate.target           runlevel3.target
hybrid-sleep.target        runlevel4.target
initrd-fs.target           runlevel5.target
initrd-root-fs.target      runlevel6.target
initrd-switch-root.target  shutdown.target
initrd.target              sigpwr.target
iprutils.target            sleep.target
kexec.target               slices.target
local-fs-pre.target        smartcard.target
local-fs.target            sockets.target
machines.target            sound.target
multi-user.target          suspend.target
network-online.target      swap.target
network-pre.target         sysinit.target
network.target             system-update.target
nfs-client.target          timers.target
nss-lookup.target          time-sync.target
nss-user-lookup.target     umount.target
paths.target               virt-guest-shutdown.target
```



可以看到 runlevel 开头的 target 文件，对应着 CentOS6 的启动级别，不过一样是软链接，指向了同目录下的其它文件，也算一种向下兼容吧

```bash
[root@wndexx system]# ll runlevel*.target
lrwxrwxrwx. 1 root root 15 5月   1 11:59 runlevel0.target -> poweroff.target
lrwxrwxrwx. 1 root root 13 5月   1 11:59 runlevel1.target -> rescue.target
lrwxrwxrwx. 1 root root 17 5月   1 11:59 runlevel2.target -> multi-user.target
lrwxrwxrwx. 1 root root 17 5月   1 11:59 runlevel3.target -> multi-user.target
lrwxrwxrwx. 1 root root 17 5月   1 11:59 runlevel4.target -> multi-user.target
lrwxrwxrwx. 1 root root 16 5月   1 11:59 runlevel5.target -> graphical.target
lrwxrwxrwx. 1 root root 13 5月   1 11:59 runlevel6.target -> reboot.target
```

可以看到 default.target 与 runlevel5.target 指向的是同一个文件，默认运行级别是 5



> /usr/lib/systemd/system/

这个目录存储每个服务的脚本，类似 CentOS6 的/etc/init.d/。



> /run/systemd/system/

系统执行过程中产生的脚本。



> /etc/systemd/system/

类似于 CentOS6 的 /etc/rc.d/rc#.d/SXX 类文件的功能，管理员建立的执行脚本，大部分是 软链接



**符号链接**（**软链接、Symbolic link**）是一类特殊的文件， 其包含有一条以绝对路径或者相对路径的形式指向其它文件或者目录的引用



**硬链接**（**hard link**）是计算机文件系统中的多个文件平等地共享同一个文件存储单元

硬链接必须在同一个文件系统中；一般用户权限下的硬链接只能用于文件，不能用于目录，因为其父目录就有歧义了。删除一个文件名字后，还可以用其它名字继续访问该文件。硬链接只能用于同一个文件系统（对于NTFS是限制于同一个分区）。不能用于不存在的文件















