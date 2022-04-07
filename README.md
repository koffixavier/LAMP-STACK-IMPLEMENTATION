# LAMP-STACK-IMPLEMENTATION
This project will help you install Apache web server, mysql and php which you can use to host a static website or deploy a dynamic PHP application that reads and writes information to a database 
## Step 1: Launch a new instance using Amazon linux (Ubuntu Server 20.04)
- Make sure that you change your security group to allow HTTP (port 80)


https://user-images.githubusercontent.com/101080172/161681675-fe25fcb3-7401-4a4b-97ce-97c82b85319e.mov

## Step 2: Connect to the AWS instance
- connect to the instance throught your terminal using the ssh command example found in the SSH Client Tab.
  - In your terminal, change directory into the location where your PEM file is 
   `cd downloads`
  - connect to the instance by running
   ` ssh -i "<private-key-name>.pem" ubuntu@<Public-IP-address>`
## Step 3: Update packages and install apache server 
- perform software updates to ensure that all of your software packages are up to date
 `sudo apt upgrade`
- install and run apache2 package installation
 `sudo apt install apache2`
- then curl into your server 
 `curl http://localhost:80`
## Step 4: install MySQL to store and manage data for your site in a relational database  
- install mysql
  `sudo apt install mysql-server`
- remove some insecure default settings and lock down access to your database system
   `sudo mysql_secure_installation`
- log in to the MySQL console
   `sudo mysql`
- Then exit the MySQL console
    `sudo mysl>exit'
## Step 5: install PHP to process code and display dynamic content to the end user
- install php 
    `sudo apt install php libapache2-mod-php php-mysql`
## Step 6: Create a virtual host for your website using apache
- create the directory for projectlamp 
   `sudo mkdir /var/www/projectlamp`
- assign ownership of the directory with your current system user
   `sudo chown -R $USER:$USER /var/www/projectlamp`
- create and open a new configuration file in Apache’s sites-available directory
   `sudo vi /etc/apache2/sites-available/projectlamp.conf`
- Paste in the following bare-bones configuration by hitting on i on the keyboard to enter the insert mode, and paste the following text
`<VirtualHost *:80>
    ServerName projectlamp
    ServerAlias www.projectlamp 
    ServerAdmin webmaster@localhost
    DocumentRoot /var/www/projectlamp
    ErrorLog ${APACHE_LOG_DIR}/error.log
    CustomLog ${APACHE_LOG_DIR}/access.log combined
</VirtualHost>`
- to show the new file in the sites-available directory
   `sudo ls /etc/apache2/sites-available`
- use a2ensite command to enable the new virtual host:
   `sudo a2ensite projectlamp`
- disable the default website that comes installed with Apache
    `sudo a2dissite 000-default`
- make sure your configuration file doesn’t contain syntax errors
   `sudo apache2ctl configtest`
- reload Apache so these changes take effect
    `sudo systemctl reload apache2`
- Create an index.html file in that location so that we can test that the virtual host works as expected
   `sudo echo 'Hello LAMP from hostname' $(curl -s http://169.254.169.254/latest/meta-data/public-hostname) 'with public IP' $(curl -s http://169.254.169.254/latest/meta-data/public-ipv4) > /var/www/projectlamp/index.html`
- try to open your website URL using your IP address
  - It should look like this. That is suppose to be static website
  ![Screen Shot 2022-04-07 at 12 46 25 AM](https://user-images.githubusercontent.com/101080172/162228337-8f8795dd-fbb8-433b-aaed-a40d1857d135.png)
## Step 7: Enable PHP on the Website
Let transform the static to a dynamic website 
- use the following commands to edit the /etc/apache2/mods-enabled/dir.conf file
    `sudo vim /etc/apache2/mods-enabled/dir.conf`
  - then change change `DirectoryIndex index.html index.cgi index.pl index.php index.xhtml index.htm` into `DirectoryIndex index.php index.html index.cgi index.pl index.xhtml index.htm`
- Reload apche so the changes take effect
   `sudo systemctl reload apache2`
- create a PHP script to test that PHP is correctly installed and configured on your server
   22  vim /var/www/projectlamp/index.php
- create a new file named index.php inside your custom web root folder
   `vim /var/www/projectlamp/index.php`
- add
  `<?php
phpinfo();`
- You should get this 

![Screen Shot 2022-04-07 at 12 51 45 AM](https://user-images.githubusercontent.com/101080172/162249074-0e56fe70-d674-4e86-b3cd-780b6d671704.png)

## History of my commands
  
    2  exit
    3  cd downloads`
    4  sudo apt install apache2
    5  curl http://localhost:80
    6  sudo apt install mysql-server
    7  sudo mysql
    8  sudo install php libapache2-mod-php php-mysql
    9  sudo apt install php libapache2-mod-php php-mysql
   
   10  `php -v`
   11  `sudo mkdir /var/www/projectlamp`
   12  `sudo chown -R $USER:$USER /var/www/projectlamp`
   13  `sudo vi /etc/apache2/sites-available/projectlamp.conf`
   14  `sudo ls /etc/apache2/sites-available`
   15  `sudo a2ensite projectlamp`
   16  `sudo a2dissite 000-default`
   17  `sudo apache2ctl configtest`
   18  `sudo systemctl reload apache2`
   19  `sudo echo 'Hello LAMP from hostname' $(curl -s http://169.254.169.254/latest/meta-data/public-hostname) 'with public IP' $(curl -s http://169.254.169.254/latest/meta-data/public-ipv4) > /var/www/projectlamp/index.html`
   20  `sudo vim /etc/apache2/mods-enabled/dir.conf`
   21  `sudo systemctl reload apache2`

   23  `sudo vim /etc/apache2/mods-enabled/dir.conf`
   24  `sudo systemctl reload apache2`
   25  `vim /var/www/projectlamp/index.php`
   26  `sudo rm /var/www/projectlamp/index.php`
   
