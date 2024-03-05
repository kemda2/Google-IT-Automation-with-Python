# Review: Puppet resources

This reading contains the code used in the instructional videos from [Puppet resources](https://www.coursera.org/lecture/configuration-management-cloud/puppet-resources-0kd5I).
 
## Introduction

This follow-along reading is organized to match the content in the video that follows. It contains the same code shown in the next video. These code blocks will provide you with the opportunity to see how the code is written, allow you to practice running it, and can be used as a reference to refer back to. 

You can follow along in the reading as the instructor discusses the code or review the code after watching the video.
 
```
class sysctl {
  *# Make sure the directory exists, some distros don't have it*
  file { '/etc/sysctl.d':
    ensure => directory,
  }
}
```

## About this code

Here a file resource is defined. This is used for managing files and directories. This block of code ensures that  **/etc/sysctl.d** exists and is a directory.
 
```
class timezone {
      file { '/etc/timezone':
        ensure  => file,
        content => "UTC\n",
        replace => true,
      }
}
```

## About this code

In this code block, we are configuring the contents of **/etc/timezone**. This will be a file, and the contents of the file will be set to the UTC timezone. We also set the replace attribute to true, which means that even if the contents of the file already exist, they will  be replaced. 
