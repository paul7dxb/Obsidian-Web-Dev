# Passing Output

# ResultSelector

- Only pass out part of the output

```JSON
{
  "bookingRef.$": "$.Payload.bookingRef"
}
```

## ResultPath

- Combine input with the output
	- Combine original input with result

```JSON
$.bookingRef
```