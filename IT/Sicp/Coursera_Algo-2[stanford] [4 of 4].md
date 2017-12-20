#Week 1: Intro
###Internet routing
Dijkstra's algo for short path (it works in allmost linear time with nonnegative edges)
But the number of nodes in Internet is large => we need local computation => Bellman-Ford algo
###Sequence alignment
Needlman-Wunsch score for
AGCCTA
AGC-TC - how are these strings close?
###Big O annotation
Why algos are important, Graph representation
Graph search
Dijkstra's shortest path algo (dijkstra's greedy critieria).
BreadFirstSearch gives the shortest path if length of all edges is 1.
Data Structures.
Heap.
- insertion O(log n)
- extract min O(log n)
Event Manager, Median Maintanence:
divide numbers by 2 parts.

## III. Intro to Greedy algos
Algorithms:
- divide and conquer
- randomized algos
- greedy = iteratively make "my opic" decisions, hope everything works out at the end
- dynamic programming

Danger: most greedy algorithms are not correct.
Proof of correctness:
1) induction.
2) exchange argument
3) whatever works
Application: Optimal Caching.
Small cache and sequence of requests. Which pages must be removed from
small memory to minimize page faults?
*Theorem*(Belady 1960s):furthest-in-the-future algorythm is optimal
=> practical "the least frequently used = furthest-back-in-the-past"
## IV A Scheduling Application
one process - many jobs
job has
 - w=weight
 - l=length
Completion time:
jobs:             #1=1min #2=2min #3=3min
completion times: =1       =3     =6min
Objective function: minimize the weighted sum of completion time
Correct algorithm: reverse sort w/l and process them
Proof: suppose there is optimal solution there some two elements
ordered the opposite, then it's easy to reverse them and gain even
better solution

## V Minimum Spanning trees
*Informal definition* Connect a bunch of points together as cheaply as
possbible
 - Prim's Algorithm (1957)  \
 - Kriskads' MST Algorithm --=> O( m log n), m - is a number of edges,
 n - a number of vertices
*Input* Undirected graph G = (V, E)
*Output* Min cost tree T <= E that spans all vertices. This T is
 connected and has no cycles.
*Assumptions* input graph is connected (otherwise Minimum spanning
 forest); edge costs are distinct;
### Prim's Algorithm:
Choose the cheapest edge in each iteration.
*Proof* Cut is a a parition of graph into 2 non-empty graphs
*lemma 1 Empty Cut*  graph is not connected <=>  exists cut with no
 crossing edges
 ...
*CUT PROPERTY* Suppose that there is a cut (A, B) such that e is the
 cheapest edge that crossing it, then e belongs to MST.
 take cheapest edges from => Prim's Algorithm
*Proof* Smart exchange. Suppose there is MST and cut with e is
 cheapest and e is not in MST, then you can smart include e in MST
 (avoiding cycles) and new solution would be better=> contradiction!
*Fast implementation*
 - brute-approach is n vertices steps with full scan of m edges => n*m
 - Using heap to store vertices. (and we store for each vertice the shortest
   edge to the vertices in not discovered partition)
 - Maintaining variants   
## VI Kruskal's minimum spanning tree algorithm
Choose the cheapest remaining edge and check that it doesn't make
cycles in already collected components. If it does - skip edge and
take other cheapest.
*Proof* There is always a Cut for which current chosen cheapes edge is
actually the cheapest => this edge belongs to MST by CUT PROPERTY.

Union-find data structure.

Can we do better?
O(m) -randomized algorithm  [Karger-Klein-Tarjan-JACM 1995]
Any deterministic O(m) algorithm? We do not know.
There is O(m * alpha(n)) [Chazelle 2000] - inverse Ackermann
function. This function is slow then log* n. Log*n is a number of
dividing by log until the result is less then 1. It's inverse function
of tower of 2 (2^2^2^.n) log* is about 5 for the biggest number on
your computer.

Also there is a proof of optimality for [Pettie 2002] algoithm, but we
do not know it's asympotic time

## VII Clustering
Greedy approach to maximize "space" function. Kruskals approach.

## VIII Huffman codes
Binary codes. Variable-length encoding (mp3). Ambiguity => Prefix-free
encoding.
Codes as Trees. Path from the root (0 to left, 1 to right) to the leaf
is it's encoding.
Prefix-free <=> no letters in nodes, letters are only in leafs.
*Problem defenition* L(T) = sum p(i) * l(i) - there p is probability
of the letter and l is the path to the node:
A -> 0, B -> 10, C -> 11, D -> 111
o
| \
A  o
   | \
   B  o
      | \
      C  D
*Huffman greedy algorithm* Heuristics: merging increase the length by
one, so merger the least frequent letters. This is a new leaf ab with p =
p(a) + p(b)
*Notes on running times*
Sorting + O(n) non-trivial (managing 2 queues)

## X Introduction to Dynamic Programming
*Maximum Weight Independent set*  Path Graph G (V, E) with weights on
vertices, find a subset of vertices with max weights that no two
vertices are adjecent.

V(n) - G... a current graph is one of twos:
V(n) not in WIS, then WIS of G
V(n) in in WIS + WIS of G` subset of G.
Linear time algorithm. Eliminating redundancy by memoization.
A[i] - optimum for vertices 0..i
Reconstruction algoritm

## XI The knapsack Problem

## XII Sequence Alignment
similarity measure:
AGCCTA
A-CCTG -- last letter and gap. Total penalty = alphaGap +
alphaTransformation
3 optimal subsolutions for the last character.
For two string X, Y keep track of Xi Yj - first letters of each
string. Reconstruction algo O(m+n), the algo itself m*n.

## XIII Optimal search trees
Keys in binary search trees with given frequences p1, p2,...
Difference between Huffman encoding = huffman tree was prefix-free.
The intuition is: for root r and T1 < r < T2 optimal solution is
optimal solutions for T1, T2 + r.
You should compute for 1, 2.. n keys  all solutions for
[i, i+1,... j-1, j]

C(i,j) = sum over p (i..j) + min r=i..j[C(i, r-1) + C(r+1, j)]
Diagonal by diagonal. O(n^3) running time.
*Fun fact* Knuth 78 optimized O(n^2)

## XIV Bellman-ford
Directed graph with edges with lengths. Compute the shortest path from
source to every other nodes.
*Dijkstra's algorithm* O(m*logn) - m edges, n vertices.
 - it doesnt work with negative costs
 - not very distributed.

On negative cycles.
Solution#1 Allow cycles. Then infinite negative cycle
Solution#2 Compute shortest cycle-free s-v path. It's NP hard.
Solution#2 Assume that no negative cycles it will fing shortest path
or show this cycle.
*Optimal solution*
Artificially restrict the number of edges in the graph. And let P be

an optimal solution for i 0..m edges it could contain. So for i+1 edge
the optimal solution is the min from (i-1 edges solution, in-vertices
Pmin + edge cost to the final vertix).

*Basic algorithm*
L(i, v) - there v - is destination vertix and i is budget (number of
edges)

L(i, v) = min {L(i-1, v), min (over edges to v) {L(i-1, v)  +c(w,v) }}
If no negative cycles => only need to solve subproblems up to i = n-1
order of loops matters:
for i = 1... n-1:
  for each vertex:
    A[i,] = min...
answer in A[n-1, v]
complexity = O(mn) = O( n (number of iteration * sum of in-deg(v) =
2*m)
*Improvements* Stopping early. If two iterations are the same - stop.
*Detecting negative cycles* G has no negative cycles <=> A[n-1, v] =
A[n,v]
*Space Optimization* space = O (n^2) = O (number of iteration * number
of vertex values). We need only the last iteration! And for solution
trains back predessors pointers.

*Internet Routing* Distributed between vertices, push-based, handling
 failures.
 Counting to infinity in naive implementation -> path vector protocol.

# All-pairs shortest path
For every pair of vertices in the graph compute the shortest path or
correct report that graph contains negative cycle.
*First guess* n times * Dijkstra = O(n^2 * log n) - sparse case
O(nm log n)                     = O(n^3 * log n) - dense case

#The Floyd-Warshall algorithm
all pair short paths with given 1,2...k vertices allowed.
O(m * n^2) where n number of vertices
# A reweighting technique
A Johnson's algorithm to the general edge case (negative weights as
well) is O(nm logn) and is
 - 1 invocation of Bellman-ford O(m*n)
 - n invocation of Dijkstra O(mn logn)

So, what's so special about negative edges. Let's shift the numbers to
all weights to be positive, but it's good only when all paths has the
same number of edges! But this shift exists:
*definition* for every edge e = (u,v)  c'(e) = c(e) + p(u) - p(v)
After that every path s-t is changed by constant factor + (p(s) -
p(t))
# Johnson's Algorithm
compute shortest paths from new vertes s which is directly connected
with every other vertix with edge 0, so the paths would < 0. Then just
use these paths as vertex weights to recompute edges.
# XVI. NP-COMPLETE PROBLEMS (Week 5)
*the class P* - all polynomial-time problems O(n^k)
Paths, trees and flowers.
Halting problem is harder then salesman problem. But
TravelSalesmanProblem(TSP) is the hardest in the class of all
brute-force solvable.
*NP* = nondetermenistic polynomial
 - solution has a length in polynomial in input size
 - solutions can be verified in polynomial times

or PET = possibly exponential time problem or one day provable
exponential time
TSP with length < 1000 and then general problem invoke these problems
*Recipe*
 - find NP problem p
 - shows that your problem reduces to this problem p

the list of problems is Garery and Johnson book "computers +
intractibility"

# P vs NP

# what to do with NP-problems?
1. focus on computationally tractable special cases
*Examples*
 - Weighted Indepentent Set (max weight edges that do not join
together). THere is a dynamic solution in 1D case.
 - knapsack with polynomial size capacity (w  = O(n))
 - 2SAT instead of 3SAT (collection of variables with only 2 possible
   values with constraints on pairs of these variables. Is this
   collection exists?)
 - vertex cover when OPT is small
2. Heuristics - fast and not always correct.
3. solver in exponential time but better then naive brute-force
   strategy

# XVII. FASTER EXACT ALGORITHMS FOR NP-COMPLETE PROBLEMS (Week 5)
## The vertex cover problem
Compute a minimum-cardinality vertex cover - a subet of vertices that
contain at least one endpoint for each edge of graph G.
This is a NP-complete problem.

Cases:
 - tree. It's P problem.
 - bipartite problem
 - optimal solution is small (~log n)

## Smart exponential solution
A substructure lemma. (solving with solution of small number K of
vertices)
Take edge (u, v) and delete vertix u or v with all adjacent edges -
this graph is called G(u) or G(v).
G has k vertix cover <=> G(u) or G(v) has k-1 vertix cover.
So let's do recursive search. Running time is 2^k recursive calls * m
work per call = O(m * 2^k) and if upper bound is k = log n =>
polynomial time
## The travelling salesman problem
Finding min cycle. O(n^2 * 2^n)
Some guesses including: L(i,j) = min {L(i-1, k) + c(k,j)} - no
repeated visits allowed.
*Subproblems* for every destination and every set S = (1,2...n) that
contains i and j  let L(S, i, j) = min path from 1 to j that visits
precise by vertices of S exactly once each.

So i -> k -> j - brute force among vertices k L(s, i, j) = min {L(s-
{j}, k)  + c(k,j)}
# XVIII. APPROXIMATION ALGORITHMS FOR NP-COMPLETE PROBLEMS (Week 6)
## A greedy knapsack heuristics.
Order by price/ weight and choose them by one skipping that do not
fit.
Step 3: compare optimal solution and every item itself.
This algo guarantee >= 50% of solution

Fractional solution (with fractions of units) >= optimal solution.
So our solution of 3step approach * 2 >= k items + k+1 item >= k
items + fraction of k+1 item >= optimal solution
=> our solution >= optimal solution / 2
