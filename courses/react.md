# Week 1
 - event-drive
 - scalable
 - resilent (react to failures)
 - responsive (react to users)

Common model: Java observer\event handler - listener is added to
resourse and it's function is called every time the event happens.
Mutable state, cannot be composed, call-back hell.

## Generators
```
trait Generator[+T] = {
  self => //an alias for "this"
  ...
}
```

## Monads
M is a parametric type M[T] with two operations flatMap and unit that
have to satisfy some lows:
```
trait M[T] {
  def flatMap(f: T => M[U]): M[U]

}

def unit[T](x: T): M[T]
```
*Lows*
 - Associativity
   m flatMap f flatMap g = m flatMap (f flatMap g)
 - Left Unit
  unit(x) flatMap f = f(x)
 - Right Unit
  m flatMap unit(x) = m

*Try* (not a monad(left unit fails on Failuer case)  but pretty close)

# Week 2
 - Stateful objects (ability to change results depending on time)

*The observer pattern*:
 - publish/subscribe
 - model/view/controller

trait Publisher {} - contains var subscribers: List and method
publish which can be called in every subscriber. publish simply call
handler method on every subscriber

Goods
 - decouples views from state
 - allows to have a varying number of views of a given state
 - simple to set up
Bads
 - imperative style, since handlers returns Unit
 - many moving that need to be coordinate
 - concurrency makes things complicated
 - views are still tightly bound to one state.

*Functional Reactive programming*
