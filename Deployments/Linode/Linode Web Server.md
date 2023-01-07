# Ubuntu Server Set Up

- Create
- New linode
- Ubuntu
- Create
	- Boot commences
- Get IP
	- `ssh root@<IP>`

# Add limited User

```bash
adduser mcpapapps
```

## Add sudo to user

```bash
adduser mcpapapps sudo
```

## Update Server

```bash
apt-get update && apt-get upgrade
```

# Set Host Name

```bash
hostnamectl set-hostname django-server
hostname
django-server
```

Host name in host file


```bash
nano /etc/hosts
```

Add in IP

```
139.162.193.12 django-server
```



## log back in as limited user

```bash
ssh mcpapapps@139.162.193.12
```

# SSH key Setup

- Set Up using:
	- [[SSH#Set up SSH key based Auth]]
- Can now login without password by using ssh key
- Prevent Root login and password auth over SSH
	- [[SSH#Prevent root login or password login]]

# Install UFW

```bash
sudo apt-get install ufw
```

Configure UFW for Django dev server
```bash
sudo ufw default allow outgoing && sudo ufw default deny incoming && sudo ufw allow ssh && sudo ufw allow 8000
sudo ufw enable
sudo ufw status
```

# Copy Files to Web Server

## Create Requirements.txt


On Host Machine virtual python environment in project folder
```bash
pip freeze > requirements.txt
asgiref==3.6.0
Django==4.1.5
django-crispy-forms==1.14.0
Pillow==9.4.0
sqlparse==0.4.3
tzdata==2022.7
```

## SCP to server

```bash
cd /mnt/d

# Move venv out of project fodler if neccessary

scp -r django_example/ mcpapapps@139.162.193.12:~/
```

# Run Server

## Create virtual environment in Project folder

```bash
sudo apt-get install python3-pip
sudo apt-get install python3-venv
python3 -m venv django_example/venv
```

## Activate venv
```bash
cd django_example/ && source venv/bin/activate
```

###  Get Python venv path
```bash
python -c 'import sys; print(sys.prefix)'
```

## Install dependancies
```bash
pip install -r requirements.txt
```

## Change settings file for static files
```bash
sudo nano django_example/settings.py
```

```python
ALLOWED_HOSTS = ['139.162.193.12']    

STATIC_ROOT = os.path.join(BASE_DIR, 'static')      
STATIC_URL = 'static/'   
```

Get static files working on server. Copies to static folder in project
```bash
python manage.py collectstatic
```

# Run server

```bash
python manage.py runserver 0.0.0.0:8000
```

View site at http://139.162.193.12:8000/ to test functionality then stop server

# Install Web Proxy

Install a web proxy such as [[Apache]] with mod [[WSGI]] or [[Nginx]] with [[Gunicorn]]

# Move Files to www

Move to /var/
```bash
 sudo mv django_example/ /var/www/django_example
```



# Storing sensitive info

## In a config.py file

Better to use [[Environment Variables]]

Create a secret key for production
[Generate Secret Key For Django](https://www.educative.io/answers/how-to-generate-a-django-secretkey)

```bash
sudo touch /etc/config.json
```

Get SECURE_KEY value from settings.py

```
sudo nano /etc/config.json
```

```json
{
	"SECRET_KEY" : "django-insecure-mfunn^)u=vzn#!lps^#ce!@w&=((+05@nghh$i-c!2hps_jqfn",

	"EMAIL_USER" : "email@gmail.com",

	"EMAIL_PASS" : "password-from-google-apps"

}

```

settings.py
```bash
sudo nano django_example/django_example/settings.py
```

```python
import json

with open('/etc/config.json') as config_file:
	config = json.load(config_file)

SECRET_KEY = config['SECRET_KEY']

DEBUG = False

EMAIL_HOST_USER = config.get('EMAIL_USER')
EMAIL_HOST_PASSWORD = config.get('EMAIL_PASS')


```

# UFW changes

Disallow port 8000 & restart Apache to deploy changes

```bash
sudo ufw delete allow 8000 && sudo ufw allow http/tcp

sudo service apache2 restart
```

