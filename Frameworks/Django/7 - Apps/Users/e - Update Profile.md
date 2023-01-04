# Create Forms

Within App's form.py (may need to create)
- Model Form
	- Form to update User model
	- Works with specific DB model
	- Form to update profile Picture

```python
from .models import Profile #Import model

class UserUpdateForm(forms.ModelForm):
    email = forms.EmailField()

    class Meta:
        #model to be affected
        model = User
        # Fields to display in form in order
        fields = ['username', 'email']


class ProfileUpdateForm(forms.ModelForm):
    class Meta:
        model = Profile
        fields = ['image']
```

# Add forms to Profile Page

## Add context to requested view

App's views.py
```python
from .forms import UserUpdateForm, ProfileUpdateForm

@login_required
def profile(request):
    u_form = UserUpdateForm()
    p_form = ProfileUpdateForm()

    context = {
        'u_form' : u_form,
        'p_form' : p_form
    }
    return render(request, 'users/profile.html', context)
```

## Add Form to profile.html

Add multiple forms to one HTML form tag using the variable from the context


```html
<form method="POST">
	{% csrf_token %}
	<fieldset class="form-group">
		<legend class="border-bottom mb-4">Profile Info</legend>
		{{ u_form|crispy }}
		{{ p_form|crispy }}
	</fieldset>
	<div class="form-group">
		<button class="btn btn-outline-info" type="submit"> Update </button>
	</div>
</form>
```

## Add encoding for form with image

```html
<form method="POST" enctype="multipart/form-data">
```

# Process POST request from form

In app's views.py

```python
@login_required
def profile(request):
    if request.method == 'POST':
        u_form = UserUpdateForm(request.POST, instance=request.user)
        p_form = ProfileUpdateForm(request.POST, request.FILES,  instance=request.user.profile)
        if u_form.is_valid() and p_form.is_valid():
            u_form.save()
            p_form.save()
            messages.success(request, f'Your account has been updated')
            return redirect('profile') #POST GET redirect pattern, forces GET request instead of post
    else:
        u_form = UserUpdateForm(instance=request.user)
        p_form = ProfileUpdateForm(instance=request.user.profile)

    context = {
        'u_form' : u_form,
        'p_form' : p_form
    }
    return render(request, 'users/profile.html', context)
```

# Resize uploaded image

[[Pillow#Resizing uploaded images|Resize uploaded image with Pillow package]]

