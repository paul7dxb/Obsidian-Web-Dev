- EC2
- Auto Scaling
	- Auto Scaling Groups
- Create
- Choose or [[#Create Launch Template]]
- Next
- Instance launch options
	- Zones
	- Can override launch templates for variable instance types
- Configure Load Balancer
	- Attach to esisting load balancer [[Load Balancer - ALB]]
	- This connects ASG instances to load balancer automatically
- Configure size and scaling

# Automatic Scaling

- EC2
- Auto Scalin Groups
- Automatic Scaling
- Create dynamic scaling policy
	- [[7.1 - ELB#ASG Scaling Policies|Scaling Policies]]


# Create Launch Template

- EC2
- Launch templates
- Create
- Choose image
- EC2 setup as usual

# View Activity

- EC2
- Auto Scaling Group
- Choose ASG
- Activity

# Target Tracking Policy

- Example setting average CPU to scale out
- Automatically creates CloudWatch alarms for scale in / out