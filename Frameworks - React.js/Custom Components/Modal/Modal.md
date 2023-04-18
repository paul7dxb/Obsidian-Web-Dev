- Pop up message box overlay for screen

# Modal with React Portal

Example used in: [React food order demo](https://github.com/paul7dxb/react-udemy-course/tree/master/react-food-order-app)
![[Image_React_Modal_Example.png]]

Note:
- Handler are passed through layers as props instead of using context
	- This allows for multiple implementations of the modal

- Create div in index.html for overlays to be rendered in with [[5 - Fragment, Portal, Refs#Portal|portal]]

```html
    <noscript>You need to enable JavaScript to run this app.</noscript>
    <div id="overlay"></div>
    <div id="root"></div>
```
- Create Modal with portal references

modal.js
```jsx
import React, { Fragment } from "react";
import ReactDOM from "react-dom"; //For Portal

import classes from "./Modal.module.css";

const Backdrop = (props) => {
  return <div onClick={props.onClose} className={classes.backdrop} />;
};

const ModalOverlay = (props) => {
  return (
    <div className={classes.modal}>
      <div className={classes.content}>{props.children}</div>
    </div>
  );
};

const portalElement = document.getElementById("overlay");

const Modal = (props) => {
  return (
    <Fragment>
      {ReactDOM.createPortal(<Backdrop onClose={props.onClose}/>, portalElement)}
      {ReactDOM.createPortal(
        <ModalOverlay> {props.children} </ModalOverlay>,
        portalElement
      )}
    </Fragment>
  );
};

export default Modal;


```

- Use Modal.js to create your more specifiuse modal

Cart.js
```JSX
import React from "react";
import classes from "./Cart.module.css";
import Modal from "../UI/Modal";

const Cart = (props) => {
  const cartItems = (
    <ul className={classes["cart-items"]}>
      {[{ id: "c1", name: "Sushi", amount: 2, price: 12.99 }].map((item) => (
        <li>{item.name}</li>
      ))}
    </ul>
  );
  return (
    <Modal onClose={props.onClose}>
      {cartItems}
      
      <div className={classes.total}> 
        <span>Total Amount</span> 
        <span>£25.52</span> 
        </div>
      <div className={classes.actions}>
        <button onClick={props.onClose} className={classes["button--alt"]}>Close</button>
        <button className={classes.button}>order</button>
      </div>
    </Modal>
  );
};

export default Cart;

```

- In appropriate app component handle the showing / hiding of the modal

App.js
```JSX
function App() {

  const [cartIsShown, setCartIsShown] = useState(false);

  const showCartHandler = () => {
    setCartIsShown(true)
  }

  const hideCartHandler = () => {
    setCartIsShown(false)
  }

  return (
    <Fragment>
      {cartIsShown && <Cart onClose={hideCartHandler} />}
      <Header onShowCart={showCartHandler} />
      <main>
        <Meals />
      </main>
    </Fragment>
  );
}

export default App;
```

## Styling

Modal.module.css
```CSS
.backdrop {
    position: fixed;
    top: 0;
    left: 0;
    width: 100%;
    height: 100vh;
    z-index: 20;
    background-color: rgba(0, 0, 0, 0.75);
  }
  
  .modal {
    position: fixed;
    top: 20vh;
    left: 5%;
    width: 90%;
    background-color: white;
    padding: 1rem;
    border-radius: 14px;
    box-shadow: 0 2px 8px rgba(0, 0, 0, 0.25);
    z-index: 30;
    animation: slide-down 300ms ease-out forwards;
  }
  
  @media (min-width: 768px) {
    .modal {
      width: 40rem;
      left: calc(50% - 20rem);
    }
  }
  
  @keyframes slide-down {
    from {
      opacity: 0;
      transform: translateY(-3rem);
    }
    to {
      opacity: 1;
      transform: translateY(0);
    }
  }
```

Cart.module.css
```CSS
.cart-items {
    list-style: none;
    margin: 0;
    padding: 0;
    max-height: 20rem;
    overflow: auto;
  }
  
  .total {
    display: flex;
    justify-content: space-between;
    align-items: center;
    font-weight: bold;
    font-size: 1.5rem;
    margin: 1rem 0;
  }
  
  .actions {
    text-align: right;
  }
  
  .actions button {
    font: inherit;
    cursor: pointer;
    background-color: transparent;
    border: 1px solid #8a2b06;
    padding: 0.5rem 2rem;
    border-radius: 25px;
    margin-left: 1rem;
  }
  
  .actions button:hover,
  .actions button:active {
    background-color: #5a1a01;
    border-color: #5a1a01;
    color: white;
  }
  
  .actions .button--alt {
    color: #8a2b06;
  }
  
  .actions .button {
    background-color: #8a2b06;
    color: white;
  }
  
```