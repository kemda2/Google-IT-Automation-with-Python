# Course 6x1 Manipulating Images

# Course introduction

Hello, and welcome to the last course of this program!

Throughout this program, you've had the opportunity to learn and practice lots of different tools and techniques for creating and maintaining automation. You've learned how to write programs in Python, how to interact with files and processes from your Python scripts, how to track the history of your changes using Git, how to understand what's happening when the automation doesn't work as expected, and how to automate your infrastructure by using tools like Puppet. Phew, that’s a lot!

This last course will give you the opportunity to put all this new knowledge in action. You'll be given a bunch of small projects based on real-life scenarios, and you'll use Python to write the automation that will solve the challenges.

Working on these projects will give you the opportunity to start building your programming portfolio. When you’re done with each of them, you can upload the code you write to GitHub to show off your skills!

Since this course builds on top of everything taught in the other courses, you need to have working knowledge of the main concepts we covered: coding in Python, interacting with files and processes, using Git, using the Linux command line, troubleshooting problems, and working with Cloud infrastructure.

Throughout the course, we'll give you an introduction to the tools and techniques necessary for solving each of the projects. We recommend that you follow along by coding on your own computer. Coming up with your own exercises and practicing using the tools that you learn is the best way to master them.

One final note. As you probably noticed, this is a reading and not a video. :) This course is composed of readings that guide you along the path of using Python to solve real-life problems, along with labs that let you put that knowledge in action. We hope you enjoy the challenges and the new skills you gain along the way.

<br> 

*** 

<br>

# Module 1 Introduction

Hi! And welcome to the last course of this program.  

This module will help you put to practice some of your newly acquired Python skills. You'll make use of interesting Python libraries, understand how to read their APIs, and learn how to use the Python Imaging Library (PIL).

By the end of this module, you'll build a program that automatically resizes and rotates a bunch of images, and converts them from one image format to another.

<br> 

*** 

<br>

# Distributed systems

A distributed system is a collection of software components that are designed to work together even though they’re on separate servers.

Distributed systems, also referred to as distributed computing or distributed databases, utilize different nodes to interact and synchronize over a shared network. These nodes can also represent independent software processes or other recursive encapsulated systems. They often represent independent physical hardware items as well, such as servers. Distributed systems work to eliminate system bottlenecks and single points of failure.

A common example of a distributed system would be a website that contains:

- Presentation logic – responsible for displaying the user interface and handling user interactions
    
- Business logic – manages the application's rules and processes, ensuring proper data handling and functionality
    
- Database engine – stores and retrieves data used by the website
    
- Web server – serves as the intermediary between the user's browser and the various components
    

All of these items could be run on a single server, but it is common to run each component on separate servers for redundancy and fault tolerance.

## Key characteristics of a distributed system:

Distributed computing systems have the following characteristics:

- Resource sharing – A distributed system may share hardware, software, or data
    
- Error detection – Errors and inefficiencies can be more easily detected
    
- Transparency – A node in the system can interact and communicate with other nodes
    
- Simultaneous processing – The same function can be processed by multiple machines at once
    
- Scalability – If more machines are added, the computation and processing power can increase as needed
    
- Heterogeneity - The majority of distributed systems have asynchronous nodes and components that use various operating systems, middleware, software, and hardware which make it possible to expand or add new components
    

Distributed systems are used in various applications and scenarios, including cloud computing, web services, peer-to-peer networks, content delivery networks (CDNs), grid computing, and more. They enable organizations to harness the power of multiple machines and locations to achieve high performance, fault tolerance, and scalability in their computing environments. However, designing and managing distributed systems can be complex, requiring careful consideration of communication protocols, data consistency, and fault-tolerant strategies. Let’s take a look at the advantages and disadvantages of using a distributed system.

## Advantages of a distributed system

Distributed computing systems have the following advantages:

- **Flexibility** - You can tune the characteristics of each server to the component that it will be hosting. For example, an application server might need more memory or CPU; a database server needs more disk and I/O throughput.
    
- **Large volume** - You can run multiple copies of components for fault tolerance or to handle higher amounts of traffic. 
    
- **Redundancy of nodes** - A distributed system's nodes provide redundancy so that if one fails, there are other nodes available to step in and take its place. 
    
- **Fault tolerance** - By lowering the risks associated with having a single point of failure, distributed systems improve dependability and fault tolerance.
    

## Disadvantages of a distributed system

Distributed computing systems have the following disadvantages:

- **Increased complexity** - Compared to conventional computer environments, distributed systems are more difficult to design, administer, and comprehend.
    
- **Extra work** - Components have to do some extra work to find each other. 
    
- **Potential introduction of new problems** - Network problems could introduce a new point of failure into your application.
    
- **Potential introduction of delays** - The network could also introduce some delays.
    
- **Increased costs** - In contrast to centralized systems, distributed systems' scalability enables managers to quickly add more capacity as needed, which can potentially raise expenses.
    

On one hand, if you are designing an application that needs to scale, you should build in some awareness of distributed systems architecture from the beginning. You should not assume that everything is on the same server as you. Try to find some way for each component to discover the others (anything from a configuration file, to a service catalog, to a full service mesh). On the other hand, don’t overcomplicate things before you need to. Overcomplicated designs can be fragile and hard to maintain in the long term.

## Key takeaways

Distributed systems are crucial in various applications, but require careful design and management to address their complexities and potential challenges.  

- **Definition of distributed systems** - A distributed system is a collection of software components that collaborate across separate servers or nodes, often using a shared network. These systems aim to eliminate bottlenecks and single points of failure by distributing tasks and functions across multiple components.
    
- **Characteristics of distributed systems** - Distributed computing systems exhibit several key characteristics, including resource sharing, error detection, transparency, simultaneous processing, scalability, and heterogeneity.
    
- **Advantages and disadvantages** - Distributed systems offer advantages such as flexibility, handling large volumes of traffic, redundancy of nodes, and fault tolerance. However, they also come with disadvantages like increased complexity, the need for extra work to locate components, potential introduction of new problems and delays due to network issues, and increased costs associated with scalability.

<br> 

*** 

<br>

# NALSD

NALSD, also known as non-abstract large system design, is a discipline and a process invented by Google that aims to give SREs (site reliability engineers) the ability to assess, design, and evaluate large systems. NALSD is the process of designing complex and substantial systems, such as software applications, hardware systems, or even organizational structures, with a focus on practical, concrete details rather than on abstract or theoretical concepts. NALSD emphasizes the tangible and real-world aspects of system design and implementation. 

NALSD combines elements of capacity planning, component isolation, and graceful system degradation that are crucial to highly available production systems. 

## Key characteristics of NALSD

NALSD requires DevOps teams to think about scale and resilience during the design process. It separates the design process into two phases. The two phases have the following key characteristics: 

### Phase 1: Technical design

Phase 1 is an iterative process that involves multiple rounds of design and refinement. It's common to create prototypes, conduct feasibility studies, and gather feedback from stakeholders to continuously refine the technical design. In this phase, the team tries to answer two questions about the proposed design:

- Is it possible? Will the design even work?
    
- Can we do better? Can we make it faster, simpler, or cheaper?
    

### Phase 2: Scaling up

In Phase 2, the team assesses whether the system design is feasible at scale. They consider how the system will perform when subjected to significant increases in load. Scalability is essential to ensure that the system can accommodate growth without a dramatic loss of performance. What if you suddenly add a million users to the system? How will the system be able to accommodate a random increase in users?

- Is it feasible? Will it work at scale? Is it cost-effective?
    
- Is it resilient? What happens if the database goes down? 
    
- Can we do better? Are there changes or additions that we need to make?
    

## Three key goals of NALSD

Three of the key goals of NALSD are the following: 

The first is proper capacity planning. Capacity planning is understanding how to properly size each component and how to properly plan for growth. This goal involves careful monitoring, performance analysis, and prediction of growth trends to prevent resource exhaustion or over-provisioning. Capacity planning is crucial in NALSD design because it involves estimating the required resources (CPU, memory, storage, network bandwidth, etc.) to meet current and future demands.

The second is component isolation. In NALSD design, a fundamental principle is component isolation, highlighting the importance of designing each element of the system to maximize simplicity, modularity, and independence from one another. The "do one thing and do it well" philosophy encourages developers to create components that have a clear and specific purpose.

The final goal is graceful degradation. This is the idea that parts of the system should continue to work when another part fails, rather than everything failing at once. For example, in a web application, if a database server becomes unavailable, the system might switch to a read-only mode, allowing users to access existing data while blocking new updates until the database is restored.

## Google’s NALSD Workbook 

The NALSD Workbook was created by Google's SRE team. It is designed to help engineers and developers with the design and architecture of large-scale, reliable systems.

The NALSD Workbook contains valuable insights, best practices, and guidelines for designing and building complex and scalable systems that can handle high loads and remain reliable. Engineers often refer to such resources to improve their system design skills and create more robust and efficient software and infrastructure. If you're interested in learning more about large-scale system design, this workbook is a fantastic resource and can be found [here](https://static.googleusercontent.com/media/sre.google/en//static/pdf/nalsd-workbook-letter.pdf). 

## Key takeaways

Here are three key takeaways from this reading on NALSD:

- **Definition of NALSD:** NALSD, or Non-Abstract Large System Design, is a discipline and process introduced by Google, primarily aimed at empowering site reliability engineers (SREs) to assess, design, and evaluate large-scale systems. 
    
- **Two phases of NALSD:** Phase 1 involves continuous refinement through feedback, prototyping, and feasibility studies. It seeks to answer: "Is it possible?" and "Can we do better?" Phase 2 evaluates the system's feasibility and resilience at scale, considering how it will perform under significant load increases. 
    
- **Three key goals of NALSD:** Proper capacity planning, component isolation, and graceful degradation are the three goals of NALSD. These goals are in place so that the system can continue functioning even when individual parts fail.
    

As previously mentioned, if you are interested in learning more about NALSD, review Google’s [Non-Abstract Large System Design Workbook](https://static.googleusercontent.com/media/sre.google/en//static/pdf/nalsd-workbook-letter.pdf).

<br> 

*** 

<br>

# Built-In Libraries vs. External Libraries

As we covered in an earlier course, the Python Standard Library comes as part of the Python installation and includes modules for the most common tasks you can do with Python. But there's tons of other things you might want to do in your scripts, and not all of them are in the standard library. This is where external modules come into play. When developers write a Python module that they think others might find useful, they publish it in _**PyPI**_ _--_ also known as the _**Python Package Index**_ ([https://pypi.org](https://pypi.org/))_._ We can browse this repository of Python modules to find the module we need. It includes thousands of projects, which are classified by different categories, like topic, development status, and intended audience.

In this module, we’re going to be _**transforming**_ and _**converting**_ images. To do that, we'll be using a popular library for image manipulation: the _**Python Imaging Library (PIL)**_. The original PIL library hasn't been updated since 2009 and does not support Python 3. Fortunately, there's a current _fork_ of PIL called [_**Pillow**_](https://pypi.org/project/Pillow/), that properly supports Python 3 and is kept up-to-date. The Pillow library is packaged with the name **pillow**, but the module name in Python is still **PIL**.

If you try to import the PIL module on a computer that doesn't have pillow (or PIL) installed, you might get an error like this:

```
import PIL

Traceback (most recent call last):

  File "<stdin>", line 1, in <module>

ModuleNotFoundError: No module named 'PIL'
```


Okay, looks like I don't have that module yet! As we covered in an [earlier course](https://www.coursera.org/learn/python-operating-system/lecture/NxUXx/getting-your-computer-ready-for-python), there are several ways to add external modules to your Python environment. PIL is a pretty common library, and on Linux it’s usually available as a native package. For example:


```
user@ubuntu:~$ sudo apt install python3-pil

Reading package lists... Done

Building dependency tree     

(...)

Unpacking python3-pil:amd64 (4.3.0-2) ...

Setting up python3-pil:amd64 (4.3.0-2) ...
```

For other environments, you should use Python's package installer, _**pip3**_. Like this:

```
$ pip3 install pillow

Collecting pillow

  Downloading https://files.pythonhosted.org/packages/85/28/2c72ba965b52884a0bd71e419761fc162763dc2e5d9bec2f3b1949f7272a/Pillow-6.2.1-cp37-cp37m-macosx_10_6_intel.whl (3.9MB)

     |████████████████████████████████| 3.9MB 1.7MB/s

Installing collected packages: pillow

Successfully installed pillow-6.2.1
```

Once we've done that, we can try to import the module again. And this time it should succeed with no errors:

```
import PIL
```

That's better!

Now, how do you learn to use a library that you’ve never worked with before? It's time to get familiar with the library's _**Application Programming Interface (API)**_!

<br> 

*** 

<br>

# What is an API?

Application Programming Interfaces (APIs) help different pieces of software talk to each other. When you write a program, you typically use a bunch of existing libraries for the programming language of your choice. These libraries provide APIs in the form of _**external**_ or _**public**_ functions, classes, and methods that other code can use to get their job done without having to create a lot of repeated code.

And not only that, APIs can also be used by other pieces of software, even if they were written in a completely different programming language. For example, Cloud services use APIs that your programs can communicate with by making web calls. What’s special about an API? What makes it different to any other function that you would write in your own code?

If you look at the library's code, you’ll find it has many functions that we're not meant to use directly from our code. These _**internal**_ or _**private**_ functions, classes, and methods do important work, but they’re there to support the functions that are published by the library. You probably don't have time to dig in to understand every little bit of how the code works, but you need to know how to interact with the library to do useful work. An API is sort of like a promise. Even if the library's internal code changes, you expect the function to keep accepting the same parameters and returning the same results. That provides a stable _**interface**_ to write your code with. That's an API!

Library authors are free to make improvements and changes to the code _behind_ the interface, but they shouldn't make changes to the way the functions are called or the results they provide. Because this would break the code that depends on that library. When a library author needs to make a _**breaking change**_ to an API, then they need to have a plan in place for communicating that change to their users. That's why [breaking changes _should_ be saved for major version increments of a library](https://semver.org/#summary).

When you choose a certain library to use with your code, the first step is to get familiar with its API. You'll need to look at how the functions are called, what inputs they expect, and what outputs they'll return.

<br> 

*** 

<br>

# How to Make Sense of an API?

How do you learn to use a library or an API that you’ve never worked with before? It might take you a bit of time to familiarize yourself with how the library operates, but that's okay. It's worth spending some time understanding the way the functions are organized, the inputs and outputs, and the general expectations of the library.

In general, a good API should be descriptive. You should be able to look at a function's name and have a pretty good idea of what it will do. A well-designed API will follow patterns and _**naming conventions**_. That means that the functions, classes and methods should have names that help you understand what to expect from them. And when the name isn’t enough, you should have access to the documentation for each of the functions that will help you figure out what they do.

For example, when we visit the [reference page for the Image object](https://pillow.readthedocs.io/en/stable/reference/Image.html) in Pillow, we see this piece of example code:

```
from PIL import Image

im = Image.open("bride.jpg")

im.rotate(45).show()
```

This piece of code is pretty straightforward. Even without having seen this library before, you can probably guess that it opens an image called bride.jpg, rotates it 45 degrees, and then shows it on the screen.

But how can we know for sure? We can look up each of the functions in the documentation and check what they’re supposed to do. When dealing with open-source libraries, we can even check out how the function is implemented to see if it matches our expectations. For a web service API or a closed-source library, you might not have access to the underlying code, but you should have access to the documentation that’s generated by the code.

For a Python library like PIL, the code is documented using _**docstrings**_. If you remember from waaaay back in our first course, docstrings are documentation that lives alongside the code. You've been using them ever since! When you use “help()” to describe a function, or read a description of what a Python function does in your IDE, what you’re reading comes from docstrings in the code.

For example, let's take a look at the documentation for PIL:


```
help(PIL)

Help on package PIL:

NAME
    PIL - Pillow (Fork of the Python Imaging Library)

DESCRIPTION
    Pillow is the friendly PIL fork by Alex Clark and Contributors.
        https://github.com/python-pillow/Pillow/

    Pillow is forked from PIL 1.1.7.

    PIL is the Python Imaging Library by Fredrik Lundh and Contributors.
    Copyright (c) 1999 by Secret Labs AB.

    Use PIL.__version__ for this Pillow version.
    PIL.VERSION is the old PIL version and will be removed in the future.

    ;-)

PACKAGE CONTENTS
    BdfFontFile
    BlpImagePlugin
    BmpImagePlugin
    BufrStubImagePlugin
    ContainerIO
    CurImagePlugin
    DcxImagePlugin
    DdsImagePlugin
    EpsImagePlugin
...
```

Lots of Python modules also publish their documentation online. Pillow's full documentation is published [here](https://pillow.readthedocs.io/). There, the docstrings have been compiled into a browsable reference, and they’ve also written [a handbook](https://pillow.readthedocs.io/en/stable/handbook/index.html) [with tutorials](https://pillow.readthedocs.io/en/stable/handbook/tutorial.html) for you to get familiar with the library's API. Woohoo!

<br> 

*** 

<br>

# Generate and manage containers

## Generating image containers

Up until now, you have been working with prepackaged container images. Now, it’s time to build your own.

To [build a container image](https://docs.docker.com/get-started/02_our_app/), you create a Dockerfile, which contains step-by-step instructions for Docker to package your application along with all its dependencies.

## Choose a base image

One important step is [deciding which base image to use](https://pythonspeed.com/articles/base-image-python-docker-images/). The base image provides all the operating system files inside the container; it’s a bit like trying to choose between different Linux distributions. The best base images provide just what your application needs to run, without a lot of extra bloat, such as extra command line tools, libraries, drivers, etc.

Here are some of the most popular base images:

- [Debian](https://hub.docker.com/_/debian) and [Ubuntu](https://hub.docker.com/_/ubuntu): containers that boot into a full-featured, general Linux environment 
    
- [Alpine Linux](https://hub.docker.com/_/alpine): a stripped-down image designed to result in small, fast containers
    
- [Python](https://hub.docker.com/_/python/): great for running Python apps
    

The base images make good use of tags to provide lots of choices. For example, you can choose among several versions of Debian or Ubuntu by providing the right tag. The Python base image not only includes every Python version since 3.7, but also includes variants based on the Debian or Alpine images.

## Create a Dockerfile

Now, you can create a Dockerfile in your project directory. Again, the Dockerfile lists the steps needed to generate your container image. 

Here’s a sample Dockerfile for a Python web app that uses Flask and SQLAlchemy:

```
FROM python:3.9
WORKDIR /app
COPY requirements.txt ./
RUN pip install -r requirements.txt
COPY . .
EXPOSE 4000
CMD [ "flask", "run", "--host=0.0.0.0", "--port=4000"]
```

Here’s a line-by-line explanation of what this does:

`FROM` sets the base image to use. In this case, we are using the Python 3.9 base image.

`WORKDIR` sets the working directory inside the image.

`COPY requirements.txt ./` copies the requirements.txt file to the working directory.

`RUN pip install -r requirements.txt` installs the requirements.

`COPY` . . copies all the files in the current directory to the working directory.

`EXPOSE 4000` exposes the port 4000.

`CMD [ "flask", "run", "--host=0.0.0.0", "--port=4000"]` tells Docker to run Flask when the container starts.

Your project probably already has a requirements.txt file. Here’s a minimal one that just installs Flask, SQLAlchemy, and the PyMysql driver:

```
flask
pymysql
Flask-SQLAlchemy
```
## Build a Docker image

Now that you have these files in your project directory, you can [build a Docker image](https://linuxize.com/post/how-to-build-docker-images-with-dockerfile/) with the `docker build` command. It’s important to [choose the best Docker image](https://www.techtarget.com/searchitoperations/tip/Choose-the-best-Docker-image-for-the-job-at-hand) for your specific project.

As we discussed previously in the section on containers and tags, you probably want to tag your container image. Most containers at least use tags for the version number. You do that by adding the -t option to the command. For example, you might use the following command:

`docker build -t myname/myapp:1.0 .`

In this command, “myname” is your registry username, and “myapp” is the name of your application.

This command usually produces a lot of output, as Docker downloads the base image, runs each of the commands in your Dockerfile, and tags the image.

If you plan to upload your image to a registry, you can do that by adding the `–push` option. Generally, though, you would build the container, test it, then push it to the registry in a separate step — ideally all as part of a CI/CD pipeline.

### Pro tip

Docker images are built from layers. You’ll notice that Docker adds a layer to the image for each command in your Dockerfile. Some of those layers can be quite large, if many files were changed from the previous layer. A common trick is to clean up at the end of a command that creates a bunch of temporary files.

## Manage images

When you’ve built your image, you can use it to start a container:

```
docker run -p 4000:4000 myname/myapp:1.0
```

In the above command, `myname/myapp:1.0` is the image you built earlier. The -p argument forwards port 4000 on the host to the webserver on port 4000 inside the container. (Note that it matches the `--port=4000` argument we included in the Dockerfile earlier.)

After you’ve been building containers for a while, you’re going to build up a lot of old, stale, or half-built images. To see what images are sitting around taking up hard drive space, you can use the ls command:

```
docker image ls -a
```

You can remove the unused images (images that are not associated with any container) with the `prune` command.

```
docker image prune
```

As mentioned in the section on generating images, you can also `push` your image to a repository like DockerHub:

```
docker image push myname/myapp:1.0
```

## Key takeaways

Developers choose to containerize their applications for several reasons, as containerization offers various benefits that make the development, deployment, and management of applications more efficient and scalable.

<br> 

*** 

<br>

# Generate and manage containers: VS Studio & Docker

Virtual Studio (VS) Code provides an [optional extension](https://code.visualstudio.com/docs/containers/overview) that integrates with Docker, making it possible to [build and manage container images](https://code.visualstudio.com/docs/devcontainers/containers) right inside the integrated development environment (IDE).

## Build a container using VS Code and Docker

**Prerequisites:** You have already installed VS Code in Course 1 and Docker Desktop in Course 4.

[Steps to install:](https://learn.microsoft.com/en-us/visualstudio/docker/tutorials/docker-tutorial)

1. In the VS Code menu, select View > Extensions.
    
2. Search for “docker.”
    
3. Install the verified Docker extension from Microsoft.
    

**When you’ve installed Docker**, the extension adds a number of helpful features to VS Code. These include:

- Autocompletion and syntax highlighting when you’re editing a Dockerfile
    
- Scanning your Dockerfile for potential problems
    
- Commands to quickly generate Dockerfile and Compose file templates
    
- A new “Docker view” that shows containers and images on your machine and allows you to start and stop containers, launch a shell inside a container, and inspect the files in a running container
    
- Connections to DockerHub and other registries, allowing you to publish images by dragging and dropping them
    
- Debugging code inside a running container
    
- Access to pretty much every Docker command from the Command Palette
    

## DevContainer option

Microsoft supports  a new open-source standard called DevContainer that extends the use of Docker in the development cycle. Rather than build your container every time you want to test it, with DevContainer, you can actually develop and debug your code inside a container.

DevContainer is also compatible with GitHub Codespaces, which means you can run your IDE in the cloud. Instead of spending time setting up your local development environment just right, you can add a devcontainer.json file to your Git repository and develop in the cloud with a development environment that is fully version controlled.

You can read more about DevContainer [here](https://code.visualstudio.com/docs/devcontainers/containers)

## Key takeaways

VS Code's integration with Docker simplifies the process of container creation, orchestration, and management, enabling developers to build, test, and deploy applications more efficiently. Containers offer a consistent and isolated environment for development, eliminating the “it works on my machine” problem and ensuring seamless collaboration across teams.

<br> 

*** 

<br>

# How to Use PIL for Working With Images

As we've mentioned, for the project in this module, you'll use the Python Imaging Library to process a bunch of images. So, how does that work?

When using PIL, we typically create **Image** objects that hold the data associated with the images that we want to process. On these objects, we operate by calling different methods that either return a new image object or modify the data in the image, and then end up saving the result in a different file.

For example, if we wanted to resize an image and save the new image with a new name, we could do it with:

```
from PIL import Image
im = Image.open("example.jpg")
new_im = im.resize((640,480))
new_im.save("example_resized.jpg")
```

In this case, we're using the resize method that returns a new image with the new size, and then we save it into a different file. Or, if we want to rotate an image, we can use code like this:

```
from PIL import Image
im = Image.open("example.jpg")
new_im = im.resize((640,480))
new_im.save("example_resized.jpg")
```

This method also returns a new image that we can then use to create the new rotated file. Because the methods return a new object, we can even combine these operations into just one line that rotates, resizes, and saves:

```
from PIL import Image
im = Image.open("example.jpg")
im.rotate(180).resize((640,480)).save("flipped_and_resized.jpg")
```

There's a ton more that you can do with the PIL library. Have a look at [the docs](https://pillow.readthedocs.io/en/stable/handbook/tutorial.html) and try it on your computer!

<br> 

*** 

<br>

# Project Problem Statement

To complete this module, you'll need to write a script that processes a bunch of images. It turns out that your company is in the process of updating its website, and a design contractor has been hired to create some new icon graphics for the site. However, the contractor has delivered the final designs and they’re in the wrong format, rotated 90° and too large. You’re unable to get in contact with the designers and your own deadline is approaching fast. You’ll need to use Python to get these images ready for launch!

So, how will you do this? You'll need to go through a folder full of images and operate with each of them. On each image, you'll use PIL methods like the ones we saw in the examples, and then write the new images in the right place.

If this sounds tricky, don't panic! You've already seen everything you need to do this, and now it's time to put it into practice.

As in the previous courses, the assessment will be done on a Virtual Machine running in the Cloud, thanks to the Qwiklabs infrastructure. You'll only have access to the VM for a limited amount of time, so we recommend that you write the script locally in your computer first, and only start the lab once your script is working correctly.

Good luck, you've got this!

<br> 

*** 

<br>

# Glossary terms from course 6, module 1

## **Terms and definitions from Course 6, Module 1**

**Distributed systems:** Also referred to as distributed computing or distributed databases, utilize different nodes to interact and synchronize over a shared network

**Docstrings:** Documentation that lives alongside the code

**NALSD (Non-Abstract Large System Design):** A discipline and process introduced by Google, primarily aimed at empowering site reliability engineers (SREs) to assess, design, and evaluate large-scale systems

**Naming conventions**: Functions, classes and methods with naming conventions to understand what to expect from them

<br> 

*** 

<br>

# Course 6x2 Interacting with Web Services

# Module 2 Introduction

Congratulations on making it through the first lab in this course!

Remember that putting your Python skills to practice with exercises like this one is the way to getting the hang of it all. By practicing solving complex challenges, you'll become a lot more confident in your programming abilities, and you'll be able to achieve a lot more.

In this module, we'll look into a bunch of different tools that can be really useful in today's IT world. You'll first learn how you can use different text formats to store data in text files, retrieve it, and even transmit it over the internet.

Later on, we'll look into how we can get our code to interact with services running on different computers using a module called Python Requests.

We'll see a bunch of different examples and give you pointers to more information. Don't forget that the best way to get comfortable with all these modules and libraries is to come up with your own examples and practice writing scripts on your local computer!

<br> 

*** 

<br>

# Web Applications and Services

A _**web application**_ is an application that you interact with over HTTP. Most of the time when you’re using a website on the Internet, you’re interacting with a web application. So, how does this look behind the scenes?

Your web browser sends an HTTP request to a web server. Then, the web server passes the request along to the web application in charge of deciding what information to show you. The application then generates the website content (in HTML format). The application is also in charge of serving images and any other necessary data so that your web browser can render the website on your computer.

Lots of web applications also have APIs that you can use from your scripts! Web applications that have an API are also known as _**web services**_. Instead of browsing to a web page to type and click around, you can use your program to send a message known as an _**API call**_ to the web service. The part of the program that listens on the network for API calls is called an _**API endpoint**_.

When you interact with a web service like this, you don't even care what language the other application is using. You interact with it using a specified protocol, and the only important constraint is that both the service and your program know how to use this protocol.

So, how does that work? That's coming up!

<br> 

*** 

<br>

# RESTful APIs

**RESTful APIs** were originally conceptualized by Roy Thomas Fielding in his 2000 PhD thesis. Unlike APIs which directly open up ports to the entire internet and directly connect, RESTful APIs rely on the HTTP protocol. The HTTP protocol, in turn, can be further secured using HTTPS, and API endpoints can authenticate users via authorization tokens, API keys, or other security mechanisms. RESTful APIs use HTTP requests to perform CRUD (create, read, update, delete) operations on resources.

## RESTful methods

RESTful APIs work by associating methods (functions) with resources. Some of the most commonly used [HTTP request methods](https://developer.mozilla.org/en-US/docs/Web/HTTP/Methods) are:

- [GET](https://developer.mozilla.org/en-US/docs/Web/HTTP/Methods/GET): The GET method requests a representation of the specified resource. Requests using GET should only retrieve data.
    
- [HEAD](https://developer.mozilla.org/en-US/docs/Web/HTTP/Methods/HEAD): The HEAD method asks for a response identical to a GET request, but without the response body.
    
- [POST](https://developer.mozilla.org/en-US/docs/Web/HTTP/Methods/POST): The POST method submits an entity to the specified resource, often causing a change in state or side effects on the server.
    
- [PUT](https://developer.mozilla.org/en-US/docs/Web/HTTP/Methods/PUT): The PUT method replaces all current representations of the target resource with the request payload.
    

You can use GET to obtain information (called a “request”) from a RESTful API endpoint, which would deliver a replay from the endpoint (called a “response”). Each type of response has a three-digit code associated with it; these are [HTTP response codes](https://developer.mozilla.org/en-US/docs/Web/HTTP/Status). You might already be familiar with a 404 (not found) response. If a request succeeds, the response status code is 200, and the response will contain a message payload, typically JSON (JavaScript Object Notation). It is important to note that RESTful APIs almost always use JSON, but RESTful APIs can also be used to send and receive files, as well as stream data. 

## JSON

JSON is a data-interchange format used in RESTful APIs to facilitate communication between clients and servers. In RESTful services, JSON serves as the standard payload format for transmitting data. When a client makes a request, the server processes it and sends back a response, often in JSON format. This structured format allows for easy parsing, ensuring both the server and client can interpret the data consistently. With its key-value pairs, JSON is both human readable and machine friendly, making it a popular choice for web-based APIs.

## Additional protection

Another important thing to note is that RESTful APIs provide a layer of protection over existing cloud assets, such as a database. Instead of allowing the entire internet to query your database, you can put an API in front of it and allow the API to serve as an intermediary: an endpoint associated with that resource. You can then force authentication using a JavaScript Web Token (JWT) or a third-party authentication provider. This layer of protection not only provides security, but it also separates control logic from data, so that rate-limiting, usage analytics, and caching can be added on top to improve quality of service.

## Compatibility 

Lastly, RESTful APIs are callable from any programming language that can support HTTP or HTTPS. This includes Python but also C#, JavaScript, Swift, Go, and many others. RESTful APIs, relying on only HTTP, allow any modern computers to talk to each other. 

## Key takeaways

RESTful APIs are a fundamental and versatile part of web development. Knowing how to design, consume, and work with them is essential for building modern web applications, ensuring they can communicate effectively with other services.

<br> 

*** 

<br>

# What is REST architecture?

REST stands for Representational State Transfer. REST architecture is an architectural style for designing networked applications and web services. It was invented as a standard way for clients and servers to communicate with each other over the internet. 

REST is designed to be stateless, meaning the server does not have to remember any information about the client between requests. Every request carries all the parameters and data needed for the server to satisfy that request.

## Constraints with the REST architecture

The six constraints or principles of REST each serve a specific purpose in guiding the design of RESTful systems, contributing to the overall scalability, simplicity, and interoperability of the architecture. The six constraints are:

- **Uniform interface** - There should be consistent methods for clients to access and change resources on the server using standard HTTP (Hypertext Transfer Protocol) conventions. 
    
- **Stateless** - Every piece of information the server requires to process the request should be within the request. There shouldn't be any leftover information on the server between requests.
    
- **Cacheable** - Every server response should indicate whether the data can be cached on the client and the length of time is needed to cache the data.
    
- **Client-server** - The client and server can evolve independently. The REST interface serves as a “contract” between them.
    
- **Layered system** - An application should be split into layers. Each layer of the application handles a particular concern (data access, business logic, presentation, etc) and acts independently from the other layers.
    
- **Code on demand (optional)** - Servers can also provide code to be executed on the client. This enables the client to change its behavior dynamically.

## HTTP protocol with REST

REST is also designed to run on top of HTTP. This design enables clients and servers to communicate over the public internet using standard HTTP conventions. Companies will often publish their REST API (Application Programing Interface) so that developers can make use of it. Nearly any programming language is capable of speaking HTTP, so you can use your favorite language, like Python, to make REST API calls.

All interaction between client and server takes place over HTTP, using standard HTTP features: verbs, headers, and data payloads. Almost everything the server needs to know is included in the request URL itself. 

For example, a photo-sharing app might send a series of HTTP requests to a REST API server that look like the following (command is listed first and then the action the command is performing is listed after the dash):

- GET /api/v1/albums - get the list of photo albums
    
- GET /api/v1/albums/1234/pictures - get the list of pictures in album 1234
    
- GET /api/v1/pictures/5678 - get the details for picture 5678
    
- GET /api/v1/pictures/5678/comments

- get the comments for picture 5678
    

HTTP allows clients to GET, PUT, and DELETE resources. Clients can also POST queries with complex data, such as performing a search or transferring money between accounts. The PATCH verb allows clients to update a resource by just sending what has changed.

REST APIs often allow the client to adjust their behavior by sending additional headers with the request. Headers might include authentication, enable optional features, or allow the client to request that the server send data in specific formats (e.g. JavaScript Object Notation, JSON, or eXtensible Markup Language).

The client may send data in the body of its request, and the server replies with data in the response body. The format of the data is controlled by a header (see above).

## What is the Richardson Maturity Model?

The Richardson Maturity Model, also known as RMM, is a framework that categorizes and describes different levels of implementation for RESTful APIs based on their adherence to the six constraints referenced earlier in this reading. RMM is a way of assessing the sophistication of a REST API based on how compliant it is with the REST constraints. 

The Richardson Maturity Model consists of four levels, each representing a progressive level of adherence to the principles of REST:

- **Level 0** - A single URI (uniform resource identifier) and a single verb (usually GET or POST)
    
- **Level 1** - Multiple URIs but still a single verb
    
- **Level 2** - Makes use of URIs and multiple methods, but is not HATEOAS (Hypermedia as the Engine of Application State)
    
- **Level 3** - Full HATEOAS
    

HATEOAS indicates that the server’s responses should include hyperlinks for the client to access related resources. For example, in the picture gallery app example above, the GET request for albums  should return a list of albums. Each album should include its name, ID, and links to retrieve album details, comments, and pictures. With a full Level 3 REST implementation, the client would not need to hardcode URIs of the resources it needs. The URIs would be discoverable from the server’s responses.

To check out some further information with how to create REST APIs in Python, check out this link [here](https://auth0.com/blog/developing-restful-apis-with-python-and-flask/). If you’re interested in further information for REST APIs with GCP, click on this link [here](https://medium.com/mdblog/creating-a-serverless-rest-api-with-gcp-32cc62188a03). 

## Key Takeaways

REST architecture is based on six key constraints, including a uniform interface for consistent interactions, statelessness for efficient communication, cacheability for improved performance, separation of client and server concerns, layered system organization, and the optional ability for servers to provide executable code to clients. REST APIs are often designed to run on top of the HTTP protocol, utilizing standard HTTP features for communication. APIs are difficult to change after they are published and being utilized. Invest the time to create clean, rational, extensible APIs right from the start.

<br> 

*** 

<br>

# Using REST APIs to access web data

Accessing web data using RESTful APIs involves a series of steps that allow clients (such as web applications or mobile apps) to communicate with servers and retrieve information. Think of APIs as a waiter at a restaurant. The waiter takes orders from the customer (front end). Then, the waiter communicates the order to the kitchen workers (back end) and comes back to the customer with their meal (API response). Here are the key steps to access web data using RESTful APIs:

1. **Identify the API endpoint:** Determine the specific API endpoint or Uniform Resource Identifier (URI) that corresponds to the resource or data you want to access. The endpoint is the URL that you will send your HTTP request to.
    
2. **Select the appropriate HTTP method:** Choose the appropriate HTTP method for the action you want to perform on the resource:
    
    1. GET: Retrieve data from the resource.
        
    2. POST: Create a new resource.
        
    3. PUT: Update an existing resource or create it if it doesn't exist (replace the entire resource).
        
    4. PATCH: Partially update an existing resource.
        
    5. DELETE: Remove a resource.
        
3. **Set up request headers:** Include any necessary request headers in your HTTP request. Common headers include authentication tokens (e.g., API keys or OAuth tokens), content type, and accept headers (indicating the desired response format, such as JSON or XML).
    
4. **Prepare the request body:** For HTTP methods like POST and PUT, you may need to prepare a request body containing data to be sent to the server. The format of the request body depends on the API's documentation.
    
5. **Send the HTTP request:** Use a programming language or tool (e.g., Python's requests library, JavaScript's Fetch API, or specialized API client libraries) to send the HTTP request to the API endpoint. Include the chosen HTTP method, headers, and request body as appropriate.
    
6. **Receive the HTTP response:** The server will process your request and respond with an HTTP response. This response will include:
    
    1. Status code: Indicates the outcome of the request (e.g., 200 for success, 404 for not found, 500 for server error)
        
    2. Response headers: Contain metadata about the response
        
    3. Response body: Contains the requested data, often in a structured format like JSON or XML
        
7. **Handle the response:**
    
    1. Parse the response body to extract the data you need. The format will depend on the API's documentation and the content type header (usually JSON or XML).
        
    2. Check the status code to determine if the request was successful or if an error occurred.
        
    3. Handle errors gracefully by examining the response body or status code and providing appropriate feedback to the user.
        
8. **Implement pagination and filtering (optional):** If the API supports pagination or filtering, you can include query parameters in the URL to request specific subsets of data or control the number of records returned.
    
9. **Authentication and authorization:** Ensure that you've implemented the necessary authentication and authorization mechanisms as required by the API. This may involve including authentication tokens or credentials in your request headers.
    
10. **Error handling:** Implement error-handling logic to handle potential issues, such as network errors, invalid responses, or HTTP status codes indicating errors (e.g., 4xx and 5xx codes). Provide informative error messages to the user.
    
11. **Rate limiting (if applicable):** Respect any rate limits imposed by the API to prevent excessive requests. Implement rate-limiting strategies on your end to ensure you don't exceed the allowed request rate.
    
12. **Repeat as needed:** If you need to access more data or perform additional actions, repeat the steps with the appropriate API endpoints, methods, and parameters.
    

By following these steps, you can effectively access web data using RESTful APIs and integrate that data into your web applications or services. It's essential to refer to the API's documentation for specific details on endpoint URLs, request formats, authentication, and other requirements.

<br> 

*** 

<br>

# Python tools for REST APIs

Any programming language can use REST APIs, and of course that includes Python. Python REST API frameworks are toolkits and software libraries that offer the functions and tools needed to build RESTful APIs using the Python programming language. 

Tools for working with REST APIs in Python break down into two categories: client-side tools for consuming REST APIs and server-side frameworks for serving your own REST APIs.

## Client-side

REST API client libraries are designed to simplify calling an API and parsing the responses. You could do all of this with the low-level built-in urllib library, but these tools are designed to make the process much easier.

### Requests

Requests is a third-party Python module that you can easily download and install to simplify sending HTTP requests. It’s easy to use and has been around for a while, so it’s frequently chosen by developers. There are newer derivatives of Requests that are gaining popularity, like HTTPX and AIOHTTP. For a comparison of these three, see [HTTPX vs Requests vs AIOHTTP](https://oxylabs.io/blog/httpx-vs-requests-vs-aiohttp). 

### PycURL

As you advance as a developer, you might want to try a client library like PycURL, which offers concurrent connections and can be much faster than Requests. Note that Pycurl is more complicated to install than Requests, and it is not written in pure Python, which can make it harder to learn. 

## Server-side

On the server side, REST API frameworks are designed to make it easier for you to write, run, and debug REST services by eliminating a lot of the boilerplate code you’d need to receive HTTP requests, parse the URI, and route the request to an appropriate class or method. The most popular REST API server frameworks are Flask, Django, and FastAPI.

### Flask

Flask is a flexible and comfortable web development framework that is easy to set up and simple to use, which makes it good for beginners. Tools like template engines, for caching, and authentication help developers work quickly. But Flask handles requests sequentially, so although you can get commercial projects going fast using Flask, it isn't good for high load needs. Flask also uses third-party modules, which can make it prone to security breaches. 

Uber, Pinterest, and Twilio were all built using the Flask framework.

### Django

Django is one of the most popular frameworks worldwide. It’s a free, open-source Python framework designed for building websites of any size, with any traffic needs. Django is sturdy and efficient, particularly because it makes use of reusable code. Django is also more secure than Flask, but Django software is much more unwieldy to work with. Developers may find Django slow because of the need to employ reusable modules and the need to check compatibility against previous versions. 

YouTube, Instagram, Spotify, and DropBox were built with Django.

### FastAPI

FastAPI is exactly what the name says: fast. It’s an open-source, high-performing web framework for building web APIs in Python, and it includes hints similar to those in Python. The main downside of FastAPI is how new it is. The FastAPI documentation is robust, but there is not as much in the way of external materials or community for Fast API as there is for Flask and Django. 

Netflix uses FastAPI internally. 

For more on comparing these three REST API frameworks, see “[Choosing between Django, Flask, and FastAPI](https://www.section.io/engineering-education/choosing-between-django-flask-and-fastapi/)” and “[Top Python REST API Frameworks in 2023](https://www.browserstack.com/guide/top-python-rest-api-frameworks).”

## Pro tip

Nothing makes a developer complain faster than when things are messy. Start your own good habits now by making your APIs clean and consistent. Best practices include:

- Use the same name for a given parameter across multiple calls, in requests, and in responses. Don’t use room_id, RoomID, and guest_room_ID to all mean the same thing.
    
- Keep things like capitalization consistent.
    
- Pay attention to when you use GET vs. POST, etc. so you know exactly what function you are calling and what response should be expected. 
    
- Keep the RESTful design principles in mind.
    

Document your APIs and publish them. Encourage developers to experiment with them, which will encourage a robust ecosystem to blossom around your project.

REST APIs can be tricky to consume. Sometimes the responses you get don’t match the published docs. Your client should try its best to validate the responses and deal with the unexpected.

## Key takeaways

There are lots of REST API frameworks available on both the server side and the client side. These include plenty of free, open-source modules so you can get started right away learning to use these in Python. As you learn to work with REST, focus on developing good habits that will make it easier to collaborate with other developers as you progress.

<br> 

*** 

<br>

# What is Flask?

Flask is a Python library that makes it easier to create web applications and REST (Representational State Transfer) web services. Flask is a microframework that does not use an object relational manager (ORM). It is designed to be simple, providing the essentials for building web applications without imposing too many constraints or requiring a lot of boilerplate code. 

## Why use Flask?

Developers have the freedom to select their favorite design pattern, database, plugins, and other features using Flask.

Flask is great for rapid development, as most features are optional and can be brought in when you need them. Supporting WSGI (Web Server Gateway Interface) templates enable scalability and flexibility.

Flask supports building REST API servers and microservices. Flask allows developers to focus on creating the specific endpoints and functionality required for their APIs without the overhead of a larger framework. Additionally, Flask's extensive options of extensions and libraries, such as Flask-RESTful and Flask-SQLAlchemy, add to the development process for building scalable APIs and microservices.

Flask has built-in support for debugging and unit testing. Integrating unit testing and a debugger enables quick debugging and development. This debugging and testing support creates quick identification and resolution of issues during development.

Flask is trusted by large companies to build their applications. MIT, Reddit, Uber, Lyft, Zillow, Patreon, and Netflix are some examples of large corporations that use Flask. 

## An alternative to Flask

Flask is simple, but powerful. Flask is unopinionated, meaning it doesn't enforce a specific project structure or dictate how you should organize your code. This flexibility allows developers to choose the tools and libraries that best suit their projects’ needs.

It is often compared to Django, which is considered a much more heavyweight framework. Django requires more setup to start building your app, whereas Flask requires very little. Django’s motto is batteries included, meaning everything you could possibly need is included. Flask takes a more selective approach, offering optional plugins to enhance functionality. Because of this, Django has a steeper learning curve. For more information on Django and how it compares to Flask, click [here](https://hackr.io/blog/flask-vs-django).

It's important to note that Flask's simplicity and flexibility may require developers to make more decisions about project structure and components than would more opinionated frameworks. However, for developers who prefer to have more control over their applications’ architecture and components, Flask can be an excellent choice.

## Popular Flask plugins 

Some popular Flask plugins include: 

- **Flask WTF:** Create and process web forms
    
- **Flask RESTful:** Create REST API services
    
- **Flask login:**  Handles user authentication and identity
    
- **Flask debug toolbar:** Provides a handy browser toolbar to help you debug your Flask app
    

Flask has several useful plugins, so don’t reinvent the wheel. Leveraging Flask's extensive collection of plugins can significantly expedite development and enhance your application's functionality. These plugins cover a wide range of features, from authentication and form handling to database integration and caching, allowing you to tap into a large selection of pre-built solutions.

## Key takeaways

Remember three key takeaways from this reading: 

- **Flexibility and freedom:** Flask's simplistic and minimalist design offers developers the freedom to select their preferred design patterns, databases, and plugins. This flexibility allows them to tailor their web applications according to their projects’ specific requirements.
    
- **Rapid development and scalability:** Flask’s support for WSGI templates enhances scalability and flexibility, making it suitable for building REST API servers and microservices. On the other hand, Django, with its comprehensive feature set, can be slower to set up initially, but may offer advantages in terms of built-in functionality for larger, more complex projects.
    
- **Trust of large corporations:** Flask is trusted by several large companies including MIT, Reddit, Uber, Lyft, Zillow, Patreon, and Netflix, to build their applications.

<br> 

*** 

<br>

# How to use Flask

Flask is a lightweight web framework used in Python. Its ease of use for beginners interested in building web apps is the reason for its appeal. Flask can be used to build both straightforward and complex web apps for a range of purposes. Some examples of web apps that you can develop with Flask are blog apps, portfolio websites, feedback forms, and social network web apps. This reading will discuss what Flask is used for and what you can accomplish with Flask.

## How to create web applications with Flask

It's enjoyable and simple to build web applications with Flask. You must be familiar with the fundamentals of Python in order to learn Flask. In addition to Python, you should have a solid understanding of front-end principles. No expertise in front-end development is required. Understanding HTML coding is helpful when using Flask; however, knowing CSS and Javascript will help even more to improve how your app looks and functions.

```
# This is not an excutable code block
from flask import Flask
app = Flask("myapp")
@app.route('/')
def hello_world():
    `return 'Hello, World!'`
```

Next, we run the app with the flask command:

```
$ flask --app hello run
 * Serving Flask app 'hello'
 * Running on http://127.0.0.1:5000 (Press CTRL+C to quit)
```

Now, we can make our app a bit more interactive. Let’s add a parameter so the app can greet you by name:

```
from flask import Flask
app = Flask("hello")
@app.route('/hello/<name>')
def hello_world(name):
    return f'Hello, {name}!'
```

More information on this example can be found [here.](https://flask.palletsprojects.com/en/2.3.x/quickstart/) 

## Importance of following best practices

Flask is not only versatile and easy to use, but it also offers a robust framework for building web applications. Its versatility means you can use it for a wide range of projects, from small prototypes to large-scale applications. However, it's important to keep in mind that the scalability, maintainability, and security of a Flask application largely depend on how well you adhere to best practices during the development process.

One of the key best practices in Flask development is the use of blueprints to modularize your application. Blueprints allow you to organize your code into separate components, making it easier to manage and maintain as your project grows.

To boost the performance of your Flask application, consider implementing caching. Caching can significantly reduce the response time of your application by storing frequently accessed data or rendered templates in memory. This not only enhances user experience, but also minimizes server load, making your application run more efficiently. If you are interested in learning more about caching, you can find more information [here](https://flask-caching.readthedocs.io/en/latest/).

Another crucial aspect of Flask development is the secure handling of sensitive data such as API keys, database credentials, or secret tokens. Leveraging environmental variables to store such information is a recommended practice. This approach helps protect sensitive data from accidental exposure and allows you to easily switch between development, testing, and production environments without compromising security.

## Flask extensions or libraries

Flask also has a number of beneficial extensions and libraries that can help streamline the development process. The extensions, created by the Flask community and third-party developers, make it effortless to extend Flask's capabilities, allowing developers to tailor their applications to specific needs without reinventing the wheel.

Flask’s has an extensive set of libraries that you can add to extend its functionality. Some of the most popular are Flask WT Forms (WTF), Flask-SQLAlchemy, Flask RESTful, Flask Login, and Flask Debug Toolbar. To read more on popular extensions or libraries with Flask, there is a great resource [here](https://nickjanetakis.com/blog/15-useful-flask-extensions-and-libraries-that-i-use-in-every-project).

## Additional resources

Fortunately, there are extensive  Flask-related resources on the internet. For a collection of additional documents about using Flask, such as a user’s guide, click [here](https://flask.palletsprojects.com/en/2.3.x/).  An official tutorial can be found [here](https://flask.palletsprojects.com/en/2.3.x/tutorial/), and if you’re interested in a guide on how to create a web application with Flask, click [here](https://www.digitalocean.com/community/tutorials/how-to-make-a-web-application-using-flask-in-python-3).

## Key takeaways

Flask is a lightweight web framework in Python. Its simplicity and ease of use make it an attractive choice for those new to web application development. Flask involves modularizing your code using blueprints. It also can implement caching to enhance performance and secure sensitive data with environmental variables. By following these guidelines, developers can ensure the scalability, maintainability, and security of their Flask applications.

<br> 

*** 

<br>

# Data Serialization

If you have two programs that need to communicate with each other, how do you get that data from one place to another? We're going to talk about two aspects of that problem: what to send, and how to send it.

First, what do you send? When you have a conversation with another person, you don't send thoughts and memories directly between your brains. At least not yet! You first have to convert your thoughts into language, and then transmit that language to another person. They take that language, and convert it back into thoughts. It’s the same with programs running in different places, or at different times.

In a previous course, we took a list of lists in memory and wrote it to disk as a _**Comma-Separated Value (CSV)**_ file. This is one example of a technique called _**data serialization**_. Data serialization is the process of taking an in-memory data structure, like a Python object, and turning it into something that can be stored on disk or transmitted across a network. Later, the file can be read, or the network transmission can be received by another program and turned back into an object again. Turning the serialized object back into an in-memory object is called _**deserialization**_.

Data serialization is extremely useful for communicating with web services. A web service's _**API endpoint**_ takes messages in a specific format, containing specific data. By the end of this module, we'll be sending messages to web services, but for now let's concentrate on how to serialize Python objects into some common formats.

Let's start with the contact information from one of our CSV examples. We'll keep just two entries to keep our examples short, but there's no limit to how long these can be.

```
name,username,phone,department,role
Sabrina Green,sgreen,802-867-5309,IT Infrastructure,System Administrator
Eli Jones,ejones,684-3481127,IT Infrastructure,IT specialist
```

Instead of having a list of lists, we could turn this information into a list of dictionaries. In each of these dictionaries, the key will be the name of the column, and the value will be the corresponding information in each row.  It could look something like this:

```
people = [
    {
        "name": "Sabrina Green",
        "username": "sgreen",
        "phone": "802-867-5309",
        "department": "IT Infrastructure",
        "role": "Systems Administrator"
    },
    {
        "name": "Eli Jones",
        "username": "ejones",
        "phone": "684-348-1127",
        "department": "IT Infrastructure",
        "role": "IT Specialist"
    },
]
```

Using a structure like this lets us do interesting things with our information that’s much harder to do with CSV files. For example, let's say we want to record more than one phone number for each person. Instead of using a single string for "phone", we could represent that data in another dictionary, like this:

```
people = [
    {
        "name": "Sabrina Green",
        "username": "sgreen",
        "phone": {
            "office": "802-867-5309",
            "cell": "802-867-5310"
        },
        "department": "IT Infrastructure",
        "role": "Systems Administrator"
    },
    {
        "name": "Eli Jones",
        "username": "ejones",
        "phone": {
            "office": "684-348-1127"
        },
        "department": "IT Infrastructure",
        "role": "IT Specialist"
    },
]
```

Now, we can record multiple phone numbers per person, and give them descriptive names like "office" and "cell". This would be hard to store in a CSV file, because the data is not _flat_. To help us with that, there's a bunch of different formats that we can use to store our data when the structure isn't flat.

Up next, we'll look into a few of the most common ones. 

<br> 

*** 

<br>

# Data Serialization Formats

There are lots and lots of ways to serialize data. In this course, we'll cover a couple of the most common ones and we'll look into how you can use them from Python. Once you get the hang of how this works, it's super easy to use a different format if needed.

[_**JSON (JavaScript Object Notation)**_](https://json.org/) is the serialization format that we'll use the most in this course. We'll go into some details later but, for now, let's just use the **json** module to convert our **people** list of dictionaries into JSON format.

```
import json
with open('people.json', 'w') as people_json:
    json.dump(people, people_json, indent=2)
```

This code uses the **json.dump()** function to serialize the **people** object into a JSON file. The contents of the file will look something like this:

```
[
  {
    "name": "Sabrina Green",
    "username": "sgreen",
    "phone": {
      "office": "802-867-5309",
      "cell": "802-867-5310"
    },
    "department": "IT Infrastructure",
    "role": "Systems Administrator"
  },
  {
    "name": "Eli Jones",
    "username": "ejones",
    "phone": {
      "office": "684-348-1127"
    },
    "department": "IT Infrastructure",
    "role": "IT Specialist"
  },
]
```

[_**YAML (Yet Another Markup Language)**_](https://yaml.org/) has a lot in common with JSON. They’re both formats that can be easily understood by a human when looking at the contents. In this example, we’re using the **yaml.safe_dump()** method to serialize our object into YAML:

```
import yaml
with open('people.yaml', 'w') as people_yaml:
    yaml.safe_dump(people, people_yaml)
```

That code will generate a **people.yaml** file that looks like this:

```
- department: IT Infrastructure
  name: Sabrina Green
  phone:
    cell: 802-867-5310
    office: 802-867-5309
  role: Systems Administrator
  username: sgreen
- department: IT Infrastructure
  name: Eli Jones
  phone:
    office: 684-348-1127
  role: IT Specialist
  username: ejones
```

While this doesn't look exactly like the JSON example above, both formats list the names of the fields as part of the format, so that both the programs _parsing_ the data and the humans looking at it can make sense out of it. The main difference is how these formats are used. JSON is used frequently for transmitting data between web services, while YAML is used the most for storing configuration values.

These are just a couple of the most common data serialization formats. We've left out some other pretty common ones like [_**Python pickle**_](https://docs.python.org/3/library/pickle.html), [_**Protocol Buffers**_](https://developers.google.com/protocol-buffers), or the [_**eXtensible Markup Language (XML)**_](https://www.w3.org/XML/). Each of them is useful in a specific context, although not the focus of this course. You can read more about them by following those links.

<br> 

*** 

<br>

# More About JSON

Alright, we've seen a couple of different serialization formats. Let's now dive into more details about [_**JSON (JavaScript Object Notation)**_](https://json.org/), which you'll be using in the lab at the end of this module.

As we mentioned before, JSON is _**human-readable**_, which means it’s encoded using printable characters, and formatted in a way that a human can understand. This doesn't necessarily mean that you _will_ understand it when you look at it, but you _can_.

Lots of web services send messages back and forth using JSON. In this module, and in future ones, you’ll serialize JSON messages to send to a web service.

JSON supports a few _**elements**_ of different data types. These are very basic data types; they represent the most common basic data types supported by any programming language that you might use.

JSON has _**strings,**_ which are enclosed in quotes.

```
"Sabrina Green"
```

It also has _**numbers,**_ which are not.

```
1002
```

JSON has _**objects**_, which are key-value pair structures like Python dictionaries.



```
{
  "name": "Sabrina Green",
  "username": "sgreen",
  "uid": 1002
}
```

And a key-value pair can contain another object as a value.

```
{
  "name": "Sabrina Green",
  "username": "sgreen",
  "uid": 1002,
  "phone": {
    "office": "802-867-5309",
    "cell": "802-867-5310"
  }
}
```

JSON has _**arrays**_, which are equivalent to Python lists. Arrays can contain strings, numbers, objects, or other arrays.


```
[
  "apple",
  "banana",
  12345,
  67890,
  {
    "name": "Sabrina Green",
    "username": "sgreen",
    "phone": {
      "office": "802-867-5309",
      "cell": "802-867-5310"
    },
    "department": "IT Infrastructure",
    "role": "Systems Administrator"
  }
]
```

And as you’ve probably noticed, JSON elements are always _**comma-delimited**_. With these basics under your belt, you could create valid JSON by hand, and edit examples of JSON that you encounter. Except we don't really want to do that, since it's clunky and we’re bound to make a ton of errors! Instead, let’s use the **json** library that does all the heavy lifting for us.

```
import json
```

The **json** library will help us turn Python objects into JSON, and turn JSON strings into Python objects! The **dump()** method serializes basic Python objects, writing them to a file. Like in this example:



```
import json

people = [
  {
    "name": "Sabrina Green",
    "username": "sgreen",
    "phone": {
      "office": "802-867-5309",
      "cell": "802-867-5310"
    },
    "department": "IT Infrastructure",
    "role": "Systems Administrator"
  },

  {
    "name": "Eli Jones",
    "username": "ejones",
    "phone": {
      "office": "684-348-1127"
    },
    "department": "IT Infrastructure",
    "role": "IT Specialist"
  }
]
```

with open('people.json', 'w') as people_json:

```
json.dump(people, people_json)
```

That gives us a file with a single line that looks like this:

```
[{"name": "Sabrina Green", "username": "sgreen", "phone": {"office": "802-867-5309", "cell": "802-867-5310"}, "department": "IT Infrastructure", "role": "Systems Administrator"}, {"name": "Eli Jones", "username": "ejones", "phone": {"office": "684-348-1127"}, "department": "IT Infrastructure", "role": "IT Specialist"}]
```

JSON doesn't _need_ to contain multiple lines, but it sure can be hard to read the result if it's formatted this way! Let's use the **indent** parameter for **json.dump()** to make it a bit easier to read.

```
with open('people.json', 'w') as people_json:

    json.dump(people, people_json, indent=2)
```

The resulting file should look like this:

```
[

  {

    "name": "Sabrina Green",

    "username": "sgreen",

    "phone": {

      "office": "802-867-5309",

      "cell": "802-867-5310"

    },

    "department": "IT Infrastructure",

    "role": "Systems Administrator"

  },

  {

    "name": "Eli Jones",

    "username": "ejones",

    "phone": {

      "office": "684-348-1127"

    },

    "department": "IT Infrastructure",

    "role": "IT Specialist"

  }

]
```

Now it’s much easier to follow! In fact, it looks very similar to how you’d write out the object in Python. Cool!

Another option is to use the **dumps()** method, which also serializes Python objects, but returns a string instead of writing directly to a file.



```
>>> import json

>>> 

>>> people = [

...   {

...     "name": "Sabrina Green",

...     "username": "sgreen",

...     "phone": {

...       "office": "802-867-5309",

...       "cell": "802-867-5310"

...     },

...     "department": "IT Infrastructure",

...     "role": "Systems Administrator"

...   },

...   {

...     "name": "Eli Jones",

...     "username": "ejones",

...     "phone": {

...       "office": "684-348-1127"

...     },

...     "department": "IT Infrastructure",

...     "role": "IT Specialist"

...   }

... ]

>>> people_json = json.dumps(people)

>>> print(people_json)

[{"name": "Sabrina Green", "username": "sgreen", "phone": {"office": "802-867-5309", "cell": "802-867-5310"}, "department": "IT Infrastructure", "role": "Systems Administrator"}, {"name": "Eli Jones", "username": "ejones", "phone": {"office": "684-348-1127"}, "department": "IT Infrastructure", "role": "IT Specialist"}]
```

The **load()** method does the inverse of the **dump()** method. It deserializes JSON from a file into basic Python objects. The **loads()** method also deserializes JSON into basic Python objects, but parses a string instead of a file.

```
>>> import json

>>> with open('people.json', 'r') as people_json:

...     people = json.load(people_json)

... 

>>> print(people)

[{'name': 'Sabrina Green', 'username': 'sgreen', 'phone': {'office': '802-867-5309', 'cell': '802-867-5310'}, 'department': 'IT Infrastructure', 'role': 'Systems Administrator'}, {'name': 'Eli Jones', 'username': 'ejones', 'phone': {'office': '684-348-1127'}, 'department': 'IT Infrastructure', 'role': 'IT Specialist'}, {'name': 'Melody Daniels', 'username': 'mdaniels', 'phone': {'cell': '846-687-7436'}, 'department': 'User Experience Research', 'role': 'Programmer'}, {'name': 'Charlie Rivera', 'username': 'riverac', 'phone': {'office': '698-746-3357'}, 'department': 'Development', 'role': 'Web Developer'}]
```

Remember that JSON elements can only represent simple data types. If you have complex Python objects, you won’t be able to automatically serialize them as JSON. Take a look at [this table](https://docs.python.org/3/library/json.html#py-to-json-table) to see in detail how Python objects are converted into JSON elements.

<br> 

*** 

<br>

# The Python Requests Library

Up to now, we've seen how we can serialize the data that we have in our programs and turn it into a format that we can store on disk. Once the data is stored, another process can open up those files, de-serialize them, and go from there.

This works, but only if the other process has access to the same filesystem you used to store your data. What if you wanted to send a message to another computer on another network? HTTP to the rescue!

Remember that _**HTTP (HyperText Transfer Protocol)**_ is the protocol of the world-wide web. When you visit a webpage with your web browser, the browser is making a series of _**HTTP requests**_ to web servers somewhere out on the Internet. Those servers will answer with _**HTTP responses**_. This is also how we’re going to send and receive messages with web applications from our code.

The [Python Requests library](https://requests.readthedocs.io/) makes it super easy to write programs that send and receive HTTP. Instead of having to understand the HTTP protocol in great detail, you can just make very simple HTTP connections using Python objects, and then send and receive messages using the methods of those objects. Let's look at an example:

```
>>> import requests

>>> response = requests.get('https://www.google.com')
```

That's it! That was a basic request for a web page! We used the Requests library to make a _**HTTP GET**_ request for a specific _**URL, or Uniform Resource Locator**_. The URL tells the Requests library the name of the resource (**www.google.com**) and what protocol to use to get the resource (**https://**). The result we get is an object of type [requests.Response](https://requests.readthedocs.io/en/master/api/#requests.Response).

Alright, now what did the web server respond with? Let's take a look at the first 300 characters of the [Response.text](https://requests.readthedocs.io/en/master/api/#requests.Response.text):

```
>>> print(response.text[:300])

<!doctype html><html itemscope="" itemtype="http://schema.org/WebPage" lang="de"><head><meta content="text/html; charset=UTF-8" http-equiv="Content-Type"><meta content="/images/branding/googleg/1x/googleg_standard_color_128dp.png" itemprop="image"><title>Google</title><script nonce="dZfbIAn803LDGXS9
```

Now, it might be hard for you to read the [HTML (HyperText Markup Language)](https://html.spec.whatwg.org/multipage/) that was returned in this response, but your web browser knows just how to turn that into a familiar-looking web page.

Even with this simple example, the Requests module has done a whole lot of work for us! We didn't have to write any code to find the web server, make a network connection, construct an HTTP message, wait for a response, or decode the response. Not that HTML can't be messy enough on its own, but let's look at the first bytes of the [_**raw**_](https://requests.readthedocs.io/en/master/api/#requests.Response.raw) message that we received from the server:

```
>>> response = requests.get('https://www.google.com', stream=True)

>>> print(response.raw.read()[:100])


b'\x1f\x8b\x08\x00\x00\x00\x00\x00\x02\xff\xc5Z\xdbz\x9b\xc8\x96\xbe\xcfS`\xf2\xb5-\xc6X\x02$t\xc28\xe3v\xdc\xdd\xee\xce\xa9\xb7\xdd;\xe9\x9d\xce\xf6W@\t\x88\x11`@>D\xd6\x9b\xce\xe5<\xc3\\\xcd\xc5\xfc\xab8\x08\xc9Nz\x1f.&\x8e1U\xb5j\xd5:\xfc\xb5jU\x15\x87;^\xe2\x16\xf7)\x97\x82b\x1e\x1d\x1d\xd2S'
```

What's all that? The response was _**compressed**_ with [_**gzip**_](https://www.gzip.org/), so it had to be _**decompressed**_ before we could even read the text of the HTML. One more thing that the Requests library handled for us!

The [requests.Response](https://requests.readthedocs.io/en/master/api/#requests.Response) object also contains the exact request that was created for us. We can check out the headers stored in our object to see that the Requests module told the web server that it was okay to compress the content:

```
>>> response.request.headers['Accept-Encoding']

'gzip, deflate'
```

And then the server told us that the content had actually been compressed

```
>>> response.headers['Content-Encoding']

'gzip'
```

And all this happened by default, without us having to do anything special to make it work. Amazing, right?

<br> 

*** 

<br>

# Useful Operations for Python Requests

There's a ton of things that we can do with Python Requests.  We'll cover some of the most important features here and give you pointers for more information at the end.

First, how do we know if a request we made got a successful response? You can check out the value of [_**Response.ok**_](https://requests.readthedocs.io/en/master/api/#requests.Response.ok), which will be **True** if the response was good, and **False** if it wasn't.

```
>>> response.ok

True
```

Now, keep in mind that this will only tell you if the web server says that the response successfully fulfilled the request. The response module can’t determine if that data that you got back is the kind of data that you were expecting. You'll need to do your own checking for that!

If the boolean isn’t specific enough for your needs, you can get the [HTTP response code](https://www.iana.org/assignments/http-status-codes/http-status-codes.xhtml) that was returned by looking at [Response.status_code](https://requests.readthedocs.io/en/master/api/#requests.Response.ok):

```
>>> response.status_code

200
```

Excellent! To write maintainable, stable code, you’ll always want to check your responses to make sure they succeeded before trying to process them further. For example, you could do something like this:

```
response = requests.get(url)

if not response.ok:

    raise Exception("GET failed with status code {}".format(response.status_code))
```

But you don't really need to do that. Requests has us covered here, too! We can use the [Response.raise_for_status()](https://requests.readthedocs.io/en/master/api/#requests.Response.raise_for_status) method, which will raise an **HTTPError** exception _only if_ the response wasn’t successful.

```
response = requests.get(url)

response.raise_for_status()
```

Up next, we'll look into the different types of HTTP request methods that we can make using this handy requests module.

<br> 

*** 

<br>

# HTTP GET and POST Methods

HTTP supports several [_**HTTP methods**_](https://tools.ietf.org/html/rfc7231#section-4.3), like GET, POST, PUT, and DELETE. We're going to spend time on the two most common HTTP requests: GET and POST.

The [_**HTTP GET method**_](https://tools.ietf.org/html/rfc7231#section-4.3.1), of course, retrieves or _**gets**_ the resource specified in the URL. By sending a GET request to the web server, you’re asking for the server to GET the resource for you. When you’re browsing the web, most of what you’re doing is using your web browser to issue a whole bunch of GET requests for the text, images, videos, and so forth that your browser will display to you.

A GET request can have _**parameters**_. Have you ever seen a URL that looked like this?

```
https://example.com/path/to/api/cat_pictures?search=grey+kitten&max_results=15
```

The question mark separates the URL resource from the resource's parameters. These parameters are one or more key-value pairs, formatted as a [_**query string**_](https://en.wikipedia.org/wiki/Query_string). In the example above, the **search** parameter is set to "grey+kitten", and the **max_results** parameter is set to 15.

But you don't have to write your own code to create an URL like that one. With [requests.get()](https://requests.readthedocs.io/en/master/api/#requests.get), you can provide a dictionary of parameters, and the Requests module will construct the correct URL for you!

```
>>> p = {"search": "grey kitten",

...      "max_results": 15}

>>> response = requests.get("https://example.com/path/to/api", params=p)

>>> response.request.url

'https://example.com/path/to/api?search=grey+kitten&max_results=15'
```

You might notice that using parameters in Requests is yet another form of data serialization. Query strings are handy when we want to send small bits of information, but as our data becomes more complex, it can get hard to represent it using query strings. 

An alternative in that case is using the [_**HTTP POST method**_](https://tools.ietf.org/html/rfc7231#section-4.3.3). This method sends, or _**posts**_, data to a web service. Whenever you fill a web form and press a button to submit, you're using the POST method to send that data back to the web server. This method tends to be used when there's a bunch of data to transmit.

In our scripts, a POST request looks very similar to a GET request. Instead of setting the **params** attribute, which gets turned into a query string and appended to the URL, we use the **data** attribute, which contains the data that will be sent as part of the POST request.

```
>>> p = {"description": "white kitten",

...      "name": "Snowball",

...      "age_months": 6}

>>> response = requests.post("https://example.com/path/to/api", data=p)
```

Let's check out the generated URL for this request:

```
>>> response.request.url

'https://example.com/path/to/api'
```

See how much simpler the URL is on this POST now? Where did all of the parameters go? They’re part of the _**body**_ of the HTTP message. We can see them by checking out the **body** attribute.

```
>>> response.request. body

'description=white+kitten&name=Snowball&age_months=6'
```

Ah, ha! There they are!

So, if we need to send and receive data from a web service, we can turn our data into dictionaries and then pass that as the **data** attribute of a POST request.

Today, it's super common to send and receive data specifically in JSON format, so the Requests module can do the conversion directly for us, using the **json** parameter.

```
>>> response = requests.post("https://example.com/path/to/api", json=p)

>>> response.request.url

'https://example.com/path/to/api'

>>> response.request.body

b'{"description": "white kitten", "name": "Snowball", "age_months": 6}' 
```

And that's it for our brief introduction to the Requests module. If you want to learn more, feel free to work through the [Requests Quickstart](https://requests.readthedocs.io/en/master/user/quickstart/).

In the project at the end of this module, you’ll use the Requests module to interact with a web application. This simple application was created using the Django web framework. So, what's that, exactly? Read on to learn more!

<br> 

*** 

<br>

# What is Django?

The lab project at the end of this module will feature a very simple web application created using [_**Django**_](https://djangoproject.com/). Django is a _**full-stack web framework**_ written in Python. For this project, you'll only need to interact with it through HTTP requests, but it's still a good idea to understand what it is, and when it would be a good tool for you to use.

A full-stack web framework handles a bunch of different components that are typical when creating a web application. It contains libraries that help you handle each of the pieces: writing your application's code, storing and retrieving data, receiving web requests, and responding to them. If you need to build an application that has a web frontend, using a web framework like Django can save you a lot of time and effort, because a lot of challenges are already solved for you.

Web frameworks are commonly split into three basic components: 
(1) the application code, where you'll add all of your application's logic; (2) the data storage, where you'll configure what data you want to store and how you're storing it; and (3) the web server, where you'll state which pages are served by which logic.

Splitting your code like that helps you write more modular code, promotes code reuse, and allows for flexibility when viewing and accessing data. For example, you could have a simple web page where users of the system can access the information already stored in it, and a separate programmatic interface that can be used by other scripts or applications to transmit data to the system.

When you’re writing a web application, there's a ton of little decisions to make. Relying on a framework like Django is similar to using external libraries for your code. There are a lot of features, which you can use very easily, instead of writing everything from scratch and re-making all of the same mistakes that we all make when writing a web application for the first time.

Django has a ton of useful components for building websites. In the lab project, Django will be used for serving the company website, including customer reviews. It does this by taking the request for a URL and parsing it using the _**urlresolver**_ module. This is a core module in Django that interprets URL requests and matches them against a list of defined patterns. If a URL matches a pattern, the request is passed to the associated function, called a _**view**_. This allows you to serve different pages depending on what URL is being requested. You can even build complex logic into the function handling the request to make more dynamic, interactive, and exciting pages.

Django can also handle reading and writing data from a database, letting you store and retrieve data used by your application. In the lab, the database holds the customer reviews for the company. When a user loads the website, the logic will ask the database for all available customer reviews. These are retrieved and formatted into a web page, which is served as a response to the URL request. Django makes it easy to interact with data stored in a database by using an _**object-relational mapper**_, or _**ORM**_. This tool provides an easy mapping between data models defined as Python classes and an underlying database that stores the data in question.

On top of this, the Django application running in the lab includes an _**endpoint**_ that can be used to add new customer reviews to the database. This endpoint is configured to receive data in JSON format, sent through an HTTP POST request. The data transmitted will then be stored in the database and added to the list of all reviews. The framework even generates an interactive web form, that lets us directly interact with the endpoint using our browser, which can be really handy for testing and debugging.

Django is one of many popular web frameworks. Alternative Python-based web frameworks similar to Django include [Flask](https://www.fullstackpython.com/flask.html), [Bottle](https://bottlepy.org/docs/dev/), [CherryPy](https://cherrypy.org/), and [CubicWeb](https://www.cubicweb.org/). There are a host of other frameworks written in other languages too, not just Python.

<br> 

*** 

<br>

# Project Problem Statement

To complete this module, you'll write a script that interacts with a running web service.  The web service is part of your company's website and is in charge of storing and displaying the customer reviews of the company.

The reviews are stored in text files in the local disk. Your script should open those files, process the information to turn it into the format expected by the web service, then send it to the web service to get stored.

For this lab, the service is running on the same machine, and you can actually look at how all of it is implemented, if you want.  But you don't need to change the service implementation to complete the exercise.

Remember that you can take your time to prepare the code that you’ll write. You can start the lab later on, once you have a good idea of what you'll do and how you'll do it.

Also, feel free to check out the resources that we pointed to as many times as you need.

Good luck, you've got this!

<br> 

*** 

<br>

# Glossary terms from course 6, module 2

## **Terms and definitions from Course 6, Module 2**

**API endpoint:** The part of the program that listens on the network for API calls

**Data serialization:** The process of taking an in-memory data structure, like a Python object, and turning it into something that can be stored on disk or transmitted across a network

**Flask:** A Python library that makes it easier to create web applications and REST web services

**JSON:** A data-interchange format used in RESTful APIs to facilitate communication between clients and servers

**REST (Representational State Transfer):** Every request carries all the parameters and data needed for the server to satisfy that request

**RESTful APIs:** Rely on the HTTP protocol, can be further secured using HTTPS, and API endpoints can authenticate users via authorization tokens, API keys, or other security mechanisms

**REST architecture:** An architectural style for designing networked applications and web services

**Richardson Maturity Model (RMM):** A framework that categorizes and describes different levels of implementation for RESTful APIs based on their adherence to the six constraints

**Web application:** An application that you interact with over HTTP

# Course 6x3 Automatic Output Generation

# Module 3 Introduction

Welcome back! And congratulations on completing yet another tricky lab.

As you get to practice your Python skills you're probably starting to see that there's a lot more to learn out there. And that's true, there's a lot of tools to help us do a ton of different things. But don't panic! You don't need to learn all these tools at the same time.  This course is designed to help you get a first taste of some of the tools available, so that you can learn about more tools in the future. As you keep writing more and more programs, you'll keep coming across more and more tools, expanding your Python skills and knowledge.

In this module, we'll look into a different aspect of automation: automating the generation of nicely formatted output from our scripts, like sending emails.

Most of us use email for a bunch of different things, all the time. We type up an email message, sometimes  attach a picture or a document, and send it to someone in our contact list. Have you ever used a script to send an email? By the end of this module, you’ll be able to send an email message with an attachment from Python! You'll even learn how to generate PDF files to attach to those emails.

To help with that, we'll look into a bunch of different Python modules that already include a lot of the functionalities that we want. As we've called out, this is one of the great things about Python -- we can use these modules to accomplish what we want with very little code!

We'll show examples of how you can do a bunch of different operations, like creating the contents of the email or the PDF, attaching a file to an email, and even sending the email to an SMTP server. As always, we recommend that you follow along on your own computer, and even try to come up with new ways to use these libraries.

At the end, you'll have the opportunity to put all of this in practice through the lab.

<br>

***

<br>

# Logging

Many Python programmers develop programs that require them to observe values to see what is going on by using print() statements. print() is a built-in Python function used for simple, immediate output to the console which can be used for debugging or quick information display. Logging is a more sophisticated and configurable logging framework that allows developers to control the level of detail, destination, and formatting of log messages. Logging makes it suitable for production-grade applications to track and analyze program behavior. print() statements are great for development, but for production, each one of these function calls increases overhead.

One example of print() statements causing negative overhead is if low-priority problems arise in a script. A third-party API endpoint isn’t responding in time, so the application tries again and isn’t able to get a response. In these cases, the system doesn't tell you that the system is broken.

For more severe problems, such as a totally offline server dependency or repeated denials for incorrect passwords, you want to know immediately. For your logs, you want to filter out errors that may go away due to external factors (data about outages and potential breaches). 

When logging problems occur, they generally do not happen in isolation. Having a massive amount of noise inside log files can make it hard to trace problems. This ideology is pointed out in the “Observing Application Behavior” chapter of Michal Jaworski’s book, _Expert Python Programming, 4th edition_. 

You might want to set up a way to notify someone in case problems arise. Filtering problems by severity level is a fantastic place to start. Logging allows this filtering with the levels: DEBUG, INFO, WARNING, ERROR, and CRITICAL.

## Printing vs. logging

Printing and logging are both methods you can use to display information, but they serve slightly different purposes and have different implications, depending on the context.

### Printing

print() is a function that prints objects (strings, but also most anything else). The syntax for using the print() function to print to a file is: 

print(open(“my_file.txt”,”r”).read(),file=open(“new_file.txt”,”w”))

print() objects sent to the text stream file must be provided as keyword arguments if they are separated by sep. These statements might also be followed by end. sep, end, file, and flush.

The stream file is generally what you interact with, but sometimes you will not use Python with console output, especially in a cloud context where code is deployed that runs on some other computer. In most cases, anything printed out inside the Python code will end up in logs. This is because logs capture all or nothing regarding print().

### Logging

The logging module provides an object-oriented way to print out statements with the additional advantage of using severity levels. More advanced features include the ability to filter which messages you care about, to route to more destinations than just the console/terminal, and to see the difference between normal print() statements and print() statements used for debugging purposes.

## Built-in logging levels 

The logging module provides five built-in log levels. In order of severity, they are debug, info, warning, error, and critical. These are referred to as methods of the logging object. 

The output of a logging statement will resemble:

```
[LOG_LEVEL]:root:[MESSAGE]
```

The name “root” in this context means logging was called directly instead of setting up a logger by name.

The following is an example of import logging:

```
# Set up basic configuration to display all log levels

logging.basicConfig(level=logging.DEBUG)

# Log messages for each severity level

logging.debug("This is a DEBUG message.")

logging.info("This is an INFO message.")

logging.warning("This is a WARNING message.")

logging.error("This is an ERROR message.")

logging.critical("This is a CRITICAL message.")
```

This prints out:

```
DEBUG:root:This is a DEBUG message.

INFO:root:This is an INFO message.

WARNING:root:This is a WARNING message.

ERROR:root:This is an ERROR message.

CRITICAL:root:This is a CRITICAL message.
```

This print out includes all of the pre-defined logging points.

## Handlers

Handlers are advanced ways to manage and route logs. Handlers define the output destinations for log messages, allowing you to control where the log data goes, such as writing to files, sending emails, or printing to the console. 

The most basic handler is StreamHandler. The StreamHandler class allows you to configure logging to display log messages on the screen, making it useful for providing feedback, debugging, and monitoring during the execution of a program. This is the print() equivalent for logging, but StreamHandler also allows routing from arbitrary objects. Handlers can be attached to user-defined loggers using addHandler() or can be directly invoked.

Here is an example of a custom logger with a debug and a StreamHandler attached to it with a different severity level:

```
import logging

# Setting up the logger and StreamHandler

# Creating a logger

stream_logger = logging.getLogger('stream_logger')

stream_logger.setLevel(logging.DEBUG)  # Set logger to capture all messages from DEBUG level and above

# Ensure no previous handlers are attached

stream_logger.handlers = []

# Creating a StreamHandler

stream_handler = logging.StreamHandler()

stream_handler.setLevel(logging.INFO)  # Set handler to display only messages from INFO level and above

# Adding handler to logger

stream_logger.addHandler(stream_handler)

# Logging messages at different levels

stream_logger.debug("This is a DEBUG message for stream_logger.")

stream_logger.info("This is an INFO message for stream_logger.")

stream_logger.warning("This is a WARNING message for stream_logger.")

stream_logger.error("This is an ERROR message for stream_logger.")

stream_logger.critical("This is a CRITICAL message for stream_logger.")
```

output:

```
This is an INFO message for stream_logger.

This is a WARNING message for stream_logger.

This is an ERROR message for stream_logger.

This is a CRITICAL message for stream_logger.
```

### Different types of logging handlers

Besides StreamHandler, there are also many other handlers: 

- FileHandler
    
- NullHandler
    
- WatchedFileHandler
    
- BaseRotatingHandler
    
- RotatingFileHandler
    
- TimedRotatingFileHandler
    
- SocketHandler
    
- DatagramHandler
    
- SysLogHandler
    
- NTEventLogHandler
    
- SMTPHandler
    
- MemoryHandler
    
- HTTPHandler
    
- QueueHandler
    
- QueueListener
    

For more information about logging handlers, click [here](https://docs.python.org/3/library/logging.handlers.html). 

## Logging business data to a database

An advanced use case, but one very common in most cloud operations, is logging business-relevant data, such as logins and expensive requests, to a database. This logging would also generate alerts for outages and other items that require immediate attention. To do this with Python logging, one may combine the capabilities of the logging library with a database library. This enables the creation of custom handlers or loggers that interact with the database, allowing seamless storage and retrieval of crucial operational data to enable effective monitoring.

## Key takeaways

These takeaways emphasize the significance of logging for effective software development and production monitoring, as well as the distinction between using print() statements and the more structured approach of logging with severity levels and handlers.  

- **Overhead of** print()**statements in production:** Although using print() statements is convenient for development, it can lead to increased overhead in production environments. 
    
- **Distinguishing severity levels for effective monitoring:** Differentiating between various issues' severity levels is crucial. By using severity levels in logging, you can effectively filter out transient errors and monitor significant problems.
    
- **Using logging handlers for advanced log management:** Logging handlers are essential components for directing log messages to various destinations. They provide advanced capabilities, such as filtering messages, routing to multiple destinations, and enabling custom loggers.

<br>

***

<br>

# The logging module

The logging module in Python is a readily available, robust module that can be used by both novice programmers and professional teams. Because the majority of Python third-party libraries use it, you can combine your log messages with messages from both libraries to create a uniform log for your application.

Many applications, especially backend components that don’t directly interact with users, keep a log of their activities to aid in troubleshooting problems or monitoring the application’s performance. The Python logging module provides a standardized way of outputting those log messages to the system console, a file, the system logging daemon (syslogd), or other destinations.

Developers will often insert code that logs any or all of the following:

- Actions the program is about to take, is taking, or just completed
    
- The value of parameters and variables that might affect the program’s behavior
    
- Return values or output from other components (such as web services or databases)
    
- Timing and other performance data
    

You can customize both the formatting of your log and the level of detail that gets logged.

## Five levels of the logging module

A developer decides on a “severity” for each log message. The logger is configured to log anything above a certain severity level; everything else gets ignored.

The severity levels are as follows:

- **DEBUG:** Extra information only needed for debugging. This level often includes values of parameters and variables to help with troubleshooting. Example: logging **Parameter x: 42** to aid in diagnosing issues and include parameter values
    
- **INFO:** Informational message that can be used for tracing the program’s activities. Example: connecting to MySQL database at mydbserver.aws.amazon.com
    
- **WARNING:** An error that doesn’t require immediate action. Examples: **query took longer than 10 seconds, configuration file not found, or reverting to default settings**.
    
- **ERROR:** Serious, but can be a recoverable error. Example: database connection failed, or a file is missing.
    
- **CRITICAL:** Fatal error. Example: **A critical error has occurred! The application will now terminate.**
    

You decide how much detail to put into your log file. Many programs have a “**DEBUG**” flag that you can turn on to output additional debugging information. When things go wrong, more detail is always better than less, especially at the **DEBUG** level. Most of the time you can leave your logging at **INFO** to keep the log readable, but don’t be afraid to throw additional logging into your code. 

If you initialize the logger with **INFO** as the minimum level, then the log will contain everything from **INFO** to **CRITICAL**. **DEBUG** messages will be discarded.

You can configure your logger to include multiple handlers; each one logs to a different destination. This way, you can log to the console and to a file at the same time, with a different level of detail (minimum severity level) for each destination.

## Initializing a logger

Initializing the logger typically refers to the process of setting up and configuring a logging system using the built-in logging module. Initializing the logger involves creating a logger object, specifying its configuration, and defining how log messages should be handled and formatted. The steps involve the following: Import the logging module, create a logger instance, configure the logger, and then start logging messages.  

A simple way to initialize the logger is the following:

```
# Set the minimum logging level to INFO,

logging.basicConfig(level=logging.INFO)

# Get a logger object

log = logging.getLogger(__name__)

# Start the log file

log.info("Hello world")
```

The `__name__` parameter adds your Python module name to the logger’s output, so if your module is called **stuff.py**, your log would include “`[stuff]`” in its output. This way, multiple modules can log to the same file, but you can still quickly find messages from a particular module.

## Alternatives to the logging module 

One popular alternative is structlog, which outputs logs in a highly structured JSON format so they can be easily parsed by monitoring systems. With structlog, log messages are not only strings but rich data structures, which can make it easier to search, filter, and analyze logs.

Another is colorlog, which adds helpful color highlights when logging to the console. An example of this is assigning different colors to log levels like DEBUG, INFO, WARNING, ERROR, and CRITICAL. This step can make it quicker to spot the severity of each log message at a glance.  

The good news is that these alternatives are nearly drop-in replacements for the built-in logging module, so you don’t need much in the way of code changes to use them. The flexibility of these alternatives means a smooth transition requiring minimal code modifications to integrate them into your Python applications.

## Key takeaways

Python's built-in logging module is a tool suitable for both beginners and experienced programmers, making it a valuable choice for creating uniform logs in applications with third-party libraries. The logging module simplifies the process of recording and outputting log messages, enabling developers to track program activities, parameter values, errors, and performance data in a standardized manner. Developers can customize the format and level of detail in their log files, with five severity levels ranging from DEBUG for debugging to CRITICAL for fatal errors. Initializing the logger involves setting the minimum logging level, creating a logger instance with a module name, and starting the log, making it straightforward for developers to get started with logging.

<br> 

*** 

<br>

# Exception handling

Exception handling in Python is a method that allows developers to manage errors or exceptions that can occur during the execution of a program. Exceptions are errors that disrupt the normal flow of a program where the code cannot recover from automatically.

 Some examples of exceptions are the following:

- Attempting to divide by zero
    
- Referencing a variable that doesn’t exist
    
- Attempting to open a file that doesn’t exist
    
- Connecting fails to a remote server
    

Exception handling is special code you can add to your program to ensure that a program doesn't crash when an error occurs. This method also provides the opportunity to respond to errors in a controlled and meaningful way.

## The most common types of exceptions

When an error arises while a program is being executed, one of Python's built-in exceptions may occur. Some of the most common exception types in Python are the following: 

- NameError - usually due to a typo in a variable name
    
- AttributeError - also usually a typo, in calling a method on an object
    
- ValueError - parameter value is incorrect
    
- TypeError - sending a string when a function is expecting an int or calling a function with the wrong number or type of arguments
    
- ImportError - when Python can’t find a module you’re trying to import
    
- FileNotFoundError - when you try to perform file-related operations (opening, reading, writing, or deleting) on a file or directory that does not exist
    

## except statements

In Python, you use the except statement as part of exception handling to catch and handle specific types of exceptions that may occur during the execution of a program. It is used to recover from the error or notify the user. 

An example of an except statement is:

```
try:

  # Try to append to a file that is normally not writable

  # for anyone other than root 

  f = open("/etc/hosts", "w+")

except IOError as ex:

  # The variable "ex" will hold details about the error

  # that occurred

  print("Error appending to file: " + str(ex))

else:

  # If there was no exception, close the file.

  f.close()
```

## Differences with syntax errors and exceptions

As the name implies, syntax errors result from incorrect syntax in the code. They cause Python to terminate the program. Syntax errors usually occur due to typographical errors in the code, such as incorrectly indenting a line or misspelling a variable or function name. 

When a program is syntactically accurate, yet the code produces an error, exceptions occur. Although this error does not prevent the application from running, it alters how the program normally runs.

Syntax errors are related to the structure and grammar of the code and are detected before the program runs; whereas, exceptions are runtime errors that occur while the program is executing and are typically related to unexpected conditions or invalid operations. Syntax errors prevent the program from running, while exceptions can be caught and handled to allow the program to continue running despite encountering errors.

## Avoiding defensive code

Defensive code is a type of coding that aims to anticipate and handle exceptional conditions, errors, or unexpected inputs in a way that prevents the program from crashing or behaving unpredictably. Python coders, also known as Pythonistas, generally say “it’s better to ask forgiveness than permission.” This means that rather than adding lots of defensive code, you should just operate as usual and catch exceptions if they occur.

That means, instead of doing this:

```
if isinstance(user, dict) and "first_name" in user:

  first_name = user["first_name"]
```

Do this instead:

```
try:

  first_name = user["first_name"]

except KeyError:

  print("User does not have a first_name field")
```

## Key takeways

Exception handling in Python is a mechanism that allows you to handle errors and exceptional situations that may occur during the execution of a program. There are a great deal of exception types, but some of the most common are NameError, AttributeError, ValueError, TypeError, and ImportError. Syntax errors are related to the code's structure and grammar and are detected before the program runs.  In contrast, exceptions are runtime errors that occur during program execution, often due to unexpected conditions or invalid operations.

<br> 

*** 

<br>

# Exception handling examples

In Python, we can prevent errors or we can catch them by using exceptions. The frequently-used exception commands are try/except, raise, and finally. try/except is like a safety net that catches errors and prevents your program from crashing. raise is like a red flag that alerts you to a problem. finally is like a parachute that helps you land safely,  even if your program crashes. 

## Using try/except

Use try/except when you think your code may raise an error. For example, opening a file may raise an error if the file does not exist or cannot be opened. Connecting to another host on the network raises an error if the host is unavailable. Rather than allowing the program to crash, try/except allows you to catch the error by providing an error message.  

Let’s take a look at an example. This function tries to print the value of x. If x has not been defined yet, print() will raise a NameError.

```
try:

  print(x)

except NameError:

  print("Variable x is not defined")

Variable x is not defined
```

Another example shown below tries to append data to a file. If the file is not found, it prints a message. If there is any other error (such as “permission denied”), it prints the actual error. Finally, if there is no exception, it closes the file.

```
try:

  f = open("/etc/hosts", "w+")

  f.write("Success!")

except FileNotFoundError:

  print("Data file not found")

except Exception as ex:

  print("Error appending to file: " + str(ex))

else:

  f.close()

Error appending to file: [Errno 30] Read-only file system: '/etc/hosts'
```

## Using raise

Use raise when your code cannot continue to execute due to an error or incorrect input. 

This example will raise a TypeError if x is not an integer value

```
x = "hello"

if not isinstance(x, int):

  raise TypeError("Only integers are allowed")
```

The example below takes one argument and validates it. It raises either a TypeError or ValueError if it is invalid. This function first checks to make sure that the port number is an integer. If it is not an integer, the function raises a TypeError exception. The function then checks to make sure that the port number is between 1024 and 65535. This is because port numbers below 1024 are typically reserved for system services. If the port number is outside of this range, the function raises a ValueError exception. If the port number is valid, the function then starts the server on that port.

```
def start_server(port):

  if not isinstance(port, int):

    raise TypeError("Port number must be an integer")

  elif port < 1024 or port > 65535:

    raise ValueError("Port number is invalid")

No Output
```

## Using finally

You use a finally block to clean up after executing a code, whether that code raises an exception or not. It is often used to clean up resources like network connections or to return a value to the calling function. For example, you can use finally to close a file or a database connection after you’re done. 

Make sure your finally block doesn’t accidentally throw another exception. Let’s see an example:

```
try:

  f = open("/etc/hosts", "w+")

except:

  print("Error appending to file: " + str(ex))

finally:

  f.close()  # causes error if the file could not be opened

Error on line 2:
    f = open("/etc/hosts", "w+")
[OSError: [Errno 30] Read-only file system: '/etc/hosts'](oserror:%20%5BErrno%2030%5D%20Read-only%20file%20system%3A%20'/etc/hosts')

During handling of the above exception, another exception occurred:

Traceback (most recent call last):

Error on line 4:
    print("Error appending to file: " + str(ex))
NameError: name 'ex' is not defined

During handling of the above exception, another exception occurred:

Traceback (most recent call last):

Error on line 6:
    f.close()  # causes error if the file could not be opened
NameError: name 'f' is not defined
```

If opening the file causes an exception, then f has no value, and the finally block will cause another exception that will not be detected.

## Key takeaways

The exceptions in Python help you catch the code errors. These commands include try/except, raise, and finally. The try/except exception allows you to catch errors before they happen. The raise exception is used when your code cannot continue to execute due to an error or incorrect input and alerts you. The finally exception helps you clean up after executing a code, whether that code raises an exception or not.

<br> 

*** 

<br>

# Introduction to Python Email Library

Email messages look simple in an email client. But behind the scenes the client is doing a lot of work to make that happen! Email messages -- even messages with images and attachments -- are actually complicated text structures made entirely of readable strings!

The [_**Simple Mail Transfer Protocol (SMTP)**_](https://tools.ietf.org/html/rfc2821.html) and [_**Multipurpose Internet Mail Extensions (MIME)**_](https://tools.ietf.org/html/rfc2045) standards define how email messages are constructed. You _could_ read the standards documentation and create email messages all on your own, but you don't need to go to all that trouble. The [email built-in Python module](https://docs.python.org/3/library/email.html) lets us easily construct email messages.

We'll start by using the [email.message.EmailMessage class](https://docs.python.org/3/library/email.message.html#email.message.EmailMessage) to create an empty email message.

```
print(message)
```

As usual, printing the message object gives us the string representation of that object. The email library has a function that converts the complex EmailMessage object into something that is fairly human-readable. Since this is an empty message, there isn't anything to see yet. Let's try adding the sender and recipient to the message and see how that looks.

We'll define a couple of variables so that we can reuse them later. 

```
sender = "me@example.com"

recipient = "you@example.com"
```

And now, add them to the From and To fields of the message.

```
message['From'] = sender

message['To'] = recipient

print(message)

From: me@example.com

To: you@example.com
```

Cool! That's starting to look a bit more like an email message now. How about a subject?

```
From: me@example.com

To: you@example.com

Subject: Greetings from me@example.com to you@example.com!

print(message)

message['Subject'] = 'Greetings from {} to {}!'.format(sender, recipient)
```

**From**, **To**, and **Subject** are examples of _**email header fields**_. They’re _**key-value pairs**_ of labels and instructions used by email clients and servers to route and display the email. They’re separate from the email's _**message body**_, which is the main content of the message.

Let's go ahead and add a message body!

```
body = """Hey there!

I'm learning to send emails using Python!"""

message.set_content(body)
```

Alright, now what does that look like?

```
To: you@example.com

Subject: Greetings from me@example.com to you@example.com!

MIME-Version: 1.0

Content-Type: text/plain; charset="utf-8"

Content-Transfer-Encoding: 7bit

Hey there!

I'm learning to send email using Python! 
```

The message has a body! The **set_content()** method also automatically added a couple of headers that the email infrastructure will use when sending this message to another machine. Remember in an earlier course, when we talked about _**character encodings**_? The _**Content-Type**_ and _**Content-Transfer-Encoding**_ headers tell email clients and servers how to interpret the bytes in this email message into a string. Now, what about this other header? What is MIME? We'll learn about that next!

<br> 

*** 

<br>

# Adding Attachments

Remember, email messages are made up completely of strings. When you add an attachment to an email, whatever type the attachment happens to be, it’s encoded as some form of text. The _**Multipurpose Internet Mail Extensions (MIME)**_ standard is used to encode all sorts of files as text strings that can be sent via email. 

Let's dive in and break down how that works.

In order for the recipient of your message to understand what to do with an attachment, you  need to label the attachment with a _**MIME type**_ and _**subtype**_ to tell them what sort of file you’re sending. The _**Internet Assigned Numbers Authority (IANA)**_ ([iana.org](https://iana.org/)) [hosts a registry of valid MIME types](https://www.iana.org/assignments/media-types/media-types.xhtml). If you know the correct type and subtype of the files you’ll be sending, you can use those values directly. If you don't know, you can use the Python **mimetypes** module to make a good guess!

```
import os.path

attachment_path = "/tmp/example.png"

attachment_filename = os.path.basename(attachment_path)

import mimetypes

mime_type, _ = mimetypes.guess_type(attachment_path)

print(mime_type)

image/png
```

Alright, that **mime_type** string contains the MIME type and subtype, separated by a slash. The **EmailMessage** type needs a MIME type and subtypes as separate strings, so let's split this up:

```
mime_type, mime_subtype = mime_type.split('/', 1)

print(mime_type)

image

print(mime_subtype)

png
```

Now, finally! Let's add the attachment to our message and see what it looks like.

```
with open(attachment_path, 'rb') as ap:

     message.add_attachment(ap.read(),

                            maintype=mime_type,

                            subtype=mime_subtype,

                            filename=os.path.basename(attachment_path))

print(message)

Content-Type: multipart/mixed; boundary="===============5350123048127315795=="

--===============5350123048127315795==

Content-Type: text/plain; charset="utf-8"

Content-Transfer-Encoding: 7bit

Hey there!

I'm learning to send email using Python!

--===============5350123048127315795==

Content-Type: image/png

Content-Transfer-Encoding: base64

Content-Disposition: attachment; filename="example.png"

MIME-Version: 1.0

iVBORw0KGgoAAAANSUhEUgAAASIAAABSCAYAAADw69nDAAAACXBIWXMAAAsTAAALEwEAmpwYAAAg

AElEQVR4nO2dd3wUZf7HP8/M9k2nKIJA4BCUNJKgNJWIBUUgEggCiSgeVhA8jzv05Gc5z4KHiqin

eBZIIBDKIXggKIeCRCAhjQAqx4UiCARSt83uzDy/PzazTDZbwy4BnHde+9qZydNn97Pf5/uUIZRS

(...We deleted a bunch of lines here...)

wgAAAABJRU5ErkJggg==

--===============5350123048127315795==--
```

The entire message can still be serialized as a text string, including the image that we attached! The email message as a whole has the MIME type "multipart/mixed". Each _**part**_ of the message has its own MIME type. The message body is still there as a "text/plain" part, and the image attachment is a "image/png" part. Cool!

Now, how do we _send_ this email message? That's coming up!

<br> 

*** 

<br>

# Sending the Email Through an SMTP Server

As we called out, to send emails, our computers use the [_**Simple Mail Transfer Protocol (SMTP)**_](https://tools.ietf.org/html/rfc2821.html). This protocol specifies how computers can deliver email to each other. There are certain steps that need to be followed to do this correctly. But, as usual, we won't do this manually; we’ll send the message using the built-in [smtplib Python module](https://docs.python.org/3/library/smtplib.html). Let's start by importing the module.

```
import smtplib
```

With smtplib, we'll create an object that will represent our mail server, and handle sending messages to that server. If you’re using a Linux computer, you might already have a configured SMTP server like postfix or sendmail. But maybe not. Let's create a smtplib.SMTP object and try to connect to the local machine.

```
mail_server = smtplib.SMTP('localhost')

Traceback (most recent call last):

  File "<stdin>", line 1, in <module>

  (...We deleted a bunch of lines here...)

ConnectionRefusedError: [Errno 61] Connection refused
```

Oops! This error means that there's no local SMTP server configured. But don't panic! You can still connect to the SMTP server for your personal email address. Most personal email services have instructions for sending email through SMTP; just search for the name of your email service and "SMTP connection settings".

When setting this up, there are a couple of things that you'll probably need to do: Use a secure transport layer and authenticate to the service using a username and password. Let's see what this means in practice.

You can connect to a remote SMTP server using _**Transport Layer Security (TLS)**_. An earlier version of the TLS protocol was called _**Secure Sockets Layer (SSL)**_, and you’ll sometimes see TLS and SSL used interchangeably. This SSL/TLS is the same protocol that's used to add a secure transmission layer to HTTP, making it HTTPS. Within the smtplib, there are two classes for making connections to an SMTP server: The [_**SMTP class**_](https://docs.python.org/3/library/smtplib.html#smtplib.SMTP) will make a direct SMTP connection, and the [_**SMTP_SSL class**_](https://docs.python.org/3/library/smtplib.html#smtplib.SMTP_SSL) will make a SMTP connection over SSL/TLS. Like this:

```
mail_server = smtplib.SMTP_SSL('smtp.example.com')
```

If you want to see the SMTP messages that are being sent back and forth by the smtplib module behind the scenes, you can set the debug level on the SMTP or SMTP_SSL object. The examples in this lesson won’t show the debug output, but you might find it interesting!

```
mail_server.set_debuglevel(1)
```

Now that we’ve made a connection to the SMTP server, the next thing we need to do is authenticate to the SMTP server. Typically, email providers wants us to provide a username and password to connect. Let's put the password into a variable so it's not visible on the screen.



```
import getpass

mail_pass = getpass.getpass('Password? ')

Password?
```

The example above uses the [getpass module](https://docs.python.org/3/library/getpass.html) so that passers-by won't see the password on the screen. Watch out, though; the **mail_pass** variable is still just an ordinary string!

```
print(mail_pass)

It'sASecr3t!
```

Now that we have the email user and password configured, we can authenticate to the email server using the SMTP object's [login method](https://docs.python.org/3/library/smtplib.html#smtplib.SMTP.login).

```
mail_server.login(sender, mail_pass)

(235, b'2.7.0 Accepted')
```

If the login attempt succeeds, the login method will return a tuple of the [SMTP status code](https://tools.ietf.org/html/rfc4954#section-6) and a message explaining the reason for the status. If the login attempt fails, the module will raise a [SMTPAuthenticationError](https://docs.python.org/3.8/library/smtplib.html#smtplib.SMTPAuthenticationError) exception.

If you wrote a script to send an email message, how would you handle this exception?

### Sending your message

Alright! We're connected and authenticated to the SMTP server. Now, how do we send the message?

```
mail_server.send_message(message)

{}
```

Okay, well that last bit was pretty easy! We did the hard part first! The [send_message method](https://docs.python.org/3/library/smtplib.html#smtplib.SMTP.send_message) returns a dictionary of any recipients that weren’t able to receive the message. Our message was delivered successfully, so send_message returned an empty dictionary. Finally, now that the email is sent, let's close the connection to the mail server.

```
mail_server.quit()
```

And there you have it! We covered a lot in this lesson, so let's recap! First, we constructed an email message by using the built-in [email module](https://docs.python.org/3/library/email.html)'s [EmailMessage class](https://docs.python.org/3/library/email.message.html). Next, we added an attachment to our message with the help of the built-in [mimetypes module](https://docs.python.org/3/library/mimetypes.html). Finally, we connected to a SMTP server and sent the email using the smtplib module's 's [SMTP_SSL class](https://docs.python.org/3/library/smtplib.html#smtplib.SMTP_SSL).

Did you have any idea all of this was happening behind a simple email message?

<br> 

*** 

<br>

# Introduction to Generating PDFs

Depending on what your automation does, you might want to generate a PDF report at the end, which lets you decide exactly how you want your information to look like.

There's a few tools in Python that let you generate PDFs with the content that you want. Here, we'll learn about one of them: [_**ReportLab**_](https://www.reportlab.com/opensource/). ReportLab has a **lot** of different features for creating PDF documents. We'll cover just the basics here, and give you pointers for more information at the end.

For our examples, we'll be mostly using the high-level classes and methods in the _**Page Layout and Typography Using Scripts (PLATYPUS)**_ part of the ReportLab module.

Let's say that I have an awesome collection of fruit, and I want to create a PDF report of all the different kinds of fruit I have! I can easily represent the different kinds of fruit and how much of each I have with a Python dictionary. It might look something like this:

```
fruit = {

  "elderberries": 1,

  "figs": 1,

  "apples": 2,

  "durians": 3,

  "bananas": 5,

  "cherries": 8,

  "grapes": 13

}
```

Now let's take this information and turn it into a report that we can show off! We're going to use the **SimpleDocTemplate** class to build our PDF.

```
>>> from reportlab.platypus import SimpleDocTemplate

>>> report = SimpleDocTemplate("/tmp/report.pdf")
```

The **report** object that we just created will end up generating a PDF using the filename **/tmp/report.pdf**. Now, let's add some content to it! We'll create a title, some text in paragraphs, and some charts and images. For that, we're going to use what reportlab calls _**Flowables**_. Flowables are sort of like chunks of a document that reportlab can arrange to make a complete report. Let's import some Flowable classes.

```
>>> from reportlab.platypus import Paragraph, Spacer, Table, Image
```

Each of these items (**Paragraph**, **Spacer**, **Table**, and **Image**) are classes that build individual elements in the final document. We have to tell reportlab what _**style**_ we want each part of the document to have, so let's import some more things from the module to describe style.

```
>>> from reportlab.lib.styles import getSampleStyleSheet

>>> styles = getSampleStyleSheet()
```

You can make a style all of your own, but we’ll use the default provided by the module for these examples. The **styles** object now contains a default "sample" style. It’s like a dictionary of different style settings. If you've ever written HTML, the style settings will look familiar. For example **h1** represents the style for the first level of headers. Alright, we're finally ready to give this report a title!

```
>>> report_title = Paragraph("A Complete Inventory of My Fruit", styles["h1"])
```

Let's take a look at what this will look like. We can build the PDF now by using the **build()** method of our report. It takes a list of Flowable elements, and generates a PDF with them.

```
>>> report.build([report_title])
```

Okay, now let's take a look at the PDF:

![_86YSNzcRjWOmEjc3PY1-Q_bcbba43b212bfe5591e1b701b44a28e2_pasted-image-0](https://github.com/kemda2/Google-Courses/assets/19648132/5c2a3e22-cecb-4b15-8cd1-58a930da762d)

It's not much, but it's a start!

Up next, we'll look into an interesting Flowable for our reports: Tables.

<br> 

*** 

<br>

# Adding Tables to our PDFs

Up to now, we've generated an extra simple PDF file, that just includes a title.

Let's spice this up by adding a _**Table**_. To make a Table object, we need our data to be in a _**list-of-lists**_, sometimes called a _**two-dimensional array**_. We have our inventory of fruit in a dictionary. How can we convert a dictionary into a list-of-lists?

```
>>> table_data = []

>>> for k, v in fruit.items():

...   table_data.append([k, v])

...

>>> print(table_data)

[['elderberries', 1], ['figs', 1], ['apples', 2], ['durians', 3], ['bananas', 5], ['cherries', 8], ['grapes', 13]]
```

Great, we have the list of lists. We can now add it to our report and then generate the PDF file once again by calling the **build** method.

```
>>> report_table = Table(data=table_data)

>>> report.build([report_title, report_table])
```

And this is how the generated report looks now:

![dDC4EkhjRs2wuBJIYybNYg_819760c210201ef87129ffcb56d26626_pasted-image-0-1-](https://github.com/kemda2/Google-Courses/assets/19648132/bd7ac3a8-69cc-4e98-b73e-0620c29c0f7d)

Okay, it worked! It's not very easy to read, though. Maybe we should add some style to **report_table**. For our example, we'll add a border around all of the cells in our table, and move the table over to the left. _**TableStyle**_ definitions can get pretty complicated, so feel free to take a look at the documentation for a more complete idea of what’s possible.

```
>>> from reportlab.lib import colors

>>> table_style = [('GRID', (0,0), (-1,-1), 1, colors.black)]

>>> report_table = Table(data=table_data, style=table_style, hAlign="LEFT")

>>> report.build([report_title, report_table])
```

![mEW73N03StaFu9zdN5rWYw_e6a691a4ab0b80af644ec2ba5890c8ba_pasted-image-0-2-](https://github.com/kemda2/Google-Courses/assets/19648132/63ad68a0-bc32-4b0b-9ada-fa89b713916f)

Much better! Up next, we'll look into making this more colorful by adding graphs to our reports.

<br> 

*** 

<br>

# Adding Graphics to our PDFs

Up to now, we've generated a report with a title and a table of data. Next let's add something a little more graphical. What could be better than a fruit pie (graph)?! We’re going to need to use the _**Drawing**_ Flowable class to create a _**Pie**_ chart.

```
from reportlab.graphics.shapes import Drawing

from reportlab.graphics.charts.piecharts import Pie

report_pie = Pie(width=3*inch, height=3*inch)
```

To add data to our **Pie** chart, we need two separate lists: One for data, and one for labels. Once more, we’re going to have to transform our fruit dictionary into a different shape. For an added twist, let's sort the fruit in alphabetical order:

```
report_pie.data = []

report_pie.labels = []

for fruit_name in sorted(fruit):

    report_pie.data.append(fruit[fruit_name])

    report_pie.labels.append(fruit_name)

print(report_pie.data)

# output: [2, 5, 8, 3, 1, 1, 13]

print(report_pie.labels)

# output: ['apples', 'bananas', 'cherries', 'durians', 'elderberries', 'figs', 'grapes']
```

The **Pie** object isn’t Flowable, but it can be placed inside of a Flowable _**Drawing**_.

```
report_chart = Drawing()

report_chart.add(report_pie)
```

Now, we'll add the new Drawing to the report, and see what it looks like.

```
report.build([report_title, report_table, report_chart])
```

![kB8L5tDnR_qfC-bQ5xf6MQ_fedb9ca05eec18eb64a7f541e5b855c9_pasted-image-0-3-](https://github.com/kemda2/Google-Courses/assets/19648132/1c466dc8-7f40-4653-a17e-a58a67bcb6f6)

Alright, and with that, you've seen a few examples of what we can do with the ReportLab library.  There's a ton more things that can be done that we won't cover here. You'll want to refer to the [ReportLab User Guide](https://www.reportlab.com/docs/reportlab-userguide.pdf) for more details on the features we've seen, and to see what else you can create with it.

By the way, the ReportLab User Guide is a PDF that is generated using reportlab! Cool, right?

<br> 

*** 

<br>

# Project Problem Statement

It's that time again, time to flex your programming muscles and practice solving a real-life problem with the skills you acquired!

In the next lab, you'll have to process information related to the sales your company generated last month, and turn that into a nicely formatted PDF report that you'll then send by email so that your boss can look at it. The lab machine has email configured so that you can check your resulting emails through a nice webmail interface that's already up and running.

The system that you'll work with already includes some scripts that will do part of the work for you. You'll need to put these pieces together to get the result you want, basing your code on the one that's already there.

As we called out before, solving these problems can take some time, and that's ok! Solving complex problems is the best way to really master your coding skills. Before you start the lab, make sure you understand what you need to do and that you know how you want to solve it. Nobody is rushing you, so take as much time as you need, review any concepts that are not totally clear, and then get to it.

Good luck, you can totally do this!

<br> 

*** 

<br>

# DevOps

The traditional method of developing and deploying code included two teams: the development team and the IT operations team. The development team would write the code and then hand it off to the operations team. Then, the operations team would be responsible for deploying the code, conducting maintenance on it, and monitoring the code. With this method, two major problems continued to occur. First, the IT operations team did not have a complete understanding about what they were deploying or how the software should behave. On the other side, the development team lacked real-world knowledge in how their applications performed in production. This siloed way of working lacked efficiency and cohesiveness. Something had to change. DevOps was the solution.

In this reading, you will learn more about DevOps, its five principles, and how it’s implemented.

## DevOps

DevOps is the union between two important teams: the development team and the operations team. It’s a philosophy that attempts to eliminate the historical communication gap between developers and the IT operations department and to automate the processes between the two teams. The goal of DevOps is to produce better software more quickly and reliably. It focuses on cross-team collaboration and communication. DevOps emphasizes automation throughout the entire development process to increase reliability from writing the code, testing it, deploying it, and monitoring it.

Let’s explore a well-known streaming service company as an example. After becoming wildly successful early on, the company realized they would need to move their services into the cloud to be able to serve their millions of new users. At the same time, they recognized that their monolithic Java application would not support the vast amount of users. The company decided to redesign their application as a collection of independent microservices so there would be no single point of failure. They wrote the applications to leverage cloud-native databases and other services offered by the cloud provider. In addition, the company allowed for each team to update and release their team’s services on their own schedule. The company built their own tools to create a continuous integration and delivery pipeline. The company did not know it yet, but the changes they were implementing were the basics of DevOps principles.

## DevOps principles

DevOps has the following key principles:

**Collaboration:** The main purpose of DevOps is to promote and facilitate collaboration among teams.

**Automation:** Each part of the development process is automated. This helps make the building, testing, deploying, and monitoring of the code more stable and predictable.

**Continuous improvement:** Teams should always be looking for opportunities to improve the process, tools, and communication between teams.

**Customer mindset:** Teams should remember that the software they are developing will be used by customers. Listen to customers and take their feedback into consideration to continually create an improved software program. You want to develop software that is fun to use.

**Create with the end in mind:** Teams should understand customer needs and pain points, and they should develop solutions that solve real problems.

## Key takeaways

The DevOps philosophy is an opportunity for the development and operations teams to work together in an agile environment and optimize the development and deployment process. For DevOps to be successful, team members need to be open to working in a collaborative way with new processes. The automation tools can take time to learn how to implement, but this is only a small part of the larger battle.

<br> 

*** 

<br>

# SLAs

The words _I promise_ are powerful and meaningful. If you tell someone you promise to do something, that person is expecting you to follow through with your promise. In the operations and tech world, these promises are called service-level agreements (SLAs).

In this reading, you will learn more about SLAs, how they relate to service-level objectives (SLOs), and common SLAs in the industry.

## Service-level agreements

A service-level agreement is an agreement between a vendor and its clients or users that can be legally binding. Typically the SLA is included in the sale contract, guaranteeing a minimum level of performance for the client’s or user’s application. You can think of these as promises you are giving your users. And as with any promise there are consequences for breaking that promise. The SLA writes out the consequences that result if the promises are not met. Metrics in the SLA can include uptime, responsiveness, and responsibilities. 

## How SLAs relate to SLOs

An SLA outlines the specific SLOs and the penalties for violating them. Oftentimes, these consequences are a financial penalty or a cancellation of the contract. Because of this, it is important to understand what SLAs have been agreed upon to make informed decisions about how much to invest in reliability.

## SLA examples

To view examples and templates of SLAs used in the industry, view the following:

[Service-level agreement (SLA) examples and template](https://www.bmc.com/blogs/sla-template-examples/)

## Key takeaways 

An SLA is a service agreement typically between an IT service provider and a client. It outlines the details of the service, including what the service should accomplish and the consequences if there is a breach in the contract.

<br> 

*** 

<br>

# SLOs

All services have a level of quality and performance they are trying to obtain or reach. In the world of tech and operations, these are called service-level objectives (SLOs).

In this reading, you will learn more about SLOs, including how to write appropriate SLOs and how SLOs relate to service-level agreements (SLAs) and service-level indicators (SLIs).

## Service-level objectives (SLOs), defined

SLOs are found within an SLA and focus on specific and measurable metrics like uptime and response time. SLOs set the customers’ expectations and communicate to the IT and DevOps teams the goals they need to achieve. It’s important to understand and educate yourself on the SLOs that have been promised in the SLA so you can make informed decisions about how to invest in reliability and keep your promise to achieve the objectives.

When creating SLOs, write them as simply and clearly as possible. If the SLOs are vague or immeasurable, they will not serve their purpose — and you will be setting yourself up for failure.

## SLO example

Imagine that you work for an IT company that has entered into a contract with a customer, and that contract contains the following SLA:

_You will maintain 99% uptime of your application, defined as “the home page loads correctly 99% of the time within 10 seconds or less.”_

The SLA tells you which SLIs need to be monitored, including the page load time and whether the page loads correctly or returns an HTTP error message.

Your SLOs include:

1. The page will load in 10 seconds or less 99% of the time.
    
2. The page will return an HTTP 200 (success) code 99% of the time.
    

Now that your SLA and SLOs are defined, you can use a combination of monitoring tools to test the site periodically and record the results for tracking your real-world performance against the SLOs.

## Key takeaways

SLOs are important as they help achieve promises defined in the SLA. These help set customer expectations and should be clearly written, measurable, and attainable.

<br> 

*** 

<br>

# SLIs

A common term used by DevOps engineers and software developers is service-level indicator (SLI). SLIs measure the performance of an application at any given time.

In this reading, you will learn more about SLIs, including what they are, how to measure and monitor them, and how they relate to service-level agreements (SLAs) and service-level objectives (SLOs).

## Service-level indicators

An SLI measures the performance of your application against the objective, or SLO. It’s important to monitor SLIs to determine if your application is meeting the objective — or violating the SLA. Simply, SLIs help answer the question, _“How did we do?”_ in terms of having a promise and reaching that promise. Remember to keep your SLIs simple and choose the right metrics to track. 

## SLI example

Imagine that you work for an IT company and enter into a contract with customers. The contract contains the following SLA:

_You will maintain 99% uptime of your application, defined as “the home page loads correctly 99% of the time within 10 seconds or less.”_

The SLA tells you which SLIs you should monitor, including the page load time and whether the page loads correctly or returns an HTTP error message.

Monitoring tools like DataDog or AppDynamics can measure and record these metrics for you. These tools offer the ability to perform synthetic checks, by simulating a user accessing your application, and recording the results. The results from the synthetics checks can be used as your SLIs. These monitoring tools help you determine if you are staying within your SLOs.

## Key takeaways 

Service-level indicators help make service-learning objectives measurable. They provide actual data on performance. SLAs, SLOs, and SLIs all play a role in the overall service reliability.

<br> 

*** 

<br>

# Error budgets

Can you remember a time when you were growing up and someone gave you twenty dollars to spend at the grocery store? They might have said to bring home a gallon of milk and a dozen eggs, and whatever money is left you can spend however you want. That extra money — or the change — is akin to an error budget in service operations.

In this reading, you will learn more about error budgets, how they pertain to IT roles, and how an error budget can be used in the real world.

## Definition of an error budget

An error budget is the maximum amount of time a software program can fail and still be in compliance with the service-level objective (SLO). An error budget is typically represented by a percentage. A simple example is this: If an SLO states that a website should function properly 99.9% of the time, then the error budget is only 0.1%.

Now let’s calculate the error budget using time as a measurement in the question below. Here is an example in which an error budget is computed for a month’s time frame using the following formula:

Error budget = Total time * (1-SLO)

What is the error budget, in minutes, with an SLO of 99.9% uptime over a month?

The total time is the total time in minutes for a given time period. (Assume a 30-day month for this example.) The SLO is the service-level objective represented as a decimal.

Total time = 30*24*60 = 43,200. This formula multiplies 30 days by 24 hours in each day by 60 minutes in each hour to get a total of 43,200 minutes.

SLO = 99.9/100 = 0.999. This value represents the SLO as a decimal.  Substitute these values into the formula to get:

Error budget = 43,200 * (1–0.999)

Error budget = 43.1 minutes. This means the maximum amount of time the service can be down  is up to 43 minutes per month without violating the agreed-upon reliability standards (the SLO).

## The role of error budgets

Error budgets are part of cloud operations, site reliability engineering, and DevOps teams. They are used as a metric to make sure everything is running smoothly. If everything is running smoothly and there is a significant amount of time to use from the error budget, then DevOps members can use this time to invest in innovation on a product or software program. Error budgets also help establish limits for the development and programming teams. If there is not a lot of error budget to use, then developers know that they can’t try new things and that their focus needs to remain on the reliability of the product or program. Developers should save the release of new features for when the error budget is large.

## Key takeaways

Error budgets are typically represented as the maximum amount of time that a program is able to fail without violating an agreement. The error budget is based on the agreed-upon SLO between the clients and vendor. Developers are in favor of higher error budgets because this allows them to innovate and try new things within the product or service.

<br> 

*** 

<br>

# DevOps review

Congratulations! You’ve made it to the end of the module! Before you tackle the practice quiz and learn more about how DevOps is used in the real world, let’s review everything you’ve learned about DevOps.

DevOps is a methodology that replaced the traditional way of developing and deploying code. DevOps is a collaborative effort between the development and operations teams. They work in an agile environment to eliminate the communication gap between the two teams. This allows the software to be developed more quickly and reliably. Automation is a key element through the entire DevOps process. DevOps has five key principles that include: collaboration, automation, continuous improvement, customer mindset, and end-goal-focused creation. For DevOps to be successful, team members need to adjust their mindsets and be open to working in a collaborative way with new processes.

A service-level agreement (SLA) acts as a promise and can be a legally binding agreement between a vendor and its clients or users. It includes the sale contract outlining the minimum level of performance for the client’s or user’s application, and it includes the consequences if there’s a breach in the contract. Metrics in the SLA include uptime, responsiveness, and responsibilities. 

Service-level objectives (SLOs) are found within an SLA and focus on specific metrics like uptime and response time. They should be measurable and clearly written. SLOs set the customers’ expectations and communicate to the IT and DevOps teams the goals they need to achieve. 

Service-level indicators (SLIs) measure the performance of an application against the SLOs at any given time. Monitoring SLIs provides you with valuable insights on whether your application is meeting the objective or violating the SLA. SLIs help development and operation teams analyze and determine if the promise — or promises — they made to their customers or users are upheld.

An error budget is the maximum amount of time a software program can fail and still be in compliance with the SLO. This value is typically represented in percentage form and is the difference between 100% and the SLO percentage value. For example, if an SLO states that a website should function properly 99.8% of the time, then the error budget is only 0.2%. DevOps teams use their error budget time either to focus on the reliability of the program or to take risks in the program (if it is running smoothly).

<br> 

*** 

<br>

# Glossary terms from course 6, module 3

## **Terms and definitions from Course 6, Module 3**

**Error budgets:** Represented as the maximum amount of time that a program is able to fail without violating an agreement

**Service-level agreements (SLAs):** An agreement between a vendor and its clients or users that can be legally binding

**Service-level objectives (SLOs):**  A specific and measurable target that defines the level of performance, reliability, or quality a service should consistently deliver

<br> 

*** 

<br>

# IT skills in action reading

Congratulations! You have gained so much knowledge on automating real-world tasks with Python. There are many technical pieces that are included within automating specific tasks, but how would you apply the skills you’ve learned in a professional setting?

In this reading, you will review an example of how calling APIs and handling exceptions are used in the real world.

**Disclaimer:** The following scenario is based on fictitious companies.

## An outdated customer support system 

Adam Reyes, a software engineer, had a vast amount of data stored in the customer support system, SupportGenius Solutions. SupportGenius Solutions was the original customer support system on the market. At the time, they were innovative and created a huge disruption in the software industry. Unfortunately, SupportGenius Solutions is still using technology that isn’t fully supported and lacks the scalability that other systems have. Because of this, Adam knew it was time to shop for a new customer support system.

## Migrating data 

Adam did some research and decided to go with a new customer support system called SupportWave Technologies. SupportWave Technologies is up to date and able to handle Adam’s growing customer service demands. Adam needed to migrate his data from SupportGenius Solutions to SupportWave Technologies, but the only way to do this was to pay for a service to transfer the data. This solution was perfectly fine with Adam until he realized this transferring service was going to cost him thousands of dollars. There had to be another — cheaper — way.

## The affordable solution

Adam decided to use his Python programming skills to migrate the data instead. He called APIs and the requests module to extract the data from SupportGenius Solutions and processed everything on his own. Then, he loaded the data onto SupportWave Technologies. One downside to SupportWave Technologies that Adam discovered was that its API was prone to random errors. Adam decided to use Python’s exception handling mechanism to retry operations until they were completed. Adam used his Python skills to not only migrate data from one customer support system to another,  and he also did it affordably, allowing him to handle the growing customer service inquiries he was receiving.

<br> 

*** 

<br>

# Course 6x4 Putting it all together

# Module 4 Introduction

Great job, you've made it to the final module! You’ve come so far! Can you believe how much you’ve learned?

In the past few modules, you've seen how you can modify images using Python Imaging Library; how you can interact with web services using the Python requests module, sending data in JSON format; how you can generate PDF files with the content you want; and how you can send emails with those PDFs as an attachment. 

For the final project in this course, you’ll use the techniques and concepts you've seen to build a solution to a complex IT task. This can seem a bit daunting at first, but don't worry, you already have all the tools to solve this task!

In the next couple of readings, we're going to get into what to expect, and some things you should keep in mind when writing your solution.

<br> 

*** 

<br>

# Project Problem Statement

Okay, here's the scenario:

You work for an online fruit store, and you need to develop a system that will update the catalog information with data provided by your suppliers. When each supplier has new products for your store, they give you an image and a description of each product.

Given a bunch of images and descriptions of each of the new products, you’ll:

- Upload the new products to your online store. Images and descriptions should be uploaded separately, using two different web endpoints.
    
- Send a report back to the supplier, letting them know what you imported.
    

Since this process is key to your business's success, you need to make sure that it keeps running! So, you’ll also:

- Run a script on your web server to monitor system health.
    
- Send an email with an alert if the server is ever unhealthy.
    

Hopefully this summary has helped you start thinking about how you’ll approach this task. In case you’re feeling a little scared, don't worry, you can definitely do this! You have all the necessary tools, and the lab description will go into a lot more detail of what you need to do.

Up next, we'll give you a few tips that can help you along the way.

<br> 

*** 

<br>

# How to Approach the Problem

We're giving you a pretty big project to do at the end of this course -- but you can totally complete it with what you've learned until now! Take your time, and be methodical. Use these tips to help you:

**Break the problem down into smaller pieces.** If you’re not sure how to solve a piece of the puzzle, look for an even smaller piece that you _can_ solve. Build up those smaller pieces into a larger solution!

**Make one change at a time.** Write unit tests to make sure that each new part of the solution works the way you think it does. Run your unit tests frequently to make sure that each part of your solution **keeps working** as you make changes.

**Use version control.** Check each part of your solution into version control as you complete it, so you can always roll back to a known version of your code if you make a mistake.

_**Review module documentation!**_ You are going to need to use these modules to complete the final project. Reading the documentation takes time, but as you become more familiar with the APIs provided by these modules, it could save you from writing a bunch of custom code that could have just been a call to a module function! Remember, we’ve covered these modules in previous lessons too, so feel free to go back and review them if you need a refresher!

- [Python Image Library (PIL)](https://pillow.readthedocs.io/) - [Tutorial](https://pillow.readthedocs.io/en/stable/handbook/tutorial.html)
    
- [Requests](https://requests.readthedocs.io/) (HTTP client library) - [Quickstart](https://requests.readthedocs.io/en/master/user/quickstart/)
    
- [ReportLab](https://www.reportlab.com/docs/reportlab-userguide.pdf) (PDF creation library)
    
- [email](https://docs.python.org/3/library/email.examples.html) (constructing email)
    
- [psutil](https://psutil.readthedocs.io/) (processes and system utilization)
    
- [shutil](https://docs.python.org/3/library/shutil.html) (file operations)
    
- [smtplib](https://docs.python.org/3/library/smtplib.html) (sending email)
    

_**Read the lab instructions carefully!**_ Following the instructions and implementing your solution to the specifications that you’re given are critical to completing the task, and to being accurately graded

<br> 

*** 

<br>

# Course 6 glossary

To use the glossary for this course item, click the following link and select “Use Template.”

Link to glossary: [Course 6 glossary](https://docs.google.com/document/d/15Ci7DtfVqISX33YRLt4RjU78YQ4gkMnTutW0aXIQfq0/template/preview)

OR

If you don’t have a Google account, you can download the glossary directly from the following attachment.

[](https://d3c33hcgiwev3.cloudfront.net/I3vF_m6uR8qhgWRpGHPMnQ_baea406d6a3b430b89b1c02c463a03f1_Course-6-glossary.docx?Expires=1709769600&Signature=hLfUnRwffLIfpkKegCW2tDgBAPQYGeGlVHP5Eu7rmCnYjnVmddBb6CrCq4OOdDd7HRMzQLTPyqEapWQyO1EMqcL0Mng2mepfNVwGCYImnINy93gEv4iRl07kzE-1Et~pvTiVD~Zk16m-j3165Hku6QbHt3izSz3jvZZdt~3JQCQ_&Key-Pair-Id=APKAJLTNE6QMUY6HBC5A)

<br> 

*** 

<br>

# IT Automation with Python glossary

To use the glossary for this course item, click the following link and select “Use Template.”

Link to glossary: [IT Automation with Python Certificate glossary](https://docs.google.com/document/d/1lWWXJ6Uo5EhgHZUCz2lW6NnLRaNF5rxHXa_rn4Bouyo/template/preview)

OR

If you don’t have a Google account, you can download the glossary directly from the following attachment.

<br> 

*** 

<br>

# Social emotional skills

Employers are seeking candidates who bring a combination of social skills and emotional intelligence in addition to traditional technical skills. Being a good communicator and developing positive relationships with coworkers help employees stand out. Possessing good social and emotional skills will help use all your relationships—from personal to professional.

Prioritizing your workload is a critical skill that will save you a lot of time and stress, and it can help you prevent burnout. There are multiple tools, apps, and online resources that can assist with time management, to-do’s, and tasks. Find a method or approach that works for you. There is no one solution that works for everyone, so stay curious about different approaches to your organization and time management strategy. Break your big projects and tasks into smaller tasks to make it more manageable and more rewarding. When you focus on what outcomes you want to achieve by completing a specific task or goal, you can feel more in control of your time and emotional well-being. 

Procrastination is a major hindrance to productivity and work satisfaction. While it is normal to experience a little bit of procrastination, it is detrimental if it means you are completing the majority of your work very close to proposed deadlines, working overtime, experiencing troubles with focus, or working on the weekends to make up for lost hours of productivity. These all lead to feeling overwhelmed and stressed, and may make you feel depressed and overworked. Identify things that distract you from your work and reflect back on times when you did procrastinate. What were some common items, events, or settings that distracted you from focusing on your work? One item to consider is your work environment. Your surroundings can have a big influence on your focus and productivity. Workplaces that have a lot of activity or noise, or working in a busy cafe are some examples of environments that can distract us. At home, you might be interrupted by pets or children who want attention, outside noise, or various house tasks that you feel need done. Notice what settings you feel the most productive in and aspire to create a work environment that emulates that. Everyone is different!Approach this exploration with an open mind and make it work for you.

Confidence is at the cornerstone of success. It’s a critical skill that will help you be seen as a leader within your workplace and eventually lead to more opportunities for advancement or raises. Carrying yourself with confidence will help you earn respect from teammates and clients. Your confidence will guide them to trust your expertise to a greater degree. Regulating emotions also goes a long way in career success. 

Practicing empathy with coworkers and clients further develops a positive relationship with them. Everyone loves to feel like they’re understood and supported in their endeavors. It’s equally important that you take time to practice self-compassion and self-forgiveness. If you ever feel overwhelmed by the amount of tasks you have to complete or don’t understand the nature of your assignment, always reach out to your colleagues and supervisors for assistance. You are not in it alone, and everyone in the IT field has been a novice at some point in their career. Reach out to your team to gain clarification on the expectations for your role, brainstorm ideas about making your work more efficient, or revising your workload if you are assigned more than what you’re able to complete without burnout.

<br> 

*** 

<br>

# Working from home

Working from home is increasing in popularity. Every day, more and more employees want to work from home. At the same time, more and more companies are evaluating the pros and cons of having employees work from the comfort of their homes and are looking for options they can provide to their employees, such as working from home full time or developing a hybrid model.

Working from home has its benefits. You are independent, no longer commuting, and more productive. You save money on gas and clothing while being able to have more quality time with family and friends, an improved work-life balance, a flexible schedule, and more job opportunities, to mention a few.

What about a hybrid model? A hybrid model means some days at home and some days at the office. This raises questions such as:how to choose which days to work at home and how many days in a week. 

The reality is, no matter if you’re a full-time or a hybrid work-from-home employee, you will need to set up your home work environment to suit your job responsibilities.

When working from home, you will need some standard and basic services and accommodations: a reliable high-speed internet connection, a computer, a phone, and a desk and chair. Depending on your job, you may also need to have an accessible printer, some specific programs, an extra monitor,  and so on. Also, you will need to have a distraction-free environment. 

One of the challenges of working from home is scheduling your work week and staying organized. Before starting to work from home, make sure to set some ground rules:

- Decide your working hours. When you start your day, when you end it, lunch time, brain breaks, etc. After you decide your working hours, try to stick to them as much as possible.
    
- Plan your working tasks. Keep track of assignments for the month, the week, and the day. It will keep you organized and help you to meet your deadlines.
    
- Set some working rules to your loved ones. Establish when it is appropriate to get your attention, appropriate noise levels, and what is considered an emergency.
    
- Create boundaries between your work and your household chores. 
    
- Learn how to prioritize your work.
    

Now that you have all that you need to start working from home successfully, it’s time to learn to take advantage of the tools available to enhance collaboration. There are a few tools that will improve your productivity when working from home. Depending on your job, you will have these tools set up by your employer, or maybe you will have the flexibility to choose the one that is right for you. Whatever is the case, familiarize yourself with these types of tools:

- Calendar sharing
    
- File sharing 
    
- Instant messaging
    
- Document synchronization
    
- Cloud storage
    
- Video conferencing 
    

## Key takeaways

To successfully work from home:

- Set your work space to be comfortable for you.
    
- Set a working schedule that works for you.
    
- Be sure to have all the tools, software and equipment you need to perform your duties.
    
- Take advantage of all the tools available for you to make your job productive.

<br> 

*** 

<br>

# Advanced communication skills

## Interpersonal communication

In your IT career, you’ll need to use interpersonal communication every day. You’ll need to speak with other people in the company, including employees and managers, as well as people outside the company, such as vendors. You may also manage a team at some point. This reading will help you build the interpersonal communication skills you can use for everyday communications.

### Interpersonal communication types

- **Verbal communication:** This is spoken communication. You use this when you speak to others at the workplace, on the phone, or in virtual meetings.
    
- **Listening:** Listening is more than hearing what people say. Listening is focusing on what they are saying and receiving their messages. 
    
- **Written communication:** Letters, emails, text messages, emojis, and GIFs are all different types of written communication. 
    
- **Nonverbal communication:** Gestures, body language, eye contact, facial expressions, and touch are all examples of nonverbal communication. 
    

### Some ways to improve interpersonal communication

For a team or an organization to work well, members need to be able to say what they need others to know and to fully understand what others need from them. Here are some tips to help with interpersonal communication:

- **Be consistent:** Set communication standards and keep them.
    
- **Focus on professional communication:** Personal communication is unprofessional and takes away time you need for work. 
    
- **Avoid assumptions:** Listen to what the other person says and respond to what the other person is saying. Making assumptions will stop their full message from reaching you.
    
- **Listen actively:** Carefully listen to what the other person says and fully understand it before you respond. Responding without knowing the message leads to misunderstanding—and could lead to conflict. 
    

### Making requests

Members of a team or organization sometimes need to make requests of each other. Effective requests are more likely to get results, and they show team or organization members that they can rely on each other. When making requests:

- Be sure you know exactly what you’re requesting.
    
- Be clear. It’s important to communicate exactly what you need from the other person.
    
- Be patient. You may need to wait for the right opportunity to make the request if the other person is busy. 
    
- Listen carefully to what the other person has to say with an open mind if the person rejects it. 
    
- Always be polite and respectful.
    

### When to use which type of communication

Some communications are done verbally in the workplace or in a virtual meeting. Others are done through phone calls. Some are done through email, messaging, or on paper. Not all communications use written or spoken language. Some communication is nonverbal. Each situation calls for one or more types of communication.

In situations where information has to be given to the whole team, you should share it at the workplace in a meeting or in a virtual meeting using **verbal communication**. These situations include:

- Announcements the whole team needs to hear
    
- Ideas and requests for the team
    
- Requests for individuals that are not personal, such as asking a team member to perform a task for the team
    
- Discussion points that need to be discussed by the team
    

A second part of this communication is a group email sent to the team with a recap of the information from the meeting. This will give team members ongoing access to the information, and it will provide the information for any team members who couldn’t attend the meeting. 

Use **group emails** to the team when you have something important to share between meetings. Use text messages when you have short messages for other individuals. You can use personal emails for longer communications. 

For communications after hours, or for **private conversations** between two people, you can have a phone conversation or meet in a private office. Whatever you choose,  be sure to respect the other person’s privacy and have the conversation in a way no one else can hear it or join in. Here are some examples of private conversations:

- **Criticism:** Use criticism to help someone else solve a problem, not to hurt them. If you criticize them in front of the team, it will embarrass them, and it can lead to gossip and conflicts. 
    
- **Personal situations:** Someone may come to you with personal information. Treat this as a private communication. If the person wants the team to know, they will share it themselves. 
    

**Nonverbal communication** is important. It helps get the message across without words, but it can also cause problems when the wrong message comes through. When having interpersonal communications at work, try to avoid too much emotion. Here are some examples of nonverbal cues:

- **Facial expressions:** Example: A person says they’re happy, but they have a sad facial expression. People who experience the expression know the person is sad.
    
- **Tone of voice:** Tone of voice can say more than the words said. For example, when someone says “good job” in an angry tone, it probably means the speaker isn’t happy about what the other person did. 
    
- **Eye contact:** Looking directly at the speaker demonstrates to them that you are listening and interested in what they have to say. 
    
- **Actions:** Hand movements and other body movements are also communication. If you slam your fist on a table but say you are not angry, people will still know you are angry. 
    

### Leadership and interpersonal communication

During your career, you may lead a team or have a supervisory role. Communication skills are essential for a leadership position. You need to be able to communicate:

- **Expectations:** Be sure to set realistic expectations and clearly communicate them to your staff members. Make sure they understand them and encourage questions if there is something they don’t fully understand.
    
- **Questions:** Asking the right questions is important. Be sure you know exactly what information you need before asking questions. 
    
    - Examine the problem or situation and decide what you need to know.
        
    - Ask your question in a tone that demonstrates to the other person that you are interested in the answer. If you ask in an overly formal or accusing tone, the other person will feel anxious, and they may not answer fully.
        
    - Ask your questions clearly, and focus them on what you need to know. If the questions aren’t clear, or if they aren’t focused on what you need to know, the answers will also be unclear.
        
    - Actively listen to the answer after you ask the question. You need to fully understand what the other person is saying before you react to the information or use it.
        
    - After you get the information you need, thank the person who gave you the information. It shows the other person respect, and they will be more likely to answer questions in the future.
        

### Communication for introverts

If you’re more introverted, your communication experiences may be different than what extroverted people experience. Here are some tips.

- Think about what you want to know, and ask open-ended questions. That will let the other person give you full answers and take on much of the conversation. 
    
- Use quick greetings and responses to others’ greetings. If someone says “Good morning” to you, say the same. You can acknowledge the greeting without starting a conversation. 
    
- Prepare for meetings and functions. Think about what you are going to say, and have answers ready for questions you may be asked. If someone asks a question you don’t have an answer prepared for, ask if you can take a little time to think about it.
    

## Cross-cultural communication

You will be working with people from many different cultures and who are all over the world. Cross-cultural communication will help you understand the similarities and differences among different cultural groups and engage with different people from different cultures. For people to work together in teams and organizations, they need to understand each other well across cultures. 

### Working with people from other cultures

Your teams and organizations will have members from all over the world. There will be cultural differences between you and them. Some things you do will be different from how they do them. Because you are working with them, you need to understand each other to work together efficiently. Here are some ways to improve your cross-cultural communications:

- **Research and study the cultures** of people you work with. Find out what types of gestures and actions they use for communication. Find out if there are any gestures you use that are offensive to them and avoid those gestures. Find out which gestures they understand and try to use those.
    
- **Don’t use slang** when having cross-cultural communications. Your slang comes from your culture, and other cultures may not understand what it means. In some cases, slang from your culture may offend people from other cultures. 
    
- **Be careful with humor.** Different cultures have different understandings of humor. What is funny in your culture might not be funny—or even offensive—in other cultures. 
    
- **Be mindful of how you sound.** Speak slower if someone asks you to, but don’t speak too slow or it may offend the other person. 
    

### Problems with cross-cultural communication

Problems happen with cross-cultural communication, but if you know what causes them, you can avoid them. Here are some of the problems that can happen:

- **Stereotyping:** Stereotyping is offensive, and it gives you the wrong ideas about cultures. Sometimes well-meaning people mistake stereotypes for knowledge of a culture and use them to communicate with members of that culture. 
    
- **Differences in messaging:** You might send an email and find it either doesn’t get a response, or the response is slow. Some cultures treat email and other communications differently. You might come from a culture where individuals answer emails right away, but the culture you sent the email to doesn’t respond until their whole team looks at the email. 
    
- **Time-zone problems:** The world has 24 time zones; one for each hour. You need to check where the people you are communicating with and what time zones they’re in. Problems happen when someone in one time zone calls at a “regular” time, such as 9:00 in the morning, but the person on the other end of the communication has to wake up at 3:00 in the morning to take the communication. The receiver sees this as inconsiderate and it can lead to conflict and lost opportunities. 
    

## Managing conflict

When people work together, there will be some miscommunications. Problems with interpersonal communications, cross-cultural communications and clashing thoughts and ideas create conflict. Conflict can make your team inefficient because members have a difficult time working together. Being able to manage conflict will keep conflict from harming productivity and help your team work together toward goals, even if they disagree with each other. 

### Why does conflict happen?

Conflict happens for many reasons. Here are a few of the situations that can cause conflict:

- **Personality conflicts:** Every person is different, and each person has their own personality. Sometimes these personalities clash. 
    
- **Work environment problems:** Having a negative work environment leads to conflict. It’s important to keep a safe, comfortable work environment to prevent conflict.
    
- **Interpersonal communication problems:** Misunderstandings and negative responses to criticism cause conflict.
    
- **Cross-cultural communication problems:** Cultural misunderstandings and assumptions may create conflicts. 
    

### How do I solve conflict?

Conflict is natural when people work together. People often have different ideas and disagree. Once conflict happens, you need to resolve the conflict before it becomes worse. 

- **Address issues** as soon as you see them. Meet with the team members involved with the conflict and listen to what each of them has to say. Give each of them a chance to share their side of the conflict. 
    
- **Be clear** about what each side needs and address the situation. Once you know what each side needs and you heard both sides’ information about the conflict, find a resolution that will stop further conflict.
    
- **Prevent conflict** by keeping a safe, pleasant work environment. Keep the environment positive. Encourage open, friendly communication between team members. If there are minor disagreements, let them share them in an open, positive environment and put them aside before they create bigger problems.
    
- **Encourage** team members to share ideas and their cultures with the rest of the team often to promote cultural understanding and prevent cross-cultural communication problems. 
    

### What if I’m in the middle of the conflict?

As an IT professional, you will face conflict at times in your career. Conflict will happen, and dealing with it well will stop it from getting in the way of your work. Handling conflict and interruptions is important for success in your field. Here are some times you may be faced with conflict:

- **Critical feedback:** How you take criticism can lead to knowledge or conflict. When you receive criticism:
    
    - Listen actively to what the other person is saying. Figure out the point they are telling you. Is it constructive criticism? If it is, thank them and learn from it. Work on improving what they criticized you about.
        
    - If the criticism is empty criticism or hostile criticism, don’t fight back. If the person keeps doing it, report the hostile behavior to your supervisor. If you fight back, it will end in conflict.
        
- **Interruptions:** Sometimes someone will interrupt you while you are speaking. When you deal with an interrupter:
    
    - Find a time to talk to the interruptor in private and tell them you are upset about the interruptions. Say something like, “Please let me finish my sentences when I speak. I would be happy to answer any questions or discuss any points after I finish speaking.”
        
    - When they interrupt you at a meeting or in a conversation, calmly ask them to let you finish your sentence. If you react with hostility, your reaction will create conflict.
        

## Key takeaways

- Having good interpersonal communication skills will help you throughout your career as a team member and as a leader. Knowing which type of communication to use helps you get messages across in specific situations. 
    
- You will be working with people from all over the world in your career. Having cross-cultural communication skills will help you understand them and show respect for their cultures. It will also help you teach them about your culture and prevent misunderstandings.
    
- Managing conflict is important when you are dealing with a team or organization and other team members. Always listen with an open mind to all sides of the conflict. 
    
- When someone criticizes you, responding with hostility will create conflict. If the criticism is constructive, learn from it. 
    
- A safe, comfortable workplace helps prevent conflict.
    
- Instead of responding to an interrupter with hostility, calmly ask them to let you finish your sentence.

<br> 

*** 

<br>

# Impostor syndrome

Professionals in many fields—including IT—sometimes feel like they don’t belong in their positions. They look at others they work with and feel like the other people are real professionals in the field, and they are impostors and are not worthy of their positions. They feel like they got into their fields through luck or timing, and they are worried others will find out they are impostors. This is called “impostor syndrome.” This reading will help you understand impostor syndrome and how to deal with it if you see it in yourself. 

## How do you know if you have impostor syndrome?

- You feel like all the success you have in your career came from luck; not from learning skills and working hard.
    
- You are afraid someone will discover you are not qualified for your position. Once someone does, you will lose your position. 
    
- You fear you will be perceived as dishonest and you won’t be able to work in your field again.
    
- You feel like you need to put a lot of extra effort in to try to be worthy of the position.
    
- If you do something well and your team members or supervisors praise you, you feel you are not worthy of the praise.
    
- You sometimes don’t try to reach for goals because you feel like they are unattainable. 
    

## How to deal with impostor syndrome

First:Don’t feel bad about yourself if you have impostor syndrome! Many professionals in your field share it with you. There are even Nobel Prize winners who have impostor syndrome. It’s very common. You are **not** an impostor, though. You worked hard to get this far.

Here are some ways to deal with impostor syndrome:

- Look at all you’ve done in the course and in your experiences. Keep a journal of all your accomplishments. Every time you think of another one, write it in the journal. Be sure to include your achievement of successfully completing your Google Professional Certificate. 
    
- Become a teacher. Teach someone about your field. Let them ask questions and answer those questions the best you can. You might find out you know a lot more about the field than you thought you did. 
    
- Take out your accomplishment journal sometimes, read it, and celebrate your accomplishments. You can even reward yourself with something you really want and celebrate your success. 
    
- Every time you doubt yourself, think about a real problem you solved or an important task you completed successfully on the job. Find something good you did that week. Maybe you were able to troubleshoot a problem others struggled with, and you solved the problem successfully. Acknowledge your accomplishments and you will find plenty of ways you are very worthy of your position. 
    

## Taking risks

Once you have beat impostor syndrome and proven to yourself you are worthy of your position, you may fail in a task or on a project and feel like an impostor again, or a failure. Even the most well-known professionals, scientists, inventors, and other innovators have failed—and they have failed often. Failure does not make you an impostor. Instead, by learning from your failures, you will become even better at what you do. 

To move ahead in your career, sometimes you need to take risks. Here are some tips for dealing with risk:

- When you fail at something, learn from the failure: What went wrong? How can you do it better next time?
    
- Examine each project or task carefully, and think about it succeeding. What is the outcome? It may take a few failed tries to get to that outcome, but if you never start, you will never achieve that outcome. 
    
- Find others on the team who have done similar projects. Ask them for advice about how they worked on those projects. If the project fails, share what you learned with them and ask them for advice on how to avoid the same problem from happening again.
    

## Safe identity workspaces

**Safe identity workspaces** are a recent development in workplace environments, and their design lets employees share their ideas freely. In these spaces, employees feel a strong sense of belonging. They feel like essential parts of the team, and are less likely to be intimidated. In your career, you may work in one of these environments, as many companies are moving toward them and away from traditional offices. 

In a safe identity workplace, there is a leader, but the leader pays close attention to what the employees have to say and acts on their suggestions and ideas. In some of them, managers and supervisors are open to constructive criticism from the team. All team members in the workspace are treated as equals and encouraged to move forward in their careers.

## Key takeaways

- Impostor syndrome happens when a professional in a field feels unworthy of their position. People with impostor syndrome are scared someone will find out they are impostors and that they got their positions through luck and timing. 
    
- You can fight impostor syndrome by beating self-doubt and using your accomplishments to prove to yourself in your field.
    
- Failure is always a possibility, but if you don’t take risks, you won’t move forward in your career. Learn from your failures.
    
- Safe identity workspaces provide a workspace where everyone is treated as an equal. This encourages creativity and helps employees experience their parts as important members of the team.

<br> 

*** 

<br>

# Recognizing burnout

Burnout is prevalent in every industry. It can negatively affect work performance, interests in personal life, relationships, and health. Burnout occurs when there is excessive stress surrounding a job. As you progress through your career in IT, it’s important to recognize symptoms of burnout and work on managing the symptoms in advance.

## Career burnout

Burnout can occur from many things, including::

- Unclear purpose
    
- Overly demanding schedules
    
- Unclear expectations
    

There are many common signs of burnout: 

- Constantly exhausted
    
- Physical pain, such as migraines, headaches, and muscle aches and pains
    
- Changes in appetite
    
- Lack of energy and interest in activities outside of work
    
- Sleeping more or less than usual
    

## Identifying burnout triggers

It’s important to take time to reflect what is contributing to your burnout symptoms and experiences.

A **lack of agency** is one of the root causes of burnout. Symptoms of this include feeling like you’re not in control of your current situation, that you have no means to progress forward, that you feel underappreciated, that you work hard but still feel constantly roadblocked, and much more. 

Not getting enough rest or sleep also contributes a lot to burnout. When we don’t get enough sleep, we’re not as productive and often have troubles focusing. Do you feel like you’re in a constructive community? Feeling like you’re alone in the workplace can lead to burnout. If you’re working at a job that doesn’t give you a sense of purpose, it might be time to reconsider your options. Completing tasks that are not fulfilling to you or making the best use of your skills can affect the quality of your work and lead to burnout.

## Repairing causes of burnout

One of the main ways to decrease symptoms of burnout is to reframe your thoughts about your current situation. It’s also always beneficial to reach out for help from Human Resources, your supervisors, or other colleagues. For example, if you feel like your work has no sense of purpose, talk to your supervisor to see if there are other tasks or positions within your organization that allow you to work on projects and teams that give you a sense of fulfillment and purpose. Resetting expectations also greatly helps with repairing burnout. Take inventory of what the contract deliverables are for your current position, assess whether you are meeting those deliverables, and then take note of your own expectations of the position up until that moment in time. 

## Sustainable workplaces

Working for a company that grants its employees schedule flexibility, mental health resources, and manageable workloads can bring peace of mind and help your career in the long run by supporting your health and well-being. Flexible schedules allow for employees to attend life events such as medical appointments, family matters, and related matters at times that work best for the employee. Some companies will support mental health days and allow you to take paid time off to rest, recover, and recharge.