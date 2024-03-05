# Using multiple containers 

Imagine you are developing a web-based platform that allows users to browse products, add items to their cart, pay for items, and ship items to different addresses. This application requires multiple components to execute properly because it relies on a number of microservices. The idea behind microservices is to take a large application and break it up into smaller, more tangible, independent parts of the application that are self-contained. This allows for each part of the application to be better maintained. Because these microservices are independent of each other, you use multiple containers to test the entirety of the application to ensure everything runs smoothly. It’s no surprise that in the programming world, programmers and developers work with multiple containers at a time.

In this reading, you will learn more about the use of multiple containers, commands for working with multiple containers, how related services find each other, and how to install Docker Compose and view an example.



## Starting multiple containers

To start multiple containers, you need to run multiple **docker run** commands. A **docker run** command creates a container and starts it. Let’s look at an example of how to create and start two containers that work together once they find each other by name.

As a programmer, you’ve been asked to set up a WordPress blog. You know WordPress requires a database to store its content. You create and start two containers, **wordpress** and **db**, using the following command:

```
$ docker run -d —name db —restart always \

    -v db_data:/var/lib/mysql -p 3306 -p 33060 \

    -e MYSQL_ROOT_PASSWORD=somewordpress \

    -e MYSQL_DATABASE=wordpress \

    -e MYSQL_USER=wordpress \

    -e MYSQL_PASSWORD=wordpress \

    mariadb:10
```

This command starts the **mariadb** database, determines a storage volume, and sets the initial password for the WordPress user. It declares two network ports open to other containers, but it is not shown on the host machine.

Now, start the WordPress container using the following command:

```
$ docker run -d —name wordpress —restart always \

    -v wp_data:/var/www/html -p 80:80 \

    -e WORDPRESS_DB_HOST=db \

    -e WORDPRESS_DB_USER=wordpress \

    -e WORDPRESS_DB_PASSWORD=wordpress \

    -e WORDPRESS_DB_NAME=wordpress \

    wordpress:latest
```
**Note:** The environment variable **WORDPRESS_DB_HOST** is set to **db** on the third line. This line of code is needed to refer to another container. Docker provides domain name system (DNS) services that allow containers to find each other by their name.



## Networking with multiple containers

Imagine you have several customers using the same application. For security reasons, you have isolated the application and created multiple containers, one for each customer. Docker allows you to create private networks for a container or groups of containers. These private containers are able to discover each other, but no other networks will be able to find the private containers you’ve started. Let’s look at an example: modifying the **wordpress** and **db** containers by putting them on a private network.

First, stop and delete both containers:

`$ docker stop wordpress && docker rm wordpress`

`$ docker stop db && docker rm db`

Then, create a private network for both containers to use:

`$ docker network create myblog`

`0f6abeb9d85a7063298cd70082ac5e5a2f0d1624bae06619fd14dbaa0942b0e2`

Once the containers are on private networks, restart them with the additional option `-network myblog`. This appears on the second to last line for both container commands.

```
$ docker run -d —name db —restart always \

    -v db_data:/var/lib/mysql -p 3306 -p 33060 \

    -e MYSQL_ROOT_PASSWORD=somewordpress \

    -e MYSQL_DATABASE=wordpress \

    -e MYSQL_USER=wordpress \

    -e MYSQL_PASSWORD=wordpress \

    —network myblog \

    mariadb:10

$ docker run -d —name wordpress —restart always \

    -v wp_data:/var/www/html -p 80:80 \

    -e WORDPRESS_DB_HOST=db \

    -e WORDPRESS_DB_USER=wordpress \

    -e WORDPRESS_DB_PASSWORD=wordpress \

    -e WORDPRESS_DB_NAME=wordpress \

    —network myblog \

    wordpress:latest
    
```

It’s good practice to verify that containers on other networks can’t access the private networks you created. To check this, start a new container and attempt to find the private containers you created.

```
$ docker run -it debian:latest 

root@7240f1e3ddab:/# ping db.myblog

ping: db.myblog: Name or service not known

```



## Docker Compose

Docker Compose is an optional tool, provided by Docker, that makes using multiple containers easy. In most instances, Docker Compose is automatically installed during the installation process of Docker Desktop. If not, follow the instructions in [Scenario two: Install the Compose plugin](https://docs.docker.com/compose/install/) to install Docker Compose on your platform.

Docker Compose allows you to define a multiple-container setup in a single [YAML](https://yaml.org/) format, called a Compose file. (YAML is a format for configuration files that’s designed to be both human- and computer-readable.) The Compose file communicates with Docker and identifies the containers you need and how you should configure them. The containers in a Compose file are called services. Let’s look at how you can use Compose to recreate the private networks from the  **wordpress** and **db** example. Run the following on your machine.

1. Create an empty folder and save the file below as `docker-compose.yml`.

```
version: '3.3'

services:

  db:

    image: mariadb:10

    volumes:

      - db_data:/var/lib/mysql

    restart: always

    environment:

      - MYSQL_ROOT_PASSWORD=somewordpress

      - MYSQL_DATABASE=wordpress

      - MYSQL_USER=wordpress

      - MYSQL_PASSWORD=wordpress

    networks:

      - myblog

    expose:

      - 3306

      - 33060

  wordpress:

    image: wordpress:latest

    volumes:

      - wp_data:/var/www/html

    ports:

      - 80:80

    networks:

      - myblog

    restart: always

    environment:

      - WORDPRESS_DB_HOST=db

      - WORDPRESS_DB_USER=wordpress

      - WORDPRESS_DB_PASSWORD=wordpress

      - WORDPRESS_DB_NAME=wordpress

volumes:

  db_data:

  wp_data:

networks:

  myblog:
```

2. Run the command **docker compose up**. This pulls up the images, creates two empty data volumes, and starts both services. The output from both services will intermingle on your screen.

The Compose file grants you control over how each service is configured, including:

Choosing the image

* Choosing the image
* Setting environment variables
* Mounting storage volumes
* Exposing network ports

**Pro tip:** You can also express any option you pass to the `docker run` command as YAML in a Compose file.

A helpful third-party tool—that’s a fan favorite of programmers—that simplifies the process of converting existing Docker run commands into Docker Compose configurations is called Composerize. Refer to [Composerize](https://www.composerize.com/) for additional information. You can test the above Docker command in the Composerize textbox. This command defines a db service similar to the one presented above. Remember, Composerize is just a tool, and unfortunately sometimes tools come and go. It’s best to understand and practice the process of converting an existing Docker run command into a Docker Compose configuration without the help of tools.

For additional information about the options you can put into a Compose file, view the [Compose file overview documentation](https://docs.docker.com/compose/compose-file/).



## Additional Compose commands

Compose has additional commands when working with a single or multiple containers. Let’s look at some examples:

* **docker compose pull:** This fetches the latest image for each service.
* **docker compose up:** This creates the containers and starts the service.
* **docker compose down:** This stops the service and deletes the container.
* **docker compose logs:** This displays the console logs from the container.



## Key takeaways

Using multiple containers enables the adoption of a microservice architecture for your application. Separating a large application into smaller, independent parts allows for a more manageable approach to building, fixing, maintaining, and deploying each part of the application.
