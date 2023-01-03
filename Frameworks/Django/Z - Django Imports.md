## Messages

- debug
- info
- success
- warning
- error
```python
from django.contrib import messages

messages.success(request, f'Account created for {username}!')
```


# Redirect

```python
from django.shortcuts import  redirect
```