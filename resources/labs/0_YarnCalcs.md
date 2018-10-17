# Doing the Math

Cluster with ten worker nodes. Each worker node has:

Twenty vcores
128 GB RAM
Twelve disks for DataNode use

## Inspect the derived/default values

The values inserted in the excel file are:

```
Worker vcores 20
Worker spindles 12
Worker RAM 128
Workload factor 2
Worker nodes 10
```

The memory works out as:

```
12.8 GB
```

This is acceptable as 10% for this size of cluster is OK.

If overall memory was too high or low this would need adjusted accordinly.

I assume Impala, HBase and Solr are not required as they have not been specified as a requirment, but if Impala was required it would be allocted 25% of the total amount of Mem and CPU as below:

```
Impala Memory 32GB
Impala vcores 5
```


The workload factor affects the mapreduce.job.maps and mapreduce.job.reduces critera.

It is currently set as 2.  If chagned higher (i.e. 4 or more) it does not change anything, but if reduced to lower than 2 it sets the mapreduce.job.maps and mapreduce.job.reduces from the minimum value of 15 to 10.
