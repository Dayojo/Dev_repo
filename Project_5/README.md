

# IMPLEMENTATION OF A CLIENT SERVER ARCHITECTURE USING MYSQL DATABASE MANAGEMENT SYSTEM (DBMS).

## CLIENT-SERVER ARCHITECTURE WITH MYSQL

- Understanding Client-Server Architecture As you proceed with your journey into the world of IT, you will begin to realise that certain concepts apply to many other areas. One of such concepts is – Client-Server architecture. Client-Server refers to an architecture in which two or more computers are connected together over a network to send and receive requests between one another. In their communication, each machine has its own role: the machine sending requests is usually referred as "Client" and the machine responding (serving) is called "Server". A simple diagram of Web Client-Server architecture is presented below:
  
![00](https://github.com/Dayojo/Dev_repo/assets/123396933/68fa1a62-b7f2-40da-8da2-7f7f000328e7)

In the example above, a machine that is trying to access a Web site using a Web browser or simply ‘curl’ command is a client and it sends HTTP requests to a Web server (Apache, Nginx, IIS or any other) over the Internet. If we extend this concept further and add a Database Server to our architecture, we can get this picture:
a
![01](https://github.com/Dayojo/Dev_repo/assets/123396933/a6acee30-fe95-421e-bcbf-5e31be95ba85)

![02](https://github.com/Dayojo/Dev_repo/assets/123396933/0d350c47-2dea-4d8b-b93b-f16f83186ba0)

![03](https://github.com/Dayojo/Dev_repo/assets/123396933/49124157-fe76-4ca0-b52e-e63471de6c53)


- On mysql server Linux Server install MySQL Server software.

`sudo apt update`

- Then install the mysql-server package:
  
`sudo apt install mysql-server`

- Ensure that the server is running using the systemctl command:

`sudo systemctl start mysql.service`

`sudo systemctl status mysql.service`

![05](https://github.com/Dayojo/Dev_repo/assets/123396933/395ecb28-4d02-438c-a887-0d527f6a7a6a)

- Let's set it up
`sudo mysql`

- For the password i'll be using 'PassWord.1'
  
`ALTER USER 'root'@'localhost' IDENTIFIED WITH mysql_native_password BY 'PassWord.1';`

- We are going to run a MySQL secure installation
  
`sudo mysql_secure_installation`


