# Create Roles for CodeDeploy

- IAM
- Roles
- Create Role
- Use cases for other AWS Services
	- CodeDeploy
- Next
- Next
- Name Role (CodeDeployServiceRoleForEC2)
- Create Role

- Create Role
- EC2
- Search S3
	- AmazonS3ReadOnlyAccess
- Next
- Name Role(EC2RoleForCodeDeploy)
- Create Role

# Create Application

- CodeDeploy
- Create Application
- Compute Platform
	- EC2
- Create Application
- Create Deployment Group
	- Make EC2 Instance first:
		- EC2 console
		- Launch instance
			- Allow SSH and Web traffic
			- Tags
				- Environment : Development
			- Role
				- EC2RoleForCodeDeploy
		- Connect to EC2 instance (SSH or connect)
		- Install CodeDeploy Agent

```bash
#!/bin/bash

# Installing CodeDeploy Agent
sudo yum update
sudo yum install ruby

# Download the agent (replace the region if it doesn't work)
wget https://aws-codedeploy-eu-west-3.s3.eu-west-3.amazonaws.com/latest/install
chmod +x ./install
sudo ./install auto # Install CodeDeploy Agent
sudo service codedeploy-agent status #Check service is running
```

- CodeDeploy
- Create Deployment Group
- Name
	- EC2 instances
	- Use tag
		- Environment : Development (or environment of group)
- Disable / Enable Load balancer

# Create Deployment

- Create Deployment
- Put application in S3
	- Copy S3 URI
		- (s3://bucket-name/SampleApp_Linux.zip)
- Paste in S3 URI
- Create Deployment

# Lifecycle Events

- CodeDeploy
- Deployments
- Select deployment
- Deployment Lifecycle Events

# TroubleShooting

- Signature expired: time earlier than time
	- Make sure CodeDeploy and EC2 time matches

- Check log files on EC2 instance
	- /opt/codedeploy-agent