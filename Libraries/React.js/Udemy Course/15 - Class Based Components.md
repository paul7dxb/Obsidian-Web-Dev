
- Functional Components are the most common and recent approach
- Class  used to have be used < 16.8 as functional components couldn't change state or sideEffects
	- Until React Hooks were introduced
	- Class based CANNOT use hooks

- It is possible to mix and match functional / class based but not recommended
	- Usuallly in migration of older projects

![[Image_React_Class_Based.png]]

# Equivalent Component Creation:

```JSX
import classes from './User.module.css';

import { Component } from 'react';
//Component adds props property accessed by this.props

//Class based
class User extends Component {
  render(){
    return <li className={classes.user}>{this.props.name}</li>
  }
}

//Funcitonal Component
const User = (props) => {
  return <li className={classes.user}>{props.name}</li>;
};

export default User;
```


# Managing State with Class Component

- Initialise and define state
	- In constructor
	- Class based state is ALWAYS and object named state
- Update when needed
	- Updated using this.setState() method
	- Takes an object that merges with existing state

```JS
class Users extends Component {

  constructor(){
    super()
    this.state = {
      showUsers: true,
      moreState: 'Test',
      nested: {}
    }
  }

  toggleUsersHandler() {
    this.setState((curState) => ({showUsers: !curState.showUsers}))
  }
  
```

- Calling a method in the Class render method
	- Due to the `this` keyword in JS. See [Link](https://academind.com/tutorials/this-keyword-function-references)
	- Solution is to bind to the method

```JSX
  render(){

      const usersList = (
    <ul>
      {DUMMY_USERS.map((user) => (
        <User key={user.id} name={user.name} />
      ))}
    </ul>
  );
    
    return (
      <div className={classes.users}>
        <button onClick={this.toggleUsersHandler.bind(this)}>
          {this.state.showUsers ? 'Hide' : 'Show'} Users
        </button>
        {this.state.showUsers && usersList}
      </div>
    );
  }
}

export default Users;
```

# Component Lifecycle

![[Image_React_Class_Lifecycle_Methods.png]]

- componentDidMount()
	- Called when component is mounted
	- Equivalent to useEffect(... ,\[\]) - with no dependancies
- componentDidUpdate()
	- Equivalent to useEffect(... ,\[someValue\]) - with dependancies
	- Need to check which properties are updated to avoid infinite updating loops
- componentWIllUnmount()
	- Called just before component is unmounted

## componentDidUpdate()

```JS
  componentDidUpdate(prevProps, prevState) {
    //Use if statement to avoid infinite loop of updating
    if (prevState.searchTerm != this.state.searchTerm) {
      this.setState({
        filteredUsers: DUMMY_USERS.filter((user) =>
          user.name.includes(this.state.searchTerm)
        ),
      });
    }
  }
```

# Class Based Context

- Only can connect to one context
	- Unless using JSX method

```JS
class UserFinder extends Component {
  //Can only be set once
  static contextType = UsersContext;

  constructor() {
    super();
    this.state = {
      filteredUsers: [],
      searchTerm: "",
    };
  }

  componentDidMount() {
    // Send http request...
    this.setState({ filteredUsers: this.context.users });
  }

 componentDidUpdate(prevProps, prevState) {
    if (prevState.searchTerm !== this.state.searchTerm) {
      this.setState({
        filteredUsers: this.context.users.filter((user) =>
          user.name.includes(this.state.searchTerm)
        ),
      });
    }
  }
```

# Error Boundaries

- Errors between one part and another
- Server not responding not getting complete request leading to error

- try catch won't work in handling in a parent component
	- Error is generated in JSX code
- Requires Error Boundary
	- [Udemy Lecture](https://www.udemy.com/course/react-the-complete-guide-incl-redux/learn/lecture/25599736#questions/15088318)

- Component named ErrorBoundary
	- Contains componentDidCatch()
	- At the moment this does not exist in functional components

```JS
import React, { Component } from "react";

class ErroryBoundary extends Component {
  constructor() {
    super();
    this.state = { hasError: false };
  }

  componentDidCatch(error) {
    //error check logic
    console.log(error);
    this.setState({ hasError: true });
  }

  render() {
    if (this.state.hasError) {
      return <p> Something Went Wrong! </p>;
    }
    return this.props.children;
  }
}

export default ErroryBoundary;
```

## componentDidCatch()

- Triggered when a child component throws an error
- Wrap child components with ErrorBoundary wrapper

Parent:
```JSX
<ErroryBoundary>
	<Users users={this.state.filteredUsers} />
</ErroryBoundary>
```

Child:
```JSX
class Users extends Component {

  constructor(){
    super()
    this.state = {
		...
    }
  }
  
  componentDidUpdate() {
    // try {
    //   someCodeWhichMightFail()
    // } catch (err) {
    //   // handle error
    // }
    if (this.props.users.length === 0) {
      throw new Error('No users provided!');
    }
  }
```