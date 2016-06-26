[Twitter school](http://twitter.github.io/scala_school/)

##Basics
`$sbt console` - to run scala REPL

`val` is for immutable results

`var` is for mutable variables

**Functions:**
```
scala> def double(x: Int): Int = x + x
double: (x: Int)Int
```
Be careful: You can leave off parens on functions with no arguments.

```
scala> three
res3: Int = 3
``` 
This **will call** the functions

**Anonymous functions:**
```
scala> val double = (x: Int) => x*x
double: Int => Int = <function1>
```
Use {} as always:
```
scala> { i: Int =>
  println("hello world")
  i * 2
}
res0: (Int) => Int = <function1>
```

**Partial application**
use `_` in args list

**Currying**
```
scala> def multiply(m: Int)(n: Int): Int = m * n
multiply: (m: Int)(n: Int)Int
```
then `multiply(2) _`

You can also curry any function with multiple arguments with `(fun _).curried`

**Variable length arguments**
`def capitalizeAll(args: String*) ={...}` - like python :3
**Classes**
```
scala> class Calculator {
     |   val brand: String = "HP"
     |   def add(m: Int, n: Int): Int = m + n
     | }
defined class Calculator
```
val and def. No constructors, just case statements in val expressions.
**Functions vs methods**
```
scala> class C {
     | var acc = 0
     | def minc =  {acc+=1}
     | def finc =  {()=> acc+=1}
     | }
```
1)  def evaluates every time it gets called while val evaluates only once.
2)  function is a syntactic sugar to f.apply().
**Inheritance**
Subclassing via `extends` or type aliases:
Sometimes use `type SocketFactory = SocketAddress => Socket` instead of `trait SocketFactory extends (SocketAddress => Socket)`
**Abstract Classes**
**Traits**
traits are collections of fields and behaviors that you can extend or mixin to your classes. `class BMW extends Car with Shiny`
**Types**

##Basics2
**Apply**
**Objects**
**Functions are objects**
A Function is a set of traits. Specifically, a function that takes one argument is an instance of a Function1 trait. 
This trait defines the apply() syntactic sugar we learned earlier, allowing you to call an object like you would a function.
**Packages**
Values and functions cannot be outside of a class or object. Objects are a useful tool for organizing static functions.
**Pattern Matching**
```
times match {
  case i if i == 1 => "one"
  case i if i == 2 => "two"
  case _ => "some other number"
}
```
**Case Classes**
Classes especially for pattern matching

##Collections
Basic Data Structures

+ Lists
+ Sets
+ Tuple
+ Maps
+ Option

Functional Combinators
+ map
+ foreach
+ filter
+ zip
+ partition
+ find
+ drop and dropWhile
+ foldRight and foldLeft
+ flatten
+ flatMap
+ Generalized functional combinators
Map?
```
val extensions = Map("steve" -> 100, "bob" -> 101, "joe" -> 201)
extensions.filter({case (name, extension) => extension < 200})
```
##Pattern Matching and functional composition
**Partial functions**
`scala> val one: PartialFunction[Int, String] = { case 1 => "one" }`
compose, andThen, composition and orElse

##Type & polymorphism basics
