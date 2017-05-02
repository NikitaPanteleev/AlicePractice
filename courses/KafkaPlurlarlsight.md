# Intro
Challenges, invented in Linkedin.

*distributed system* - consist of multiple broker-nodes
Controller election - elected broker.

In order to prevent losses, controller assign leader nodes per task,
leaders assign peers (number of peers = replication factor).

Distributed consensus using zookeeper.

The offset:
- placeholder for last read message
- maintained by kafka-consumer
- corresponds to message identifier

/tmp/kafka-logs
*.log
*.index

Each topic has 1 or more partitions. Each partition fit on
machine. Partitions managed difference messages
