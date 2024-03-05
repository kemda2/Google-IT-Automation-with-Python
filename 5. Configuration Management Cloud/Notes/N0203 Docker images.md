# Docker images 

Docker images are the building blocks of Docker containers. They are lightweight, immutable, and composed of multiple layers. A Docker image contains the application code, data files, configuration files, libraries, and other dependencies needed to run an application.

In this reading, you will learn more about Docker images and their layers. You’ll also learn how to build a Docker image, and you’ll review an example of a Dockerfile.

## Docker images and image layers

You can think of a Docker image as a template from which Docker containers are created and executed. Each Docker image is composed of multiple layers—adding or removing files from the previous layer. Each layer represents a specific set of changes made to the image and is composed based on the instructions in a Dockerfile. The instructions in a Dockerfile define how the image should be built.

**Note:** It’s not uncommon for an image to be composed of a dozen or more layers.

The purpose of having multiple layers is to keep the final images as small as possible—you do this by reusing layers in multiple images—and to speed up the process of building containers, as Docker has to rebuild only the layers that have changed.

## How to build a Docker image

The key to packaging your own application as a Docker image is to have a Dockerfile. The Dockerfile acts as your source of truth or instruction manual: It specifies how Docker should build the image and contains a series of commands to build the image. Each command builds a new layer that becomes part of the final image. A common process is to start with a base image such as Debian Linux or Python 3.10, install the libraries your application requires, then copy the application and any related files into the image. Let’s take a look at a simple Dockerfile for a Python application example:

`FROM python:3.9 `

This line of code says that you’re starting from the Python 3.9 base image.

`COPY *.py setup.cfg LICENSE README.md requirements.txt /app/`

`WORKDIR /app`

This command says to copy all of the application’s files to a folder inside the container named **/app** and make it the current working directory.

`RUN pip install -r requirements.txt`

`RUN python setup.py install`

These two lines of code run the Python commands to install the libraries required by the app. When that step is complete, build and install the app inside the container.

`EXPOSE 8000`

`CMD [ "/usr/local/bin/my-application" ]`

This command tells Docker what executable should run when the container starts and that the container will listen for network connections on port 8000.

**Pro tip:** To build this image from the Dockerfile, use the command: **docker build**. If the build is successful, Docker outputs the ID of the new image, which you can then use to start a container.

Refer to the [Dockerfile reference](https://docs.docker.com/engine/reference/builder/) for a full list of commands that can appear in a Dockerfile.

## Image names, tags, and IDs

You use tags and IDs to identify and reference Docker images. Their unique names provide a way to differentiate between specific versions of Docker images. The ID is a random string of numbers and letters, which most of the time are way too complicated to remember. But there’s good news! You can assign any number of tags to the image, in addition to the ID. Tags are alphanumeric labels that help users find the correct image. Most images are tagged with the author’s Github username, the name of the application, and a version number. 

**Pro tip:** Tag the most recent version of an image with **latest** in addition to a version number. This makes it easy for people to find the current version of your application.

Let’s look at an example:


```
csmith/my-docker-image:1.0

csmith/my-docker-image:latest 

sha256:abc123def456

```

**csmith** is the name of the author, **my-docker-image** is the image name, **1.0** is the version number (and it’s the latest version), and **sha256:abc123def456** represents the image ID.

## How to manage images

A great thing about Docker is that it caches images on a disk. Therefore, you don’t need to go grab them or rebuild them every time you need them. This saves you so much time! Some of the Docker CLI (command line interface) commands you can use include:

- **docker image ls** – This command lists the images cached locally.

- **docker image tag** – This command applies tags to a local image.

- **docker image pull** – This command fetches an image from a remote repository.

- **docker image push** – This command sends a local image to a remote repository.

- **docker image rm** – This command removes an image from the cache.

- **docker image prune** – This command removes all unused images to reclaim disk space.

## Key takeaways

Docker images—including tags and IDs—are essential for programmers to package, distribute, and deploy applications more efficiently, reducing issues and improving the stages of the software workflow. Remember, in order to have a Docker image, you must have a Dockerfile. These components work hand-in-hand; you can’t have one without the other.

  


