- Store token for logged in user so they can authorise themselves on future actions

- Storage options
	- Local storage
		- Using browser features

- Create utility function to get the token for requests that require a token

```JS
export function getAuthToken() {
  const token = localStorage.getItem("token");

  const tokenDuration = getTokenDuration();

  if (!token) {
    return null;
  }

  if (tokenDuration < 0) {
    return "EXPIRED";
  }

  return token;
}
```