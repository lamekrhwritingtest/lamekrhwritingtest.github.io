---
# Feel free to add content and custom Front Matter to this file.
# To modify the layout, see https://jekyllrb.com/docs/themes/#overriding-theme-defaults

layout: quickstart
title: Getting Started with ownCloud
---
ownCloud is an open-source file sharing platform. You host ownCloud on your own private server or private cloud, giving you full control of your data. ownCloud allows you to sync and store your data, and access it from all of your devices.

In this quickstart we walk through setting up ownCloud Community Edition on Ubuntu 18.04, then we create a new user, and last we cover the steps to connect to your ownCloud server.

# Prerequisites
While ownCloud can be installed and run on a number of different operating systems, this quickstart specifically uses Ubuntu 18.04. If you are using a different operating system, use this quickstart for general guidance, or as a means to get a server up and running so you can explore the user interface and functionality.

To complete the steps in this quickstart you will need to have the following:
- An Ubuntu 18.04 server with a standard LAMP stack.
- A user with sudo privileges on your server.

Once you have completed these prerequisites, read on to get started installing ownCloud.

>If you need help with either of these steps, there are [a number of resouces on the internet](https://www.digitalocean.com/community/tutorials/initial-server-setup-with-ubuntu-18-04) that can help guide you.

# Install ownCloud
To install ownCloud on Ubuntu 18.04 we will use the `apt` package manager. 

First, add the ownCloud repository key to `apt`.
```bash
wget -nv https://download.owncloud.org/download/repositories/10.0/Ubuntu_18.04/Release.key -O Release.key
apt-key add - < Release.key
```
>If you experience difficulty with any of the commands referenced in this section, check the [ownCloud download page](http://download.owncloud.org/download/repositories/10.0/owncloud/) for the most up to date information.

Next, run the following shell commands as root. This adds the repository, then installs ownCloud.
```bash
echo 'deb http://download.owncloud.org/download/repositories/10.0/Ubuntu_18.04/ /' > /etc/apt/sources.list.d/owncloud.list
apt-get update
apt-get install owncloud-files
```

Our ownCloud files installed to `/var/www/owncloud`. Depending on our web server configuration, you may need to adjust the document root to point to this directory. Navigate to `/etc/apache2/sites-enabled/` and open your `.conf` file.
> You might have more than one `.conf` file. In this case you can run the following command to show your parsed vhost settings, and pipe the output to grep to search for your server's domain or IP. The output will help you locate the correct `.conf` file (or files) to modify.
>This is most likely the case only if you are using an existing Apache setup, or a server that is for shared hosting.
>In the following command, replace `server_domain_or_IP` with your server's domain or IP.
>```sudo apache2ctl -t -D DUMP_VHOSTS | grep server_domain_or_IP```

Inside your `.conf` file we will make two changes.

First, change the `DocumentRoot` directive to point to `/var/www/owncloud`. For example, your updated file will look like this: 
```
<VirtualHost *:80>

    ...

    DocumentRoot /var/www/owncloud

    ...

</VirtualHost>
```

Second, change the default port from `80` to `8080` in the VirtualHost directive. Your updated VirtualHost directive will look like this:
```
<VirtualHost *:8080>
```

Next, open your `/etc/apache2/ports.conf` file and change the Listen directive to listen on port 8080. We are making this change to avoid any arbitrary restrictions our ISP may impose on the default port 80. Your updated Listen directive will look like this:
```
Listen 8080
```

Last, reload Apache to activate these changes by executing the following command.
```bash
sudo systemctl reload apache2
```

This completes the ownCloud installation.

# Configure a MySQL Database
Next we will set up a MySQL database with the information we need to provide when configuring our new ownCloud instance.

Start by creating a new database. You can name this database anything you would like. In our example, we name our database `owncloud`.
```sql
CREATE DATABASE owncloud;
```

Next, create a new MySQL user account to manage the `owncloud` database you just created. As with the database, we name our new user `owncloud`. 
> Be sure to replace `new_user_password` with an actual password in the command below.

```sql
GRANT ALL ON owncloud.* to 'owncloud'@'localhost' IDENTIFIED BY 'new_user_password';
```

Last, activte your changes.
```sql
FLUSH PRIVILEGES;
```

Now your database is setup and you are ready to configure your ownCloud instance.

# Configure ownCloud
When you first install ownCloud you need to complete some initial configuration steps.

First, navigate to your server from a browser.
> Be sure to replace `server_domain_or_IP` with your actual server domain or IP. Note that we have included `:8080` to reflect the changes we made to our Apache server to listen on port 8080.

```
https://server_domain_or_IP:8080
```

![Adding database information](/assets/owncloudqs-configure-loginpage.png)

Create your admin user by entering a username and a password.

![Adding an admin username and password](/assets/owncloudqs-configure-username.png)

Leave the **Data folder** field set to `/var/www/owncloud/data`.

![Leave the data folder setting as is](/assets/owncloudqs-configure-datafolder.png)

Enter the details of the MySQL database we configured in the previous section. Use the database name, and the database user and password you created. Leave the database host as `localhost`.

![Adding database information](/assets/owncloudqs-configure-databaseinfo.png)

Click the **Finish setup** button to complete your configuration.

# Add a user account
Now that our ownCloud server is configured, the next step is to create a user.

Navigate to your server in a browser, and log in as an admin.

Click on your username in the top right corner, and from the dropdown select **Users**.

![Navigate to the users tab](/assets/owncloudqs-usercreate-userstab.png)

Enter a username and user email, then click **Create**.

![Enter a new username and password](/assets/owncloudqs-usercreate-newuserinfo.png)

A new user is generated. Click into the *Password* field for your new user, and update the password.

![Enter a new username and password](/assets/owncloudqs-usercreate-updatepassword.png)

Now your new user is ready to connect and share files on your ownCloud server. 


# Connect with a user account
ownCloud provides a number of clients to connect to ownCloud servers. In this example we will connect to our new ownCloud server using the MacOS desktop client.

Download and install the client from [ownCloud's download page](https://owncloud.org/download/).

Open the desktop client and enter your server domain or IP.

![Enter your server address](/assets/owncloudqs-userconnect-serveraddress.png)

On the next page enter the new username and password you created.

![Enter your username and password](/assets/owncloudqs-userconnect-userlogin.png)

On the last page of the wizard you can select your folder syncing options. For this tutorial we will leave the default settings and click **Connect**.

![Select your folder syncing options](/assets/owncloudqs-userconnect-foldersyncsettings.png)

After connecting, the ownCloud client displays all of the servers you are connected to. You can view the status of your connections, edit the specific folders that are syncing, and create new connections to other ownCloud servers.

![View your connected servers](/assets/owncloudqs-userconnect-connectedservers.png)

Test out your server by creating a new test file on your desktop. Be sure to create the file in the folder you are syncing to your ownCloud server.

After creating the file, log into your server from your browser and view the file appear on the **File** tab. 

![Test syncing a file](/assets/owncloudqs-userconnect-testfile.png)

# Conclusion
This tutorial walked you through setting up an ownCloud instance, creating users, and connecting. From here you should feel comfortable with the basics of ownCloud, and be ready to set up your own instance to manage your data.

Check out [ownCloud's documentation](https://owncloud.org/community/documentation/) for more information.