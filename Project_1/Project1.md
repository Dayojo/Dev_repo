# WEB STACK IMPLEMENTATION (LAMP STACK)

## LAMP (Linux, Apache, MySQL, PHP or Python, or Perl)
###Setting up our instance
- We require an AWS account
- Initiate the creation of a new EC2 instance from the t2.micro family, running Ubuntu Server 20.04 LTS
- Ensure that the private key (.PEM file) is saved securely before starting the instance

![0](https://user-images.githubusercontent.com/123396933/230746708-9004290c-a603-4d95-b70e-7534c0225186.PNG)

- Connecting to EC2 terminal
  - Using the terminal on MAC/Linux
  - Using Windows Terminal
  - We'll be connecting to the EC2 instance using Gitbash terminal installed in my windows system

- We will need the PEM key file that we have saved. Navigate to the download folder in the terminal

![1](https://user-images.githubusercontent.com/123396933/230747272-2918f605-de67-408f-967f-8cbdeaea2ef6.PNG)

- We need to run this command to ensure our key is not publicly viewable.

`chmod 400 <your-PEM-file-name>.pem`

![2](https://user-images.githubusercontent.com/123396933/230747436-6f268d67-e136-4414-9fd0-9d9c827f3c2f.PNG)

- I'll be utilizing the SSH protocol to establish a connection between my local terminal and the EC2 server

 `ssh -i <private-key-name>. pem ubuntu@<Public-IP-address>`

![3](https://user-images.githubusercontent.com/123396933/230747683-a8c1bb1f-b938-47ba-a4aa-91d354f7d253.PNG)

 - Type `yes` to connect
 - Now we are connected to our instance well done.
 
![3 1](https://user-images.githubusercontent.com/123396933/230747623-1a595e80-9dc8-46e5-88d3-661cd6dceef6.PNG)

We have successfully created our first Linux server in the cloud, and our current setup looks like this: (we are the client)
![5 1](https://user-images.githubusercontent.com/123396933/230748018-a579a4a1-2b5a-407e-9b21-fcef3595ae1a.PNG)

### STEP 1
#### Installing Apache and updating the firewall

Update the list of software packages in the package manager:

`sudo apt update`

Run apache2 package installation:

`sudo apt install apache2`

To confirm if apache2 is running as a service in our operating system, execute the following command.:

`sudo systemctl status apache2`

If the status of apache2 is displayed as "green" and it is running, then we have successfully completed all the necessary steps. Congratulations! We have successfully launched our first web server in the cloud!

![4](https://user-images.githubusercontent.com/123396933/230793860-ae4235c8-b3eb-4123-8bdb-1dabf76a7356.PNG)

Now, let's verify if our server is running and accessible both locally and from the internet. To check the local access in Ubuntu shell, we can run the following command:

`curl http://localhost:80`

![5](https://user-images.githubusercontent.com/123396933/230793962-3ca0f69d-d884-42ec-a9ea-03882af1d1bb.PNG)

It's now time to test the responsiveness of our Apache HTTP server to requests from the internet. We need to open a web browser and attempt to access the following URL:
`http://<Public-IP-Address>:80`

![6](https://user-images.githubusercontent.com/123396933/230794092-00e7daba-16e3-4a08-bd8d-2cd8c4571da2.PNG)

looks like this:

![7](https://user-images.githubusercontent.com/123396933/230794149-5cfd2246-35a5-4ae1-86fa-5a656c5e0846.PNG)

It works

### STEP 2
#### Installing MYSQL

- Use ‘apt’ to acquire and install this software

- `sudo apt install mysql-server`

When prompted, confirm installation by typing Y, and then ENTER.

- When the installation is finished, log in to the MySQL console by typing:
 `sudo mysql`
 
 ![8](https://user-images.githubusercontent.com/123396933/230795249-caba6ba2-1ed8-4563-9cd2-ab9c4b0485de.PNG)

- It is advisable to execute a security script that is pre-installed with MySQL. This script will eliminate insecure default settings and secure access to our database system. Prior to running the script, we will need to set a password for the root user, using 'mysql_native_password' as the default authentication method. The password for this user will be defined as 'PassWord.1'.
`ALTER USER 'root'@'localhost' IDENTIFIED WITH mysql_native_password BY 'PassWord.1';`

![9](https://user-images.githubusercontent.com/123396933/230795348-ba8809ef-cb90-45eb-a9c9-d074688e48a5.PNG)

- Exit the MySQL shell with:

`mysql> exit`  

![11](https://user-images.githubusercontent.com/123396933/230795544-cfc662f5-52dd-4522-805b-3d8a195afebb.PNG)

- Start the interactive script by running
`sudo mysql_secure_installation`

  - Answer Y for yes, or anything else to continue without enabling.
  
  ![12](https://user-images.githubusercontent.com/123396933/230795759-50d2bef0-2915-4635-8c85-24d9152bdfd3.PNG)

Press y|Y for Yes, any other key for No:

If we choose to answer "yes" to the script, we will be prompted to select a level of password validation. It's important to note that if we input '2' for the strongest level, we may encounter errors while setting passwords that do not meet the criteria of including numbers, uppercase and lowercase letters, special characters, or are based on common dictionary words. For example, "PassWord.1" would meet the criteria for this level of password validation.

![13](https://user-images.githubusercontent.com/123396933/230795922-ff154097-48ef-4dab-8804-b652ff9f6fa5.PNG)

For the remaining prompts, press 'Y' and then press the 'ENTER' key to proceed. This will guide you through changing the root password, removing anonymous users and the test database, disabling remote root logins, and loading the new rules so that MySQL immediately incorporates the changes you have made.

To log in to the MySQL console, type:
`sudo mysql -p`

![14](https://user-images.githubusercontent.com/123396933/230796044-10106ddd-9725-48cf-9020-8e24217e9266.PNG)


- Exit the MySQL shell with:

`mysql> exit`

#### Your MySQL server is now installed and secured. Next, we will install PHP, the final component in the LAMP stack.

### STEP 3  INSTALLING PHP

We have Apache installed to serve our content, MySQL installed to store and manage our data, and PHP as the component that will process code to display dynamic content to the end user. To complete the setup, we will need to install the following packages:

php-mysql: This is a PHP module that allows PHP to communicate with MySQL-based databases.
libapache2-mod-php: This package enables Apache to handle PHP files.
When we install the php package, the necessary core PHP packages will be automatically installed as dependencies.

- To install all three packages - php, php-mysql, and libapache2-mod-php - simultaneously, we can run the following command:

`sudo apt install php libapache2-mod-php php-mysql`

- After the installation is completed, we can use the following command to verify our PHP version:

`php -v`

![16](https://user-images.githubusercontent.com/123396933/230796369-26c485fc-55cb-413d-8793-298553b51bf3.PNG)

At this point, our LAMP stack is completely installed and fully operational.

· Linux (Ubuntu)

· Apache HTTP Server

· MySQL

· PHP 

### STEP 4  CREATING A VIRTUAL HOST FOR YOUR WEBSITE USING APACHE

- Create the directory for projectlamp using ‘mkdir’ command as follows:

`sudo mkdir /var/www/projectlamp`

- Next, assign ownership of the directory with our current system user:

`sudo chown -R $USER:$USER /var/www/projectlamp`

- Then, create and open a new configuration file in Apache’s sites-available directory using your preferred command-line editor.

`sudo nano /etc/apache2/sites-available/projectlamp.conf`

 This will create a new blank file. Paste in the following configuration text:
```
<VirtualHost *:80>

ServerName projectlamp

ServerAlias www.projectlamp

ServerAdmin webmaster@localhost

DocumentRoot /var/www/projectlamp

ErrorLog ${APACHE_LOG_DIR}/error.log

CustomLog ${APACHE_LOG_DIR}/access.log combined

</VirtualHost>
```     
- right click and paste

![17](https://user-images.githubusercontent.com/123396933/230796484-b539b828-e45b-47d5-b0b6-55626f91a4a7.PNG)

- press ctrl + x to exit

- Type Yes and Enter
![18](https://user-images.githubusercontent.com/123396933/230796546-156020fb-5b46-4660-a969-4aaa0be9e482.PNG)

Please press the 'ENTER' key to execute the command.

![19](https://user-images.githubusercontent.com/123396933/230796582-4ada17de-f669-4a89-a412-0efd0c5c83ba.PNG)

We can utilize the 'ls' command to display the new file in the 'sites-available' directory.

`sudo ls /etc/apache2/sites-available`

 You will see something like this;
 
 ![20](https://user-images.githubusercontent.com/123396933/230797076-7f2a23ea-fc10-4af3-a22d-cfa4383f7dde.PNG)

We can now enable the new virtual host using the 'a2ensite' command.

`sudo a2ensite projectlamp`

If we are not using a custom domain name and want to disable Apache's default website to prevent it from overriding our virtual host configuration, we can use the 'a2dissite' command. Enter the following command:

`sudo a2dissite 000-default`

To ensure that our configuration file does not contain any syntax errors, we can run the following command:

`sudo apache2ctl configtest`

![21](https://user-images.githubusercontent.com/123396933/230797387-593ac689-ea50-43b9-9b40-df33e0ebe3de.PNG)

- Finally, reload Apache so these changes take effect:

`sudo systemctl reload apache2`

![22](https://user-images.githubusercontent.com/123396933/230797424-46023dfc-5241-4ba1-833b-0ae02c7a2393.PNG)

- Our new website is now active, but the web root /var/www/projectlamp is still empty. Lets create an index.html file in that location so that we can test that the virtual host works as expected:

 `sudo echo 'Hello LAMP from hostname' $(curl -s http://169.254.169.254/latest/meta-data/public-hostname) 'with public IP' $(curl -s http://169.254.169.254/latest/meta-data/public-ipv4) > /var/www/projectlamp/index.html`
 
 - Now let's go to our browser and try to open our website URL using IP address:

   `http://<EC2-Public-IP-Address>:80`
   
![23](https://user-images.githubusercontent.com/123396933/230797545-8e521d2a-060c-4ccd-90ce-fb1b49c0c62c.PNG)

- We can also access our website in our browser by public DNS name, not only by IP. Let us try it out, the result must be the same (port is optional)

  `http://<Public-DNS-Name>:80`
  
  ![24](https://user-images.githubusercontent.com/123396933/230797596-5252653d-1172-4c82-886f-9c6e16d62bb6.PNG)

- Let's keep the 'index.html' file as a temporary landing page for our application until we set up an 'index.php' file to replace it. Once we configure the 'index.php' file, we will remove or rename the 'index.html' file from our document root, as it would take precedence over an 'index.php' file by default.

### STEP 5  ENABLE PHP ON THE WEBSITE

- In case we want to change the default behavior of Apache where 'index.html' takes precedence over 'index.php' file, we can edit the '/etc/apache2/mods-enabled/dir.conf' file and modify the order of listing within the 'DirectoryIndex' directive to prioritize 'index.php' file.

`sudo nano /etc/apache2/mods-enabled/dir.conf`

- clear everythng and paste this in:

 ```
<IfModule mod_dir.c>

#Change this:

#DirectoryIndex index.html index.cgi index.pl index.php index.xhtml index.htm

#To this:

DirectoryIndex index.php index.html index.cgi index.pl index.xhtml index.htm

</IfModule>
```

- press ctrl + x to exit
- Type Yes and Enter

![25](https://user-images.githubusercontent.com/123396933/230798026-5294012e-af13-4328-8d2c-8263b4ba066c.PNG)

- press Enter

- After saving and closing the file, you will need to reload Apache so the changes take effect:

`sudo systemctl reload apache2`


- Create a new file named index.php inside your custom web root folder:

`nano /var/www/projectlamp/index.php`

- This will open a blank file. Add the following text, which is valid PHP code, inside the file:

```
<?php

phpinfo();
```

![26](https://user-images.githubusercontent.com/123396933/230798051-6a372118-ad3f-4b6d-b5db-4ea23168ed91.PNG)

- save and close the file, refresh the page and you will see a page similar to this:

![27](https://user-images.githubusercontent.com/123396933/230798224-227eb2b2-44cc-4b46-bf68-5cb02974254c.PNG)

This webpage provides PHP-related server information, useful for debugging and verifying correct settings implementation. This page shows that our PHP installation is working.

After reviewing the PHP server information, it is recommended that we delete the created file as it may contain sensitive data about our PHP environment and Ubuntu server. We can use the "rm" command to remove the file.

`sudo rm /var/www/projectlamp/index.php`

We can always recreate this page whenever need to access the information again later.



## We can now terminate our instance and any other resources to avoid additional charges





















