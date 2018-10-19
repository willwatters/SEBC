Challenge 3 - Install CDH

Create the Issue Install CDH
Assign the issue to yourself and label it started
Install the latest CDH release; deploy Coreset services only
Rename your cluster after your GitHub handle
Create user directories in HDFS for raffles and fullerton:

```
[root@ip-172-31-41-38 mysql-connector-java-5.1.46]# su hdfs
[hdfs@ip-172-31-41-38 mysql-connector-java-5.1.46]$ hdfs dfs -ls /
Found 2 items
drwxrwxrwt   - hdfs supergroup          0 2018-10-19 09:35 /tmp
drwxr-xr-x   - hdfs supergroup          0 2018-10-19 09:35 /user
[hdfs@ip-172-31-41-38 mysql-connector-java-5.1.46]$ hdfs dfs -mkdir /user/raffles
[hdfs@ip-172-31-41-38 mysql-connector-java-5.1.46]$ hdfs dfs -mkdir /user/fullerton
[hdfs@ip-172-31-41-38 mysql-connector-java-5.1.46]$ hdfs dfs -chown raffles /user/raffles
[hdfs@ip-172-31-41-38 mysql-connector-java-5.1.46]$ hdfs dfs -chown fullerton /user/fullerton
[hdfs@ip-172-31-41-38 mysql-connector-java-5.1.46]$ hdfs dfs -ls /user

Found 6 items
drwxr-xr-x   - fullerton supergroup          0 2018-10-19 09:37 /user/fullerton
drwxrwxrwx   - mapred    hadoop              0 2018-10-19 09:34 /user/history
drwxrwxr-t   - hive      hive                0 2018-10-19 09:34 /user/hive
drwxrwxr-x   - hue       hue                 0 2018-10-19 09:35 /user/hue
drwxrwxr-x   - oozie     oozie               0 2018-10-19 09:35 /user/oozie
drwxr-xr-x   - raffles   supergroup          0 2018-10-19 09:37 /user/raffles
```

Add the following to 3_cm.md:
Command and output for hdfs dfs -ls /user
The output from the CM API call ../api/v14/hosts

```
[root@ip-172-31-47-28 cloudera-scm-server]# curl -u admin:admin 'http://localhost:7180/api/v14/hosts'
{
  "items" : [ {
    "hostId" : "fc1151df-f00b-4d58-9e56-a048022e2481",
    "ipAddress" : "172.31.33.13",
    "hostname" : "ip-172-31-33-13.eu-west-3.compute.internal",
    "rackId" : "/default",
    "hostUrl" : "http://ip-172-31-47-28.eu-west-3.compute.internal:7180/cmf/hostRedirect/fc1151df-f00b-4d58-9e56-a048022e2481",
    "maintenanceMode" : false,
    "maintenanceOwners" : [ ],
    "commissionState" : "COMMISSIONED",
    "numCores" : 4,
    "numPhysicalCores" : 2,
    "totalPhysMemBytes" : 16170954752
  }, {
    "hostId" : "bdae2d3f-591b-48a4-a591-90b1dc425ee8",
    "ipAddress" : "172.31.41.38",
    "hostname" : "ip-172-31-41-38.eu-west-3.compute.internal",
    "rackId" : "/default",
    "hostUrl" : "http://ip-172-31-47-28.eu-west-3.compute.internal:7180/cmf/hostRedirect/bdae2d3f-591b-48a4-a591-90b1dc425ee8",
    "maintenanceMode" : false,
    "maintenanceOwners" : [ ],
    "commissionState" : "COMMISSIONED",
    "numCores" : 4,
    "numPhysicalCores" : 2,
    "totalPhysMemBytes" : 16170954752
  }, {
    "hostId" : "22c7e83f-5fca-4c52-bb47-ec5c3af2b572",
    "ipAddress" : "172.31.46.53",
    "hostname" : "ip-172-31-46-53.eu-west-3.compute.internal",
    "rackId" : "/default",
    "hostUrl" : "http://ip-172-31-47-28.eu-west-3.compute.internal:7180/cmf/hostRedirect/22c7e83f-5fca-4c52-bb47-ec5c3af2b572",
    "maintenanceMode" : false,
    "maintenanceOwners" : [ ],
    "commissionState" : "COMMISSIONED",
    "numCores" : 4,
    "numPhysicalCores" : 2,
    "totalPhysMemBytes" : 16170954752
  }, {
    "hostId" : "7f2c817c-06a8-4c44-9e41-fe4849d084de",
    "ipAddress" : "172.31.47.28",
    "hostname" : "ip-172-31-47-28.eu-west-3.compute.internal",
    "rackId" : "/default",
    "hostUrl" : "http://ip-172-31-47-28.eu-west-3.compute.internal:7180/cmf/hostRedirect/7f2c817c-06a8-4c44-9e41-fe4849d084de",
    "maintenanceMode" : false,
    "maintenanceOwners" : [ ],
    "commissionState" : "COMMISSIONED",
    "numCores" : 4,
    "numPhysicalCores" : 2,
    "totalPhysMemBytes" : 16170954752
  }, {
    "hostId" : "e65784d3-4c28-4d14-ab32-58520452567d",
    "ipAddress" : "172.31.47.96",
    "hostname" : "ip-172-31-47-96.eu-west-3.compute.internal",
    "rackId" : "/default",
    "hostUrl" : "http://ip-172-31-47-28.eu-west-3.compute.internal:7180/cmf/hostRedirect/e65784d3-4c28-4d14-ab32-58520452567d",
    "maintenanceMode" : false,
    "maintenanceOwners" : [ ],
    "commissionState" : "COMMISSIONED",
    "numCores" : 4,
    "numPhysicalCores" : 2,
    "totalPhysMemBytes" : 16170954752
  } ]
}[root@ip-172-31-47-28 cloudera-scm-server]#
```
