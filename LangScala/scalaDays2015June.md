# https://www.parleys.com/tutorial/5-minute-microservices
@Inject @checked
SignalCacheInvalid, postgres-bi-directional-replication, akka-cluster,
DataReplication() data structures, conductR

# https://www.parleys.com/tutorial/understanding-back-end-big-data
Containers: docker.
Orchestration: like https://github.com/spotify/helios
Resource management: like Apahce Mesos or YARN. Mesos need scheduler,
the one of prominent ones is Marathon.
Or Apache Myriad (incubator) on Yarn.

DCOS - the Datacenter Operation system.

Apps:          Docker\cgroups; node.js; RoR; Java; Redis; MySql
orchestration: Kubernetes; Marathon; Chronos; Spark; HDFS; C; Kafka
DCOS kerner:   Apache Mesos
machines:      nodes, virtual machines

# https://www.parleys.com/tutorial/ensime-why-would-anybody-build-another-scala-ide
shippable.com for CI

Greenspun's tenth rule
"Any sufficiently complicated C or Fortran program contains an ad hoc, informally-specified, bug-ridden, slow implementation of half of Common Lisp."

Shapeless Co-Product to implementing toJson

# https://www.parleys.com/tutorial/state-meta-summer-2015
scala.meta relies on tokens.\
Context.

# https://www.parleys.com/tutorial/building-your-first-rest-api-less-than-30-minutes
https://github.com/kevinswiber/siren - hypermedia object spec
or HAL - hypermedia object spec
swagger.io - for documentation.

# https://www.parleys.com/tutorial/the-future-ai-scala-jvm
Deeplearning4j
no parallel ML
 - HPC
 - Distbelief - partitioning over data

# https://www.parleys.com/tutorial/essential-scala-six-core-principles-learning-scala-1
Essential Scala: Six Core Principles for Learning Scala
1. Expressions, types, & values
2. Objects and classes
3. Algebraic data types
4. Structural recursion
5. Sequencing computation (fold, map, flatMap)
6. Type classes http://stackoverflow.com/questions/5408861/what-are-type-classes-in-scala-useful-for

4. - ADT. Model your data in terms of OR(sum type) and AND(product type). User is logged OR
   anononmyous. Logged user has id AND email

product type A has B AND C: `final case class A(b: B, c: C)`
sum type A has B or C: `sealed trait A; final case class B() extends
A; final case class C() extends A;`

Use structural recursion on ADT: pattern matching (match cases in
trait A) or (define abstract method in A; implement in each case
class)

5. fold : A => B is used with ADT. (futures, infinite streams are not ADT)

# https://www.parleys.com/tutorial/from-source-scala-twitter
 - MonoRep
 - Being stateless wins. They dont use actors.

# https://www.parleys.com/tutorial/making-your-scala-applications-smaller-faster-dotty-linker
 - Specialized versions of functions for type parameters. Call graphs.

# https://www.parleys.com/tutorial/functional-data-validation-how-think-functionally
type Rule[A] = A => Result
case class ~[A+, B+] (a: A, b: B)
Applicative builder.
https://github.com/davegurnell/functional-data-validation
https://github.com/davegurnell/validation

# https://www.parleys.com/tutorial/meerkat-parsers-general-parser-combinator-library-real-programming-languages
BNF-like notation vs Combinator
left-recursion is nonterminal. there are ways to overcome it.
Backtracking schemas are problematic. Local backtracking (PEG).
Deterministic parser is formula-1 car;
General parser is a jeep.
Order precedence. Lexing and Parsing.
 - Disambiguation filters
 - General parser
 - Combinator parser

# https://www.parleys.com/tutorial/types-vs-tests-an-epic-battle
Type signature is a Theorem and function definition is the proof
*Types*
 - reduce bugs
 - make code run faster
 - define interfaces
 - Check compilation
 - document model

*Model*
The main feature is to throw this model away.

Easy way and lazy street.
Types = For All
Tests = There exists

# https://www.parleys.com/tutorial/the-twelve-factor-app-best-practices-scala-deployment

sbt-native-packager -> sbt stage

1. Codebase.
 1. version for every package
 2. git submodule
2. Dependencies in local file - vendoring. 
3. Configure. Litmus test (can you opensource code without
   compromising any credentials).
 1. Configuration should be stored in the environment. And you can
    extract information in `conf/application.conf` from ENV.
4. Build, release and run.
5. Process.
 1. Processes should be stateless
6. Port binding.

# https://www.parleys.com/tutorial/so-how-do-i-do-2-phase-commit-akka
Reactive Manifesto. typesafe boring talk.

# https://www.parleys.com/tutorial/graphx-graph-analytics-insights-about-developer-communities
spark summit, spark certification.

# https://www.parleys.com/tutorial/almost-zen-reflections-four-years-scala-practice
Codegen. Swagger, Spray Spec.
Scalacheck: http://www.youtube.com/watch?v=lgyGFG6hBa0

# https://www.parleys.com/tutorial/hiring-onboarding-your-scala-team
If you want go fast, go alone.
If you want go far, go together.
Dog is fine:
https://whilstibloom.files.wordpress.com/2014/12/fine-dog-fine.jpg?w=620
 - Enforce style guidelines
 - Enforce compiler warnings
 - Make failing tests critical
 - Use testing frameworks
 - Have real time statistics
 - Profile regularly

Raise the bus factor (one teammember is hitten by the bus).
Multiple hats.

# https://www.parleys.com/tutorial/life-beyond-illusion-present
Jonas Bonér
 - "Time is a device that was invented to keep everything from hapenning
at once." - Graffiti on a wall at Cambridge university
 - "The future is a function of the past"
 - confirm, wait and repeat protocol in real life.
 - memories, guesses and apologies
 - time is a seria of facts. fact is a piece of information
 - functional programming
 - logic programming
 - dataflow programming
 - CR*UD* is dead, no update and deletes.
 - aggregate root. you can't touch my guys behind me, you should get
   through me.
 - eventual consistency.
 - conflicted-free replicated data types.

# https://www.parleys.com/tutorial/a-purely-functional-approach-building-large-applications
kleisli

shapeless-scala-check

#https://www.parleys.com/tutorial/the-reactive-streams-implementation-landscape

Flow chart.
