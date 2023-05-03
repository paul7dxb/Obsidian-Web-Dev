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