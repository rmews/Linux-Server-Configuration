# Linux-Server-Configuration

## Server Info
Address: http://18.218.75.238/

## Server Configuration Steps
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

Then you will want to move that file to your .ssh folder.

`mv name-of-the-key-downloaded ~/.ssh`

Finally, change the permissions of the key file. This step is important, otherwise you will recieve an error upon trying to login saying permissions are too open.

`chmod 600 name-of-the-key-downloaded`

### Step 6: Login to Server via SSH
Login to using one simple command

`ssh ubuntu@ip address -p 22 -i ~/.ssh/name-of-the-key-downloaded`

### Step 7: Update all packages
`sudo apt-get update` 

and then install the updates

`sudo apt-get upgrade`

autoremove any unnessary packages

`sudo apt autoremove`

### Step 8: Configure Firewall & Ports
To ensure security of your server, you will want to only allow communication into the ports that are nessassary. 




## Additional Resources
