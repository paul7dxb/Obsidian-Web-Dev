- Using `any` type can prevent TS from being able to infer a type and therefore catch errors in its later use

Example
```TS
function insertAtBeginning(array: any[], value: any){
    const newArray = [value, ...array]
    return newArray
}

const demoArray = [1,2,3]
const updatedArray = insertAtBeginning(demoArray, -1); //[-1, 1, 2, 3]
// Typescript will not know that updatedArray is type number
```

By using Generics you can tell TS to expect a type in relation to other types:

```TS
function insertAtBeginningGenerics<T>(array: T[], value: T){
    const newArray = [value, ...array]
    return newArray
}

// Now calling function TS will be able to understand the array type
const stringArray = insertAtBeginningGenerics(['a','b','c'], 'd'); // ['a','b','c', 'd'] type: string[]
```

![[TypeScript_Generics.png]]

- Generics also align with declaring array types
	- `numbers[]`
	- `Array<numbers>`

