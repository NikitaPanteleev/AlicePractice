# Chapter 10. Batch Processing.
Materials:
 - [MapReduce 2004](https://pdos.csail.mit.edu/6.824/papers/mapreduce.pdf)
 -  Designing Data-Intensive Applications. Chapter 10: Batch Processing

## Types of systems:
- realtime services
- batch processing systems
- stream processing systems

## Batch processing with Unix Tools
```
cat var/log/containers/p2p-service-528ca62b826b-stdouterr.log | awk '{print $8}' | sort | uniq -c | head -n 5
  26 auditLogger
  29 o.s.web.servlet.PageNotFound
```

Let's solve the same problem using Java ``HashMap<String, Integer>`. Which approach is better?
<details><summary>Answer</summary>
<p>
If data fits in the memory, then both are fine (although theoretically, hashmap is faster then sorting).
If not, then sorting via MergeSort with sequential access pattern perform well on disks. GNU coreutils spills large chunks to the disk & use all cores. 

</p>
</details>

## Unix philosophy
 - each program does one thing well
 - uniform interfaces: output of one program is the input of another (avoid complicated formats, unnecessary information)
 - rapid prototyping & incremental iteration

In Unix uniform interface is a file descriptor = ordered sequence of bytes (file, another process, device driver).
And moreover it can be parallelized on multiple machines using GNU Parallel

## MapReduce And Distributed Systems

Distributed file storages: GFS, HDFS, Gluster FS, Amazon S3, Azure Blob Storage, OpenStak Swift.
### GFS
Master & nodes

Master Data: array of chunk handlers (non-volitile storage = nv)
chunk handler -> 
  - list of chunk servers (volatile storage=v)
  - version # (nv)
  - primary (v)
  - lease expiration(v)

LOG, CHECKPOINT are saved on the disk

### MapReduce
[Picture](https://data-flair.training/blogs/wp-content/uploads/sites/2/2017/04/Map-only.png)
Shuffling:
Mapper: fat jar with code, read file, execute code, partition output (K, V) by reducer hashkey, sort ouput files, notify reducers.
Reducer: download data from mappers.

Simple jobs are combined in the workflows by tools such as Oozie, Azbakan, Luigi, Airflow and Pinball.
Or higher level (on top of Hadoop): Pig, Hive, Cascading, Crunch, FlumeJava.

### Joins
Reduce-side joins: partition by the same key and group on reducer job (sort merge join), handling hot keys.
Map-side joins: broadcast hash joins (or partitioned hash joins).


Output of files, optimization based on in-memory computing, not waiting the previous job to finsh, diversity of storage, sql-like API with related optimizations.
Graphs models (like Pregel) uses iterative over vertices approach.

