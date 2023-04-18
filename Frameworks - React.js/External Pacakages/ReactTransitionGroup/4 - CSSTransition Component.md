- Doesn't use function in between tags unlike [[2 - Transition Component|Transittion]]
	- Makes managing the CSS classes used a lot easier and not have to join classname in the JS
- Requires an additional property classNames
	- Which CSS classes should be added to element depending on transition state

- Appends class names to "trunk" depending on state of animation:
	- myClass-enter
		- Starts entering
		- Removed after 1 frame
	- myClass-enter-active
		- Whilst in entering mode
	- myClass-exit
		- Start exiting
		- Removed after 1 frame
	- myClass-exit-active
		- While in exiting mode

- Can also use appear and appearActive classes for first time animation of hardcoded elements


# Modal Example

- Same example as [[2 - Transition Component#Modal Example]]

Component:
```JSX
import React from "react";
import CSSTransition from "react-transition-group/CSSTransition";

import "./Modal.css";

const animationTiming = {
  enter: 400,
  exit: 900,
};

const modal = (props) => {
  return (
    <CSSTransition
      in={props.show}
      timeout={animationTiming}
      mountOnEnter
      unmountOnExit
      classNames="fade-slide"
    >
      {/* // rendered components */}
      <div className="Modal">
        <h1>A Modal</h1>
        <button className="Button" onClick={props.closed}>
          Dismiss
        </button>
      </div>
    </CSSTransition>
  );
};

export default modal;

```

CSS:
```CSS
.Modal {
  position: fixed;
  z-index: 200;
  border: 1px solid #eee;
  box-shadow: 0 2px 2px #ccc;
  background-color: white;
  padding: 10px;
  text-align: center;
  box-sizing: border-box;
  top: 30%;
  left: 25%;
  width: 50%;
  transition: all 0.3s ease-out;
}

.fade-slide-enter {
  /* Any initiisation required before active animation */
}

.fade-slide-enter-active {
  animation: openModal 0.4s ease-out forwards;
}
.fade-slide-exit {
  /* Any initiisation required before active animation */
}

.fade-slide-exit-active {
  animation: closeModal 0.8s ease-out forwards;
}

@keyframes openModal {
  0% {
    opacity: 0;
    transform: translateY(-100%);
  }
  50% {
    opacity: 1;
    transform: translateY(20%);
  }
  100% {
    opacity: 1;
    transform: translateY(0);
  }
}
@keyframes closeModal {
  0% {
    opacity: 1;
    transform: translateY(0%);
  }
  50% {
    opacity: 0.8;
    transform: translateY(60%);
  }
  100% {
    opacity: 0;
    transform: translateY(-100%);
  }
}

```


# Modal Example Custom CSS Classnames

- Can use an object in order to set custom names

```JS
import React from "react";
import CSSTransition from "react-transition-group/CSSTransition";

import "./Modal.css";

const animationTiming = {
  enter: 400,
  exit: 900,
};

const modal = (props) => {
  return (
    <CSSTransition
      in={props.show}
      timeout={animationTiming}
      mountOnEnter
      unmountOnExit
      // classNames="fade-slide"
      classNames={{
        enter: '',
        enterActive: 'ModalOpen',
        exit: '',
        exitActive: 'ModalClosed'
      }}
    >
      {/* // rendered components */}
      <div className="Modal">
        <h1>A Modal</h1>
        <button className="Button" onClick={props.closed}>
          Dismiss
        </button>
      </div>
    </CSSTransition>
  );
};

export default modal;

```

```CSS
.Modal {
  position: fixed;
  z-index: 200;
  border: 1px solid #eee;
  box-shadow: 0 2px 2px #ccc;
  background-color: white;
  padding: 10px;
  text-align: center;
  box-sizing: border-box;
  top: 30%;
  left: 25%;
  width: 50%;
  transition: all 0.3s ease-out;
}

.ModalOpen {
  animation: openModal 0.4s ease-out forwards;
}
.ModalClosed {
  animation: closeModal 0.8s ease-out forwards;
}

@keyframes openModal {
  0% {
    opacity: 0;
    transform: translateY(-100%);
  }
  50% {
    opacity: 1;
    transform: translateY(20%);
  }
  100% {
    opacity: 1;
    transform: translateY(0);
  }
}
@keyframes closeModal {
  0% {
    opacity: 1;
    transform: translateY(0%);
  }
  50% {
    opacity: 0.8;
    transform: translateY(60%);
  }
  100% {
    opacity: 0;
    transform: translateY(-100%);
  }
}

```