![[whenToCatchError.png]]

- Throwing an exception
	- Errors bubble up the "call stack"
	- Something in the call stack can catch the exception
	- If the exception reaches the top it can crash application (program will end)
	- Ending the program may be the best option
		- Catch fixable problems (user input again)
	- 

# JS Try Catch

- https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/try...catch

```JS
try {
	//Do something
} catch (error) {
	// Add details for diagnosis or error
	console.error(
		"There has been a problem with the [attempted action]:",
		error
	);
	// If unable to fix error throw the error
	throw error
} finally {
	// Always run this part regardless of error or not 
}
```