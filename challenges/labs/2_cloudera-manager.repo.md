Copy the cloudera-manager.repo file to challenges/labs/2_cloudera-manager.repo.md:

```
[root@ip-172-31-47-28 yum.repos.d]# wget https://archive.cloudera.com/cm5/redhat/7/x86_64/cm/cloudera-manager.repo
--2018-10-19 08:13:58--  https://archive.cloudera.com/cm5/redhat/7/x86_64/cm/cloudera-manager.repo
Resolving archive.cloudera.com (archive.cloudera.com)... 151.101.60.167
Connecting to archive.cloudera.com (archive.cloudera.com)|151.101.60.167|:443... connected.
HTTP request sent, awaiting response... 200 OK
Length: 290 [binary/octet-stream]
Saving to: ‘cloudera-manager.repo’

100%[==================================================================================================================================================================>] 290         --.-K/s   in 0s

2018-10-19 08:13:59 (68.6 MB/s) - ‘cloudera-manager.repo’ saved [290/290]

[root@ip-172-31-47-28 yum.repos.d]# ls -lrt
total 36
-rw-r--r--. 1 root root 4768 May 17 13:53 CentOS-Vault.repo
-rw-r--r--. 1 root root 1331 May 17 13:53 CentOS-Sources.repo
-rw-r--r--. 1 root root  630 May 17 13:53 CentOS-Media.repo
-rw-r--r--. 1 root root  314 May 17 13:53 CentOS-fasttrack.repo
-rw-r--r--. 1 root root  649 May 17 13:53 CentOS-Debuginfo.repo
-rw-r--r--. 1 root root 1309 May 17 13:53 CentOS-CR.repo
-rw-r--r--. 1 root root 1664 May 17 13:53 CentOS-Base.repo
-rw-r--r--  1 root root  290 Aug 22 15:00 cloudera-manager.repo

[root@ip-172-31-47-28 yum.repos.d]# vi cloudera-manager.repo
[root@ip-172-31-47-28 yum.repos.d]# cat cloudera-manager.repo
[cloudera-manager]
# Packages for Cloudera Manager, Version 5, on RedHat or CentOS 7 x86_64
name=Cloudera Manager
#baseurl=https://archive.cloudera.com/cm5/redhat/7/x86_64/cm/5/
baseurl=https://archive.cloudera.com/cm5/redhat/7/x86_64/cm/5.14.4/
gpgkey =https://archive.cloudera.com/cm5/redhat/7/x86_64/cm/RPM-GPG-KEY-cloudera
gpgcheck = 1
```
