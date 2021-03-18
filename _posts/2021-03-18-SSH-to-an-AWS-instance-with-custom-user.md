---
layout: post
title: SSH to an AWS instance with custom added user on Ubuntu 18
---

## Add a new user

First of all create a user called joe under Ubuntu group.

`sudo adduser deployer --ingroup ubuntu`

Add a password

## Switch the terminal session

Switch the terminal session with the new user account

`su - deployer`

Type the password

We'll get a path like: `deployer@ip-X-X-X-X:~/.ssh$` with X.X.X.X is default by AWS

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