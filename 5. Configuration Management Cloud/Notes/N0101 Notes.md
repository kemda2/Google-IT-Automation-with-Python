# Configuration Management Cloud

## Customizing VMs in GCP

```
$ git clone https://github.com/blue-kale/hello cloning into 'hello'.
remote: Enumerating objects: 16, done.
remote: Counting objects: 100% (16/16), done.
remote: Compressing objects: 100% (12/12), done.
remote: total 16 (delta 4), reused 6 (delta 2), pack-reused 0
unpacking objects: 100% (16/16), done.


$ cd hello/


hello$ ls -l
README.md
hello_cloud.py
hello_cloud.service
setup_puppet.sh


hello$ ./hello_cloud.py
Listening for connections on port 8000
KeyboardInterrupt # ctrl+c ile durdurdu


hello$ sudo ./hello_cloud.py 80
Listening for connections on port 80


hello$ cat hello_cloud.service
[Unit]

After-network.target

[Service]

ExecStart=/usr/local/bin/hello_cloud.py 80

[Install]

WantedBy=default.target


hello$ sudo cp hello_cloud.py /usr/local/bin/ 


hello$ sudo cp hello_cloud.service /etc/systemd/system/


hello$ sudo systemctl enable hello_cloud
Created symlink /etc/systemd/system/default.target.wants/hello_cloud.service /etc/systemd/system/hello_cloud.service


hello$ sudo reboot


hello$ ps ax | grep hello

1061 ?     Ss 0:00 python3 /usr/local/bin/hello_cloud.py 80
1735 pts/0 S+ 0:00 grep --color=auto hello


hello$ sudo apt install puppet
Reading package lists... Done

Building dependency tree

Reading state information... Done

The following packages were automatically installed and are no longer required:

grub-pc-bin libnuma1 Use 'sudo apt autoremove' to remove them.

The following additional packages will be installed:

augeas-lenses debconf-utils facter fonts-lato hiera javascript-common libaugease libboost-filesystem1.65.1

libboost-locale1.65.1 libboost-log1.65.1 libboost-program-options1.65.1 libboost-regex1.65.1 libboost-system1.65.1

libboost-thread1.65.1 libcpp-hocone.1.6 libfacter3.10.0 libjs-jquery libleatherman-data libleatherman1.4.0 libruby2.5 libyaml-cppe.5v5 rake ruby ruby-augeas ruby-deep-merge ruby-did-you-mean ruby-json ruby-minitest ruby-net-telnet ruby-power-assert ruby-selinux ruby-shadow ruby-test-unit ruby2.5 rubygems-integration unzip zip

Suggested packages:

augeas-doc mcollective-common puppet-common apache2 | lighttpd | httpd augeas-tools ruby-rrd ruby-hocon ri ruby-dev bundler

The following NEW packages will be installed:

augeas-lenses debconf-utils facter fonts-lato hiera javascript-common libaugease libboost-filesystem1.65.1

libboost-locale1.65.1 libboost-log1.65.1 libboost-program-options1.65.1 libboost-regex1.65.1 libboost-system1.65.1 libboost-thread1.65.1 libcpp-hocone.1.6 libfacter3.10.0 libjs-jquery libleatherman-data libleatherman1.4.0 libruby2.5

libyaml-cppe.5v5 puppet rake ruby ruby-augeas ruby-deep-merge ruby-did-you-mean ruby-json ruby-minitest ruby-net-telnet ruby-power-assert ruby-selinux ruby-shadow ruby-test-unit ruby2.5 rubygems-integration unzip zip

upgraded, 38 newly installed, o to remove and 41 not upgraded.

Need to get 10.9 MB of archives. After this operation, 49.9 MB of additional disk space will be used.

Do you want to continue? [Y/n] y


hello$ ./hello/setup puppet.sh
```

```
gcloud init

Welcome! This command will take you through the configuration of gcloud.

Your current configuration has been set to: [default]

You can skip diagnostics next time by using the following flag:

gcloud init --skip-diagnostics

Network diagnostic detects and fixes local network connection issues.

Checking network connection...done.

Reachability Check passed.

Network diagnostic passed (1/1 checks passed).

You must log in to continue. Would you like to log in (Y/n)? y



gcloud init --skip-diagnostics

Network diagnostic detects and fixes local network connection issues.

Checking network connection...done.

Reachability Check passed.

Network diagnostic passed (1/1 checks passed).

You must log in to continue. Would you like to log in (Y/n)? y

Your browser has been opened to visit:

https://accounts.google.com/o/oauth2/auth?code_challenge=c233_zwO-mKzILP-zI9lwXOvfeISysHUmbcCj2QeTmA& prompt=select_account&code_challenge_method=S256&access_type=offline&redirect_uri=http://localhost% 3A8085/&response_type=code&client_id=32555940559.apps.googleusercontent.com&scope=https://www.goo gleapis.com/auth/userinfo.email+https://www.googleapis.com/auth/cloud-platform+https:/% 2Fwww.googleapis.com/auth/appengine.admin+https://www.googleapis.com/auth/compute+https:% 2F/www.googleapis.com/auth/accounts.reauth

Opening in existing browser session.

You are logged in as: [redquinoa2020@gmail.com].

Pick cloud project to use:

[1] first-cloud-steps-261217

[2] Create a new project

Please enter numeric choice or text value (must exactly match list

item):

1



[28] asia-east1-c

[29] asia-southeast1-b

[30] asia-southeasti-a

[31] asia-southeast1-c

[32] asia-northeast1-b

[33] asia-northeast1-c

[34] asia-northeast1-a

[35] asia-south1-c

[36] asia-south1-b

[37] asia-south1-a

[38] australia-southeast1-b

[39] australia-southeast1-c

[40] australia-southeast1-a

[41] southamerica-east1-b

[42] southamerica-east1-c

[43] southamerica-east1-a

[44] asia-east2-a

[45] asia-east2-b

[46] asia-east2-c

[47] asia-northeast2-a

[48] asia-northeast2-b

[49] asia-northeast2-c

[50] europe-north1-a

Did not print [12] options.

Too many options [62]. Enter "list" at prompt to print choices fully.

item):

Please enter numeric choice or text value (must exactly match list
1



$ gcloud compute instances create-source-instance-template webserver-template ws1 ws2 ws3 ws4 ws5
Created [https://www.googleapis.com/compute/v1/projects/first-cloud-steps-261217/zones/us-east1-b/instances/ws1].

Created [https://www.googleapis.com/compute/v1/projects/first-cloud-steps-261217/zones/us-east1-b/instances/ws2].

Created [https://www.googleapis.com/compute/v1/projects/first-cloud-steps-261217/zones/us-east1-b/instances/ws3].

Created [https://www.googleapis.com/compute/v1/projects/first-cloud-steps-261217/zones/us-east1-b/instances/ws4].

Created [https://www.googleapis.com/compute/v1/projects/first-cloud-steps-261217/zones/us-east1-b/instances/ws5].
```

|NAME|ZONE|MACHINE TYPE|PREEMPTIBLE|INTERNAL_IP|EXTERNAL_IP|STATUS|
|---|---|---|---|---|---|---|
|ws1|us-east1-b|n1-standard-1| |10.142.0.6|104.196.180.185|RUNNING|
|ws2|us-east1-b|n1-standard-1| |10.142.0.2|35.196.250.21|RUNNING|
|ws3|us-east1-b|n1-standard-1| |10.142.0.5|35.231.171.29|RUNNING|
|ws4|us-east1-b|n1-standard-1| |10.142.0.4|35.229.19.208|RUNNING|
|ws5|us-east1-b|n1-standard-1| |10.142.0.3|34.73.247.104|RUNNING|

## 

```








```


