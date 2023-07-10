
# Bottom-up strategy (iteration)
- In this strategy, you start solving from the smallest subproblem up towards the original problem. If you’re doing this, you’ll solve all of the subproblems, thereby solving the larger problem. The cache in bottom-up solutions is usually an array (either one or multi-dimensional).

# Top-down strategy (recursion)
- Start solving the identified subproblems. If a subproblem hasn’t been solved yet, solve it and cache the answer; if it has been solved, return the cached answer. This is called memoization. The cache in top-down solutions is usually a hash table, binary search tree, or other dynamic data structure.
