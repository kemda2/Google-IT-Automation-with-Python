# Build artifacts testing

No matter what code you write, you’ll need to test it. You want to create a product that is free of errors and bugs. Testing build artifacts and troubleshooting within your tests are great ways to ensure the quality of your work.

In this reading, you will learn more about different types of build artifacts, how to test a Docker container, and how to troubleshoot any issues along the way.



## Build artifacts  

Build artifacts are items that you create during the build process. Your main artifact is your Docker container, if you’re working within a Dockerized application. All other items that you generate during the Docker image build process are also considered build artifacts. Some examples include:

* Libraries
* Documentation
* Static files
* Configuration files
* Scripts
* Build artifacts in Docker 

Build artifacts in Docker play a crucial role in the software development and deployment lifecycle. No matter what you create with code, you need to test it. You must test your code before deployment to ensure that you catch and correct all issues, defects, and errors. This is true whether your code is built as a Docker container or built the more “classic” way. The process to execute the testing varies based on the application and the programming language it’s written in.

**Pro tip:** It’s important to check that Docker built the container itself correctly if you are testing your code with a containerized application.

There are several types of software testing that you can execute with Docker containers:

* Unit tests: These are small, granular tests written by the developer to test individual functions in the code. In Docker, unit tests are run directly on your codebase before the Docker image is built, ensuring the code is working as expected before being packaged.
* Integration tests: These refer to testing an application or microservice in conjunction with the other services on which it relies. In a Dockerized environment, integration tests are run after the docker image is built and the container is running, testing how different components operate together inside the Docker container. 
* End-to-end (E2E) tests: This type of testing simulates the behavior of a real user (e.g., by opening the browser and navigating through several pages). E2E tests are run against the fully deployed docker container, checking that the entire application stack with its various components and services functions correctly as a whole.
* Performance tests: This type of testing identifies bottlenecks. Performance tests are run against the fully deployed Docker container and test various stresses and loads to ensure the application performs at expectations. 

Docker makes it easy to set up and tear down tests in a repeatable and predictable way. Testing Docker containers ensures the reliability, stability, and quality of the application running within them. By testing containers, you can discover bugs and compatibility and performance issues to ensure your application functions as intended.



## How to test a Docker container 

Automated testing often requires supplying configuration files, data files, and test tools to the application you want to test, which unfortunately increases the size of your container. Instead, you can build a container just for testing, using your output artifact as a base image. Let’s take a look at an example: 

Let’s say a Python application uses pytest as a unit testing framework and Sphix to generate documentation. You can reuse your application container and build a new image that includes the tools on top.

```
FROM myapp:latest

RUN pip install pytest pydoc

WORKDIR /opt/myapp

CMD pytest .
```

This part of the code shows that you have a container that has both the application and the test framework in it. Now it’s time for you to run the test according to the framework you chose:

```
docker run -it myapp:test
```

You can mount data files for input or configuration as a volume when you create your test container:

``` 
docker run -it -v ./testdata:/data myapp:test 
```

What should you do if your test fails? Hopefully it won’t, but if it does, don’t worry! You can troubleshoot it. First, open the shell inside the failed container and see if you can identify the problem. If the container is still running, use the docker exec command and the container ID:

```
docker exec -it c47da2b409a1 /bin/sh
```

If you get an error running the above command, that means the container exited. You can restart the container and then try again:

```
docker start c47da2b409a1

docker exec -it c47da2b409a1 /bin/sh
```

Sometimes the container is built with automatic health checks, and Docker might terminate the container before you can investigate the issue. If this happens, you can disable the health checks in your test container by adding the command **HEALTHCHECK NONE** to the Dockerfile.

If you run into this type of troubleshooting often, there are tools you can add to the Dockerfile so they’re always available. A couple of examples include:

* jq: This is for examining JSON files.
* curl, httpie, netcat: These are for testing network services.

If you want to add these tools to your test container, add it using the line below in bold:

```
FROM myapp:latest

RUN apt update && apt install -y jq curl netcat

RUN pip install pytest pydoc

WORKDIR /opt/myapp

CMD pytest .
```

**Pro tip:** You can never have too many automated tests. At a minimum, a good test suite will include both unit tests and integration tests.



## Key takeaways

Running tests for your build artifacts and Docker containers helps ensure the reliability, stability, and quality of your work. You can never run too many tests. Tests are designed to catch bugs, identify compatibility issues, and find performance problems to assist in ensuring the application runs as intended.
