# CLI Access Key

# Configure Profile for user

- User
- Security Credentials
- Access Key
- Create Access Key
- CLI
- aws configure
- Access Key
- Secret Key

```cmd
aws configure --profile userprod
```

## List Profiles

```cmd
aws configure list-profiles
```


# List IAM users
```cmd
aws iam list-users --profile default
```

# EC2 Roles to use CLI

- Amazon linux comes with amazon cli
- Do not enter IAM access keys into an EC2 instance
- Use IAM roles
	- EC2 instances
	- Actions
	- Update IAM role
	- Assign role