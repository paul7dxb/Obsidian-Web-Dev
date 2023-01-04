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
<a class="ml-2" href="{% url 'register' %}">Sign Up Now</a>
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