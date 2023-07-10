# Get Middle point of Linked List

```JS
    //  set i to point to middle of list using runner j
    i = j = l
    
    while (j.next){
        j = j.next.next
        if (!j){
            break
        }
        i = i.next
    }
    
```

# Reverse Values in linked list

```JS
function solution(a, b) {

// Funciton to reverse LL
    const revertList = list => {
        var prev = null;
        while (list) {
            tmp = list.next;
            list.next = prev;
            prev = list;
            list = tmp;
        }
        return prev;
    }
    
    // Reverse input lists
    a = revertList(a)
    b = revertList(b)
}
```

## Reverse part of list
- e.g reverse list l from index i onwards
```JS
    curAddr = i
    prevAddr=null
    
    while(curAddr){
        nextAddr = curAddr.next
        // Point current to previous reversing direction
        curAddr.next = prevAddr
        
        // Assign prev current's for next loop
        prevAddr = curAddr
        i.next = curAddr
        // Assign for next loop
        curAddr = nextAddr
        
    }
```
