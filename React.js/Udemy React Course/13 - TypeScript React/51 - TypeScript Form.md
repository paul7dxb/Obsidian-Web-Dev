
- Special React type `React.FormEvent`

Basic example:
```TSX
import React from "react";
import { useRef } from "react";


const NewToDo = () => {

const todoTextInputRef = useRef<HTMLInputElement>(null);
    const submitHandler = (event :React.FormEvent) => {
        event.preventDefault()

        // ! tells TS we know it will not be null. ? would make enteredText string OR null
        const enteredText = todoTextInputRef.current!.value

        if(enteredText.trim().length === 0) {
            // throw an error
            return;
        }

        // If valid add to Todo list. Communicate back to app component
    }

  return (
    <form onSubmit={submitHandler}>
      <label htmlFor="text">To Do text</label>
      <input type="text" id="text" ref={todoTextInputRef}/>
      <button>Add ToDo</button>
    </form>
  );
};

export default NewToDo;

```

# Get form Data

## useState approach
- Validate every key stroke
	- ToDo: create example for this approach

## useRef approach
- [[2 - Hooks#useRef Hook|useRef() notes]]
- Use generic type with useRef to set concrete type of ref
	- HTMLInputElement
	- MDN will tell you input element interface if using others
- Assign inital value explicitally
- Use [[52 - Function Props]] to use function from other component

# Store Data

- Hold data somewhere, example in app using useState()
	- Ensure useState has array appropriately declared
	- `const [todos, setTodos] = useState<Todo[]>([]);`