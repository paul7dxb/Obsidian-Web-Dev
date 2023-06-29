https://aws.amazon.com/certification/certified-developer-associate/

# Practice Exams

- Free
	- https://awslagi.com/course/aws-certified-developer-associate-dva-c02-practice-exam/lessons/aws-certified-developer-associate-dva-c02-practice-exam-part-1/
- Paid
	- https://awslagi.com/course/aws-certified-developer-associate-dva-c02-actual-exam/
	- https://portal.tutorialsdojo.com/product/aws-certified-developer-associate-practice-exams/
	- https://www.whizlabs.com/aws-developer-associate/

# RCU WCU
R - Read
W - Write

# Auth

- Social Identity Providers (IdP)
	- OpenID

- Web Identity Fedartion error `AccessDenied -- Not authorized to perform sts:AssumeRoleWithWebIdentity`
	- Incorrectly defined authenticated **principal role trust policy**
	- Set in the `amr` of the token

- OpenID -> AWS creds
	- `GetID` to get Cognito ID
	- `GetCredentialsForIdentity` with the Cognito ID to get temporary credentials

- Unauthentiated access to a service using SDK
		- Requires AWS security if performing `AssumeRole`
			- Create IAM role and Cognito Identity Pool
			- Use role for unauthenticated identities
				- CIP gives temporary credentials
			- https://docs.aws.amazon.com/cognito/latest/developerguide/cognito-identity.html

- Attribute Based Access Control (ABAC)
	- Use **Tag key for principal**
		- `"s3:ExistingObjectTag/department" : "${aws:PrincipalTag/department}"`

- Lambda Authorizer
	- API -> caller's identity -> Lambda -> returns IAM policy
	- Token or request-parameter based

# Staging

- Integrate stage variables into lambda
	- Lmabda funciton name suffix
		- `:£{stageVariables.ENV}`

# Encryption

- KMS can make asymmetric keys
	- but SSE-KMS can only use symmetric keys
	- Asymmetric encryption is done client side with public key

- SSE-C
	- Server side with client key
	- Client provides key for AWS to use then it discards it

- CloudWatch Logs
	- CLI to use customer managed key
	- Symmetric only

- RDS encryption
	- TDE (Transparent Data Encryption)
		- SQL Server
	- 
# CICD

- CodeBuild
	- buildspec.yml
- CodeDeploy
	- appspec.yml

- Large dependencies CodeBuild
	- Implement local caching

# CLI

- Decode Unauthorized operation
```bash
sts decode-authorization-message --encoded-message <pasted message>
```

# SQS

- You cannot change a standard SQS to FIFO after creation
- Must use FIFO for deduplicaiton


# Lambda

## Limits

- Max function size 50MB zipped
- Max unzipped including layers = 250
- Max in console 3MB
- /tmp 512MB

# Xray
- X-ray segment document (T2 Q11)
	- https://docs.aws.amazon.com/apigateway/latest/developerguide/apigateway-xray.html
	- Subsegment for downstream events
	- Tracing header
	- metadata
		- key:value
	- annotations
		- Key:value filterable

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
	- Data Stream
		- Real time data streaming service
		- WHen you eed multiple apps to consume same stream concurrently
		- Ordering and replay ability
	- Data firehouse
		- Streaming data to storage and analytics
		- Near real time
	- Data Analytics
		- Analysze steraming data in real time
		- Used to build SQL queries and Java applicaitons
- CodeDeploy rollback
- EBS encryption
- SWF
	- **SWF ensures the task is assigned only once while SQS may deliver the message multiple times**
	- **SWF has task-oriented APIs and SQS has message-oriented APIs**
- ASG unhealthy instance replace
- codedeploy
	- stages of update
	- Hooks - lifecycle events
- ecr commands
	- `$(aws ecr get-login --no-include-email) docker pull 1234567890.dkr.ecr.eu-west-1.amazonaws.com/demo:latest`
- Lamabda
	- Provisioned vs reserved concurrency
- .ebextensions
- RCU / WCU
- CloudFormation values (!::, Ref, Att)
	- !ImportValue
		- The intrinsic function Fn::ImportValue returns the value of an output exported by another stack. You typically use this function to create cross-stack references.
	- !Ref - Returns the value of the specified **parameter** or **resource**.
	- !GetAtt - Returns the value of an attribute from a resource in the template.
	- !Sub - Substitutes variables in an input string with values that you specify.


- Cross account S3 (Q29)
- Cross zone load balancing
- ECS Bootstrap (Q53)
	- In the ecs.config file you have to configure the parameter ECS_CLUSTER='your_cluster_name' to register the container instance with a cluster named 'your_cluster_name'.

- Bastion host
	- meta data ec2 ip
	- `http://169.254.169.254/latest/meta-data/`.
		- The IP address 169.254.169.254 is a link-local address and is valid only from the instance. All instance metadata is returned as text (HTTP content type text/plain).

- NoSQL (DYnamoDB) commands
	- [[23.1 - DynamoDB - Basic Operations#DynamoDB CLI]]
	- 

- DynamoDB streams

- SQS
	- max size
	- DKQ / poison pill process
	- 

- Beanstalk
	- Environments
		- https://docs.aws.amazon.com/elasticbeanstalk/latest/dg/using-features.managing.html

- S3 programmatic access
	- [https://docs.aws.amazon.com/AmazonS3/latest/dev/example-walkthroughs-managing-access-example3.html](https://docs.aws.amazon.com/AmazonS3/latest/dev/example-walkthroughs-managing-access-example3.html)
	- [https://docs.aws.amazon.com/IAM/latest/UserGuide/tutorial_cross-account-with-roles.html](https://docs.aws.amazon.com/IAM/latest/UserGuide/tutorial_cross-account-with-roles.html
	- [https://docs.aws.amazon.com/IAM/latest/UserGuide/id_roles_compare-resource-policies.html](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_roles_compare-resource-policies.html)
	- [https://aws.amazon.com/premiumsupport/knowledge-center/cross-account-access-s3/](https://aws.amazon.com/premiumsupport/knowledge-center/cross-account-access-s3/)

# AWS Practice Exam

- lambda unqualified
- Session state across devices
	- Amazon Elasticahce for Redis Cluster
		- https://aws.amazon.com/getting-started/hands-on/building-fast-session-caching-with-amazon-elasticache-for-redis/
		- https://docs.aws.amazon.com/wellarchitected/latest/reliability-pillar/design-interactions-in-a-distributed-system-to-mitigate-or-withstand-failures.html

# AWS SKills Builder

- [DVA-c01 compared to C02](https://explore.skillbuilder.aws/learn/course/14724/play/73778/comparison-dva-c01-to-dva-c02)
- [Whitepapares and FAQs](https://explore.skillbuilder.aws/learn/course/14724/play/73031/whitepapers-and-faqs)


## Revisit

- Domain
	- configuration and use of SDK API and keys
	- Micro services
	- Jitter & DLQ
	- Method requests and responses
	- Mapping templates
	- Throttling
- Lambda
	- Layers
	- Extensions
	- env variables
	- config paramters
		- Triggers
- Data Stores
	- Caching services & strategies
	- DB consistency and use cases
	- Migrating DB
	- Encryption on DB


- Stateful vs stateless
	- https://aws.amazon.com/blogs/gametech/stateful-or-stateless/

- API
	- Mapping templates
	- status code handling
	- caches
	- throttling
	- usage plans / keys
	- proxy / none proxy lambda
	- Query string parameters

- Ensure syncing profile data syncing
	- Cognito Sync, cross syncs user data across devices without backend

# PT 1

- Q13

## Videos to watch

- Step functions
- SAM (all)
- CloudFront
	- Viewer Protocol Policy
	- Origin Protocol Policy
- CloudWatch Metrics
- Aurora
- SQS ordering/splitting
	- MessageGroupID
	- Change to FIFO after deployment
	- https://docs.aws.amazon.com/AWSSimpleQueueService/latest/SQSDeveloperGuide/sqs-delay-queues.html

# Topics

- Viewer Protocol Policy
- Systems Manager Parameter Store vs others
- Lambda authorizer (T2 Q42)
- StackSets vs stacks
	- Stack sets
	- Multi region
	- https://www.youtube.com/watch?v=9Xpuprxg7aY
	- https://tutorialsdojo.com/aws-cloudformation/?src=udemy
	- [https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/what-is-cfnstacksets.html](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/what-is-cfnstacksets.html)
	- [https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/stacksets-getting-started.html](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/stacksets-getting-started.html)
- S3 
	- ET Q 38 permissions
		- https://www.examtopics.com/exams/amazon/aws-certified-developer-associate-dva-c02/view/10/
	- Download S3 encrypted
- Authentication
	- SAML
	- IdP auth OpenID
	- authenticated principal role acces / role trust (Q12)
- CodeBuild
	- Caching dependancies (locally)
	- Custom build image (Docker)
- CloudWatch
	- Encrypt old logs (PT Q43)
- Secret store SecureString access in lambda func
- AWS Artifact
	- On demand download of security and compliance docs
- AWS CodeArtifact
	- Artifact repository service
	- Store approved artifacts with AWS account
- AD in cloud options
- Step functions
	- Errors
	- Passage of info

- NAT gateways
	- https://docs.aws.amazon.com/vpc/latest/userguide/vpc-nat-gateway.html
- AWS SDK for JS in browser
- DataSync
	- Transfer data from on prem to AWS storage
- Nitro Enclave
	- Can assign certs to EC2
- SWF (Simple Workflow Service)
	- https://docs.aws.amazon.com/amazonswf/latest/developerguide/swf-welcome.html
	- Markers
		- record events for decider logic (number of loops)
	- Signals
		- Inject information into workflow execution
- https://www.youtube.com/watch?v=q0DmxfyGkeU

API limits and scaling
	- https://docs.aws.amazon.com/apigateway/latest/developerguide/api-gateway-caching.html
- Origin Access Identity
	- https://docs.aws.amazon.com/AmazonCloudFront/latest/DeveloperGuide/private-content-restricting-access-to-s3.html#private-content-restricting-access-to-s3-oai
## Cheat Sheets to review

- Lambda
- SAM
- CloudWatch
- [[20.3 - X-Ray#X-Ray API Actions]]
- EB CLI commands
	- [https://docs.aws.amazon.com/elasticbeanstalk/latest/dg/eb-cli3.html](https://docs.aws.amazon.com/elasticbeanstalk/latest/dg/eb-cli3.html)
	- [https://docs.aws.amazon.com/elasticbeanstalk/latest/dg/eb-cli3-configuration.html#eb-cli3-artifact](https://docs.aws.amazon.com/elasticbeanstalk/latest/dg/eb-cli3-configuration.html#eb-cli3-artifact)
	- **Check out this AWS Elastic Beanstalk Cheat Sheet:**
		- [https://tutorialsdojo.com/aws-elastic-beanstalk/](https://tutorialsdojo.com/aws-elastic-beanstalk/?src=udemy)


# RDS

- RDS port 3306
- RDS proxy 
	- to reduce connection timeouts and CPU/RAM
	- Failover time reduced
- Elasticache
	- Code changes required
	- Redis
		- Sets / sorted sets
		- Durability
	- Memcached
		- Multi threaded & sharding

# CodeDeploy

- Stages have action groups
	- Parallel or sequential

- Manual approval
	- Owner: aws
	- Action: manual

# Auth 

![[AWS_Auth_IAM_User_Policy_Variable_Example.png]]

`${aws:username}`

4) you need to log in to see a private repository. The format for pulling an image from a repository is:

```
1.  aws ecr get-login-password | docker login 
2.  docker pull <registry>/<repository>:<tag>  
```

# Step Functions

- express
	- async
		- at least once
	- sync
		- at most once