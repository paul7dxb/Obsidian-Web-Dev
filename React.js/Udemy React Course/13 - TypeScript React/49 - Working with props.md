- Declare type of props in order to get error support for types
	- Or explicitly declare type `any`
- Project will be able to notice missing props once required types are declared

# Describe required props

```TS
import React from "react"

// Props is an object with an items key of type array of strings
// Using generics using React component in order to get types of children etc.
// Type React Functional Component
const Todos: React.FC<{items: string[]}> = (props) => {
    return (
        <ul>
            {props.items.map(item => <li key={item}>{item}</li> )}
        </ul>
    )
}

export default Todos
```


# No more PropsWithChildren

```TS
If you are using React 18+ then you need to use PropsWithChildren type

    import { PropsWithChildren } from "react";
     
    const Todos: React.FC<PropsWithChildren<{items: string[]}>> = ({ children, items }) => {
        return (
            <ul>
                {children}
            </ul>
        )
    }
```