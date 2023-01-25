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