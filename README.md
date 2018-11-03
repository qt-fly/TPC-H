# TPC-H Benchmark test
Simple experiment runs TPC-H benchmark on a small cluster. 
Congigure hadoop yarn sparksql.

Based on https://github.com/ssavvides/tpch-spark &
         https://github.com/xiandong79/tpch-Spark.git
         
Requirements:
sudo apt install default-jdk, scala

Possible problems
0. Java_home hadoop-env.sh.
1. hadoop configuration
   hadoop: bin/hadoop namenode -format
   hadoop: ./sbin/start-all.sh
   hadoop: ./sbin/stop-all.sh
2. Cannot start namenode or datanode
   Delete hdfs file which contains namenode and datanode and do #1
   Then, need to upload data to hdfs
         hdfs dfs -mkdir /tpch
         hdfs dfs -put dbgen/*.tbl /tpch
   Check data: hdfs dfs -ls /tpch
               hadoop fs -du -s /tpch/* | awk '{s+=$1} END {printf "%.3fGB\n", s/1000000000}' (total size, GB)
3. Name node is in safe mode
   Solve: hadoop dfsadmin -safemode leave
4. Change INPUT_DIR & OUTPUT_DIR in TpchQuery.scala. Either hdfs or local file
5. Default yarn.nodemanager.vmem-pmem-ratio is 2.1. Depend on your dataset, you need to change this in yarn-site.xml


