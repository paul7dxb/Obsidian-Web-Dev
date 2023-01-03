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

# Database interaction in Python

## Command line interatction

``` python
python manage.py shell 

# import models
from blog.models import Post
from django.contrib.auth.models import User
```

## Query Table
```python
User.objects.all() # View all users
User.objects.filter(username='name') #Find users with username. Returns list even if single
user = User.objects.filter(username='name').first() #Find first user with username
user = User.objects.get(id=1) #Find first user with username

# Access object attributes
user.id
user.pk

#Access using foreign key
post_1.author.email

#Get set from relation table. E.g a user's posts
# Uses many to one manager
user.post_set
# This can then be queried
user.post_set.all()

```

## Create new data entry and save to DB

```python
post_1 = Post(title = 'Blog Post 1', content = 'First Post content', author = user)
	# Same as
post_1 = Post(title = 'Blog Post 1', content = 'First Post content', author_id = user.id)


post_1.save()

# Create data using reverse many to one data
	# E.g a new post for a user
	# Takes author from user
	#Does not require .save()
	
user.post_set.create(title='Blog 4', content = 'Fourth Post content')


```

## Admin DB from admin site

[[5 - Admin#Admin panel access to DB|Admin: Access DB from admin site]]
