## WEB STACK IMPLEMENTATION (LAMP STACK) IN AWS
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
 

    
    
    

