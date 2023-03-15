
# Methods

# Sort Array

```JS
myArr = [1,5,4,3]
myArr.sort()
```

# Add element to end of Array

```JS
myArr = [1,5,4,3]
myArr.push(4) //[1,5,4,3,4]
```

# Add element to start of Array

```JS
myArr = [1,5,4,3]
myArr.unshift(4) //[4,1,5,4,3]
```

# Shift / Remove First Element

- Remove first element from array
```JS
const array1 = [1, 2, 3];

const firstElement = array1.shift();

console.log(array1);
// Expected output: Array [2, 3]

console.log(firstElement);
// Expected output: 1
```

# Every

- Loop through each element with given reference
- Use index to get matching element in another array
	- Used in [[Sets Challenges#Check if consistent mapping between two arrays|Sets Challenge]]

```JS
// Arrow function
every((element) => { /* … */ })
every((element, index) => { /* … */ })
every((element, index, array) => { /* … */ })
```

# forEach()
```JS
a.forEach( (elem,index) => { /** ... / } )
```

# some()

- The **`some()`** method tests whether at least one element in the array passes the test implemented by the provided function. It returns true if, in the array, it finds an element for which the provided function returns true; otherwise it returns false. It doesn't modify the array.