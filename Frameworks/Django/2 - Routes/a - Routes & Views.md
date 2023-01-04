# Navigation process

- Segment features into self contatined "apps"

### How requests find page
- Request made goes to project urls.py
- Matches first part to app (e.g /blog)
- Uses `include` to send remaining request (taking away blog) to app url.py

## Type of Views

- Function Based Views
	- URL pattern directed to view, which is a function
	- handles logic for route and then renders template
- Class based view
	- More built in functionality

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

# POST requests

## Taking Form POST data

```python
from django.shortcuts import render, redirect
from django.contrib.auth.forms import UserCreationForm # Django User Creation Form
from django.contrib import messages #Flash messages library

def register(request):
    if request.method == 'POST':
        form = UserCreationForm(request.POST)
        #Check form is valid
        if form.is_valid():
            form.save()
            username = form.cleaned_data.get('username')
            messages.success(request, f'Account created for {username}!')
            #Redirect user to home page after successful account create
            return redirect('blog-home')
  
    else:
        form = UserCreationForm()
    return render(request, 'users/register.html', { 'form' : form })
```


# Restricting Route Access

import login required decorator

```python
from django.contrib.auth.decorators import login_required

@login_required
def profile(request):
    return render(request, 'users/profile.html')
```

Change login route for django of settings.py

```python
LOGIN_URL = 'login'
```

Django will hold info on attempted page to go to after login

Does not work for class based views

# Class Based Views

- Types
	- List
		- Blogs
		- Youtube subscription
	- Detail
		- Blog page
		- Youtube video page
	- Create
	- Update
	- Delete

Class based Views just need to assign variables compared to function which requires calling functions


Default `<app>/<model>_<viewtype>.html` e.g blog/post_list.html

## Create an equivalent ListView

```python
from django.shortcuts import render
from django.views.generic import ListView # For class based views
from .models import Post

def home(request):
    context = {
        'posts': Post.objects.all()
    }
    return render(request, 'blog/home.html', context)

# Is the same as

class PostListView(ListView):
    model = Post
    template_name = 'blog/home.html'     # <app>/<model>_<viewtype>.html is default
    context_object_name = 'posts'
```

## Add to app's urls.py

```python
from .views import PostListView
from . import views

urlpatterns = [
    path('', PostListView.as_view(), name='blog-home'),
```


## Conventional Class Based DetailView

### Create DetailView
```python
class PostDetailView(DetailView):
    model = Post
```

### Create Route For specific post

URL pattern that contains a variable

urls.py

```python
    path('post/<int:pk>/', PostDetailView.as_view(), name='post-detail'), # pk is primary key, post-detail is the default view name
```