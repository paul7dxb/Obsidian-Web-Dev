- Used to let React know which [[1 - Components|components]] will need to be re rendered on data changes
	- React will ususlaly just render from root down once.
	- Need to tell React that something has changed and needs to be reevaluated
- Add event listeners not in the . Use prop element
	- E.g: Button click event
		- Select by id
		- add click listenter
	- Use special `on` props (e.g onClick)

- [[12 - React under the hood#State Rendering|How state works with rendering]]


# Button Clicks

- Use onClick prop
- Pass pointer to desired dunction to `onClick` prop.
- Convention functions will end `Handler` (optional)

```JSX
function ExpenseItem(props) {
  const clickHandler = () => {
    console.log("clicked");
  };
  return (
    <Card className="expense-item">
        <h2>{props.title}</h2>
      <button onClick={clickHandler}>Change Title</button>
    </Card>
  );
}
```

- Without state this would have no effect as it will have already been rendered

# Hooks

- Used to update the state of the app

## useState

- Must call useState function directly inside the component function (not in nested function)
- Requires defualt state value
- Returns value and a function to assign the variable
	- Use [[JS#Destructuring Arrays|array destructuring]]
- Convention
	- `const [name, setName] = useState(defaultVal)`

```jsx
import React, { useState } from 'react'

function ExpenseItem(props) {
	//Set inside component and not nested further
	//Use array destructuring to store returned Array
  const [title, setTitle] = useState(props.title);

  const clickHandler = () => {
    setTitle("Updated Value")
  };

  return (
    <Card className="expense-item">
      <ExpenseDate date={props.date} />
      <div className="expense-item__description">
        <h2>{title}</h2>
        <div className="expense-item__price">${props.amount}</div>
      </div>
      <button onClick={clickHandler}>Change Title</button>
    </Card>
  );
}
```

- When the set funciton is called the parent component is executed again
	- Re evaluates component values in re render
	- New states created for each independent instance of the component
- The update is 'scheduled' for change and may not change straight away
	- console log on next line will likely contain old value

# Group Together States

- Use the [[Next Gen Features#Spread|Spread operator]] to ensure other values are not lost when updating one value
- Ensure to follow approach of [[#Updating State that depends on Previous State]]

# Updating State that depends on Previous State

- Due to scheduled updates not being performed instantly
- Use a function call to ensure the action is performed on the most recent state

```jsx
const ExpenseForm = () => {
  const [userInput, setUserInput] = useState({
    enteredTitle: "",
    enteredAmount: "",
    enteredDate: "",
  });

  const titleChangeHandler = (event) => {
  //Use function call in handler to make sure most recent state is used
    setUserInput((prevState) => {
      return { ...userInput, enteredTitle: event.target.value };
    });
  };
```

# Two Way Binding

- Listen to changes
- Feed the state back into the input
- Useful with forms to gather input and also change it as required

```JSX
const ExpenseForm = () => {
    
  const [enteredTitle, setEnteredTitle] = useState("");

  const titleChangeHandler = (event) => {
    setEnteredTitle(event.target.value);
  };

  const submitHandler = (event) => {
    event.preventDefault();
    const expenseData = {
      title: enteredTitle,
		//..other values
    };

    console.log(expenseData);
    //Able to reset value after submit as input value={enteredTitle}
    setEnteredTitle("");
  };

  return (
    <form onSubmit={submitHandler}>
        <div>
          <label>Title</label>
          <input type="text" value={enteredTitle} onChange={titleChangeHandler} />
```

# Pass data from Child to Parent (Bottom-Up)

[Udemy Lecture on Bottom-Up](https://www.udemy.com/course/react-the-complete-guide-incl-redux/learn/lecture/25596020#overview)


- Send a function to a child component in a function
- Let the child pass the data in to the function in the child component

In Parent:
- Create function for handler
- Add pointer to function as prop in child tag within parent component
- Use the function inside child component
	- Get props in componet call
	- This will usually be the "onSomeActionHappened(valueToGoUp)" function

Parent File:
```JSX
const NewExpense = () => {
  const saveExpenseDataHandler = (enteredExpenseData) => {
    const expenseData = {
      ...enteredExpenseData,
      id: Math.random().toString(),
    };
    console.log("parent got data");
    console.log(expenseData);
  };

  return (
    <div className="new-expense">
      <ExpenseForm onSaveExpenseData={saveExpenseDataHandler} />
    </div>
  );
};
```

Child file:
```JSX
const ExpenseForm = (props) => {

	//Function called by component to collect data and send to parent
  const submitHandler = (event) => {
    event.preventDefault();
    const expenseData = {
      title: enteredTitle,
      amount: enteredAmount,
      date: new Date(enteredDate),
    };
	//Parent function passed in from props
    props.onSaveExpenseData(expenseData);

  };
  return (
    <form onSubmit={submitHandler}>
      <div>
		// Form items to collect
      </div>
      <div>
        <button type="submit">Add Expense</button>
      </div>
    </form>
  );
```

# Lifting the State Up

- Passing data between siblings
- Used via the closest shared parent component
- Use [[#Pass data from Child to Parent (Bottom-Up)|Bottom-UP]] to get data to parent and then pass down through props to required component

# Managing States

## Controlled Components

- When a parent controls a child component and child passes data back
	- aka statefull component
- Uses two way binding [[2 - States#Two Way Binding]]
- Stateless component
	- Only output
	- aka dumb component
	- aka presentation component

# Resources

- [Module Git code and slides](https://github.com/academind/react-complete-guide-code/tree/04-react-state-events)
