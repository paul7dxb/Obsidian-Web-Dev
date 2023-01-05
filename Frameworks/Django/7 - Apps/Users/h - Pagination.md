# Intro

Improve performance by loading in a certain amount of posts per page and then have links at the bottom to more objects

## Optional add dummy data

Add posts.json to same directory as manage.py

```python

import json
from blog.models import Post

with open('posts.json') as f:
...     posts_json = json.load(f)  
... 

>>> for post in posts_json:
...     post = Post(title= post['title'], content=post['content'], author_id = post['user_id'])
...     post.save()
...
... exit()
    
```

## Paginator Class

``` python
from django.core.paginator import Paginator

posts = ['post1', 'post2', 'post3', 'post4', 'post15']
p = Paginator(posts, 2) # 2 posts per page
p.num_pages # Returns total number of pages (3)
for page in p.page_range: # Looping thorugh pages
	print(page)

p1 = p.page(1)
p1.number
p1.object_list
p1.has_previous() #Lets you know if there is a previous page (1 returns False)
p1.has_next() #Lets you know if there is a next page (1 returns True)
p1.next_page_number # Gets page number of next page
```

# Add to DetailView Class View

``` python
class PostListView(ListView):
	...
    paginate_by = 5 # How many posts to show per page

```

Access other pages using url parameter /?page=\<num\>
Get 404 error going to page to big

# Add page navigation

```html
<!-- Pagination -->
{% if is_paginated %}

	{% if page_obj.has_previous %}
		<a class="btn btn-outline-info mb-4" href="?page=1">First</a>
		<a class="btn btn-outline-info mb-4" href="?page={{ page_obj.previous_page_number }}">Previous</a>
	{% endif %}

	{% for num in page_obj.paginator.page_range %}
		{% if page_obj.number == num %}
			<a class="btn btn-info mb-4" href="?page={{ num }}">{{ num }}</a>
		{% elif num > page_obj.number|add:'-3' and num < page_obj.number|add:'3' %}
			<a class="btn btn-outline-info mb-4" href="?page={{ num }}">{{ num }}</a>
		{% endif %}
	
	{% endfor %}

	{% if page_obj.has_next %}
		<a class="btn btn-outline-info mb-4" href="?page={{ page_obj.next_page_number }}">Next</a>
		<a class="btn btn-outline-info mb-4" href="?page={{ page_obj.paginator.num_pages }}">Last</a>
	{% endif %}

{% endif %}
```

