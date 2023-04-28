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

- I will utilize the ssh protocol to establish a connection between my local terminal and my EC2 server

  `ssh -i <private-key-name>. pem ubuntu@<Public-IP-address>`

![1](https://user-images.githubusercontent.com/123396933/235173887-6f58b62a-fdeb-4316-a126-4e841f2f7936.PNG)

- Type `yes` to connect

- Now we are connected to our instance well done 🎉

# Step 1 Installing the Nginx Web Server

- `sudo apt update` `sudo apt install nginx` When prompted, enter Y to confirm that you want to install Nginx

- To confirm that nginx has been installed correctly and is functioning as a service on Ubuntu. Run `sudo systemctl status nginx`
