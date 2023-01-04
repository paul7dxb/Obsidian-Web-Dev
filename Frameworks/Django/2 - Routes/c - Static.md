Make static folder inside app with subfolder same name as app

Create static files as required

# Linking static files

At top of document
```
{% load static %}
```

CSS
```html
<link rel="stylesheet" type="text/css" href="{% static 'blog/main.css' %}">
```

Route
```html
<!-- register loooked up in urls.py -->
<a class="ml-2" href="{% url 'register' %}">Sign Up Now</a>
```

Using Variables in Routes
```python
    path('post/<int:pk>/', PostDetailView.as_view(), name='post-detail'), # pk is primary key, post-detail is the default view name
```

```html
<a class="ml-2" href="{% url 'register' %}">Sign Up Now</a>

<!-- Accessing /post/4 where 4 is the post primary key id -->
<h2><a class="article-title" href="{% url 'post-detail' post.id %}"> {{ post.title }}</a></h2>
```

# Set Location for Uploaded Media


settings.py
media root and media url

```python
import os

# Full path for where Django will store uploaded files. File system, not DB
MEDIA_ROOT = os.path.join(BASE_DIR, 'media')

# Where to access media folder in browser
MEDIA_URL = '/media/'
```



# Deploying Static Files

TODO Read docs