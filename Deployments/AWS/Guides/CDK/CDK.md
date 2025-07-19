# Intro

- Levels
	- 1 - Cloudformation 1:1
	- 2 - Improved L1 with helper methods and defaults
	- 3 - Combinations of constructs

- Assets
	- Files bundled into the apps
		- Docker, lambda handlers
		- Get output to cdk.out
- Bootstrapping
	- Creates S3 bucket to store assets

- Aspects
	- Apply an operation to all constructs in a given scope
		- e.g all buckets to be encrypted

# Commands

|Command| Description|
| --- | --- |
|npm install -g aws-cdk-lib |Install the CDK CLI and libraries
|cdk init app |Create a new CDK project from a specified template
|cdk synth |Synthesizes and prints the CloudFormation template
|cdk bootstrap |Deploys the CDK Toolkit staging Stack
|cdk deploy |Deploy the Stack(s)
|cdk diff |View differences of local CDK and deployed Stack
|cdk destroy |Destroy the Stack(s)
| cdk deploy --hotswap | Drift Cloudformation instead of redeploying (dev) |
| cdk deploy --outputs-file \<filename> | Output Stack outputs to a file |

- May require npx and --profile
	- `npx cdk deploy --profile default`

# New App

```bash
cdk init sample-app --language typescript

```

# Deploy stack from CDK

- Can be done from cloudshell

```Shell
# 1. install the CDK
sudo npm install -g aws-cdk-lib

# directory name must be cdk-app/ to go with the rest of the tutorial, changing it will cause an error
mkdir cdk-app
cd cdk-app/

# initialize the application
cdk init app --language javascript
# verify it works correctly
cdk ls
# Should return CdkAppStack

# 2. copy the content of cdk-app-stack.js into lib/cdk-app-stack.js


# 3. setup the Lambda function
mkdir lambda && cd lambda
touch index.py

# 4. bootstrap the CDK application
# install Create CDK toolkit
# Once per region per account
cdk bootstrap

# 5. (optional) synthesize as a CloudFormation template
cdk synth


# 6. deploy the CDK stack
cdk deploy

# 7. empty the s3 bucket
# 8. destroy the stack
cdk destroy
```

# CDK Watch

- Monitors code and assets for changes
	- Attempts to deploy changes automatically
- Default uses `--hotswap`
	- Disable with `cdk watch --no-hotswap`

- Watched files determined by the `cdk.json` file

```JSON
{
  "app": "python3 app.py",
  "watch": {
    "include": [
      "**"
    ],
    "exclude": [
      "README.md",
      "cdk*.json",
      ...
```