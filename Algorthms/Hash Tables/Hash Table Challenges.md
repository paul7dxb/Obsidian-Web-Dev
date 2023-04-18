# All possible Summations

- Given array of coins and up to quantity amount of each. Find out how many different total amounts you can make

```JS
function solution(coins, quantity) {
    
    solutionTotals = {0 : true}
    solutionTotalsArr = [0]
    
    for(let i = 0; i < coins.length ; i++){
        // Go through each coin value
        coinValue = coins[i]
        // console.log("New coin" + coinValue)
        
        
        currentSolutionLength = solutionTotalsArr.length
        
        for(let j=0; j < currentSolutionLength ; j++){
            // Go through previous solutions for each new coin in list
            foundSolutionVal = solutionTotalsArr[j]
            
            
            for(let coinCount = 1; coinCount <= quantity[i] ; coinCount++ ){
                // console.log(coinCount + " of " + coinValue)
                addedValue = coinValue * coinCount
                totalSum = addedValue + foundSolutionVal
                
                if(!solutionTotals[totalSum]){
                    // console.log("addedSol " + totalSum)
                    solutionTotals[totalSum] = true
                    solutionTotalsArr.push(totalSum)
                }
            }  
        }
    }

    return (solutionTotalsArr.length - 1)

}
```