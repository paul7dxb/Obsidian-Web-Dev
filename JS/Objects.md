# Returning Objects Shorthand

- I returning objects with the same name, e.g:

```JS
  return {
    isLoading: isLoading,
    error: error,
    sendRequest: sendRequest
  }
```

You can also write the equivalent:

```JS
  return {
    isLoading,
    error,
    sendRequest
  }
```