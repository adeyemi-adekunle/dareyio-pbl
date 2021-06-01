##  MY WEB STACK IMPLEMENTATION (LAMP STACK) IN AWS
### Step 1 Installing Apache Web Server 
#### 1) Install apache using Ubuntu's package manage "apt"
##### update a list of packages in package manager by run command below: 
    $ sudo apt update
   
   ![apt update package update](https://user-images.githubusercontent.com/19293380/120109683-5c094800-c162-11eb-9267-9502846c7c6e.jpg)
#####  run apache2 package installation by run command below:
    $ sudo apt install apaches 
   
   ![installing apache2](https://user-images.githubusercontent.com/19293380/120109710-7e02ca80-c162-11eb-936b-e7fd08e59e8c.jpg)

#### 2) I need to verify that apache2 is running as a service in my OS by run the command below:
    $ sudo systemctl status apache2

![checking apache2 status if running](https://user-images.githubusercontent.com/19293380/120109925-6bd55c00-c163-11eb-8f56-11cbe3bfffba.jpg)
#### 3)  I need to add a rule to EC2 configuration to open inbound connection through port 80:

![Open HTTP inbound port 80](https://user-images.githubusercontent.com/19293380/120109959-96bfb000-c163-11eb-8df4-e3cc06c701a2.jpg)

#### 4) Now my server is runing, I need to check how we can access it locally in our Ubuntu terminal, by run below command:
    $ curl http://localhost:80
    
   or 
   
    $ curl http://127.0.0.1:80

   ![accessing the apache2 web in terminal](https://user-images.githubusercontent.com/19293380/120110217-80662400-c164-11eb-8d8b-1898e8803ac5.jpg)
#### 5) To test how our Apache HTTP server respond to requests from the Internet
#####   I open a web browser and I access following url or Ip In this case my public IP from AWS is                3.134.252.92
    http://3.134.252.92:80
    
![apache web from the Internet](https://user-images.githubusercontent.com/19293380/120110580-e69f7680-c165-11eb-84a6-b468faa1fa51.jpg)
###  Step 2  Installing MySQL
#####  I need to install a Database Management System (DBMS) to be able to store and manage data for your site in a relational database.
#### 1) Install MySQL using Ubuntu's package manage "apt" by run the below command
    $ sudo apt install mysql-server
    
![Installing mysql server](https://user-images.githubusercontent.com/19293380/120110773-e2278d80-c166-11eb-8dbc-596d76ce783c.jpg)
#####  When prompted,  I confirm installation by typing Y, and then ENTER
#### 2) It’s recommended to run a security script that comes pre-installed with MySQL. This script will remove some insecure default settings and lock down access to your database system. Starting the interactive script by running below command:  
    $ sudo mysql_secure_installation
 ![mysql secure installation](https://user-images.githubusercontent.com/19293380/120111047-31ba8900-c168-11eb-9707-6b4a1e73610a.jpg)
 ##### This ask if I want to configure the VALIDATE PASSWORD PLUGIN
 ##### I select Yes or Y and I was shown the below level of password Validation
 
 ![password validation policy](https://user-images.githubusercontent.com/19293380/120111092-721a0700-c168-11eb-952b-c1dcb875683c.jpg)
Note: Keep in mind if I enter 2 for the strongest level, I  will receive errors when attempting to # set any password which does not contain numbers, upper and lowercase letters, and special characters, # or which is based on common dictionary words.

##### I select 1 and input my password and i was showned the password strength and ask if i want to continue with the password i input and i select Y or yes
##### For the rest of the questions,  i press Y and hit the ENTER key at each prompt. This will remove some anonymous users and the test database, disable remote root logins, and load these new rules so that MySQL immediately respects the changes you have made. 
#### 3) To test if i am able to log in to the MySQL console by typing below command:
    $ sudo mysql
  
 ![test mysql](https://user-images.githubusercontent.com/19293380/120111455-f1f4a100-c169-11eb-85a8-9aa804a4ddfd.jpg)
##### This will connect to the MySQL server as the administrative database user root, which is inferred    by the use of sudo when running this command
##### To exit the MySQL console, type:
    $ exit 
![exit mysql](https://user-images.githubusercontent.com/19293380/120324948-1920af00-c2df-11eb-95de-410d61a7dc73.jpg)

#### Step 3 Installing PHP 
##### In addition to the php package, i need php-mysql, a PHP module that allows PHP to communicate with MySQL-based databases. I also need libapache2-mod-php to enable Apache to handle PHP files
##### 1) In Order to instal the 3 package at once the below command will be run

     $ sudo apt install php libapache2-mod-php php-mysql 
![Installing php package 3](https://user-images.githubusercontent.com/19293380/120119547-31ce7f00-c190-11eb-97c8-2144f633bcab.jpg)
##### 2) Once the installation is finished, I need to run the following command to confirm the PHP version:
     $ php -v
![php version](https://user-images.githubusercontent.com/19293380/120119733-4d865500-c191-11eb-868e-19552f0d7dd3.jpg)

#### Step 4 Creating a Virtual Host for your Website using Apache
#####  Apache Virtual host allows me to have multiple websites located on a single machine and users of the websites will not even notice it. In this project, I am setting up a domain called projectlamp
##### 1) I Create the directory for projectlamp using ‘mkdir’ command as follows:
    $ sudo mkdir /var/www/projectlamp
    
  ![creating virtual host](https://user-images.githubusercontent.com/19293380/120330738-01e4c000-c2e5-11eb-86a1-17b03fd320a3.JPG)

##### 2) I assign ownership of the directory with the $USER environment variable, which will reference my current system user:
    $ sudo chown -R $USER:$USER /var/www/projectlamp
    
  ![sudo chown assign ownership](https://user-images.githubusercontent.com/19293380/120330928-322c5e80-c2e5-11eb-884c-63fb85d5fabc.JPG)

##### 3) I create and open a new configuration file in Apache’s sites-available directory using your preferred command-line editor. Here, we’ll be using nano running the below command
    $ sudo nano /etc/apache2/sites-available/projectlamp.conf
    
  ![open a new configuration file](https://user-images.githubusercontent.com/19293380/120331592-d7473700-c2e5-11eb-8e7f-8a8129f02b27.JPG)

##### 4) The command will create a new blank file. Paste in the following bare-bones configuration by hitting on i on the keyboard to enter the insert mode, and paste the text:
        <VirtualHost *:80>
    ServerName projectlamp
    ServerAlias www.projectlamp 
    ServerAdmin webmaster@localhost
    DocumentRoot /var/www/projectlamp
    ErrorLog ${APACHE_LOG_DIR}/error.log
    CustomLog ${APACHE_LOG_DIR}/access.log combined
    </VirtualHost>  
 
![new configuation file](https://user-images.githubusercontent.com/19293380/120332449-aa475400-c2e6-11eb-8c41-ce1bb3243c85.JPG)

Note: To save and close the file, simply follow the steps below:

*Press CTRL + O to save change made, then press Enter 

*Press CTRL + X to exit

##### 5) I use the ls command  to show the new file in the sites-available directory
    $ sudo ls /etc/apache2/sites-available
    
![showing configuration file on site-available](https://user-images.githubusercontent.com/19293380/120333161-52f5b380-c2e7-11eb-833c-e75846ff41b7.jpg)

Note: With this VirtualHost configuration, we’re telling Apache to serve projectlamp using /var/www/projectlampl as its web root directory

##### 5) I  use a2ensite command to enable the new virtual host:
    $ sudo a2ensite projectlamp
    
 ![enabled  virtual host](https://user-images.githubusercontent.com/19293380/120333598-c26ba300-c2e7-11eb-8748-20ed263542c0.jpg)

##### 6) Before, I reload the Apache, I need  to disable the default website that comes installed with Apache and to disable Apache’s default website I use a2dissite command , type:
    $ sudo a2dissite 000-default
    
![disabled default virtual host](https://user-images.githubusercontent.com/19293380/120334017-2c844800-c2e8-11eb-90e0-b92df4a5f569.jpg)

##### 7) To make sure your configuration file doesn’t contain syntax errors, run:
    $ sudo apache2ctl configtest
    
  ![to make sure apache no error](https://user-images.githubusercontent.com/19293380/120334402-8127c300-c2e8-11eb-8e13-7acb9c57f9c0.JPG)
  
##### 8) Finally, reload Apache so these changes take effect:
    $ sudo systemctl reload apache2
    
![apache2 reload](https://user-images.githubusercontent.com/19293380/120334883-f0051c00-c2e8-11eb-8a6b-ae60f8c27e2f.JPG)

##### 9) My new website is now active, but the web root /var/www/projectlamp is still empty. I need to create an index.html file in that location so that I can test that the virtual host works as expected:
    sudo echo 'Hello LAMP from hostname' $(curl -s http://169.254.169.254/latest/meta-data/public-hostname) 'with public IP' $(curl -s http://169.254.169.254/latest/meta-data/public-ipv4) > /var/www/projectlamp/index.html
    
![create an index html file](https://user-images.githubusercontent.com/19293380/120335228-3a869880-c2e9-11eb-8a01-6bcecd2c7c80.jpg)

##### 10) Now  i need go to my browser and try to open my website URL using  the below IP address in this case or reload the previous open browser:
    http://18.216.235.61:80
![curely website](https://user-images.githubusercontent.com/19293380/120336333-25f6d000-c2ea-11eb-9dd7-2e4d56f3ecf2.JPG)

Note: As you see the text from ‘echo’ command I wrote to index.html file appear on the browser, then it means my Apache virtual host is working as expected.

#### Step 5 Enable PHP on the website
Note: With the default DirectoryIndex settings on Apache, a file named index.html will always take precedence over an index.php file. This is useful for setting up maintenance pages in PHP applications, by creating a temporary index.html file containing an informative message to visitors. Because this page will take precedence over the index.php page, it will then become the landing page for the application. Once maintenance is over, the index.html is renamed or removed from the document root, bringing back the regular application page.

##### 1) In  the case I want to change this behavior, I need to edit the /etc/apache2/mods-enabled/dir.conf file and change the order in which the index.php file is listed within the DirectoryIndex directive:
    sudo nano /etc/apache2/mods-enabled/dir.conf
  ![changing precedence order](https://user-images.githubusercontent.com/19293380/120337511-4a9f7780-c2eb-11eb-9e08-e1095b0ffa8c.jpg)
  
##### 2) After saving and closing the file, you will need to reload Apache so the changes take effect:
    $ sudo systemctl reload apache2
  ![reload apache2](https://user-images.githubusercontent.com/19293380/120337961-aec23b80-c2eb-11eb-8dc2-bcb004739185.JPG)
  
##### 3) Finally, I will create a PHP script to test that PHP is correctly installed and configured on my server
  I need  to create a new file named index.php inside your custom web root folder:
  
    $ nano /var/www/projectlamp/index.php
This will open a blank file. Add the following text, which is valid PHP code, inside the file:

          <?php
       phpinfo();
       
![php script](https://user-images.githubusercontent.com/19293380/120338530-390a9f80-c2ec-11eb-93eb-48a7905c8827.JPG)

When  finished,  I save and close the file, refresh the page and you will see a page similar to this

![php land page](https://user-images.githubusercontent.com/19293380/120339380-fac1b000-c2ec-11eb-9989-2ce20a5611e1.jpg)

This page provides information about my server from the perspective of PHP. It is useful for debugging and to ensure that my settings are being applied correctly.

As I  can see this page in my  browser, then my PHP installation is working as expected.

Note: It’s best to remove the file I created as it contains sensitive information about my PHP environment  and my Ubuntu server. 
To do that i run the below command

    $ sudo rm /var/www/projectlamp/index.php
   
   
   ** THE END **

