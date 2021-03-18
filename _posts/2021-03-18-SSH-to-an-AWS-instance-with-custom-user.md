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

## Create .ssh directory

Create a directory named .ssh in the home folder:

```
$ mkdir .ssh
```

We'll get a path like: `deployer@ip-X-X-X-X:~/.ssh$` with X.X.X.X is default by AWS

## Give permission

Give permission to the .ssh folder

```
deployer@ip-X-X-X-X:~/.ssh$ chmod 700 .ssh
```

## Create authorized_keys file

Create authorized_keys file inside .ssh directory

```
$ touch authorized_keys
```

## Add user’s public key

Add the public key id_rsa.pub to the authorized_keys file

```
$ vi authorized_keys
```

id_rsa.pub can be found here in windows:

![_config.yml]({{ site.baseurl }}/images/_ssh_folder.png)