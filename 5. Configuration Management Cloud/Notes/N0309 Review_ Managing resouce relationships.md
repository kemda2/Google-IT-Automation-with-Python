#  Review: Managing resouce relationships

This reading contains the code used in the instructional videos from [Managing Resource Relationships Opens in a new tab](https://www.coursera.org/lecture/configuration-management-cloud/managing-resource-relationships-xV1AK).

## Introduction

This follow-along reading is organized to match the content in the video that follows. It contains the same code shown in the next video. These code blocks will provide you with the opportunity to see how the code is written and can be used as a reference as you work through the course.

You can follow along in the reading as the instructor discusses the code or review the code after watching the video.

```
class ntp {
  package { 'ntp':
    ensure => latest,
  } 
  file { '/etc/ntp.conf':
    source => '/home/user/ntp.conf',
    replace => true,
    require => Package['ntp'],
    notify  => Service['ntp'],
  }
  service { 'ntp':
    enable  => true,
    ensure  => running,
    require => File['/etc/ntp.conf'],
  }
}
include ntp
```

## About this code

View the **ntp.pp** manifest file by entering editing mode with the **vim** command. This file contains resources related to the NTP configuration: the ntp package, the ntp configuration file, and ntp service.

The relationships between these resources are also included in the code. In Puppet, code that defines a resource begins with a lowercase letter, whereas code that defines a relationship begins with a capital letter. The ntp configuration file requires the ntp package, which is indicated with the code **require => Package['ntp']**. The ntp service requires the ntp configuration file, which is indicated with the code **require => File['/etc/ntp.conf']**. Additionally, the ntp configuration file resource notifies the ntp service when it is present, which is indicated by the code **notify  => Service['ntp']**. 

The line **include ntp** indicates that the code will include the rules in this file as a class.

`sudo puppet apply -v ntp.pp`

## About this code

This code applies the rules from the ntp.pp file locally. The-v parameter specifies that the output should be verbose.

### Code output:

The code output indicates that the package was created, checked whether the configuration file needed to be updated, and restarted the ntp service.

```
Notice: Compiled catalog for ubuntu in environment production in 0.42 seconds

Info: Applying configuration version '1574775824'

Notice: /Stage[main]/Ntp/Package[ntp]/ensure: created

Info: /Stage[main]/Ntp/File[/etc/ntp.conf]: Filebucketed /etc/ntp.conf to puppet with sum aaad5b52b0cfa143eab6b62b247a1c19

Notice: /Stage[main]/Ntp/File[/etc/ntp.conf]/content: content changed '{md5}aaad5b52b0cfa143eab6b62b247a1c19' to '{md5}cebe9424982d7a311aafcf85c6410389'

Info: /Stage[main]/Ntp/File[/etc/ntp.conf]: Scheduling refresh of Service[ntp]

Notice: /Stage[main]/Ntp/Service[ntp]: Triggered 'refresh' from 1 event

Notice: Applied catalog in 6.55 seconds
```



```
vim ntp.conf
 
driftfile /var/lib/ntp/ntp.drift
statistics loopstats peerstats clockstats
filegen loopstats file loopstats type day enable
filegen peerstats file peerstats type day enable
filegen clockstats file clockstats type day enable
 
server 0.pool.ntp.org
server 1.pool.ntp.org
server 2.pool.ntp.org
server 3.pool.ntp.org
 
restrict -4 default kod notrap nomodify nopeer noquery limited
restrict -6 default kod notrap nomodify nopeer noquery limited
 
restrict 127.0.0.1
restrict ::1
 
restrict source notrap nomodify noquery
```


## About this code

View the ntp.pp manifest file by entering editing mode with the vim command. The lines beginning with “**server**” indicate that the NTP service uses servers from ntp.org. 

```
driftfile /var/lib/ntp/ntp.drift
statistics loopstats peerstats clockstats
filegen loopstats file loopstats type day enable
filegen peerstats file peerstats type day enable
filegen clockstats file clockstats type day enable

server time1.google.com
server time2.google.com
server time3.google.com
server time4.google.com

restrict -4 default kod notrap nomodify nopeer noquery limited
restrict -6 default kod notrap nomodify nopeer noquery limited
 
restrict 127.0.0.1
restrict ::1
 
restrict source notrap nomodify noquery
```

## About this code

The lines beginning with “**server**” have been updated to use the NTP servers provided by Google. 

`sudo puppet apply -v ntp.pp`


## About this code

This code applies the rules from the ntp.pp file locally, updates the configuration file with the new content from the file, then refreshes the service.
