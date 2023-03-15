
## Removing specific value k from linked list
```JS
// Singly-linked lists are already defined with this interface:
// function ListNode(x) {
//   this.value = x;
//   this.next = null;
// }

const { template } = require("lodash")

//
function solution(l, k) {    
    
    // Check not empty
    if(!l){
        return []
    }
    
    // Get first valid value
    while(l.value === k) {
        if(l.next){
            l = l.next
        }else {
            return []
        }
    }
    
    // Loop through remaining values by checking the next value isn't k
    curAddr = l
    while(curAddr.next){
        nextAddr = curAddr.next
        nextVal = nextAddr.value
        if(nextVal === k){
            curAddr.next = nextAddr.next
        }else{
        curAddr = nextAddr
        }
    }

    return l
}
```


# Linked list Palindrome

```JS
// Singly-linked lists are already defined with this interface:
// function ListNode(x) {
//   this.value = x;
//   this.next = null;
// }
//
function solution(l) {
    
    // Check not null
    if(!l){
        return true
    }
    
    // Check length 1
    if(!l.next){
        return true
    }
    
    //  set i to point to middle of list using runner j
    i = j = l
    while (j.next){
        j = j.next.next
        if (!j){
            
            break
        }
        i = i.next
    }
    
    // Reverse second half
    
    curAddr = i.next
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
    
    // Match values
    i = i.next
    while(i){
        if(l.value != i.value){
            return false
        }
        i = i.next
        l = l.next
    }
    
    return true

}
```

# Adding Large Integers
```JS
// Singly-linked lists are already defined with this interface:
// function ListNode(x) {
//   this.value = x;
//   this.next = null;
// }

const { tmpdir } = require("os");

//
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
    
    
    carry = 0;
    sum = null;
    
    while (a || b || carry){
        
        if(!a){
            valOne = 0
        } else {
            valOne = a.value
        }
        
        if(!b){
            valTwo = 0
        }else {
            valTwo = b.value
        }
        
        // Create new element for list. Elements next value will be from last round due to big to small
        tempElem = new ListNode( (valOne + valTwo + carry ) % 10000)
        tempElem.next=sum
        
        sum = tempElem
        
        // Truncate any decimal
        carry = (valOne + valTwo + carry ) / 10000 | 0
        
        if(a){
            a = a.next
        }
        if(b){
            b = b.next
        }
        
    }
    return sum
}



}
```

# Merge Linked Lists into Ascending Order

```JS
// Singly-linked lists are already defined with this interface:
// function ListNode(x) {
//   this.value = x;
//   this.next = null;
// }

const { result } = require("lodash")

//
function solution(l1, l2) {
    
    // Check if one list is null
    if(!l1){
        return l2
    }
    if(!l2){
        return l1
    }

	//Get starting value
    if(l1.value < l2.value){
        firstVal = l1.value 
        l1Next = l1.next
        l2Next = l2
    } else{
        firstVal = l2.value    
        l2Next = l2.next
        l1Next = l1  
    }
    
    mergedList = new ListNode(firstVal)
    firstElem = mergedList
    // console.log(mergedList)
    
    
    
    
    while(l1Next || l2Next){
	    //If one list is ended remaining is rest of other list
        if(!l1Next){
            mergedList.next = l2Next
            return firstElem
        }
        if(!l2Next){
            mergedList.next = l1Next
            return firstElem
        }
        // console.log("l1N: " + l1Next.value + " l2N: " + l2Next.value)
        // console.log(firstElem)

        if(l1Next.value < l2Next.value){
            mergedList.next = l1Next
            l1Next = l1Next.next
        } else{
            mergedList.next = l2Next  
            l2Next = l2Next.next   
        }
        mergedList = mergedList.next
    
    }
    
    return firstElem

}
```