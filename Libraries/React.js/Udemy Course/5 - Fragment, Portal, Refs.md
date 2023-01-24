
- Renders empty [[Wrapper|Wrapper Component]]


```JSX
import React from "react";
<React.Fragment>

</React.Fragment>

```

or

```JSX
import {Fragment} from "react";
<Fragment>

</Fragment>
```

or

```JSX
<>

</>
```

# Portal

- Rendered HTML looks different to acheive cleaner DOM output
- Write components in same way

## Usage

- Add to index.html with an id

```html
  <body>
    <noscript>You need to enable JavaScript to run this app.</noscript>
    <div id="backdrop-root"></div>
    <div id="overlay-root"></div>
    <div id="root"></div>
```


- Let React know that they are portals

old ErrorModal.js:
```JSX
import React from "react";
import Card from "./Card";
import Button from "./Button";

import styles from "./ErrorModal.module.css";

const ErrorModal = (props) => {
  return (
    <React.Fragment>
      <div onClick={props.onConfirm} className={styles.backdrop}></div>
      <Card className={styles.modal}>
        <header className={styles.header}>
          <h2>{props.title}</h2>
        </header>
        <div className={styles.content}>
          <p>{props.message}</p>
        </div>
        <footer className={styles.actions}>
          <Button onClick={props.onConfirm} >Okay</Button>
        </footer>
      </Card>
    </React.Fragment>
  );
};

export default ErrorModal;
```

- Move JSX elements their own components

New ErrorModal.js:
```JSX
import React from "react";
import Card from "./Card";
import Button from "./Button";

import styles from "./ErrorModal.module.css";

const Backdrop = (props) => {
  return <div className={styles.backdrop} onClick={props.onConfirm}></div>;
};

const ModalOverlay = (props) => {
  return (
    <Card className={styles.modal}>
      <header className={styles.header}>
        <h2>{props.title}</h2>
      </header>
      <div className={styles.content}>
        <p>{props.message}</p>
      </div>
      <footer className={styles.actions}>
        <Button onClick={props.onConfirm}>Okay</Button>
      </footer>
    </Card>
  );
};

const ErrorModal = (props) => {
  return (
  <React.Fragment>
    {}
  </React.Fragment>
  );
};

export default ErrorModal;

```

Import React-DOM

```js
import ReactDOM from "react-dom";
```

Create portal using JSX and where compoent goes in DOM

```JSX
const ErrorModal = (props) => {
  return (
  <React.Fragment>
    {ReactDOM.createPortal( <Backdrop onConfirm={props.onConfirm}/>,document.getElementById("backdrop-root")  )}
    {ReactDOM.createPortal( <ModalOverlay title={props.title} message={props.message} onConfirm={props.onConfirm} />,document.getElementById("overlay-root")  )}
  </React.Fragment>
  );
};
```

# Refs

- For reading values without wanting to change anything refs are better than [[2 - States#useState|useState]] as they are lighter weight and less code
- Access DOM elements and work with them
- Managing data instead of using useState()

- First time React gets to the DOM element it will set the value to the current DOM element

```JSX
import React, { useRef } from "react";

const NewUser = (props) => {
  const nameInputRef = useRef();
  const ageInputRef = useRef();

  const addUserHandler = (event) => {
    event.preventDefault();
    const enteredUsername = nameInputRef.current.value;
    const enteredAge = ageInputRef.current.value;

    props.onAddUser({
      id: Math.random().toString(),
      username: enteredUsername,
      age: enteredAge,
    });

    nameInputRef.current.value = "";
    ageInputRef.current.value = "";
  };
  
  return (
  <Card className="input">
	<form onSubmit={addUserHandler}>
	  <label>Username</label>
	  <input ref={nameInputRef} type="text" placeholder="username" />
	  <label>Age (in years)</label>
	  <input ref={ageInputRef} type="text" placeholder="Age" />
	  <Button type="submit">Add User</Button>
	</form>
  </Card>
  );
};
```

- The useRef() will be an onject with the current prop which will hold the DOM node. NOT A REFERENCE.
- This means that you can directly manipulate the DOM although it is not recommended to do it outside.
- Access values with variableName.current.value

- If you need to manipulate the DOM (resetting input value)


# Uncontrolled Components

**Uncontrolled**
- Internal state not controlled by React
	- E.g setting value using a useRef()

Controlled
- Internal state controlled by React
	- E.g using useState to track keystrokes and update the value of the input field
	- All managed by react without accessing DOM elements and setting directly