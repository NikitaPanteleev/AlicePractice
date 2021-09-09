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

```
/tmp/kafka-logs
*.log
*.index
```
Each topic has 1 or more partitions. Each partition fit on
machine. Partitions managed difference messages

# White paper
http://notes.stephenholiday.com/Kafka.pdf
## Intro & related work
Issues with other systems:
 - most of them guarantee delivery: leads to complexity and performance issues
 - not focusing on throughput (no batch api)
 - no distributed support

## Kafka Architecture and Design Principles
Messages, topic, brokers.
### Efficiency on a single partition.
