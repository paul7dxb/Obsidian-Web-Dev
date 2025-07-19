n.toString()

# Check for an odd digit in a number

```JS
function solution(n) {
	return !(n+'').match(/[13579]/)
}
```


# Binary to String Conversions

```JS
function dec2bin(dec) {
  // return (dec).toString(2);
  return (dec).toString(2);
}

function bin2dec(bin) {
  return parseInt(bin, 2)
}
```