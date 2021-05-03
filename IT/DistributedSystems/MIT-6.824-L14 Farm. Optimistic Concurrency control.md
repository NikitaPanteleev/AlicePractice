FaRM - fast remote memory
#Performance:
 - sharding
 - data fit in RAM
 - Non volatile RAM
 - RDMA (clever interface )
 - kernel bypass

# Non volatile RAM
- battery near machine for 10 minutes

# Network
CPU spends a lot of time in network operations
common RPC:
App -> socket buffer -> TCP -> NIC driver -> NIC(network interface card) -> another machine
10GIB/s

# Kernel bypass - 
https://github.com/DPDK/dpdk
DPDK framework
App -> NIC direct communication

# Remote Direct memory access (RDMA)
Set up for local network using switch.

One sided RDMA:
source: App -> special message -> RDMA NIC
destination RDMA NIC -> access to App message

10 million read/write
lattency 5 microseconds

# Optimistic concurrency control (OCC)
How to get transaciton
- pessimistic
2 phase locking
- optimistic
read without locking
buffer writes
commit -> validation stage
conflict -> abort

# FARM API
```
txCreate()
o = txRead(OID) - read remote data
o.f += 1
txWrite(OID, O) - only locally modify the buffer
ok = txCommit()
```

Server memory
Region
Log | version + other computers locks
