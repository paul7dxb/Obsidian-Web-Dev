# S3 CORS guide

- [[14 - S3 Security#CORS|CORS S3 Notes]]
- Required to access buckets from another origin


# Setup bucket to allow CORS

- Bucket
- Permissions
- CORS
	- Edit

```JSON
[
    {
        "AllowedHeaders": [
            "Authorization"
        ],
        "AllowedMethods": [
            "GET"
        ],
        "AllowedOrigins": [
            "<url of first bucket with http://...without slash at the end>"
        ],
        "ExposeHeaders": [],
        "MaxAgeSeconds": 3000
    }
]
```