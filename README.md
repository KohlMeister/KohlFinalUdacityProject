# Udacity Full Stack Web Developer Final Project

## Project Description:
You will take a baseline installation of a Linux distribution on a virtual machine and prepare it to host your web applications, to include installing updates, securing it from a number of attack vectors and installing/configuring web and database servers.

## Submission Requirements

* IP Address: 34.214.113.147
* SSH Port: 2200
* Application URL: 
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
Run: `touch /home/grader/.ssh/authorized_keys` <br />
Run: `nano /home/grader/.ssh/authorized_keys` and copy locally created key<br />
Run: `chmod 700 /home/grader/.ssh` <br />
Run: `chmod 644 /home/grader/.ssh/authorized_keys` <br />
Run: `sudo service ssh restart`

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
Run: `sudo -u postgres createusr -P catalog` <br />
Run: `sudo -u postgres createdb -O catalog catalog`

#### Install git
Run: `sudo apt-get install git`

#### Clone Item Catalog Project
Run: `sudo mkdir /var/www/itemCatalog` <br />
Run: `sudo git clone https://github.com/KohlMeister/Udacity_Drink_Catalog`

#### Changes make to ensure app functions correctly

##### Install Flask and Associated Libraries
Run: `sudo mv catalog_website.py __init__.py` <br />
Run: `sudo apt-get install python-pip` <br />
Run: `sudo pip install virtualenv` <br />
Run: `sudo virtualenv venv` <br />
Run: `source venv/bin/activate` <br />
Run: `sudo pip install Flask` <br />
Run: `sudo pip install httplib2` <br />
Run: `sudo pip install oauth2client` <br />
Run: `sudo pip install sqlalchemy` <br />
Run: `sudo pip install psycopg2` <br />
Run: `sudo pip install passlib` <br />
Run: `sudo pip install requests`

##### Configure and enable new virtual host


### Third Party Resources

* [Deploy Flask App with Ubuntu - Digital Ocean](https://www.digitalocean.com/community/tutorials/how-to-deploy-a-flask-application-on-an-ubuntu-vps)
