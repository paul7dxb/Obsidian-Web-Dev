
# AWS CAF (Cloud Adoption Framework)
- Used to make guidance to transition into a cloud environment

## Perspectives

- Business Capabilities
	- Business
		- Business case
		- Finance managers
	- People
		- OU structures -> training and staffing
		- HR
	- Governance
		- CIO
		- Business analysts
- Technical capabilities
	- Platform
		- Architectural models for structure of IT systems and relationships
		- CTO (Chief Technology Officer)
		- Cloud architect
	- Security
		- Security controls
		- CISO (Chief Information Security Officer)
	- Operation
		- Current operating procedures and identify the process changes and training needed
		- IT support/operations managers

# Migration Strategies

- Rehosting
	- Lift and shift
	- Move as is
- Replatforming
	- Lift, tinker & shift
	- Few small optimisations
		- MySQL replatformed to RDS MySQL or Amazon aurora
		- No code changes
- Refactoring
	- Write new code
	- Dramatic changes to architecture
	- Highest initial cost
- Repurchasing
	- Abandon legacy and get a fresh start
	- Have to deal with new software package
	- Larger initial investment
- Retaining
	- Applications not quite ready to retire
	- Don't migrate to cloud and then deprecate where they live
- Retiring
	- Applications no longer being used or live replacements. EOL applications.

# Moving Data

## AWS Snow Family

- Physical devices to transport data in and out of AWS
	- Up to exabytes transfer
	- Secure and tamper resistent
	- 256 bit encryption key you manage (AWS KMS)

![[AWS_Snow_Family.png]]

- Snowcone
	- 8 Terabytes
- Snowball Edge 
	- Storage Optimised
		- 80TB
	- Compute Optimised
		- 42TB
- Snowmobile
	- Shipping container
	- 100 petaBytes

# Other Innovation

- VMware to cloud
- Amazon Sagemaker
	- ML models at scale
- Amazon A2I (Augmented AI)
- Amazon Lex
	- Interactive chat bots
- Amazon Textract
	- Usable text
- Amazon DeepRacer
	- Reenforcement learning
- AWS Ground Station
	- Satalite time PAYG