# Intro
- Backtracking is a technique used to build up to a solution to a problem incrementally. These "partial solutions" can be phrased in terms of a sequence of decisions. Once it is determined that a "partial solution" is not viable (i.e. no subsequent decision can convert it into a solution) then the backtracking algorithm retraces its step to the last viable "partial solution" and tries again.
- it into a solution) then the backtracking algorithm retraces its step to the last viable "partial solution" and tries again.
- Visualizing the decisions as a tree, backtracking has many of the same properties of depth-first search. The difference is that depth-first search will guarantee that it visits every node until it finds a solution, whereas backtracking doesn't visit branches that are not viable.
- Because backtracking breaks problems into smaller subproblems, it is often combined with dynamic programming, or a divide-and-conquer approach.
- Common interview tasks that use backtracking are crossword puzzles, Sudoku solvers, splitting strings, and cryptarithmetic puzzles.

# Concepts

-   **State:** 
	- A "partial solution" to the problem.
-   **Rejection criterion:** 
	- A function that rejects a partial solution as "unrecoverable". i. e. no sequence of subsequent decisions can turn this state into a solution. Without rejection criteria, backtracking is the same as depth-first search.
-   **Viable:** 
	- A state that may still lead to a solution. This reflects what is known "at this stage". All states that fail the rejection criteria are not viable. If we have a state that is initially viable, and find that all paths to leaves eventually terminate at a state that fail the rejection criteria, the state will become non-viable.
-   **Heuristic:** 
	- Backtracking will (eventually) look at all the different viable nodes by recursively applying all the possible decisions. A heuristic is a quick way of ordering which decisions are likely to be the best ones at each stage, so that they get evaluated first. The goal is to find a solution early (if one exists).
-   **Pruning:** 
	- The concept of determining that there are no nodes / states along a particular branch, so it is not worth visiting those nodes.

-   **Depth-first search:**  
	- A backtracking algorithm is conceptually very similar to depth-first search (DFS). A DFS will "roll back" the current state to a node up the tree once it reaches a leaf node, and is guaranteed to find a solution (or search every node). Backtracking can be thought of as DFS with early pruning.
-   **Recursion:**  
	- Backtracking is often implemented using recursion, so it helps to be familiar with how to write recursive functions.
-   **Stacks:**  
	- If you need a lot of nested recursive calls, trying to use simple recursion might result in a _stack overflow_ error. You can mimic recursion by using a stack data structure.