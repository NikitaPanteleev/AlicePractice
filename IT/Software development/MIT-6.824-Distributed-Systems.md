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
