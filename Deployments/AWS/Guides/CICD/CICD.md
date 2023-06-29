# Common Misconfigurations

- GitHub Actions
	- Don't use AWS_ACCESS_KEY_IS / AWS_SECRET_ACCESS_KEY
	- Use OIDC
		- Token signed by github to AWS
			- Belongs to repo in brach
			- Temporary credential