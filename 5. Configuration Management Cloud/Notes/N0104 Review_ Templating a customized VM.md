# Review: Templating a customized VM

This reading contains the code used in the instructional videos from [Templating a Customized VM](https://www.coursera.org/learn/configuration-management-cloud/lecture/YIXOl/templating-a-customized-vm).

## Introduction

This follow-along reading is organized to match the content in the video that follows. It contains the same code shown in the next video. These code blocks will provide you with the opportunity to see how the code is written and can be used as a reference as you work through the course.

You can follow along in the reading as the instructor discusses the code or review the code after watching the video.

> gcloud init

## About this code

The **gcloud init** command sets up the authentication procedure between the virtual machine and Google Cloud. Note that you must log in to your cloud account to work with Google cloud from your CLI.

> gcloud compute instances create --source-instance-template webserver-template ws1 ws2 ws3 ws4 ws5

## About this code

This line of code creates five new virtual machines from the webserver template. In this code, the gcloud command calls Google Cloud. The compute parameter indicates we are working with virtual machines. The instances parameter indicates we’ll work with the VM instances, and the create command indicates that we’ll create new instances. The --source-instance-template webserver-template indicates which template to use to create these instances. And finally, the code ws1 ws2 ws3 ws4 ws5 lists the names of the five instances that will be created when this code is run.


