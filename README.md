# 2-tier-java-application

1. Launch ubuntu ec2 instance on amazon
2. connect using SSH

3. Install Docker on it
   ```bash
   sudo apt install docker.io
   ```
4. clone repository using
   ```bash
   git clone https://github.com/LondheShubham153/two-tier-flask-app.git
   ```
5. Navigate to the project directory:
   ```bash
   cd two-tier-flask-app
   ```

6. Create a .env file in the project directory to store your MySQL environment variables:
   ```bash
   touch .env
   ```
7.Open the .env file and add your MySQL configuration:
   ```bash
   MYSQL_HOST=mysql
   MYSQL_USER=your_username
   MYSQL_PASSWORD=your_password
   MYSQL_DB=your_database
   ```
8. Create requirements.txt file and packages in it
   ```bash
   Flask==2.0.1
   Flask-MySQLdb==0.2.0
   requests==2.26.0
   Werkzeug==2.2.2
   ```
9. Create Dockerfile and add all things in it
10. After That build Dockerfile:
    ```bash
    docker build . -t flaskapp
    ```
11. Crete newwork for connecting mysql and flsk app docker container
    ```bash
    docker network create twotier
    ```

12. Now run the dockerfile with port mapping as 5000 port and network connection between mysql and app docker image and with environment variables
    ```bash
     docker run -d -p 5000:5000 --network=twotier -e MYSQL_HOST=mysql -e MYSQL_USER=admin -e MYSQLPASSWORD=admin -e MYSQL_DB=myDb --name=flaskapp flaskapp:latest
    ```
13. For database we require mysql so pull images of mysql and connect network and add env variables
    ```bash
    docker run -d -p 3306:3306 --network=twotier -e MYSQL_DATABASE=myDb -e MYSQL_USER=admin -e MYSQLPASSWORD=admin -e MYSQL_ROOT_PASSWORD=admin --name=mysql mysql:5.7
    ```
    
