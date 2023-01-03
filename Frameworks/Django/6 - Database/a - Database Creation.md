# Intro

**ORM - Object Relational Mapper**
Allows  you to access db data in object oriented way
code to query database same for diffferenet database (can do dev with sqlite and production with postgreSQL)

Models represented with classes using models.py

Migrations allow you to make changes a working database model

# Make Migrations

When you change models you need to make migrations. Detects changes

```python
python mananage.py makemigrations

python manage.py migrate
```

## View SQL commands for migration
```
python manage.py sqlmigrate <app_name> <number>
python manage.py sqlmigrate blog 0001
```

# Create Database


# Create Model

Create DB model in models.py file under relevant application

## Useful Models

```Python
#Users
from django.contrib.auth.models import User 
author = models.ForeignKey(User, on_delete=models.CASCADE) #on delete deletes users content

#Date Time
from django.utils import timezone
date_posted = models.DateTimeField(default=timezone.now)
date_posted = models.DateTimeField(auto_now_add=True) #Only sets time on creation
date_modified = models.DateTimeField(auto_now=True) #Sets time to now


```

## Set information to display on access 
(username for user, title for post)

Dunder STR method

In models.py
```python
class Post(models.Model):

    def __str__(self):
        return self.title
```

