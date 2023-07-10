## Finding First duplicate number

```JS
solution = (a) => {
    const pastNums = {}
    
    for (let v of a){
        if (pastNums[v]){
            return v
        } 
        pastNums[v] = v
    }

    return -1   
}
```

- contatinsDuplicates(a)
```JS
function solution(a) {
dic = {}

for(i=0; i< a.length ; i++){
    if(dic[a[i]]){
        return true
    }
    dic[a[i]] = 1
}

return false
}
```

## First Character that doesn't appear twice

```JS
function solution(s) {
    foundRepeatLetters={}
    
    for( i=0; i< s.length -1; i++){
        foundRepeat = false
        
        if ( foundRepeatLetters[s[i]] ){       
            foundRepeat = true
        } else{
            for( j=i+1; j< s.length; j++){
                if( s[i] == s[j]){
                    foundRepeatLetters[s[i]] = s[i]
                    foundRepeat = true
                    break
                }
            }   
        }
        if(!foundRepeat){
            return s[i]
        }
        
    }
    
    if(s.length == 1){
        return s[0]
    }
   
    return ("_")
}
```

## Rotate Matrix 90 degrees
```JS
// create new row made from required a elements
// Each new row is made up from bottom to top of element x from each a row

function solution(a) {
    //First row
    b=[]
    
    // b[0] = [a[2][0],a[1],a[0]]
    for (x=0 ; x<a.length; x++){
        b[x]=[]
        for (y = 0 ; y < a.length ; y++ ){
            b[x][y] = a[a.length-y-1][x]
        } 
    }

    return b
}
```

## Soduku Checker

```JS
function solution(grid) {
    // Validate rows
    console.log("checking rows")
    for (row=0; row<9; row++){
        if(findRepeatedNum(grid[row]) ) {
            console.log("in if")
            return false
        }
    }
    
    //Validate columns
    console.log("checking cols")
    for (x=0; x<9; x++){
        col = grid.map((value,index) => {
            return value[x]
        })
        if(findRepeatedNum(col)){
            return false
        }
    }
    
    // Validate squares
    console.log("checking squares")
    // col of squares
    for(startX = 0; startX < 3; startX++){

        for(startY = 0; startY < 3; startY++){
            sqArr=[]
            for (y=0; y<3;y++){
                sqArr.push(...grid[3* startY + y].slice(startX * 3, startX * 3 + 3))
            }
            console.log(sqArr)
            if(findRepeatedNum(sqArr)){
                return false
            }
        }
    }
    return true
}

function findRepeatedNum(arr){
    const pastNums = {}
    console.log("Checking: " + arr)
    for (let n of arr){
        if (pastNums[n] && n !== '.'){
            console.log("found repeated: " + n)
            return true
        }
        pastNums[n] = n
    }
    return false
}
```

# Dictionary Lookup

Check if word1 + word2 = word3 and none of the words have a leading 0 (but can = 0 only)
```
crypt:
["SEND", 
 "MORE", 
 "MONEY"]
solution:
[["O","0"], 
 ["M","1"], 
 ["Y","2"], 
 ["E","5"], 
 ["N","6"], 
 ["D","7"], 
 ["R","8"], 
 ["S","9"]]
```

```JS
const { forEach } = require("lodash");

function solution(crypt, solution) {
    // Create dictionary lookup
    dictionary = {}
    solution.forEach((x) => {
        dictionary[x[0]] = x[1]
    })

	// Translate each word
    wordTotals=[]
    for (word = 0; word < 3; word++){
        wordLetters = crypt[word].split('')
        console.log(wordLetters)
        // check for leading zero start
        if(dictionary[wordLetters[0]] == 0 && wordLetters.length !== 1){
            return false
        }
        wordNum = ''
        for(i=0; i < wordLetters.length ; i++){
            wordNum += dictionary[wordLetters[i]]
        }
        console.log(wordNum) 
        wordTotals[word] = parseInt( wordNum)
    }
    
    //Check if valid crypt
    return (wordTotals[0] + wordTotals[1] === wordTotals[2])
    
}
```

# Array holding longest values
```JS
const { words } = require("lodash");

function solution(inputArray) {
    // Find max
    
    //max = 0;
    //inputArray.forEach((elem) => {console.log(elem.length);if(elem.length > max){max = elem.length}})
	let max = Math.max(...inputArray.map(x => x.length));
    
    return inputArray.filter((elem) => (elem.length == max))
}
```

# Check Similar array

- a can be made into b with at most one swap

```JS

```


# Array of Numbers into Ascending Order

```JS
// Sort numerically because default is lexicographical sort:
[3, 8, -10, 23, 19, -4, -14, 27].sort((a,b)=>a-b)
// Output: Array(8)  [ -14, -10, -4, 3, 8, 19, 23, 27 ]
```

# Total number of 'True's' in Array

```JS
totalTrues = roadRegister[j].filter( x => x).length
// or
totalTrues = roadRegister[j].filter( Boolean ).length
```