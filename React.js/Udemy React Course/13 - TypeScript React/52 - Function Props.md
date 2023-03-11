- Communicate data between components
- Pointers to function as a prop

# Function Type

- Used to define how a function passed in with the props will look
	- Parameter types 
	- return type

- Example:
	- function that takes in a string and has no return value (void)

```TSX
const NewToDo: React.FC<{onAddTodo: (text: string) => void }> = (props) => {
```

# Defining functions

```TSX
import { useState } from "react";
import NewToDo from "./components/NewToDo";
import Todos from "./components/Todos";
import Todo from "./models/todo";

function App() {
  const [todos, setTodos] = useState<Todo[]>([]);

  const addTodoHandler = (todoText: string) => {
    const newTodo = new Todo(todoText);

    // return new array to ensure latest state
    setTodos((prevToDos) => {
      return prevToDos.concat(newTodo);
    });
  };

  // Remove a todo item on click
  const removeTodoHandler = (todoId: string) =>{
    setTodos((prevToDos) => {
      return prevToDos.filter(todo => todo.id !== todoId)
    })
  }

  return (
    <div>
      <NewToDo onAddTodo={addTodoHandler} />
      <Todos items={todos} onRemoveTodo={removeTodoHandler}/>
      
    </div>
  );
}

export default App;

```

Usage in child component:
- Bind id here so its not passed to child where function is triggered

```TSX
import React from "react"
import Todo from "../models/todo"
import TodoItem from "./TodoItem"
import classes from './Todos.module.css'

// Props is an object with an items key of type array of Todos
// Using generics using React component in order to get types of children etc.
// Type React Functional Component
const Todos: React.FC<{items: Todo[]; onRemoveTodo: (id: string) => void }> = (props) => {
    return (
        <ul className={classes.todos}>
            {/* Bind to precpnfigure id for function call */}
            {props.items.map(item => <TodoItem key={item.id} text={item.text} onRemoveTodo={props.onRemoveTodo.bind(null, item.id)} /> )}
           
        </ul>
    )
}

export default Todos
```

Child to call function:

```TSX
import React from "react"
import Todo from "../models/todo"
import classes from './TodoItem.module.css'

// Props is an object with an items key of type array of Todos
// Using generics using React component in order to get types of children etc.
// Type React Functional Component
const TodoItem: React.FC<{text: string; onRemoveTodo: () => void}> = (props) => {

    return (
        <li onClick={props.onRemoveTodo} className={classes.item}>
            {props.text}
        </li>
    )
}

export default TodoItem
```



