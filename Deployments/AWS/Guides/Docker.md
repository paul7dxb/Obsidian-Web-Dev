# Create ECS Cluster

- ECS
- All Clusters
- Create CLuster
- Choose subnets
- Choose Infrastructure
	- Fargate / EC2 Instances

# Using EC2 Instances in Cluster

- EC2
- Auto Scaling Groups
	- Will show Cluster ASG
	- Can launch tasks on these instances
	- Can change ASG values here
- Show in cluster as container instance
	- Used to launch tasks

# Using Cluster

- Infrastructure
	- Capacity providers are what will launch tasks

# Create ECS Task

- ECS
- Task Definitions
- Create
- Use docker repo name in image URI
- Set Port mappings
- Add environment variables

- Choose app environment (fargate / EC2 instance)
- Set OS
- Set Task size

- Add IAM Task Role
	- Used for API calls to AWS

# Create ECS Service

- ECS
- Clusters
- Choose cluster
- Services
	- Create Service
- Service
	- Long running
- Task
	- Runs and terminates
- 