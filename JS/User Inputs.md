# Check not empty string or white space

```js
    if(enteredValue.trim().length === 0){
      setIsValid(false);
      return;
    }
```

# readline-sync

```JS
const readline = require("readline-sync");

function getMaxValueFromUser() {
	console.log("Please enter the max value to go to:");
	const response = readline.prompt();

	// Validate input
	let convertedInput = parseInt(response)
	while (!Number.isInteger(convertedInput) && convertedInput <= 0){
		console.log("Please enter a valid number");
		console.log("Please enter the max value to go to:");
		const response = readline.prompt();
		convertedInput = parseInt(response)
	}
	
	return convertedInput
}
```

# Command Line inputs

```JS
process.argv.forEach(function (val, index, array) {
	console.log(index + ": " + val);
});
```