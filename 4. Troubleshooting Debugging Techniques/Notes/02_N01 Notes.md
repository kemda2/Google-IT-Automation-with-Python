# Slowness

## Slow Web Server

```
$ ab -n 500 site.example.com/
This is ApacheBench, Version 2.3 <$Revision: 1843412 $>
Copyright 1996 Adam Twiss, Zeus Technology Ltd, http://www.zeustech.net/
Licensed to The Apache Software Foundation, http://www.apache.org/

Benchmarking site.example.com (be patient)
Completed 100 requests
Completed 200 requests
Completed 300 requests
Completed 400 requests

Complete requests: 500
Failed requests: 0
Total transferred: 483000 bytes
HTML transferred: 399500 bytes
Requests per second: 6.43 [#/sec] (mean)
Time per request: 155.488 [ms] (mean)
Time per request: 155.488 [ms] (mean, across all concurrent requests)
Transfer rate: 6.07 [Kbytes/sec] received

Connection Times (ms)
            min mean    [+/-sd] median  max
Connect:    0   0       0.3     0       8
Processing: 31  155     44.0    150     336
Waiting:    31  155     44.0    150     336
Total:      31  155     44.0    150     336

Percentage of the requests served within a certain time (ms)
50% 150
66% 164
75% 179
80% 187
90% 217
95% 234 
98% 259 
99% 279
100% 336 (longest request)


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
Last login: Tue Jan 7 10:58:48 2020 from 192.168.122.1

$ top
top - 11:18:52 up 20 min, 2 users, load average: 30.36, 29.00, 18.93
Tasks: 206 total, 4 running, 164 sleeping, 0 stopped, 0 zombie
%Cpu(s): 30.4 us, 0.7 sy, 68.9 ni, 0.0 id, 0.0 wa, 0.0 hi, 0.0 si, 0.0 st
KiB Mem : 2038492 total, 65620 free, 1901176 used, 71696 buff/cache
KiB Swap: 728520 total, 91408 free, 637112 used. 25892 avail Mem

PID     USER    PR      NI      VIRT        RES     SHR     S       %CPU        %MEM        TIME+       COMMAND
2854    user    20      0       868252      65180   1400    S       22.6        3.2         2:28.28     ffmpeg
2844    user    20      0       1134572     212128  1148    S       21.9        10.4        2:39.78     ffmpeg
2859    user    20      0       1136080     214592  1776    R       21.6        10.5        2:32.56     ffmpeg
2874    user    20      0       1135300     213472  1060    S       20.9        10.5        2:35.08     ffmpeg
2839    user    20      0       868244      65380   1348    S       20.6        3.2         2:27.90     ffmpeg
2849    user    20      0       1135924     214804  1124    S       19.6        10.5        2:31.48     ffmpeg
2869    user    20      0       868216      64980   1212    S       19.6        3.2         2:27.19     ffmpeg
2834    user    20      0       1136416     215256  1360    S       18.9        10.6        2:31-54     ffmpeg
2829    user    20      0       1137196     214736  1228    R       17.9        10.5        2:27.55     ffmpeg
2864    user    20      0       1135832     214696  1192    S       16.6        10.5        2:30.94     ffmpeg
1       root    20      0       159860      1384    244     S       0.0         0.1         0:02.62     systemd
2       root    20      0       0 0 0 S     0.0     0.0     S       0.7         0.0         0:00.00     kthreadd
3       root    0       -20     0 0 0 I     0.0     0.0     R       0.3         0.0         0:00.00     rcu_gp
4       root    0       -20     0 0 0 I     0.0     0.0     S       0.0         0.1         0:00.00     rcu_par_gp
6       root    0       -20     0 0 0 I     0.0     0.0     S       0.0         0.0         0:00.00     kworker/0:0H-kb
8       root    0       -20     0 0 0 I     0.0     0.0     I       0.0         0.0         0:00.00     mm_percpu_wq
9       root            20      0 0 0 0     S 0.    0.0     I       0.0         0.0         0 0:00.05   ksoftirqd/0
10      root    20      0       0 0 0 I     0.0     0.0     I       0.0         0.0         0:00.17     rcu_sched


$ for pid in $(pidof ffmpeg); do renice 19 $pid; done
2874 (process ID) old priority 0, new priority 19
2869 (process ID) old priority 0, new priority 19
2864 (process ID) old priority 0, new priority 19
2859 (process ID) old priority 0, new priority 19
2854 (process ID) old priority 0, new priority 19
2849 (process ID) old priority 0, new priority 19
2844 (process ID) old priority 0, new priority 19
2839 (process ID) old priority 0, new priority 19
2834 (process ID) old priority 0, new priority 19
2829 (process ID) old priority 0, new priority 19


$ ab -n 500 site.example.com/

This is ApacheBench, Version 2.3 <$Revisionz 1843412 $>
Copyright 1996 Adam Twiss, Zeus Technology Ltd, http://www.zeustech.net/
Licensed to The Apache Software Foundation, http://www.apache.org/

Benchmarking site.example.com (be patient)

Completed 100 requests
Completed 200 requests
Completed 300 requests
Completed 400 requests 

Failed requests: 0
Total transferred: 483000 bytes
HTML transferred: 399500 bytes
Requests per second: 6.52 [#lsec] (mean)
Time per request: 153.434 [ms] (mean)
Time per request: 153.434 [ms] (mean, across all concurrent requests)
Transfer rate: 6.15 [Kbytes/sec] received
Connection Times (ms)

            min     mean    [+/—sd]     median      max
Connect:    0       0       0.0         0           1
Processing: 36      153     43.3        148         332
Waiting:    36      153     43.3        148         332
Total:      36      153     43.3        148         332

Percentage of the requests served within a certain time (ms)
50% 148
66% 161
75% 178
80% 190
90% 210
95% 229
98% 263
99% 286
100% 332 (longest request)


$ ps ax | less
```
<br>

![Ekran görüntüsü 2024-02-03 213054](https://github.com/kemda2/Google-Courses/assets/19648132/183747d1-4125-4616-9e1f-71c087a61bd3)

<br>

```
$ /ffmpeg
```

<br>

![Ekran görüntüsü 2024-02-03 213054](https://github.com/kemda2/Google-Courses/assets/19648132/438316e0-9591-4cee-bca2-61676bd5e80c)

<br>

```
$ ps ax | less


$ locate static/001.webm
/srv/deploy_videos/static/001.webm


$ cd /srv/deploy_videos/


$ ls -l
```
<br>

![Ekran görüntüsü 2024-02-03 213054](https://github.com/kemda2/Google-Courses/assets/19648132/4ca88ae4-d6b9-4627-b505-9710bcd4ddd0)

<br>

![Ekran görüntüsü 2024-02-03 215544](https://github.com/kemda2/Google-Courses/assets/19648132/d5b4d673-fd25-4226-b450-e1fb3d9e8139)

<br>

```
$ vim deploy.sh
#!/bin/bash
# The videos need to be in the mp4 format in order to serve them
# in the website.
#
# This script runs ffmpeg in parallel to convert all of the webm files to mp4.
echo "Starting video conversion"
for video in static/*.webmg do
mp4_video="$(echo "$video" | sed 's/\.webm$/.mp4/')"
- daemonize -c $PWD /usr/bin/ffmpeg -nostats -nostdin -i "$video" "$mp4_video"
+ /usr/bin/ffmpeg -nostats -nostdin -i "$video" "$mp4_video"
done


$ killall -STOP ffmpeg


$ for pid in $(Pidof ffmpeg); do while kill -CONT $pid; do sleep 1; done; done


$ ab -n 500 site.example.com/ # 153'tn 33'e düşecek.
```

<br>


![Ekran görüntüsü 2024-02-03 213054](https://github.com/kemda2/Google-Courses/assets/19648132/29a5e7c2-8501-49c2-a3e5-ea7d900caa0e)

<br>

# Slow Code

## Slow Script with Expensive Loop

```
$ time ./send_reminders.py "2020-01-13|Example|test1"
Successfully sent reminders to: test1

real 0m0.129s
user 0m0.068s
sys 0m0.013s


$ time ./send_reminders.py "2020-01-13|Example|testl,test2,test3,test4,test5,test6,test7,test8,test9"

Successfully sent reminders to: test1,test2,test3,test4,test5,test6,test7,test8,test9

real 0m0.296s
user 0m0.222s
sys 0m0.008s


$ pprofile3 -f callgrind -o profile.out ./send_reminders.py "2020-01-13|Example|test1,test2,test3,test4,test5,test6,test7,test8,test9"
Successfully sent reminders to: testl,test2,test3,test4,test5,test6,test7,test8,test9


$ kcachegrind profile.out # En çok süreyi harcayan kısım get name
```
<br>
<br>

![Ekran görüntüsü 2024-02-05 120324](https://github.com/kemda2/Google-Courses/assets/19648132/3a454b57-d8e0-430c-99d7-5427a55b5b07)

![Ekran görüntüsü 2024-02-05 12](https://github.com/kemda2/Google-Courses/assets/19648132/c08dfe74-b901-47c7-8f50-dbc5b920b525)

<br>
<br>

```
# eski hali
$ atom send_reminders.py
def get_name(contacts, email):
  name = ""
  with open(contacts) as csvfile:
    reader = csv.reader(csvfile)
    for row in reader:
      if row[0] == email:
        name = row[1]
  return name

# Yeni Hali
def read_names(contacts):
  names = {}
  with open(contacts) as csvfile:
    reader = csv.reader(csvfile)
    for row in reader:
      names[row[0]] = row[1]
  return names

def send_message(date, title, emails, contacts):

  smtp = smtplib.SMTP('localhost')
  + names = read_names(contacts)
  for email in emails.split(','):
    - name= get_name(contacts, email)
    name = names[email]
    message = message_template(date, title, name)
    message['From'] = 'noreply@example.com'
    message['To'] = email
  smtp.send_message(message) 
  smtp.quit()


$ pprofile3 -f callgrind -o profile.out ./send_reminders.py "2020-01-13|Example|test1,test2,test3,test4,test5,test6,test7,test8,test9"
Successfully sent reminders to: testl;testz;test3;test4;tes:5,test6,test7,test8,test9


$ kcachegrind profile.out
```

<br>
<br>

![Ekran görüntüsü 2024-02-05 121914](https://github.com/kemda2/Google-Courses/assets/19648132/efb7514e-fbc2-449d-b29d-2f135f2730ec)

<br>
<br>

# When slowness Problems Get Complex 

## Using Threads to Make Things Go Faster

```
$ cd thumbnail_generator/


thumbnail_generator$ time ./thumbnail_generator.py
Processing: 100%    1000/1000     [00:01<00:00, 529.33it/s]

real 0m1.962s
user 0ml.898s
sys 0m0.065s


thumbnail_generator$ atom thumbnail_generator.py
+ from concurrent import futures
import argparse
import logging
import os
import sys
import PIL
import PIL.Image
from tqdm import tqdm
def process_options():
  kwargs = {
  'format': '[%(levelname)s] %(message)s',
  }
  parser = argparse.ArgumentParser(
  description='Thumbnail generator',
  fromfile_prefix_chars='@'
  )

def progress_bar(files):
  return tqdm(files, desc='Processing', total=len(files), dynamic_ncols=True)

def main():

  process_options()

  if not os.path.exists('thumbnails'):
    os.mkdir('thumbnails')
  
  + executor = futures.ThreadPoolExecutor()
  for root, _, files in os.walk('images'):
    for basename in progress_bar(files):
      if not basename.endswith('.jpg'):
        continue
      - process_file(root, basename)
      + executor.submit(process_file, root, basename)
  print('Waiting for all threads to finish')
  executor.shutdown()
  return 0

if _name_ == "_main_":
  sys.exit(main)


thumbnail_generator$ time ./thumbnail_generator.py
Processing: 100%  1000/1000 [00:00<00:00. 90266.09it/s]
Waiting for all threads to finish.

real 0m1.252s
user 0m2.637s
sys 0m0.295s 


thumbnail_generator$ atom thumbnail_generator.py
from concurrent import futures
import argparse
import logging
import os
import sys
import PIL
import PIL.Image
from tqdm import tqdm
def process_options():
  kwargs = {
  'format': '[%(levelname)s] %(message)s',
  }
  parser = argparse.ArgumentParser(
  description='Thumbnail generator',
  fromfile_prefix_chars='@'
  )

def progress_bar(files):
  return tqdm(files, desc='Processing', total=len(files), dynamic_ncols=True)

def main():

  process_options()

  if not os.path.exists('thumbnails'):
    os.mkdir('thumbnails')
  
  - executor = futures.ThreadPoolExecutor()
  + executor = futures.ProcessPoolExecutor()
  for root, _, files in os.walk('images'):
    for basename in progress_bar(files):
      if not basename.endswith('.jpg'):
        continue
      executor.submit(process_file, root, basename)
  print('Waiting for all threads to finish')
  executor.shutdown()
  return 0

if _name_ == "_main_":
  sys.exit(main)


thumbnail_generator$ time ./thumbnail_generator.py
Processing: %100 1000/1000 [00:00<00:00. 18019.25it/s]
Waiting for all threads to finish.

real 0m0.945s
user 0m3.277s
sys 0m0.173s


thumbnail_generator$
```

##