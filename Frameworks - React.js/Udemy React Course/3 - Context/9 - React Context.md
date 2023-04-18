

![[Image_React_State.png]]
![[Image_React_Context_Diagram.png]]

- Helps avoid having to use props being sent through multiple components

- Create store solder under src
- Create a JS file to store the data
- Set default state
	- Usually an object

![[Image_React_Context_Structure.png]]

auth-context.js:
```JS
import React from "react";

const AuthContext = React.createContext({isLoggedIn: false});

export default AuthContext
```

- Use this to wrap the are it is needed with AuthContext.Provider
	- If needed throughout app wrap App.js

App.js:
```JSX
//Value for provider is passed down to all consumers
  return (
    <AuthContext.Provider value={{isLoggedIn: isLoggedIn}}>
      <MainHeader onLogout={logoutHandler} />
      <main>
        {!isLoggedIn && <Login onLogin={loginHandler} />}
        {isLoggedIn && <Home onLogout={logoutHandler} />}
      </main>
    </AuthContext.Provider>
  );
}
```

# Disadvantages

![[Image_React_Context_Disadvantages.png]]

- For high frequency changes use a flux based system like [[18 - Redux|Redux]]

# Consuming

## Option 1: Consumer Function
- To consume (access)
	- requires AuthContext.Consumer
	- Takes a child that is a function with argument being context data
	- Move normal component return into function which now has access to context from parameter

```JSX
import AuthContext from "../../store/auth-context";

const Navigation = (props) => {
  return (
    <AuthContext.Consumer>
      {(ctx_) => {
        return (
          <nav className={classes.nav}>
            <ul>
              {ctx_.isLoggedIn && (
                <li>
                  <a href="/">Users</a>
                </li>
              )}
              {ctx_.isLoggedIn && (
                <li>
                  <a href="/">Admin</a>
                </li>
              )}
              {ctx_.isLoggedIn && (
                <li>
                  <button onClick={props.onLogout}>Logout</button>
                </li>
              )}
            </ul>
          </nav>
        );
      }}
    </AuthContext.Consumer>
  );
};
```

## Option 2: useContext Hook

- Avoids function calls
- Create useContext constant in consumer file
- Access constant (ctx) in component as required

```JSX
import React, { useContext } from "react";
import AuthContext from "../../store/auth-context";

const Navigation = (props) => {
  const ctx = useContext(AuthContext);

  return (
    <nav className={classes.nav}>
      <ul>
        {ctx.isLoggedIn && (
          <li>
            <a href="/">Users</a>
          </li>
        )}
        {ctx.isLoggedIn && (
          <li>
            <a href="/">Admin</a>
          </li>
        )}
        {ctx.isLoggedIn && (
          <li>
            <button onClick={props.onLogout}>Logout</button>
          </li>
        )}
      </ul>
    </nav>
  );
};

export default Navigation;
```

# Forwarding a Function In Context

- Send reference to function
```JSX
  return (
    <AuthContext.Provider value={{isLoggedIn: isLoggedIn, onLogout: logoutHandler}}>
```

# Custom Context Provider

- Useful to contain functions related to context use
	- E.g authentication could contain loginHandlers etc.
- Allows you to strip the functions out of the parent component that had the code there previously

auth-context.js
```JS
import React, { useState, useEffect } from "react";

const AuthContext = React.createContext({
  isLoggedIn: false,
  onLogout: () => {},
  onLogin: (email, password) => {},
});

export const AuthContextProvider = (props) => {
  const [isLoggedIn, setIsLoggedIn] = useState(false);

  useEffect(() => {
    const storedUserLoggedInInformation = localStorage.getItem("isLoggedIn");
    if (storedUserLoggedInInformation === "1") {
      setIsLoggedIn(true);
    }
  }, []);

  const logoutHandler = () => {
    localStorage.removeItem("isLoggedIn");
    setIsLoggedIn(false);
  };

  const loginHandler = () => {
    localStorage.setItem("isLoggedIn", "1");
    setIsLoggedIn(true);
  };
  return (
    <AuthContext.Provider
      value={{
        isLoggedIn: isLoggedIn,
        onLogout: logoutHandler,
        onLogin: loginHandler,
      }}
    >
      {props.children}
    </AuthContext.Provider>
  );
};

export default AuthContext;

```

- Wrap the App ceated at root with the context provider
	- Cleans up App.js

index.js
```JS
const root = ReactDOM.createRoot(document.getElementById("root"));
root.render(
  <AuthContextProvider>
    <App />
  </AuthContextProvider>
);
```

Implement context in child components as required
```JSX
const Navigation = () => {
  const ctx = useContext(AuthContext);

  return (
    <nav className={classes.nav}>
      <ul>
        {ctx.isLoggedIn && (
          <li>
            <a href="/">Users</a>
          </li>
        )}
        {ctx.isLoggedIn && (
          <li>
            <a href="/">Admin</a>
          </li>
        )}
        {ctx.isLoggedIn && (
          <li>
            <button onClick={ctx.onLogout}>Logout</button>
          </li>
        )}
      </ul>
    </nav>
  );
};
```

# React Context Limitations

- Strit usage of components
	- E.g button
	- Using state would be better for flexibility in unctionality
- Not optimised for high frequency changes
	- For app wide high frequency use Redux


# Example Cart

Example used in: [React food order demo](https://github.com/paul7dxb/react-udemy-course/tree/master/react-food-order-app)

## Non Dynamic setup

- Add store folder
![[Image_React_Context_Structure 1.png]]
![[Image_React_Context_Structure_cart.png]]
- Create cart-context.js
- values are just placeholders for autocompletion

```JS
import React from "react";

const CartContext = React.createContext({
  items: [],
  totalAmount: 0,
  addItem: () => {},
  removeItem: () => {},
});

export default CartContext;
```

- Create Provider to hold context functions and dynamic data eventually

CartProvider.js
```JSX
import CartContext from "./cart-context";

const CartProvider = (props) => {
  const addItemHandler = (item) => {};
  const removeItemHandler = (id) => {};

  const cartContext = {
    items: [],
    totalAmount: 0,
    addItem: addItemHandler,
    removeItem: removeItemHandler,
  };

  return (
    <CartContext.Provider value={cartContext}>
      {props.children}
    </CartContext.Provider>
  );
};

export default CartProvider;

```

- Wrap context needing components

App.js
```JSX
  return (
    <CartProvider>
      {cartIsShown && <Cart onClose={hideCartHandler} />}
      <Header onShowCart={showCartHandler} />
      <main>
        <Meals />
      </main>
    </CartProvider>
  );
}
```

## Count cart items

- Use useContext() to get closest provider
- Use [[Array Functions#Array.reduce()|reduce()]] to total up the amount of each item

```JS
const HeaderCartButton = (props) => {
  //Gets provider used by closest provider
  const cartCtx = useContext(CartContext);
  const numberOfCartItems = cartCtx.items.reduce((curNumber, item) => {}, 0);1
```

