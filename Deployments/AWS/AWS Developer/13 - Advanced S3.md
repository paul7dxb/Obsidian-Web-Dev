# Lifecycle Rules

- Transition Actions
	- Configure objects to transition to another storage class

- Expiration Actions
	- Delete files after some time

- Can apply rules to file types

- Amazon S3 Analytics
	- Helps decide when to transition objects to right class
	- Standard and Standard IA
		- Not glacier on One Zone IA
	- Produces .csv report
		- 24 to 48 hours before seeing data analysis


# S3 Event Notifications

- Triggered from:
	- S3:ObjectCreated
	- S3:ObjectRemoved
	- S3:ObjectRestore
	- S3:ObjectReplicaiton ...
- Possible to filter (e.g file type)
- Example cases:
	- Generate thumbnail when image uploaded to S3
	- Trigger SNS, SQS, Lambda function
	- EventBridge
		- All events end up in EventBridge
			- Set up rules to go to over 18 AWS services
			- Enhancing capabilities
				- Advanced filtering options
				- Multiple destinations
				- Archive, replay


# Performance

- Scales to request rates
- Request rates are per prefix (bucket or folder in bucket)
	- 3500 PUT/COPY/POST/DELETE
	- 5500 GET/HEAD

## Optimising S3

- Uploading
	- Multi part upload
		- Recommended for files >100MB
		- Must for >5GB
		- Parallelize upload that is then recombined into file in S3
	- S3 Transfer Acceleration
		- Increase transfer speed by transferring to AWS edge location, then forwarded to S3 bucket in target region
		- Minimise public internet used
	- Can be used together

![[AWS_S3_Transfer_Acceleration.png]]

- Downloading
	- Requests in parrallel
		- Parallelize GET by requesting specific byte ranges
		- Better resiliance to failures only re requesting smaller parts
	- Head request if that is all that is required (first part of file)

# S3 Select

- Use SQL to perform server-side filtering and retrieve less data
- Returns filtered dataset

![[AWS_S3_Select.png]]

# S3 User-defined Metadata

- User Defined Metadata
	- Key value pairs
	- Must begins with:
		- "x-amz-meta-"
- S3 Object Tags
	- Key Value Pairs
	- Useful for fine grained permissions (access to objects with tag)
	- Analytics can be grouped by tag

- These are not searchable / filterable
	- Search using external index e.g DynamoDB

