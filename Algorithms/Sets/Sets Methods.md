# Declare
```JS
doubleMenusSet = new Set()

//Convert to Array
doubleMenus = Array.from(doubleMenusSet)
```

# add element

- add()

```JS
const mySet1 = new Set();

mySet1.add(1); // Set(1) { 1 }
mySet1.add(5); // Set(2) { 1, 5 }
```

# Remove element

- delete()

```JS
mySet1.delete(5); // removes 5 from the set
```

# has()

- returns a boolean indicating whether an element with the specified value exists in a `Set` object or not.

```JS
function solution(a, b, v) {
  
  // Convert to set
  const setB = new Set(b);
  return a.some(elem => setB.has(v - elem)); // returns true if an element of a is in set b

}
```

# Iterate over Set

```JS
for (const item of mySet1) {
  console.log(item);
}
// 1, "some text", { "a": 1, "b": 2 }, { "a": 1, "b": 2 }, 5
```

# Convert to Array

```JS
// Convert Set object to an Array object, with Array.from
const myArr = Array.from(mySet1); // [1, "some text", {"a": 1, "b": 2}, {"a": 1, "b": 2}, 5]
```

# Others

```JS
// intersect can be simulated via
const intersection = new Set([...mySet1].filter((x) => mySet2.has(x)));

// difference can be simulated via
const difference = new Set([...mySet1].filter((x) => !mySet2.has(x)));

// Iterate set entries with forEach()
mySet2.forEach((value) => {
  console.log(value);
});
```