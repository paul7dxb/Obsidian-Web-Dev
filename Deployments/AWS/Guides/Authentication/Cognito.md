# Cognito to API
- Create user pool
	- Implicit grant allows access to token instead of code when authorising
- Create Hosted UI
	- Get to hosted UI through the connected app's "app client" link
- login
	- Get code
	- Change code to token
- Add authentic

- Testing:
	- API agateway auth test
		- Use `id token`
	- Make request with `Authorization` header set to `id token` value
		- Or whatever header value is used in API authorizer