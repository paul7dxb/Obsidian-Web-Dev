-  Primitives: number, string, boolean
-  More complex types: arrays, objects
-  Function types, parameters

```ts

// Primitives

let age: number;
age = 12;

let userName: string;
userName = 'Max';

let isInstructor: boolean;
isInstructor = true;

// More complex types

let hobbies: string[];
hobbies = ['Sports', 'Cooking'];

let person: {
  name: string;
  age: number;
};

person = {
  name: 'Max',
  age: 32
};

let people: {
  name: string;
  age: number;
}[];
```

# Type Inference

- Create variable and immediately assign value
- By default TypeScript will try to infer as many types as possible

declaring string declaration is redundant here:
```TS
let course: string = 'The title of the course'
```

# Union Types

- When there are multiple types are appropriate
- Use `|` to declare union types

```TS
let userName: string | string[]
let course: string | number = 'The title of the course'
```

# Type alias

- Create a base type declaration that can then be used in multiple type definitions
- Use `type` keyword

- Gets thrown out when compiled to JS

```TS
// Base type
type Person = {
  name: string;
  age: number;
}

let person: Person
let people: Person[]
```