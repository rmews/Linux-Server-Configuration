# Linux-Server-Configuration

## Server Info
Address: http://18.218.75.238/

## Configuration Steps
### Step 1: Signup for an Amazon Web Services account [here](https://lightsail.aws.amazon.com/).

### Step 2: Create a Ubuntu instance on AWS
Lightsail will greet and guide you through making the Ubuntu instance. For this setup, make sure to select Ubuntu and select "OS Only"

### Step 3: Choose instance plan
Select the configuration you need to support the application. For this configuraiton, I've selected the lowest tier, which allows you to cancel within 30 days before incurring any charges.

### Step 4: Create an instance name
Any name will do. Only requirement is that the name has no spaces. 

### Step 5: Download SSH Key 
Before you begin to configure the server, you'll want to download an SSH key from Amazon so you can connect to the server via SSH. To do this, just head to your AWS Account and download the key. 

If you are on OSX, the key will likely now be located in your Downloads folder. You will want to open your Terminal application cd into your Downloads folder.

`cd /path-to-Downloads-folder`

Then move that file to your .ssh folder.

`mv name-of-the-key-downloaded ~/.ssh`

Finally, change the permissions of the key file.

`chmod 600 name-of-the-key-downloaded`

### Step 6: Login to Server via SSH
Login to using one simple command

`ssh ubuntu@ip address -p 22 -i ~/.ssh/name-of-the-key-downloaded`

### Step 7: Update all packages
`sudo apt-get update` 

then install the updates

`sudo apt-get upgrade`

autoremove any unnessary packages

`sudo apt autoremove`

### Step 8: Configure ports & firewall
Ensure security of server. Configure ufw settings to allow communication in and out of server. 

1. Check status of ufw: `sudo ufw status`
2. Set defaults:
`sudo ufw default deny incoming`
`sudo ufw default allow outgoing`
3. Configure ufw to allow SSH connection over port 2200
`sudo ufw allow 2200`
4. Configure ufw to allow HTTP 
`sudo ufw allow http`
4. Configure ufw to allow UTF connection over port 123
`sudo ufw allow 123`
5. Configure SSH to communicate over port 2200
`sudo nano /etc/ssh/sshd_config`
Change the line that says Port 22 to 2200, then:
`sudo service ssh restart`
6. Enable ufw
`sudo ufw enable`

### Step 9: Add new user & give sudo permission
1. Add new user: `sudo adduser new-user-name`
2. Give new user sudo permission: `sudo usermod -aG sudo new-user-name`

### Step 10: Give new user SSH access
1. Switch to new user: `su -l new-user-name` and enter password for user
2. Make SSH directory: `mkdir .ssh`
3. Create authorized key file: `touch .ssh/authorized_keys`
4. On your local machine, create key pair: `ssh-keygen`
5. Enter file in which to save key on your local machine. This should be stored in your .ssh directory.
6. Enter password for the key
7. On your local machine, copy the string in the key file: `cat key-file.pub`
8. Back on the server, paste the key into the authorized_keys file: `nano .ssh/authorized_keys`
9. Update user permissions of the ssh folder and keys: `chmod 700 .ssh` & `chmod 644 .ssh/authorized_keys`

### Step 11: Enforce key-based authentication
1. `sudo nano /etc/ssh/sshd_config`
2. Change PasswordAuthentication to no.
3. `sudo service ssh restart`

### Step 12: Configure the local timezone to UTC
1. `sudo dpkg-reconfigure tzdata`
2. Select `None of the above`
3. Select `UTC`

### Step 13: Install webserver packages (Apache & mod_wsgi) and Flask
1. Install Apache `sudo apt-get install apache2`
2. Install mod_wsgi. This is an Apache HTTP server mod that enables Apache to serve Flask applications. `sudo apt-get install libapache2-mod-wsgi`
3. Install Flask `sudo apt-get install python-flask`

### Step 14: Configure wsgi, git and clone app to serve flask app
1. Move into web directory /var/www
2. Create new directory `sudo mkdir FlaskApp`
3. Move into newly created folder and intialize Git `sudo git init`
4. Clone repo `sudo git clone https://github.com/rmews/flask-catalog-app.git` This will create a new directory in FlaskApp called flask-catalog-app
5. Edit the config file to point to our new Flask site

### Step 15: Install application dependencies 



## Additional Resources
