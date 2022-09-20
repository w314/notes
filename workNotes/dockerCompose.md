# [docker compose](https://docs.docker.com/compose/)

- [medium article](https://medium.com/codex/docker-compose-explained-3954baf495ec)
- docker compose is the solution when it's too cumbersome to run docker complicated docker commands in the command line. It provides the way to give all necessary parameters to run one or more containers with one command

To use docker-compose:
1. Define the app's environment in a `Dockerfile` (image)
1. Define the services that make up your app in a `docker-compose.yaml` file, so that they can run together in an isolated environment
1. Run `docker compose up` that starts and runs your app

Docker Compose Explained
Learn how to create a YAML file for Docker containers and create containers using docker-compose.

Docker Compose Example
Docker containers are created using the docker commands in the command line tool such as command prompt for Windows and terminal for Mac, Linux. Working in the command-line tool is easy when you beginning to learn Docker. However, if you are creating a complex Docker container such as creating multiple Docker containers and connecting them using the network. Managing the complex docker code/command is a tedious task. We have to use the backslash for multiple lines. Editing the commands in the terminal is also not an easy task. To address this problem, Docker proposed a new solution.

The solution is docker-compose. The docker-compose needs a YAML file. Put all the configuration code in the YAML file such as Image name, container name, host port and container, environment variables, etc. The YAML file format will be a little bit different from the Docker commands in the command line. I created a pictorial representation to understand it better.

Convert Commands To YAML File:
In the previous article, I had shown how to connect MySQL and phpMyAdmin using the Docker network. The code used for connecting MySQL and phpMyAdmin Docker containers is given below.

Create a common Docker Network.

docker network create mysql-network
Create MySQL Docker container.

docker run -d -p 3307:3306 \
    -e MYSQL_ROOT_PASSWORD=password \
    --name mysqldb \
    --net mysql-network \
    mysql
Create phpMyAdmin Docker container.

docker run -d -p 8082:80 \
    -e PMA_HOST=mysqldb \
    --name phpmyadmin \
    --net mysql-network \
    phpmyadmin:5.1-apache
Please note. If we are using the YAML file, then there is no need to create the Docker network. The docker-compose tool will automatically create a network and connect the containers present in the YAML file.

Create a YAML file for the MySQL container:
Rather than explaining the steps, I thought to give a pictorial explanation on how to map the commands to the YAML file. I think the image given below will help you to understand it better. If you are not able to understand how to convert the commands to the YAML file, then please feel to comment on it.

The file extension is yaml.


MySQL Docker Compose Example
Create a YAML file for the phpMyAdmin container:
Same as like MySQL, the below image shows how to create a YAML from the docker commands.


phpMyAdmin Docker Compose Example
Full YAML File Code:
The full code for MySQL and phpMyAdmin is given below.


Create a new file names mysql.yaml using the below command. And paste the above code into the file.

sudo nano mysql.yaml
Execute YAML File Using Docker Compose:
Now we have a YAML file for deploying Docker containers( MySQL and phpMyAdmin ). To up and run the containers using the YAML file, Docker offers a special tool called docker-compose. By using docker-compose, we can easily spin a container from the YAML file and down the containers created too.

The docker-compose installed while installing the Docker.

Create containers using the command docker-compose up.

#docker-compose -f file_name up -d
docker-compose -f mysql.yaml up -d
Please use detach mode using -d.

Stop the created container using the command docker-compose down.

docker-compose -f mysql.yaml down
Summary:
Using Docker compose tool is recommended. Why because, if we are implementing a complex container setup, then the command line won’t suit. Managing all the commands in the command line is a tedious task. And modifying the code is also a complex one if we use the command-line tool. The docker-compose addresses all the mentioned problems. We can easily edit the code using any text editor. So using docker-compose is highly recommended. I hope this tutorial will help you to learn about docker-compose.

Stay tuned for more articles.

