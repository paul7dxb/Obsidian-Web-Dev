- Used to trigger functions
- [[2 - States#Button Clicks|Button Click Theory]]
- Event listeners will pass an event value through to the called function
	- event has values:
		- target (DOM element that called it)
		- value (holds current value of object)
		- `event.target.value`
			- Always returns as a String

# onCLick

- Button click listener

# onChange

- Executes same as onInput but this will also work for other non input types (e.g a dropdown selection)

```JSX
const ExpenseForm = () => {
	const [enteredTitle, setEnteredTitle] = useState('');
	
	const titleChangeHandler = (event) => {
		setEnteredTitle(event.target.value);
	}
	
	...
	
	<input type="text" onChange={titleChangeHandler}/>
```

# onSubmit

- Used with [[Semantic Markup#Form|HTML Form]]
- Usually will want to disable page refresh when used in React using
- Make use of [[2 - States|States]]

```JSX
const ExpenseForm = () => {
  const [enteredTitle, setEnteredTitle] = useState("");
  const [enteredAmount, setEnteredAmount] = useState("");
  const [enteredDate, setEnteredDate] = useState("");


  const titleChangeHandler = (event) => {
    setEnteredTitle(event.target.value);
  };

  const amountChangeHandler = (event) => {
    setEnteredAmount(event.target.value);
  };

  const dateChangeHandler = (event) => {
    setEnteredDate(event.target.value);
  };

  const submitHandler = (event) => {
    event.preventDefault();
    const expenseData = {
      title: enteredTitle,
      amount: enteredAmount,
      date: new Date(enteredDate),
    };

    console.log(expenseData);
  };

  return (
    <form onSubmit={submitHandler}>
```

