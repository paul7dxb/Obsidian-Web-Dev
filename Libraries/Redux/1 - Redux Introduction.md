- State Management System or cross component or app wide state
- Only ever have **ONE** store
	- Central Data (State) Store
- - Components subscribe to central store

![[Image_Redux_Diagram.png]]

# Getting Data

- Components subscribe to the store to get a "silce" of the store

# Setting Data

- Components NEVER directly manipulate the store data
- Reducer function is responsible for mutating the store data
	- Not a useReducer hook
	- Take input and transform input to create a new output (a general programming concept)
- Components dispath (trigger) Actions to describe action reducer should perform
	- Redux forwards actions to reducer
	- Reads type of operration
	- Reducer performs operation
	- Reducer spits out a new state
	- Relevant components notified of update


# Basic set up

- In a new empty folder
- Creates package.json
- Install redux
	- For react install [[#React Redux]]

```bash
npm init -y
npm install redux
```

## Import redux

```JS
const redux = require('redux');
```

# Create Store

```JS
const store = redux.createStore();
```

# Create Reducer Function
- Create Function and add to store

```JS
const counterReducer = (state = {counter: 0}, action) => {
    return {
        counter: state.counter + 1
    }
}

const store = redux.createStore(counterReducer);
```

# Create Subscription
- Access with store.getState() for latest state snapshot after it is updated

```JS
const counterSubscriber = () => {
    const latestState = store.getState();
}
```

- Let the Redux know bout subscriber function
- Subscribe the subscriber function to the store

```JS
store.subscribe(counterSubscriber);
```


# Create Action

- Use dispatch
	- Set type for action with a unique string for desired action

```JS
store.dispatch({type: 'increment' })
```

- Handle actions in reducer

```JS
const counterReducer = (state = { counter: 0 }, action) => {
  if (action.type === "increment") {
    return {
      counter: state.counter + 1,
    };
  }
  return state;
};
```

# Final output

```JS
const redux = require("redux");

const counterReducer = (state = { counter: 0 }, action) => {
  if (action.type === "increment") {
    return {
      counter: state.counter + 1,
    };
  }
  if (action.type === "decrement") {
    return {
      counter: state.counter - 1,
    };
  }
  return state;
};

const store = redux.createStore(counterReducer);

const counterSubscriber = () => {
  const latestState = store.getState();
  console.log(latestState);
};

store.subscribe(counterSubscriber);

store.dispatch({ type: "increment" }); //Output { counter: 1 }
store.dispatch({ type: "decrement" }); //Output { counter: 0 }

```


# Using Redux With React

- Makes connecting react to redux simpler
	- Components to Store subscription

```bash
npm install react-redux
```

- More details and examples found from React Udemy Course notes:
	- [[18 - Redux]]
	- [[19 - Redux Toolkit]]
	- [[20 - Redux Side Effects]]