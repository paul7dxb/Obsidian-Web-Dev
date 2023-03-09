# Transition Component

- Poroperties
	- in
		- Wether the wrapped elements will be shown
	- timeout
		- How long animation will be played from entering to entered and exiting to exited
		- Defining shorter than the animation play time will result in animation being cut short
	- mountOnEnter
		- If in property is true then add element to the DOM
	- unmountOnExit
		- If in property is false then remove element from the DOM
		- Removed after given timeout period

- Gives a state property
	- States of transition
		- ENTERING
		- ENTERED
		- EXITING
		- EXITED

# Modal Example

- Parent
```JSX
        <Modal show={this.state.modalIsOpen} closed={this.closeModal} />
```

- Component:
```JSX
import React from "react";
import Transition from "react-transition-group/Transition";

import "./Modal.css";

const animationTiming = {
  enter: 400,
  exit: 600
}

const modal = (props) => {
  const cssClasses = [
    "Modal",
    props.show === "entering"
      ? "ModalOpen"
      : props.show === "exiting"
      ? "ModalClosed"
      : null,
  ];

  return (
    <Transition in={props.show} timeout={animationTiming} mountOnEnter unmountOnExit>
      {(state) => {
        const cssClasses = [
          "Modal",
          state === "entering"
            ? "ModalOpen"
            : state === "exiting"
            ? "ModalClosed"
            : null,
        ];
        return (
          // rendered components
          <div className={cssClasses.join(" ")}>
            <h1>A Modal</h1>
            <button className="Button" onClick={props.closed}>
              Dismiss
            </button>
          </div>
        );
      }}
    </Transition>
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



