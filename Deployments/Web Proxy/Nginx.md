

# Nginx, gunicorn, django configurations

Also include HTTPS
https://realpython.com/django-nginx-gunicorn/

https://www.linode.com/docs/guides/deploy-django-applications-using-uwsgi-and-nginx-on-ubuntu-14-04/


# TODO In Progress need to complete
[

## Install nginx, Python Tools and uWSGI

](https://www.linode.com/docs/guides/deploy-django-applications-using-uwsgi-and-nginx-on-ubuntu-14-04/#install-nginx-python-tools-and-uwsgi)

1.  Install the system packages required for nginx, the SQLite Python bindings, and managing Python Tools:

```bash
sudo apt-get install build-essential nginx python-dev python-pip python-sqlite sqlite
```

## Install [virtualenv](https://virtualenv.pypa.io/en/latest/) and [virtualenvwrapper](http://virtualenvwrapper.readthedocs.org/en/latest/):

```
sudo apt-get install python3-pip
sudo pip install virtualenv virtualenvwrapper
```

`virtualenv` and `virtualenvwrapper` are tools to create isolated Python environments. They help better manage application dependencies, versions and permissions. For `virtualenvwrapper` to function correctly, run the following commands:

```
echo "export WORKON_HOME=~/Env" >> ~/.bashrc
echo "source /usr/local/bin/virtualenvwrapper.sh" >> ~/.bashrc
```




## Activate `virtualenvwrapper` in the current session:

```
source ~/.bashrc
```

## Install uWSGI using `pip`:

```
sudo pip install uwsgi
```

## Set up a Sample Django Application

[Linode Docs Link](https://www.linode.com/docs/guides/deploy-django-applications-using-uwsgi-and-nginx-on-ubuntu-14-04/#set-up-a-sample-django-application)

1.  Be sure that you’re in the `django` user’s home directory and create the virtual environment for the application:
    
    ```
    cd /home/username && mkvirtualenv sample
    ```
    
    After executing this command your prompt will change to something like `(sample)django@example.com:~$` indicating that you are using the sample virtual environment. To quit the virtual environment, enter `deactivate`.
    ## Test

```
sudo gedit ~/.bashrc
```

After opening it, add the following  lines to it :

```
export WORKON_HOME=$HOME/.virtualenvs
export PROJECT_HOME=$HOME/Devel
source /usr/local/bin/virtualenvwrapper.sh
```

**Using mkvirtualenv command**


```
mkvirtualenv venv_name
```

If you want to work on another version of python, try this :

```
$ mkvirtualenv -p python3.x venv_name
$(venv_name) // You will see something like this
```

Note: You can use any version in place of x. 

To work on an existing virtual environment,

```
$ workon venv_name
```

To get out of the virtual environment –

```
$(venv_name) deactivate
```

To see the list of your virtual environments are, go to-

```
Home/.virtualenvs
```

## End of test


2.  Install the Django framework:
    
    ```
    pip install Django
    ```
    
3.  Create the new Django application _sample_, located at `/home/django/sample`:
    
    ```
    django-admin.py startproject sample
    ```
    
4.  Switch to the Django application’s directory and initialize SQLite database:
    
    ```
    cd ~/sample && ./manage.py migrate
    ```
    
5.  When running Django with nginx, it’s necessary to configure Django to put all static assets in your application’s `static` folder. Specify its location in `settings.py`:
    
    ```
    echo 'STATIC_ROOT = os.path.join(BASE_DIR, "static/")' >> sample/settings.py
    ```
    
6.  Run the following command to move all static assets into the directory mentioned above:
    
    ```
    ./manage.py collectstatic
    ```
    
7.  Start a development server to test the sample application:
    
    ```
    ./manage.py runserver 0.0.0.0:8080
    ```
    
    Visit `http://example.com:8080` in your browser to confirm that the sample application is set up correctly and working. You should see the Django test page:
    
    ![Django test page.](https://www.linode.com/docs/guides/deploy-django-applications-using-uwsgi-and-nginx-on-ubuntu-14-04/django-test-page_hu73d7446e4bba9848c927269b0e27f060_37556_1388x0_resize_q71_bgfafafc_catmullrom_3.jpg "Django test page.")
    
    Then stop development server with **Ctrl-C**.
    

[

## Configure uWSGI

](https://www.linode.com/docs/guides/deploy-django-applications-using-uwsgi-and-nginx-on-ubuntu-14-04/#configure-uwsgi)

1.  Create a directory with uWSGI configuration files:
    
    ```
    sudo mkdir -p /etc/uwsgi/sites
    ```
    
2.  Create configuration file `sample.ini` with the following contents:
    

File: /etc/uwsgi/sites/sample.ini

-   ```ini
    [uwsgi]
    project = sample
    base = /home/django
    
    chdir = %(base)/%(project)
    home = %(base)/Env/%(project)
    module = %(project).wsgi:application
    
    master = true
    processes = 2
    
    socket = %(base)/%(project)/%(project).sock
    chmod-socket = 664
    vacuum = true
    ```
    
-   Create an Upstart job for uWSGI:
    

File: /etc/init/uwsgi.conf

1.  ```aconf
    description "uWSGI"
    start on runlevel [2345]
    stop on runlevel [06]
    respawn
    
    env UWSGI=/usr/local/bin/uwsgi
    env LOGTO=/var/log/uwsgi.log
    
    exec $UWSGI --master --emperor /etc/uwsgi/sites --die-on-term --uid django --gid www-data --logto $LOGTO
    ```
    
    This job will start uWSGI in _Emperor_ mode, meaning that it will monitor `/etc/uwsgi/sites` directory and will spawn instances (_vassals_) for each configuration file it finds. Whenever a config file is changed, the emperor will automatically restart its vassals.
    
2.  Start the `uwsgi` service:
    
    ```
    sudo service uwsgi start
    ```
    

[

## Configure nginx

](https://www.linode.com/docs/guides/deploy-django-applications-using-uwsgi-and-nginx-on-ubuntu-14-04/#configure-nginx)

1.  Remove the default nginx site configuration:
    
    ```
    sudo rm /etc/nginx/sites-enabled/default
    ```
    
2.  Create an nginx site configuration file for your Django application:
    

File: /etc/nginx/sites-available/sample

-   ```aconf
    server {
        listen 80;
        server_name example.com;
    
        location = /favicon.ico { access_log off; log_not_found off; }
        location /static/ {
            root /home/django/sample;
        }
    
        location / {
            include         uwsgi_params;
            uwsgi_pass      unix:/home/django/sample/sample.sock;
        }
    }
    ```
    
-   Create a symlink to nginx’s `sites-enabled` directory to enable your site configuration file:
    
    ```
    sudo ln -s /etc/nginx/sites-available/sample /etc/nginx/sites-enabled
    ```
    
-   Check nginx’s configuration and restart it:
    
    ```
    sudo service nginx configtest && sudo service nginx restart
    ```
    
-   You should now be able to reach your Django application by visiting your Linode’s hostname or IP address on port 80 in your browser.