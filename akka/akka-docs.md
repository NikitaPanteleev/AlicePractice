# 1. Getting started.
Nothing interesting...
# 2. General
 - Concurrency vs Parallelism
   = mixed execution vs simultaneous one
 - Asynchronous vs Synchronous
   = a very CPU intensive task might give a similar behavior as blocking
 - Nonblocking vs Blocking
 - Deadlock vs Starvation vs Live-lock
  starvation - some participants can not make progress (a simple
  schedular that choose only high-priority tasks and there are enough
  of them => low-priority never executes)

### Race condition
 - an assumption that an order of events might be violated by external
   effects. Akka guarantee for a given pair of actors that messages
   sent between them are preserved in their order.

### Non-blocking
 - wait-freedom = every call guarantees to finish in the finite number
   of steps
 - lock-freedom = some calls finishes. do not prevent from starvation
 - obstruction-free = after some time the call is executed in
   isolation. the weakest property
 - Optimistic Concurrency Control. if participant detects some
   conflicts it rolls back the modifications and try again according
   to some schedule.

## Books
-  The Art of Multiprocessor Programming, M. Herlihy and N
   Shavit, 2008. ISBN 978-0123705914
-  Java Concurrency in Practice, B. Goetz, T. Peierls, J. Bloch, J. Bowbeer, D. Holmes and D. Lea, 2006.
ISBN 978-0321349606
   
### 2.2 Actor System.
 Supervision
 - manager supervises the child
 - if one actor carries imporant data, it should source and possible
   dangerous tasks to children - "Error kernel Pattern"
 - watch the other actor you depend on

Building blocks:
 - Actor reference
 - State
 - Behavior
   function can be changed by become\unbecome operations
 - Mailbox. Default is FIFO, but the engueue may be changed and
   messages can be put in different order.
 - Children
 - Supervisor Strategy
 - When an actor terminates - all letters are redirected as DeadLetter
   to EventStream.
   
### 2.4 Supervision and monitoring
 Top-level supervisors
 /, /user, /system
 - /user, `system.actorOf()` - are children of this actor.
 - /system - is to keep logging when actors are terminating

Failure
 - programming error
 - failure of external resource
 - corrupt internal state of actor

Restarting

What Lifecycle Monitoring means.
 Watching Terminated messaged by `ActorContext.watch(targetActorRef)`
 Also delayed restarts with the BackoffSupervisor pattern

*One-for-one vs All-for-One Strategy*
oneForOne applyes directive only to failed child not to all children

# 3. Actors
###defining the actor
```
class MyActor extends Actor {
  def receive: PartialFunction[Any, Unit] = ???
}
```
### Props
`val prop = Props(classOf[MyActor], args)`
recommended practice to put props in the companion object.
### Creating Actors with Props:
`val myActor: ActorRef = system.actorOf(Props[MyActor], "actorName")`
### Dependency Injection
another guideline. IndirectActorProducer.
### The Inbox
receive multiple replies and watch other actors' lifecycle.

### Actor api
Actor trait provides only `def receive` +
- self - ActorRef
- sender - of the last message
- supervisorStrategy
- context - actorOf, system, parent supervisor, supervisedChildren, lifecycle monitoring, hotswap behavior stack

ActorRef represents the current incarnation (path and UID) but ActorSelection + Identify message + resolveOne give the current incarnation.

- Lifecycle monitoring aka DeathWatch
- start, restart hooks
the content of mailbox is not affected by restart

### Send messages
- ! fire-and-forgot = tell
- ? ask
- forward message, original address/reference is maintained

### Receive messages
### become/unbecome
### Stash messages
### Killing actor
`actor ! Kill`
### Extending Actors using PartialFunction chainging orElse
### Initialization patterns
- initialization via constructor
- preStart()
- become() + messages (warning! - messages can be lost, user message can come first)

## 3.2 Akka Typed - experimental
Main differences: no sender() functionality - encode it in messages; no Actor trait -> moved to messages.

# 3.3 Fault-tolerance

# 3.4 Dispatchers
responsible for thread pools, maiboxes management

# 3.5 Mailboxes

# 3.6 Routing
Creation of the pool of actors

#  3.7 FSM - finite state machine
State x Event => Actions, State

# 3.8 Persistence
p 157


