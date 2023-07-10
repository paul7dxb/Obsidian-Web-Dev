# Climbing Stairs at most k at a time

```JS
let gloN
let gloK
let viableStack
let solutions

function solution(n, k) {

gloN = n
gloK = k

solutions = []

viableStack = []

search([])
// console.log(viableStack)

while( viableStack.length > 0 ){
    curState = getNextState()
    // console.log("current state: " + curState)
    search(curState)
}

return solutions

}

function search(state){
    
    
    stateSum = getStateSum(state)
    
    if (stateSum === gloN){
        solutionState = getDeepCopyArr(state)
        // console.log(solutionState)  
        solutions.push(solutionState)

        // return
    }
    for(j = gloK ; j >=1; j--){
        if (stateSum + j <= gloN){
            addToStack(state, j)
        }
    }
    
    // else if (stateSum + gloK <= gloN && gloK !==1){
    //     addToStack(state, gloK)
    //     addToStack(state, 1)
    // } else{
    //     addToStack(state, 1)   
    // }
}

function addToStack(addState, number){
    addStateCopy = getDeepCopyArr(addState)
    addStateCopy.push(number)
    viableStack.unshift(addStateCopy)
}

function getNextState(){
    return viableStack.shift()
}

function getDeepCopyArr(arr){
    return JSON.parse(JSON.stringify(arr));
}

function getStateSum(sumState){
    sum = 0
    for(i=0; i< sumState.length ; i++){
        sum += sumState[i]
    }
    return sum
}
```