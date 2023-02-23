
- For basic information on Redux see [[1 - Redux Introduction]]
- Use react-redux to make connecting components to store simpler

![[Image_React_Redux_Reducers.png]]

# Setup

# Create Store in Src Folder

![[Image_React_Redux_Store_Structure.png]]

store/index.js:
```JS
import { createStore } from redux

const counterReducer = (state = {counter:0}, action) => {
    if (action.type === 'increment'){
        return {
            counter : state.counter + 1
        }
    }
    if (action.type === 'decrement'){
        return {
            counter : state.counter - 1
        }
    }
    return state;
}

const store = createStore(counterReducer) 

export default store;
```

# Provide Store

- import provider component from react-redux
- Similar to provider components with react context
- Import store from store/index.js file and provide it to the Provider

root/index.js:
```JS
import React from 'react';
import ReactDOM from 'react-dom/client';
import {Provider} from 'react-redux'


import './index.css';
import App from './App';
import store from './store/index'

const root = ReactDOM.createRoot(document.getElementById('root'));
root.render(<Provider store={store}> <App /></Provider>);

```

# React-Redux Hooks

## Get data with useSelector()

- Custom hooks provided by react-redux to reach in to redux store
- useSelector()
	- Used to get data
	- Requires function for peice of data to extrract from store
		- Get a slice from the store
	- Automatically sets subscription to the data in the store
	- Changes cause component to rerender
	- Unmounting component manages unsubscribing component removed

E.g to get counter
```JS
import { useSelector } from "react-redux";

const counter = useSelector(state => state.counter);
//Can now reference counter in component
```

# Dispatch Actions

- useDispatch() Hook
	- Returns a function that you can execute
	- Dispatches action against redux store

```JS
  const dispatch = useDispatch();

  const incrementHandler = () => {
    dispatch({type: 'increment'});
  }

    return (
        <button onClick={incrementHandler}>Increment</button>
	)
```

all together to compare to class based:
```JSX
import classes from "./Counter.module.css";
import { useDispatch, useSelector} from "react-redux";

const Counter = () => {
  const dispatch = useDispatch();
const counter = useSelector(state => state.counter);

  const toggleCounterHandler = () => {};

  const incrementHandler = () => {
    dispatch({type: 'increment'});
  }
  const decrementHandler = () => {
    dispatch({type: 'decrement'});
  }

  return (
    <main className={classes.counter}>
      <h1>Redux Counter</h1>
      <div className={classes.value}>{counter} </div>
      <div>
        <button onClick={incrementHandler}>Increment</button>
        <button onClick={decrementHandler}>Decrement</button>
      </div>
      <button onClick={toggleCounterHandler}>Toggle Counter</button>
    </main>
  );
};

export default Counter;
```
# Class based Redux

- Use connect as cannot use hooks like in funcional components
- Change export to use connect
	- Connect returns new value as a value which executes again using component as argument
	- Works as a Higher Oreder Component
	- Takes two arguemnts
		- mapStateToProps
			- Returns keys available in class as props
			- Similar to useSelector() hook
		- mapDispatchToProps
			- Props that can be executed as a function
				- When executed dispatch an action to the store
			- Equivalent to useDispatch() hook
			- Return object where keys are prop names with value a function calling dispatch

```JSX
import classes from "./Counter.module.css";
import { connect } from "react-redux";
import { Component } from "react";

class Counter extends Component {
  incrementHandler() {
    this.props.increment();
  }
  decrementHandler() {
    this.props.decrement();
  }
  toggleCounterHandler() {}

  render() {
    return (
      <main className={classes.counter}>
        <h1>Redux Counter</h1>
        <div className={classes.value}> {this.props.counter} </div>
        <div>
          <button onClick={this.incrementHandler.bind(this)}>Increment</button>
          <button onClick={this.decrementHandler.bind(this)}>Decrement</button>
        </div>
        <button onClick={this.toggleCounterHandler}>Toggle Counter</button>
      </main>
    );
  }
}

const mapStateToProps = (state) => {
  return {
    counter: state.counter
  };
};

const mapDispatchToProps = (dispatch) => {
  return {
    increment: () => dispatch({ type: "increment" }),
    decrement: () => dispatch({ type: "decrement" }),
  };
};

export default connect(mapStateToProps, mapDispatchToProps)(Counter);
```

# Passing values into actions

- Pass variable into action to give more flexibility
- Dispatch ation has a type & also a payload of data

Component Dispatches:
```JS
  const increaseHandler = () => {
    dispatch({type: 'increase', amount: 5});
  }
```

Store action:
```JS
    if (action.type === 'increase'){
        return {
            counter : state.counter + action.amount
        }
    }
```

# Redux State

- Reducer doesn't merge states, it replaces it
- Always set all other states when updating a state
- Do not mutate existing state
	- Overwrite by retuning a brand new object
	- https://academind.com/tutorials/reference-vs-primitive-values/
	- Can lead to bugs in bigger applications where state can get out of sync
- For larger apps look to use [[19 - Redux Toolkit|Redux Toolkit]] to make work easier