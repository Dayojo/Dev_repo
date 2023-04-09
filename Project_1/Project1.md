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
 
![3 1](https://user-images.githubusercontent.com/123396933/230747623-1a595e80-9dc8-46e5-88d3-661cd6dceef6.PNG)

- Now we are connected to our instance well done🎉.


![4](https://user-images.githubusercontent.com/123396933/230747836-42a0091d-aab8-496f-a6b4-afc308aaf768.PNG)



