# Conditional (ternary) operator
One Line If Statement

https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Conditional_Operator

```js
condition ? exprIfTrue : exprIfFalse
```

```js
function getFee(isMember) {
  return (isMember ? '$2.00' : '$10.00');
}

console.log(getFee(true));
// Expected output: "$2.00"

console.log(getFee(false));
// Expected output: "$10.00"

console.log(getFee(null));
// Expected output: "$10.00"
```


# Destructuring Arrays

Access component variable by key instead of using props.parameter

E.g

```JSX
root.render(
  <React.StrictMode>
    <App library="react"/>
  </React.StrictMode>
);


function App({library}) {
  return (
    <div className="App">
      <h1>Hello there from {library}</h1>
    </div>
  );
}

export default App;

```

Array Destructuing

- Assign variable name based on the position in an array

```js
const [firstCity, secondCity, thirdCity] = ["London", "Tokyo", "Berlin"];

console.log(firstCity); //London
console.log(secondCity); //Tokyo
console.log(thirdCity); //Berlin
```

# Add HTML element to document
```js
function myFunction() {  
  var element = document.getElementById("myDIV");  
  element.classList.add("mystyle");  
}
```


# for...in

```js
const object = { a: 1, b: 2, c: 3 };

for (const property in object) {
  console.log(`${property}: ${object[property]}`);
}

// Expected output:
// "a: 1"
// "b: 2"
// "c: 3"

```