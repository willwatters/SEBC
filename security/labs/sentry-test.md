# Sentry Tutorial

## Verify user privileges

```
[centos@ip-172-31-47-1 ~]$ sudo su - willwatters

[willwatters@ip-172-31-47-1 ~]$ kinit willwatters/admin
Password for willwatters/admin@PUNEETHA.COM:

[willwatters@ip-172-31-47-1 ~]$ beeline
Beeline version 1.1.0-cdh5.13.3 by Apache Hive
beeline> !connect jdbc:hive2://localhost:10000/default;principal=hive/ip-172-31-47-1.eu-west-3.compute.internal@PUNEETHA.COM
scan complete in 1ms
Connecting to jdbc:hive2://localhost:10000/default;principal=hive/ip-172-31-47-1.eu-west-3.compute.internal@PUNEETHA.COM
Connected to: Apache Hive (version 1.1.0-cdh5.13.3)
Driver: Hive JDBC (version 1.1.0-cdh5.13.3)
Transaction isolation: TRANSACTION_REPEATABLE_READ
0: jdbc:hive2://localhost:10000/default> SHOW TABLES;
INFO  : Compiling command(queryId=hive_20181018110808_39e5b3cc-e145-4d3c-a61e-c4001b8aa3c3): SHOW TABLES
INFO  : Semantic Analysis Completed
INFO  : Returning Hive schema: Schema(fieldSchemas:[FieldSchema(name:tab_name, type:string, comment:from deserializer)], properties:null)
INFO  : Completed compiling command(queryId=hive_20181018110808_39e5b3cc-e145-4d3c-a61e-c4001b8aa3c3); Time taken: 0.56 seconds
INFO  : Executing command(queryId=hive_20181018110808_39e5b3cc-e145-4d3c-a61e-c4001b8aa3c3): SHOW TABLES
INFO  : Starting task [Stage-0:DDL] in serial mode
INFO  : Completed executing command(queryId=hive_20181018110808_39e5b3cc-e145-4d3c-a61e-c4001b8aa3c3); Time taken: 0.345 seconds
INFO  : OK
+-----------+--+
| tab_name  |
+-----------+--+
+-----------+--+
No rows selected (2.182 seconds)
0: jdbc:hive2://localhost:10000/default>
```


## Create a Sentry role with full authorization
In beeline:
CREATE ROLE sentry_admin;
GRANT ALL ON SERVER server1 TO ROLE sentry_admin;
GRANT ROLE sentry_admin TO GROUP {your_primary};
SHOW TABLES;
The statement should now return all tables

```
0: jdbc:hive2://localhost:10000/default> CREATE ROLE sentry_admin;
INFO  : Compiling command(queryId=hive_20181018114646_e70fe2bc-ffe0-4c97-90da-4414c6efe85c): CREATE ROLE sentry_admin
INFO  : Semantic Analysis Completed
INFO  : Returning Hive schema: Schema(fieldSchemas:null, properties:null)
INFO  : Completed compiling command(queryId=hive_20181018114646_e70fe2bc-ffe0-4c97-90da-4414c6efe85c); Time taken: 0.062 seconds
INFO  : Executing command(queryId=hive_20181018114646_e70fe2bc-ffe0-4c97-90da-4414c6efe85c): CREATE ROLE sentry_admin
INFO  : Starting task [Stage-0:DDL] in serial mode
INFO  : Completed executing command(queryId=hive_20181018114646_e70fe2bc-ffe0-4c97-90da-4414c6efe85c); Time taken: 0.096 seconds
INFO  : OK
No rows affected (0.17 seconds)
0: jdbc:hive2://localhost:10000/default> GRANT ALL ON SERVER server1 TO ROLE sentry_admin;
INFO  : Compiling command(queryId=hive_20181018114747_d5f81b13-c95b-45c0-bf73-f2c1adeb7142): GRANT ALL ON SERVER server1 TO ROLE sentry_admin
INFO  : Semantic Analysis Completed
INFO  : Returning Hive schema: Schema(fieldSchemas:null, properties:null)
INFO  : Completed compiling command(queryId=hive_20181018114747_d5f81b13-c95b-45c0-bf73-f2c1adeb7142); Time taken: 0.07 seconds
INFO  : Executing command(queryId=hive_20181018114747_d5f81b13-c95b-45c0-bf73-f2c1adeb7142): GRANT ALL ON SERVER server1 TO ROLE sentry_admin
INFO  : Starting task [Stage-0:DDL] in serial mode
INFO  : Completed executing command(queryId=hive_20181018114747_d5f81b13-c95b-45c0-bf73-f2c1adeb7142); Time taken: 0.06 seconds
INFO  : OK
No rows affected (0.14 seconds)
0: jdbc:hive2://localhost:10000/default> grant role sentry_admin to group willwatters;
INFO  : Compiling command(queryId=hive_20181018124646_bc5a8481-cb07-4f9b-8947-ce2e4e354434): grant role sentry_admin to group willwatters
INFO  : Semantic Analysis Completed
INFO  : Returning Hive schema: Schema(fieldSchemas:null, properties:null)
INFO  : Completed compiling command(queryId=hive_20181018124646_bc5a8481-cb07-4f9b-8947-ce2e4e354434); Time taken: 0.075 seconds
INFO  : Executing command(queryId=hive_20181018124646_bc5a8481-cb07-4f9b-8947-ce2e4e354434): grant role sentry_admin to group willwatters
INFO  : Starting task [Stage-0:DDL] in serial mode
INFO  : Completed executing command(queryId=hive_20181018124646_bc5a8481-cb07-4f9b-8947-ce2e4e354434); Time taken: 0.047 seconds
INFO  : OK
No rows affected (0.172 seconds)
0: jdbc:hive2://localhost:10000/default> show tables;
INFO  : Compiling command(queryId=hive_20181018133737_0d604844-bc10-4448-b17a-a8436a3aabd9): show tables
INFO  : Semantic Analysis Completed
INFO  : Returning Hive schema: Schema(fieldSchemas:[FieldSchema(name:tab_name, type:string, comment:from deserializer)], properties:null)
INFO  : Completed compiling command(queryId=hive_20181018133737_0d604844-bc10-4448-b17a-a8436a3aabd9); Time taken: 0.061 seconds
INFO  : Executing command(queryId=hive_20181018133737_0d604844-bc10-4448-b17a-a8436a3aabd9): show tables
INFO  : Starting task [Stage-0:DDL] in serial mode
INFO  : Completed executing command(queryId=hive_20181018133737_0d604844-bc10-4448-b17a-a8436a3aabd9); Time taken: 0.089 seconds
INFO  : OK
+------------+--+
|  tab_name  |
+------------+--+
| customers  |
| sample_07  |
| sample_08  |
| web_logs   |
+------------+--+
4 rows selected (0.163 seconds)
```


## Create additional test users
Add new users to all cluster nodes
$ sudo groupadd selector
$ sudo groupadd inserters
$ sudo useradd -u 1100 -g selector george
$ sudo useradd -u 1200 -g inserters ferdinand
$ kadmin.local: add_principal george
$ kadmin.local: add_principal ferdinand

This was done on all cluster hosts.  See below for one of the hosts:

```
[root@ip-172-31-47-1 ~]# sudo groupadd selector
[root@ip-172-31-47-1 ~]# sudo groupadd inserters
[root@ip-172-31-47-1 ~]# sudo useradd -u 1100 -g selector george
[root@ip-172-31-47-1 ~]# sudo useradd -u 1200 -g inserters ferdinand
```

This was done on the KRB5 server:

```
[root@ip-172-31-32-222 etc]# kadmin.local
Authenticating as principal willwatters/admin@PUNEETHA.COM with password.
kadmin.local:  add_principal george
WARNING: no policy specified for george@PUNEETHA.COM; defaulting to no policy
Enter password for principal "george@PUNEETHA.COM":
Re-enter password for principal "george@PUNEETHA.COM":
Principal "george@PUNEETHA.COM" created.
kadmin.local:  add_principal ferdinand
WARNING: no policy specified for ferdinand@PUNEETHA.COM; defaulting to no policy
Enter password for principal "ferdinand@PUNEETHA.COM":
Re-enter password for principal "ferdinand@PUNEETHA.COM":
Principal "ferdinand@PUNEETHA.COM" created.
kadmin.local:  exit
```


## Create test roles
Login to beeline as your admin user
CREATE ROLE reads;
CREATE ROLE writes;

```
0: jdbc:hive2://localhost:10000/default> CREATE ROLE reads;
INFO  : Compiling command(queryId=hive_20181018135050_e55f0186-822b-4a94-b8d9-2b1a29236bc4): CREATE ROLE reads
INFO  : Semantic Analysis Completed
INFO  : Returning Hive schema: Schema(fieldSchemas:null, properties:null)
INFO  : Completed compiling command(queryId=hive_20181018135050_e55f0186-822b-4a94-b8d9-2b1a29236bc4); Time taken: 0.056 seconds
INFO  : Executing command(queryId=hive_20181018135050_e55f0186-822b-4a94-b8d9-2b1a29236bc4): CREATE ROLE reads
INFO  : Starting task [Stage-0:DDL] in serial mode
INFO  : Completed executing command(queryId=hive_20181018135050_e55f0186-822b-4a94-b8d9-2b1a29236bc4); Time taken: 0.062 seconds
INFO  : OK
No rows affected (0.126 seconds)
0: jdbc:hive2://localhost:10000/default> CREATE ROLE writes;
INFO  : Compiling command(queryId=hive_20181018135050_825c840b-ec3b-445f-a316-ea4b6108696c): CREATE ROLE writes
INFO  : Semantic Analysis Completed
INFO  : Returning Hive schema: Schema(fieldSchemas:null, properties:null)
INFO  : Completed compiling command(queryId=hive_20181018135050_825c840b-ec3b-445f-a316-ea4b6108696c); Time taken: 0.054 seconds
INFO  : Executing command(queryId=hive_20181018135050_825c840b-ec3b-445f-a316-ea4b6108696c): CREATE ROLE writes
INFO  : Starting task [Stage-0:DDL] in serial mode
INFO  : Completed executing command(queryId=hive_20181018135050_825c840b-ec3b-445f-a316-ea4b6108696c); Time taken: 0.007 seconds
INFO  : OK
No rows affected (0.069 seconds)
```

## Grant read privilege for all tables to reads
GRANT SELECT ON DATABASE default TO ROLE reads;
GRANT ROLE reads TO GROUP selector;

```
0: jdbc:hive2://localhost:10000/default> GRANT SELECT ON DATABASE default TO ROLE reads;
INFO  : Compiling command(queryId=hive_20181018135151_fcab843a-cbae-4d70-ad0d-501c6ff710df): GRANT SELECT ON DATABASE default TO ROLE reads
INFO  : Semantic Analysis Completed
INFO  : Returning Hive schema: Schema(fieldSchemas:null, properties:null)
INFO  : Completed compiling command(queryId=hive_20181018135151_fcab843a-cbae-4d70-ad0d-501c6ff710df); Time taken: 0.057 seconds
INFO  : Executing command(queryId=hive_20181018135151_fcab843a-cbae-4d70-ad0d-501c6ff710df): GRANT SELECT ON DATABASE default TO ROLE reads
INFO  : Starting task [Stage-0:DDL] in serial mode
INFO  : Completed executing command(queryId=hive_20181018135151_fcab843a-cbae-4d70-ad0d-501c6ff710df); Time taken: 0.046 seconds
INFO  : OK
No rows affected (0.111 seconds)
0: jdbc:hive2://localhost:10000/default> GRANT ROLE reads TO GROUP selector;
INFO  : Compiling command(queryId=hive_20181018135151_816742c8-098d-4c61-a51b-a94266527486): GRANT ROLE reads TO GROUP selector
INFO  : Semantic Analysis Completed
INFO  : Returning Hive schema: Schema(fieldSchemas:null, properties:null)
INFO  : Completed compiling command(queryId=hive_20181018135151_816742c8-098d-4c61-a51b-a94266527486); Time taken: 0.056 seconds
INFO  : Executing command(queryId=hive_20181018135151_816742c8-098d-4c61-a51b-a94266527486): GRANT ROLE reads TO GROUP selector
INFO  : Starting task [Stage-0:DDL] in serial mode
INFO  : Completed executing command(queryId=hive_20181018135151_816742c8-098d-4c61-a51b-a94266527486); Time taken: 0.038 seconds
INFO  : OK
No rows affected (0.101 seconds)
```

## Grant read privilege for default.sample07 only to 'writes':
REVOKE ALL ON DATABASE default FROM ROLE writes;
GRANT SELECT ON default.sample_07 TO ROLE writes;
GRANT ROLE writes TO GROUP inserters;

```
0: jdbc:hive2://localhost:10000/default> REVOKE ALL ON DATABASE default FROM ROLE writes;
INFO  : Compiling command(queryId=hive_20181018135252_c0f1eed4-9213-4e52-bbf2-550063362f34): REVOKE ALL ON DATABASE default FROM ROLE writes
INFO  : Semantic Analysis Completed
INFO  : Returning Hive schema: Schema(fieldSchemas:null, properties:null)
INFO  : Completed compiling command(queryId=hive_20181018135252_c0f1eed4-9213-4e52-bbf2-550063362f34); Time taken: 0.054 seconds
INFO  : Executing command(queryId=hive_20181018135252_c0f1eed4-9213-4e52-bbf2-550063362f34): REVOKE ALL ON DATABASE default FROM ROLE writes
INFO  : Starting task [Stage-0:DDL] in serial mode
INFO  : Completed executing command(queryId=hive_20181018135252_c0f1eed4-9213-4e52-bbf2-550063362f34); Time taken: 0.036 seconds
INFO  : OK
No rows affected (0.099 seconds)
0: jdbc:hive2://localhost:10000/default> GRANT SELECT ON default.sample_07 TO ROLE writes;
INFO  : Compiling command(queryId=hive_20181018135252_ed5f9645-fce3-4114-84f9-886d64b537da): GRANT SELECT ON default.sample_07 TO ROLE writes
INFO  : Semantic Analysis Completed
INFO  : Returning Hive schema: Schema(fieldSchemas:null, properties:null)
INFO  : Completed compiling command(queryId=hive_20181018135252_ed5f9645-fce3-4114-84f9-886d64b537da); Time taken: 0.053 seconds
INFO  : Executing command(queryId=hive_20181018135252_ed5f9645-fce3-4114-84f9-886d64b537da): GRANT SELECT ON default.sample_07 TO ROLE writes
INFO  : Starting task [Stage-0:DDL] in serial mode
INFO  : Completed executing command(queryId=hive_20181018135252_ed5f9645-fce3-4114-84f9-886d64b537da); Time taken: 0.009 seconds
INFO  : OK
No rows affected (0.07 seconds)
0: jdbc:hive2://localhost:10000/default> GRANT ROLE writes TO GROUP inserters;
INFO  : Compiling command(queryId=hive_20181018135252_3734528a-8865-40f3-a8ac-92a158207f29): GRANT ROLE writes TO GROUP inserters
INFO  : Semantic Analysis Completed
INFO  : Returning Hive schema: Schema(fieldSchemas:null, properties:null)
INFO  : Completed compiling command(queryId=hive_20181018135252_3734528a-8865-40f3-a8ac-92a158207f29); Time taken: 0.053 seconds
INFO  : Executing command(queryId=hive_20181018135252_3734528a-8865-40f3-a8ac-92a158207f29): GRANT ROLE writes TO GROUP inserters
INFO  : Starting task [Stage-0:DDL] in serial mode
INFO  : Completed executing command(queryId=hive_20181018135252_3734528a-8865-40f3-a8ac-92a158207f29); Time taken: 0.009 seconds
INFO  : OK
No rows affected (0.079 seconds)
```

## kinit as george, then login to beeline
kinit as george, login to beeline, and use SHOW TABLES;
george should be able to see all tables
Repeat the process as ferdinand
ferdinand should see sample_07

```
[root@ip-172-31-47-1 ~]# sudo su - george
[george@ip-172-31-47-1 ~]$ kinit george
Password for george@PUNEETHA.COM:
[george@ip-172-31-47-1 ~]$ beeline
Beeline version 1.1.0-cdh5.13.3 by Apache Hive
beeline> !connect jdbc:hive2://localhost:10000/default;principal=hive/ip-172-31-47-1.eu-west-3.compute.internal@PUNEETHA.COM
scan complete in 1ms
Connecting to jdbc:hive2://localhost:10000/default;principal=hive/ip-172-31-47-1.eu-west-3.compute.internal@PUNEETHA.COM
Connected to: Apache Hive (version 1.1.0-cdh5.13.3)
Driver: Hive JDBC (version 1.1.0-cdh5.13.3)
Transaction isolation: TRANSACTION_REPEATABLE_READ
0: jdbc:hive2://localhost:10000/default> show tables;
INFO  : Compiling command(queryId=hive_20181018135454_203d9045-2481-4d7c-8c13-4738868adcce): show tables
INFO  : Semantic Analysis Completed
INFO  : Returning Hive schema: Schema(fieldSchemas:[FieldSchema(name:tab_name, type:string, comment:from deserializer)], properties:null)
INFO  : Completed compiling command(queryId=hive_20181018135454_203d9045-2481-4d7c-8c13-4738868adcce); Time taken: 0.082 seconds
INFO  : Executing command(queryId=hive_20181018135454_203d9045-2481-4d7c-8c13-4738868adcce): show tables
INFO  : Starting task [Stage-0:DDL] in serial mode
INFO  : Completed executing command(queryId=hive_20181018135454_203d9045-2481-4d7c-8c13-4738868adcce); Time taken: 0.103 seconds
INFO  : OK
+------------+--+
|  tab_name  |
+------------+--+
| customers  |
| sample_07  |
| sample_08  |
| web_logs   |
+------------+--+
4 rows selected (0.255 seconds)
0: jdbc:hive2://localhost:10000/default> !quit
Closing: 0: jdbc:hive2://localhost:10000/default;principal=hive/ip-172-31-47-1.eu-west-3.compute.internal@PUNEETHA.COM
[george@ip-172-31-47-1 ~]$ exit
logout

[root@ip-172-31-47-1 ~]# sudo su - ferdinand
[ferdinand@ip-172-31-47-1 ~]$ kinit ferdinand
Password for ferdinand@PUNEETHA.COM:
[ferdinand@ip-172-31-47-1 ~]$ beeline
Beeline version 1.1.0-cdh5.13.3 by Apache Hive
beeline> !connect jdbc:hive2://localhost:10000/default;principal=hive/ip-172-31-47-1.eu-west-3.compute.internal@PUNEETHA.COM
scan complete in 1ms
Connecting to jdbc:hive2://localhost:10000/default;principal=hive/ip-172-31-47-1.eu-west-3.compute.internal@PUNEETHA.COM
Connected to: Apache Hive (version 1.1.0-cdh5.13.3)
Driver: Hive JDBC (version 1.1.0-cdh5.13.3)
Transaction isolation: TRANSACTION_REPEATABLE_READ
0: jdbc:hive2://localhost:10000/default> show tables;
INFO  : Compiling command(queryId=hive_20181018135656_4bb046d8-6269-4498-8b59-a45093fa0595): show tables
INFO  : Semantic Analysis Completed
INFO  : Returning Hive schema: Schema(fieldSchemas:[FieldSchema(name:tab_name, type:string, comment:from deserializer)], properties:null)
INFO  : Completed compiling command(queryId=hive_20181018135656_4bb046d8-6269-4498-8b59-a45093fa0595); Time taken: 0.061 seconds
INFO  : Executing command(queryId=hive_20181018135656_4bb046d8-6269-4498-8b59-a45093fa0595): show tables
INFO  : Starting task [Stage-0:DDL] in serial mode
INFO  : Completed executing command(queryId=hive_20181018135656_4bb046d8-6269-4498-8b59-a45093fa0595); Time taken: 0.105 seconds
INFO  : OK
+------------+--+
|  tab_name  |
+------------+--+
| sample_07  |
+------------+--+
1 row selected (0.237 seconds)
0: jdbc:hive2://localhost:10000/default>
```
