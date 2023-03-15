# climbingStairs

```JS
function solution(n) {

// Number of ways of getting to nth step is:
// Number of ways of getting to n-1 step + one step
//  number of ways of getting to n-2 step + a two step

combos = []
combos[1] = 1
combos[2] = 2

for ( i = 3 ; i <=n ; i++){
    combos[i] = combos[i-1] + combos[i-2]
}
return combos[n]

}
```

# houseRobber

```JS
function solution(nums) {
    
    // Max will be:
    // The max from new house plus max of two houses less OR
    // Same as max from one house less
    
    // Approach:
    // Accumulate max values from start of street as max values are based on previous
    
    max = []
    noOfHouses = nums.length
    
    max[0] = 0
    max[1] = nums[0]
    
    // max[2] = Math.max( nums[1] + max[0] , nums[0])
    // max[3] = Math.max( nums[2] + max[1], max[2])
    for(i=2; i<= noOfHouses; i++){
        max[i] = Math.max( nums[i-1] + max[i-2], max[i-1] )
    }

    return max[noOfHouses]

}

```