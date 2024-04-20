---
layout: post
title: Install Mysql - Nginx - PHP8 on Ubuntu18
---

## Mysql - Nginx - PHP8

First of all log in to your EC2 instance and create a user called `deployer`under Ubuntu group.

`sudo apt-get install mysql-server -y`

`sudo mysql_secure_installation`

Use sudo mysql to login as root user

`sudo apt-get install software-properties-common -y`

`sudo add-apt-repository ppa:ondrej/php`

`sudo apt-get update -y`

`sudo apt-get install -y php8.0`

`sudo apt install php8.0-fpm php-mysql php8.0-xml php8.0-curl php8.0-gd -y`

`sudo chown -R www-data:www-data /var/www/html`

## Install LetsEncrypt

1. Install SNAPD

   `$ sudo apt update`

   `$ sudo apt install snapd`

2. Ensure that our version of snapd is up to date:

   `$ sudo snap install core; sudo snap refresh core`

3. Remove certbot-auto and any Certbot package:

4. Install Certbot: `$ sudo snap install --classic certbot`

5. Prepare the Certbot command: `sudo ln -s /snap/bin/certbot /usr/bin/certbot`

6. Run Certbot to install certificate: `sudo certbot --nginx`

7. Test automatic renewal:  `sudo certbot renew --dry-run`

8. Done

## Create .ssh directory

Create a directory named .ssh in the home folder:


`deployer@ip-X-X-X-X:~$ mkdir .ssh`

## Give permission

Give permission to the .ssh folder

`deployer@ip-X-X-X-X:~$ chmod 700 .ssh`

## Create authorized_keys file

Create authorized_keys file inside .ssh directory

`deployer@ip-X-X-X-X:~$ cd .ssh && touch authorized_keys`

## Add user’s public key

Add the public key id_rsa.pub to the authorized_keys file

`deployer@ip-X-X-X-X:~/.ssh$ vi authorized_keys`

id_rsa.pub can be found here in windows:

`C:\Users\[your-user-name]\.ssh`

and the format will be like `ssh-rsa xxxxxx-very-long-string-here`

![_config.yml]({{ site.baseurl }}/images/ssh_rsa_location_win.png)