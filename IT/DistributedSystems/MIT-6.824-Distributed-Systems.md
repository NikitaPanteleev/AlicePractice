[youtube lectures](https://www.youtube.com/watch?v=-pKNCjUhPjQ&list=PLrw6a1wE39_tb2fErI4-WkMbsvGQk9_UB)

# Lecture 1: Introduction
reasons:
 - parallelism
 - fault taulerant
 - physical 
 - security / isolated.

challenges: 
 - concurrency
 - partial failure
 - performance

implementations
 - rpc
 - threads
 - concurrency ctrl

 performance

 fault tolerance:
 - availability
 - recoverability (non volatile storage is costly, replication)

 Consistency


# Lecture 2: RPC & threads.

Threads:
 - IO concurrency
 - parallelism
 - convinience

Race & locks
 - channels
 - sync.Cond
 - waitGroup

Deadlock

Webcrawler
 - parallel
 - every page single time
 - no cycles
 - know when to stop

# Lecture 3: GFS
## GFS [paper](https://pdos.csail.mit.edu/6.824/papers/gfs.pdf)
### Assumptions:
 - component failures are normal
 - huge files
 - mostly append/read operaions
 - co-designing API SLAs

### Architecture

Master reads chunk locations on start up. Writes event logs locally and remotely, saves checkpoint in parallel thread.

Master data:
 - file name -> array of chunks each of 64mb (nv - non-volatile)
 - file handler: list of chunk servers (v)
 - file handlers: version (nv)
 - file handler: primaty (v)
 - file handler: lease expiration (v)
 - log, checkpoint

### Operations
 - Read
 client -> master: name,ofsset
 master -> client: handler with list of servers
 client: metadata is cached
 client -> cs: read file in linux system
 cs -> client: return data

- Write (record-append)
client -> master: where is the last chunk

case 1: no primary.
master: find up-to-date replica, pick primary, secondary (P, S) - gives lease to primary.
master: increment #version number, tells P, S the latest version
master: write new version.
client -> primary
primary: picks offset and tells others to write the same.
primary: all secondaries replies YES, reply SUCCESS to the client
or
primary: if one secondaries failure, reply NO to the client


"split brain" is resolved by assigning the only one primary node for lease period (60 seconds)
no "two-phase commit" - ask secondary for the promise to do the operation.
the most serious limitation is the only one master, master is the bottleneck, manual recovery from master failure.
### other details
copy-on-write, locking based on file-name
High availability due ot fast recovery & chunk replication

Shadows of masters.

On reading, replicas verifies checksum

# Lecture 4: Primary-Backup Replication

Failures: fail-stop faults vs Bugs

State transfers (send RAM to the backup replica)
Replicated state machines (single core).

What state? : full memory/registers, not application level
P/B sync
Cut over anomolies
new replicas

VMware FT
Non-determenistic events:
- inputs from external sources (packets - packets - interruption)
- weird instructions 
- multicore parallelism
### [FT paper](https://pdos.csail.mit.edu/6.824/papers/vm-ft.pdf)
Virtual machine managed by hypervisor with all operations being virtualized.
Primary -> logging channel -> Backup

# Lecture 5: Go, Threads, and Raft


# Lecture 8: Zookeeper

Important concept is [Linearizability](https://en.wikipedia.org/wiki/Linearizability#Linearizability_versus_serializability)

## [Zookeeper (2010)](https://pdos.csail.mit.edu/6.824/papers/zookeeper.pdf)

Q1. How general purpose API for coordination service look like?
Q2. Does N of service increase performance?

No stong consistency, but
 - Linearizable writes: all requests that update the state
of ZooKeeper are serializable and respect precedence;
 - FIFO client order: all requests from a given client are
executed in the order that they were sent by the
client

Mimic of file system - Znodes:
 - regular
 - ephemeric
 - sequential file names

create(path, data, flags) -> Yes/No: exclusive creation, locking on file name
delete(path, version)
exists(path, watch) - atomic operation
get(path, watch)
setData(path, data, version)

Applications:
atomic transactions, locks, herd effect or non-scalable code.

# Lecture 9. Chain replication. CRAQ Chain Replication with Apportioned Queries
[paper](https://pdos.csail.mit.edu/6.824/papers/craq.pdf)
Topology over datacenters, write to the head, read from the tail, strong consistency guarantees.

dirty, clean commits

#Lecture 10: Cloud Replicated DB, Aurora

Database
pages, write-ahead-log (WAL)

Aurora has 3 Availability zones with 2 servers inside
 - replicated WAL
 - write with 1 AZ down
 - read with 1 AZ down + 1 server
 - fast re-replication

 quorum replication:
  - N replicas
  - W replicas to write
  - R read replicated

 W + R = N + 1 means readers & writers overlap at most 1 server
 example: S1, S2, S3, then w=r=2
 quorum relies on the highest version number


 Large databases are split into 10GB Protection groups. Each group has set up of 6 replicas in 3 Availability zones.

#Lecture 11: Cache Consistency: Frangipani


Frangipani clients --> Petal servers ---> lock server

1. cache coherence (historical version of linerazability)
2. atomocity
3. crash recovery

## Cache coherence
lineraziable in reads. LockServer, locks on the files, Statuses: busy, idle

Rules:
1. no cache data without lock. =>
 - before reading get the lock
 - update data on the petal servers before releasing lock.

Coherence protocol.
 - Request
 - Grant
 - Revoke
 - Release

## Atomicity
Transactions:
Acquire all the locks
	Do all the operations
Release

## Crash recovery
Write Ahead Logging
 - per-workstation logs, stored in petal not in local disk
