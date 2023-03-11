
Makes use of [[JS#Destructuring Arrays|Destructuring Arrays]]

# useState Hook

Used to chage state for the entire app

```JSX
function App() {

  //Set initial value when page first rendered
  const [emotion, setEmotion] = useState("happy");

  return (
    <div className="App">
      <h1>Current emotion is {emotion} </h1>
      <button onClick={() => setEmotion("sad")} >Set Sad</button>
      <button onClick={() => setEmotion("excited")} >Set Excited</button>
    </div>
  );
}
```

# useEffect Hook

- First execution of the useEffect willl be done AFTER the component function is exececuted

- First argument function to happen
- Second, when effect is to be called. Can listen for changes in the array

```JS
  useEffect(functionToCall, [dependencies])
```

```JSX
  const [emotion, setEmotion] = useState("happy");

// Logs emotion on initial render and then whenever "emotion" is changed
  useEffect(() => {
    console.log(`Its ${emotion} right now`)},[emotion])
```

Multiple Variables:

```JSX
  useEffect(() => {
    console.log(`Its ${emotion} and ${secondary} right now`)},[emotion, secondary])
```

Taking input logic
```JSX
import { useState } from "react";

function App() {
  const [checked, setChecked] = useState(false);

  return (
    <div className="App">
      <input
        type="checkbox"
        value={checked}
        onChange={() => setChecked((checked) => !checked)}
      />
      <label> {checked ? "checked" : "not checked"} </label>
    </div>
  );
}
```

This can be helped by using the useReducer hook
# useReducer Hook

```JSX
import { useReducer } from "react";

function App() {
	//useReducer( functionToBeCalled, intitialValue)
  const [checked, setChecked] = useReducer((checked) => !checked, false);

  return (
    <div className="App">
      <input type="checkbox" value={checked} onChange={setChecked} />
      <label> {checked ? "checked" : "not checked"} </label>
    </div>
  );
}
```

# useRef Hook

- Often used in Forms
- Reaches out to a UI element and gets its value

```JSX
import { useRef } from "react";
```

[[3 - Forms]]

- Access through the current property
```JS
const nameInputRef = useRef();
const enteredValue = nameInputRef.current.value
```

# Custom Hook

As forms often have same interaction (initial value -> user sets value -> form handles value on submit), it is useful to create custom hook to deal with these actions

- Is a function
- start with use
- expand on a normal hook

```JSX

function useInput(initialValue) {
  const [value, setValue] = useState(initialValue);
  return [
    { value, onChange: (e) => setValue(e.target.value) },
    () => setValue(initialValue),
  ];
}

function App() {
  const [titleProps, resetTitle] = useInput("");
  const [colorProps, resetColor] = useInput("#000000");

  const submit = (e) => {
    e.preventDefault();
    console.log(`${titleProps.value}, ${colorProps.value}`);
    //Reset values after change
    resetTitle();
    resetColor();
  };

  return (
    <div className="App">
      <form onSubmit={submit}>
        <input
          {...titleProps}
          type="text"
          placeholder="Color Title..."
        />
        <input
          {...colorProps}
          type="color"
        />
        <button>Add</button>
      </form>
    </div>
  );
}

```