https://aws.amazon.com/certification/certified-developer-associate/

# Practice Exams

- Free
	- https://awslagi.com/course/aws-certified-developer-associate-dva-c02-practice-exam/lessons/aws-certified-developer-associate-dva-c02-practice-exam-part-1/
- Paid
	- https://awslagi.com/course/aws-certified-developer-associate-dva-c02-actual-exam/
# Ports
- 21 FTP
- 22 SSH
- 22 SFTP
- 3389 RDP


# EC2 Purchasing

- On demand
	- Pay by the second
	- Short workloads
	- Highest cost but no upfront
- Reserved Instances (1 & 3 years)
	- For long workloads
	- Reserve Instance type
	- Payment options (no upfront, partial, all upfront)
	- Convertible Reserved Instances
		- Allow to change over time
- Saving Plan (1 & 3 years)
	- Commit to amount of usage instead of instance type
	- Locked to instance type in a region
	- Can vary instance size
- Spot Instances
	- Short workloads, cheap but can lose instances
	- Define a spot price to work at. If it goes over you lose the instance
	- Most cost efficient
- Dedicated Hosts
	- Entire physical server 
	- Most expensive
	- Used with specific BYOL (bring your own license)
	- Meeting compliances
- Deicated Instances
	- Own instance on own hardware
- Capacity Reservations
	- Reserve on demand instances in a specific AZ for any duration
	- No discount, only to make sure you get the capacity
	- Charged by running instances or not

![[AWS_Dedicated_Host_Vs_Instance.png]]

- Hotel analogy
![[AWS_Hotel_Analogy.png]]


# RDS

- Read replica Asynchronous
- Multi AZ synchronous

- Elasticache Redis Cluster maximum 5 read replicas when cluster mode disabled

# 

- You have a Classic ECS cluster that you want to enable IAM roles for your ECS tasks so that they can make API requests to AWS services. Which ECS configuration option should you enable in `/etc/ecs/ecs.config`?

- `ECS_ENABLE_TASK_IAM_ROLE`

# CloudWatch

- CloudWatch Alarm set on a High-Resolution Custom Metric can be triggered as often as **10 seconds**
- CloudWatch Logs, Log Retention Policy defined at **Log Groups** level.

# SAM

- SAM is built on CloudFormation  
- SAM requires the Transform and Resources sections  
- Commands to know:  
- `sam build`: fetch dependencies and create local deployment artifacts  
- `sam package`: package and upload to Amazon S3, generate CF template  
- `sam deploy`: deploy to CloudFormation  
- SAM Policy templates for easy IAM policy definition  
- SAM is integrated with CodeDeploy to do deploy to Lambda aliases

# Cognito

## Cognito User Pools vs Identity Pools  ]

- Cognito User Pools (for authentication = identity verification) 
	- Database of users for your web and mobile application  
	- Allows to federate logins through Public Social, OIDC, SAML...  
	- Can customize the hosted UI for authentication (including the logo)  
	- Has triggers with AWS Lambda during the authentication flow  
	- Adapt the sign-in experience to different risk levels (MFA, adaptive authentication, etc...)  

- Cognito Identity Pools (for authorization = access control)  
	- Obtain AWS credentials for your users  
	- Users can login through Public Social, OIDC, SAML & Cognito User Pools  
	- Users can be unauthenticated (guests)  
	- Users are mapped to IAM roles & policies, can leverage policy variables  

- CUP + CIP = authentication + authorization

# S3 Force SSL

- IAM policy condition
	- `aws:SecureTransport`

# Things to revisit

- CICD
- AWS CLI commands
- SDK
- Containers / ECS = docker
- Kinesis