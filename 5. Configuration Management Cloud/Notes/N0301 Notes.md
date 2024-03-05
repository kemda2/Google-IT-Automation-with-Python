# Puppet resources


```
class sysctl {

  # Make sure the directory exists, some distros don't have it 
  file { '/etc/sysctl.d': 
    ensure => directory, }

}
```

```
class timezone {

  file { '/etc/timezone': 
    ensure => file, 
    content => "UTC\n", 
    replace => true, 
  }

}
```

# Puppet Classes

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
    enable => true,
    ensure => running,

  }
}
```

# What are domain-specific languages?

```
if $facts['is_virtual'] {
  package { 'smartmontools': 
  ensure => purged,
  }

} else {
  package { 'smartmontools': 
  ensure => installed,
  }
}
```

# The Driving Principles of Configuration Management

```
file { '/etc/issue':
  mode => '0644',
  content => "Internal system \l \n",
}
```

```
$ ls -l example.txt
-rw-r--r-- 1 user user 0 Dec 6 07:09 example.txt


$ mv example.txt Desktop/


$ mv example.txt Desktop/
mv: cannot stat 'example.txt': No such file or directory # ikinci kez çalışmıyor. idempotent değil
```

```
exec{'move example file':
  command => 'mv /home/user example.txt /home/user/Desktop',
  onlyif => 'test -e /home/user/example.txt', # eğer dosya varsa çalıştır demek
}
```

# Applying Rules Locally

```
$ sudo apt install puppet-master



$ vim tools.pp

# vim
package {'htop':
ensure => present,
}



$ htop

Command 'htop' not found, but can be installed with:

sudo snap install htop # version 2.2.0, ог

sudo apt install htop # version 2.2.0-1

See 'snap info htop' for additional versions.



$ sudo puppet apply v tools.pp

Info: Loading facts

Notice: Compiled catalog for ubuntu.example.com in environment production in 0.02 seconds

Info: Applying configuration version 1575648408

Notice: /Stage[main]/Main/Package [htop]/ensure: created

Notice: Applied_catalog in 2.32 seconds



$ htop
```

![IMG_9864](https://github.com/kemda2/Google-Courses/assets/19648132/7bb68aa0-6f46-48a1-aaef-cedc354c7f61)

```

$ sudo puppet apply -v tools.pp

Info: Loading facts

Notice: Compiled catalog for ubuntu.example.com in environment production in 0.02 seconds

Info: Applying configuration version '1575648598'

Notice: Applied catalog in 0.08 seconds

```

# Managing Resource Relationships

```
$ vim ntp.pp

class ntp {
  package { 'ntp':
    ensure => latest,
  }
  file { '/etc/ntp.conf ':
    source => /home/user/ntp.conf',
    replace => true,
    require => Package['ntp'],
    notify => Service['ntp'],
  }
  service { ntp':
    enable => true,
    ensure => running, 
    require => File['/etc/ntp.conf'],
  }

include ntp
```


```
$ sudo puppet apply -v ntp.pp

Info: Loading facts

Notice: Compiled catalog for ubuntu.example.com in environment production in 0.02 seconds

Info: Applying configuration version 1575649201 

Notice: /Stage [main]/NtpPackage[ntp]/ensure: created 

Info: Computing checksum on file /etc/ntp.conf 

Info: /Stage[main]/Ntp/FLle[/etc/ntp.conf]: Filebucketed /etc/ntp.conf to puppet with sum 7898203e4c378c58b

Notice: /Stage[main]/Ntp/File[/etc/ntp.conf]/content: content changed (md5)10552d6aaf31958b' to (md53e70d0fa8ead9dfa08e41fc834fbb9bdc 

Info: Stage[nan]/Ntp/File[/etc/ntp.conf]: Scheduling refresh of Service[ntp]

Notice: /Stage [main]/Ntp/Service[ntp]: Triggered 'refresh' from 1 event

Notice: Applied catalog in 4.38 seconds



$ vim ntp.conf

driftfile /var/lib/ntp/ntp.drift
leapfile /usr/share/zoneinfo/leap-seconds.list
statistics loopstats peerstats clockstats

filegen loopstats file loopstats type day enable
filegen peerstats file peerstats type day enable
filegen clockstats file clockstats type day enable

# server 0.pool.ntp.org
# server 1.pool.ntp.org
# server 2.pool.ntp.org
# server 3.pool.ntp.org

server time1.google.com
server time2.google.com 
server time3.google.com
server time4.google.com

restrict -4 default kod notrap nomodify nopeer noquery limited
restrict -6 default kod notrap nomodify nopeer noquery limited

restrict 127.0.0.1
restrict ::1

restrict source notrap nomodify noquery



$ sudo puppet apply -v ntp.pp
```

#  Organizing Your Puppet Modules

```$ tree modules/
$ tree modules/
nodules/
  Ntp
    files
      ntp.conf
    manifests
      init.pp
3 directories, 2 files
```

```
# module installation
$ sudo apt install puppet-module-puppetlabs-apache
Reading package lists... Done
Building dependency tree
Reading state information... Done
The following additional packages will be installed:
puppet-module-puppetlabs-concat puppet-module-puppetlabs-stdlib
The following NEW packages will be installed:
puppet-module-puppetlabs-apache puppet-module-puppetlabs-concat puppet-module-puppetlabs-stdlib 0 upgraded, 3 newly installed, 0 to remove and 4 not upgraded.
Need to get 268 kB of archives.
After this operation, 1,161 kB of additional disk space will be used.
Do you want to continue? [Y/n] y
```

```
$ cd /usr/share/puppet/modules.available/puppetlabs-apache/



/usr/share/puppet/modules.available/puppetlabs-apache$ ls -l
total 20

drwxr-xr-x 2 root root 4096 files
drwxr-xr-x 4 root root 4096 lib
drwxr-xr-x 9 root root 4096 manifests
-rw-r--r-- 1 root root 1820 metadata.json
drwxr-xr-x 6 root root 4096 templates



/usr/share/puppet/modules.available/puppetlabs-apache $ ls -l manifests/
# lots of files



/usr/share/puppet/modules.available/puppetlabs-apache $ cd



$ vim webserver.pp
include::apache



$ sudo puppet apply -v webserver.pp
```

#  Puppet Nodes

```
node default {
  class { 'sudo': }
  class { 'ntp':
    servers => ['ntp1.example.com', 'ntp2.example.com']
  }
}
```

# Setting up Puppet Clients and Servers

```
$ sudo puppet config -section master set autosign true
ssh webserver user@webserver's password:

Welcome to Ubuntu 18.04.3 LTS (GNU/Linux 5.0.0-29-generic x86_64)

* Documentation: https://help.ubuntu.com

Management: https://landscape.canonical.com

Support: https://ubuntu.com/advantage

Canonical Livepatch is available for installation.

Reduce system reboots and improve kernel security. Activate at:

https://ubuntu.com/livepatch

0 packages can be updated. 8 updates are security updates.

Your Hardware Enablement Stack (HWE) is supported until April 2023.

*** System restart required Welcome to the WebServer

Last login: Fri Dec 6 08:42:00 2019 from 192.168.122.1



$ sudo apt_install puppet



$ sudo puppet config set server ubuntu.example.com



$ sudo puppet agent-v-test
Info: Creating a new SSL key for webserver.example.com
Info: Caching certificate for ca
Info: csc attributes file loading fron /etc/puppet/csr_attributes.yanl Info: Creating a new SSL certificate request for webserver.example.com
Info: Certificate Request fingerprint (SHA256): ΘE:E1:73:FB:E1:44:2F:FD:F8:84:A4:E4:00:99:37:F9:54:48:23:88:C4:E9:50:6C:EC:F5:07:05:40:C8:02:A7
Info: Caching certificate for webserver.example.com Info: Caching certificate revocation list for ca
Info: Caching certificate for ca Info: Using configured environment 'production
Info: Retrieving pluginfacts Info: Retrieving plugin
Info: Retrieving locales Info: Loading facts
Info: Caching catalog for webserver.example.com
Info: Applying configuration version 1575651019
Notice: Applied catalog in 0.07 seconds



$ vim /etc/puppet/code/environments/production/manifests/site.pp
node webserver.example.com {
  class {'apache':}
}

node default {}



$ sudo puppet agent -v --test



$ sudo systemctl enable puppet

Synchronizing state of puppet.service with SysV service script with /lib/systemd/systemd-sysv-install.

Executing: /lib/systemd/systemd-sysv-install enable puppet



$ sudo systemctl start puppet



$ sudo systemctl status puppet
puppet.service Puppet agent

Loaded: loaded (/lib/systemd/system/puppet.service; enabled; vendor preset: enabled)

Active: active (running) since Fri 2019-12-06 08:59:10 PST; 6s ago

Docs: man:puppet-agent(8)

Process: 7033 ExecStart=/usr/bin/puppet agent (code=exited, status=0/SUCCESS)

Main PID

: 7041 (puppet) Tasks: 2 (limit: 2332)

CGroup:

/system.slice/puppet.service

L7041 /usr/bin/ruby /usr/bin/puppet agent

Dec 06 08:59:09 webserver systemd[1]: Starting Puppet agent. Dec 06 08:59:10 webserver puppet-agent[7041]: Reopening log files

Dec 06 08:59:10 webserver puppet-agent[7041]: Starting Puppet client version 5.4.0

Dec 06 08:59:10 webserver systemd[1]: Started Puppet agent. Dec 06 08:59:13 webserver puppet-agent[7045]: Applied catalog in 0.42 seconds
```

#  Modifying and Testing Manifests

```
describe 'gksu', :type => : class do
  let (:facts) { { 'is_virtual' => 'false' } }
  it { should contain_package('gksu').with_ensure('latest') }
end
```
