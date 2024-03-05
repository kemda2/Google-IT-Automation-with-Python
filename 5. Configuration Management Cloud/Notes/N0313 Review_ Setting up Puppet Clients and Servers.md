# Review: Setting up Puppet Clients and Servers

This reading contains the code used in the instructional videos from [Setting up Puppet Clients and Servers Opens in a new tab](https://www.coursera.org/learn/configuration-management-cloud/lecture/tOqXw/setting-up-puppet-clients-and-servers). 

## Introduction

This follow-along reading is organized to match the content in the video that follows. It contains the same code shown in the next video. These code blocks will provide you with the opportunity to see how the code is written and can be used as a reference as you work through the course. 

You can follow along in the reading as the instructor discusses the code or review the code after watching the video.

```
sudo puppet config --section master set autosign true
```

## About this code

This command configures Puppet to automatically sign the certificate requests of added nodes.

```
ssh webserver
sudo apt install puppet
sudo puppet config set server ubuntu.example.com
```

## About this code

The command ssh webserver allows you to ssh into a machine called webserver. The sudo apt install puppet installs the Puppet agent onto webserver with the Puppet package. Then, the command sudo puppet config set server [ubuntu.example.com Opens in a new tab](http://ubuntu.example.com/) configures Puppet to talk to the server on ubuntu.example.com.

`sudo puppet agent -v --test`

## About this code

This code tests the connection between the Puppet agent on the machine and the Puppet master. The **-v** command indicates that the output should be verbose, and the **--test** command indicates that this is a test run. 

**Code output:**
This output lists what puppet did to set up the connection between the Puppet agent on the machine and the Puppet master. First, it created an SSL key for the machine. Then, it read information from the machine and used it to create a certificate request. The puppet master generated a certificate, sent it to our puppet agent to store locally. Then, the agent retrieved the information from the machine and sent it to the master. It received a catalog from the master and applied it. 

Info: Creating a new SSL key for webserver.example.com
Info: Caching certificates for ca
Info: csr_attributes file loading from /etc/puppet/csr_attributes.yaml
Info: Creating a new SSL certificate request for webserver.example.com
Info: Certificate Request fingerprint (SHA256): 0E:E1:73:FB:E1:44:2F:FD:F8:84:A4:E4:00:99:37:F9:5A:48:23:B8:C4:E9:50:6C:EC:F5:D7:05:4D:C8:02:A7
Info: Caching certificate for webserver.example.com
Info: Caching certificate_revocation_list for ca
Info: Caching certificates for ca
Info: Using configured environment ‘production’
Info: Retrieving pluginfacts
Info: Retrieving plugin
Info: Retrieving locales
Info: Loading facts
Info: Caching catalog for webserver.example.com
Info: Applying configuration version ‘1575651019’
Notice: Applied catalog in 0.07 seconds

```
vim /etc/puppet/code/environments/production/manifests/site.pp
 
node webserver {
  class { 'apache': }
}
 
node default {}
```

## About this code

View and create the **site.pp** manifest file by entering editing mode with the **vim** command. First, to install Apache on the webserver nodes, define the webserver node with the **node webserver** command, and then include the Apache class without any parameters with **class{‘apache’}**. Second, define the default node definition with the code **node default{}**. We won’t add any classes yet. 

`sudo systemctl enable puppet`

## About this code

This code uses the **systemctl** command to enable the puppet service with the **enable** parameter so that the Puppet agent is started whenever the machine reboots. 

```
sudo systemctl start puppet
sudo systemctl status puppet
```

## About this code

This code starts the puppet service with the start parameter, then checks its status with the status parameter. 

**Code output:**
The code output confirms that the puppet service has been loaded and is actively running. 

```
* puppet.service - Puppet agent
   Loaded: loaded (/lib/systemd/system/puppet.service; enabled; vendor preset: enabled)
   Active: active (running) since Tue 2019-11-26 21:13:30 UTC; 5s ago
     Docs: man:puppet-agent(8)
  Process: 30471 ExecStart=/usr/bin/puppet agent (code=exited, status=0/SUCCESS)
 Main PID: 30496 (puppet)
    Tasks: 2 (limit: 4395)
   CGroup: /system.slice/puppet.service
           └─30496 /usr/bin/ruby /usr/bin/puppet agent
```
