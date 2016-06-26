#Video 1
https://www.youtube.com/watch?v=y-lX1mx5_i0&list=PLt7hcIEdZLAnbUxKaG7XIynEWrozOBtXU

Type theory <-> Proof Theory <-> Category Theory

Proof <-> Cat = Categorial logic\algebraic way of thinking about logic and proofs
Type <-> Cat = Categrorial semantics\well-typed terms corresponds to morphisms in category
Type <-> Proof = Propositions as types\formal proofs -- lectures about this one.

Things to keep an eye on:
- abstraction - "behaviour characterazaion"
N != {0, {0}, {{0}, 0}}
- structures, not affordances
(non)conservative extensions
Expression power of programming language is restriction it imposes.
Constructivity.
- proof relevance
- identity
"no entity withour identity"


Truth vs Proof
1. truth table
2. Euclid

Boolean algebra - a complemented distributed lattice
1. pre-order
2. finite meets + joins = greatest lower and upper bounds
Meets:
x<=1
greatest lower bound = z<= x, z<= y and z <x^y
among the lower bound x^y <= x and x^y <=y

Joins:
0<=x
least lower bound z:
z>=x, z>=y and z>= x V y
among x V y >= x and x V y >= y

3. complemented
~x ^ x <= 0
~x V x >= 1

4. Observation: exponential
power(y, x) = x V y

5. distributive
x ^ (y V z) = x ^ y V x ^ z
X V (y ^ z) = x V y ^ x V z

#Video 2
Classical logic = the existence of complemented.

Heyting algebra:
For all a and b there is x such that: a ^ x <= b. This b is denoted as a -> b
= lattice with exponentials
pow(y,x) ^ x <= y
z ^ x <= y
then z <= pow(y,x)

Boolean Algebra is Heyting algebra withour complements.
