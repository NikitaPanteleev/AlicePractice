# Markov Network Fundamentals (Week 2)
## Pairwise Markov Networks (10:59)
  A
 / \
D   B
 \ /
  C
fi(1)[A,B] - affinity, compatibility, soft consttraints. If A student has misconception
and he studies with B, then B is probably has it either.
a(0) has misconception
a(1) doesnt have

fi(1)[A,B]
a0, b0 30
a0, b1  5
a1, b0  1
a1, b1 10

P~(A,B,C,D) = fi(A,B) * fi(B,C) * fi(C,D) * fi(D,A) - informalized
measure
* 1/Z partitior function to normalize

And probability isn't directly mapped to factor fi[A,B] because it's
not local.

*Pairwise Markov Networks* - undirected graph whose nodes are X1,
 ... Xn and each edge X(i) - X(j) is associated with a factor
 potential fi(i, j) (Xi, Xj)
## General Gibbs Distribution (15:52)
  A
 /|\
D - B
 \|/
  C

P(A, B, C, D). The number of parameters O(n^2*d^2)
Gibbs Distribution
parameter fi({set})
F = {fi(D1), fi(D2), ...fik(Dk)}
probability = 1/z * fi1 * fi2 *... fik

Induced Markov Network for A, B, C, D is fi(A,B,C) * fi(B,C,D)
Factorization. Active trail: X1 - X2 -.. Xn given Z if no X(i) in Z
## Conditional Random Fields (22:22)
Task-specific prediction
X input, Y target variable
Image segmentation, Text processing.
X - pixel -> Y - class (grass, cow, water on picture)
X - word  -> Y label
CRF model is P(X, Y) = fi(Di) *...* fi(Dk) / Z(X) - distribution of Y
given X.
A CRF is parameterized the same as a Gibbs distribution but normalized
differently
-  generalizes logistic regression models
-  dont need to model distribution over variables we dont care about
-  allow models with highly expressive features without worrying about
   wrong dependencies
