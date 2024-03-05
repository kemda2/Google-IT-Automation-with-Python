# Review: Puppet classes

This reading contains the code used in the instructional videos from ~[Puppet classes](https://www.coursera.org/learn/configuration-management-cloud/lecture/eYifs/puppet-classes)~. 
 
## Introduction

This follow-along reading is organized to match the content in the video that follows. It contains the same code shown in the next video. These code blocks will provide you with the opportunity to see how the code is written, allow you to practice running it, and can be used as a reference to refer back to. 

You can follow along in the reading as the instructor discusses the code or review the code after watching the video.

```
class ntp {
  package { 'ntp':
    ensure => latest,
  }

  file { '/etc/ntp.conf':
    source => 'puppet:///modules/ntp/ntp.conf'
    replace => true,
  }

  service { 'ntp':
    enable  => true,
    ensure  => running,
  }
}
```

## About this code

This code block includes a class with three resources, a package, a file, and a service. All of them are related to the Network Time Protocol, or NTP, the mechanism our computers use to synchronize the clocks. This code ensures that the NTP package is always upgraded to the latest version. We're setting the contents of the configuration file using the source attribute, which means that the agent will read the required contents from the specified location. And we're saying that we want the NTP service to be enabled and running. By grouping all of the resources related to NTP in the same class, we only need a quick glance to understand how the service is configured and how it's supposed to work. This would make it easier to make changes in the future since we have all the related resources together. It makes sense to use this technique whenever we want to group related resources. 
