# Updated script

```
[root@ip-172-31-32-222 tmp]# cat YARNtest.sh
#!/bin/sh
# Confirm the path values given below correspond to your installation

MR=/opt/cloudera/parcels/CDH/lib/hadoop-0.20-mapreduce
HADOOP=/opt/cloudera/parcels/CDH/bin

# Mark start of the loop
echo Testing loop started on `date`

# Mapper containers
for i in 4 6 8
do
   # Reducer containers
   for j in 4 6 8
   do
      # Container memory
      for k in 512
      do
         # Set mapper JVM heap
         MAP_MB=`echo "($k*0.8)/1" | bc`

         # Set reducer JVM heap
         RED_MB=`echo "($k*0.8)/1" | bc`

  echo "Mappers= ${i}, Reducers= ${j}, Container memory= ${k}, Map MB=$MAP_MB"

        time ${HADOOP}/hadoop jar ${MR}/hadoop-examples.jar teragen \
                     -Dmapreduce.job.maps=$i \
                     -Dmapreduce.map.memory.mb=$k \
                     -Dmapreduce.map.java.opts.max.heap=$MAP_MB \
                     53687091 /results/tg-5GB-${i}-${j}-${k} 1>tera_${i}_${j}_${k}.out 2>tera_${i}_${j}_${k}.err

       time ${HADOOP}/hadoop jar $MR/hadoop-examples.jar terasort \
                     -Dmapreduce.job.maps=$i \
                     -Dmapreduce.job.reduces=$j \
                     -Dmapreduce.map.memory.mb=$k \
                     -Dmapreduce.map.java.opts.max.heap=$MAP_MB \
                     -Dmapreduce.reduce.memory.mb=$k \
                     -Dmapreduce.reduce.java.opts.max.heap=$RED_MB \
               /results/tg-5GB-${i}-${j}-${k}  \
                     /results/ts-5GB-${i}-${j}-${k} 1>>tera_${i}_${j}_${k}.out 2>>tera_${i}_${j}_${k}.err

        $HADOOP/hadoop fs -rm -r -skipTrash /results/tg-5GB-${i}-${j}-${k}
        $HADOOP/hadoop fs -rm -r -skipTrash /results/ts-5GB-${i}-${j}-${k}
      done
   done
done

echo Testing loop ended on `date`
```
