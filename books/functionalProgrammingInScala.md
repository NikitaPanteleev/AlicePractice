#PART 1: INTRODUCTION TO FUNCTIONAL PROGRAMMING
##1. What is functional programming?
*Referential transparency and purity*
An expression e is referentially transparent if for all programs p, all
occurrences of e in p can be replaced by the result of evaluating e,
without affecting the observable behavior of p. A function f is pure if the
expression f(x) is referentially transparent for all referentially
transparent x.1

This transformation can be repeated to push side
effects to the "outer layers" of the program. Functional programmers often speak of
implementing programs with a pure core and a thin layer on the outside that
handles effects.

##2. Getting Started.
 - REPL: :load fileName;
 - Tail Calls.
 - It is a common convention to use f, g, and h as parameter names for
functions passed to a HOF.
 - Parametric polymorphism  - `func[A,B](...) =  {...}`

*Boxed types and specialization in Scala*
A function that is polymorphic in some type is generally forced to
represent values of these types as boxed, or non-primitive values,
meaning they are stored as a pointer to a value on the heap. It is
possible to instruct the Scala compiler to produce specialized versions
of a function for each of the primitive types, just by adding an annotation
to that type parameter:
`def binarySearch[@specialized A](as: Array[A], key: A, gt: (A,A) =>
Boolean): Int`
This can potentially be much more efficient, though the mechanism is
rather fragile, since the polymorphic values will get boxed as soon as
they are passed to any other polymorphic function or data type which is
unspecialized in this way.

#03 Functional Data Structures. (p 36)
*Variadic functions in Scala*
The function List.apply in the listing above is a variadic function,
meaning it accepts zero or more arguments of type A.

*Type inference in Scala*
When writing functions like dropWhile, we will often place the List in
the first argument group, and any functions, f that receive elements of
the List in a later argument group. We can call this function with two
sets of parentheses, like `dropWhile(xs)(f)`, or we can partially
apply it by supplying only the first argument `dropWhile(xs)`. This
returns a function that accepts the other argument, f. The main reason
for grouping the arguments this way is to assist with type
inference, so we can pass `x => x < 34` instead of `(x: Int) => x <
34`. This is an unfortunate restriction of the Scala compiler;
other functional languages like Haskell and OCaml provide
complete inference, meaning type annotations are almost never
required.

*Vector* has constant-time random access, updates, head,
tail, init, and constant-time additions to either the front or rear of the
sequence.

*Trees* - another example of Algebraic Data Type = sum of data
 constructors and each constructor is a product of it's arguments.

# Chapter 4. Handling errors without exceptions. (p54)
Use options Failure & Success

# Chapter 5. Strictness and laziness
*Termination and strictness*
If the evaluation of an expression runs forever or throws an error
instead of returning a definite value, we say that the expression does
not terminate, or that it evaluates to bottom. A function f is strict if
the expression f(x) evaluates to bottom for all x that evaluate to
bottom.

So, non-strict function may choose not to evaluate one or more its
arguments.
`def if2[A](cond: Boolean, onTrue: => A, onFalse: => A): A `

The unevaluated form of an expression is often called a thunk.

# Chapter 6. Purely functional State
State monad `type State[R] = S => (S, R)`

# Chapter 7. Purely functional Parallelism
Some ideas:
 - `def unit[A](a: => A): Par[A]` - for taking an unevaluated A and
   returning a parallel computation that yields an A.
 - `def get[A](a: Par[A]): A` - for extracting the resulting value
   from a parallel computation.

Here we can see that unit has a very definite side-effect, but only
with regard to get.

 - `def fork(a: => A): Par[A]`

Strict or lazy? We can use strict unit and async call:
 - `def unit[A](a: A): Par[A]` - example of primitive combinator
 - `def async[A](a: => A): Par[A] = fork(unit(a))` - example of
   derived combinator

And finally `Par[A]` is a container. And functions are:
```
def unit[A](a: A): Par[A]
def map2[A,B,C](a: Par[A], b: Par[B])(f: (A,B) => C): Par[C]
def fork[A](a: => Par[A]): Par[A]
def async[A](a: => A): Par[A] = fork(unit(a))
def run[A](a: Par[A]): A
```

# Chapter 8. Property-based testing.
 - We aren't using Scala's standard library streams here. They have an unfortunate "off-by-one" error—they strictly evaluate their first element
# Chapter 9. Parser combinators

