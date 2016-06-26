#Chapter 1.  Strings
1.1 Equality: `s1 == s2`. == checks first for null values, then go to
equals method in this class. `a.equalsIgnoreCase(b)`
1.2 Multiline: `""" ...|... """.stripMargin`
1.3 Splitting: `"hi,bro".split(",")`
1.4 Substituting variables into String: String interpolation.
```
scala> println(f"$name is $age years old, and weighs $weight%.2f pounds.")
Fred is 33 years old, and weighs 200.00 pounds.
scala> raw"foo\nbar"
res1: String = foo\nbar
```
1.5 Processing a string one character at time.
1.6 Finding patterns in String. Create `"[0-9]+".r` pattern and use
`findFirstIn`.
1.7 Replace patterns. `replaceAll`
1.8. Extracting Parts of a String That Match Patterns
`val pattern = "([0-9]+) ([A-Za-z]+)".r` and
`val pattern(count, fruit) = "100 Bananas"`
1.9. Accessing a Character in a String
`"hello"(1)`
1.10. Add Your Own Methods to the String Class
Implicits are allowed in class, object or package object.

#Chapter 2. Numbers (p.31)
2.1. Parsing a Number from a String
`.toInt, .toDouble`
```
scala> Integer.parseInt("10", 2)
res1: Int = 2
```
2.2. Converting Between Numeric Types (Casting)
`.toInt, .toDouble` + `.isValid[Short, Byte, Int]`
2.3. Overriding the Default Numeric Type
According to ScalaGuide this is preferred:
```
scala> val a = 0: Float
a: Float = 0.0
```
but I use `val a: Float = 0`.

*NB* Upcasting:
```
scala> val s = "Dave"
s: String = Dave
scala> val p = s: Object
p: Object = Dave
```
2.4. Replacements for ++ and −−
`var i += 1`
2.5. Comparing Floating-Point Numbers
```
scala> 0.1 + 0.2
res10: Double = 0.30000000000000004
```
Writing comparasion ~= with precision
2.6. Handling Very Large Numbers
`BigInt`
2.7. Generating Random Numbers
```
scala> val r = scala.util.Random
r: scala.util.Random = scala.util.Random@13eb41e5
scala> r.nextInt
res0: Int = −1323477914
```
2.8. Creating a Range, List, or Array of Numbers
`1 to 10 by 2`. And some arguments to not use infix notation anywhere
except for internal DSL.
2.9. Formatting Numbers and Currency
with locale:
```
scala> val locale = new java.util.Locale("de", "DE")
locale: java.util.Locale = de_DE
scala> val formatter = java.text.NumberFormat.getIntegerInstance(locale)
formatter: java.text.NumberFormat = java.text.DecimalFormat@674dc
scala> formatter.format(1000000)
res2: String = 1.000.000
```
There is alsow Joda Money library.

#Chapter 3. Control Structures.

3.1 Iterating over collection
```
scala> val newArray = for (e <- a) yield {
    |// imagine this requires multiple lines
    |val s = e.toUpperCase
    |s
    | }
newArray: Array[java.lang.String] = Array(APPLE, BANANA, ORANGE)
```
Translation of for loop by compiler:
 - for loop is translated into foreach
 - for loop with guard is translated into withFilter + foreach
 - yield -> map
 - yield + guard -> withFilter + map

To investigate use `$ scalac -Xprint:parse Main.scala` or
`-Xprint:all`.
3.2. Using for Loops with Multiple Counters
`scala> for (i <- 1 to 2; j <- 1 to 2) println(s"i = $i, j = $j")`
3.3. Using a for Loop with Embedded if Statements (Guards)
3.4. Creating a for Comprehension (for/yield Combination)
3.5 Implementing break and continue
It’s true that Scala doesn’t have break and continue keywords, but it does offer similar
functionality through `scala.util.control.Breaks`. Use code inside
`breakable` and use `break`. Break throws exception which is handled
by breakable. Recursive functions in FP with @tailrec optimization.
3.6. Using the if Construct Like a Ternary Operator
3.7. Using a Match Expression Like a switch Statement
You can use @switch annotation in simple cases (matched value is a
known integer, available at compile time, no type checks..) of pattern
matching: it compiles to tableswitch or lookup switch instead of
decision trees.
3.8. Matching Multiple Conditions with One Case
Statement
`case 1 | 2 | 3 => ...`
3.9. Assigning the Result of a Match Expression to a
Variable
Match anything except for `case l: List[Int] => "List"` due to type
erasure. Also pattern annotation to access the variable: `case list @ List(1, _*) => s"$list"
`
3.12. Using Case Classes in Match Expressions
3.13. Adding if Expressions (Guards) to Case Statements
3.14. Using a Match Expression Instead of isInstanceOf
3.15. Working with a List in a Match Expression
3.16. Matching One or More Exceptions with try/catch
`@throws(classOf[NumberFormatException])` to interact with Java
3.17. Declaring a Variable Before Using It in a try/catch/
finally Block
`var in = None: Option[FileInputStream]`
3.18. Creating Your Own Control Structures

#Chapter 4. Classes and properties (p.99)
##4.1. Creating a Primary Constructor
getters\setters are automatically generated for var fields; everything
except for method definitions is executed during class initialization.
##4.2 Controlling the Visibility of Constructor Fields
` class Person(var name: String)` - or val generates getter\setter or
only getter
`class Person(val name: String)` - generates nothing, so p.name gets
error.
`case class Person(name: String)` - case classes fields are vals.
##4.3. Defining Auxiliary Constructors
`def this(..)` inside the class.
Or `def apply()` in Companion object for Case classes.
##4.4. Defining a Private Primary Constructor
` class Person private (name: String)` - so it could be accessable
only via Companion object. Companion object (object with the same name
in the same file) add all it's methods as static methods to class.
##4.5. Providing Default Values for Constructor Parameters
`class Socket (val timeout: Int = 10000)`
##4.6. Overriding Default Accessors and Mutators
Use another variable `private var _name` and write getter\setter:
```
def name = _name
def name_=(aName: String) { _name = aName } // mutator
```
##4.7. Preventing Getter and Setter Methods from Being
Generated
Define the field with the
 - private = available only from all instances
of the same class
 -  private[this] - available only in this object
##4.8. Assigning a Field to a Block or Function
do it + maybe make the field lazy.
##4.9. Setting Uninitialized var Field Types
Define field is an Option.
##4.10. Handling Constructor Parameters When Extending a
Class
Declare your base class as usual with val or var constructor parameters. When defining
a subclass constructor, leave the val or var declaration off of the fields that are common
to both classes.
##4.11. Calling a Superclass Constructor
You can control the superclass constructor that’s
called by the primary constructor in a subclass, but you can’t control the superclass
constructor that’s called by an auxiliary constructor in the
subclass. Just use what you want in extend NeededConstructor.
##4.12. When to Use an Abstract Class
 -  You want to create a base class that requires constructor arguments.
 -  The code will be called from Java code.
Leaving the body of the method undefined makes it abstract.
##4.13. Defining Properties in an Abstract Base Class (or
Trait)
Scala compiler doesn't generate values for abstract field - it creates
only method.
You may define a def that takes no parameters in the abstract base
class rather than defining a val. They can then define a val in the
concrete class, if desired. Use final to prevent overriding behaviour.
##4.14. Generating Boilerplate Code with Case Classes
case class generates apply(), accessor methods, default toString,
unnapply, equals and hashcode, copy
##4.15. Defining an equals Method (Object Equality)
##4.16. Creating Inner Classes
“Opposed to Java-like languages where such inner classes are
members of the enclosing class, in Scala, such inner classes are bound to the outer
object.”

# Chapter 5. Methods (p 147)
##5.1. Controlling Method Scope
 - object-private = `private[this]`
 - class-private = `private`
 - protected (in Java different behavior: protected methods can be
   accessed from other classes in the same package)
 - package scope = `private[package name]`
 - public
##5.2. Calling a Method on a Superclass
`super.doSmth` or `super[ChosenTrait].doSmth` - if there is more then
one method with this name. (by default - right closesest is chosen)
##5.3. Setting Default Values for Method Parameters
##5.4. Using Parameter Names When Calling a Method
##5.5. Defining a Method That Returns Multiple Items (Tuples)
##5.6. Forcing Callers to Leave Parentheses off Accessor Methods
Define your getter/accessor method without parentheses after the method name:
```
class Pizza {
  // no parentheses after crustSize
  def crustSize = 12
}
```
*Methods which act as accessors of any sort ... should be declared without parentheses,
except if they have side effects.*
##5.7. Creating Methods That Take Variable-Argument Fields
`def printAll(strings: String*)`
And pass any Sequence like this:
```
val fruits = List("apple", "banana", "cherry")
printAll(fruits: _*)
```
##5.8. Declaring That a Method Can Throw an Exception
```
@throws(classOf[Exception])
@throws(classOf[AnotherException])
override def play() = {}
```
##5.9. Supporting a Fluent Style of Programming (method chaining)
```
def setLastName(lastName: String): this.type = {
  lname = lastName
  this
}
```

#6 Objects
##6.1. Object Casting
`obj.isInstanceOf[AnotherObject]`
##6.2. The Scala Equivalent of Java’s .class
Use `classOf[YourClass]` to pass a type of YourClass.
##6.3. Determining the Class of an Object
`getClass`
##6.4. Launching an Application with an Object
`extends App` or implement main method
##6.5. Creating Singletons with object
##6.6. Creating Static Members with Companion Objects
##6.7. Putting Common Code in Package Objects
Put your code in package.scala in desired directory = package object
put it in .../model directory:
```
package com.alvinalexander.myapp
package object model {
```
##6.8. Creating Object Instances Without Using the new Keyword

Case class or companion object (possible to provide many apply
constructors).

##6.9. Implement the Factory Method in Scala with apply
In superClass Companion object apply's method return different types
depending on provided arguments.

#7 Packages and import
 - java.lang._
 - scala._
 - scala.Predef
##7.1. Packaging with the Curly Braces Style Notation
```
package com.acme.store {
  class Foo { override def toString = "I am com.acme.store.Foo" }
}
```
##7.2. Importing One or More Members
`import java.io.{File, IOException, FileNotFoundException}`
##7.3. Renaming Members on Import
`import java.util.{ArrayList => JavaList}`
##7.4. Hiding a Class During the Import Process
`import java.util.{Random => _, _}` - imports everything but `Random`
##7.5. Using Static Imports
`import java.lang.Math._`
##7.6. Using Import Statements Anywhere

#8 Traits.
##8.1. Using a Trait as an Interface
`val f = new Foo with Trait1` - mixin traits into class.
##8.2. Using Abstract and Concrete Fields in Traits
##8.3. Using a Trait Like an Abstract Class
##8.4. Using Traits as Simple Mixins
##8.5. Limiting Which Classes Can Use a Trait by Inheritance
inherite trait from class and class can't inherit from multiple
classes.
##8.6. Marking Traits So They Can Only Be Used by Subclasses of a
##Certain Type
```
trait MyTrait {
  this: BaseType =>
```
##8.7. Ensuring a Trait Can Only Be Added to a Type That Has a
##Specific Method
```
trait WarpCore {
  this: { def ejectWarpCore(password: String): Boolean } =>
}
```
It's known as structural type.
##8.8. Adding a Trait to an Object Instance
`val hulk = new DavidBanner with Angry`
##8.9. Extending a Java Interface Like a Trait
just use interfaces as traits.

#9 Functional Programming.
##9.1. Using Function Literals (Anonymous Functions)
##9.2. Using Functions as Variables
`val f = (i: Int) => { i % 2 == 0 }`
Or reassign as partially applied method: `val c = scala.math.cos(_)`
##9.3. Defining a Method That Accepts a Simple Function Parameter
##9.4. More Complex Functions
looks like OOP Strategy pattern.
##9.5. Using Closures
“In computer science, a closure (also lexical closure or function closure) is a function
together with a referencing environment for the non-local variables of that function. A
closure allows a function to access variables outside its immediate lexical scope.”
##9.6. Using Partially Applied Functions
`val f = sum(1, 2, _: Int)`
##9.7. Creating a Function That Returns a Function
##9.8. Creating Partial Functions
```
val divide2: PartialFunction[Int, Int] = {
  case d: Int if d != 0 => 42 / d
}
```
"A partial function of type PartialFunction[A, B] is a unary function where the domain
does not necessarily include all values of type A. The function `isDefinedAt` allows [you]
to test dynamically if a value is in the domain of the function." + 
`orElse and andThen`

#10 Collections
#11 List, Array, Set (and More)
#12 Files and Processes
#13 Actors and Concurrency
##13.1. Getting Started with a Simple Actor
`val helloActor = system.actorOf(Props[HelloActor], name = "helloactor")`
##13.2. Creating an Actor Whose Class Constructor Requires Arguments
`val helloActor = system.actorOf(Props(new HelloActor("Fred")), name =
"helloactor")`
##13.3. How to Communicate Between Actors
When an actor receives a message from another actor, it also receives an implicit ref‐
erence named `sender`.
##13.4. Understanding the Methods in the Akka Actor Lifecycle
• receive
• preStart
• postStop
• preRestart
• postRestart
##13.5. Starting an Actor
 - At the ActorSystem level you create actors by calling the `system.actorOf`.
 - Within an actor, you create a child actor by calling the `context.actorOf`.
##13.6. Stopping Actors
 - `system.stop(actorRef)` at the ActorSystem level or `context.stop(actorRef)` from
inside an actor. Actor processes current message and then stopped
 - `actor ! PoisonPill` - msg in the queue. actor stops when reads it
 - `actor ! gracefulStop` - waiting them to timeout. (when specific
   order is needed)

Actor terminates in 2 steps: suspend mailbox and sent stop messages
with waiting for responses. Then it terminates itself.

`actor ! Kill` - allows supervisor to restart actor.
##13.7. Shutting Down the Akka Actor System
`system.shutdown`
##13.8. Monitoring the Death of an Actor with watch
```
class Parent extends Actor {
// start Kenny as a child, then keep an eye on it
  val kenny = context.actorOf(Props[Kenny], name = "Kenny")
  context.watch(kenny)
  def receive = {
    case Terminated(kenny) => println("OMG, they killed Kenny")
    case _ => println("Parent received a message")
  }
}
```
Exception doesn't kill the actor, actor is restarted.

###Looking up for actor:
`val kenny = system.actorSelection("/user/Parent/Kenny")`
##13.9. Simple Concurrency with Futures
 - blocking with `Await.result(f, time)`
 - callback - onComplete, onFailure, onSuccess
 - Run in parallel, join together on completion:
```
val result: Future[T] = for {
r1 <- result1
r2 <- result2
r3 <- result3
} yield (r1 + r2 + r3)
```
ExecutionContext is like ThreadPool.
Callbacks methods: map, foreach... +  recover, recoverWith, and
fallbackTo + andThen
You can read result from future and *promise* it somewhere else.
##13.10. Sending a Message to an Actor and Waiting for a Reply
Use `?` method => causes blocking.
##13.11. Switching Between Different States with become
Use `become`.
##13.12. Using Parallel Collections




























    
