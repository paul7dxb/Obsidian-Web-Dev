# Input validation

```JS
function isSafeUsername(username) {
    const regex = new RegExp(/^[a-z0-9]+$/i);
    return regex.test(username);
}
```

# Libraries

- DOMPurify library

# JSX Sanitisation

- Input in JSX will automatically escape HTML & JS

# Further measures
Content security policies (CSPs) can also be configured to help mitigate XSS attacks. The script-src component of the Content-Security-Policy HTTP header can be set to block the execution of inline JavaScript, or you can allow JavaScript to be loaded from trusted domains exclusively.

If the React application has been created with Create-React-App (CRA), the environment variable INLINE_RUNTIME_CHUNK should be set to false to ensure React can still function properly.

This can be used to restrict an attacker's ability to launch a successful XSS attack but should be used in addition to proper input validation and output encoding – not relied on as the only measure to mitigate XSS.
