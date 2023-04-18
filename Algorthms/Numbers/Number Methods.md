n.toString()

# Check for an odd digit in a number

```JS
function solution(n) {
	return !(n+'').match(/[13579]/)
}
```