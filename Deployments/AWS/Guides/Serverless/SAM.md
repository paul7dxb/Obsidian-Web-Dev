# CLI Install

- [AWS instructions](https://docs.aws.amazon.com/serverless-application-model/latest/developerguide/install-sam-cli.html)

# Simple Deployment From CLI

```bash
# Create S3 Bucket
aws s3 mb s3://<bucket-name>

# Package CloudFormation
# Can use 'sam package'
aws cloudformation package --s3-bucket <bucket-name> --template-file template.yaml --output-template-file gen/template-generated.yaml --profile default

# Deploy
aws cloudformation deploy --template-file '<filepath>\template-generated.yaml' --stack-name <stack-name> --capabilities CAPABILITY_IAM --profile default
```

# Deploy with SAM

- From: https://docs.aws.amazon.com/serverless-application-model/latest/developerguide/serverless-getting-started-hello-world.html

```bash
# Step 1 - Download a sample application
sam init --runtime python3.9

# Step 2 - Build your application
cd sam-app
sam build

# Step 3 - Package your application
sam deploy --guided
```

# CodeDeploy Canary

```YAML
Properties:
	...
  AutoPublishAlias: live

  DeploymentPreference:
   Type: Canary10Percent10Minutes 
```