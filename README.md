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

#### Configure local timezoe

#### Install Apache and mod_wsgi

#### Install and Configure PostgreSQL

#### Install git

#### Clone Item Catalog Project

#### Changes make to ensure app functions correctly


### Third Party Resources

* [Deploy Flask App with Ubuntu - Digital Ocean](https://www.digitalocean.com/community/tutorials/how-to-deploy-a-flask-application-on-an-ubuntu-vps)
