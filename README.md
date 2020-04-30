# Docker_Project_NextCloud
Hey! I have created a Docker Project using a cloud called NextCloud and MySQL Database on top of RedHat Linux. Here I am  going to show you the whole set-up step by step. 
 ## A) Download the RedHat Linux 8
 ## B) Download the Docker tool
      First of all configure the yum command in linux and download the software by <span style="color:grey;">yum install docker-ce --nobest</span> and start the docker by systemctl start docker.
 ## C) Download the Required Images
      Download The NextCloud and MySQL image from hub.docker.com using docker pull nextcloud:latest and docker pull mysql:5.7 commands.
 ## D) MySQL setup
      Write a command docker -i -t -e MYSQL_ROOT_PASSWORD=(your_password) -e MYSQL_USER=(username) -e MYSQL_PASSWORD=(your_password) -e         MYSQL_DATABASE=(any_database_name) --name dbos mysql:5.7
 ## E) MySQL client
      If you want to verify that your database folder has been created or not, install MySQL client software using yum install mysql.
      After installation run this command : mysql -h 172.17.0.0/16 (your MySQL container IP) -u (username) -p
 ## F) Docker-Compose
      Install a docker-compose software from https://docs.docker.com/compose/install
      Make a mycompose file using mkdir mycompose. You can create/edit your docker-compose file using vim docker-compose.yml 
      
