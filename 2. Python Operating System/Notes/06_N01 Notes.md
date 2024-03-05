# Notes

```
$ mkdir mynewdir
$ cd mynewdir
mynewdir$ pwd
/home/user/mynewdir
mynewdir$ cp ../spyder.txt . # cp copy .. parent directory . current directory
mynewdir$ touch myfile.txt # boş dosya oluşturma
mynewdir$ ls -l # without -l only the file names appear 
total 4
-rw-r--r-- 1 user user 0 Jan 8 14:41 myfile.txt # permissions column number owner owner group size (byte) modified date filename
-rw-r--r-- 1 user user 192 Jan 8 14:39 spider.txt

mynewdir$ ls -la
total 12
drwxr-xr-x 2 user user 4096 Jan 8 14:41
drwxr-xr-x 30 user user 4096 Jan 8 14:37
-rw-r--r-- 1 user user 0 Jan 8 14:41 myfile.txt
-rw-r--r-- 1 user user 192 Jan 8 14:39 spider.txt

mynewdir$ mv myfile.txt emptyfile.txt # rename 
mynewdir$ cp spider.txt yetanotherfile.txt # copy

mynewdir$ ls -l
total 8
-rw-r--r-- 1 user user 0 Jan 8 14:41 emptyfile.txt
-rw-r--r-- 1 user user 192 Jan 8 14:39 spider.txt
-rw-r--r-- 1 user user 122 Jan 8 14:45 yetanotherfile.txt

mynewdir$ rm *
mynewdir$ ls -l # delete
total 0

mynewdir$ cd ..
$ rmdir mynewdir/
$ ls mynewdir
ls: cannot access 'mynewdir': No such file or directory
```

```
$ cat stdout_example.py
#!/usr/bin/env python3
print("Don't mind me, just a bit of text here...")

$ ./stdout_example.py
Don't mind me, just a bit of text here...

$ stdout_example.py > new_file.txt # çıkışı new file dosyasına aktar yoksa oluştur varsa üstüne yaz
$ cat new_file.txt
Don't mind me, just a bit of text here...

$ stdout_example.py >> new_file.txt # çıkışı new file dosyasının en alt satırına ekle
$ cat new_file.txt
Don't mind me, just a bit of text here...
Don't mind me, just a bit of text here...

$ cat streams_err.py
data = input("Thi5 will come from STDIN: ")
print("Now we write it to STDOUT: " + data)
raise ValueError("Now we generate an error to STDERR")


$ ./streams_err.py < new_file.txt
This will come from STDIN: Now we write it to STDOUT: Don't mind me, just a bit of text here...
Traceback (most recent call last):
  File "./5treams_err.py", line 5, in <module>
    raise ValueError("Now we generate an error to STDERR")
ValueError: Now we generate an error to STDERR

$ ./streams_err.py < new_file.txt 2> error_file.txt
This will come from STDIN: Now we write it to STDOUT: Don't mind me, just a bit of text here...

$ cat error_file.txt
Traceback (most recent call last):
  File "./streams_err.py", line 5, in <module>
    raise ValueError("Now we generate an error to STDERR")
ValueError: Now we generate an error to STDERR

$ echo "These are the contents of the file" > myamazingfile.txt
$ cat myamazingfile.txt
These are the contents of the file
```

```
$ ls -l | less
total 3444
-rw-r--r-- 1 user user 273 Jan 5 14:47 areas.py
-rw-r--r-- 1 user user 134 Jan 6 11:31 by_department.csv
-rwxr-xr-x 1 user user 96 May 12 2019 capitalize.py
-rwxr-xr-x 1 user user 151 May 24 2019 capitalize_words.py
-rwxr-xr-x 1 user user 425 May 19 2019 charfreq.py
-rwxr-xr-x 1 user user 400 Jan 8 09:19 check_cron.py
-rwxr—xr-x 1 user user 126 May 12 2019 check_localhost.sh
-rwxr-xr-x 1 user user 263 Jun 14 2019 create_file.py
-rw-r--r-- 1 user user 165 Jun 14 2019 csv_file.txt
drwxr-xr-x 2 user user 4096 Jun 16 2019 Desktop
drwxr-xr-x 2 user user 4096 Mar 6 2019 Documents
drwxr-xr-x 3 user user 4096 Jun 23 2019 Downloads
-rw-r--r-- 1 user user 188 Jan 9 07:24 error_file.txt
-rw-r--r-- 1 user user 17 Jan 7 14:22 example
drwxr-xr-x 3 user user 4096 Jun 17 2019 final
-rw-r--r-- 1 user user 0 Jun 17 2019 finished_masterpiece.txt
-rwxr-xr-x 1 user user 76 Jun 14 2019 fruits.sh
-rwxr-xr-x 1 user user 147 Jun 17 2019 gather-information.sh
-rw-r--r-- 1 user user 25 May 12 2019 greeting.txt
~rw-r--r-- 1 user user 67 May 12 2019 haiku.txt
-rwxr-xr-x 1 user user 368 Jan 6 07:52 health_checks.py
~rwxr-xr-x 1 user user 89 May 12 2019 hello.py
-rwxr-xr-x 1 user user 46 Jan 5 13:53 hello_world.py
-rw-r--r-- 1 user user 59 Jan 6 11:13 hosts.csv
-rw-r--r-- 1 user user 3303415 May 11 2019 houses.jpg

$ cat spider.txt | tr ' ' '\n' | sort | uniq -c | sort -nr | head
7 the
3 up
3 spider
3 and
2 rain
2 itsy
2 climbed
2 came
2 bitsy
1 waterspout.

$ cat capitalize.py
#!/usr/bin/env python3
import sys
for line in sys.stdin:
  print(line.strip().capitalize())

$ cat haiku.txt
advance your career,
automating with Python,
it's so fun to learn.

$ cat haiku.txt | ./capitalize.py
Advance your career,
Automating with python,
It's so fun to learn.

$ ./capitalize.py < haiku.txt
Advance your career,
Automating with python,
It's so fun to learn.
```

```
$ ping www.example.com
PING www.example.com(2606:2800:220:1:248:1893:25c8:1946 (2606:2800:220:1:248:1893:25c8:1946)) 56 data byt
es
64 bytes from 2606:2800:220:1:248:1893:25c8:1946 (2606:2800:220:1:248:1893:25c8:1946): icmp_seq=1 ttl=56
time=564 ms
64 bytes from 2606:2800:220:1:248:1893:25c8:1946 (2606:2800:220:1:248:1893:25c8:1946): icmp_seq=2 ttl=56
time=5.07 ms
64 bytes from 2606:2800:220:1:248:1893:25c8:1946 (2606:2800:220:1:248:1893:25c8:1946): icmp_seq=3 ttl=56
time=27.10 ms
64 bytes from 2606:2800:220:1:248:1893:25c8:1946 (2606:2800:220:1:248:1893:25c8:1946): icmp_seq=4 ttl=56
time=5.91 ms
...
^C # Bitirip rapor verir
--- www.example.com ping statistics ---
21 packets transmitted, 21 received, 0% packet loss, time 168ms
rtt min/avg/max/mdev = 5.201/7.029/22.700/3.340 ms

^Z # Direk durdurur. Durduktan sonra fg ile devam edebiliyor.
Terminated

```

```
$ cat gather-information.sh
echo "Starting at: $(date)"
echo
echo "UPTIME"
uptime
echo
echo "FREE"
free
echo
echo "WHO"
who
echo
echo "Finishing at: $(date)"

$ ./gather-information.sh
Starting at: Thu 09 Jan 2020 08:12:35 AM PST
UPTIME
08:12:35 up 3 days, 20:56, 1 user, load average: 0.07, 0.02, 0.00
FREE
       total      used     free     shared   buff/cache   available
Mem:  7841988   1285096   3884428   253228   2672464       5998856
Swap: 2097148      0      2097148
WHO
user tty7 2020-01-05 11:16 (:0)
Finishing at: Thu 09 Jan 2020 08:12:35 AM PST

echo "Starting at: $(date)"; echo # Same thing
echo "UPTIME"; uptime; echo
echo "FREE"; free; echo
echo "WHO"; who; kcho
echo "Finishing at: $(date)"

```

```
$ example=hello
$ echo $example
hello

$ cat gather-information.sh # line eklendi.
line="------------------------------"
echo "Starting at: $(date)"; echo $line
echo "UPTIME"; uptime; echo $line
echo "FREE"; free; echo $line
echo "WHO"; who; echo $line
echo "Finishing at: $(date)"

$ ./gather-information.sh
Starting at: Thu 09 Jan 2020 08:24:42 AM PST
------------------------------
UPTIME
08:24:42 up 3 days, 21:08, 1 user, load average: 0.00, 0.00, 0.00
------------------------------
FREE
total used free shared buff/cache available
Mem: 7841988 1325352 3839336 257076 2677300 5954752
Swap: 2097148 0 2097148
------------------------------
WHO
user tty7 2020-01-05 11:16 (:0)
------------------------------
Finishing at: Thu 09 Jan 2020 08:24:42 AM PST

$ echo *.py
areas.py capitalize.py capitalize_words.py charfreq.py check_cron.py create_file.py health_checks.py hell
o.py hello_world.py myapp.py parameters.py random-exit.py rearrange.py rearrange_test.py seconds.py stdou
t_example.py streams_err.py streams.py validations.py validations_test.py variables.py

$ echo *
areas.py by_department.csv capitalize.py capitalize_words.py charfreq.py check_cron.py check_localhost.sh
create_file.py csv_file.txt Desktop Documents Downloads error_file.txt example final finished_masterpiec
e.txt fruits.sh gather-information.sh greeting.txt haiku.txt health_checks.py hello.py hello_world.py hos
ts.csv houses.jpg Music myamazingfile.txt myapp.py new_dir new_file.txt old_website parameters.py Picture
5 Public __pycache__ random-exit.py rearrange.py rearrange_test.py retry.sh seconds.py snippets software.
csv spider.txt stdout_example.py story.txt streams_err.py streams.py syslog Templates toploglines.sh vali
dations.py validations_test.py variables.py Videos website while.sh

$ echo c*
capitalize.py capitalize_words.py charfreq.py check_cron.py check_localhost.sh create_file.py csv_file.tx
t

$ echo ?????.py
areas.py hello.py myapp.py
```

```
$ cat check_localhost.sh
#!/bin/bash

if grep "127.0.0.1" /etc/hosts; then
    echo "Everything ok"
else
    echo "ERROR! 127.0.0.1 is not in /etc/hosts"
fi

$ ./check_localhost.sh
127.0.0.1 localhost
Everything ok

$ if test -n "$PATH"; then echo "Your path is not empty"; fi
Your path is not empty

if ['-n "$PATH" ]; then echo "Your path is not empty"; fi
Your path is not empty
```

```
$ cat while.sh
n=1
while [ $n -le 5 ]; do
  echo "Iteration number $n"
  ((n+=1))
done

$ ./while.sh
Iteration number 1
Iteration number 2
Iteration number 3
Iteration number 4
Iteration number 5

$ cat random-exit.py
import sys
import random
value=random.randint(0, 3)
print("Returning: " + str(value))
sys.exit(value)

$ ./random-exit.py
Returning: 1
$ ./random-exit.py
Returning: 2
$ ./random-exit.py
Returning: 3

$ atom retry.sh
n=0
command=$1
while ! $command && [ $n -le 5 ]; do
  sleep $n
  ((n=n+1))
  echo "Retry #$n"
done;

$ ./retry.sh ./random-exit.py
Returning: 1
Retry #1
Returning: 3
Retry #2
Returning: 1
Retry #3
Returning: 0 
```

```
$ cat fruits.sh

for fruit in peach orange apple; do
echo "I like $fruit!"
done

$ ./fruits.sh
I like peach!
I like orange!
I like apple!

$ cd old_website/
old_website$ ls -l
total 0
-rw-r--r-- 1 user user 0 May 24 2019 about.HTM
-rw-r--r-- 1 user user 0 May 24 2019 contact.HTM
-rw-r--r-- 1 user user 0 May 24 2019 footer.HTM
-rw-r--r-- 1 user user 0 May 24 2019 header.HTM
-rw-r--r-- 1 user user 0 May 24 2019 index.HTM

old_website$ cat rename.sh
for file in "*.HTM"; do
  name=$(basename "sfile" .HTM)
  echo mv "Sfile" "Sname.html" # değişimi görmek için echo ekledik.
done

old_website$ chmod +x rename.sh
old_website$ ./rename.sh
mv about.HTM about.html
mv contact.HTM contact.html
mv footer.HTM footer.html
mv header.HTM header.html
mv index.HTM index.html # değişim uygun.

old_website$ cat rename.sh
for file in "*.HTM"; do
  name=$(basename "sfile" .HTM)
  mv "Sfile" "Sname.html" #echo'yu sildik.
done

old_website$ rename.sh
old_website$ ls -l
total 4
-rw-r--r-- 1 user user 0 May 24 2019 about.html
-rw-r--r-- 1 user user 0 May 24 2019 contact.html
-rw-r--r-- 1 user user 0 May 24 2019 footer.html
-rw-r--r-- 1 user user 0 May 24 2019 header.html
-rw-r--r-- 1 user user 0 May 24 2019 index.html
-rwxr-xr-x 1 user user 98 Jan 9 09:44 rename.sh
```

```
$ tail /var/log/syslog
Jan 9 09:32:59 ubuntu anacron[5170]: Anacron 2.3 started on 2020-01-09
Jan 9 09:32:59 ubuntu anacron[5170]: Normal exit (0 jobs run)
Jan 9 09:32:59 ubuntu systemd[1]: anacron.service: Succeeded.
Jan 9 09:34:26 ubuntu snapd[708]: autorefresh.go:382: Cannot prepare auto-refresh change: cannot refresh
snap-declaration for "gnome-characters": Get https://api.snapcraft.io/api/vl/snaps/assertions/snap-decla
ration/16/chS3UjpF9AMJKNAinASEwbm0y6Uduw2max-format=3: x509: certificate has expired or is not yet vali
d
Jan 9 09:34:26 ubuntu snapd[708]: stateengine.go:102: state ensure error: cannot refresh snap-declaratio
n for "gnome-characters": Get https://api.snapcraft.io/api/vl/snaps/assertions/snap-declaration/16/ch53U
jpF9AMJKwAinA5Eme0y6Uduw?max-format=3: x509: certificate has expired or is not yet valid
Jan 9 09:38:33 ubuntu dbus-daemon[632]: [system] Activating via systemd: service name='org.freedesktop.h
ostname1' unit='dbus-org.freedesktop.hostname1.service' requested by ':1.798' (uid=1000 pid=4640 comm="/u
sr/share/atom/atom --executed-from=/home/user --" label="unconfined")
Jan 9 09:38:33 ubuntu systemd[1]: Starting Hostname Service...
Jan 9 09:38:33 ubuntu dbus-daemon[632]: [system] Successfully activated service 'org.freedesktop.hostnam
e1'
Jan 9 09:38:33 ubuntu systemd[1]: Started Hostname Service.
Jan 9 09:39:03_ubuntu systemd[1]: systemd-hostnamed.service: Succeeded.

$ tail /var/log/syslog | cut -d' ' -f5-
ubuntu anacron[5170]: Anacron 2.3 started on 2020-01-09
ubuntu anacron[5170]: Normal exit (0 jobs run)
ubuntu systemd[1]: anacron.service: Succeeded.
ubuntu snapd[708]: autorefresh.go:382: Cannot prepare auto-refresh change: cannot refresh snap-declaratio
n for "gnome-characters": Get https://api.snapcraft.io/api/vl/snaps/assertions/snap-declaration/16/chS3U
jpF9AMJKNAinASEwbm0y6Uduw2max-format=3: x509: certificate has expired or is not yet valid
ubuntu snapd[708]: stateengine.go:102: state ensure error: cannot refresh snap-declaration for "gnome-cha
racters": Get https://api.snapcraft.io/api/v1/snaps/assertions/snap-declaration/16/chS3UjpF9AMJKwAinA5E
me0y6Uduw2max-f0rmat=3: x509: certificate has expired or is not yet valid
ubuntu dbus-daemon[632]: [system] Activating via systemd: service name='org.freedesktop.hostname1' unit='
dbus-org.freedesktop.hostname1.service‘ requested by ':1.798' (uid=1000 pid=4640 comm="/usr/share/atom/at
om --executed-from=/home/user --" label="unconfined")
ubuntu systemd[1]: Starting Hostname Service...
ubuntu dbus-daemon[632]: [system] Successfully activated service 'org.freedesktop.hostname1'
ubuntu systemd[1]: Started Hostname Service.
ubuntu systemd[1]: systemd-hostnamed.service: Succeeded.

$ cut -d' ' -f5- /var/log/syslog | sort | uniq -c | sort -nr | head
8 ubuntu dhclient[3203]: DHCPREQUEST for 100.83.177.199 on wlp4s0 to 100.109.105.22 port 67 (xid=0x
337b618)
8 ubuntu dhclient[3203]: DHCPREQUEST for 100.83.177.199 on wlp450 to 100.108.132.199 port 67 (xid=0
x337b618)
7 ubuntu systemd[2302]: tracker-extract.service: Succeeded.
7 ubuntu systemd[2302]: Starting Tracker metadata extractor...
7 ubuntu systemd[2302]: Started Tracker metadata extractor.
7 ubuntu dbus-daemon[2411]: [session uid=1000 pid=2411] Successfully activated service 'org.freedes
ktop.Tracker1.Miner.Extract'
7 ubuntu dbus-daemon[2411]: [session uid=1000 pid=2411] Activating via systemd: service name='org.f
reedesktop.Tracker1.Miner.Extract' unit='tracker-extract.service' requested by ':1.48' (uid=1000 pid=4038
comm="/usr/lib/tracker/tracker-miner-fs " label="unconfined")
6 ubuntu systemd[2302]: This usually indicates unclean termination of a previous run, or service im
plementation deficiencies.
5 ubuntu systemd-resolved[577]: Server returned error NXDOMAIN, mitigating potential DNS violation
DVE-2018-0001, retrying transaction with reduced feature level UDP.
4 ubuntu systemd[1]: anacron.service: Succeeded.

$ cat toploglines.sh
#!/bin/bash
for logfile in /var/log/*log; do
  echo "Processing: $logfile"
  cut -d' ' -f5- Slogfile | sort | uniq -c | sort -nr | head -5
done

$ ./toploglines.sh
  1 ubuntu kernel: [84667.432410] [drm] Reducing the compressed framebuffer size. This may lead to le
ss power savings than a non-reduced-size. Try to increase stolen memory size if available in BIOS.
  1 ubuntu kernel: [71292.953455] wlp450: Limiting TX power to 36 (36 - 0) dBm as advertised by 70:3a
:0e:45:31:11
  1 ubuntu kernel: [71292.678418] IPv6: ADDRCONF(NETDEV_CHANGE): wlp450: link becomes ready
  1 ubuntu kernel: [71292.677577] wlp450: associated
Processing: /var/log/lastlog
  1
Processing: /var/log/sddm.log
Processing: /var/log/syslog
  9 ubuntu dhclient[3203]: DHCPREQUEST for 100.83.177.199 on wlp450 to 100.108.132.199 port 67 (xid=0
X337b618)
  8 ubuntu dhclient[3203]: DHCPREQUEST for 100.83.177.199 on wlp450 to 100.109.105.22 port 67 (xid=0x
3376618)
  7 ubuntu systemd[2302]: tracker-extract.service: Succeeded.
  7 ubuntu systemd[2302]: Starting Tracker metadata extractor...
  7 ubuntu systemd[2302]: Started Tracker metadata extractor.
Processing: /var/log/tallylog
cut: /var/log/tallylog: Permission denied
Processing: /var/log/Xorg.0.log
  88
  75 - Synaptics TM3072-003: kernel bug: Touch jump detected and discarded.
  25 Printing DDC gathered Modelines:
  16 Modeline "2560x1440"x0.0 237.80 2560 2608 2640 2720 1440 1442 1445 1457 +hsync -vsync (87.4 kH
z eP) 
  16 EDID vendor "LGD", prod id 1049
```

```
$ for i in $(cat story.txt); do B=`echo -n "${i:0:1}" | tr "[:lower:]" "[:upper:]"`; echo -n
"${B}${i:1} "; done; echo -e "\n"
Once Upon A Time There Has An Egg Of A Programming Language Called Python

$ cat capitalize_words.py
#!/usr/bin/env python3
import sys
for line in sys.stdin:
  words = line.strip().split()
  print(" ".join([word.capitalize() for word in words]))

$ cat story.txt | ./capitalize_words.py
Once Upon A Time There Was An Egg Of A Programming Language Called Python
```

