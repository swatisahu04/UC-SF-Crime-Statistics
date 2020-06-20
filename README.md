# UC-SF-Crime-Statistics
Kafka and Spark Streaming Integration project - SF Crime Statistics

  In this project we have real-world dataset, extracted from Kaggle, on San Francisco crime incidents, ane we have done  statistical analysis of the data using Apache Spark Structured Streaming. We have created a Kafka server to produce data, and ingest data through Spark Structured Streaming.
  
##################################
**Development Environment:

pip install -r requirements.txt

**Tools and Environemntal set-up details :

Spark 2.4.3
Scala 2.11.x
Java 1.8.x
Kafka build with Scala 2.11.x
Python 3.6.x or 3.7.x

**Environment set-up:

**Verify Java and Scals set-up

java -version
scala -version

**We can modify zookeeper.properties and sever.properties in Kafka Config folder as per our requirements.

**We should these variables set-up in /.bash_profile as per you system configuration

export SPARK_HOME=$HOME/setups/spark-2.3.3-bin-hadoop2.7
export JAVA_HOME=/Library/Java/JavaVirtualMachines/jdk1.8.0_202.jdk/Contents/Home
export SCALA_HOME=/usr/local/bin/scala/
export PATH=$JAVA_HOME/bin:$SPARK_HOME/bin:$SCALA_HOME/bin:$PATH


  
##################################
**Starting ZooKeeper/Kafka Services

$HOME/Kafka/kafka_2.11-2.3.0/bin/zookeeper-server-start.sh $HOME/Kafka/kafka_2.11-2.3.0/config/zookeeper.properties > $HOME/Kafka/kafkaLogs/zookeeper_server_`date +%F`_$$.log 2>&1 &
$HOME/Kafka/kafka_2.11-2.3.0/bin/kafka-server-start.sh $HOME/Kafka/kafka_2.11-2.3.0/config/server.properties > $HOME/Kafka/kafkaLogs/kafka_server_`date +%F`
_$$.log 2>&1 &

##################################
**Dependency

pip install kafka-python

##################################
**To trigger Kafka Server set-up

python $HOME/Kafka/Udacity_Kafka/sf-crime-data-project-files/producer_server.py
python $HOME/Kafka/Udacity_Kafka/sf-crime-data-project-files/kafka_server.py

##################################
**To check topic set-up

$HOME/Kafka/kafka_2.11-2.3.0/bin/kafka-topics.sh --list --zookeeper localhost:2181

Topic Name : department.call.service.log

##################################
**To see if you correctly implemented the server, try consuming data from topic

$HOME/Kafka/kafka_2.11-2.3.0/bin/kafka-console-consumer.sh --bootstrap-server localhost:9092 --topic department.call.service.log --from-beginning

##################################
**To start spark streaming job

spark-submit --packages org.apache.spark:spark-sql-kafka-0-10_2.11:2.4.5 --master local[*] data_stream.py > $HOME/Kafka/Udacity_Kafka/sf-crime-data-project-files/Logs/data_stream_$Log_Date_$$.log 2>&1 &

##################################
**Spark Streaming Optimization

How did changing values on the SparkSession property parameters affect the throughput and latency of the data?
Changing the spark session properties affect the inputRowsPerSecond and processedRowsPerSecond values which are used to analyze latency/throughput.

What were the 2-3 most efficient SparkSession property key/value pairs? Through testing multiple variations on values, how can you tell these were the most optimal?
To optimize the SparkSession property we should modify these properties :
spark.default.parallelism : 100
spark.sql.shuffle.partitions : 100
spark.streaming.kafka.maxRatePerPartition : 100



