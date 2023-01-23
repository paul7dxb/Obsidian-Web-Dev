
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

