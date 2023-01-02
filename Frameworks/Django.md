[Tutorial Series Django by Corey Schafer](https://www.youtube.com/watch?v=UmljXZIypDc&list=PL-osiE80TeTtoQCKZ03TU5fNfx2UY6U4p&index=1)


## Setup

Setup virtual python environment

Install Django
```
pip install django
```

## Commands

VSCode start environment
	command pallette (ctrl + shift + p)
	Python: Start REPL

Check version
```
python -m django --version
```

List djjango commands
```
django-admin
```

Start django project from venv
```
django-admin startproject django_example
```

### Running

From project folder

```
python manage.py runserver
```

### Adding Routes

#### Navigation process
- Request made goes to project urls.py
- Matches first part (e.g /blog)
- Uses `include` to send remaining request (taking away blog) to app url.py


Create new app withing website (e.g blog)
Seperates part of project
From project directory (where manage.py is)

```
python .\manage.py startapp blog
```

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


## Templates
