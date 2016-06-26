@renatocaval
github.com/rcavalcanti
github.com/strongtyped

# DDD and CQRS
Command and Query Responsibility aggregation

*Aggregate* is a central DDD concept
It has a root and zero or more entities underneath
- Responsible for consistency of underneath objects
- You can only modify one aggregate per transaction.

Example: Order = initial order for customer + operations.
CQRS - segregation of commands and analytics.
- Write model receives commands and produces Events (CQRS)
Event sourcing is saving the events.

Async CQRS:
tx=transaction
tx(command => write model => event)
tx(event => view1)
tx(event => view2)
it leads to eventual consistency

- Strict consistency on Write Model side

# Akka basics
`type Receive = PartialFunction[Any, Unit]` - playing around that with Typed Protocol where types are bounded inside the traits using type parameter.

```
trait Aggregate {
 type Protocol <: ProtocolDef
}
```

# Reactive fashion
`def validate(cmd: DomainCommand): Future[Seq[DomainEvent]]` - it can go somewhere to check
`def applyEvent(event: DomainEvent): Aggregate` - without futures because we need the exact order

Lifting it... magnet pattern

#Coding the Q in CQRS
- Akka Persistence Query (experimental in akka 2.4.0)
- Generate Read Models (Views) from the Events
- Akka Streams Source with Selected Events
- ProjectionActor to consume the source and save the pointer (offset) to the last processed event

You need to identify system errors (database is down, for example) - retry in 2 mins - and programming errors - skip this event.

## Akka for CQRS
- Given an Aggregate, its Protocol and its Behavior...
- ... we can have an AggregateActor that understands the life-cycle of an Aggregate
- Events are stored and replayed via Akka Persistence
- one Actor per Aggreagate id
- Actor MUST handle one single Command at time (become\unbecome)
- Guarantees consistency withou Optimistic Locking
- Projections backed by Akka Persistence Query

postres can process 10,000 events per secons
