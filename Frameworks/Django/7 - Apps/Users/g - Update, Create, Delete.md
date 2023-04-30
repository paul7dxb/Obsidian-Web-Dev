
Using [[a - Routes & Views#Class Based Views|class based view]]

# Add Class to views.py

```python
from django.contrib.auth.mixins import (LoginRequiredMixin, # Used in class based views instead of login required decorator.
    UserPassesTestMixin)  # UserPassesTestMixin for correct user accessing
from django.views.generic import (ListView, 
    DetailView, 
    CreateView, 
    UpdateView, 
    DeleteView) # For class based views

class PostCreateView(LoginRequiredMixin, CreateView):
    model = Post
    fields = ['title', 'content']

    # Use current logged in user as author
    def form_valid(self, form):
        form.instance.author = self.request.user
        return super().form_valid(form)

class PostUpdateView(LoginRequiredMixin, UserPassesTestMixin, UpdateView):
    model = Post
    fields = ['title', 'content']

    # Use current logged in user as author
    def form_valid(self, form):
        form.instance.author = self.request.user
        return super().form_valid(form)

    def test_func(self):
        post = self.get_object() # gets current post trying to update
        if self.request.user == post.author:
            return True
        else:
            return False

class PostDeleteView(LoginRequiredMixin, UserPassesTestMixin, DeleteView):
    model = Post
    success_url = '/'

    def test_func(self):
        post = self.get_object() # gets current post trying to update
        if self.request.user == post.author:
            return True
        else:
            return False
```

# Update urls.py

```python
from .views import PostListView, PostDetailView, PostCreateView, PostUpdateView, PostDeleteView

urlpatterns = [
    path('post/<int:pk>/', PostDetailView.as_view(), name='post-detail'), # pk is primary key, post-detail is the default view name
    path('post/new/', PostCreateView.as_view(), name='post-create'), # default view is post_form. Same as update view
    path('post/<int:pk>/update/', PostUpdateView.as_view(), name='post-update'), # pk is primary key, post-update uses post_form.html
    path('post/<int:pk>/delete/', PostDeleteView.as_view(), name='post-delete'), # pk is primary key, post-delete uses post_confirm_delete.html


```

# Update model to be able to use primary key

```python
# get absolute url method to redirect to post after creating a new post
def get_absolute_url(self):
	return reverse('post-detail', kwargs={'pk' : self.pk})
```
# Create related templates for classes to use

![[Image_blog_file_structure.png]]
