# let / const

- let is the new var
- const for constant value

- In essence, blocks are finally treated as scopes in ES6, but only if you declare variables with `let` or `const`

# Arrow Functions

- shorter sytax
- this keyword
	- inside arrow function always keeps its constant
- With one argument you can ommit the parens. Only for one arg!

```js
function myFnc(){
...
}

const myFnc = () => {
...
}
```

If only returning a value can use one line ommit return keyword
```js
const multiplyByTwo = (numberOne, numberTwo) => numberOne * numberTwo
const multiplyByTwo = number => number * 2
```

# Import / Export (Modules)

Export files:

## Default Exports
person.js
```js
const person = {
	name: 'Max'
}
export defualt person
```

## Named Exports

utility.js
```js
export const clean = () => { ... }

export const baseData = 10;
```

## Importing
app.js
```js
//As using defualt export from file can import person as another name
import person from './person.js'
import prs from './person.js'

// Named export
import { clean } from './utility.js'
import { baseData } from './utility.js'

//Alias
import { clean as clen } from './utility.js'

// Bundle in to one JS object
import * as bundled from './utility.js'
```

# Classes

# Construction

## Old Construction

```js
class Human {
	constructor(){
		this.gender = 'Male'
	}

	printGender(){
		console.log(this.gender)
	}
}

class Person extends Human {
	constructor(){
		super(); // Executes parent constructor
		this.name = 'Max';
	}
	
	printName(){
		console.log(this.name)
	}
}

const person = new Person();
person.printName(); //Max
person.printGender(); //Male
```

## New Generation Construction

- Requires babel
- Assign value
- Arrow functions
	- Controls access

```js
class Human {
	gender = 'Male';
	printGender = () => {
		console.log(this.gender)
	}
}

class Person extends Human {
	name = 'Max';
	
	printName = () => {
		console.log(this.name)
	}
}

const person = new Person();
person.printName(); //Max
person.printGender(); //Male
```

## Inheritence

```js
class Person extends Master
```

# Spread & Rest Operators

[Udemy Lecture Spread & Rest](https://www.udemy.com/course/react-the-complete-guide-incl-redux/learn/lecture/8211796#overview)

- Safely copy objects
- 
## Spread

- Split up array elements or object properties

```js
const newArray = [...oldArray, 1, 2]
const newObject = [...oldObject, newProp: 5] //newProp can be used to overwrite old value
```


## Rest

- Used in a function
- Used to merge a list of funtion arguments into an array

```js
function sortArgs(...args){
	return args.sort()
}
```

