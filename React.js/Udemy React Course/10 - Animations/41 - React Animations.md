# Limitations of CSS animations and transitions

- animated divs may still be visible in the DOM
	- All HTML is displayed in the DOM
	- Bad for performance
	- Bad for accessibility

- Rendering conditionally will remove item from DOM
	- Animations will be stopped if item is removed from DOM