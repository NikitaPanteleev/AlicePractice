
# Typeclasses.

It could be nice to define business logic as traits + case classes (as Algebraic Data Types), define transformations in separate traits and mix them with type classes.


# LambdaConf 2015 - Cats — A Fresh Look at Functional Programming in Scala Mike Stew O'Connor
https://www.youtube.com/watch?v=hIwdaP3-U6I&list=PLE7tQUdRKcybh21_zOg8_y4f2oMKDHpUS&index=34

missing types:
- Writer
- RWSM
- Task - computation with side effect returns future
- Process
- Tags

out of scope
- Ilist better coz not .head and it's invariant
- Maybe
-  ==>>
- FingerTree
- Dequeue

Dead ideas
- left biased xor
- shared sun type


Structure
- core: type classes, data types
- std: type class instances for scala
- laws: property based testing for typeclass instances
- docs: compiler verified documentation and examples
- free: free monad, free applicative
- state: (state monad)

Another nice projects
- Discipline allows law transformation
- Simulacrum - eleminates boilerplate when working with type classes
- tut compiles markdown /tpolecat/tut
- sbt-site
- sbt-ghpages
