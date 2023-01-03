## Django provided login view

<span style=" font-size:1.3em;">Uses Class based views!</span>

In project urls.py

Point the views to Users app templates

```python
from django.contrib.auth import views as auth_views

urlpatterns = [
	    path('login/', auth_views.LoginView.as_view(template_name="users/login.html"), name='login'),
    path('logout/', auth_views.LogoutView.as_view(template_name="users/logout.html"), name='logout'),
```

Create Users app templates for login and logout
- users
	- templates
		- users
			- login.html
			- logout.html

Change redirect URL for successful login in project settings.py
```python
LOGIN_REDIRECT_URL = 'blog-home'
```



