JavaScript library for building user interfaces.

isolated pieces of code called “components”.

TicTacToe Example
https://codepen.io/papapps/pen/ZEjBxrP

# Changing Component State

```js
class Square extends React.Component {
  constructor(props) {
    super(props);
    this.state = {
      value: null,
    };
  }

  render() {
    return (
      <button className="square" onClick={() => console.log('click')}>
        {this.props.value}
      </button>
    );
  }
}
```

Chrome/Firefox extension can view React component treee in dev tools

# Get components to share information
- Declare shared state in parent component

## Immutable Objects for data
https://reactjs.org/tutorial/tutorial.html#function-components
- Easier to detect need to rerender
- Can Maintain history of changes

Using immutable data changes to make it easier for REact to know when to rerender componenents


# Function Component
https://reactjs.org/tutorial/tutorial.html#function-components

Components that only contain a render function

```js
class Square extends React.Component {
  render() {
    return (
      <button className="square" onClick={() => this.props.onClick()}>
        {this.props.value}
      </button>
    );
  }
}
```

Becomes:
```js
function Square(props){
  return (
  <button className="square" onClick={props.onClick}> {props.value} </button>
  )
}
```

