# Web Stack Implementation of LAMP (Linux, Apache, MySQL, PHP)

## Introduction: 
### Technology Stack- A technology stack is a set of frameworks and tools used to develop a software product.
### LAMP stands for a technology stack tool suite with Linux running as the OS; Apache as the webserver; MySQL as the database; PHP as the server-side scripting language 

![LAMP Architecture](./images/HLD_LAMP.PNG)
*LAMP Architecture, Source: K7. India* 

### Step 0: Setting up EC2 Instance on AWS

Launched EC2 instance of Linux Ubuntu Server 20.04 LTS (HVM) and named it as pbl_p1_lamp. Created security group with relevant ports opened and also created and saved my private key to be used for SSH into the EC2 instance.

![EC2 Machine](./images/EC2_Instance.PNG)
*EC2 Instance Linux Ubuntu Server 20.04 1 CPU 8G Storage*

![Security ports](./images/Security_ports.PNG)
*Security: Opened ports*

![SSH session](./images/SSH_from_Client_to_Server.PNG)
*SSH connection from client to EC2 Instance*

### Step 1: Installing Apache and updating the firewall

` #update a list of packages in package manager`

   `sudo apt update`

` #run apache2 package installation`

  `sudo apt install apache2`

![Apache installation](./images/Installing_Apache.PNG)
![Apache Startup](./images/Starting_Apache.PNG)
![Apache installation](./images/Installing_Apache.PNG)
*Screenshot for Apache Server installation and Startup*

![Apache webpage](./images/Apache_webpage_index.PNG)
*Screenshot of Apache webpage*

### Step 2: Installing mysql
` sudo apt install mysql-server`

` sudo mysql_secure_installation`
![MySQL](./images/mysql_instal_launch.PNG)
*Screenshot of MySQL*

### Step 3:Installing php

![PHP](./images/php_install.PNG)
*Screenshot of PHP_Install*

### Step 4: Creating a virtual host for your website using apache


` #Create the directory for projectlamp`

  `sudo mkdir /var/www/projectlamp `

` #assign ownership of the directory with your current system user:` 

`  sudo chown -R $USER:$USER /var/www/projectlamp`


` #create and open a new configuration file in Apache’s sites-available directory using your preferred command-line editor.`

` sudo vi /etc/apache2/sites-available/projectlamp.conf `

`	<VirtualHost *:80>`
`   	 ServerName projectlamp`
`   	 ServerAlias www.projectlamp `
`   	 ServerAdmin webmaster@localhost`
`   	 DocumentRoot /var/www/projectlamp`
`    	 ErrorLog ${APACHE_LOG_DIR}/error.log`
`   	 CustomLog ${APACHE_LOG_DIR}/access.log combined`
`	</VirtualHost> `

` sudo ls /etc/apache2/sites-available`

`#==>>>>>000-default.conf  default-ssl.conf  projectlamp.conf`

`#a2ensite command to enable the new virtual host`

` sudo a2ensite projectlamp`

`#To disable Apache’s default website use a2dissite command`

` sudo a2dissite 000-default`

`#To make sure your configuration file doesn’t contain syntax errors`

` sudo apache2ctl configtest`

`#Finally, reload Apache so these changes take effect`

` sudo systemctl reload apache2`

`#new website is now active, but the web root /var/www/projectlamp is still empty. Create an index.html file in that location so that we can test that the virtual host works as expected:`

`sudo echo 'Hello LAMP from hostname' $(curl -s http://169.254.169.254/latest/meta-data/public-hostname) 'with public IP' $(curl -s http://169.254.169.254/latest/meta-data/public-ipv4) > /var/www/projectlamp/index.html`

`# http://52.14.112.248:80 --open in web browser`

![virtualhost](./images/virtual_host_webpage.PNG)
*Screenshot of Virtual host webpage*
