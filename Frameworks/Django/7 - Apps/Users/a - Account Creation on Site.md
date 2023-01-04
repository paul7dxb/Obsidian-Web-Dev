# Create App and route

[[a - Routes & Views]]

# Create Registration Form

Django registration form

```

```

## Create templates folder and file

[[b - Templates]]

Add form

Add CSRF token

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

## Extending the default form

Create a new file called froms.py under users directory

```python
from django import forms
from django.contrib.auth.models import User
from django.contrib.auth.forms import UserCreationForm

#Create new class that inherits from UserCreationForm
class UserRegisterForm(UserCreationForm):
    email = forms.EmailField()

    class Meta:
        #model to be affected
        model = User
        # Fields to display in form in order
        fields = ['username', 'email', 'password1', 'password2']
```

Replace the old UserCreationForm import in views.py

```python
from django.shortcuts import render, redirect
from .forms import UserRegisterForm # Form for User creation Extended form from forms.py
from django.contrib import messages #Flash messages library

def register(request):
    if request.method == 'POST':
        form = UserRegisterForm(request.POST)
        #Check form is valid
        if form.is_valid():
            form.save()
            username = form.cleaned_data.get('username')
            messages.success(request, f'Account created for {username}!')
            #Redirect user to home page after successful account create
            return redirect('blog-home')
  
    else:
        form = UserRegisterForm()
    return render(request, 'users/register.html', { 'form' : form })
```

### Improve using crispy forms

[[Crispy Forms#Crispy Forms Sign Up]]

