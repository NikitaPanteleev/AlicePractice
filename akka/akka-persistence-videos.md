#Intro to Akka persistence with Patrik Nordwall
 - recover application state after a crash
 - opt-in at-least-once delivery semantics

from akka 2.3.0

Domain events - store the transition, not the state itself.
 - things that have complete, facts
 - immutable
 - verbs in past tense
   - CustomerRelocated
   - ShipOrdered

Benefits.
 - bullet-proof auditing and historical tracing
 - support future ways of looking at data
 - perfomance and scalability
 - testability
 - reconstruct production scenarios
 - no object-relational impedance mismatch
 - nice fit with actors

|Command Sourcing | Event Sourcing|
|- write-ahead-log - incoming commands are the things you store|
|-- derive events from a command|
|-same behavior during recovery as normal operation
|-- only state changing behavior during recovery
|- persisted before validation
|-- events cannot fail
|- allows retroactive changes to the businesss logic
|-- fixing the business logic will not affect persisted events
|- naming: represent intent, imperative
|-- naming: things that have completed, verbs in past tense

Consistence boundary
 - an actor is a consistency boundary
 - Domain Driven Design Aggregate
 - No distributed transactions
   - eventually consistent
   - compensating actions

Building blocks

akka.persistence.Processor - actor which stores the message after it
receives.

it has invoices: `Map[A, B]`

Processor
- automatic recovery on start and restart
- stashing until recovery completed
- failure handling with supervisor strategy
- might want to delete erroneous messages

What about side effects during recovery? - processor with Channel

EventSourcedProcessor
- incoming commands are not stores
- steps
  1. validate command
  2. create domain event and explicitly persist it
  3. update internal state, by applying the event.
  4. external side effects

```
def receiveCommand: Receive = ???
def receiveRecover: Receive = ???
```

Snapshots

View
 - read from journal
 - query side of CQRS(command-query-responsibility-segregation) 

PersistedChannel - allows at-least-one delivery

sender -> $$ -> destination
sender <- ok <- destination
recommendation: one destination per channel

Serialization
 - pluggable, akka serialization
 - application life-cycle, versioning
 - dont use default Java serialization

#Event-Sourced Architectures with Akka

Actor is "an island of consistency in a sea of concurrency".
mailbox, state, behavior.
mailbox is non-durable. state is also transient.

commands -> PersistencActor
      ||
      \/
derive events => save events in journal => do some side effects 
"The database is a cache of a subset of the log"
