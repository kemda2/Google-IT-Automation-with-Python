# Review: Puppet Nodes

This reading contains the code used in the instructional videos from [Puppet Nodes Opens in a new tab](https://www.coursera.org/learn/configuration-management-cloud/lecture/gSFeH/puppet-nodes).

## Introduction

This follow-along reading is organized to match the content in the video that follows. It contains the same code shown in the next video. These code blocks will provide you with the opportunity to see how the code is written and can be used as a reference as you work through the course. 

You can follow along in the reading as the instructor discusses the code or review the code after watching the video.

```
node default {
  class { 'sudo': }
  class { 'ntp':
        servers => ['ntp1.example.com', 'ntp2.example.com']
  }
} /
```

## About this code

The command **node default** installs the sudo and ntp classes on all default nodes. The sudo class is installed with its default parameters, because no parameters are specified. The ntp class is installed with an additional parameter, indicated by **servers => ['ntp1.example.com', 'ntp2.example.com']**. 

```
node webserver.example.com {
  class { 'sudo': }
  class { 'ntp':
        servers => ['ntp1.example.com', 'ntp2.example.com']
  }
  class { 'apache': }
}
```

## About this code

The command **node webserver.example.com** installs the sudo, ntp, and apache classes on nodes with the fully-qualified domain name (FQDN) webserver.example.com. 

Note: Because nodes with this FQDN have a specific set of classes that apply to them, the **node default** command will not apply any classes to them. 
