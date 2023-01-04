## Extend existing user model from django

In App's models.py
```python
from django.contrib.auth.models import User

class Profile(models.Model):
    #One to one relationship with User Acccount. CASCADE will delete profile on user deletion. Not other way around
    user = models.OneToOneField(User, on_delete=models.CASCADE)
    # Profile picture. Choose default image and directory where profile pictures are stored
    image = models.ImageField(default='default.jpg', upload_to='profile_pics')

    # Dunder STR method for printing out object
    def __str__(self) -> str:
        return f'{self.user.username} Profile'
```

## Install Pillow

Library for working with images in Python

```
pip install pillow
```

## Do Migrations

[[a - Database Creation#Make Migrations|Make DB Migrations]]

## Register Profile Model to View on Admin Site

[[SuperUser Admin#Admin panel access to DB]]

Check on Admin Page section is accessable

## Access profile from user in DB

```python
>>> user = User.objects.filter(username='mcpapa').first() 
>>> user
<User: mcpapa>
>>> user.profile
<Profile: mcpapa Profile>
>>> user.profile.image
<ImageFieldFile: profile_pics/growlithe.png>
>>> user.profile.image.width
1920
>>> user.profile.image.url  
'/profile_pics/growlithe.png'
```


# Change location for Image storage

[[c - Static#Set Location for Uploaded Media]]

## Add Image to page

```html
<img class="rounded-circle account-img" src="{{ user.profile.image.url }}">
```

# 

Add to project urls.py

# Use Signals to create profile with new user

Create signals.py file in App directory

```python
from django.db.models.signals import post_save # Fires after a object is saved
from django.contrib.auth.models import User
from django.dispatch import receiver # Receiver gets signal and performs task. Decorator
from .models import Profile

# When User is saved send signal
# Get post_save signal when user is created
@receiver(post_save, sender=User)
def create_profile(sender, instance, created, **kwargs): #kwargs accepts additional keyword arguments. post save signal sends argurments. instance is instance of user created
    if created:
        Profile.objects.create(user=instance)

# If User is saved also save the profile
@receiver(post_save, sender=User)
def save_profile(sender, instance, created, **kwargs):
    instance.profile.save()
```

## Import signals in ready function of Users app.py
In apps.py in Users

```python
class UsersConfig(AppConfig):
    default_auto_field = 'django.db.models.BigAutoField'
    name = 'users'

    def ready(self):
        import users.signals
```