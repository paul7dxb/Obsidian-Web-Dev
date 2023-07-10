# Binary Tree sum of vertex

```JS
//
// Binary trees are already defined with this interface:
// function Tree(x) {
//   this.value = x;
//   this.left = null;
//   this.right = null;
// }

let goalVal
let found = false
function solution(t, s) {
    
    // Empty tree check
    if(!t){
        return false
    }
    
    goalVal = s; 
    start = anotherOne(t, 0, [0])
    
    return found
}

function anotherOne(node, sumAtEntry, treeArr){
    // console.log("another one: " + treeArr)
    // console.log("another one: " + node.value)
    
    sumSoFar = sumAtEntry + node["value"]
    
    newTree = [ treeArr,node["value"]]
    if(node["left"] ==null && node["right"] == null){
        // Reached leaf to check sum
        // console.log("end of leaf at: " + newTree + " sum so far: " + sumSoFar)
        if(sumSoFar == goalVal){
            found = true
            console.log("Found good val" + sumSoFar)
            return true
        }
    }else{
        if (node["left"] ){
            // console.log("send left:")
            newTreeL = [ treeArr,node["value"]]
            sumSoFarL = sumAtEntry + node["value"]
            anotherOne(node["left"] , sumSoFarL, newTreeL)
            
        }
        if(node["right"]){
            // console.log("send right:")
            newTreeR = [ treeArr,node["value"]]
            sumSoFarR = sumAtEntry + node["value"]
            
            
            anotherOne(node["right"] , sumSoFarR, newTreeR)
        }
    }
    
}
```

```JS
function solution(t, s) {
    if (!t) return s === 0;
    s -= t.value;
    return solution(t.left, s) ||
           solution(t.right, s);
}
```

```JS
solution = (t, s) => {
    if (!t) return (s === 0);
    return traverse(t, s);
}

traverse = (t, s) => {
    if (t.left === null && t.right === null && t.value === s) {
        return true;
    }
    s = s - t.value;
    return (!!t.left && !!traverse(t.left, s)) || (!!t.right && !!traverse(t.right, s));
}
```

# Symmetric Tree

```JS
//
// Binary trees are already defined with this interface:
// function Tree(x) {
//   this.value = x;
//   this.left = null;
//   this.right = null;
// }


function solution(t) {
    return checkSplitTree(t, t);
}

function checkSplitTree(t1, t2) {
    // OKay if both null
    if (t1 == null && t2 == null) {
        return true;
    }
    // Check not one null OR values not equal
    if ( (t1 == null || t2 == null) || t1.value != t2.value) {
        return false;
    }
    // Recursive check of children. Mirroed (left <-> right on each side)
    return checkSplitTree(t1.left, t2.right) && checkSplitTree (t1.right, t2.left);
}
```

# Tree Traversal

- Output tree from left to right -> top to bottom
- Get max Value at each level

```JS
//
// Binary trees are already defined with this interface:
// function Tree(x) {
//   this.value = x;
//   this.left = null;
//   this.right = null;
// }
function solution(t) {
// Root elem
if(!t){
    return []
}

topDown = [t.value]
maxAtLevels = [t.value]

lastLevel = [t]

while (lastLevel.length > 0){
    // Check for children in any
    // Store children locations

    // make new array for next level
        nextLevel = []
        lastLevel.forEach((node) => {
            if(node["left"]){ 
                nextLevel.push(node["left"])
            }
            if(node["right"]){             
                nextLevel.push(node["right"])
            }
        })


    // for elem in next Level location
    // store value in result array

    if(nextLevel.length > 0){
        nextLevel.forEach((node) =>{
            topDown.push(node.value)
            console.log(node.value)
        })
    }

    if(nextLevel.length > 0){
        levelVals=[]
        nextLevel.forEach((node) =>{
            levelVals.push(node.value)
            // console.log(node.value)
        })
        maxLevel = Math.max(...levelVals)
        maxAtLevels.push(maxLevel)
    }

    lastLevel = nextLevel
}

return topDown, maxAtLevels

}

```