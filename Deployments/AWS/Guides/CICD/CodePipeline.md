- CodePipeline
- Create Pipeline
- Service Role
	- Required
- Define source from code repo
- Build Provider
	- Can skip
- Deploy Provider
	- Elastic Beanstalk
		- Requires already existing

# Approve Before Deploy

- Pipeline
- Choose Pipeline
- Edit 
- Add stage
	- Add action group
		- Action Provider
		- Manual Approval
	- Add action Group
		- AWS Beanstalk
		- Application name
		- Application environment