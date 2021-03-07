---
layout: post
title: Deploy a rails application on Ubuntu 18.4
---

The stack for deploying a rails app:
1. Nginx
2. Unicorn
3. Postgresql DB ` sudo apt-get install -y postgresql postgresql-contrib`
4. Nodejs + Webpack

Rails version 6.2
Ruby version 2.6.5
RBENV.

Generate SSH key: `ssh-keygen -t rsa -b 4096 -C "yourmail@example.com"`

Deploy with Capistrano.

Generate master key:

START: Login to the server via SSH with root permission. (Not best practice)

1. Create a user for deployment: `adduser deployer --ingroup sudo`

2. Add a password for deployer user and use the switch user command to login: `su - deployer`

3. Install build tool: `sudo apt-get install -y build-essential`

4. Install dependencies: `sudo apt-get install -y git-core curl zlib1g-dev libpq-dev libssl-dev libreadline-dev libyaml-dev libxml2-dev libxslt1-dev libcurl4-openssl-dev libffi-dev libpq-dev` 

   - If we need sqlite3, try to install `sudo apt-get install -y sqlite3 libsqlite3-dev`

5. Clone rbenv:

   `git clone https://github.com/rbenv/rbenv.git ~/.rbenv` 

6. Init the RBENV: `~/.rbenv/bin/rbenv init`

7. Export the PATH: `echo 'export PATH="$HOME/.rbenv/bin:$PATH"' >> ~/.bash_profile`

8. Add this line: `eval "$(rbenv init -)"` into **~/.bash_profile** 

   ​	 `vi ~/.bash_profile` 

   ​	`echo 'eval "$(rbenv init -)"' >> ~/.bash_profile`

   ​	`source ~/.bash_profile`

9. Clone Ruby Build from Github: `git clone https://github.com/rbenv/ruby-build.git ~/.rbenv/plugins/ruby-build`

10. Install Ruby: `rbenv install -v 2.6.5`

11. Set Ruby version globally: `rbenv global 2.6.5`

12. Install bundler: `gem install bundler`

13. Install Node JS: `curl -sL https://deb.nodesource.com/setup_10.x -o nodesource_setup.sh`

    1. `sudo bash nodesource_setup.sh`
    2. `sudo apt-get -y update && sudo apt-get install -y nodejs`

14. Install Yarn: `curl -sS https://dl.yarnpkg.com/debian/pubkey.gpg | sudo apt-key add -`

    1. `echo "deb https://dl.yarnpkg.com/debian/ stable main" | sudo tee /etc/apt/sources.list.d/yarn.list`
    2. `sudo apt-get -y update && sudo apt-get -y install yarn`

15. Config SSH for github to clone repository.

16. Config NGINX: remove default site, add symlink to project nginx.conf file.

    `cd /etc/nginx/sites-enabled/` & `rm default` or `rm /etc/nginx/sites-enabled/default`

    `sudo ln -s /home/deployer/[APP_NAME]/current/config/nginx.conf /etc/nginx/sites-enabled/[APP_NAME]`

17. Copy master key to server: `vi /home/deployer/[APP_NAME]/shared/config/master.key`

18. Symlink unicorn shell: `sudo ln -s /home/deployer/[APP_NAME]/current/config/unicorn_init.sh /etc/init.d/unicorn_[APP_NAME]`

19. Config **deployer** to allow unicorn shell to use sudo command, open the deployer user config.

    `sudo vi /etc/sudoers.d/deployer`

    deployer        ALL=(ALL:ALL) ALL
    deployer        ALL=NOPASSWD: /home/deployer/[APP_NAME]/current/config/unicorn_init.sh

20. Config unicorn start each time server restart: `sudo update-rc.d unicorn_[APP_NAME] defaults`

