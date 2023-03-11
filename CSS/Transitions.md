# Transitions

```css
transition: property time timing-function delay 
transition: 1s;
transition: var(--transitionTime) ease-out;
```

## Swap between CSS values
```css
.transition-2 {
    position: fixed;
    top: 0;
    left: -100%;
    width: 100%;
    bottom: 0;
    z-index: 101;
    background-color: var(--primary);
    transition: var(--transitionSideTime) ease-out;
}

.transition-2.is-active {
	left: 0;
}
```

- Timing function: 
	- The timing of the transition 
		- linear - even
		- ease in - slow to fast
		- esae out
		- step
		- cubic-bezier - reverse in the middle for short time
			- easeings.net for timings

# Fly In From Top

```CSS
.Modal {
    transition: all 0.3s ease-out;
}

.ModalOpen {
    opacity: 1;
    transform: translateY(0);
}
.ModalClosed {
    opacity: 0;
    transform: translateY(-100%);
}
```