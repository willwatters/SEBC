# Test HDFS performance

## Create an end-user Linux account named with your GitHub handle

GitHub handle account name added on all cluster hosts.  Below shows this done on one host:

```
[root@ip-172-31-39-85 ~]# adduser willwatters
[root@ip-172-31-39-85 ~]# passwd willwatters
Changing password for user willwatters.
New password:
```

## Create HDFS user home directory for this user (command typed on a DataNode):

```
[root@ip-172-31-39-85 ~]# sudo su hdfs
[hdfs@ip-172-31-39-85 root]$ hdfs dfs -mkdir /user/willwatters
[hdfs@ip-172-31-39-85 root]$ hdfs dfs -ls /user
Found 5 items
drwx------   - hdfs   supergroup          0 2018-10-16 14:37 /user/hdfs
drwxrwxrwx   - mapred hadoop              0 2018-10-16 13:55 /user/history
drwxr-xr-x   - hdfs   supergroup          0 2018-10-16 14:42 /user/teragen_copy
drwxr-xr-x   - hdfs   supergroup          0 2018-10-16 14:58 /user/willwatters
drwxr-xr-x   - hdfs   supergroup          0 2018-10-16 14:51 /user/willwatters_copy
```

Change ownership:

```
[hdfs@ip-172-31-39-85 root]$ hdfs dfs -chown willwatters:willwatters /user/willwatters
[hdfs@ip-172-31-39-85 root]$ hdfs dfs -ls /user
Found 5 items
drwx------   - hdfs        supergroup           0 2018-10-16 14:37 /user/hdfs
drwxrwxrwx   - mapred      hadoop               0 2018-10-16 13:55 /user/history
drwxr-xr-x   - hdfs        supergroup           0 2018-10-16 14:42 /user/teragen_copy
drwxr-xr-x   - willwatters willwatters          0 2018-10-16 14:58 /user/willwatters
drwxr-xr-x   - hdfs        supergroup           0 2018-10-16 14:51 /user/willwatters_copy
```

## Create a 10 GB file using teragen, as the new created HDFS user

Create a 10 GB file using teragen (1024 (KB) x 1024 (MB) x 1024 (GB) x 10 (10 GB) / 100 (Byte) = 107374182)
Set the number of mappers to four
Limit the block size to 32 MB (1024 (KB) x 1024 (MB) x 32 (MB) = 33554432 (Bytes))
Land the result under your user's home directory
Use the time command to report the job's duration

```
[willwatters@ip-172-31-39-85 root]$ time hadoop jar /opt/cloudera/parcels/CDH/jars/hadoop-examples.jar teragen -Dmapreduce.job.maps=4 -Ddfs.blocksize=33554432 107374182 /user/willwatters/teragen
18/10/16 15:33:38 INFO client.RMProxy: Connecting to ResourceManager at ip-172-31-46-203.eu-west-3.compute.internal/172.31.46.203:8032
18/10/16 15:33:38 INFO terasort.TeraGen: Generating 107374182 using 4
18/10/16 15:33:38 INFO mapreduce.JobSubmitter: number of splits:4teragen -Dmapreduce.job.maps=4 -Ddfs.blocksize=335544[willwatters@ip-172-31-39-85 root]$ time hadoop jar /opt/cloudera/parcels/CDH/jars/h
18/10/16 15:33:38 INFO mapreduce.JobSubmitter: Submitting tokens for job: job_1539698111610_0005
18/10/16 15:33:38 INFO impl.YarnClientImpl: Submitted application application_1539698111610_0005
18/10/16 15:33:39 INFO mapreduce.Job: The url to track the job: http://ip-172-31-46-203.eu-west-3.compute.internal:8088/proxy/application_1539698111610_0005/
18/10/16 15:33:39 INFO mapreduce.Job: Running job: job_1539698111610_0005
18/10/16 15:33:45 INFO mapreduce.Job: Job job_1539698111610_0005 running in uber mode : false
18/10/16 15:33:45 INFO mapreduce.Job:  map 0% reduce 0%
18/10/16 15:34:01 INFO mapreduce.Job:  map 11% reduce 0%
18/10/16 15:34:02 INFO mapreduce.Job:  map 39% reduce 0%
18/10/16 15:34:07 INFO mapreduce.Job:  map 49% reduce 0%
18/10/16 15:34:08 INFO mapreduce.Job:  map 59% reduce 0%
18/10/16 15:34:13 INFO mapreduce.Job:  map 67% reduce 0%
18/10/16 15:34:14 INFO mapreduce.Job:  map 74% reduce 0%
18/10/16 15:34:19 INFO mapreduce.Job:  map 77% reduce 0%
18/10/16 15:34:20 INFO mapreduce.Job:  map 80% reduce 0%
18/10/16 15:34:25 INFO mapreduce.Job:  map 84% reduce 0%
18/10/16 15:34:26 INFO mapreduce.Job:  map 88% reduce 0%
18/10/16 15:34:28 INFO mapreduce.Job:  map 89% reduce 0%
18/10/16 15:34:30 INFO mapreduce.Job:  map 90% reduce 0%
18/10/16 15:34:31 INFO mapreduce.Job:  map 92% reduce 0%
18/10/16 15:34:32 INFO mapreduce.Job:  map 94% reduce 0%
18/10/16 15:34:37 INFO mapreduce.Job:  map 97% reduce 0%
18/10/16 15:34:38 INFO mapreduce.Job:  map 99% reduce 0%
18/10/16 15:34:39 INFO mapreduce.Job:  map 100% reduce 0%
18/10/16 15:34:41 INFO mapreduce.Job: Job job_1539698111610_0005 completed successfully
18/10/16 15:34:41 INFO mapreduce.Job: Counters: 31
  File System Counters
    FILE: Number of bytes read=0
    FILE: Number of bytes written=592484
    FILE: Number of read operations=0
    FILE: Number of large read operations=0
    FILE: Number of write operations=0
    HDFS: Number of bytes read=344
    HDFS: Number of bytes written=10737418200
    HDFS: Number of read operations=16
    HDFS: Number of large read operations=0
    HDFS: Number of write operations=8
  Job Counters
    Launched map tasks=4
    Other local map tasks=4
    Total time spent by all maps in occupied slots (ms)=188888
    Total time spent by all reduces in occupied slots (ms)=0
    Total time spent by all map tasks (ms)=188888
    Total vcore-milliseconds taken by all map tasks=188888
    Total megabyte-milliseconds taken by all map tasks=193421312
  Map-Reduce Framework
    Map input records=107374182
    Map output records=107374182
    Input split bytes=344
    Spilled Records=0
    Failed Shuffles=0
    Merged Map outputs=0
    GC time elapsed (ms)=1132
    CPU time spent (ms)=125120
    Physical memory (bytes) snapshot=678985728
    Virtual memory (bytes) snapshot=6332100608
    Total committed heap usage (bytes)=870842368
  org.apache.hadoop.examples.terasort.TeraGen$Counters
    CHECKSUM=230593859918397906
  File Input Format Counters
    Bytes Read=0
  File Output Format Counters
    Bytes Written=10737418200

real  1m5.377s
user  0m4.319s
sys 0m0.209s
```

Confirm that the four files exist and the total sum of the produced files is 10GB:

```
[willwatters@ip-172-31-39-85 root]$ hdfs dfs -ls /user/willwatters/teragen
Found 5 items
-rw-r--r--   3 willwatters willwatters          0 2018-10-16 15:34 /user/willwatters/teragen/_SUCCESS
-rw-r--r--   3 willwatters willwatters 2684354600 2018-10-16 15:34 /user/willwatters/teragen/part-m-00000
-rw-r--r--   3 willwatters willwatters 2684354500 2018-10-16 15:34 /user/willwatters/teragen/part-m-00001
-rw-r--r--   3 willwatters willwatters 2684354600 2018-10-16 15:34 /user/willwatters/teragen/part-m-00002
-rw-r--r--   3 willwatters willwatters 2684354500 2018-10-16 15:34 /user/willwatters/teragen/part-m-00003
```


## Run the terasort command on the produced file

Use the time command to report the job's duration
Land the result under your user's home directory

```
[willwatters@ip-172-31-39-85 root]$ time hadoop jar /opt/cloudera/parcels/CDH/jars/hadoop-examples.jar terasort /user/willwatters/teragen /user/willwatters/terasort
18/10/16 15:43:26 INFO terasort.TeraSort: starting
18/10/16 15:43:27 INFO input.FileInputFormat: Total input paths to process : 4
Spent 195ms computing base-splits.
Spent 5ms computing TeraScheduler splits.
Computing input splits took 201ms
Sampling 10 splits of 320
Making 8 from 100000 sampled records
Computing parititions took 535ms
Spent 737ms computing partitions.
18/10/16 15:43:27 INFO client.RMProxy: Connecting to ResourceManager at ip-172-31-46-203.eu-west-3.compute.internal/172.31.46.203:8032
18/10/16 15:43:28 INFO mapreduce.JobSubmitter: number of splits:320
18/10/16 15:43:28 INFO mapreduce.JobSubmitter: Submitting tokens for job: job_1539698111610_0006
18/10/16 15:43:28 INFO impl.YarnClientImpl: Submitted application application_1539698111610_0006
18/10/16 15:43:28 INFO mapreduce.Job: The url to track the job: http://ip-172-31-46-203.eu-west-3.compute.internal:8088/proxy/application_1539698111610_0006/
18/10/16 15:43:28 INFO mapreduce.Job: Running job: job_1539698111610_0006
18/10/16 15:43:33 INFO mapreduce.Job: Job job_1539698111610_0006 running in uber mode : false
18/10/16 15:43:33 INFO mapreduce.Job:  map 0% reduce 0%
18/10/16 15:43:40 INFO mapreduce.Job:  map 1% reduce 0%
18/10/16 15:43:41 INFO mapreduce.Job:  map 2% reduce 0%
18/10/16 15:43:44 INFO mapreduce.Job:  map 3% reduce 0%
18/10/16 15:43:46 INFO mapreduce.Job:  map 4% reduce 0%
18/10/16 15:43:49 INFO mapreduce.Job:  map 5% reduce 0%
18/10/16 15:43:52 INFO mapreduce.Job:  map 6% reduce 0%
18/10/16 15:43:53 INFO mapreduce.Job:  map 7% reduce 0%
18/10/16 15:43:54 INFO mapreduce.Job:  map 8% reduce 0%
18/10/16 15:44:00 INFO mapreduce.Job:  map 9% reduce 0%
18/10/16 15:44:03 INFO mapreduce.Job:  map 10% reduce 0%
18/10/16 15:44:04 INFO mapreduce.Job:  map 11% reduce 0%
18/10/16 15:44:06 INFO mapreduce.Job:  map 12% reduce 0%
18/10/16 15:44:10 INFO mapreduce.Job:  map 13% reduce 0%
18/10/16 15:44:11 INFO mapreduce.Job:  map 14% reduce 0%
18/10/16 15:44:13 INFO mapreduce.Job:  map 15% reduce 0%
18/10/16 15:44:17 INFO mapreduce.Job:  map 16% reduce 0%
18/10/16 15:44:19 INFO mapreduce.Job:  map 17% reduce 0%
18/10/16 15:44:22 INFO mapreduce.Job:  map 18% reduce 0%
18/10/16 15:44:23 INFO mapreduce.Job:  map 19% reduce 0%
18/10/16 15:44:28 INFO mapreduce.Job:  map 20% reduce 0%
18/10/16 15:44:29 INFO mapreduce.Job:  map 21% reduce 0%
18/10/16 15:44:30 INFO mapreduce.Job:  map 22% reduce 0%
18/10/16 15:44:34 INFO mapreduce.Job:  map 23% reduce 0%
18/10/16 15:44:35 INFO mapreduce.Job:  map 24% reduce 0%
18/10/16 15:44:39 INFO mapreduce.Job:  map 25% reduce 0%
18/10/16 15:44:40 INFO mapreduce.Job:  map 26% reduce 0%
18/10/16 15:44:41 INFO mapreduce.Job:  map 27% reduce 0%
18/10/16 15:44:46 INFO mapreduce.Job:  map 28% reduce 0%
18/10/16 15:44:48 INFO mapreduce.Job:  map 29% reduce 0%
18/10/16 15:44:49 INFO mapreduce.Job:  map 30% reduce 0%
18/10/16 15:44:53 INFO mapreduce.Job:  map 31% reduce 0%
18/10/16 15:44:55 INFO mapreduce.Job:  map 32% reduce 0%
18/10/16 15:44:58 INFO mapreduce.Job:  map 33% reduce 0%
18/10/16 15:44:59 INFO mapreduce.Job:  map 34% reduce 0%
18/10/16 15:45:04 INFO mapreduce.Job:  map 35% reduce 0%
18/10/16 15:45:05 INFO mapreduce.Job:  map 36% reduce 0%
18/10/16 15:45:06 INFO mapreduce.Job:  map 37% reduce 0%
18/10/16 15:45:10 INFO mapreduce.Job:  map 38% reduce 0%
18/10/16 15:45:12 INFO mapreduce.Job:  map 39% reduce 0%
18/10/16 15:45:16 INFO mapreduce.Job:  map 40% reduce 0%
18/10/16 15:45:17 INFO mapreduce.Job:  map 41% reduce 0%
18/10/16 15:45:20 INFO mapreduce.Job:  map 42% reduce 0%
18/10/16 15:45:23 INFO mapreduce.Job:  map 43% reduce 0%
18/10/16 15:45:24 INFO mapreduce.Job:  map 44% reduce 0%
18/10/16 15:45:29 INFO mapreduce.Job:  map 46% reduce 0%
18/10/16 15:45:34 INFO mapreduce.Job:  map 47% reduce 0%
18/10/16 15:45:35 INFO mapreduce.Job:  map 48% reduce 0%
18/10/16 15:45:36 INFO mapreduce.Job:  map 49% reduce 0%
18/10/16 15:45:41 INFO mapreduce.Job:  map 50% reduce 0%
18/10/16 15:45:42 INFO mapreduce.Job:  map 51% reduce 0%
18/10/16 15:45:43 INFO mapreduce.Job:  map 52% reduce 0%
18/10/16 15:45:47 INFO mapreduce.Job:  map 53% reduce 0%
18/10/16 15:45:49 INFO mapreduce.Job:  map 54% reduce 0%
18/10/16 15:45:51 INFO mapreduce.Job:  map 55% reduce 0%
18/10/16 15:45:53 INFO mapreduce.Job:  map 56% reduce 0%
18/10/16 15:45:56 INFO mapreduce.Job:  map 57% reduce 0%
18/10/16 15:45:59 INFO mapreduce.Job:  map 58% reduce 0%
18/10/16 15:46:00 INFO mapreduce.Job:  map 59% reduce 0%
18/10/16 15:46:04 INFO mapreduce.Job:  map 60% reduce 0%
18/10/16 15:46:05 INFO mapreduce.Job:  map 61% reduce 0%
18/10/16 15:46:09 INFO mapreduce.Job:  map 62% reduce 0%
18/10/16 15:46:10 INFO mapreduce.Job:  map 63% reduce 0%
18/10/16 15:46:13 INFO mapreduce.Job:  map 64% reduce 0%
18/10/16 15:46:16 INFO mapreduce.Job:  map 65% reduce 0%
18/10/16 15:46:18 INFO mapreduce.Job:  map 66% reduce 0%
18/10/16 15:46:19 INFO mapreduce.Job:  map 67% reduce 0%
18/10/16 15:46:23 INFO mapreduce.Job:  map 68% reduce 0%
18/10/16 15:46:28 INFO mapreduce.Job:  map 69% reduce 0%
18/10/16 15:46:29 INFO mapreduce.Job:  map 70% reduce 0%
18/10/16 15:46:30 INFO mapreduce.Job:  map 71% reduce 0%
18/10/16 15:46:35 INFO mapreduce.Job:  map 72% reduce 0%
18/10/16 15:46:36 INFO mapreduce.Job:  map 73% reduce 0%
18/10/16 15:46:38 INFO mapreduce.Job:  map 74% reduce 0%
18/10/16 15:46:41 INFO mapreduce.Job:  map 75% reduce 0%
18/10/16 15:46:42 INFO mapreduce.Job:  map 76% reduce 0%
18/10/16 15:46:45 INFO mapreduce.Job:  map 77% reduce 0%
18/10/16 15:46:47 INFO mapreduce.Job:  map 78% reduce 0%
18/10/16 15:46:49 INFO mapreduce.Job:  map 79% reduce 0%
18/10/16 15:46:53 INFO mapreduce.Job:  map 80% reduce 0%
18/10/16 15:46:54 INFO mapreduce.Job:  map 81% reduce 0%
18/10/16 15:46:56 INFO mapreduce.Job:  map 82% reduce 0%
18/10/16 15:46:59 INFO mapreduce.Job:  map 83% reduce 0%
18/10/16 15:47:04 INFO mapreduce.Job:  map 84% reduce 0%
18/10/16 15:47:10 INFO mapreduce.Job:  map 85% reduce 0%
18/10/16 15:47:13 INFO mapreduce.Job:  map 86% reduce 4%
18/10/16 15:47:15 INFO mapreduce.Job:  map 86% reduce 14%
18/10/16 15:47:16 INFO mapreduce.Job:  map 86% reduce 18%
18/10/16 15:47:19 INFO mapreduce.Job:  map 87% reduce 18%
18/10/16 15:47:20 INFO mapreduce.Job:  map 88% reduce 18%
18/10/16 15:47:26 INFO mapreduce.Job:  map 89% reduce 18%
18/10/16 15:47:31 INFO mapreduce.Job:  map 90% reduce 18%
18/10/16 15:47:32 INFO mapreduce.Job:  map 90% reduce 19%
18/10/16 15:47:35 INFO mapreduce.Job:  map 91% reduce 19%
18/10/16 15:47:39 INFO mapreduce.Job:  map 92% reduce 19%
18/10/16 15:47:44 INFO mapreduce.Job:  map 93% reduce 19%
18/10/16 15:47:49 INFO mapreduce.Job:  map 94% reduce 19%
18/10/16 15:47:51 INFO mapreduce.Job:  map 94% reduce 20%
18/10/16 15:47:54 INFO mapreduce.Job:  map 95% reduce 20%
18/10/16 15:47:55 INFO mapreduce.Job:  map 96% reduce 20%
18/10/16 15:48:02 INFO mapreduce.Job:  map 97% reduce 20%
18/10/16 15:48:06 INFO mapreduce.Job:  map 98% reduce 20%
18/10/16 15:48:11 INFO mapreduce.Job:  map 99% reduce 20%
18/10/16 15:48:15 INFO mapreduce.Job:  map 100% reduce 21%
18/10/16 15:48:20 INFO mapreduce.Job:  map 100% reduce 24%
18/10/16 15:48:21 INFO mapreduce.Job:  map 100% reduce 29%
18/10/16 15:48:22 INFO mapreduce.Job:  map 100% reduce 44%
18/10/16 15:48:26 INFO mapreduce.Job:  map 100% reduce 45%
18/10/16 15:48:27 INFO mapreduce.Job:  map 100% reduce 47%
18/10/16 15:48:28 INFO mapreduce.Job:  map 100% reduce 53%
18/10/16 15:48:30 INFO mapreduce.Job:  map 100% reduce 58%
18/10/16 15:48:31 INFO mapreduce.Job:  map 100% reduce 64%
18/10/16 15:48:32 INFO mapreduce.Job:  map 100% reduce 66%
18/10/16 15:48:34 INFO mapreduce.Job:  map 100% reduce 68%
18/10/16 15:48:36 INFO mapreduce.Job:  map 100% reduce 73%
18/10/16 15:48:37 INFO mapreduce.Job:  map 100% reduce 75%
18/10/16 15:48:38 INFO mapreduce.Job:  map 100% reduce 77%
18/10/16 15:48:40 INFO mapreduce.Job:  map 100% reduce 78%
18/10/16 15:48:42 INFO mapreduce.Job:  map 100% reduce 81%
18/10/16 15:48:43 INFO mapreduce.Job:  map 100% reduce 91%
18/10/16 15:48:45 INFO mapreduce.Job:  map 100% reduce 92%
18/10/16 15:48:49 INFO mapreduce.Job:  map 100% reduce 96%
18/10/16 15:48:55 INFO mapreduce.Job:  map 100% reduce 100%
18/10/16 15:48:55 INFO mapreduce.Job: Job job_1539698111610_0006 completed successfully
18/10/16 15:48:55 INFO mapreduce.Job: Counters: 49
  File System Counters
    FILE: Number of bytes read=4777727684
    FILE: Number of bytes written=9489701595
    FILE: Number of read operations=0
    FILE: Number of large read operations=0
    FILE: Number of write operations=0
    HDFS: Number of bytes read=10737468120
    HDFS: Number of bytes written=10737418200
    HDFS: Number of read operations=984
    HDFS: Number of large read operations=0
    HDFS: Number of write operations=16
  Job Counters
    Launched map tasks=320
    Launched reduce tasks=8
    Data-local map tasks=320
    Total time spent by all maps in occupied slots (ms)=1752593
    Total time spent by all reduces in occupied slots (ms)=589058
    Total time spent by all map tasks (ms)=1752593
    Total time spent by all reduce tasks (ms)=589058
    Total vcore-milliseconds taken by all map tasks=1752593
    Total vcore-milliseconds taken by all reduce tasks=589058
    Total megabyte-milliseconds taken by all map tasks=1794655232
    Total megabyte-milliseconds taken by all reduce tasks=603195392
  Map-Reduce Framework
    Map input records=107374182
    Map output records=107374182
    Map output bytes=10952166564
    Map output materialized bytes=4662839493
    Input split bytes=49920
    Combine input records=0
    Combine output records=0
    Reduce input groups=107374182
    Reduce shuffle bytes=4662839493
    Reduce input records=107374182
    Reduce output records=107374182
    Spilled Records=214748364
    Shuffled Maps =2560
    Failed Shuffles=0
    Merged Map outputs=2560
    GC time elapsed (ms)=37939
    CPU time spent (ms)=1150330
    Physical memory (bytes) snapshot=166114967552
    Virtual memory (bytes) snapshot=519803752448
    Total committed heap usage (bytes)=189347135488
  Shuffle Errors
    BAD_ID=0
    CONNECTION=0
    IO_ERROR=0
    WRONG_LENGTH=0
    WRONG_MAP=0
    WRONG_REDUCE=0
  File Input Format Counters
    Bytes Read=10737418200
  File Output Format Counters
    Bytes Written=10737418200
18/10/16 15:48:55 INFO terasort.TeraSort: done

real  5m30.186s
user  0m6.706s
sys 0m0.273s
```

Confirm output of Terasort:

```
[willwatters@ip-172-31-39-85 root]$ hdfs dfs -ls /user/willwatters/terasort
Found 10 items
-rw-r--r--   1 willwatters willwatters          0 2018-10-16 15:48 /user/willwatters/terasort/_SUCCESS
-rw-r--r--  10 willwatters willwatters         77 2018-10-16 15:43 /user/willwatters/terasort/_partition.lst
-rw-r--r--   1 willwatters willwatters 1331095000 2018-10-16 15:48 /user/willwatters/terasort/part-r-00000
-rw-r--r--   1 willwatters willwatters 1321689500 2018-10-16 15:48 /user/willwatters/terasort/part-r-00001
-rw-r--r--   1 willwatters willwatters 1350237000 2018-10-16 15:48 /user/willwatters/terasort/part-r-00002
-rw-r--r--   1 willwatters willwatters 1355345000 2018-10-16 15:48 /user/willwatters/terasort/part-r-00003
-rw-r--r--   1 willwatters willwatters 1343449500 2018-10-16 15:48 /user/willwatters/terasort/part-r-00004
-rw-r--r--   1 willwatters willwatters 1355238700 2018-10-16 15:48 /user/willwatters/terasort/part-r-00005
-rw-r--r--   1 willwatters willwatters 1319811300 2018-10-16 15:48 /user/willwatters/terasort/part-r-00006
-rw-r--r--   1 willwatters willwatters 1360552200 2018-10-16 15:48 /user/willwatters/terasort/part-r-00007
```
