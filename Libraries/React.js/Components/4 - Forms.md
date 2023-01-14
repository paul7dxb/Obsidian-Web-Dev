Can be used with [[3 - Hooks#useRef Hook|useRef Hook]]



```JSX
function App() {

  const textTitle = useRef();
  const hexColor = useRef();

  const submit = (e) => {
    e.preventDefault();
    const title = textTitle.current.value;
    const color = hexColor.current.value;
    console.log(`${title}, ${color}`);
    //Clear values
    textTitle.current.value = ""
    hexColor.current.value = ""
  };

  return (
    <div className="App">
      <form onSubmit={submit}>
        <input ref={textTitle} type="text" placeholder="Color Title..." />
        <input ref={hexColor} type="color" />
        <button>Add</button>
      </form>
    </div>
  );
}
```

Controlled forms with useState

[[3 - Hooks#useState Hook]]

Same example with useState:
```JSX
function App() {
  const [title, setTitle] = useState("");
  const [color, setColor] = useState("#000000");

  const submit = (e) => {
    e.preventDefault();
    console.log(`${title}, ${color}`);
    //Reset values after change
    setTitle("");
    setColor("#000000");
  };

  return (
    <div className="App">
      <form onSubmit={submit}>
        <input
          value={title}
          onChange={(event) => setTitle(event.target.value)}
          type="text"
          placeholder="Color Title..."
        />
        <input
          value={color}
          onChange={(event) => setColor(event.target.value)}
          type="color"
        />
        <button>Add</button>
      </form>
    </div>
  );
}
```

Or use [[3 - Hooks#Custom Hook]]

# Predefined forms

- [Formik Docs](https://formik.org/)
- [React hook form](https://react-hook-form.com/)
- [useHooks() - not forms specific](https://usehooks.com)
- 





React hook form

use hooks (not form specifric)