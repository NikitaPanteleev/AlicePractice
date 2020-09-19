# Guide

## Major steps
1. Requirements clarifications.
2. Estimation.
3. System interface definition
4. Defining data model
5. High level design
6. Detailed design
7. Identifying & resolving bottlenecks


# System design glossary

## Key charactiristics
Scalability
Reliablitly
Availability
Efficiency
Maintance costs (serviceability or manageability)

## Load balancing
Choice of server: round-robin, IP hashing, least traffic,...
Redundant LB to form cluster.
https://lethain.com/introduction-to-architecting-systems-for-scale/

## Cache
 - Application layer cache
 - Content Distrubuted Cache (CDN)
 - Cache invalidation
   - write-though: write to cache and rds
   - write-around: write to rds and invalidate cache
   - write-back: write to cache, write to rds later
 - cache eviction (fifo, lifo, time expiration)

## Data partitioning
Paritioning methods:
 - horizontal (data sharding)
 - vertical 
 - directory based partitioning (hybrid approach)

Partitioning criteria
 - hash
 - list
 - round robin
 - composite approach

Common problems of data partitioning
 - joins are very unefficient, data should be denormalized
 - no referential integrity (as foreign keys are not supported)
 - rebalancing without downtime is a challenge

## Indexes

## Proxies
Forward & reverse proxies

## Redundancy & replication

## SQL vs NoSql

NoSql:
 - key-value stores (redis, dynamoDB)
 - document db (coachdb & mongodb)
 - column based (cassandra & hbase)
 - graphs (neo4J)

Difference:
 - querying
 - scalability
 - SQL are ACID (atomic, consistent, isolated, durable)

Reasons for SQL
 - ACID
 - expected load and structure

Reasons for NoSQL:
 - large volumes
 - scalable solution out of the box
 - rapid development


## CAP theorem
CAP
CA - RDBS
AP - cassandra
CP - mongodb, hbase

## Long-Polling vs WS vs Server Events
Ajax polling, long-polling, WS (dupliex), Server Side Events (one way)





## Consistent hashing

Hash function: index = key % n
Problems:
 - it's not horizontally scalable
 - it may not be uniformly load balanced

