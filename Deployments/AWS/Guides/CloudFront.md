# Create Distribution

- CloudFront
- Create distribution
- Choose S3 bucket for origin
	- (or HTTP origin)
- Origin Access Control (OAC)
	- Create OAC
	- Create
- Set default root object (optional)
- Create
- Copy Policy (Update S3 bucket to allow CloudFront to access bucket)
	- Allows cloudfront distribution to perform getObject on any file in bucket
	- Click S3 shortcut in header
	- If you lose policy
	- Click on distribution
		- Origins
		- Edit
		- Copy Policy is on page
- Wait for distribution to become deployed

# View Origin Access

- CloudFront
- Origin Access (Left bar)
	- Origin Access Controls
	- Assigned to distribution

# CloudFront Caching Behaviours

- CloudFront
- Choose Distribution
- Behaviours
- Create Behaviour
	- Cache Key and Origin Requests
		- [[#Create Cache Policy]]
	- 

# Create Cache Policy

- CloudFront
- Policies
- Cache
- Create Cache Policy
	- Name
	- Set TTL
	- Choose or set custom headers / query strings / cookies

# Create Invalidation to CloudFront

- Force cached data to be refetched when requested again
	- Useful when origin data is changed

- CloudFront
- Distributions
- Invalidations
	- Create Invalidation
	- Choose path (invalidate all with /*)

# Create geographic restriction

- CloudFront
- Distributions
- Select distribution
- Edit geographic restrictions
	- Allow / Block

# Key Management

- CloudFront
- Public Keys
- Create Public Key
	- Use tool to create key pair and paste public key to CloudFront
- Create Key Group
	- Create
	- 