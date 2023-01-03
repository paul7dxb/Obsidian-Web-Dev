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

[[SuperUser Admin#Admin panel access to DB|Admin: Access DB from admin site]]
