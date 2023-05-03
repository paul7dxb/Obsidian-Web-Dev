- Kinesis
- Create data stream
- Name
- Provisioned / on Demand

```bash
# get the AWS CLI version
aws --version

# PRODUCER

# CLI v2
aws kinesis put-record --stream-name test --partition-key user1 --data "user signup" --cli-binary-format raw-in-base64-out

# CLI v1
aws kinesis put-record --stream-name test --partition-key user1 --data "user signup"


# CONSUMER 

# describe the stream
aws kinesis describe-stream --stream-name test

# Consume some data
aws kinesis get-shard-iterator --stream-name test --shard-id shardId-000000000000 --shard-iterator-type TRIM_HORIZON
# Returns a shard interator. Use in the get-records call

aws kinesis get-records --shard-iterator <>

# next shard iterator will tell you where to start form on next call
```

# Firehose

- Kinesis
- Delivery Stream
- Source
- Destination
	- S3

- Advanced
	- service access
	- Can create IAM role to use with required permissions

