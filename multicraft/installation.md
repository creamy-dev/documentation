# How to install Multicraft
# Table of Contents
- [How to install Multicraft](#how-to-install-multicraft)
- [Table of Contents](#table-of-contents)
- [Dependencies](#dependencies)
  - [Java](#java)
  - [MySQL](#mysql)
  - [Apache](#apache)
  - [PHP](#php)
- [Configuration](#configuration)
  - [Services](#services)
  - [MySQL](#mysql-1)
  - [Apache](#apache-1)
  - [Multicraft](#multicraft)
    - [Backend](#backend)
    - [Frontend](#frontend)
# Dependencies
First, connect via SSH for this guide to save hassle.  
## Java
If using Minecraft 1.17, install Java 16.
```bash
sudo apt install openjdk-16-jre -y
```
Else if you are using Minecraft 1.18, install Java 18.
```bash
sudo apt install openjdk-18-jre -y
```
Else, install Java 8.
```bash
sudo apt install openjdk-8-jre -y
```
## MySQL
Add the MySQL repositories:
```bash
curl https://repo.mysql.com/mysql-apt-config_0.8.20-1_all.deb > mysql-apt-config_0.8.20-1_all.deb
sudo dpkg -i mysql-apt-config_0.8.20-1_all.deb
```
Select MySQL server and cluster, and select mysql-8.0.  
It will kick you back, so scroll down and click `Ok`.  
Then, update your package lists:
```bash
sudo apt update
```
Then, install the following packages:
```bash
sudo apt install mysql-community-server mysql-community-client -y
```
Enter a password that you will renember for later.
## Apache
Install the following packages:
```bash
sudo apt install apache2 -y
```
## PHP
Install the following packages:
```bash
sudo apt install libapache2-mod-php php php-mysql -y
```
# Configuration
## Services
Enable the following services:
```bash
sudo systemctl enable apache2
sudo systemctl enable mysql
```
## MySQL
Now, we need to configure MySQL.
First, we need to securly finish the installation procedure.
```bash
sudo mysql_secure_installation
```
Then, we need to enter the same password.  
I recommend turning off validating passwords, because password security can be annoying, and you are the only person that has access to the database. (hopefully)  
Enter `n` for the first two. Then, enter `y`. Enter `n`. Enter `y` again. Finally, enter `y` one last time.  
Connect to the database:
```bash
mysql -u root -p
```
Then, create a new user named `multicraft` with a password of your choice.
```sql
CREATE USER 'multicraft'@'localhost' IDENTIFIED BY 'password';
```
Finally, we need to create the multicraft databases, and give the new user permissions.
```sql
CREATE DATABASE multicraft_panel;
GRANT ALL PRIVILEGES ON multicraft_panel.* TO 'multicraft'@'localhost';
CREATE DATABASE multicraft_daemon;
GRANT ALL PRIVILEGES ON multicraft_daemon.* TO 'multicraft'@'localhost';
```
Make sure you can still connect to the database as root:
```bash
mysql -u root -p
```
If you can't, change the password of the root user, to the same password you used before.
```sql
ALTER USER 'root'@'localhost' IDENTIFIED BY 'password';
```
Then, exit the database.
```sql
exit;
```
## Apache
Now, we need to configure Apache.
First, we need to stop the Apache service.
```bash
sudo systemctl stop apache2
```
Then, we need to edit the `/etc/apache2/apache2.conf` file.
```bash
sudo nano /etc/apache2/apache2.conf
```
Then, we need to scroll down to the `<Directory /var/www/>` line, and change `AllowOverride None` to `AllowOverride All`.
```text
<Directory /var/www/>
    Options Indexes FollowSymLinks
    AllowOverride All
    Require all granted
</Directory>
```
Then, save and exit nano. 
```text
CTRL+O, Enter, CTRL+X
```
Then, restart the Apache service.
```bash
sudo systemctl restart apache2
```
## Multicraft
### Backend
Now, we need to configure Multicraft.
First, download multicraft.
```bash
curl http://multicraft.org/files/multicraft-2.4.1-64.tar.gz > multicraft.tar.gz
```
Then, extract the archive.
```bash
tar -xvzf multicraft.tar.gz
```
Run setup as root:
```bash
cd multicraft 
sudo ./setup.sh
```
First, press enter until you get to the part that says `IP the FTP server will listen on (0.0.0.0 for all IPs):`.  
For that part, enter `0.0.0.0` twice.  
Press enter until you get to the part that says `What kind of database do you want to use?`.  
Enter `mysql`. Press enter twice. Enter `multicraft`. Enter the password for the `multicraft` user.  
Press enter for the rest of the times.  
### Frontend
Go to `http://ip/multicraft`.  
Follow the prompts until you get to the database part. Select `MySQL`. Enter `multicraft` for the username. Enter the user password for the password.  
Follow the prompts, and repeat the process for the other database.  
Update the config `/home/minecraft/multicraft/multicraft.conf` with the data on screen.  
Finally, delete the install.php file when it tells you to.
```bash
sudo rm -rf /var/www/html/multicraft/install.php
```