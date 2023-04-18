## useEffect()
```JS
useEffect(() -> {...}, [ dependencies]);
```
- Function that is executed AFTER component evaluation IF specified dependecies have changed
	- Avoids infinite loops that could be created using setting a useState which causes rerender
- Dependecies will be considered change on first render so function willl run on initial render
	- No dependencies will only trigger useEffect funciton on first run

Reducers
- Managing more Complex States

Context
- Managing App-Wide or Coponet-Wide state
- Makes sharing state and state updates across components easier

## Maintaining loggedIn State

- Persist reload storing in localStorage
	- In production use cookies
- Use function with no dependencies so it will only run on first run
- The data access to localStroage is a 'side effect'

```JSX
import React, { useEffect, useState } from "react";

import Login from "./components/Login/Login";
import Home from "./components/Home/Home";
import MainHeader from "./components/MainHeader/MainHeader";

function App() {
  const [isLoggedIn, setIsLoggedIn] = useState(false);

  useEffect(() => {
    const storedUserLoggedInInformation = localStorage.getItem("isLoggedIn");
    if (storedUserLoggedInInformation === "1") {
      setIsLoggedIn(true);
    }
  }, []);

  const loginHandler = (email, password) => {
    // We should of course check email and password
    // But it's just a dummy/ demo anyways
    localStorage.setItem("isLoggedIn", "1");
    setIsLoggedIn(true);
  };

  const logoutHandler = () => {
    localStorage.removeItem('isLoggedIn');
    setIsLoggedIn(false);
  };

  return (
    <React.Fragment>
      <MainHeader isAuthenticated={isLoggedIn} onLogout={logoutHandler} />
      <main>
        {!isLoggedIn && <Login onLogin={loginHandler} />}
        {isLoggedIn && <Home onLogout={logoutHandler} />}
      </main>
    </React.Fragment>
  );
}

export default App;
```

# Debouncing

- Use a timer to limit the rate a funciton is called
	- E.g on user input check after they stop typing for a small amount of time instead of firing on every key entry
	- Clear other timers when starting a new one

- When used with useEffect() the return function is first called which can be used to clear any timer

```js
  useEffect(() => {
    const identifier = setTimeout(() => {
      console.log("setting validity");
      setFormIsValid(
        enteredEmail.includes("@") && enteredPassword.trim().length > 6
      );
    }, 500);

    return () => {
      console.log("cleanup");
      clearTimeout(identifier);
    };
  }, [enteredEmail, enteredPassword]);
```
