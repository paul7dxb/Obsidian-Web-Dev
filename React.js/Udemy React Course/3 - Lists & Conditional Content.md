

Instead of making a hardcoded list e.g
```JSX
      <ExpenseItem
        title={expenses[0].title}
        amount={expenses[0].amount}
        date={expenses[0].date}
      />
      <ExpenseItem
        title={expenses[1].title}
        amount={expenses[1].amount}
        date={expenses[1].date}
      />
```


```JSX
{props.items.map((expense) => (
<ExpenseItem
  key={expense.id}
  title={expense.title}
  amount={expense.amount}
  date={expense.date}
/>
))}
```

# Stateful Lists

- Like with variables React will not know to rerender a change. See [[2 - States|States]]
- Can still use `useState`

```JSX
const DUMMY_EXPENSES = [
	//....data
];

function App() {
	//useState to keep track of data
  const [expenses, setExpenses] = useState(DUMMY_EXPENSES);
	//Handle data change
  const addExpenseHandler = (expense) => {
    setExpenses((prevExpenses) => {
      return [expense, ...prevExpenses];
    });
  };

  return (
    <div>
      <NewExpense onAddExpense={addExpenseHandler} />
      <Expenses items={expenses} />
    </div>
  );
}

export default App;
```

# Keys

- Without it when an item is added all items are rerendered with new data
	- new element created at end but new data put in first element. Old first data now rendered in second element etc.
	- Poor for performance
	- Introduce bugs when using state changes
- Key prop lets react identify individualitems

Define own key:
```JSX
  {props.items.map((expense) => (
	<ExpenseItem
	  key={expense.id}
	  title={expense.title}
	  amount={expense.amount}
	  date={expense.date}
	/>
```

# Conditional Content

- Can use conditionals to choose between displaying different content
- [[JSX#JSX Conditionals]]
	- Can use [[JS#Conditional (ternary) operator]]
	- Can use && operator
	- Preferred: Can store content in a variable outside of component return and perform usual conditional JS statements on data
	- Have two different return cases
		- Only really useful where WHOLE return statement is different, not just a part

Variable stored outside component return:
```JSX
  let expensesContent = <p>No expenses found.</p>

  if (filteredExpenses.length > 0){
    expensesContent = filteredExpenses.map((expense) => (
      <ExpenseItem
        key={expense.id}
        title={expense.title}
        amount={expense.amount}
        date={expense.date}
      />
    ))
  }

  return (
    <Card className="expenses">
      <ExpensesFilter
        selected={filteredYear}
        onChangeFilter={filterChangeHandler}
      />
      {expensesContent}
    </Card>
  );
```

Two different return cases:
```jsx
function ExpensesList(props) {

  if (props.items.length === 0) {
    return <p>No expenses found.</p>;
  }

  return (
    <ul className="expenses-list">
      {props.items.map((expense) => (
        <ExpenseItem
          key={expense.id}
          title={expense.title}
          amount={expense.amount}
          date={expense.date}
        />
      ))}
    </ul>
  );
}

export default ExpensesList;
```