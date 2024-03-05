# Review: Customizing VMs in GCP
This reading contains the code used in the instructional videos from 
[Customizing VMs in GCP](https://www.coursera.org/learn/configuration-management-cloud/lecture/Y1aU8/customizing-vms-in-gcp)
. 

 
<br>
<br>

## Introduction

This follow-along reading is organized to match the content in the video that follows. It contains the same code shown in the next video. These code blocks will provide you with the opportunity to see how the code is written and can be used as a reference as you work through the course.

You can follow along in the reading as the instructor discusses the code or review the code after watching the video.

`./hello_cloud.py`

<br>
<br>

## About this code

The first line of this code uses the git clone command to clone the github repository blue-kale/hello. The second line uses the cd command to change the directory to this new directory, hello. The third line uses the ls command to list the files in the hello directory. This directory includes a simple web-serving application written in Python, called hello_cloud.py. The last line of code runs this application, which causes a socket to open and listen for HTTP connections on port 8000.

`sudo ./hello_cloud.py 80`

<br>
<br>

## About this code
The sudo command allows us to pass a different port, port 80, to the hello_cloud.py application so it listens on port 80 instead of on port 8000. 

`cat hello_cloud.service`

<br>
<br>

## About this code

This code opens the service definition file, also called a systemd file, for the hello_cloud.py application. 

Code output: 
The service entry in this file displays the directory in which the configuration expects to find the script we want to execute, /usr/local/bin/.

[Unit]

After=network.target

[Service]

ExecStart=/usr/local/bin/hello_cloud.py 80

[Install]

WantedBy=default.target

```
sudo cp hello_cloud.py /usr/local/bin/
sudo cp hello_cloud.service /etc/systemd/system/
sudo systemctl enable hello_cloud
```

<br>
<br>

## About this code

The first line of code copies the hello_cloud.py file into the directory /usr/local/bin/ . The second line copies the service file, hello_cloud.service, into the directory /etc/systemd/system/. In the third line of code, the systectl command enables hello_cloud to run automatically.

`sudo reboot`

<br>
<br>

## About this code

This code triggers a reboot of the system, which will restart the hello_cloud application. 

`ps ax | grep hello`

<br>
<br>

## About this code
In this code, the ps ax command provides a list of the running processes. The grep command filters this list to match and keep any items that match the pattern hello. 

`sudo apt install puppet`

<br>
<br>

## About this code
This code installs Puppet on this machine so it’s ready to run Puppet in the future.

`./hello/setup_puppet.sh`

<br>
<br>

## About this code
This code runs a script to do the initial configuration of the Puppet server and sets the Puppet process to run automatically on boot.