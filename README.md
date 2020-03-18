# New York Taxis Queries

Implementation of a system which uses New York taxi data and answering Batch &amp; Streaming queries using Spark and Hadoop Cluster.

It is implementation of a project in Distributed Systems, Big Data and Cloud Computing course.

The project is coded in **Spark Java** , **Python** and **Docker** is used.

# Project Informations 

 -First Part
    -Execution of 8 batch/streaming queries in a distributed environment (Hadoop and Spark cluster).

 -Second Part 
    -Set up Hadoop on Docker and run our app on it.
  
# Run Instractions
_--------------Basic Steps-------------_
 
docker-compose up -d
docker exec -it namenode bash #namenode to container name , -it 
docker cp fares.csv namenode:/
docker cp SparkHadoop-1.0-SNAPSHOT.jar namenode:/ 

_--------------Installs-------------_
  
apt-get update #must
apt-get install wget tar bash
wget https://www-eu.apache.org/dist/spark/spark-2.4.4/spark-2.4.4-bin-hadoop2.7.tgz #download to spark

tar -xzf spark-2.4.4-bin-hadoop2.7.tgz && \
    mv spark-2.4.4-bin-hadoop2.7 /spark && \
    rm spark-2.4.4-bin-hadoop2.7.tgz    
    
_--------------Move files to \spark/bin-------------_

mv SparkHadoop-1.0-SNAPSHOT.jar /spark/bin

_---------------Load fares csv to hadoop hdfs---------_

mkdir input
mv fares.csv input
hadoop fs -mkdir -p input
hdfs dfs -put ./input/* /user/root/
hdfs dfsadmin -safemode leave

_---------------Run Spark ---------_

cd spark/bin
./spark-submit --class testspark --master local[*] SparkHadoop-1.0-SNAPSHOT.jar
docker-compose down
    
 


