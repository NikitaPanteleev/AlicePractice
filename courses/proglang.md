sat, 3rd jan
10:17
========================================================================
#Week 6: Rucket data structures.
========================================================================

##Environment
Environment is mapping from variables to values.

##Struct
`(struct foo (bar quiz name3) #: transparent)`

It provides:
struct e, struct? e, struct-bar e

`#:transparent` - print values of struct in REPL
`#:mutable`


##Struct vs list approach
`(struct add (e1 e2))`
vs
`(define (add e1 e2) (list 'add e1 e2))`

Call of struct returns the result of new kind of primitive data. Not a list. And list approach is too error-prone.
There is no abstract data types but module system + contract system (allows invariant)

Structs are special:
- function cannot introduce multiple bindings
- neither functions nor macros can create a new kind of data
  the key feature is that you can ask `number?`, `new_data_type?`
  
##Implementing workflow
string -> parsing -> error
            |
   abstract syntax tree -> type checking
   
Interpreter for A in another language B (Evaluator)
Compiler in another language B to a third language C. (Translator)
A is metalanguage.

###legal AST
We implement language B as a subset of all trees (legal AST) that language A can handle.
###Result of interpreter is a values:
Values is an expression which evalueates to itself.

##Implementing closures
High-order functions. Body used the scope where it was defined and arguments are passed from the current environment.
`(struct closure (env func))` - store the environemnt + func
Are closures efficient? - Not store the whole environments but the only variables that could be used in function body
(free variables - not bounded yet)
Computing free variables is done in pre-compiling time. In language with no closures convert environment to additional
arguments.

##Using macros to implement language
It's ok because macros extends before interpreter and Racket has no Hygiene issues (ok with local variables inside macros).

##ML vs Racket
ML from Racket perspective is a subset of Racket which rejects some programs. And you don't need number? coz it's already
type checked.
Racket from ML perspective. Everything in Racket is just of one "big data type". Except for structs.

##What is static checking?
The step after parsing expression and before runs the program. And it catches some errors.
##Soundness and completeness
Accept program and prevent to do some X.
Sound - no false positive - never accepts the program which will do X.
Complete - no falst negative
Usually type systems are sound but not complete.
There is theorem that type checked cant satisfy all the 3 assumptions:
1) Always terminate.
2) Sound.
3) Complete.

##Weak typing(c/c++)
There exist program that by definition must pass static checking but then when run can set "computer on fire".
Java, python, ML.. do some dynamic checking to prevent mistakes.

Why weak typing?
- easier to implement language
- performance: faster
- lower level: compile doesn't insert information like array sizes
Array bounds is the most known example

##Static vs Dynamic
Dynamic: is more convinient for [1, "hi"] ... then pattern matching
Static:  is more convinient to be sure the data you recieve is of the right type.

Dynamic: static prevents usefull programs.
Static: well, use combined data types. Tag your data.

Static prevents some bugs vs static prevents only easy bugs.

Static: static programs are faster.
Dynamic: it's just small portion of program that matters and can be optimized.

Dynamic: code reuse is easier
Static: modern system supports enough code to reuse. + static libraries help avoid misuse.

Dynamic: is better for prototyping.
Static: use | _ => raise Unimplemented

Dynamic: better for evolution
Static:  when i change something - compiler gives me todo list.

##Eval and quote
quoting concrete syntax
quasiquoting in python,ruby ... - get string.
Treat data as program and run it.
======================================================================

#Week 7: Ruby

##Introduction ruby. 
- pure object-oriented
- class-bases
-- mixin (like Java interface)
- dynamically typed
- convenient reflection
- very dynamic
- blocks and idioms
- scripting language

##Classes and objects
1) all valueas are references to objects
2) object communicates via method call or message
3) each object has it's private state
4) each object has class
5) object's class determines the object's behavior

```
class A
    def m1 (x,y)
        42 *x + y
    end
end

a = A.new
```
new line matters, indentation doesn't matter.

##Object state
State consists of instance variables (also known as fields).
@foo - assignment just "springs into being"

Variable assignment x=y - aliasing.

def initialize - special method is called when object is created.

Class variables - @@foo - shared by every instance of class.
Class constants - 
Class methods   - static (C.method_name() - apply to class not instance)

##Visibility
Every state is private:
Getter\setter to access outside the scope.
`def foo
  @foo
end`
and cute sugar
`def foo= x
    @foo=x
 end`

Methods visibility: private, public, protected.
`class Foo
  #public methods
  protected
  ...
  public
  ...
  private
  ...
end`
for private methods instead of self.m use just m.

##Class definitions are dynamic
you can change\add class method and all instances(even defined previously) will also have this method.
##Duck Typing
##Arrays
a.pop \ a.push - like stack
a.shift \ a.push - like queue
a.unshift - put element in the front of the line
d = a -aliasing
d = a +[] - returns new array

##Blocks
blocks are almost as closures
`[4,6,8].each {|x| puts x}`
Can pass 0 or 1 block with any message.
`{|x,y| exp}` or `do |x,y| exp end`
`a.inject(0) {|acc,elt| acc+elt}`
`a.inject {}` - use first element as accamulator
select = filter

##Using Blocks
`def silly a
  (yield a) + (yield 42)
end`
- using blocks in function body with args (a or 42 in example)
`block_given?`

##Procs
Blocks are second-class expression.
Procs are first-class: you can return it, store it, call it.
lambda takes Block and return Proc.
Procs are called with `a.call 17`
##Hashes and ranges
##Subclasses
class ColorPoint < Point --every object has superclass.
Point < Object < BasicObject < nil
superclass
cp = ColorPoint.new
cp.is_a? Point -> true (in Java instanceof)
cp.is_instance_of? Point -> false

You can use proxy class instead of sublclass, but it's not common technique.

##Overriding and Dynamic Dispatch
So far objects are not really different from closures:
- Multiple methods rather than just one 'call me'
- Explicit instance variables rather than environment where function is defined
- Inheritance avoids helper functions or code copying
- "simple" overriding just replaces methods

One big essential difference:
- overriding can make a method define in the superclass
   call a method in the subclass
   
##Methods lookups rules
Dynamic dispatch - late binding or virtual methods
call self.m2() can resolve to method m2 in a subclass.
The whole story is about self is pointing to current class.

dynamic dispatch - Ruby\Java 
vs 
static overloading - C\C++ - (rules for choosing the method with the same name and the same number of arguments)

##Dynamic Dispatch vs closures
closures are 'closed' after definition, you can't change environent. And dispatch can override methods.

===================================================================================
#Week 8: OOP versus Functional Dispatching.

Variants and operations over them.
Functional:
one datatype with one constructor
one function with case expression.
OOP:
Datatypes are subclasses
Functions are methods.

##Extension
if you add new function: in OOP  - add to every class method
                         in Func - add just one new function
if you add new datatype: in OOP  - just add new class
                         in Func - add case to every function
                         
tradeoffs: funcs hide some functions in modules system and Java's final prevents subclassing\overriding

##Binary Methods with Functional Decomposition
Extend language to work with pairs. very natural in func (recursive call for communicate cases (in math sense a+b=b+a)
Double dispatch: call v method and tell him who we are = who calls him.
##Multimethods
The same methods with different class args, downside is sometimes "no clean winner". Java\c\c++ allows static overloading
- methods are distinguished in compile time not in runtime.
##Multiple inheritance
- multiple inheritance > 1 superclass (c++ with 2 ways of inheritance)
- mixins 1 superclass; > 1 method providers (ruby mixins, scala traits)
- java\c# interfaces: allow > 1 types
a lot of problems such as the same fields, methods in parent classesand which one to choose

##Mixins
mixin is just a collection of methods (like interfaces; can use self)
`module Doubler
  def double
    self + self
  end
end`

`class String
  include Doubler
end`
lookup rules: object, mixin, then superclass, then superclass mixin...
poor style to use instance variables
include Comparable: >, <=, !=... defined just by <=> 'spaceship' operator.
include Enumerable: defines many iterators in terms of `each`

##Interfaces (java\c#)
In statically typed language: interface is a type but not a class. Dynamic typing is more flexible then Java with interfaces.
##Abstract Methods (java\c#)
(pure virtual in c++)
C++ has pure virtual methods and multiple inheritance instead of interfaces.
Just help to reader and compiler but doesn't make language powerfull.
##Subtyping from the begining.
{f1=e1, f2=e2, f3=e3} has type {f1:t1, f2:t2, f3:t3}
e.f - access
e.f=e2
##The subtype relation
t1 <: t2 for subtype t1. That means if e has type of t1, it also has subtype of t2.
Four rules for subtype system:
1) A supertype can have subset of fields with the same types. "Width"
2) A supertype can have fields in different order. "Permutation"
3) Transitivity. If t1 <: t2 and t2 <: t3 then t1 <: t3
4) Reflexivity: every type is a subset of itself.
##Depth subtyping
depth subtyping: if ta <: tb, then  {f1:t1, f2:t2, ... f:ta,.. fn::tn} <: {f1:t1,..f:tb,..fn:tn} - THIS BREAKS SOUNDNESS!
with language with mutable fields.

In language with immutable fields then depth subtyping is ok.
Choose two of three: setters, depth subtyping, soundness.

##Java\c# arrays.
t1 <: t2, then t1[] <: t2[] but should not!
+ null is like the superobject

##Function subtyping
function with t1 -> t4
              \/    /\          
can take      t2 -> t3
t1->t4 <: t2->t3
function can return more t4 <: t3. return types are covariant.
function need all the fields, but you can provide more then you pass a child. Contravariant.

##Subtyping for OOP
in Java\c# class names are also types.
Methods are immutable.
Classes vs. Types
class describes object's behavior
type describes object's methods type arguments\return types
Java\c# confuses class and type.

Example: you can have two fields the same name but different types in class and superclass. There will be 2 fields, and you will
point in superclass to one, and in child to the another.

Self\this is special! It's covariant argument.

##Generics versus subtyping.
Generics in ML `val length: 'a list -> list`
Subtyping (polymorphism) is not good for smthing like swap() 
##Bounded polymorphism
combine generics and subtyping "only type t1 that is subtype of t2"