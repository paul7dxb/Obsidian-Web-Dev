
- Includes custom components
	- [[Card]]
	- [[CustomButton]]

ErrorModal.js:
```JSX
import React from "react";
import Card from "./Card";
import Button from "./Button";

import styles from "./ErrorModal.module.css";

const ErrorModal = (props) => {
  return (
    <div>
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
    </div>
  );
};

export default ErrorModal;

```

ErrorModal.module.css:
```CSS
.backdrop {
    position: fixed;
    top: 0;
    left: 0;
    width: 100%;
    height: 100vh;
    z-index: 10;
    background: rgba(0, 0, 0, 0.75);
  }
  
  .modal {
    position: fixed;
    top: 30vh;
    left: 10%;
    width: 80%;
    z-index: 100;
    overflow: hidden;
  }
  
  .header {
    background: #4f005f;
    padding: 1rem;
  }
  
  .header h2 {
    margin: 0;
    color: white;
  }
  
  .content {
    padding: 1rem;
  }
  
  .actions {
    padding: 1rem;
    display: flex;
    justify-content: flex-end;
  }
  
  @media (min-width: 768px) {
    .modal {
      left: calc(50% - 20rem);
      width: 40rem;
    }
  }
  
```

## Usage

- Example project:
	- [Udemy React Create User](https://github.com/paul7dxb/react-udemy-course/tree/master/react-create-user-app)
- The error state variable handles wether the modal should show or not
- Set as null until an error is found on the input validation
- When the error is not null the && condition in the render will cause the JSX after the && to be rendered. See [[JS#JS && "Trick"|JS && conditional trick]] 

NewUser.js:
```JSX
import React, { useState } from "react";
import ErrorModal from "../UI/ErrorModal";

...

const NewUser = (props) => {
	const [error, setError] = useState();
	
	  const addUserHandler = (event) => {
	    event.preventDefault();
	
	    //Username Validation
	    if (username.trim().length === 0) {
	      setError({
	        title: "Empty Input Field",
	        message: "Ensure all fields are completed",
	      });
	      return;
	    }
	    ...

  const errorHandler = () => {
    setError(null)
  }

  
  return (
    <div>
      {error && <ErrorModal title={error.title} message={error.message} onConfirm={errorHandler} />}
      <Card className="input">
      ...

  
```



