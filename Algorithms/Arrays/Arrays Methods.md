
# Methods

![[JS_Array_Methods_Cheatsheet.jpeg]]

# Sort Array

```JS
myArr = [1,5,4,3]
myArr.sort()

const array1 = [1, 30, 4, 21, 100000];
array1.sort(); // Expected output: Array [1, 100000, 21, 30, 4]
// 10000 before 21

const months = ['March', 'Jan', 'Feb', 'Dec'];
months.sort(); // Expected output: Array ["Dec", "Feb", "Jan", "March"]
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

```JS
const array = [1, 2, 3, 4, 5];

// Checks whether an element is even
const even = (element) => element % 2 === 0;

console.log(array.some(even));
// Expected output: true

```


# reduce()

- callback function on each element of the array
- In order passing return value from last element

```JS
const array1 = [1, 2, 3, 4];

// 0 + 1 + 2 + 3 + 4
const initialValue = 0;
const sumWithInitial = array1.reduce(
  (accumulator, currentValue) => accumulator + currentValue,
  initialValue
);

console.log(sumWithInitial);
// Expected output: 10
```


# Find if Array in another Array

- Use JSON.stringify() to the be able to find the "string" array in the other
- [SO Link](https://stackoverflow.com/questions/19543514/check-whether-an-array-exists-in-an-array-of-arrays)

```JS
 var a = [ [1,2] , [3,4] ];
 var b = [1,2];
 a = JSON.stringify(a);
 b = JSON.stringify(b);

//then you can do just an indexOf() to check if it is present

var c = a.indexOf(b);
if(c != -1){
    console.log('element present');
}

```


# filter()

- return new array with elements that meet condition
- Can use the element, index

```JS
function solution(inputArray, k) {
    return inputArray.filter((elem,index) => ((index + 1) % k) )
}
```