# Docs References

-   `map()`  => [https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/map](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/map)
-   `find()`  => [https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/find](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/find)
-   `findIndex()`  => [https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/findIndex](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/findIndex)
-   `filter()`  => [https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/filter](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/filter)
-   `reduce()`  => [https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/Reduce?v=b](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/Reduce?v=b)
-   `concat()`  => [https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/concat?v=b](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/concat?v=b)
-   `slice()`  => [https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/slice](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/slice)
-   `splice()`  => [https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/splice](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/splice)

# Array.map()

[MDN docs](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/map)

- Creates a new array based on another array
- Tranforms each element on the original array using a function
- Function is the argument to the map method

- function as an input
- Applied to each member of an array

```js
const numbers = [1,2,3];

const doubleNumArray = numbers.map((num => {
  return num * 2;
}));

console.log(doubleNumArray); //[2,4,6]
```

# Array.reduce()

- Performs function on each element of array
- Return value is used with next element
- [MDN Docs](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/reduce)

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

# Array.concat()

- Returns new array with item added to the end
- Useful when working with states as new object created and not editing the current object

```JS
newArray = oldArray.concat("newItem")
```



## Filter()

- Create a shallow copy of a portion of a given array

Matching year example:
```JS
  const filteredArray = fullArray.filter((expense) => {
    return expense.date.getFullYear().toString() === filteredYear;
  });
```


## Math.max() for an Array

- Math.max() expects individual values as the arguments
- For an array use the [[Next Gen Features#Spread| spread operator]] to get the max value in an array

For an array of objects
```JS
//Map array object to get an array on wanted values
const dataPointValues = props.dataPoints.map(dataPoint => dataPoint.value)
//Spread the array into the Math.max() function
const totalMaximum = Math.max(...dataPointValues);
```

# Array.reverse()

- Reverses an array in place and returns reference to same array
- IT CHANGES THE ORIGINAL ARRAY
- [MDN Docs](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/reverse)

```JS
const array1 = ['one', 'two', 'three'];
console.log('array1:', array1);
// Expected output: "array1:" Array ["one", "two", "three"]

const reversed = array1.reverse();
console.log('reversed:', reversed);
// Expected output: "reversed:" Array ["three", "two", "one"]

// Careful: reverse is destructive -- it changes the original array.
console.log('array1:', array1);
// Expected output: "array1:" Array ["three", "two", "one"]
```