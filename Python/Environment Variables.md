Used to store variables locally so they do not get shared in repositories

# Generate secret key

```python
import secrets
secrets.token_hex(24)
```

# Setting on Windows

- Veiw advanced system settings
- Environment Variables
- 

# Setting on Linux

- Navigate to home directory
	- `cd`

`nano .bash_profile`

```
export DB_USER="my_db_user"
export DB_PASS="my_db_pass_123!"
```

Save file

Restart services using

# Accessing Environment Variable

```python
import os

db_user = os.environ.get('DB_USER')
db_password = os.environ.get('DB_PASS')

print(db_user)
print(db_password)
```

## Changing environment variable to Boolean

```python
DEBUG = (os.environ.get('DEBUG_VALUE') == 'True')
```