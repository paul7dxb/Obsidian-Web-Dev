# S3 Encryption

- You can set a bucket policy to force encryption by refusing API calls that PUT an object in S3 that do not have the encryption headers
- The policy is enforced before "default encryption" setting

![[AWS_S3_Bucket_Policy_Encryption.png]]


## SSE-KMS

- [[14 - S3 Security#SSE-KMS|SSE-KMS Notes]]
- Selected either at bucket creation or changing encryption settings (e.g on a file already uploaded)
	- Changing object encryption creates a new version of the file
- KMS key
	- Choose from AWS KMS keys
		- S3 is the default key
		- Creating others is a paid feature

## Change Bucket Encrpytion

- Bucket
- Properties
- Default Encryption

## SSE-C

- Must use CLI

# Bucket MFA

## MFA Delete

- Create bucket that has versioning enabled
- Must be logged in as root
- Properties
	- Versioning
	- Enabled
- IAM
- Create new access key for root in IAM
	- aws configure --profile root-mfa-delete-demo
	- access key
	- secret key
- aws s3 ls --profileroot-mfa-delete-demo
	- This will show buckets

### enable mfa delete
```cmd
aws s3api put-bucket-versioning --name-of-your-bucket --versioning-configuration Status=Enabled,MFADelete=Enabled --mfa "arn-of-mfa-device mfa-code" --profile root-mfa-delete-demo
```

### disable mfa delete
```cmd
aws s3api put-bucket-versioning --name-of-your-bucket --versioning-configuration Status=Enabled,MFADelete=Disabled --mfa "arn-of-mfa-device mfa-code" --profile root-mfa-delete-demo
```

### delete the root credentials in the IAM console!!!

- IAM
- Access keys
- Deactivate access key

# S3 Bucket Logging

- Bucket
- Properties
- Server Access Logging
	- Choose target bucket
- Access, uploads, changes to buckets will create activity for the log

- Permissions
	- Automatically updated when selecting to log
	- Bucket Policy on logged bucket
	- Allows logging service
	- Allows logging using PutObject into target bucket

# S3 Pre Signed URL

- Navigate to object
- Object actions
	- Share pre signed url
	- Specify time