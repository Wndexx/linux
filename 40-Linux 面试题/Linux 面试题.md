## Linux 面试题

### 问题1 分析日志 t.log（访问量）

> 分析日志 t.log（访问量），将各个 ip 地址截取，统计出现次数，并按从大到小顺序排序（腾讯）
>
> http://192.168.200.10/index1.html
> http://192.168.200.10/index2.html
> http://192.168.200.20/index1.html
> http://192.168.200.30/index1.html
> http://192.168.200.40/index1.html
> http://192.168.200.30/order.html
> http://192.168.200.10/order.html

```bash
cat t.txt | cut -d '/' -f 3 | sort | uniq -c | sort -nr
```



```bash
[root@wndexx interview]# vim t.txt
[root@wndexx interview]# cat t.txt 
http://192.168.200.10/index1.html
http://192.168.200.10/index2.html
http://192.168.200.20/index1.html
http://192.168.200.30/index1.html
http://192.168.200.40/index1.html
http://192.168.200.30/order.html
http://192.168.200.10/order.html
[root@wndexx interview]# cat t.txt | cut -d '/' -f 3
192.168.200.10
192.168.200.10
192.168.200.20
192.168.200.30
192.168.200.40
192.168.200.30
192.168.200.10
[root@wndexx interview]# cat t.txt | cut -d '/' -f 3 | sort
192.168.200.10
192.168.200.10
192.168.200.10
192.168.200.20
192.168.200.30
192.168.200.30
192.168.200.40
[root@wndexx interview]# cat t.txt | cut -d '/' -f 3 | sort | uniq -c
      3 192.168.200.10
      1 192.168.200.20
      2 192.168.200.30
      1 192.168.200.40
[root@wndexx interview]# cat t.txt | cut -d '/' -f 3 | sort | uniq -c | sort
      1 192.168.200.20
      1 192.168.200.40
      2 192.168.200.30
      3 192.168.200.10
[root@wndexx interview]# cat t.txt | cut -d '/' -f 3 | sort | uniq -c | sort -nr
      3 192.168.200.10
      2 192.168.200.30
      1 192.168.200.40
      1 192.168.200.20
```



> **cut**	在文件的每一行中提取片断
>
> 基本指令：`cut [选项] 文件`
>
> [选项]
>
> ​	-d  <字符>		以该字符作为分隔符。分隔符不能是 空格
>
> ​	-f    N		        输出指定位置的片段，从 1 开始。
>
> ​					  如果是 N-，输出第 N 个片段到最后一个片段
>
> ​					  如果是 N-M，输出第 N 个片段到第 M 个片段
>
> ​					  如果是 -N，输出第一个片段到第 N 个片段



> **sort**	对文本文件的行进行排序。将排序好的所有文件串写到标准输出上。默认从小到大
>
> 基本指令：`sort [选项] 文件`
>
> [选项]
>
> ​	-b     	忽略排序字段或关键字中开头的空格
>
> ​	-n    	 按照字符串的数值顺序比较,暗含 -b
>
> ​	-r     	 颠倒比较的结果



> **uniq**	删除排序文件中的重复行。从 INPUT (或 标准输入) 数据中忽略 (但是 保留 一行) ==连续==的相似行, 结果 送入 OUTPUT (或 标准输出)。
>
> 基本指令：`uniq [选项] [标准输入 [标准输出]]`
>
> ​	-c		在 行首显示出现的数目





### 问题2 统计连接到服务器的各个 ip 情况

> 统计连接到服务器的各个 ip 情况，并按连接数从大到小排序

```bash
netstat -an | grep ESTABLISHED | awk -F " " '{print $5}' | cut -d ":" -f 1 | sort | uniq -c | sort -nr
```



```bash
[root@wndexx interview]# netstat -an | grep ESTABLISHED
tcp        0      0 192.168.200.130:22      192.168.200.1:6699      ESTABLISHED
tcp        0     36 192.168.200.130:22      192.168.200.1:1405      ESTABLISHED
[root@wndexx interview]# netstat -an | grep ESTABLISHED | awk -F " " "{print $5}"
tcp        0      0 192.168.200.130:22      192.168.200.1:6699      ESTABLISHED
tcp        0     36 192.168.200.130:22      192.168.200.1:1405      ESTABLISHED
[root@wndexx interview]# netstat -an | grep ESTABLISHED | awk -F " " '{print $5}'
192.168.200.1:6699
192.168.200.1:1405
[root@wndexx interview]# netstat -an | grep ESTABLISHED | awk -F " " '{print $5}' | awk -F ":"  'print $1'
awk: cmd. line:1: print $1
awk: cmd. line:1: ^ syntax error
[root@wndexx interview]# netstat -an | grep ESTABLISHED | awk -F " " '{print $5}' | awk -F ":" 'print $1'
awk: cmd. line:1: print $1
awk: cmd. line:1: ^ syntax error
[root@wndexx interview]# netstat -an | grep ESTABLISHED | awk -F " " '{print $5}' | awk -F ":" '{print $1}'
192.168.200.1
192.168.200.1
[root@wndexx interview]# netstat -an | grep ESTABLISHED | awk -F " " '{print $5}' | cut -d ":" -f 1
192.168.200.1
192.168.200.1
[root@wndexx interview]# netstat -an | grep ESTABLISHED | awk -F " " '{print $5}' | cut -d ":" -f 1 | sort -nr
192.168.200.1
192.168.200.1
[root@wndexx interview]# netstat -an | grep ESTABLISHED | awk -F " " '{print $5}' | cut -d ":" -f 1 | sort
192.168.200.1
192.168.200.1
[root@wndexx interview]# netstat -an | grep ESTABLISHED | awk -F " " '{print $5}' | cut -d ":" -f 1 | sort | uniq -c
      2 192.168.200.1
[root@wndexx interview]# netstat -an | grep ESTABLISHED | awk -F " " '{print $5}' | cut -d ":" -f 1 | sort | uniq -c | sort -nr
      2 192.168.200.1

```



> awk	文本处理指令
>
> 基本语法：`awk -F 字符 '{处理程序}' 文件`
>
> 选项 
>
> ​	-F   <字符>	以该字符作为分隔符
>
> ​	'{处理程序}'       命令代码块。如 `print $5` 输出分割后的第 5 个片段，从 1 开始
>
> 说明：awk 的功能非常强大，需要详尽学习	





### 问题3 重置 mysql 数据库的 ROOT 用户的密码

> 如果忘记了 mysql5.7 数据库的 ROOT 用户的密码，如何找回？



- `vim /etc/my.cnf`，加入一句话 `skip-grant-tables`，即跳过权限表

  ```bash
  [root@wndexx interview]# vim /etc/my.cnf
  
  # For advice on how to change settings please see
  # http://dev.mysql.com/doc/refman/5.7/en/server-configuration-defaults.html
  
  [mysqld]
  #
  # Remove leading # and set to the amount of RAM for the most important data
  # cache in MySQL. Start at 70% of total RAM for dedicated server, else 10%.
  # innodb_buffer_pool_size = 128M
  #
  # Remove leading # to turn on a very important data integrity option: logging
  # changes to the binary log between backups.
  # log_bin
  #
  # Remove leading # to set options mainly useful for reporting servers.
  # The server defaults are faster for transactions and fast SELECTs.
  # Adjust sizes as needed, experiment to find the optimal values.
  # join_buffer_size = 128M
  # sort_buffer_size = 2M
  # read_rnd_buffer_size = 2M
  datadir=/var/lib/mysql
  socket=/var/lib/mysql/mysql.sock
  
  # Disabling symbolic-links is recommended to prevent assorted security risks
  symbolic-links=0
  
  log-error=/var/log/mysqld.log
  pid-file=/var/run/mysqld/mysqld.pid
  skip-grant-tables
  
  ```

  

- 重启 mysqld 服务

  ```bash
  service mysqld restart
  # 或
  systemctl restart mysqld
  ```

  

- 登录mysql，此时不再需要密码

  ```bash
  [root@wndexx interview]# systemctl restart mysqld
  [root@wndexx interview]# mysql -uroot -p
  Enter password: 
  Welcome to the MySQL monitor.  Commands end with ; or \g.
  Your MySQL connection id is 2
  Server version: 5.7.26 MySQL Community Server (GPL)
  
  Copyright (c) 2000, 2019, Oracle and/or its affiliates. All rights reserved.
  
  Oracle is a registered trademark of Oracle Corporation and/or its
  affiliates. Other names may be trademarks of their respective
  owners.
  
  Type 'help;' or '\h' for help. Type '\c' to clear the current input statement.
  
  mysql> 
  
  ```

  

- 更改 mysql 数据库的 user 表里 root 用户对应的的 authentication_string 值

  ```mysql
  # 1
  mysql> show databases;
  +--------------------+
  | Database           |
  +--------------------+
  | information_schema |
  | demodb             |
  | mysql              |
  | performance_schema |
  | sys                |
  +--------------------+
  5 rows in set (0.00 sec)
  
  
  # 2
  mysql> use mysql;
  Reading table information for completion of table and column names
  You can turn off this feature to get a quicker startup with -A
  
  Database changed
  
  
  # 3
  mysql> show tables;
  +---------------------------+
  | Tables_in_mysql           |
  +---------------------------+
  | columns_priv              |
  | db                        |
  | engine_cost               |
  | event                     |
  | func                      |
  | general_log               |
  | gtid_executed             |
  | help_category             |
  | help_keyword              |
  | help_relation             |
  | help_topic                |
  | innodb_index_stats        |
  | innodb_table_stats        |
  | ndb_binlog_index          |
  | plugin                    |
  | proc                      |
  | procs_priv                |
  | proxies_priv              |
  | server_cost               |
  | servers                   |
  | slave_master_info         |
  | slave_relay_log_info      |
  | slave_worker_info         |
  | slow_log                  |
  | tables_priv               |
  | time_zone                 |
  | time_zone_leap_second     |
  | time_zone_name            |
  | time_zone_transition      |
  | time_zone_transition_type |
  | user                      |
  +---------------------------+
  31 rows in set (0.00 sec)
  
  
  # 4
  mysql> desc user;
  ...
  | authentication_string  | text      | YES  |     | NULL      |       |
  ...
  
  
  # 5
  mysql> update user set authentication_string=password("root") where user='root';
  Query OK, 1 row affected, 1 warning (0.00 sec)
  Rows matched: 1  Changed: 1  Warnings: 1
  
  ```

  

- 刷新权限

  ```mysql
  flush privileges;
  ```



- 退出

  ```mysql
  exit;
  ```

  

- `vim /etc/my.cnf`，注释掉 `skip-grant-tables`

  ```bash
  [root@wndexx interview]# vim /etc/my.cnf
  
  # For advice on how to change settings please see
  # http://dev.mysql.com/doc/refman/5.7/en/server-configuration-defaults.html
  
  [mysqld]
  #
  # Remove leading # and set to the amount of RAM for the most important data
  # cache in MySQL. Start at 70% of total RAM for dedicated server, else 10%.
  # innodb_buffer_pool_size = 128M
  #
  # Remove leading # to turn on a very important data integrity option: logging
  # changes to the binary log between backups.
  # log_bin
  #
  # Remove leading # to set options mainly useful for reporting servers.
  # The server defaults are faster for transactions and fast SELECTs.
  # Adjust sizes as needed, experiment to find the optimal values.
  # join_buffer_size = 128M
  # sort_buffer_size = 2M
  # read_rnd_buffer_size = 2M
  datadir=/var/lib/mysql
  socket=/var/lib/mysql/mysql.sock
  
  # Disabling symbolic-links is recommended to prevent assorted security risks
  symbolic-links=0
  
  log-error=/var/log/mysqld.log
  pid-file=/var/run/mysqld/mysqld.pid
  # skip-grant-tables
  ```



- 重启 mysqld 服务

  ```bash
  systemctl restart mysqld
  ```

  

- 测试新密码登录

  ```bash
  [root@wndexx interview]# mysql -uroot -p
  Enter password: 
  Welcome to the MySQL monitor.  Commands end with ; or \g.
  Your MySQL connection id is 2
  Server version: 5.7.26 MySQL Community Server (GPL)
  
  Copyright (c) 2000, 2019, Oracle and/or its affiliates. All rights reserved.
  
  Oracle is a registered trademark of Oracle Corporation and/or its
  affiliates. Other names may be trademarks of their respective
  owners.
  
  Type 'help;' or '\h' for help. Type '\c' to clear the current input statement.
  
  mysql> 
  ```

  

### 问题 4 统计 ip 访问情况

> 写出指令：统计 ip 访问情况，要求分析 nginx 访问日志（access.log），找出访问页面数量在前 2 位的 ip

```bash
cat access.log | awk -F " " '{print $1}' | sort | uniq -c | sort -nr | head -2
```



```bash
===== access.log ======
192.168.130.21 aaa.html
192.168.130.20 aaa.html
192.168.130.20 aaa.html
192.168.130.20 aaa.html
192.168.130.23 aaa.html
192.168.130.20 aaa.html
192.168.130.25 aaa.html
192.168.130.20 aaa.html
192.168.130.20 aaa.html
192.168.130.25 aaa.html
192.168.130.20 aaa.html
=======================
```



```bash
[root@wndexx interview]# vim access.log
[root@wndexx interview]# cat access.log 
192.168.130.21 aaa.html
192.168.130.20 aaa.html
192.168.130.20 aaa.html
192.168.130.20 aaa.html
192.168.130.23 aaa.html
192.168.130.20 aaa.html
192.168.130.25 aaa.html
192.168.130.20 aaa.html
192.168.130.20 aaa.html
192.168.130.25 aaa.html
192.168.130.20 aaa.html 
[root@wndexx interview]# cat access.log | awk -F " " '{print $1}'
192.168.130.21
192.168.130.20
192.168.130.20
192.168.130.20
192.168.130.23
192.168.130.20
192.168.130.25
192.168.130.20
192.168.130.20
192.168.130.25
192.168.130.20
[root@wndexx interview]# cat access.log | awk -F " " '{print $1}' | sort
192.168.130.20
192.168.130.20
192.168.130.20
192.168.130.20
192.168.130.20
192.168.130.20
192.168.130.20
192.168.130.21
192.168.130.23
192.168.130.25
192.168.130.25
[root@wndexx interview]# cat access.log | awk -F " " '{print $1}' | sort | uniq -c
      7 192.168.130.20
      1 192.168.130.21
      1 192.168.130.23
      2 192.168.130.25
[root@wndexx interview]# cat access.log | awk -F " " '{print $1}' | sort | uniq -c | sort -nr
      7 192.168.130.20
      2 192.168.130.25
      1 192.168.130.23
      1 192.168.130.21
[root@wndexx interview]# cat access.log | awk -F " " '{print $1}' | sort | uniq -c | sort -nr | head -n 2
      7 192.168.130.20
      2 192.168.130.25
# 或
[root@wndexx interview]# cat access.log | awk -F " " '{print $1}' | sort | uniq -c | sort -nr | head -2
      7 192.168.130.20
      2 192.168.130.25
```





### 问题5  tcpdump 监听与本机某个端口进行通信的某个 IP

> 使用 tcpdump 监听本机，将来自 ip 192.168.200.1，tcp 端口为 22 的数据，保存的输出到 tcpdump.log，用来做数据分析

```bash
# tcpdump 监听某个ip 和本机某个端口的通信
tcpdump -i ens33 host 192.168.200.1 and port 22 >> /opt/interview/tcpdump.log
```



```bash
[root@wndexx interview]# tcpdump -i ens33 host 192.168.200.1 and port 22 >> /opt/interview/tcpdump.log
tcpdump: verbose output suppressed, use -v or -vv for full protocol decode
listening on ens33, link-type EN10MB (Ethernet), capture size 262144 bytes
^C4 packets captured
7 packets received by filter
0 packets dropped by kernel
[root@wndexx interview]# cat tcpdump.log 
19:06:32.169765 IP wndexx.ssh > PC.ibm-res: Flags [P.], seq 1269973929:1269974117, ack 2131995627, win 1105, length 188
19:06:32.170111 IP PC.ibm-res > wndexx.ssh: Flags [.], ack 188, win 4105, length 0
19:06:46.620019 IP PC.ibm-res > wndexx.ssh: Flags [P.], seq 1:37, ack 188, win 4105, length 36
19:06:46.660685 IP wndexx.ssh > PC.ibm-res: Flags [.], ack 37, win 1105, length 0
```



### 问题 6 Nginx 模块的用途

> 常用的 Nginx 模块，用来做什么

```bash
rewrite 模块			实现重写功能
access 模块			来源控制
ssl 模块				安全控制
ngx_http_gzip_module		网络传输压缩模块
ngx_http_proxy_module		实现代理
ngx_http_upstream_module 	实现定义后端服务器列表
ngx_cache_purge				实现缓存清除功能
```





























