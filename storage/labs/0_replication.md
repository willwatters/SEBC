# Replicate to another cluster

## HDFS folder creation with GitHub handle

Create HDFS folders with Github handle (partner & myself):

```
[root@ip-172-31-39-85 ~]# sudo su hdfs
[hdfs@ip-172-31-39-85 root]$ hdfs dfs -mkdir /willwatters
[hdfs@ip-172-31-39-85 root]$ hdfs dfs -mkdir /ronniet7626
[hdfs@ip-172-31-39-85 root]$ hdfs dfs -ls /
Found 4 items
drwxr-xr-x   - hdfs supergroup          0 2018-10-16 14:20 /ronniet7626
drwxrwxrwt   - hdfs supergroup          0 2018-10-16 13:55 /tmp
drwxr-xr-x   - hdfs supergroup          0 2018-10-16 13:55 /user
drwxr-xr-x   - hdfs supergroup          0 2018-10-16 14:19 /willwatters
```


## Use Teragen to create a 500 MB file

I removed /willwatters as the teragen command below will create this folder, when specified:

```
hdfs@ip-172-31-39-85 root]$ hdfs dfs -rmdir /willwatters
[hdfs@ip-172-31-39-85 root]$ hdfs dfs -ls /
Found 4 items
drwxr-xr-x   - hdfs supergroup          0 2018-10-16 14:37 /hadoop
drwxr-xr-x   - hdfs supergroup          0 2018-10-16 14:20 /ronniet7626
drwxrwxrwt   - hdfs supergroup          0 2018-10-16 13:55 /tmp
drwxr-xr-x   - hdfs supergroup          0 2018-10-16 14:42 /user
```


To calcuate 500 MB file - 1024 (KB) x 1024 (MB) x 500 (500 MB) / 100 (Byte) = 5242880

Run the Teragen command to create a 500 MB file:

```
hdfs@ip-172-31-39-85 root]$ hadoop jar /opt/cloudera/parcels/CDH/jars/hadoop-examples.jar teragen 5242880 /willwatters
18/10/16 14:50:09 INFO client.RMProxy: Connecting to ResourceManager at ip-172-31-46-203.eu-west-3.compute.internal/172.31.46.203:8032
18/10/16 14:50:09 INFO terasort.TeraGen: Generating 5242880 using 2
18/10/16 14:50:09 INFO mapreduce.JobSubmitter: number of splits:2
18/10/16 14:50:09 INFO mapreduce.JobSubmitter: Submitting tokens for job: job_1539698111610_0003
18/10/16 14:50:10 INFO impl.YarnClientImpl: Submitted application application_1539698111610_0003
18/10/16 14:50:10 INFO mapreduce.Job: The url to track the job: http://ip-172-31-46-203.eu-west-3.compute.internal:8088/proxy/application_1539698111610_0003/
18/10/16 14:50:10 INFO mapreduce.Job: Running job: job_1539698111610_0003
18/10/16 14:50:15 INFO mapreduce.Job: Job job_1539698111610_0003 running in uber mode : false
18/10/16 14:50:15 INFO mapreduce.Job:  map 0% reduce 0%
18/10/16 14:50:22 INFO mapreduce.Job:  map 50% reduce 0%
18/10/16 14:50:23 INFO mapreduce.Job:  map 100% reduce 0%
18/10/16 14:50:23 INFO mapreduce.Job: Job job_1539698111610_0003 completed successfully
18/10/16 14:50:23 INFO mapreduce.Job: Counters: 31
  File System Counters
    FILE: Number of bytes read=0
    FILE: Number of bytes written=296114
    FILE: Number of read operations=0
    FILE: Number of large read operations=0
    FILE: Number of write operations=0
    HDFS: Number of bytes read=167
    HDFS: Number of bytes written=524288000
    HDFS: Number of read operations=8
    HDFS: Number of large read operations=0
    HDFS: Number of write operations=4
  Job Counters
    Launched map tasks=2
    Other local map tasks=2
    Total time spent by all maps in occupied slots (ms)=10192
    Total time spent by all reduces in occupied slots (ms)=0
    Total time spent by all map tasks (ms)=10192
    Total vcore-milliseconds taken by all map tasks=10192
    Total megabyte-milliseconds taken by all map tasks=10436608
  Map-Reduce Framework
    Map input records=5242880
    Map output records=5242880
    Input split bytes=167
    Spilled Records=0
    Failed Shuffles=0
    Merged Map outputs=0
    GC time elapsed (ms)=128
    CPU time spent (ms)=9340
    Physical memory (bytes) snapshot=749821952
    Virtual memory (bytes) snapshot=3164409856
    Total committed heap usage (bytes)=886046720
  org.apache.hadoop.examples.terasort.TeraGen$Counters
    CHECKSUM=11257830824958050
  File Input Format Counters
    Bytes Read=0
  File Output Format Counters
    Bytes Written=524288000
```

Verify that the file created is 500MB:

```
[hdfs@ip-172-31-39-85 root]$ hdfs dfs -ls /willwatters
Found 3 items
-rw-r--r--   3 hdfs supergroup          0 2018-10-16 14:50 /willwatters/_SUCCESS
-rw-r--r--   3 hdfs supergroup  262144000 2018-10-16 14:50 /willwatters/part-m-00000
-rw-r--r--   3 hdfs supergroup  262144000 2018-10-16 14:50 /willwatters/part-m-00001
```


## Distcp

Unable to replicate the Teragen file produced to my partner's (ronniet7626) cluster due to the datanodes not listening on the public interface.  Therefore we cannot transfer data between two clusters.

Transfer data within the same cluster, using Distcp:

```
[hdfs@ip-172-31-39-85 root]$ hadoop distcp /willwatters /user/willwatters_copy
18/10/16 14:51:10 INFO tools.OptionsParser: parseChunkSize: blocksperchunk false
18/10/16 14:51:11 INFO tools.DistCp: Input Options: DistCpOptions{atomicCommit=false, syncFolder=false, deleteMissing=false, ignoreFailures=false, overwrite=false, append=false, useDiff=false, useRdiff=false, fromSnapshot=null, toSnapshot=null, skipCRC=false, blocking=true, numListstatusThreads=0, maxMaps=20, mapBandwidth=100, sslConfigurationFile='null', copyStrategy='uniformsize', preserveStatus=[], preserveRawXattrs=false, atomicWorkPath=null, logPath=null, sourceFileListing=null, sourcePaths=[/willwatters], targetPath=/user/willwatters_copy, targetPathExists=false, filtersFile='null', blocksPerChunk=0, copyBufferSize=8192}
18/10/16 14:51:11 INFO client.RMProxy: Connecting to ResourceManager at ip-172-31-46-203.eu-west-3.compute.internal/172.31.46.203:8032
18/10/16 14:51:11 INFO tools.SimpleCopyListing: Paths (files+dirs) cnt = 4; dirCnt = 1
18/10/16 14:51:11 INFO tools.SimpleCopyListing: Build file listing completed.
18/10/16 14:51:11 INFO Configuration.deprecation: io.sort.mb is deprecated. Instead, use mapreduce.task.io.sort.mb
18/10/16 14:51:11 INFO Configuration.deprecation: io.sort.factor is deprecated. Instead, use mapreduce.task.io.sort.factor
18/10/16 14:51:12 INFO tools.DistCp: Number of paths in the copy list: 4
18/10/16 14:51:12 INFO tools.DistCp: Number of paths in the copy list: 4
18/10/16 14:51:12 INFO client.RMProxy: Connecting to ResourceManager at ip-172-31-46-203.eu-west-3.compute.internal/172.31.46.203:8032
18/10/16 14:51:12 INFO mapreduce.JobSubmitter: number of splits:4
18/10/16 14:51:12 INFO mapreduce.JobSubmitter: Submitting tokens for job: job_1539698111610_0004
18/10/16 14:51:12 INFO impl.YarnClientImpl: Submitted application application_1539698111610_0004
18/10/16 14:51:12 INFO mapreduce.Job: The url to track the job: http://ip-172-31-46-203.eu-west-3.compute.internal:8088/proxy/application_1539698111610_0004/
18/10/16 14:51:12 INFO tools.DistCp: DistCp job-id: job_1539698111610_0004
18/10/16 14:51:12 INFO mapreduce.Job: Running job: job_1539698111610_0004
18/10/16 14:51:18 INFO mapreduce.Job: Job job_1539698111610_0004 running in uber mode : false
18/10/16 14:51:18 INFO mapreduce.Job:  map 0% reduce 0%
18/10/16 14:51:23 INFO mapreduce.Job:  map 25% reduce 0%
18/10/16 14:51:25 INFO mapreduce.Job:  map 50% reduce 0%
18/10/16 14:51:26 INFO mapreduce.Job:  map 75% reduce 0%
18/10/16 14:51:28 INFO mapreduce.Job:  map 100% reduce 0%
18/10/16 14:51:28 INFO mapreduce.Job: Job job_1539698111610_0004 completed successfully
18/10/16 14:51:28 INFO mapreduce.Job: Counters: 33
  File System Counters
    FILE: Number of bytes read=0
    FILE: Number of bytes written=606592
    FILE: Number of read operations=0
    FILE: Number of large read operations=0
    FILE: Number of write operations=0
    HDFS: Number of bytes read=524290223
    HDFS: Number of bytes written=524288000
    HDFS: Number of read operations=58
    HDFS: Number of large read operations=0
    HDFS: Number of write operations=15
  Job Counters
    Launched map tasks=4
    Other local map tasks=4
    Total time spent by all maps in occupied slots (ms)=20657
    Total time spent by all reduces in occupied slots (ms)=0
    Total time spent by all map tasks (ms)=20657
    Total vcore-milliseconds taken by all map tasks=20657
    Total megabyte-milliseconds taken by all map tasks=21152768
  Map-Reduce Framework
    Map input records=4
    Map output records=0
    Input split bytes=460
    Spilled Records=0
    Failed Shuffles=0
    Merged Map outputs=0
    GC time elapsed (ms)=237
    CPU time spent (ms)=6910
    Physical memory (bytes) snapshot=1145573376
    Virtual memory (bytes) snapshot=6334038016
    Total committed heap usage (bytes)=1412956160
  File Input Format Counters
    Bytes Read=1763
  File Output Format Counters
    Bytes Written=0
  DistCp Counters
    Bytes Copied=524288000
    Bytes Expected=524288000
    Files Copied=4
```


Confirm files copied successfully:

```
[hdfs@ip-172-31-39-85 root]$ hdfs dfs -ls /user/willwatters_copy
Found 3 items
-rw-r--r--   3 hdfs supergroup          0 2018-10-16 14:51 /user/willwatters_copy/_SUCCESS
-rw-r--r--   3 hdfs supergroup  262144000 2018-10-16 14:51 /user/willwatters_copy/part-m-00000
-rw-r--r--   3 hdfs supergroup  262144000 2018-10-16 14:51 /user/willwatters_copy/part-m-00001
```


## Browse the results - use hdfs fsck <path> -files -blocks on your source and target directories

hdfs fsck <path> -files -blocks on source directory:

```
[hdfs@ip-172-31-39-85 root]$ hdfs fsck /willwatters -files -blocks
Connecting to namenode via http://ip-172-31-38-0.eu-west-3.compute.internal:50070/fsck?ugi=hdfs&files=1&blocks=1&path=%2Fwillwatters
FSCK started by hdfs (auth:SIMPLE) from /172.31.39.85 for path /willwatters at Tue Oct 16 14:52:38 UTC 2018
/willwatters <dir>
/willwatters/_SUCCESS 0 bytes, 0 block(s):  OK

/willwatters/part-m-00000 262144000 bytes, 2 block(s):  OK
0. BP-1433147642-172.31.38.0-1539698066621:blk_1073741918_1094 len=134217728 Live_repl=3
1. BP-1433147642-172.31.38.0-1539698066621:blk_1073741921_1097 len=127926272 Live_repl=3

/willwatters/part-m-00001 262144000 bytes, 2 block(s):  OK
0. BP-1433147642-172.31.38.0-1539698066621:blk_1073741919_1095 len=134217728 Live_repl=3
1. BP-1433147642-172.31.38.0-1539698066621:blk_1073741922_1098 len=127926272 Live_repl=3

Status: HEALTHY
 Total size:  524288000 B
 Total dirs:  1
 Total files: 3
 Total symlinks:    0
 Total blocks (validated):  4 (avg. block size 131072000 B)
 Minimally replicated blocks: 4 (100.0 %)
 Over-replicated blocks:  0 (0.0 %)
 Under-replicated blocks: 0 (0.0 %)
 Mis-replicated blocks:   0 (0.0 %)
 Default replication factor:  3
 Average block replication: 3.0
 Corrupt blocks:    0
 Missing replicas:    0 (0.0 %)
 Number of data-nodes:    4
 Number of racks:   1
FSCK ended at Tue Oct 16 14:52:38 UTC 2018 in 2 milliseconds


The filesystem under path '/willwatters' is HEALTHY
```

hdfs fsck <path> -files -blocks on target directory:

```
[hdfs@ip-172-31-39-85 root]$ hdfs fsck /user/willwatters_copy -files -blocks
Connecting to namenode via http://ip-172-31-38-0.eu-west-3.compute.internal:50070/fsck?ugi=hdfs&files=1&blocks=1&path=%2Fuser%2Fwillwatters_copy
FSCK started by hdfs (auth:SIMPLE) from /172.31.39.85 for path /user/willwatters_copy at Tue Oct 16 14:53:41 UTC 2018
/user/willwatters_copy <dir>
/user/willwatters_copy/_SUCCESS 0 bytes, 0 block(s):  OK

/user/willwatters_copy/part-m-00000 262144000 bytes, 2 block(s):  OK
0. BP-1433147642-172.31.38.0-1539698066621:blk_1073741939_1115 len=134217728 Live_repl=3
1. BP-1433147642-172.31.38.0-1539698066621:blk_1073741942_1118 len=127926272 Live_repl=3

/user/willwatters_copy/part-m-00001 262144000 bytes, 2 block(s):  OK
0. BP-1433147642-172.31.38.0-1539698066621:blk_1073741941_1117 len=134217728 Live_repl=3
1. BP-1433147642-172.31.38.0-1539698066621:blk_1073741943_1119 len=127926272 Live_repl=3

Status: HEALTHY
 Total size:  524288000 B
 Total dirs:  1
 Total files: 3
 Total symlinks:    0
 Total blocks (validated):  4 (avg. block size 131072000 B)
 Minimally replicated blocks: 4 (100.0 %)
 Over-replicated blocks:  0 (0.0 %)
 Under-replicated blocks: 0 (0.0 %)
 Mis-replicated blocks:   0 (0.0 %)
 Default replication factor:  3
 Average block replication: 3.0
 Corrupt blocks:    0
 Missing replicas:    0 (0.0 %)
 Number of data-nodes:    4
 Number of racks:   1
FSCK ended at Tue Oct 16 14:53:41 UTC 2018 in 1 milliseconds


The filesystem under path '/user/willwatters_copy' is HEALTHY
```
