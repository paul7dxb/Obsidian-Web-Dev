https://s3.console.aws.amazon.com/s3/buckets?region=us-east-1#

- Create bucket
- Universally unique name

- click bucket
- permissions
- CORS configurations
	- Cross origin resource configuration

# CORS Config

CORS JSON config

```JSON
[
    {
        "AllowedHeaders": [
            "*"
        ],
        "AllowedMethods": [
            "PUT",
            "POST",
            "DELETE"
        ],
        "AllowedOrigins": [
            "*"
        ],
        "ExposeHeaders": []
    }
]
```


# Identitiy Access Management

https://us-east-1.console.aws.amazon.com/iamv2/home?region=us-east-1#/users

- IAM management console
- Create user
	- Username
	- Access key - programmatic access
		- secret access key
	- Permissions
		- Attach exisiting policies directly
		- Filter: S3
		- AmazonS3FullAccess (more access than needed)

## Add to Environment Variable

[[Environment Variables]]

```
expot AWS_ACCESS_KEY_ID="AKIA6NCS8JHDES4OMPX7"
export AWS_SECRET_ACCESS_KEY="+qMf7KK13JQJ7dBf8eSdeFV030joNAcop/lep5"
export AWS_STORAGE_BUCKET_NAME="django-blog-files-mcpapapps"
```




