# Docker_Project_NextCloud
Hey! I have created a Docker Project using a cloud called NextCloud and MySQL Database on top of RedHat Linux. Here I am  going to show you the whole set-up step by step. 
 ## A) Download the RedHat Linux 8
 ## B) Download the Docker tool
First of all configure the yum command in linux and download the software by 
        
    yum install docker-ce --nobest 
and start the docker by command 

    systemctl start docker.
 ## C) Download the Required Images
Download The NextCloud and MySQL image from [](hub.docker.com) using 
    
    docker pull nextcloud:latest
    docker pull mysql:5.7 
commands.
 ## D) MySQL setup
Write a command 

    docker -i -t -e MYSQL_ROOT_PASSWORD=(your_password) -e MYSQL_USER=(username) -e MYSQL_PASSWORD=(your_password) -e MYSQL_DATABASE=       (any_database_name) --name dbos mysql:5.7
 ## E) MySQL client
If you want to verify that your database folder has been created or not, install MySQL client software using yum install mysql. After installation run this command : 
   
    mysql -h 172.17.0.0/16 (your MySQL container IP) -u (username) -p
 ## F) Docker-Compose
Install a docker-compose software from https://docs.docker.com/compose/install. 
Make a compose file using 

    mkdir mycompose. 
You can create/edit your docker-compose file using 
    
    vim docker-compose.yml
The file name should always be docker-compose.yml
This is my yml file :
      
![docker-compose (2)](https://user-images.githubusercontent.com/58370459/80699329-68534980-8af9-11ea-8917-89e1176fa03c.jpg)

You can start/stop the service in just a single command using docker-compose up and docker-compose stop. 
   #### Version :
Each version has different syntax. This version supports docker-compose fine. 
   #### Services : 
In service, which containers we want to run.
   #### Containers :
dbos and cloudos are the name of docker container. Docker-compose will automatically create the specified name containers.
   ####  Image : 
Specify the image we want to use.
   #### Restart :
By chance any of the container stops, docker-compose will restart it again.
   #### Volumes : 
All our data will be permanent if we mount a volume to the folders where NextCloud and MySQL stores data. The data will remain permanent if any of the container terminates. For that you have to create volumes first. 
   #### Depends_on : 
NextCloud uses database server. We have to specify which database container it should depend on.
   #### Ports : 
To expose our container to outside world by using PAT.
   
   ## H) Troubleshooting the errors
Linux firewall won't allow to connect to MySQL database server and to outside world. Hence following commands should be implemented first in order to connect to server.
- selinux 0
- iptables -F
- iptables -P FORWARD ACCEPT
- firewall-cmd --zone=trusted --change-interface=docker0 --permanent (If there are any other networks for docker add them too like br-xxxxx)
- firewall-cmd --zone=trusted --add-masquerade --permanent
- firewall-cmd --add-port=3306/tcp
- firewall-cmd --reload
- systemctl restart docker
- Change your network settings to Bridge Adapter
         
   That's it. You can start/stop your services in just a single go.  
             NOTE : - It only works on other devices if you have a same network connectivity (LAN). You can use any of the images like WordPress, Joomla, Drupal, Owncloud, etc and Database images like MariaDB, Oracle, etc.
