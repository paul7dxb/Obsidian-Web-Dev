useCallback()

- Store a function across component execution
	- Save the function and avoid recreating it on each execution
	- Prevents the issue with prop function references in [[#State Change Render Component]]

## Usage

- Wrap the setting state with the useCallback function

```js
const toggleParagraphHandler = useCallback(() => {
	//arror function in setFunction as dealing with a live state
	setShowParagraph((prevShowParagraph) => !prevShowParagraph);
}, [])
```

- When component is rerendered the useCallback tells react to look back for the old function to use
- Second Argument is the dependencies of the function
	- Empty means no dependencies so the same function component should be used on each render

- When there are more arguments involved you must be aware of the  [[Functions#Functions are Closures|function's closure]]