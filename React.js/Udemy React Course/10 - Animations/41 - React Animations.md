# Limitations of CSS animations and transitions

- animated divs may still be visible in the DOM
	- All HTML is displayed in the DOM
	- Bad for performance
	- Bad for accessibility

- Rendering conditionally will remove item from DOM
	- Animations will be stopped if item is removed from DOM

# Packages

- [[1 - ReactTransitionGroup|ReactTransitionGroup]]
	- Lets you use the packages components to work with React's management of the DOM
- React Motion
	- Emulates real world physics using start and end state by interpolation
	- Natural animation look
- React Move
	- Two components (single or groups)
	- Objects describing states of animation
	- Build complex animations
	- Sorting for graphs animation
- React-router-transition
	- Animations between different routes
	- AnimatedSwitch Component