#  Set up AWS S3 bucket for files

[[S3 Buckets]]

# Install Heroku CLI

[Donwload Link](https://devcenter.heroku.com/articles/heroku-cli#install-the-heroku-cli)

```cmd
heroku login
```

# Create requirements.txt

```
pip freeze > requirements.txt
```

# Create Heroku app

```cmd
create djangoherokuusername
heroku open
```

```
https://djangoherokuusername.herokuapp.com/ | https://git.heroku.com/djangoherokuusername.git
```

# Set Static Route

```python
STATIC_ROOT = os.path.join(BASE_DIR, 'staticfiles')
```

# Commiting to Heroku

```bash
git init
git status
git add -A
git commit -m "Git Message"
git push heroku master
```


# Git Push

```cmd
git push heroku master
```

## Setting Remote Heroku App

```
heroku git:remote -a djangoherokuusername
```

# View error logs

```

heroku logs --tail
```

# Create Proc File

In project directory create file call Procfile
```
web: gunicorn django_example.wsgi
```

# DisallowedHost at /

```
ALLOWED_HOSTS = ['djangoherokuusername.herokuapp.com']
```

# Make secret key

[[Environment Variables#Generate secret key]]

# Set Heroku environment variables

```
heroku config:set DEBUG_VALUE="True"

heroku config:set AWS_ACCESS_KEY_ID="AKIAAKJKJHASDJKHASDWFD"
heroku config:set AWS_SECRET_ACCESS_KEY="f5R/34kjhg2jhvga8das8gf7sdfVx9Uj"
heroku config:set AWS_STORAGE_BUCKET_NAME="django-blog-files-username"

heroku config:set EMAIL_PASS="hebdcghjdjaosmnfgjhd"
heroku config:set EMAIL_USER="email@gmail.com"
```


# Set up PostgreSQL

## Get add on

**No longer Free**
```
heroku addons:create heroku-postgresql:hobby-dev
```

## Talk to database

Configures database URL and connects static to gunicorn using white noise package.

```
pip install django-heroku
```

settings.py
```
django_heroku.settings(locals())
```

Recreate [[#Create requirements.txt]]

# Create Tables From Migration

Run migrate command on Heroku

```
heroku run python manage.py migrate
python manage.py createsuperuser
```


