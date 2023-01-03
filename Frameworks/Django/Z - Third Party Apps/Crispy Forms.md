# Crispy Forms Sign Up

- Styles forms in bootstrap fashion
- Colours error tags

Install crispy forms in python environment

```
pip install django-crispy-forms
```

Tell Django it is installed
Project settings.py

```python
INSTALLED_APPS = [
    'crispy_forms',
```

Tell crispy forms which CSS styling to use

```python
CRISPY_TEMPLATE_PACK = 'bootstrap4'
```

Load into form

```html
{% extends "blog/base.html" %}

{% load crispy_forms_tags %}

    {% block content %}

        <div class="content-section">
            <form method="POST">
                {% csrf_token %}
                <fieldset class="form-group">
                    <legend class="border-bottom mb-4">Join Today</legend>
                    {{ form|crispy }}
                </fieldset>
                <div class="form-group">
                    <button class="btn btn-outline-info" type="submit"> Sign Up</button>
                </div>
            </form>
            <div class="border-top pt-3">
                <small class="text-muted">
                    Already have an account? <a class="ml-2" href="#">Log in</a>
                </small>
            </div>
        </div>

{% endblock content %}

```