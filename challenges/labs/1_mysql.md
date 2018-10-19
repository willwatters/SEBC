Challenge 1: Install a MySQL or MariaDB server


Install a compatible MySQL or MariaDB server on the node you listed first
On all cluster nodes
Install the MySQL client package and JDBC connector jar
Create the following databases
scm
rman
hive
oozie
hue
sentry
Put the following in the file challenges/labs/1_mysql.md

The hostname of your DB node:

```
[root@ip-172-31-33-13 tmp]# hostname --fqdn
ip-172-31-33-13.eu-west-3.compute.internal
```

The command screenshot to display the DB version:

```
[root@ip-172-31-33-13 tmp]# mysql --version
mysql  Ver 15.1 Distrib 5.5.60-MariaDB, for Linux (x86_64) using readline 5.1
[root@ip-172-31-33-13 tmp]#
```


The command and output for listing databases:
```
MariaDB [(none)]> show tables;
ERROR 1046 (3D000): No database selected
MariaDB [(none)]> show databases;
+--------------------+
| Database           |
+--------------------+
| information_schema |
| hue                |
| metastore          |
| mysql              |
| oozie              |
| performance_schema |
| rman               |
| scm                |
| sentry             |
+--------------------+
9 rows in set (0.00 sec)
```


Push this work to your GitHub repo
Label the Issue 'submitted` and assign it to the instructors

