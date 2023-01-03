# Navigation process

- Segment features into self contatined "apps"

### How requests find page
- Request made goes to project urls.py
- Matches first part to app (e.g /blog)
- Uses `include` to send remaining request (taking away blog) to app url.py

# Setting Up Routes
Create new app within website (e.g blog)
Seperates part of project
From project directory (where manage.py is)

## For new app in project

### Create App within Project

```
python .\manage.py startapp blog
```

### Add App to project's setting.py file

Found in app's app.py file
```python
class BlogConfig(AppConfig):
    default_auto_field = 'django.db.models.BigAutoField'
    name = 'blog'
```

Add to to project's setting.py file
```python
INSTALLED_APPS = [
    'blog.apps.BlogConfig',
```

## Create Route
Add response to app's view.py

``` python
def home(request):
    return HttpResponse('<h1>Blog Home</h1>')
```

Create urls.py in app directory

```python 
from . import views
urlpatterns = [
    path('', views.home, name='blog-home'),
]
```

Add app urls to project urls.py if first page of app
```python
from django.urls import path, include

urlpatterns = [
    path('admin/', admin.site.urls),
    path('blog/', include('blog.urls')),
]
```

Or import URL directly to urls.py
``` python

```

# Linking to DB data

Use views.py to import models data
Import required models
Add quieries to route function
```python
from .models import Post

def home(request):
    context = {
        'posts': Post.objects.all()
    }
    return render(request, 'blog/home.html', context)

```

# Post requests
