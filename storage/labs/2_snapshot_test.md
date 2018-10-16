# Test HDFS Snapshots

## Create a precious directory in HDFS; copy the ZIP course file into it.

Create directory called precious:

```
[centos@ip-172-31-39-85 ~]$ sudo su hdfs
[hdfs@ip-172-31-39-85 centos]$ hdfs dfs -mkdir /precious
[hdfs@ip-172-31-39-85 centos]$ hdfs dfs -ls /
Found 5 items
drwxr-xr-x   - hdfs supergroup          0 2018-10-16 17:03 /precious
drwxr-xr-x   - hdfs supergroup          0 2018-10-16 14:20 /ronniet7626
drwxrwxrwt   - hdfs supergroup          0 2018-10-16 13:55 /tmp
drwxr-xr-x   - hdfs supergroup          0 2018-10-16 15:09 /user
drwxr-xr-x   - hdfs supergroup          0 2018-10-16 14:50 /willwatters
```

On local server copy the local copy to /tmp director on one of the DataNodes:

```
➜  SEBootCamp git:(master) ✗ scp -i /Users/williamw/Documents/Training/SEBootCamp/SEBC-Key2.pem SEBC-master.zip centos@ec2-52-47-175-88.eu-west-3.compute.amazonaws.com:/tmp
SEBC-master.zip
```

Copy the Zip course file into the precious directory:

```
[hdfs@ip-172-31-39-85 centos]$ cd /tmp

[hdfs@ip-172-31-39-85 tmp]$ hdfs dfs -put SEBC-master.zip /precious
[hdfs@ip-172-31-39-85 tmp]$ hdfs dfs -ls /precious
Found 1 items
-rw-r--r--   3 hdfs supergroup    1720611 2018-10-16 17:14 /precious/SEBC-master.zip
```


## Enable snapshots for precious

Enable the snapshot for precious from Cloudera Manager HDFS File Browser UI:

```
HDFS > File Browser > select 'precious' > select top right arrow and click "Enable Snapshot"
```

## Create a snapshot called sebc-hdfs-test

Take snapshot from Cloudera Manager HDFS File Browser UI:

```
HDFS > File Browser > select 'precious' > select top right arrow and click "Take Snapshot" > enter the name as "sebc-hdfs-test"
```

## Delete the directory

Unable to delete the 'precious' directory as a snapshottable folder cannot be deleted:

```
[hdfs@ip-172-31-39-85 tmp]$ hdfs dfs -rm -r /precious
rm: Failed to move to trash: hdfs://ip-172-31-38-0.eu-west-3.compute.internal:8020/precious: The directory /precious cannot be deleted since /precious is snapshottable and already has snapshots
```

## Delete the zip file

```
[hdfs@ip-172-31-39-85 tmp]$ hdfs dfs -rm -r /precious/SEBC-master.zip
18/10/16 17:20:28 INFO fs.TrashPolicyDefault: Moved: 'hdfs://ip-172-31-38-0.eu-west-3.compute.internal:8020/precious/SEBC-master.zip' to trash at: hdfs://ip-172-31-38-0.eu-west-3.compute.internal:8020/user/hdfs/.Trash/Current/precious/SEBC-master.zip

[hdfs@ip-172-31-39-85 tmp]$ hdfs dfs -ls /precious
```

## Restore the deleted file

Restore the snapshot from Cloudera Manager HDFS File Browser UI:

```
HDFS > File Browser > select 'precious' > select top right arrow and click "Restore Directory From Snapshot" > select the "sebc-hdfs-test" snapshot > selected "HDFS copy" option for the restore > click "restore"
```

Verify that the file has been correctly restored:

```
[hdfs@ip-172-31-39-85 tmp]$ hdfs dfs -ls /precious
Found 1 items
-rw-r--r--   3 hdfs supergroup    1720611 2018-10-16 17:23 /precious/SEBC-master.zip
```
