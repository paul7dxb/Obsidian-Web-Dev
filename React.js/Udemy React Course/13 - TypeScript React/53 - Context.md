# Define types in context

- Use alias to define types for context structure

todos-context.tsx:
```TSX
import React, { useState } from "react";
import Todo from "../models/todo";

// Describe shape of todos Context
type TodosContextObj = {
    items: Todo[];
    addTodo: (text: string) => void;
    removeTodo: (id: string) => void;
  }

  type Props = {
    children: React.ReactNode
  }


// Angle brackets to define types
export const TodosContext = React.createContext<TodosContextObj>({
  items: [],
  addTodo: () => {},
  removeTodo: (id: string) => {},
});

const TodosContextProvider: React.FC<Props> = (props) => {
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

    const contextValue: TodosContextObj = {
        items: todos,
        addTodo: addTodoHandler,
        removeTodo: removeTodoHandler
    }


  return (
  <TodosContext.Provider value={contextValue}>
    {props.children}
    </TodosContext.Provider>
    )
};

export default TodosContextProvider;
```

Use provider in app:
```TSX
  return (
    <TodosContextProvider>
      <NewToDo  />
      <Todos />
    </TodosContextProvider>
  );
```

useContext in comnponents:
```TSX
import React, { useContext } from "react";
// import Todo from "../models/todo";
import TodoItem from "./TodoItem";
import { TodosContext } from "../store/todos-context";
import classes from "./Todos.module.css";

// Props is an object with an items key of type array of Todos
// Using generics using React component in order to get types of children etc.
// Type React Functional Component
const Todos: React.FC = () => {
  const todosCtx = useContext(TodosContext);

  return (
    <ul className={classes.todos}>
      {/* Bind to precpnfigure id for function call */}
      {todosCtx.items.map((item) => (
        <TodoItem
          key={item.id}
          text={item.text}
          onRemoveTodo={todosCtx.removeTodo.bind(null, item.id)}
        />
      ))}
    </ul>
  );
};

export default Todos;
```