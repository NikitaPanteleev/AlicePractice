# Chapter 1 Introduction
React manifesto:
- responsive
- resilient
- elastic
- message driven

# Chapter 2 Akka.
## Implementing actors
/ - root guardian
|      \
/user   /system

Create actor directly: `val processManagersRef: ActorRef = system.actorOf(Props[ProcessManagers], "processManagers")`

tell: ! or `processManagersRef.tell(BrokerForLoan(banks), self)` - ! looks for implicit ActorRef
actorSelection: `val selection = system.actorSelection("/user/processManagers")`

preStart & postStop
preRestart & postRestart  - these normally are not overwritten

change resceive behaviour (State patten GoF)
```
override def preStart(): Unit {
  context.become(houseKeeper)
}
```

*Be Careful with sender()* - it's a function and depend on context where it's called

## Supervision
```
override val supervisorStrategy =
 OneForOneStrategy(
       maxNrOfRetries = 5,
       withinTimeRange = 1 minute) {
    case NullPointerException => Restart
...
}
```


## Remoting
peer-to-peer fashion
Keep in mind
- network lattency
- serialization overhead (protobuf or kryo)

Usage:
- Remote creating
Specify in application.conf deployment path for the actorName
- Remote lookup
path for remote actors: akka.tcp//hostname@akkaname:port/(remote/host@akka:port/...)

Due to lattency: need to know sender for id: `senderFor()`

actorSelection (path vs ref) and resolveOne(timeout)

selection ! Identify(searchPath)

## Clustering
- Cluster singleton - one actor of given type anywhere on the cluster
- Cluster sharding - actors are distributed evenly across all the cluster
- Cluster client - actors outside the cluster need to send messages inside cluster without knowing precise location
- Cluster-aware routes - distribute work across the nodes

Gossip protocol - all nodes send messages to all about health, leader
node identifire host:port:uid
seed nodes - nodes at startup, the first one in the list started before others.

heartbeat messages are maintained by another dispatcher in different thread.
### Joining the cluster
- config through defined seed nodes
- programmatically:
`Cluster(system).join(address)`
- manually, using JavaManagementExtension
### Cluster roles and events
roles: cluster {roles = [RoleName]}

`cluster.subscribe(self, classOf[MemeberEvent], classOf[UnreachableEvent])`

### Cluster singleton
`ClusterSingletonManager.props()`
Could be created twice in *Split-brain* condition, specify `min-nr-of-members` property to prevent a leadership
election until there is an established quorum of nodes.
### Cluster sharding
- memory
- node-actor affinity to use local dispatcher
- collect to one shard to store

Shard contains a number of entries (actors). Singleton ShardCoordinator talks with ShardRegion actors on each node
and track which regions have how many shards. When the message is send -> ShardRegion -> entry

### Cluster client
ClusterReceptionist - exists on every node, actors have to register as service in this list.
Contact points are registered on client side. `ClusterClient.Send` or send not by name but by topic to all
cluster subscribers with `ClusterClient.Publish`

### Cluster-Aware Routers
Routers exist in two forms in Akka:
- as groups - preexisting actors
- as pools - router can create new actors

Routes has configured path `routees.paths = ["/user/backendService"]`. Wrap messages in `ConsistentHashableEnvelope`,
so that route can distribute msgs my hash.
Pool is in one-to-many relations.

### Scaling with load.
- load-balancing routers (heap, cpu, load = cpu run query length)
`libraryDependencies += "org.fusesource" % "sigar" % "1.6.4" %classifier("native") classifier("")`

## Testing actors

```
import akka.testkit.TestActorRef

val riskManagerRef = TestActorRef[RiskManager]
val riskManager = actorRef.underlyingActor”
```

# Chapter 3. Performance Bent
- 64-bit instruction set (versus 32-bit processor in 2005)
- Four cores, with the capability to run eight threads simultaneously (versus one core, and possibly hyperthreading in 2005)
- 6MB CPU cache (versus perhaps 2MB in 2005)
CAP (consistency, availability, partition tolerance)

## Multithreading
- Deadlock
- Livelock
- Starvation
- Inefficient code
- False sharing = thread share different data in the same cache

## Actors help
- share nothing
- think reactively
- model with actors
- tell actors what to do
- actor system provides scheduling
- design for resilence

## False sharing
Each actor in the only one thread = no false sharing generally.
For hottest actors - compute their size that they occupy one single line of caching.

# Chapter 4. Messaging with Actors.
## Message channel (p128)
actor mailbox
## Message (p130)
## Pipes and filter (p135)
## Message router (p140)
## Data translation (p143)
## Message endpoints

# Chapter 5. Messaging channels.
- Point-to-Point Channel
  in akka-remoting actor creation is async, so one should be aware of that actor doesn't exist yet (request-reply contract)

- Publish-Subscribe Channel
-- Subscribe to Local Event Stream
```
system.eventStream.subscribe(
  sysListener,
  classOf[akka.actor.DeadLetter])
  ```

And publish there: `system.eventStream.publish(PriceQuoted(ticker, price))`
`class QuotesEventBus extends EventBus`

-- Distributed publish-subcribe
`DistributedPubSubMediator` - Send, sendToAll, publish(topic, message)
To subscribe one needs:
--- PubSubMediator.Put - to receive Send
--- DistributedPubSubMediator.Subscribe - to receive published messages
- Datatype Channel

- Invalid Message Channel
- Dead Letter Channel
- Guaranteed Delivery
- Channel Adapter
- Message Bridge
- Message Bus

