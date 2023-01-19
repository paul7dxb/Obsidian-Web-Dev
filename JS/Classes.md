# Creating Classes

Use the [[Next Gen Features#New Generation Construction|New Generation Class Construction]] (requires Babel)

# Add Class

https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Classes

```js
// Declaration
class Rectangle {
  constructor(height, width) {
    this.height = height;
    this.width = width;
  }
}

// Expression; the class is anonymous but assigned to a variable
const Rectangle = class {
  constructor(height, width) {
    this.height = height;
    this.width = width;
  }
};
```

