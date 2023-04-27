# Encryption Methods

- Server Side Encryption (SSE)
	- SSE-S3
		- Amazon managed keys 
	- SSE-KMS 
		- Key Management Service
	- SSE-C
		- Customer Provided Keys
- Client SIde Encryption

# SSE-S3

- Key managed by AWS
	- You never have access
- AES-256
- Default for new buckets / objects
- Set header: "x-amz-server-side-encryption":"AES256"

![[AWS_S3_SSE-S3.png]]

# SSE-KMS

- AWS KMS (Key Management Service)
	- You manage the keys
	- Can create and audit key usage using CloudTrail
	- Set header: "x-amz-server-side-encryption":"aws:kms"

- Requires API calls into the KMS API
	- Counts towards quota calls of KMS
	- High throughput may hit throttling (5500, 10000, 30000 req/s region dependent)

![[AWS_S3_SSE-KMS.png]]

# SSE-C

- Keys managed by customer oustide of AWS
- S3 does not store the encryption key
- HTTPS ***must*** be used
- Encryption key must be in HTTP headers for ever HTTP request made

![[AWS_S3_SSE-C.png]]

# Client Side Encryption

- CLient encrypts before sending the data
- Decryption happens by client outside of AWS
- Client manages all encryption and keys


# Encyption in Transit

- SSL / TLS
- AKA encrytion in flight
- You can force encryption in transit using bucket policy

![[AWS_S3_Force_SSL.png| 350]]

# CORS

- Cross-Origin Resource Sharing
- Origin = scheme (protocol) + host (domain) + port
- Web browser security mechanism
	- Allow requests to other origins while visiting main origin

- E.g different origins - http://www.example.com & http://other.example.com
- Requests are not fulfilled unless the ***other origin*** allows for requests using CORS header

![[AWS_CORS_Request.png]]

- Use example:
	- Going to one origins index.html page which tells the client to get images from another origin 

- With S3:
	- Client makes cross-origin request to S3 bucket
		- Need to enable correct CORS headers
		- Can allow specific origin or * (all origins)
	- If headers are set requests are allowed

![[AWS_S3_CORS_Bucket.png]]

# MFA Delete

- Generate MFA code before doing important S3 operations
- Versioning must be enabled
- Only bucket owner (root) can enable/disable
	- Permanently delete object version
	- Suspend Versioning

# S3 Access Logs

- Access granted or denied is logged
- Can be analyzed by tool such as Athena
- Target logging must be in the same AWS region
- *** DO NOT*** create a logging bucket in your monitored bucket!!! Creates a loop

![[AWS_S3_Logging_Bucket.png|150]]


# S3 Pre Signed URL

- S3 Console 1 min to 12 hours
- CLI up to ~ 168 hours
- Users with pre signed URL inherit permission of the user that generated the URL
- Temporary access to someone

![[AWS_S3_Pre_Signed_URL.png]]

# S3 Access Points

- Different groups that want to access data
- Manage S3 security at scale
- Create access points
	- This has an access point policy
	- Grants read/write access as required
- Access point has
	- Its own DNS name (internet or VPC)
	- Access Point Policy (similar to bucket policy)

![[AWS_S3_Access_Point.png]]

- VPC origin access point
	- Only available within VPC
	- Create VPC Endpoint (Gateway or Interface Endpoint)
![[AWS_S3_VPC_Acess_Point.png|400]]

- VPC Endpoint Policy allows access to target bucket and Access Point
![[AWS_S3_VPC_Acess_Point_Policy.png]]

# S3 Object Lambda

- Modify object before it is retrieved by caller application

- Example redaction:
	- Application wants to access data without PII (personally identifiable info)
	- Create Access point connected to lambda function
		- Redacts object
	- Lambda access point
		- Used to access object

![[AWS_S3_Lambda_Example.png]]

- Other examples:
	- Add user specific watermark