# List IAM users

```cmd
aws iam list-users
```

# Stress EC2 Instance

- Stress EC2 instances to test ASG
- [Git Link](https://gist.github.com/mikepfeiffer/d27f5c478bef92e8aff4241154b77e54)

# Dry Run

- Run command to see if the correct IAM permissions are assigned
- Will give errors:
	- UnauthorizedOperation
		- Don't have permissions
	- DryRunOperation
		- Have permissions but dry run flag set so no execution

Example for creating EC2 instance

```bash
aws ec2 run-instances --dry-run --image-id ami-0d76271a8a1525c1a --instance-type t2.micro
```

## Decode CLI STS

- Use STS command line
- [CLI reference](https://docs.aws.amazon.com/cli/latest/reference/sts/decode-authorization-message.html)

```bash
sts decode-authorization-message --encoded-message <pasted message>
```

# CLI Profiles

- Default links to an AWS account

- User profile

```cmd
aws configure --profile other-aws-account
Access key
Secret Access key
eu-west-2

```

- New account is in config
- Switch between accounts
	- Execute command using other account by adding `--profile other-aws-account`

- List profiles
```
aws configure list-profiles
```

- Run command as other profile
```bash
aws s3 mb s3://<bucket-name> --profile default
```

# DynamoDB CLI

- [[Deployments/AWS/Guides/Serverless/DynamoDB#DynamoDB CLI|DynamoDB CLI commands]]

# S3 commands

```bash
# Create bucket
aws s3 mb s3://<bucket-name> --profile default

# Delete all files in bucket
aws s3 rm s3://<your-bucket-name> --recursive
```


# Install nano

```shell
sudo yum install nano
```