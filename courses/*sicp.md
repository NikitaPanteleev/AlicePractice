(link)[http://ocw.mit.edu/courses/electrical-engineering-and-computer-science/6-001-structure-and-interpretation-of-computer-programs-spring-2005/video-lectures/1a-overview-and-introduction-to-lisp/]

# Week 1: Overview and Intro to Lisp
##Blackbox abstraction
##Conventional interfaces
 - Generic operations
 - Large-scale structure and modularity
 - Object-oriented programming
 - Operations on aggregates (Streams)

##Metalinguistic abstraction
YF = (F (YF)) <=> Eval\Apply

##Lisp
 - Primities + * 28
 - Means Of Operations (), COND, IF
 - Means Of Abstractions DEFINE

Prefix Notations; Pretty Printing; Balancins parathensis.
```
(DEFINE A (* 5 5))
(* A A)```
```
(DEFINE (SQUARE X) (* X X)) is syntactic sugar for
(DEFINE SQUARE (LAMBDA(X) (* X X)))```
define is a symbol = DEFINE SQUARE
defina a procedure = DEFINE (..)
```
(COND ((predicate) (action)) ((other cond) (other action)) ()...)```
Also algorithm for finding square root (try guess if good enough guess
else improve guess)

Block structure
