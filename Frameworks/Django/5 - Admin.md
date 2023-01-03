# Create Database

[[6 - Database|Create DB and make migrations]]

# Create new admin user


```python
python manage.py createsuperuser 
```

# Admin panel access to DB

Register model with admin page

Go to admin.py in app directory
Import model and register with admin site

```python
from django.contrib import admin
from .models import Post

admin.site.register(Post)
```
