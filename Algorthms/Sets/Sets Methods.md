# Declare
```JS
doubleMenusSet = new Set()

//Convert to Array
doubleMenus = Array.from(doubleMenusSet)
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
