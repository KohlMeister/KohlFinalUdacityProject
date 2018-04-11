# Udacity Full Stack Web Developer Final Project

## Project Description:
You will take a baseline installation of a Linux distribution on a virtual machine and prepare it to host your web applications, to include installing updates, securing it from a number of attack vectors and installing/configuring web and database servers.

## Submission Requirements

* IP Address: 52.25.3.13
* SSH Port: 2200
* Application URL: http://ec2-52-25-3-13.us-west-2.compute.amazonaws.com
* Software installed and configuration changes: Below
* Third Party Resources: Below

### Software Installed and Configuration Changes

#### Update currently installed packages
Run: `sudo apt-get update` <br />
Run: `sudo apt-get upgrade`

#### Configure SSH port
Run: `sudo nano /etc/ssh/sshd_config` <br />
Update line ~5 from `Port 22` to `Port 2200`

#### Configure Uncomplicated Firewall
Run: `sudo ufw allow 2200/tcp` <br />
Run: `sudo ufw allow 80/tcp` <br />
Run: `sudo ufw allow 123/udp` <br />
Run: `sudo ufw enable`

#### Add user 'grader'
Run: `sudo adduser grader` <br />
Run: `sudo nano /etc/sudoers.d/grader` <br />
Add line `grader ALL=(ALL) NOPASSWD:ALL`

#### Create SSH key pair
Run: `ssh-keygen` locally using git bash <br />
Then on VM: <br />
Run: `sudo mkdir /home/grader/.ssh` <br />
Run: `sudo touch /home/grader/.ssh/authorized_keys` <br />
Run: `sudo nano /home/grader/.ssh/authorized_keys` and copy locally created key<br />
Run: `sudo chmod 700 /home/grader/.ssh` <br />
Run: `sudo chmod 644 /home/grader/.ssh/authorized_keys` <br />
Run: `sudo service ssh restart` <br />

Ensure owner and group are grader: <br />
Run: `sudo chown grader /home/grader/.ssh` <br />
Run: `sudo chgrp grader /home/grader/.ssh` <br />
Run: `sudo chown grader /home/grader/.ssh/authorized_keys` <br />
Run: `sudo chgrp grader /home/grader/.ssh/authorized_keys`

#### Configure local timezone
Run: `sudo dpkg-reconfigure tzdata` and select UTC

#### Remove ability to login as root remotely
Run: `sudo nano /etc/ssh/sshd_config` <br />
Update `PermitRootLogin prohibit-password` to `PermitRootLogin no`

#### Install Apache and mod_wsgi
Run: `sudo apt-get install apache2` <br />
Run: `sudo apt-get install python-setuptools libapache2-mod-wsgi` <br />
Run: `sudo service apache2 restart`

#### Install and Configure PostgreSQL
Run: `sudo apt-get install postgresql postgresql-contrib` <br />
//Run: `sudo -u postgres createusr -P catalog` <br />
//Run: `sudo -u postgres createdb -O catalog catalog`

#### Install git
Run: `sudo apt-get install git`

#### Changes make to ensure app functions correctly

##### Configure and enable new virtual host
Test app by following Digital Ocean <br />
Run: `cd /var/www` <br />
Run: `sudo mkdir catalog` <br />
Run: `sudo mkdir catalog/catalog` <br />
Run: `cd catalog/catalog` <br />
Run: `sudo mkdir static templates` <br />
Run: `sudo nano __init__.py` <br />
Add to file: <br />
```python
from flask import Flask
app = Flask(__name__)
@app.route("/")
def hello():
    return "Hello, I love Digital Ocean!"
if __name__ == "__main__":
    app.run()
```
Run: `sudo apt-get install python-pip` <br />
Run: `sudo pip install virtualenv` <br />
Run: `sudo virtualenv venv` <br />
Run: `source venv/bin/activate` <br />
Run: `sudo pip install Flask` <br />
Run: `sudo python __init__.py` <br />
Run: `deactivate`
<br /><br />
Run: `sudo nano /etc/apache2/sites-available/catalog.conf` <br />
Add to file: <br />
```xml
<VirtualHost *:80>
		ServerName 52.25.3.13
		ServerAdmin admin@52.25.3.13
    		ServerAlias http://ec2-52-25-3-13.us-west-2.compute.amazonaws.com
		WSGIScriptAlias / /var/www/catalog/catalog.wsgi
		<Directory /var/www/catalog/catalog/>
			Order allow,deny
			Allow from all
		</Directory>
		Alias /static /var/www/catalog/catalog/static
		<Directory /var/www/catalog/catalog/static/>
			Order allow,deny
			Allow from all
		</Directory>
		ErrorLog ${APACHE_LOG_DIR}/error.log
		LogLevel warn
		CustomLog ${APACHE_LOG_DIR}/access.log combined
</VirtualHost>
```
Run: `sudo nano /var/www/catalog/catalog.wsgi` <br />
Add to file: <br />
```python
#!/usr/bin/python
import sys
import logging
logging.basicConfig(stream=sys.stderr)
sys.path.insert(0,"/var/www/catalog/")

from catalog import app as application
application.secret_key = 'Add your secret key'
```
Run: `sudo service apache2 restart` <br />

##### Install Flask and Associated Libraries
Clone Item Catalog Project
Run: `sudo git clone https://github.com/KohlMeister/Udacity_Drink_Catalog`
Run: `sudo `
Run: `sudo mv catalog_website.py __init__.py` <br />
Run: `sudo pip install httplib2` <br />
Run: `sudo pip install oauth2client` <br />
Run: `sudo pip install sqlalchemy` <br />
Run: `sudo pip install psycopg2` <br />
Run: `sudo pip install passlib` <br />
Run: `sudo pip install requests`



### Third Party Resources

* [Deploy Flask App with Ubuntu - Digital Ocean](https://www.digitalocean.com/community/tutorials/how-to-deploy-a-flask-application-on-an-ubuntu-vps)
