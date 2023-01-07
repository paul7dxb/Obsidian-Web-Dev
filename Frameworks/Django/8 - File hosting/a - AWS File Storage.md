# Set Up AWS S3 Bucket

[[S3 Buckets]]

# Install Packages

```bash
pip install boto3
pip install django-storages
```

# Settings.py

```python
INSTALLED_APPS = [
    'storages'

AWS_ACCESS_KEY_ID = os.environ.get('AWS_ACCESS_KEY_ID')
AWS_SECRET_ACCESS_KEY = os.environ.get('AWS_SECRET_ACCESS_KEY')
AWS_STORAGE_BUCKET_NAME = os.environ.get('AWS_STORAGE_BUCKET_NAME')

AWS_S3_FILE_OVERWRITE = False
AWS_DEFAULT_ACL = None

DEFAULT_FILE_STORAGE = 'storages.backends.s3boto3.S3Boto3Storage'

```

# Change save method

Resizing no longer done on server. If you want AWS to do resizing will have to use an AWS lambda function

Django docs for storage:

https://django-storages.readthedocs.io/en/latest/

# For those whose images (profile picture) are not loading.
If you are getting similar error:
<Error>

    <Code>InvalidRequest</Code>

    <Message>The authorization mechanism you have provided is not supported. Please use AWS4-HMAC-SHA256.</Message>

    <RequestId>BA4D72AC9CD1F73B</RequestId>

    <HostId>RixYpYIGhs1V1L/JqjHHBUejHoX8UGfChX+vVfB+A9F+Of+/u/UZ64ub8zrN5uJ+cmEDHI75JLA=</HostId>

</Error>

Add these lines in your settings.py:
AWS_S3_REGION_NAME = 'us-east-2'
AWS_S3_ADDRESSING_STYLE = 'virtual'
AWS_S3_SIGNATURE_VERSION = 's3v4'