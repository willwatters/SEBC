CM & CDH to use: Latest 5.14

Challenge start time: 9:06 - 12:06


List the cloud provider you are using: AWS

List the Linux release you have chosen: CentOS Linux release 7.5.1804


```
[root@ip-172-31-33-13 tmp]# uname -a
Linux ip-172-31-33-13.eu-west-3.compute.internal 3.10.0-862.3.2.el7.x86_64 #1 SMP Mon May 21 23:36:36 UTC 2018 x86_64 x86_64 x86_64 GNU/Linux

[root@ip-172-31-33-13 tmp]# cat /etc/redhat-release
CentOS Linux release 7.5.1804 (Core)
```


Show that the disk space on each node is at least 30 GB:

This has been checked on all nodes:

```
[root@ip-172-31-33-13 tmp]# df -h
Filesystem      Size  Used Avail Use% Mounted on
/dev/nvme0n1p1   30G  1.2G   29G   4% /
devtmpfs        7.6G     0  7.6G   0% /dev
tmpfs           7.6G     0  7.6G   0% /dev/shm
tmpfs           7.6G   17M  7.6G   1% /run
tmpfs           7.6G     0  7.6G   0% /sys/fs/cgroup
tmpfs           1.6G     0  1.6G   0% /run/user/1000
```

List the command and output for yum repolist enabled:

```
[root@ip-172-31-33-13 tmp]# yum repolist enabled
Loaded plugins: fastestmirror
Loading mirror speeds from cached hostfile
 * base: centos.quelquesmots.fr
 * extras: centos.mirror.fr.planethoster.net
 * updates: centos.crazyfrogs.org
repo id                                                                                           repo name                                                                                           status
base/7/x86_64                                                                                     CentOS-7 - Base                                                                                     9,911
extras/7/x86_64                                                                                   CentOS-7 - Extras                                                                                     432
updates/7/x86_64                                                                                  CentOS-7 - Updates                                                                                  1,561
repolist: 11,904
[root@ip-172-31-33-13 mysql-connector-java-5.1.46]#
```


Add the following Linux accounts to all nodes
User raffles with a UID of 2000
User fullerton with a UID of 3000
Create the group hotels and add fullerton to it
Create the group shops and add raffles to it

This was done on all hosts:

On all the hosts, create the users:

```
[root@ip-172-31-33-13 tmp]# useradd -u 2000 raffles
[root@ip-172-31-33-13 tmp]# useradd -u 3000 fullerton
[root@ip-172-31-33-13 tmp]# groupadd hotels
[root@ip-172-31-33-13 tmp]# groupadd shops
[root@ip-172-31-33-13 tmp]# usermod -a -G hotels fullerton
[root@ip-172-31-33-13 tmp]# usermod -a -G shops raffles
```

List the /etc/passwd entries for raffles and fullerton in your setup file
List the /etc/group entries for hotels and shops in your setup file

```
[root@ip-172-31-33-13 tmp]# cat /etc/passwd | grep raffles
raffles:x:2000:2000::/home/raffles:/bin/bash
[root@ip-172-31-33-13 tmp]# cat /etc/passwd | grep fullerton
fullerton:x:3000:3000::/home/fullerton:/bin/bash
[root@ip-172-31-33-13 tmp]# cat /etc/group | grep hotels
hotels:x:3001:fullerton
[root@ip-172-31-33-13 tmp]# cat /etc/group | grep shops
shops:x:3002:raffles
```
