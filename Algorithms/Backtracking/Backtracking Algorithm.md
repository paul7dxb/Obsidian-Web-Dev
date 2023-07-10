# General Approach

```
function doBacktrack( current ):
    if current is a solution:
        return current
    for each decision d from current:
        new_state <- state obtained from current by making decision d
        if new_state is viable:
            sol <- doBacktrack(new_state)
            if sol is not None:
                return sol
    # indicate there is no solution
    return None   
```

# Approach avoiding stack overflow

```
function doBacktrackIterative(start):
    stack <- initialize a stack
    stack.push(start)

    while (stack not empty):
        current = stack.pop()

        if current is a solution:
            return current

        for each decision d from current:
            new_state <- state obtained from current by making decision d
            if new_state is viable:
                stack.push(new_state)

    return None
```


```python
def is_valid_state(state):
    # check if it is a valid solution
    return True

def get_candidates(state):
    return []

def search(state, solutions):
    if is_valid_state(state):
        solutions.append(state.copy())
        # return

    for candidate in get_candidates(state):
        state.add(candidate)
        search(state, solutions)
        state.remove(candidate)

def solve():
    solutions = []
    state = set()
    search(state, solutions)
    return solutions
```