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

# Step 1 Installing the Nginx Web Server

- `sudo apt update` 
![3](https://user-images.githubusercontent.com/123396933/235178553-a166c566-1577-4383-87fd-dc3aee92a725.PNG)

- `sudo apt install nginx` 
- When prompted, enter `Y` to confirm that you want to install Nginx


![4](https://user-images.githubusercontent.com/123396933/235178761-02c92412-b825-4458-bbae-9751b9d84d37.jpg)


- To confirm that nginx has been installed correctly and is functioning as a service on Ubuntu. Run: `sudo systemctl status nginx`

If it is green and running, then you did everything correctly
![5](https://user-images.githubusercontent.com/123396933/235179975-ab92a830-22a0-4b97-8cf5-0608f6b532ff.jpg)





