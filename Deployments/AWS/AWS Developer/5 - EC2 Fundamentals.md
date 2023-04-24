# Types

- Naming convention e.g m5.2xlarge
	- m: instance class
	- 5: generation
	- 2xlarge: size within the instance class
- General Purpose
	- Web server / code repo
	- Well balanced compute, memory and networking
- Compute Optimized
	- Naming c
	- Batch processing
	- Media transcoding
	- Machine Learning
	- Game Server
	- High performance web server
- Memory Optimized
	- R series, X series
	- Processing large data sets in RAM
	- Elastic Cache
	- High performance database
	- Real Time data processing
- Storage Optimized
	- Large data sets on local storage
	- Relational & NoSQL database
	- Data Warehousing

# Security Groups

- Act as a firewall
- Runs outside of EC2

- Only contain allow rules
- Refer to IP or by security group

# SSH to EC2 Instance

- Use powershell to use ssh
- Go to location of RSA key

```powershell
ssh -i '.\EC2 Tutorial.pem' ec2-user@13.40.109.26
```

- Requires .pem file to have you as owner and the ONLY principal with any permissions on it. Give full control

# EC2 Instance Connect

- Connect to terminal from AWS console
- Uploads temporary SSH key for us

# EC2 Instance Roles

- [[2 - CLI#EC2 Roles to use CLI|EC2 Roles to use CLI]]
