# Review: Organizing your Puppet modules

This reading contains the code used in the instructional videos from [Organizing your Puppet modules Opens in a new tab](https://www.coursera.org/lecture/configuration-management-cloud/organizing-your-puppet-modules-0dYuQ). 

## Introduction

This follow-along reading is organized to match the content in the video that follows. It contains the same code shown in the next video. These code blocks will provide you with the opportunity to see how the code is written and can be used as a reference as you work through the course.

You can follow along in the reading as the instructor discusses the code or review the code after watching the video.

`tree modules/`

**Code output:** 

This is the file directory of the NTP class module from the previous videos. It includes the file and manifest directories and the ntp.conf and init.pp files that are associated with the NTP class. 

**modules/**
**|_ ntp**
    **|_ files**
    **|    |_ ntp.conf**
    **|_manifests**
         **|_ init.pp**
**3 directories, 2 files**

`sudo apt install puppet-module-puppetlabs-apache`

## About this code
This line of code installs the Apache module, provided by Puppet Labs. 

```
cd /usr/share/puppet/modules.available/puppetlabs-apache
ls -l
```

## About this code

The **cd** command changes directories to the directory that holds available modules from Puppet Labs, **/usr/share/puppet/modules.available/puppetlabs-apache**. The **ls -l** command lists its contents. 

**Code output:** 

The lib directory adds functions and facts to the ones already shipped by Puppet. The metadata.json file includes data about the Apache module. 

**Total 20**
**drwxr-xr-x 2 root root 4096 Dec 6 08:36 files**
**drwxr-xr-x 4 root root 4096 Dec 6 08:36 lib**
**drwxr-xr-x 9 root root 4096 Dec 6 08:36 manifests**
**-rw-r–r– 1 root root 4096 Sep 28 2018 metadata.json**
**drwxr-xr-x 6 root root 4096 Dec 6 08:36 templates**

`ls -l manifests/`

## About this code

This code displays a list of the manifests included in the Apache module. 


```
vim webserver.pp
include ::apache
```

## About this code

View the **webserver.pp** manifest file by entering editing mode with the vim command. When the manifest file opens, it is blank. Add the line **include ::apache**. This code indicates that the Apache module should be included. The **::** before **apache** indicates that it is a global module.

`sudo puppet apply -v webserver.pp`

## About this code

This code applies the rules from the **webserver.pp** file locally, configuring the Apache server. 
