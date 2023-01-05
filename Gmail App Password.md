2FA set up

go to google app passowords

Register device

Get password


# Add gmail credentials

Add credentials to [[Environment Variables]]

Add to settings.py
``` python
EMAIL_HOST_USER = os.environ.get('EMAIL_USER')
EMAIL_HOST_PASSWORD = os.environ.get('EMAIL_PASS')
```


# linode set up 
https://www.linode.com/community/questions/19082/i-just-created-my-first-linode-and-i-cant-send-emails-why
