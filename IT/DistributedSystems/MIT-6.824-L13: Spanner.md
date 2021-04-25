# Links:
https://www.youtube.com/watch?v=4eW5SWBi7vs&list=PLrw6a1wE39_tb2fErI4-WkMbsvGQk9_UB&index=13
https://pdos.csail.mit.edu/6.824/papers/spanner.pdf

Sharded DB, each shard group managed by it's own paxos protocol

## Key ideas:
- run two phase commit across paxos coordinated shards to avoid the problem 
  that crashed coordinator can block everyone
- syncronized timestamps for efficient read-only  transactions
## Transactions
###Read/write transactions.

```
BEGIN
 x = x + 1
 y = y - 1
END
```

DC1  DC2          DC3
X    X(leader)    X
Y    Y            Y(leader) 


read locks maintained at the leader.
Client chooses one paxos leader as transaction coordinator.
On write transactions, the leaders sends PREPARE to replicas and on majority answers with YES
to coordinator.
Once all YES received, coordinator sends COMMIT command to leaders and to its own replicas.

People hate to use two-phase commit in real world, because of failed coordinate indefinitely 
locks the data. But in Spanner coordinator is paxos replicated.

### Read-only transactions
- serializable
- external consistency

write trx timestamp is commit time
read trx timestamp is read time.

Servers containt multi versioned data

### Sync clock
true time pair. Current time is greater earliest and less than latest
now() = `[earliest, latest]`



###Paper
https://pdos.csail.mit.edu/6.824/papers/spanner.pdf
#### features
Spanner is Google’s 
- scalable, 
- multi-version
- globallydistributed
- synchronously-replicated database
- supports externally-consistent distributed transactions

  Features:
- nonblocking reads in the past, 
- lock-free read-only transactions
- atomic schema changes, across all of Spanner.

CAP theorem:
https://storage.googleapis.com/pub-tools-public-publication-data/pdf/45855.pdf
 - C: Consistency, which we can think of as serializability for this discussion (and linearizabile in initial paper) ;
 - A: 100% availability, for both reads and updates;
 - P: tolerance to network partitions.
 
#### use case
F1, a rewrite of Google’s advertising backend, number of reads outline the number of writes

Specific features:
 - Applications can specify constraints to control which datacenters contain which data, how far data is from its users.
 - externally consistent reads and writes, and globally-consistent reads across the database at a timestamp 
 
 
