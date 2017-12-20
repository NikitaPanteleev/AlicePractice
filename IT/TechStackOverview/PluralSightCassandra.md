# Cassandra for developers
## Introduction
### Facebook paper:
https://www.cs.cornell.edu/projects/ladis2009/papers/lakshman-ladis2009.pdf

1. Introduction
- cheap commodity
- handle high write throughput while not sacrificing read efficiency.
- developed for Ibox search problem (250 millions user)
2. Related work
Availability vs consistency.
- Farsite uses replicattion
- Google File system uses master node
- Bayou disconnected operations, eventual data consistency
- dynamo by amazon for user shopping carts. Vector clocks
http://courses.cs.vt.edu/~cs5204/fall00/vector_clocks.html
Process has internal counters and information about all other process
counters. Inforamtion is updated on each message. Events are caused
ony by another or independent.
3. Data model
- A table in Cassandra is a distributed multi dimensional map indexed by a key.
- Every operation under a single row key is atomic per replica
- The system allows columns to be sorted either by time or by name.
4. API
- insert(table, key, rowMutation)
- get(table, key, columnName)
- delete(table, key, columnName)
5. SYSTEM ARCHITECTURE
- request for key -> any node -> go to replicas
- for write -> wait for quorom of replicas
- for read -> either closest replica or route
5. 1 Partitioning
Nodes are placed in ring. Each key hash go to ring, then assigned to
the nearest clockwise node. Adding new node affects only 2 neigbours

There are 2 approaches
- assign nodes to multiple positions in the ring.
- analyze load information and move lightly assigned node to the
heavily ones. (this one is used)

5. 2 Replication.
- replicas are chosen based on replication policy.
- zookeeper chose the leader node to detemine ranges for each node

5. 3 Membership
- Gossip based mechanism.
- Accrual Failure Detection - detection module emits not boolean value
but some function about node up or down

5. 4 Bootstraping
manual joining of new node

5. 5 Scaling the cluster
40 Mb/s to transfer data to new node

5. 6 Local persistence
- The write into the in-memory data structure is performed only after a
successful write into the commit log.
- in-memorey data structure alsow writes itself on disk based on some
interval

5. 7 Implementation details
- partitioning module,
- the cluster membership and failure detection module
- the storage engine module
- all reads/writes are sequantial thus no locks
- writes are normal mode or fast async mode
- merge and compact files over time
6. PRACTICAL EXPERIENCES
- run M/R jobs to import data from MySQL to cassandra
- most application requires atomic, but transactional support is in
progress
- failure detection is reduced to 15 secs from 2 mins
- monitoring Ganglia
- zookeeper

6. Facebook Index Search
messages are indexed by user_id and families are words - value
messageId

## Dynamo and Bigtable papers
Dynamo: Amazon's High available key-value Store.

## virtual nodes with cassandra 2.0
Nodes on more powerfull nodes maintain more virtual nodes.
num_nodes: 256 - number of virtual tokesn
nodetool status
snitch  - GossipingPropertyFileSnitch

##Replication and consistency
-SimpleStrategy just with number of replicas.
-NetworkTopologyStrategy - number of replicas per datacentre

`docker -it n1 noodtool status keyspace`
