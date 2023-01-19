# let / Const

- let is the new var
- const for constant value

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