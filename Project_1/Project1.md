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

- Run this command to ensure your key is not publicly viewable.

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

If the status of apache2 is displayed as "green" and it is running, then you have successfully completed all the necessary steps. Congratulations! You have successfully launched your first web server in the cloud!

![4](https://user-images.githubusercontent.com/123396933/230793860-ae4235c8-b3eb-4123-8bdb-1dabf76a7356.PNG)

Now, let's verify if our server is running and accessible both locally and from the internet. To check the local access in Ubuntu shell, you can run the following command:

`curl http://localhost:80`

![5](https://user-images.githubusercontent.com/123396933/230793962-3ca0f69d-d884-42ec-a9ea-03882af1d1bb.PNG)

It's now time to test the responsiveness of our Apache HTTP server to requests from the internet. Please open a web browser of your choice and attempt to access the following URL:
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

- It is advisable to execute a security script that is pre-installed with MySQL. This script will eliminate insecure default settings and secure access to your database system. Prior to running the script, you will need to set a password for the root user, using 'mysql_native_password' as the default authentication method. The password for this user will be defined as 'PassWord.1'.
`ALTER USER 'root'@'localhost' IDENTIFIED WITH mysql_native_password BY 'PassWord.1';`

![9](https://user-images.githubusercontent.com/123396933/230795348-ba8809ef-cb90-45eb-a9c9-d074688e48a5.PNG)

- Exit the MySQL shell with:

`mysql> exit`  












