# Formal Logic

## Formal Logic Undressed — Paul Snively
https://www.youtube.com/watch?v=saMtzIaDCJM

formality - means put constraint
=>, ^ (conjuction = and), \/ disjunction, for every, exist

Types are propositions, programs are proofs.
Bertran Rassel -> Principia Mathematica
and Alonso Church created a new logic which includes substitution, abstraction, application. And it's called Lambda-calculas.

Raymond Smullian

Presenter uses Coq.
http://milessabin.com/blog/2011/06/09/scala-union-types-curry-howard/


https://www.youtube.com/watch?v=7BPQ-gpXKt4&list=PLlb7e2G7aSpRDR44HMNqDHYgrAOPp7QLr
# Лямбда-исчисление

pure λ-calculus
V = {x , y, z ..}
A - λ terms

x \in V => x \in A
M,m \in A => M N \in A
x \in V, M \in A => λx.M \in A

A ::= V | AA | λV. A

λx. M[x] - bounds x in term M


λy ((λx (xz)) y) = λy (λx xz) y => BV( (λx xz) y) with {y} = BV( (λx xz)) with BV(y) with {y} = BV(xz) with {x} with empty with {y} = {x, y}

M - Замкнутый лямбда-терм = комбинатор if FV(M) = empty

(λx. xx) (λz zz) y = M N K

(λx xz) x = xz


M x = yzx
(λx. (x z)) yxx = yxx z
