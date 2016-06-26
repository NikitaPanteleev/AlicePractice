#Optimization
##Course motivation
NP-problem
 - if you have solution you can verify it very quickly
 - if you can solve one of these problems you can solve them all
Techniques
 - push exponentinal growth, so on real world problems time is acceptable
 - find not the best solution

 ##Knapsack
 Items with (weight, value). Maximize value such that capacity is lower then K weight
 1. Greedy algorithms (like value/weight)
 2. Modeling (sum x(i)* w(i) < K and max value)
 3. Dynamic Programming
 	- divide and conquer
 	- bottom up computation

 O(k, j) - optimal solution for j first items, capacity k 
 complexity O(K*n) - it's pseudo-polynomial. O(log K) from input size. Efficient when K is small
4. Relaxation (optimistic estimate), branch(branch-broad search) and bound
5. Search strategies: depth first, best first, least discrepancy (start from wave "go left branches always", then 1 mistake, then 2... then "go right always")
