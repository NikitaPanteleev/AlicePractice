# Course 1 Parallelism

## Week 1.
Async, Finish.

Java Fork-Join. `InvokeAll(task1, task2)`

Metrics:
`work` - total work
`span` - length of the longest path
`ideal parallelism = work/span`
`T(p)` - execution time on p processors.
`T(infinity) = span`
`speedup = T1 / T(p) <= p` and `speedup <= Work/span`

*Amdahl's law*
`q` - sequential fraction of application (like 0.5), then the best speedup `1/q`


## Week 2.

In FJ, RecursiveTask returns value on join.

`Benign non-determinish` - outputs are different but all acceptatble (example search string)


## Week 3

Parallel loops. `forall`
Matrix multiplication.
Barriers in Parallel Loops.
Grouping: sequential & cycling.
