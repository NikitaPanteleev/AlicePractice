# Apache Spark Streaming
## Transformations
 - UpdateStateByKey Operation
Allows Statefull computation
 - Transform Operation
Allows use dstream.map(rdd => {rdd.join().. or other RDD operation})
 - Window Operation
 - Join Operations
   * stream-stream
   * stream-dataset

 - Output operations
   * print()
   * saveAsObjectFile()
   * foreachRDD
   
*NB* Be carefull with partitions:
```
dstream.foreachRDD { rdd =>
  rdd.foreachPartition { partitionOfRecords =>
    val connection = createNewConnection()
    partitionOfRecords.foreach(record => connection.send(record))
    connection.close()
  }
}
```
## MLib Operations
Some models can be learnt from stream: (Streaming Linear Regression,
Streaming KMeans), others are learnt offline and applied to streams.
## Caching / Persistence
https://spark.apache.org/docs/latest/streaming-programming-guide.html#caching--persistence

HashMap on nodes.
http://stackoverflow.com/questions/23414238/apache-spark-hashmap-accumulators-give-type-mismatch-error

