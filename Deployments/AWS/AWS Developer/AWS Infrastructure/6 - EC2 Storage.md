- Network USB stick
- Network drive that is attached to an instance while it runs
- Allows data to persist after termination
- Only mounted to one instance at a time
- Bound to one AZ

- Introduces latency (e.g us-east-1a)
- Has provisioned capacticy (size and IOPS)
- Can set delete on termination
	- When EC2 instance in terminated
	- Set to preserve root data

# EBS Snapshot

- Elastic Block Storage
- Used to transfer data from one AZ to another
- EBS snapshot archive
	- Move snapshot to archive tier
	- 24 - 72 hours to restore archive
- Recycle bin from 1 day to 1 year
- Fast Snapshot Restore
	- Full initialization of snapshot to have no latency on first use \$\$\$

# AMI

- Amazon Machine Image
	- Custom EC2 instance
		- Add your own software, configuration, OS, monitoring...
		- Fast boot time as software is pre packaged
	- Built in a specific region (can be copied to others)
	- AWS marketplace sells AMI

# EC2 Instance Store

- Storage physically attached to where the instance is running
- Better IO
- Storage lost is EC2 terminated (ephemeral)
- Loss of data if hardware fails and backups are your responsibility

# EBS Volume Types

- 6 types
	- Size | Throughput | IOPS
	- ![[AWS_ECB_Storage_Types.png]]
	- Only gp2/3 or io1/2 cna be used as boot volumes



- General Purpose SSD
	- - 1 GiB - 16 TiB
	- gp3
		- Baseline 3 000 IOPS throughput 125MiB/s
		- can increase to 16 000 and 1 000MiB/a
	- gp2
		- Burst 3 000 IOPS
		- IOPS and volume are **linked**
		- 5 334 GB gets max IOPS = 16 000

- Provisioned IOPS (PIOPS)
	- For sustained IOPS
	- Application > 16000 IOPS
	- Databse workloads
	- io1 io2 (new generation) - (4 GiB - 16 TiB)
		- Nitro EC2 instance > 32 000 IOPS
		- Can increase PIOPS independently from storage size
	- io2 Block Exporess (4 GiB - 64 TiB)

- HDD
	- Not Boot volume
	- 125 GiB to 16 TiB
	- Throughput Optimized
		- Big data
	- Cold HDD
		- Infrequently accessed
		- Lowest cost

# Multi Attach Feature

- Attach the same EBS volume to multiple EC2 instances in the same AZ
- Only io1 / io2
	- Up to 16 EC2 instances
- Read and write from all
- Used to achieve higher availability in clusterd applications
- Require concurrent writes
- Cluster aware file system

![[AWS_io2_MultiAttach.png]]

# EFS

- Elastice File System
- Network File System
	- Can be in different AZ
- Expensive
- Only compatible with Linux AMI
- KMS to encrypt at rest

![[AWS_EFS.png]]

- Types
	- EFS Scale
	- Grows automatically up to PetaByte
- Performance mode
	- General
	- Max IO
- Throughput Mode
	- Bursting
	- Provisioned - throughput regardless of storage size
	- Elastic - automatically scales

- Storage Classes
	- Standard - frequently accessed
	- Infrequent Access (EFS-IA)
		- lifecycle policy move from standard to lower tier
		- Standard is multi AZ (one zone usually for dev)
