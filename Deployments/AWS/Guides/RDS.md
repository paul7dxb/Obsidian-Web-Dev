- Relational Database Service

- RDS
- Databases
- Create database
- Choose engine
- Choose template
- Availability and Durability
- Set DB access username and password
- Configuration
	- Free tier:
		- Instance
			- Burstable class
			- Include previous gen classes
			- db.t2.micro
		- Storage
			- gp2
			- 10GB
- Connectivity
	- Choose an EC2 instance to connect to database
	- or
	- Don't choose EC2
		- Choose VPC
		- Subnet
		- Public access
		- VPC security group
- Additional Configuration (last dropdown)
	- DB name
	- Backup retention period
	- Backup time window
	- Export logs to CloudWatch
	- Update window
# Ports

- MySQL - 3306

# Access MySQL from Computer

- Use [[SQL Electron]]

# Create Read Replica

- RDS
- Select DB radio button
- Actions
	- Create read replica


# Create RDS Snapshot

- RDS
- Select DB radio button
- Actions
	- Take snapshot
	- (Can now migrate snapshot if necessary)

# Delete RDS

- Remove Database protection
	- Select DB
	- Modify
	- Remove database protection (bottom of page)
	- Apply immediately
	- Actions
	- Delete

