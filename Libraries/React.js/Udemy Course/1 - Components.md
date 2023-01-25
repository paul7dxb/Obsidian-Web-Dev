# Components

- Capital letters like in a class name
- Components are just a JS function
	- Held in a JS file where a function is exported
	- Imported by the app.js file
	- Added to render
- Only one root element per return statement
	- Due to `React.createElement()` function having first argument as HTML type (e.g div)

# Styling

## Linking CSS to Component

- Create .css file in components (conventionally same name as component)
- Use **className** instead of class in JSX

```jsx
import './ExpenseItem.css';

function ExpenseItem() {
  return (
    <div className='expense-item'>
```

# Dynamic Data

- Receive data from somewhere and then output

## Props

- (Properties)
- Used to pass data to custom components
- Used attribute in the component

App.js
```jsx
import ExpenseItem from "./components/ExpenseItem";

function App() {
  const expenses = [
    {
      id: "e1",
      title: "Toilet Paper",
      amount: 94.12,
      date: new Date(2020, 7, 14),
    },
    { id: "e2", title: "New TV", amount: 799.49, date: new Date(2021, 2, 12) },
    {
      id: "e3",
      title: "Car Insurance",
      amount: 294.67,
      date: new Date(2021, 2, 28),
    },
    {
      id: "e4",
      title: "New Desk (Wooden)",
      amount: 450,
      date: new Date(2021, 5, 12),
    },
  ];

  return (
    <div>
      <h2>Let's get started!</h2>
      <ExpenseItem
        title={expenses[0].title}
        amount={expenses[0].amount}
        date={expenses[0].date}
      />
```

ExpenseItem.js
```JSX
function ExpenseItem(props) {

  return (
    <div className='expense-item'>
      <div>{props.date.toISOString()}</div>
      <div className='expense-item__description'>
        <h2>{props.title}</h2>
        <div className='expense-item__price'>${props.amount}</div>
      </div>
    </div>
  );
}

export default ExpenseItem;
```

# Nesting Components (aka Composition)

- Makes application more manageable
- Make child components to make up other components
- Ensure correct props are passed (funneling data through components)

## Use Custom Component as Wrapper

- children reserved
	- Allows code to be inserted between tags letting component "wrap it"
- Content between opening and closing tags of component
- Add classNames to custom component by reaching into props

Card.js
```jsx
import './Card.css'

function Card(props){
    const classes = 'card ' + props.className; 
    return(
        <div className={classes}>{props.children}</div>
    )
}

export default Card;
```

ExpenseItem.js
```JSX
import Card from './Card';

function ExpenseItem(props) {

  return (
    <Card className='expense-item'>
```

# Arrow Function

- Arrow functions can be used for the creation of Components instead of the regular funciton call
- [[Next Gen Features#Arrow Functions|Arrow Functions Obsidian Notes]]
- [Arrow Functions MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Functions/Arrow_functions)

Both are equivalent:
```JSX
const Card = (props) => {
	...
}


function Card(props){
	...
}
```


# Resources

- [[1 - Creating Components|Linked In Learning Components]]
- [Udemy Course Git Notes and Code](https://github.com/academind/react-complete-guide-code/tree/03-react-basics-working-with-components)
