# Docs

- AWS constructs
	- https://docs.aws.amazon.com/cdk/api/v2/docs/aws-construct-library.html

# Solutions

- AWS Solutions Constructs
	- an open-source extension of the [AWS Cloud Development Kit (AWS CDK)](http://aws.amazon.com/cdk/) that provides multi-service, well-architected patterns for quickly defining solutions in code to create predictable and repeatable infrastructure
	- https://docs.aws.amazon.com/solutions/latest/constructs/welcome.html
	- An npm library
- CDKpatterns.com
	- Community provided examples
- Construct Hub
	- Find libraries for CDK
- Restaurant Solution AWS
	- https://github.com/awslabs/aws-solutions-constructs/tree/main/source/use_cases/aws-restaurant-management-demo
	- https://youtu.be/9YW1sL0dFV8

- AWS Solutions CDK API
	- https://docs.aws.amazon.com/solutions/latest/constructs/welcome.html
# Tutorials

- cdkworkshop
- FreeCodeCamp three tier CDK application
	- https://www.freecodecamp.org/news/aws-cdk-v2-three-tier-serverless-application/
		- Data Tier
			- DynamoDB
		- Application Tier
			- HTTP API GW
			- Lambda functions
		- Presentation Tier
			- React
				- React application built as part of synth with vitejs & esbuild
					- By default it will be built with docker
				- S3 storage
				- CloudFront distribution and build step
				- Custom resource to provide API URL to web application
- Host React app on Amplify using CDK