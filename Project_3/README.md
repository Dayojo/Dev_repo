# SIMPLE TO-DO APPLICATION ON MERN WEB STACK

## Step 1
- In order to complete this project, you will need an AWS account and a virtual server with Ubuntu Server OS. When you create your EC2 Instances, you can add Tag "Name" to it with a value that corresponds to a current project you are working on – it will be reflected in the name of the EC2 Instance. Like this:

![0](https://github.com/Dayojo/Dev_repo/assets/123396933/b8c4abd0-49c5-40cc-86cd-1cca550adf63)

## STEP 2 BACKEND CONFIGURATION

`Update ubuntu`

`sudo apt update`

`Upgrade ubuntu`

`sudo apt upgrade`

- Let’s get the location of Node.js software from Ubuntu repositories.

`curl -fsSL https://deb.nodesource.com/setup_18.x | sudo -E bash -`

- Install Node.js on the server:

`sudo apt-get install -y nodejs`

- Verify the node installation with the command:

`node -v`

- Verify the node installation with the command:

`npm -v`
