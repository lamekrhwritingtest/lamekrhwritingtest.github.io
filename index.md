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

First, change the `DocumentRoot` directive to point to `/var/www/owncloud`. For example, your updated file will look like this: 
```
<VirtualHost *:80>

    ...

    DocumentRoot /var/www/owncloud

    ...

</VirtualHost>
```

Second, change the default port from `80` to `8080` in the VirtualHost directive. Your updated file will look like this:
```
<VirtualHost *:8080>
```

Next, open your `/etc/apache2/ports.conf` and change the Listen directove to listen on port 8080. We're making this change to avoid any arbitrary restrictions our ISP may impose on the default port 80. Your updated file will look like this:
````
Listen 8080
```

Last, reload Apache to activate these changes by executing the following command.
```bash
sudo systemctl reload apache2
```

This completes the ownCloud installation.

# Configure the MySQL Database
Next we will setup a MySQL database with the information we need to provide when configuring our new ownCloud instance.

Start by creating a new database. You can name this database anything you'd like. In our example, we are naming our database `owncloud`.
```sql
CREATE DATABASE owncloud;
```

Next, create a new MySQL user account to manage the ownCloud database. As with the database, we named our new user `owncloud`. 
> Be sure to replace `new_user_password` with an actual password in the command below.

```sql
GRANT ALL ON owncloud.* to 'owncloud'@'localhost' IDENTIFIED BY 'new_user_password';
```

Last, activte your changes.
```sql
FLUSH PRIVILEGES;
```

Now your database is setup and you're ready to configure your ownCloud instance.

# Configure ownCloud
When you first install ownCloud you need to take some initial configuration steps.

First, navigate to your server from your browser.
> Be sure to replace `server_domain_or_IP` with your actual server domain or IP. Note that we've included `:8080` to reflect the changes we made to our Apache server to listen on port 8080.

```
https://server_domain_or_IP:8080
```

Create your admin user by entering a username and a password.
![Adding an admin username and password](/assets/owncloudqs-configure-username.png)

Leave the **Data folder** field set to `/var/www/owncloud/data`.

Enter the details of the MySQL database we configured in the previous section. Use the database name and username you created. Leave the database host as `localhost`.
img

Fill out the details of the database name, database username, and database password you created in the previous section. If you used the settings from this guide, both the database name and username will be owncloud. Leave the database host as localhost.
img

Click the **Finish setup** button to complete your configuration.

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

