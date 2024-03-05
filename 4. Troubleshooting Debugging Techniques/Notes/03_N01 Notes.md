# Crashing Programs

## Internal Server Error

```
$ ssh webserver
user@webserver's password:
Welcome to Ubuntu 18.04.3 LTS (GNU/Linux 5.0.0-29-generic x86_64)

* Documentation: https://help.ubuntu.com
* Management: https://landscape.canonical.com
* Support: https://ubuntu.com/advantage
* Canonical Livepatch is available for installation.

- Reduce system reboots and improve kernel security. Activate at:
https://ubuntu.com/livepatch

0 packages can be updated.
0 updates are security updates.

Failed to connect to https://changelogs.ubuntu.com/meta-release-lts. Check your Internet connection or proxy settings
Your Hardware Enablement Stack (HWE) is supported until April 2023.
Welcome to the WebServer

Last login: Thu Jan 9 13:26:53 2020 from 192.168.122.1


$ date
Thu Jan 9 13:41:09 PST 2020
```
<br>
<br>

![Ekran görüntüsü 2024-02-06 123845](https://github.com/kemda2/Google-Courses/assets/19648132/6fe18151-adac-4c61-b832-cb8590001a6b)

<br>
<br>

```
/var/log/$ tail syslog # Anormal bir şey yok
Jan 9 13:28:14 webserver anacron[3669]: Job ‘cron.daily' terminated
Jan 9 13:28:14 webserver anacron[3669]: Normal exit (1 job run)
Jan 9 13:39:12 webserver_systemd[1]: Started Session 11 of user user.
```

<br>
<br>

![Ekran görüntüsü 2024-02-06 124155](https://github.com/kemda2/Google-Courses/assets/19648132/174b001f-2f66-41ee-987c-70ee87d71e3d)

<br>
<br>

![Ekran görüntüsü 2024-02-06 124414](https://github.com/kemda2/Google-Courses/assets/19648132/c70dffc3-df34-4579-93fb-50cc1c68996a)

<br>
<br>

![Ekran görüntüsü 2024-02-06 125127](https://github.com/kemda2/Google-Courses/assets/19648132/757c8274-595f-4a3d-9170-d215653c8450)

<br>
<br>

```
/var/log/$ vim /etc/nginx/sites~enabled/site.example.com.conf
server {
    listen 80;
    listen [:z]:80;
    server_name site.example.com;
    root /var/www/site.example.com;
    index index.html;
    location / {
        include uwsgi_params;
        uwsgi_pass 127.0.0.1:3031;
    }
}


/var/log/$ ls -l /etc/uwsgi/
total 8
drwxr-xr-x 2 root root 4096 Jan 9 2020 apps-available
drwxr-xr-x 2 root root 4026 Jan 9 2020 apps-enabled


/var/log/$ ls -l /etc/uwsgi/apps-enabled/
total 4 
-rw-r--r-- 1 root root 424 Feb 9 2018 README
lrwxrwxrwx 1 root root 46 Jan 9 2020 site.example.com.ini -> /etc/uwsgi/apps-available/site.example.com.ini


/var/log/$ vi /etc/uwsgi/apps-enabled/site.example.com.ini
[uwsgi]

chdir = /srv/site.example.com
uid = www-data
gid = www-data

plugins = python3
wsgi-file = prod.py
callable = app

plugins = logfile
logger = logs file:/var/log/site.log
log-route = logs .*

processes = 4
threads = 2
socket = 127.0.0.1:3031
stats = 127.0.0.1:9191


/var/log/$ ls -l site.log # 0 byte mantıklı değil
-rw-r----- 1 root root 0 Jan 9 13:25 site.log


/var/log/$ vi /srv/site.example.com/prod
prod.py products.py


/var/log/$ vi /srv/site.example.com/prod.py
```
<br>
<br>

![Ekran görüntüsü 2024-02-06 130403](https://github.com/kemda2/Google-Courses/assets/19648132/a0933308-bc99-428d-91cf-599398bede97)

<br>
<br>

![Ekran görüntüsü 2024-02-06 130436](https://github.com/kemda2/Google-Courses/assets/19648132/d5a7b275-4ab5-4740-aab2-91b24ea68308)

<br>
<br>


```
# Debug için bu satırın başındaki # işaretini sil diyor. Sudo ile açarak değişiklik yapacak
/var/log/$ sudo vi /srv/site.example.com/prod.py
```

<br>
<br>

![Ekran görüntüsü 2024-02-06 130844](https://github.com/kemda2/Google-Courses/assets/19648132/402225b6-5045-4d7f-ba71-770516cc45bb)

<br>
<br>

```
# Kaydedip yeniden çalıştıracak.
/var/log/$ sudo service uwsgi reload
Exception:
PermissionError(13. 'Permission denied')

Traceback:
Traceback (most recent call last):
    File "/usr/lib/python3/dist-packages/bottle.py", line 862, in dhandle
        return route.call("args)
    File "/usr/lib/python3/dist-packages/bottlc.py". line 1746. in wrapper
        rv = callback(‘a, 0Re)
    File "prod.py", line 25, in 1095
        with open(LOGFILE) as f:
PermissionError: [Errno 13] Permission denied: '/var/log/site.log'


/var/log/$ ls -l site*
-rw-r----- 1 root root 0 Jan 9 13:25 site.log
-rw-r----- 1 www-data www;data 203416 Jan 9 13:25 site.log.1


# sorunu düzeltmek için yetkileri değiştiriyoruz
/var/log/$ sudo chown www-data.www-data site.log 

# İşe yaradı
```

## Debugging a Segmentation Fault

```
example_coredump$ ./example
Segmentation fault


example_coredump$ ulimit -c unlimited


example_coredump$ ./example
Segmentation fault (core dumped)


example_coredump$ ls -l core
-rw------- 1 user user 380928 Jan 9 14:27 core


example_coredump$ gdb -c core example

Copyright (C) 2019 Free Software Foundation, Inc.
License GPLv3+z GNU GPL version 3 or later <http://gnu.org/licenses/gpl.html>
This is free software: you are free to change and redistribute it.
There is NO WARRANTY, to the extent permitted by law.
Type "show copying" and "show warranty" for details.
This GDB was configured as "x86_64-linux-gnu".
Type "show configuration" for configuration details.
For bug reporting instructions, please see:

<http://www.gnu.org/software/gdb/bugs/>.

Find the GDB manual and other documentation resources online at:
<http://www.gnu.org/software/gdb/documentation/>.

For help, type "help".
Type "apropos word" to search for commands related to "word"...
Reading symbols from exampLE...
[New LWP 15422]
Core was generated by ‘./example'.
Program terminated with signal SIGSEGV, Segmentation fault.
#0 _strlen_av_x2 () at ../sysdeps/x86_64/multiarch/strlen-avx2.S:65
65 _ ../sysdeps/x86_64/multiarch/strlen-avx2.S: No such file or directory.


(gdb)backtrace
#0 _strlen_av_x2 () at ../sysdeps/x86_64/multiarch/strlen-avx2.S:65
#1 0x0000558e723961b5 in copy_parameters (argc=1, argv=0x7fffcef4cd88) at example.c :10
#2 0x0000558e72396268 in main (argc=1, argv=0x7fffcef4cd88) at example.c:47

### strlen main fonksiyonundan copy parameters fonksiyonuyla alakalı bir sorun var demektir.

(gdb) up 
#1 0x0000558e723961b5 in copy_parameters (argc=1, argv=0x7fffcef4cd88) at example.c:10
10       size_t len = strlen(argv[i]) + 1;


(gdb) list
5
6   char** copy_parameters(int argc, char* argv[]) {
7       char **parameters = malloc(sizeof(char *) * argc);
8
9           for (int i = 0; i <= argc; i++) {
10          size_t len = strlen(argv[i]) + 1;
11          parameters[i] = malloc(len);
12          strncpy(parameters[i], argv[i], len);
13 }


(gdb) print i
$1 = 1
(gdb) print argv[0]
$2 = 0x7fffcef4e32c "./example"


(gdb) print argv[1]
$3= 0x0
### null pointer
```

## Debugging a Python Crash

```
$ cd update_products/


update_products$ cat new_products.csv
product_code,description
AV—101,Audio and Video converter 101 mm
SP-405,Sound Proofing 4.05 inches
TH-2,Tethering connector v2


update_products$ ./update_products.py new_products.csv
Traceback (most recent call last):
    File "./update_products.py", line 59, in <module>
        sys.exit(main())
    File "./update_products.py", line 54, in main
        update_data(database, options)
    File "./update_products.py", line 42, in update_data
        row['product_code'], row['description']))
KeyError: 'product_code'


update_products$ pdb3 update_products.py new_products.csv
> /home/user/update_products/update_products.py(2)<module>()
-> import argparse
(Pdb) continue
Traceback (most recent call last):
    File "/usr/lib/python3.7/pdb.py", line 1701, in main
        pdb._runscript(mainpyfile)
    File "/usr/lib/python3.7/pdb.py", line 1570, in _runscript
        self.run(statement)
    File "/usr/lib/python3.7/bdb.py", line 585, in run
        exec(cmd, globals, locals)
    File "<string>", line 1, in <module>
    File "/home/user/update_products/update_products.py", line 2, in <module>
        import argparse
    File "/home/user/update_products/update_products.py", line 54, in main
        update_data(database, options)
    File "/home/user/update_products/update_products.py", line 42, in update_data
        row['product_code'], row['description']))
KeyError: 'product_code'
Uncaught exception. Entering post mortem debugging
Running 'cont' or 'step' will restart the program
> /home/user/update_products/update_products.py(42)update_data()
-> row['product_code'], row['description']))
(Pdb) print(row)
OrderedDict([('\ufeffproduct_code', 'AV-101'), ('description', 'Audio and Video converter 101 mm')])
### ufeff kısmından little endian ve big endian sorunu olduğunu anladık.
update_products$ atom update_products.py
```

<br>
<br>

![Ekran görüntüsü 2024-02-06 175005](https://github.com/kemda2/Google-Courses/assets/19648132/b7ac803c-fd3c-40f4-b867-2d925f9a41de)

<br>
<br>

Eski Hali

![Ekran görüntüsü 2024-02-06 174956](https://github.com/kemda2/Google-Courses/assets/19648132/08ed428a-8805-4fdd-b5c2-dbf1bc2313a4)

<br>
<br>

Yeni Hali

![Ekran görüntüsü 2024-02-06 175046](https://github.com/kemda2/Google-Courses/assets/19648132/90fec69e-1784-420d-a903-c1ee45b40a09)

```
### UTF8-Sig olarak açıldı. Sorun çözüldü.
update_products$ ./update_products.py new_products.csv
Updating AV-101 with value: Audio and Video converter 101 mm
Updating SP-405 with value: Sound Proofing 4.05 inches
Updating TH-2 with value: Tethering connector v2
Update successful
```