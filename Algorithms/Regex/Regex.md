# Creation
- forward slashes / /
	- Escape the / with a \\ if required
- Object `new RegExp(pattern[, flags])`

```JS
var regexLiteral = /abc/;
var regexConst = new RegExp('abc');
```

# Website to Create Expressions

- [regexr.com](https://regexr.com/)
- [MDN Cheat Sheet](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Regular_expressions/Cheatsheet)

# Regex Testing

```JS
function checkValidPostcode(postcode) {
	var regex = /^([A-Z]{1,2}[0-9]{1,2}[A-Z]? ?[0-9][A-Z]{2})$/g;
	return regex.test(postcode);
}
```