PNWS 2014 - Apache Spark I: From Scala Collections to Fast Interactive Big Data with Spark
[slide](http://velvia.github.io/presentations/scala-collections-spark-intro-2014/index.html#/)
- Why do you love Scala so much? 
- It's almost Haskell

When reading data from HDFS or Cassandra the partition is given but it can be overriden with RDD.coalesce()

Within RDD Transformations:
- map, filter, groupBy, sample
Cross RDD Transformations:
- join, cartesian, coGroup
RDD Actions:
- reduce, count, collect, take, foreach
RDD Optimization / Misc:
- coalesce, repartition, pipe

Spark work with RDD as with streams.
.cache() : default is JVM heap... and SparkSQL caching based on column-value format

Part II 
[video](http://www.youtube.com/watch?v=J8FPrcsfqeY)