
# Setup

```bash
cd
sudo apt-get install apache2
sudo apt-get install libapache2-mod-wsgi-py3
```

[[Linode Web Server#TESTING Move Files to www]]

```bash
cd /etc/apache2/sites-available/
sudo cp 000-default.conf django_example.conf
sudo nano django_example.conf
```

copy base apache config

https://github.com/CoreyMSchafer/code_snippets/blob/master/Django_Blog/snippets/django_project.conf

```
<VirtualHost *:80>


    ServerAdmin webmaster@localhost
    DocumentRoot /var/www/html


    ErrorLog ${APACHE_LOG_DIR}/error.log
    CustomLog ${APACHE_LOG_DIR}/access.log combined


  Alias /static /home/YOURUSER/YOURPROJECT/static
  <Directory /home/YOURUSER/YOURPROJECT/static>
    Require all granted
  </Directory>

  Alias /media /home/YOURUSER/YOURPROJECT/media
  <Directory /home/YOURUSER/YOURPROJECT/media>
    Require all granted
  </Directory>

  <Directory /home/YOURUSER/YOURPROJECT/YOURPROJECT>
    <Files wsgi.py>
      Require all granted
    </Files>
  </Directory>

  WSGIScriptAlias / /home/YOURUSER/YOURPROJECT/YOURPROJECT/wsgi.py
  WSGIDaemonProcess django_app python-path=/home/YOURUSER/YOURPROJECT python-home=/home/YOURUSER/YOURPROJECT/venv
  WSGIProcessGroup django_app

</VirtualHost>

# vim: syntax=apache ts=4 sw=4 sts=4 sr noet
```

TESTING /var/www
```
<VirtualHost *:80>


    ServerAdmin webmaster@localhost
    DocumentRoot /var/www/html


    ErrorLog ${APACHE_LOG_DIR}/error.log
    CustomLog ${APACHE_LOG_DIR}/access.log combined


	  Alias /static /var/www/django_example/static
	  <Directory /var/www/django_example/static>
		Require all granted
	  </Directory>
	
	  Alias /media /var/www/django_example/media
	  <Directory /var/www/django_example/media>
		Require all granted
	  </Directory>
	
	  <Directory /var/www/django_example/django_example>
		<Files wsgi.py>
		  Require all granted
		</Files>
	  </Directory>
	
	  WSGIScriptAlias / /var/www/django_example/django_example/wsgi.py
	  WSGIDaemonProcess django_app python-path=/var/www/django_example python-home=/var/www/django_example/venv
	  WSGIProcessGroup django_app

</VirtualHost>

# vim: syntax=apache ts=4 sw=4 sts=4 sr noet
```

Replace YOURUSER and YOURPROJECT using
```bash
sed -i 's/original/new/g' django_project.conf

sudo sed -i 's/YOURUSER/username/g' django_project.conf  
sudo sed -i 's/YOURPROJECT/django_example/g' django_project.conf  

```

## Enable / Disable site through Apache

```
cd ~

sudo a2ensite django_example
sudo a2dissite 000-default.conf 
```

## Change permissions

Apache to read and write to SQL and media folder

Apache group owner on the DB
```bash
sudo chown :www-data django_example/db.sqlite3 
sudo chmod 664 django_example/db.sqlite3 
sudo chown :www-data django_example/ 

```

Media folder
```bash
sudo chown -R :www-data django_example/media/
sudo chmod -R 775 django_example/media
```

Return to server setup now

# Logs

```bash
sudo tail -n 50 /var/log/apache2/error.log
sudo tail -n 50 /var/log/apache2/access.log     
sudo tail -n 50 /var/log/apache2/other_vhosts_access.log  


sudo journalctl -u apache2.service --since today --no-pager
```

# Check Apache Status

```bash
sudo systemctl status apache2.service -l --no-pager
```

# Restart Apache Service

```bash
sudo service apache2 restart
```