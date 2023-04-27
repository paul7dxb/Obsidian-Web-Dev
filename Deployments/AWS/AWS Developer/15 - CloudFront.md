
- CloudFront is a CDN (Content Delivery Network)
	- Global service (not regioned)
- Cache content at edge location
- Imporives latency
- 216 points
	- Edge locations
- DDoS protection
- Integration with Shield and WAF

# CloudFront Origins

- S3 Bucket
	- Caching files at edge locations
	- Enhanced security with CloudFront Origin Access Control (OAC)
	- Can be used to ingress to S3
- Custom Origin (HTTP)

# CloudFront Process

- Request made from user to CloudFront Edge Location
- CloudFront checks its cache
	- If it doesn't have it, fetches from origin and caches it
	- Files are cached with a TTL

![[AWS_CloudFront_S3_Access.png]]

# CloudFront Cache

- Object in CloudFront cache is identified using a Cache Key
	- By default hostname + resource portion of URL
- Can invalidate part of the cahce using CreateInvalidation API

![[AWS_CloudFront_Cache_Key.png]]

- If content varies on more complex data (user specfic)
	- Define CloudFront Cache Policies
		- HTTP headers
		- Cookies
		- Query Strings
	- Options
		- None
		- Whitelist headers to only use specified headers
			- Forwarded to origin
		- Include all except
		- All
		- Origin Request Policy
			- Include in the origin request but not in the cache key
				- Passing API or secret header

- All HTTP headers including in cahce key are forwarded to origin request

![[AWS_CloudFront_Cache_Vs_Origin.png]]

# CloudFront Invalidations

- Force Cache refresh when origin is updated
	- TTL will not look to origin for cached data while it is valid
- Done using CacheInvalidation
	- Can do path or everything

![[AWS_CloudFront_Cahce_Invalidation.png]]

- Now when next request is made the new origin will be stored in cache at edge

# Cache Behaviour

- Can have different cache behaviours for different file types
- Can route different orgins based on content type or path
- Default is last to be processed

![[AWS_CloudFront_Cache_Behaviour.png]]

- Use case:
	- Sign In to access bucket
	- Use signed cookies to access any other URL than the login page
		- Only accept cache behaviour to other if there is a signed cookie

![[AWS_CloudFront_Login_Example.png]]

# CloudFront ALB

- If cloudfront is accessing EC2 instances cloudfront IPs must be allowed to access EC2
	- Create Security Group to allow 
		- https://d7uri8nf7uskq.cloudfront.net/tools/list-cloudfront-ips
- Or
- Use ALB that is public
	- Allow EC2 access from ALB

![[AWS_CloudFront_Allow_IPs.png]]

# CloudFront GeoLocation

- Define allowlist or blocklist
- Determined using 3rd party geo ip database
	- Copyright laws

# CloudFront Sign URL / Cookies

- Use case:
	- Distribute premium content to premium users worldwide
- Attach policy
	- URL expiration
	- IP ranges
	- Trusted signers

- Cookie or URL
	- URL for individual files (one URL per file)
	- Sign cookies allow access to multiple files (one cookie many files)

![[AWS_CloudFront_Signed_URL.png]]

- CloudFront Signed URL vs S3 pre-signed URL
	- CloudFront
		- Allow access no matter the origin
		- Account wide managed by root
		- Can use caching features
	- S3 Pre Signed
		- Request is made with rights of the person who made the URL
		- Uses IAM key
		- Limited lifetime

# CloudFront Signing

- Signers
	- Trusted Key Group
		- APIs create and rotate keys
	- AWS account that contains CloudFront Key Pair
		- Not recommended
		- Uses root account

- Private key used by applications to sign URLs
- Public key used by CloudFront to verify URLs

# CloudFront Advanced Concepts

## Pricing

- Edge location prices vary
- More data => lower cost per GB
- Price classes
	- Can reduce number of edge locations to get lower price
		- All - best performance
		- Class 200 - most regions but excludes most expensive
		- Class 100 - Least expensive regions

![[AWS_CloudFront_Classes.png]]

## Multiple Origin

- Different origin based on content type
	- Cache behaviour dependent on path

![[AWS_CloudFront_Origins.png|400]]

- Origin Groups
	- Primary and secondary origin
		- Failover to second origin

![[AWS_CloudFront_Origin_Failover.png]]

## Field Level Encryption

- Protect sensitive information through application stack
- Additional to encryption in flight
- Information encrypted at edge location close to user
- Asymmetric encryption
	- Encrypt fields using public key which is then decrypted to web servers

![[AWS_CloudFront_Field_Level_Encryption.png]]

# CloudFront Real Time Logs

- Sent to Kinesis Data Streams
- Monitor, analyze and take actions
	- Real time: Lambda funciton
	- Near real time: Kinesiss Data Firehouse
- Can choose sampling rate
- Can specify fields and cache behaviours