# Create Queue

- SQS
- Create
- Access Policy
- Change policy to allow SQS to write to SQS
	- Policy generator
	- SQS Queue Policy
	- Allow *
	- SendMessage
	- Copy Amazon Resource (Notification)

# Send & Receive to Queue

- SQS
- Top right (send and receive)
- Type message and send
- Send
- Poll for Message
- View message
	- Details
	- Body
	- Attributes
- Select
- Delete (signal it has been processed)

# Delete All Messages (Purge)

- SQS
- Choose queue
- Purge

# Get Message From S3 Event

- Create Queue
	- Create an S3 bucket to get the name for access policy
- Disable encryption
- Access Policy
	- [Link to access policy](https://docs.aws.amazon.com/AmazonS3/latest/userguide/grant-destinations-permissions-to-s3.html)
```JSON
{
    "Version": "2012-10-17",
    "Id": "example-ID",
    "Statement": [
        {
            "Sid": "example-statement-ID",
            "Effect": "Allow",
            "Principal": {
                "Service": "s3.amazonaws.com"
            },
            "Action": [
                "SQS:SendMessage"
            ],
            "Resource": "arn:aws:sqs:Region:account-id:queue-name",
            "Condition": {
                "ArnLike": {
                    "aws:SourceArn": "arn:aws:s3:*:*:awsexamplebucket1"
                },
                "StringEquals": {
                    "aws:SourceAccount": "bucket-owner-account-id"
                }
            }
        }
    ]
}
```

- Go to S3 bucket
	- Properties
	- Event Notification
	- Create
		- Choose event type (e.g all uploads)
		- Destination
			- SQS queue
			- Choose queue created
		- Save

- This will create a test message to the queue