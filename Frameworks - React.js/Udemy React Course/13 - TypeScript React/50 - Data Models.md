- Create classes similar to other OOP languages
- Usually in a `models` folder

```TS
class Todo {
    id: string;
    text: string

    constructor(todoText: string) {
        this.text = todoText;
        this.id = new Date().toISOString();
    }
}

export default Todo;
```

- This can then be used in React

Creating Data:
```TS
import Todos from "./components/Todos";
import Todo from "./models/todo";

function App() {

  const todos = [
    new Todo('Todo One'),
    new Todo('Todo Two')
  ]

  return (
    <div>
      <Todos items={todos} />
    </div>
  );
}

export default App;

```

In Component:
```TSX
import React from "react"
import Todo from "../models/todo"

// Props is an object with an items key of type array of Todos
// Using generics using React component in order to get types of children etc.
// Type React Functional Component
const Todos: React.FC<{items: Todo[]}> = (props) => {
    return (
        <ul>
            {props.items.map(item => <li key={item.id}>{item.text}</li> )}
        </ul>
    )
}

export default Todos
```
