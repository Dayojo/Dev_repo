# WEB STACK IMPLEMENTATION (LEMP STACK)

## LEMP (Linux, Engine X (NGINX), MySQL, PHP)

- We need an AWS account

- launch a new EC2 instance of t2.micro family with Ubuntu Server 22.04 LTS

- Private key (.PEM file) should be saved securely and spin up the instance

- Connecting to EC2 terminal

  - Using the terminal on MAC/Linux

  - Using Windows Terminal

  - We'll be connecting to the EC2 instance using Gitbash terminal installed in my windows system
  
- We'll be needing our saved PEM key file change directory to download folder 
![0](https://user-images.githubusercontent.com/123396933/235159484-1bd168a5-8bd9-4ea5-a1c6-d3defeb4fac9.PNG)

- Run this command to ensure your key is not publicly viewable

  `chmod 400 <your-PEM-file-name>.pem`
  
![1](https://user-images.githubusercontent.com/123396933/235173887-6f58b62a-fdeb-4316-a126-4e841f2f7936.PNG)

- I will utilize the ssh protocol to establish a connection between my local terminal and my EC2 server

  `ssh -i <private-key-name>. pem ubuntu@<Public-IP-address>`
  
  ![2](https://user-images.githubusercontent.com/123396933/235178210-2324b0d5-b42a-4970-87c3-1d897a87fe14.jpg)

- Type `yes` to connect

- Now we are connected to our instance well done 🎉

## Step 1 Installing the Nginx Web Server

- `sudo apt update` 
![3](https://user-images.githubusercontent.com/123396933/235178553-a166c566-1577-4383-87fd-dc3aee92a725.PNG)

- `sudo apt install nginx` 
- When prompted, enter `Y` to confirm that you want to install Nginx


![4](https://user-images.githubusercontent.com/123396933/235178761-02c92412-b825-4458-bbae-9751b9d84d37.jpg)


- To confirm that nginx has been installed correctly and is functioning as a service on Ubuntu. 

- Run: `sudo systemctl status nginx`

If it is green and running, then you did everything correctly

- As we know, we have TCP port 22 open by default on our EC2 machine to access it via SSH, so we need to add a rule to EC2 configuration to open inbound connection through port 80: Our server is running and we can access it locally and from the Internet (Source 0.0.0.0/0 means ‘from any IP address’). First, let us try to check how we can access it locally in our Ubuntu shell

- Run: `curl http://localhost:80`

![5](https://user-images.githubusercontent.com/123396933/235179975-ab92a830-22a0-4b97-8cf5-0608f6b532ff.jpg)

- Let's test if our Nginx server can respond to requests from the Internet

Open a web browser of your choice and try to access following url `http://<EcintancePublic-IP-Address>:80`

![6](https://user-images.githubusercontent.com/123396933/235182576-22ca64ed-aaf8-4e80-8227-9c66528ad6bb.PNG)

If you see following page, then your web server is now correctly installed and accessible through your firewall.


## STEP 2 INSTALLING MYSQL

- To acquire and install this software:

`sudo apt install mysql-server` 
when promted type `yes`

- When the installation is finished, log in to the MySQL console by typing:

`sudo mysql`

![7](https://user-images.githubusercontent.com/123396933/235184723-9157a0aa-1906-4d87-b4b1-0c7e872d3168.jpg)

- Before running the script, you will set a password for the root user, using mysql_native_password as default authentication method. We’re defining this user’s password as PassWord.1 `ALTER USER 'root'@'localhost' IDENTIFIED WITH mysql_native_password BY 'PassWord.1';`

Exit the MySQL shell with:

mysql> `exit`

Start the interactive script by running:

`sudo mysql_secure_installation`

This will ask if you want to configure the VALIDATE PASSWORD PLUGIN.

Answer `Y` for yes, or anything else to continue without enabling.

![8](https://user-images.githubusercontent.com/123396933/235187868-ffdb7413-1ab2-4a4c-913c-39b1f0fcb7f2.jpg)

Let's test if we are able to log in to the MySQL console by typing: `sudo mysql -p`
Notice the -p flag in this command, which will prompt you for the password used after changing the root user password.

Exit the MySQL console, type: mysql> `exit` Notice that you need to provide a password to connect as the root user.

## STEP 3 INSTALLING PHP

- To process PHP requests, it's necessary to set up php-fpm, an acronym for "PHP fastCGI process manager", and configure Nginx to route them to this program. Moreover, you'll require php-mysql, a PHP extension that facilitates communication with databases based on MySQL. The fundamental PHP packages will be automatically installed as dependencies.

 - To install these 2 packages at once, run:

`sudo apt install php-fpm php-mysql`

When prompted, type `Y` and press ENTER to confirm installation. You now have your PHP components installed. Next, you will configure Nginx to use them.

## STEP 4 CONFIGURING NGINX TO USE PHP PROCESSOR

- Nginx web server allows us to create server blocks that act like virtual hosts in Apache, enabling us to compartmentalize configuration details and support multiple domains on a single server. To illustrate this concept, we will use the domain name "project LEMP" in this guide.

- Create the root web directory for your domain as follows:
`sudo mkdir /var/www/projectLEMP`

- Let's assign ownership of the directory with the $USER environment variable, which will reference your current system user:
`sudo chown -R $USER:$USER /var/www/projectLEMP`

- Then, open a new configuration file in Nginx’s sites-available directory using your preferred command-line editor. Here, we’ll use nano:
`sudo nano /etc/nginx/sites-available/projectLEMP`

paste this:
```
#/etc/nginx/sites-available/projectLEMP

server {
    listen 80;
    server_name projectLEMP www.projectLEMP;
    root /var/www/projectLEMP;

    index index.html index.htm index.php;

    location / {
        try_files $uri $uri/ =404;
    }

    location ~ \.php$ {
        include snippets/fastcgi-php.conf;
        fastcgi_pass unix:/var/run/php/php8.1-fpm.sock;
    }

    location ~ /\.ht {
        deny all;
    }

}

```

When you’re done editing, save and close the file. If you’re using nano, you can do so by typing: CTRL+X and then y and ENTER to confirm.

- Activate your configuration by linking to the config file from Nginx’s sites-enabled directory:

`sudo ln -s /etc/nginx/sites-available/projectLEMP /etc/nginx/sites-enabled/`

This will tell Nginx to use the configuration next time it is reloaded. You can test your configuration for syntax errors by typing:

`sudo nginx -t`

You shall see following message:

![9](https://user-images.githubusercontent.com/123396933/235194647-e79f0522-647c-4545-8e5b-53c6e765f38a.jpg)

- If you receive any error messages, you should revisit your configuration file and check its contents before proceeding further. In addition, you must deactivate the default Nginx host that is presently set to use port 80. To accomplish this, execute the following command:

`sudo unlink /etc/nginx/sites-enabled/default`

- Let's reload Nginx to apply the changes:

`sudo systemctl reload nginx`

- The website is up and running now, but the web root directory located at /var/www/projectLEMP is still empty. To ensure that your new server block is functioning correctly, We will create an index.html file in that directory using the following command:

`sudo echo 'Hello LEMP from hostname' $(curl -s http://169.254.169.254/latest/meta-data/public-hostname) 'with public IP' $(curl -s http://169.254.169.254/latest/meta-data/public-ipv4) > /var/www/projectLEMP/index.html`

Now go to your browser and try to open your website URL using IP address: `http://<EcintancePublic-IP-Address>:80`

![10](https://user-images.githubusercontent.com/123396933/235366448-679f2aab-289d-41f6-8af5-95b083da3824.PNG)

The "echo" command we used to write to the index.html file was successful, indicating that our Nginx site is working correctly.

Next, let's attempt to access the website using the DNS name by navigating to the following URL in a web browser:

`http://<InstancePublicPublic-DNS-Name>:80`

![11](https://user-images.githubusercontent.com/123396933/235366570-935c81d7-6ef9-41b2-9bd1-1c93dfd0ad16.PNG)

- Your LEMP stack is now fully configured. In the next step, we’ll create a PHP script to test that Nginx is in fact able to handle .php files within your newly configured website.

## STEP 5 TESTING PHP WITH NGINX

Open a new file called info.php within your document root in your text editor:
`sudo nano /var/www/projectLEMP/info.php`

Type or paste the following lines into the new file. This is valid PHP code that will return information about your server:

```
<?php
phpinfo();
```

![12](https://user-images.githubusercontent.com/123396933/235366894-b7b3269a-0973-49db-b01d-cc5a7504e791.PNG)








