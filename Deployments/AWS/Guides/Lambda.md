- [[22.0 - Lambda|Lambda Notes]]

# CLI Invoke Lambda synchronous function

```bash
# List Lambda function by region
aws lambda list-functions --region eu-west-1

# LINUX / MAC
aws lambda invoke --function-name demo-lambda --cli-binary-format raw-in-base64-out --payload '{"key1": "value1", "key2": "value2", "key3": "value3" }' --region eu-west-2 response.json

# WINDOWS POWERSHELL
aws lambda invoke --function-name demo-lambda --cli-binary-format raw-in-base64-out --payload '{\"key1\": \"value1\", \"key2\": \"value2\", \"key3\": \"value3\" }' --region eu-west-1 response.json

# WINDOWS CMD
aws lambda invoke --function-name demo-lambda --cli-binary-format raw-in-base64-out --payload "{""key1"":""value1"",""key2"":""value2"",""key3"":""value3""}" --region eu-west-1 response.json
```

# CLI Invoke Lambda asynchronous function

```bash
# LINUX / MAC
aws lambda invoke --function-name demo-lambda --cli-binary-format raw-in-base64-out --payload '{"key1": "value1", "key2": "value2", "key3": "value3" }' --invocation-type Event --region eu-west-1 response.json

# WINDOWS POWERSHELL
aws lambda invoke --function-name demo-lambda --cli-binary-format raw-in-base64-out --payload '{\"key1\": \"value1\", \"key2\": \"value2\", \"key3\": \"value3\" }' --invocation-type Event --region eu-west-1 response.json

# WINDOWS CMD
aws lambda invoke --function-name demo-lambda --cli-binary-format raw-in-base64-out --payload "{""key1"":""value1"",""key2"":""value2"",""key3"":""value3""}" --invocation-type Event --region eu-west-1 response.json
```

# Destinations

- Create queues to be destinations
	- e.g SQS
- Lambda function
	- Add destination with condition
	- Permissions should be added to IAM role of the lambda function automatically
		- Write to SQS queue with specified name

# Lambda Environment Variables

- Create lambda function
- Import os
```python
import os

def lambda_handler(event, context):
    return os.getenv("ENVIRONMENT_NAME")
```
- Read in variable
- Function configuration
	- Environment variables
	- Edit
	- Add key value pair 
		- (e.g ENVIRONMENT_NAME : dev)

# Enable X Ray Tracing

- Function
- Configuration
- Monitoring and operations tools
- Edit
	- Enable X-Ray tracing
		- Permissions will add automatically (`AWSXRayDaemonWriteAccess`)

# Create Security Group For Lambda function In VPC

## Create Security Group for Lambda
- EC2
- Security Group
- Create security Group

### Give Permissions to function to 
- Lambda
- Configuration
- Permissions
- Role
- Add permissions
- Add policy
- `## AWSLambdaENIManagementAccess`

## Add Functions to VPC
- Lambda
- VPC
- Edit
- Choose subnet
- Use created security group

# Add Lambda Layer

- Function
- Layers
- Add Layer
	- Choose package
	- Call import in function code

- [[CDK Lambda Layers]]

# Create Version

- Lambda function
- Action 
- Publish new version

# Create Alias

- Create a version
- Configuration
- Create Alias

# Allow CORS

```JS
exports.handler = async (event) => {
    console.log(`EVENT: ${JSON.stringify(event)}`);
    return {
        statusCode: 200,
    //  Headers to enable CORS requests
     headers: {
         "Access-Control-Allow-Origin": "*",
         "Access-Control-Allow-Headers": "*"
     },
        body: JSON.stringify('Hello from Lambda!'),
    };
};
```

# Lambda Node with package

- https://repost.aws/knowledge-center/lambda-deployment-package-nodejs