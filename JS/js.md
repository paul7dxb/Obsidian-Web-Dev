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

# Destructuring

[Udemy Lecture Destructuring](https://www.udemy.com/course/react-the-complete-guide-incl-redux/learn/lecture/8211798#overview)

- Extract array elements or object properties and store them in variables
- Single elements or properties

```js
//Array Destructuring
[a,b] = ["Hello", "Max"]
console.log(a) // Hello

//Object Destructuring
{name} = {name: "Max", age: 28}
console.log(name) //Max
```

## Destructuring Arrays

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


# Reference & Primitive Types

- Storing a variable in anohter variable copies the value
- Assigning some values may only copy pointer
	- Arrays
	- Objects
	- Copy in an immutabel way by copying with spread
		- Deep versus shallow copying (child items may only be references)

```js
const person = {
	name: "Max"
};
const secondPerson = person;
person.name = "Manu"

console.log(secondPerson) // Manu due to copied pointer
```

# JS Date Formatting

```js
    const month = date.toLocaleString('en-US', {month: 'long'}); //June
    const day = date.toLocaleString('en-US', {day: '2-digit'}); //12
    const year = date.getFullYear(); //2022
```