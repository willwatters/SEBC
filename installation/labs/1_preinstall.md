# System Configuration Checks

The following system configuration checks were done on all servers.  Below is the output from one of them.


## Check and configure vm.swappiness

Check current setting for vm.swappiness:

```
[root@ip-172-31-32-222 ~]# sysctl vm.swappiness
vm.swappiness = 30
```

Change to recommended setting of 1 and verify:

```
[root@ip-172-31-32-222 ~]# echo "vm.swappiness = 1" >> /etc/sysctl.conf

[root@ip-172-31-32-222 ~]# sysctl -p
vm.swappiness = 1
[root@ip-172-31-32-222 ~]# sysctl vm.swappiness
vm.swappiness = 1
[root@ip-172-31-32-222 ~]# cat /proc/sys/vm/swappiness
1

```


## Show the mount attributes of all volumes and update so it is noatime

```
[root@ip-172-31-32-222 ~]# cat /etc/fstab

#
# /etc/fstab
# Created by anaconda on Tue Jun  5 14:06:12 2018
#
# Accessible filesystems, by reference, are maintained under '/dev/disk'
# See man pages fstab(5), findfs(8), mount(8) and/or blkid(8) for more info
#
UUID=8c1540fa-e2b4-407d-bcd1-59848a73e463 /                       xfs     defaults        0 0
```

Update /etc/fstab so it is set to noatime:

```
[root@ip-172-31-32-222 ~]# vi /etc/fstab
[root@ip-172-31-32-222 ~]# mount -o remount /
```

Verify and show updated mount attributes:

```
[root@ip-172-31-32-222 ~]# df -h
Filesystem      Size  Used Avail Use% Mounted on
/dev/nvme0n1p1   30G  894M   30G   3% /
devtmpfs        7.6G     0  7.6G   0% /dev
tmpfs           7.6G     0  7.6G   0% /dev/shm
tmpfs           7.6G   17M  7.6G   1% /run
tmpfs           7.6G     0  7.6G   0% /sys/fs/cgroup
tmpfs           1.6G     0  1.6G   0% /run/user/1000
tmpfs           1.6G     0  1.6G   0% /run/user/0

[root@ip-172-31-32-222 ~]# cat /etc/fstab

#
# /etc/fstab
# Created by anaconda on Tue Jun  5 14:06:12 2018
#
# Accessible filesystems, by reference, are maintained under '/dev/disk'
# See man pages fstab(5), findfs(8), mount(8) and/or blkid(8) for more info
#
UUID=8c1540fa-e2b4-407d-bcd1-59848a73e463 /                       xfs    defaults,noatime        0 0
```


## Show the reserve space of any non-root, ext-based volumes

This uses XFS volumes, which do not maintain reserve space:

```
[root@ip-172-31-32-222 ~]# cat /etc/fstab

#
# /etc/fstab
# Created by anaconda on Tue Jun  5 14:06:12 2018
#
# Accessible filesystems, by reference, are maintained under '/dev/disk'
# See man pages fstab(5), findfs(8), mount(8) and/or blkid(8) for more info
#
UUID=8c1540fa-e2b4-407d-bcd1-59848a73e463 /                       xfs    defaults,noatime        0 0
```


## Disable transparent hugepage support

Check current setting:

```
[root@ip-172-31-32-222 ~]# cat /sys/kernel/mm/transparent_hugepage/defrag
[always] madvise never
[root@ip-172-31-32-222 ~]# cat /sys/kernel/mm/transparent_hugepage/enabled
[always] madvise never
```

Disable Transparent Hugepage support:

```
[root@ip-172-31-32-222 ~]# echo never > /sys/kernel/mm/transparent_hugepage/defrag
[root@ip-172-31-32-222 ~]# cat /sys/kernel/mm/transparent_hugepage/defrag
always madvise [never]

[root@ip-172-31-32-222 ~]# echo never > /sys/kernel/mm/transparent_hugepage/enabled
[root@ip-172-31-32-222 ~]# cat /sys/kernel/mm/transparent_hugepage/enabled
always madvise [never]
```


Permanently disable Transparent Hugepage support (i.e. applied after server reboots):

```
[root@ip-172-31-32-222 ~]# chmod +x /etc/rc.d/rc.local
[root@ip-172-31-32-222 ~]# echo "echo never > /sys/kernel/mm/transparent_hugepage/defrag" >> /etc/rc.local
[root@ip-172-31-32-222 ~]# echo "echo never > /sys/kernel/mm/transparent_hugepage/enabled" >> /etc/rc.local
[root@ip-172-31-32-222 ~]# cat /etc/rc.d/rc.local
#!/bin/bash
# THIS FILE IS ADDED FOR COMPATIBILITY PURPOSES
#
# It is highly advisable to create own systemd services or udev rules
# to run scripts during boot instead of using this file.
#
# In contrast to previous versions due to parallel execution during boot
# this script will NOT be run after all other services.
#
# Please note that you must run 'chmod +x /etc/rc.d/rc.local' to ensure
# that this script will be executed during boot.

touch /var/lock/subsys/local
echo never > /sys/kernel/mm/transparent_hugepage/defrag
echo never > /sys/kernel/mm/transparent_hugepage/enabled

[root@ip-172-31-32-222 ~]# ls -l /etc/rc.d/rc.local
-rwxr-xr-x. 1 root root 586 Oct 15 13:10 /etc/rc.d/rc.local
```


## List your network interface configuration

```
[root@ip-172-31-32-222 ~]# ifconfig -a
ens5: flags=4163<UP,BROADCAST,RUNNING,MULTICAST>  mtu 9001
        inet 172.31.32.222  netmask 255.255.240.0  broadcast 172.31.47.255
        inet6 fe80::cd1:3dff:fed0:a24c  prefixlen 64  scopeid 0x20<link>
        ether 0e:d1:3d:d0:a2:4c  txqueuelen 1000  (Ethernet)
        RX packets 2353  bytes 211722 (206.7 KiB)
        RX errors 0  dropped 0  overruns 0  frame 0
        TX packets 1591  bytes 409086 (399.4 KiB)
        TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0

lo: flags=73<UP,LOOPBACK,RUNNING>  mtu 65536
        inet 127.0.0.1  netmask 255.0.0.0
        inet6 ::1  prefixlen 128  scopeid 0x10<host>
        loop  txqueuelen 1000  (Local Loopback)
        RX packets 6  bytes 416 (416.0 B)
        RX errors 0  dropped 0  overruns 0  frame 0
        TX packets 6  bytes 416 (416.0 B)
        TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0

[root@ip-172-31-32-222 ~]# ls -l /etc/sysconfig/network-scripts/
total 232
-rw-r--r--. 1 root root   159 Oct 15 12:16 ifcfg-ens5
-rw-r--r--. 1 root root   126 Jun  5 14:13 ifcfg-eth0
-rw-r--r--. 1 root root   254 Jan  2  2018 ifcfg-lo
lrwxrwxrwx. 1 root root    24 Jun  5 14:08 ifdown -> ../../../usr/sbin/ifdown
-rwxr-xr-x. 1 root root   654 Jan  2  2018 ifdown-bnep
-rwxr-xr-x. 1 root root  6569 Jan  2  2018 ifdown-eth
-rwxr-xr-x. 1 root root   781 Jan  2  2018 ifdown-ippp
-rwxr-xr-x. 1 root root  4540 Jan  2  2018 ifdown-ipv6
lrwxrwxrwx. 1 root root    11 Jun  5 14:08 ifdown-isdn -> ifdown-ippp
-rwxr-xr-x. 1 root root  2102 Jan  2  2018 ifdown-post
-rwxr-xr-x. 1 root root  1068 Jan  2  2018 ifdown-ppp
-rwxr-xr-x. 1 root root   870 Jan  2  2018 ifdown-routes
-rwxr-xr-x. 1 root root  1456 Jan  2  2018 ifdown-sit
-rwxr-xr-x. 1 root root  1621 Mar 17  2017 ifdown-Team
-rwxr-xr-x. 1 root root  1556 Mar 17  2017 ifdown-TeamPort
-rwxr-xr-x. 1 root root  1462 Jan  2  2018 ifdown-tunnel
lrwxrwxrwx. 1 root root    22 Jun  5 14:08 ifup -> ../../../usr/sbin/ifup
-rwxr-xr-x. 1 root root 12415 Jan  2  2018 ifup-aliases
-rwxr-xr-x. 1 root root   910 Jan  2  2018 ifup-bnep
-rwxr-xr-x. 1 root root 13442 Jan  2  2018 ifup-eth
-rwxr-xr-x. 1 root root 12075 Jan  2  2018 ifup-ippp
-rwxr-xr-x. 1 root root 11893 Jan  2  2018 ifup-ipv6
lrwxrwxrwx. 1 root root     9 Jun  5 14:08 ifup-isdn -> ifup-ippp
-rwxr-xr-x. 1 root root   650 Jan  2  2018 ifup-plip
-rwxr-xr-x. 1 root root  1064 Jan  2  2018 ifup-plusb
-rwxr-xr-x. 1 root root  4981 Jan  2  2018 ifup-post
-rwxr-xr-x. 1 root root  4154 Jan  2  2018 ifup-ppp
-rwxr-xr-x. 1 root root  2001 Jan  2  2018 ifup-routes
-rwxr-xr-x. 1 root root  3303 Jan  2  2018 ifup-sit
-rwxr-xr-x. 1 root root  1755 Mar 17  2017 ifup-Team
-rwxr-xr-x. 1 root root  1876 Mar 17  2017 ifup-TeamPort
-rwxr-xr-x. 1 root root  2711 Jan  2  2018 ifup-tunnel
-rwxr-xr-x. 1 root root  1836 Jan  2  2018 ifup-wireless
-rwxr-xr-x. 1 root root  5419 Jan  2  2018 init.ipv6-global
-rw-r--r--. 1 root root 19948 Jan  2  2018 network-functions
-rw-r--r--. 1 root root 31027 Jan  2  2018 network-functions-ipv6

[root@ip-172-31-32-222 ~]# cat /etc/sysconfig/network-scripts/ifcfg-eth0
DEVICE="eth0"
BOOTPROTO="dhcp"
ONBOOT="yes"
TYPE="Ethernet"
USERCTL="yes"
PEERDNS="yes"
IPV6INIT="no"
PERSISTENT_DHCLIENT="1"

[root@ip-172-31-32-222 ~]# cat /etc/sysconfig/network-scripts/ifcfg-ens5
# Created by cloud-init on instance boot automatically, do not edit.
#
BOOTPROTO=dhcp
DEVICE=ens5
HWADDR=0e:d1:3d:d0:a2:4c
ONBOOT=yes
TYPE=Ethernet
USERCTL=no

[root@ip-172-31-32-222 ~]# netstat -i
Kernel Interface table
Iface      MTU    RX-OK RX-ERR RX-DRP RX-OVR    TX-OK TX-ERR TX-DRP TX-OVR Flg
ens5      9001     2540      0      0 0          1694      0      0      0 BMRU
lo       65536        6      0      0 0             6      0      0      0 LRU

[root@ip-172-31-32-222 ~]# ip addr show
1: lo: <LOOPBACK,UP,LOWER_UP> mtu 65536 qdisc noqueue state UNKNOWN group default qlen 1000
    link/loopback 00:00:00:00:00:00 brd 00:00:00:00:00:00
    inet 127.0.0.1/8 scope host lo
       valid_lft forever preferred_lft forever
    inet6 ::1/128 scope host
       valid_lft forever preferred_lft forever
2: ens5: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 9001 qdisc mq state UP group default qlen 1000
    link/ether 0e:d1:3d:d0:a2:4c brd ff:ff:ff:ff:ff:ff
    inet 172.31.32.222/20 brd 172.31.47.255 scope global dynamic ens5
       valid_lft 3179sec preferred_lft 3179sec
    inet6 fe80::cd1:3dff:fed0:a24c/64 scope link
       valid_lft forever preferred_lft forever
```

## List forward and reverse host lookups using getent or nslookup

List of hosts in the cluster:
```
[root@ip-172-31-32-222 ~]# getent ahosts
127.0.0.1       localhost localhost.localdomain localhost4 localhost4.localdomain4
127.0.0.1       localhost localhost.localdomain localhost6 localhost6.localdomain6
172.31.32.222   ip-172-31-32-222.eu-west-3.compute.internal cm
172.31.39.85    ip-172-31-39-85.eu-west-3.compute.internal dnode1
172.31.47.1     ip-172-31-47-1.eu-west-3.compute.internal dnode2
172.31.46.203   ip-172-31-46-203.eu-west-3.compute.internal dnode3
172.31.38.0     ip-172-31-38-0.eu-west-3.compute.internal dnode4
```

Forward host lookups:

```
[root@ip-172-31-32-222 ~]# getent hosts ip-172-31-32-222.eu-west-3.compute.internal
172.31.32.222   ip-172-31-32-222.eu-west-3.compute.internal cm
[root@ip-172-31-32-222 ~]# getent hosts ip-172-31-39-85.eu-west-3.compute.internal
172.31.39.85    ip-172-31-39-85.eu-west-3.compute.internal dnode1
[root@ip-172-31-32-222 ~]# getent hosts ip-172-31-47-1.eu-west-3.compute.internal
172.31.47.1     ip-172-31-47-1.eu-west-3.compute.internal dnode2
[root@ip-172-31-32-222 ~]# getent hosts ip-172-31-46-203.eu-west-3.compute.internal
172.31.46.203   ip-172-31-46-203.eu-west-3.compute.internal dnode3
[root@ip-172-31-32-222 ~]# getent hosts ip-172-31-38-0.eu-west-3.compute.internal
172.31.38.0     ip-172-31-38-0.eu-west-3.compute.internal dnode4
```

Reverse host lookups:

```
[root@ip-172-31-32-222 ~]# getent hosts 172.31.32.222
172.31.32.222   ip-172-31-32-222.eu-west-3.compute.internal cm
[root@ip-172-31-32-222 ~]# getent hosts 172.31.39.85
172.31.39.85    ip-172-31-39-85.eu-west-3.compute.internal dnode1
[root@ip-172-31-32-222 ~]# getent hosts 172.31.47.1
172.31.47.1     ip-172-31-47-1.eu-west-3.compute.internal dnode2
[root@ip-172-31-32-222 ~]# getent hosts 172.31.46.203
172.31.46.203   ip-172-31-46-203.eu-west-3.compute.internal dnode3
[root@ip-172-31-32-222 ~]# getent hosts 172.31.38.0
172.31.38.0     ip-172-31-38-0.eu-west-3.compute.internal dnode4
```

DNS not used so nslookup N/A:

```
[root@ip-172-31-32-222 ~]# nslookup ip-172-31-32-222.eu-west-3.compute.internal
-bash: nslookup: command not found
[root@ip-172-31-32-222 ~]# nslookup 172.31.32.222
-bash: nslookup: command not found
```


## Show the nscd service is running:

Nscd service not running:

```
[root@ip-172-31-32-222 ~]# systemctl status nscd
Unit nscd.service could not be found.
```

Install nscd:

```
[root@ip-172-31-32-222 ~]# yum install nscd
```

Enable nscd service for reboots:

```
[root@ip-172-31-32-222 ~]# systemctl enable nscd
Created symlink from /etc/systemd/system/multi-user.target.wants/nscd.service to /usr/lib/systemd/system/nscd.service.
Created symlink from /etc/systemd/system/sockets.target.wants/nscd.socket to /usr/lib/systemd/system/nscd.socket.
```

Start nscd service and check status:

```
[root@ip-172-31-32-222 ~]# systemctl start nscd

[root@ip-172-31-32-222 ~]# systemctl status nscd
● nscd.service - Name Service Cache Daemon
   Loaded: loaded (/usr/lib/systemd/system/nscd.service; enabled; vendor preset: disabled)
   Active: active (running) since Mon 2018-10-15 13:29:57 UTC; 10s ago
  Process: 17320 ExecStart=/usr/sbin/nscd $NSCD_OPTIONS (code=exited, status=0/SUCCESS)
 Main PID: 17321 (nscd)
   CGroup: /system.slice/nscd.service
           └─17321 /usr/sbin/nscd

Oct 15 13:29:57 ip-172-31-32-222.eu-west-3.compute.internal nscd[17321]: 17321 monitoring file `/etc/hosts` (4)
Oct 15 13:29:57 ip-172-31-32-222.eu-west-3.compute.internal nscd[17321]: 17321 monitoring directory `/etc` (2)
Oct 15 13:29:57 ip-172-31-32-222.eu-west-3.compute.internal nscd[17321]: 17321 monitoring file `/etc/resolv.conf` (5)
Oct 15 13:29:57 ip-172-31-32-222.eu-west-3.compute.internal nscd[17321]: 17321 monitoring directory `/etc` (2)
Oct 15 13:29:57 ip-172-31-32-222.eu-west-3.compute.internal nscd[17321]: 17321 monitoring file `/etc/services` (6)
Oct 15 13:29:57 ip-172-31-32-222.eu-west-3.compute.internal nscd[17321]: 17321 monitoring directory `/etc` (2)
Oct 15 13:29:57 ip-172-31-32-222.eu-west-3.compute.internal nscd[17321]: 17321 disabled inotify-based monitoring for file `/etc/netgroup': No such file or directory
Oct 15 13:29:57 ip-172-31-32-222.eu-west-3.compute.internal nscd[17321]: 17321 stat failed for file `/etc/netgroup'; will try again later: No such file or directory
Oct 15 13:29:57 ip-172-31-32-222.eu-west-3.compute.internal nscd[17321]: 17321 Access Vector Cache (AVC) started
Oct 15 13:29:57 ip-172-31-32-222.eu-west-3.compute.internal systemd[1]: Started Name Service Cache Daemon.
```

Ntpd service not running:

```
[root@ip-172-31-32-222 ~]# systemctl status ntpd
Unit ntpd.service could not be found.
```


Install ntpd:

```
[root@ip-172-31-32-222 ~]# yum install ntp
```

Enable ntpd service for reboots:

```
[root@ip-172-31-32-222 ~]# systemctl enable ntpd
Created symlink from /etc/systemd/system/multi-user.target.wants/ntpd.service to /usr/lib/systemd/system/ntpd.service.
```

Start nscd service and check status:

```
[root@ip-172-31-32-222 ~]# systemctl start ntpd
[root@ip-172-31-32-222 ~]# systemctl status ntpd
● ntpd.service - Network Time Service
   Loaded: loaded (/usr/lib/systemd/system/ntpd.service; enabled; vendor preset: disabled)
   Active: active (running) since Mon 2018-10-15 13:27:30 UTC; 3s ago
  Process: 17269 ExecStart=/usr/sbin/ntpd -u ntp:ntp $OPTIONS (code=exited, status=0/SUCCESS)
 Main PID: 17270 (ntpd)
   CGroup: /system.slice/ntpd.service
           └─17270 /usr/sbin/ntpd -u ntp:ntp -g

Oct 15 13:27:30 ip-172-31-32-222.eu-west-3.compute.internal ntpd[17270]: Listen and drop on 0 v4wildcard 0.0.0.0 UDP 123
Oct 15 13:27:30 ip-172-31-32-222.eu-west-3.compute.internal ntpd[17270]: Listen and drop on 1 v6wildcard :: UDP 123
Oct 15 13:27:30 ip-172-31-32-222.eu-west-3.compute.internal ntpd[17270]: Listen normally on 2 lo 127.0.0.1 UDP 123
Oct 15 13:27:30 ip-172-31-32-222.eu-west-3.compute.internal ntpd[17270]: Listen normally on 3 ens5 172.31.32.222 UDP 123
Oct 15 13:27:30 ip-172-31-32-222.eu-west-3.compute.internal ntpd[17270]: Listen normally on 4 lo ::1 UDP 123
Oct 15 13:27:30 ip-172-31-32-222.eu-west-3.compute.internal ntpd[17270]: Listen normally on 5 ens5 fe80::cd1:3dff:fed0:a24c UDP 123
Oct 15 13:27:30 ip-172-31-32-222.eu-west-3.compute.internal ntpd[17270]: Listening on routing socket on fd #22 for interface updates
Oct 15 13:27:31 ip-172-31-32-222.eu-west-3.compute.internal ntpd[17270]: 0.0.0.0 c016 06 restart
Oct 15 13:27:31 ip-172-31-32-222.eu-west-3.compute.internal ntpd[17270]: 0.0.0.0 c012 02 freq_set kernel 0.000 PPM
Oct 15 13:27:31 ip-172-31-32-222.eu-west-3.compute.internal ntpd[17270]: 0.0.0.0 c011 01 freq_not_set
```


Check synchronised settings:

```
[root@ip-172-31-32-222 ~]# date
Mon Oct 15 13:31:01 UTC 2018

[root@ip-172-31-32-222 ~]# ntpstat
synchronised to NTP server (194.158.196.171) at stratum 3
   time correct to within 269 ms
   polling server every 64 s
[root@ip-172-31-32-222 ~]# date
Mon Oct 15 13:28:21 UTC 2018

[root@ip-172-31-32-222 ~]# time

real  0m0.000s
user  0m0.000s
sys 0m0.000s
```


## Check if selinux is disabled

Selinux not disabled:

```
[root@ip-172-31-32-222 ~]# cat /etc/sysconfig/selinux

# This file controls the state of SELinux on the system.
# SELINUX= can take one of these three values:
#     enforcing - SELinux security policy is enforced.
#     permissive - SELinux prints warnings instead of enforcing.
#     disabled - No SELinux policy is loaded.
SELINUX=enforcing
# SELINUXTYPE= can take one of three two values:
#     targeted - Targeted processes are protected,
#     minimum - Modification of targeted policy. Only selected processes are protected.
#     mls - Multi Level Security protection.
SELINUXTYPE=targeted

[root@ip-172-31-32-222 ~]# getenforce
Enforcing
```

Disable selinux:

```
[root@ip-172-31-32-222 ~]# vi /etc/sysconfig/selinux

[root@ip-172-31-32-222 ~]# cat /etc/sysconfig/selinux

# This file controls the state of SELinux on the system.
# SELINUX= can take one of these three values:
#     enforcing - SELinux security policy is enforced.
#     permissive - SELinux prints warnings instead of enforcing.
#     disabled - No SELinux policy is loaded.
SELINUX=disabled
# SELINUXTYPE= can take one of three two values:
#     targeted - Targeted processes are protected,
#     minimum - Modification of targeted policy. Only selected processes are protected.
#     mls - Multi Level Security protection.
SELINUXTYPE=targeted
```

Reboot server and confirm selinux disabled:

```
[root@ip-172-31-32-222 ~]# reboot

[root@ip-172-31-32-222 ~]# getenforce
Disabled
```


## Confirm no iptables or firewalls running on servers:

```
[root@ip-172-31-32-222 ~]# systemctl status iptables
Unit iptables.service could not be found.

[root@ip-172-31-32-222 ~]# systemctl status firewalld
Unit firewalld.service could not be found.
```

## Disable IPv6

```
[root@ip-172-31-32-222 ~]# echo "net.ipv6.conf.all.disable_ipv6 = 1" >> /etc/sysctl.conf
[root@ip-172-31-32-222 ~]# echo "net.ipv6.conf.default.disable_ipv6 = 1" >> /etc/sysctl.conf

[root@ip-172-31-32-222 ~]# cat /etc/sysctl.conf
# sysctl settings are defined through files in
# /usr/lib/sysctl.d/, /run/sysctl.d/, and /etc/sysctl.d/.
#
# Vendors settings live in /usr/lib/sysctl.d/.
# To override a whole file, create a new file with the same in
# /etc/sysctl.d/ and put new settings there. To override
# only specific settings, add a file with a lexically later
# name in /etc/sysctl.d/ and put new settings there.
#
# For more information, see sysctl.conf(5) and sysctl.d(5).
vm.swappiness = 1
net.ipv6.conf.all.disable_ipv6 = 1
net.ipv6.conf.default.disable_ipv6 = 1
[root@ip-172-31-32-222 ~]# sysctl -p
vm.swappiness = 1
net.ipv6.conf.all.disable_ipv6 = 1
net.ipv6.conf.default.disable_ipv6 = 1
```
