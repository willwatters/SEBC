Challenge 2: Install Cloudera Manager

Create the Issue Install CM
Assign yourself to the Issue and label it started
Install Cloudera Manager on a different node from MySQL or MariaDB
Configure the CM repo to install the latest release

List the command and output of ls /etc/yum.repos.d in challenges/labs/2_cm.md:

Before:
```
[root@ip-172-31-47-28 yum.repos.d]# ls -l
total 32
-rw-r--r--. 1 root root 1664 May 17 13:53 CentOS-Base.repo
-rw-r--r--. 1 root root 1309 May 17 13:53 CentOS-CR.repo
-rw-r--r--. 1 root root  649 May 17 13:53 CentOS-Debuginfo.repo
-rw-r--r--. 1 root root  314 May 17 13:53 CentOS-fasttrack.repo
-rw-r--r--. 1 root root  630 May 17 13:53 CentOS-Media.repo
-rw-r--r--. 1 root root 1331 May 17 13:53 CentOS-Sources.repo

```

After:

```
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
```


Configure Cloudera Manager
Use the scm_prepare_database.sh script to write your db.properties file
List the full command line in 2_cm.md

```
[root@ip-172-31-47-28 yum.repos.d]# /usr/share/cmf/schema/scm_prepare_database.sh mysql -h ip-172-31-33-13.eu-west-3.compute.internal -utemp -ppassword1 --scm-host ip-172-31-47-28.eu-west-3.compute.internal scm scm password1 --force
JAVA_HOME=/usr/java/jdk1.7.0_67-cloudera
Verifying that we can write to /etc/cloudera-scm-server
[                          main] DbProvisioner                  ERROR Exception when creating/dropping database with user 'temp' and jdbc url 'jdbc:mysql://ip-172-31-33-13.eu-west-3.compute.internal/?useUnicode=true&characterEncoding=UTF-8'
java.sql.SQLException: Can't create database 'scm'; database exists
  at com.mysql.jdbc.SQLError.createSQLException(SQLError.java:965)[mysql-connector-java.jar:5.1.46]
  at com.mysql.jdbc.MysqlIO.checkErrorPacket(MysqlIO.java:3976)[mysql-connector-java.jar:5.1.46]
  at com.mysql.jdbc.MysqlIO.checkErrorPacket(MysqlIO.java:3912)[mysql-connector-java.jar:5.1.46]
  at com.mysql.jdbc.MysqlIO.sendCommand(MysqlIO.java:2530)[mysql-connector-java.jar:5.1.46]
  at com.mysql.jdbc.MysqlIO.sqlQueryDirect(MysqlIO.java:2683)[mysql-connector-java.jar:5.1.46]
  at com.mysql.jdbc.ConnectionImpl.execSQL(ConnectionImpl.java:2482)[mysql-connector-java.jar:5.1.46]
  at com.mysql.jdbc.ConnectionImpl.execSQL(ConnectionImpl.java:2440)[mysql-connector-java.jar:5.1.46]
  at com.mysql.jdbc.StatementImpl.executeInternal(StatementImpl.java:845)[mysql-connector-java.jar:5.1.46]
  at com.mysql.jdbc.StatementImpl.execute(StatementImpl.java:745)[mysql-connector-java.jar:5.1.46]
  at com.cloudera.enterprise.dbutil.DbProvisioner.executeSql(DbProvisioner.java:299)[db-common-5.14.4.jar:]
  at com.cloudera.enterprise.dbutil.DbProvisioner.doMain(DbProvisioner.java:104)[db-common-5.14.4.jar:]
  at com.cloudera.enterprise.dbutil.DbProvisioner.main(DbProvisioner.java:123)[db-common-5.14.4.jar:]
[                          main] DbProvisioner                  ERROR Stack Trace:
java.sql.SQLException: Can't create database 'scm'; database exists
  at com.mysql.jdbc.SQLError.createSQLException(SQLError.java:965)[mysql-connector-java.jar:5.1.46]
  at com.mysql.jdbc.MysqlIO.checkErrorPacket(MysqlIO.java:3976)[mysql-connector-java.jar:5.1.46]
  at com.mysql.jdbc.MysqlIO.checkErrorPacket(MysqlIO.java:3912)[mysql-connector-java.jar:5.1.46]
  at com.mysql.jdbc.MysqlIO.sendCommand(MysqlIO.java:2530)[mysql-connector-java.jar:5.1.46]
  at com.mysql.jdbc.MysqlIO.sqlQueryDirect(MysqlIO.java:2683)[mysql-connector-java.jar:5.1.46]
  at com.mysql.jdbc.ConnectionImpl.execSQL(ConnectionImpl.java:2482)[mysql-connector-java.jar:5.1.46]
  at com.mysql.jdbc.ConnectionImpl.execSQL(ConnectionImpl.java:2440)[mysql-connector-java.jar:5.1.46]
  at com.mysql.jdbc.StatementImpl.executeInternal(StatementImpl.java:845)[mysql-connector-java.jar:5.1.46]
  at com.mysql.jdbc.StatementImpl.execute(StatementImpl.java:745)[mysql-connector-java.jar:5.1.46]
  at com.cloudera.enterprise.dbutil.DbProvisioner.executeSql(DbProvisioner.java:299)[db-common-5.14.4.jar:]
  at com.cloudera.enterprise.dbutil.DbProvisioner.doMain(DbProvisioner.java:104)[db-common-5.14.4.jar:]
  at com.cloudera.enterprise.dbutil.DbProvisioner.main(DbProvisioner.java:123)[db-common-5.14.4.jar:]
--> Error 1, ignoring (because force flag is set)
Creating SCM configuration file in /etc/cloudera-scm-server
Executing:  /usr/java/jdk1.7.0_67-cloudera/bin/java -cp /usr/share/java/mysql-connector-java.jar:/usr/share/java/oracle-connector-java.jar:/usr/share/cmf/schema/../lib/* com.cloudera.enterprise.dbutil.DbCommandExecutor /etc/cloudera-scm-server/db.properties com.cloudera.cmf.db.
[                          main] DbCommandExecutor              INFO  Successfully connected to database.
All done, your SCM database is configured correctly!


[root@ip-172-31-47-28 etc]# cd cloudera-scm-server
[root@ip-172-31-47-28 cloudera-scm-server]# ls -l
total 12
-rw------- 1 cloudera-scm cloudera-scm  463 Oct 19 08:58 db.properties
-rw------- 1 cloudera-scm cloudera-scm  714 Jul  7 05:20 db.properties.~1~
-rw-r--r-- 1 root         root         2229 Jul  7 05:20 log4j.properties
[root@ip-172-31-47-28 cloudera-scm-server]# cat db.properties
# Auto-generated by scm_prepare_database.sh on Fri Oct 19 08:58:38 UTC 2018
#
# For information describing how to configure the Cloudera Manager Server
# to connect to databases, see the "Cloudera Manager Installation Guide."
#
com.cloudera.cmf.db.type=mysql
com.cloudera.cmf.db.host=ip-172-31-33-13.eu-west-3.compute.internal
com.cloudera.cmf.db.name=scm
com.cloudera.cmf.db.user=scm
com.cloudera.cmf.db.setupType=EXTERNAL
com.cloudera.cmf.db.password=password1
[root@ip-172-31-47-28 cloudera-scm-server]#
```

