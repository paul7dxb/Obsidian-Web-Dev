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

- Used to transfer data from one AZ to anaother
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

- Storage pphysically attached to where the instance is running
- Better IO
- Storage lost is EC2 terminated (ephemeral)
- Loss of data if hardware fails and backups are your responsibility