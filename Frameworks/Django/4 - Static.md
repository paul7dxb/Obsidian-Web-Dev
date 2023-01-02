Make static folder inside app with subfolder same name as app

Create static files as required

## Linking static files

At top of document
```
{% load static %}
```

CSS
```html

    <link rel="stylesheet" type="text/css" href="{% static 'blog/main.css' %}">
```