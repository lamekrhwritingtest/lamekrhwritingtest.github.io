---
# Feel free to add content and custom Front Matter to this file.
# To modify the layout, see https://jekyllrb.com/docs/themes/#overriding-theme-defaults

layout: quickstart
title: Getting Started with ownCloud
---
ownCloud is an open-source file sharing platform. You host ownCloud on your own private server or private cloud, giving you full control of your data. ownCloud allows you to sync and store your data, and access it from all of your devices.

In this quickstart we walk through setting up ownCloud Community Edition or Ubuntu 18.04, then we create a few users, and last we cover the steps to connect to your ownCloud server.

# Prerequisites
While ownCloud can be installed and run on a number of different operating systems, this quickstart specifically uses Ubuntu 18.04. If you're using a different operating system, use this quickstart for general guidance, or as a means to get a server up and running so you can explore the user interface and functionality.

To complete the steps in this quickstart you will need to have the following:
- A user with sudo privileges on your server.
- A standard LAMP stack.

Once you have completed the prerequisites, read on to get started installing ownCloud.

# Install ownCloud
Installing ownCloud
To install ownCloud on Ubuntu 18.04 we will use the `apt` package manager. 

First, add the ownCloud repository key to `apt`.
```bash
wget -nv https://download.owncloud.org/download/repositories/10.0/Ubuntu_18.04/Release.key -O Release.key
apt-key add - < Release.key
```
>If you experience difficulty with any of the commands referenced in this step, check the [ownCloud download page](http://download.owncloud.org/download/repositories/10.0/owncloud/) for the most up to date information.

Next, run the following shell commands as root. This adds the repository, then installs ownCloud.
```bash
echo 'deb http://download.owncloud.org/download/repositories/10.0/Ubuntu_18.04/ /' > /etc/apt/sources.list.d/owncloud.list
apt-get update
apt-get install owncloud-files
```

Our ownCloud files installed to `/var/www/owncloud`. Depending on our web server configuration, we may need to adjust the document root to point to this directory. Navigate to `/etc/apache2/sites-enabled/` and open your `.conf` file. Inside this file we will make two changes.

First, change the `DocumentRoot` directive to point to `/var/www/owncloud`.
```
<VirtualHost *:80>

    ...

    DocumentRoot /var/www/owncloud

    ...

</VirtualHost>
```

Second, change the default port from `80` to `8080` in the VirtualHost directive.
`<VirtualHost *:8080>`

Next, open your `/etc/apache2/ports.conf` and change the `Listen 8080`.

Last, reload Apache to activate these changes by executing the following command.
`sudo systemctl reload apache2`

This completes the ownCloud installation.

# Configure the MySQL Database
asdf

# Configure ownCloud
asdf

# Add a user account
- log in to the web UI as an admin
- click hamburger menu, select users
- fill in the user info (note about using a new, non-admin group.)
- reset password (This is what I need to double check. With the current default workflow, I don't know where to set the pass, and if it is set, I don't know what it is set to.)

# Connect with a user account
- number of options, we show using the Mac OSX client
- open desktop client
- enter server address (what if I already entered a server, and I want to add another or change?)
- enter username and pass, then click conect

# Conclusion
Gets you up and running

