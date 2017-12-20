#Lambda Days 2015 - Manuel Bernhardt - Scala, Akka, Play: The Why and How of reactive web-applications on the JVM

https://vimeo.com/125440021
95% of syncronized code is broken. The other 5% is written by Brian
Goetz. - Venkat Subramaniam at #s2gx
## Whys
 - many-core CPUs are here
 - everything is distributed
 - IoT around the corner
 - our traditional approach doesn't work here.

## How
 - Functional programming => Scala
 - The Actor model => Akka
 - Evented Server model (vs. thread server model) => Play
 - Stateless architecture => Play
 - Event Sourcing => Akka Persistence
 - Reactive streams => Akka Streams

23:47
2010 Akka
 - lightweight object
 - send and recieve messages
 - can have children (supervision)
20012 Play 2
 - everything is compiled
 - non-blocking I/O
 - controller actions are functions (request => response)
 - share nothing => horizontal scalability

waiters in restaurant

