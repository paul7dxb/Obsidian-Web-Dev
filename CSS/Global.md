- Used to access globally defined
- animate.css package

App.css
```CSS
@import "animate.css";
...
```

Animate Cards using the animate.css fadeIn animation:

Card.module.css
```CSS
.card{
	...
    opacity: 0;
}

/* Use global */
.card :global{
    animation: fadeIn 1.5s forwards;
	animation-delay: 0.1s; 
}

/* Can use defined lengths */
.card :global{
    animation: fadeIn var(--animationDurationMedium) forwards;
	animation-delay: var(--animationDelayMedium); 
}

/* OR */
.card{
	...
    opacity: 0;
    &:global{
	    animation: fadeIn 1.5s forwards;
		animation-delay: 0.1s; 
	}
}
```