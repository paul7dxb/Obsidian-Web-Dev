
# Navigation
Process of 

- password-reset
- password-reset/done
- Receive email
- password-reset-confirm (with id and token)
- password-reset-complete

# Implementation
urls.py

```python
urlpatterns = [
	...
    path('password-reset/', auth_views.PasswordResetView.as_view(template_name="users/password_reset.html"), name='password_reset'),
    path('password-reset/done/', auth_views.PasswordResetDoneView.as_view(template_name="users/password_reset_done.html"), name='password_reset_done'),
	path('password-reset-confirm/<uidb64>/<token>/', auth_views.PasswordResetConfirmView.as_view(template_name="users/password_reset_confirm.html"), name='password_reset_confirm'),
	path('password-reset-complete/', auth_views.PasswordResetCompleteView.as_view(template_name="users/password_reset_complete.html"), name='password_reset_complete'),

    ...
```

password_reset.html
```html
{% extends "blog/base.html" %}

{% load crispy_forms_tags %}

    {% block content %}
        <div class="content-section">
            <form method="POST">
                {% csrf_token %}
                <fieldset class="form-group">
                    <legend class="border-bottom mb-4">Reset Password</legend>
                    {{ form|crispy }}
                </fieldset>
                <div class="form-group">
                    <button class="btn btn-outline-info" type="submit"> Request Password Reset </button>
                </div>
            </form>

        </div>
{% endblock content %}

```

password_reset_done.html
```html
{% extends "blog/base.html" %}

    {% block content %}

        <div class="alert alert-info">
            An emails has been sent with instructions to reset your password
        </div>

    {% endblock content %}

```

password_reset_confirm.html
```html
{% extends "blog/base.html" %}

{% load crispy_forms_tags %}

    {% block content %}
        <div class="content-section">
            <form method="POST">
                {% csrf_token %}
                <fieldset class="form-group">
                    <legend class="border-bottom mb-4">Reset Password</legend>
                    {{ form|crispy }}
                </fieldset>
                <div class="form-group">
                    <button class="btn btn-outline-info" type="submit"> Reset Password </button>
                </div>
            </form>

        </div>
{% endblock content %}

```

password_reset_complete.html
```html
{% extends "blog/base.html" %}

    {% block content %}

        <div class="alert alert-info">
            Your Password has been set
        </div>
        <a href="{% url 'login' %}">Sign In Here</a>

    {% endblock content %}

```

# Fix error

Error on submit

> Reverse for 'password_reset_confirm' not found. 'password_reset_confirm' is not a valid view function or pattern name.

> {{ protocol }}://{{ domain }}{% url 'password_reset_confirm' uidb64=uid token=token %}

Need to accept parameters in URL. Adding security to routes
user id base 64 
user token

# Fix connection Error

Cannot send email

> ConnectionRefusedError at /password-reset/

Need email server

# Gmail App password sign in

Let google know to expect sign ins from Python

Use [[Environment Variables]] & [[Gmail App Password]] to let server sign in to required gmail account

# Add reset to login

login.html
```html
<small class="text-muted ml-2" >
	<a href="{% url 'password_reset' %}">Forgot Password?</a>
</small>
```

