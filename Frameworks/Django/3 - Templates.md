
Create folder 'templates' in app folder
Create folder in templates named the same as the app (django convention)

Add app (blog) configuration to INSTALLED_APPS in settings.py. Class name is taken from apps.py in app folder

```python
# Application definition
INSTALLED_APPS = [
    'blog.apps.BlogConfig',
```

In views.py return rendered template
```python
def home(request):
    return render(request, 'blog/home.html') #folder in templates followed by file
```


# Django context variable access

```
{% %}
```

```
{% for item in list %}
	<h1> {{ item.title }} </h1>
{% endfor %}
```

```
{% if %}
	<h1> {{ item.title }} </h1>
{% endif %}
```

# Base.html

Used to hold repeated sections and use blocks for unique content pages will add

```html
<!DOCTYPE html>

<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    {% if title %}
        <title>Django Blog - {{ title }}</title>
    {% else %}
        <title>Django Blog</title>
    {% endif %}
    
</head>
<body>

    <!--Create block for content to into -->
    {% block content %} {% endblock %}
    
</body>
</html>
```

### Extend base.html in templates

```html
{% extends "blog/base.html" %}
    {% block content %}
        {% for post in posts %}
            <h1>{{ post.title }}</h1>
            <p>By {{post.author }} on {{ post.date_posted }}</p>
            <p>By {{post.content }}</p>
        {% endfor %}    
    {% endblock content %}
```

### Django URL paths

From URL patterns reference pages using its name
``` python
urlpatterns = [
    path('', views.home, name='blog-home'),
]
```

```html
<a class="nav-item nav-link" href="{% url 'blog-home' %}">Home</a>
```

Note: Cannot reference URL's before they exist