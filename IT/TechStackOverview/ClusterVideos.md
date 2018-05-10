#code.talks 2017 - Real-Time Databases Explained: Why Meteor, RethinkDB, Parse & Firebase Don't Scale
https://www.youtube.com/watch?v=HiQgQ88AdYo

##Traditional db - pull approach.

PushBased approach:

##meteor = js+mongoDb
10 seconds update between nodes
Oplog tailing
Mongo cluster - Write operation goes to the only one primary node, and then it broadcased to all secondary nodes.
App node subscribed as secondary node.
Doesn't scale, load from mongoDB is too high.

##RethinkDB
Doesn't scale, proxy servers read all updates.
Parse - the same problem.

## Other options.
Streams/ephermal persistent: pipelineDb, esperTech, sqlStream, influxData,

streams: storm, flink, spark
