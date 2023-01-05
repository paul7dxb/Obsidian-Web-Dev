# Filter posts by username

views.py

```python
from django.shortcuts import render, get_object_or_404
from django.contrib.auth.models import User

class UserPostListView(ListView):
    model = Post
    template_name = 'blog/user_posts.html'     # <app>/<model>_<viewtype>.html is default
    context_object_name = 'posts'
    paginate_by = 5

    def get_queryset(self):
        user = get_object_or_404(User, username = self.kwargs.get('username'))
        return Post.objects.filter(author = user).order_by('-date_posted')

```

urls.py

```python
path('user/<str:username>', UserPostListView.as_view(), name='user-posts'),
```

Accessing user in Template

```html
<h1 class="mb-3" >Posts by {{ view.kwargs.username }} ({{ page_obj.paginator.count }} posts) </h1>
```