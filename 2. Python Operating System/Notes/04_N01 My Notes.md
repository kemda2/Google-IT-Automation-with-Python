# My Notes

```
$ cat hello.py
#l/usr/bin/env python3
name = input("Please enter your name: ")
print("Hello, " + name)

$ ./hello.py
Please enter your name: Roger
Hello, Roger

$ atom seconds.py

def to_seconds(hours, minutes, seconds):
  return hours*3600+minutes*60+seconds

print("Welcome to this time converter")

cont = "y" 
while(cont.lower() == "y"):
  hours = int(input("Enter the number of hours: "))
  minutes = int(input("Enter the number of minutes: "))
  seconds = int(input("Enter the number of seconds: "))
  print("That's {} seconds".format(to_seconds(hours, minutes, seconds)))
  print()
  cont = input("Do you want to do another conversion? [y to continue] ")
print("Good bye!")

$ ./seconds.py
Welcome to this time converter
Enter the number of hours: 1
Enter the number of minutes: 2
Enter the number of seconds: 3
That's 3723 seconds

Do you want to do another conversion? [y to continue] y
Enter the number of hours: 3
Enter the number of minutes: 2
Enter the number of seconds: 1
That's 10921 seconds

Do you want to do another conversion? [y to continue] n
Good bye! 
```

```
$ cat streams.py
#!/usr/bin/env python3
data = input("This will come from STDIN: ")
print("Now we write it to STDOUT: " + data)
print("Now we generate an error to STDERR: " + data + 1)

$ ./streams.py
This will come from STDIN: Python ROCKS!!!
Now we write it to STDOUT: Python ROCKS!!!
Traceback (most recent call last):
File "./streams.py", line 5, in <module>
print("Now we generate an error to STDERR: " + data + 1)
TypeError: can only concatenate str (not "int") to str

$ cat greeting.txt
Well hello there, STDOUT

$ ls -z
ls: invalid option -- 'z'
Try 'ls --help' for more information.
```

```
$ env
VTE_VERSION=5601
XDG_SEAT_PATH=/org/freedesktop/DisplayManager/Seat0
GNOME_TERMINAL_SCREEN=/org/gnome/Terminal/screen/8fO4fe6e_ac34_4baf_a547_9160a92d54a3
GJS_DEBUG_OUTPUT=stderr
LESSCLOSE=/usr/bin/lesspipe %s %s
XDG_SESSION_CLASS=user
TERM=xterm-256color
GTK_OVERLAY_SCROLLING=0
DEFAULTS_PATH=/usr/share/gconf/cinnamon.default.path
LESSOPEN=| /usr/bin/lesspipe %s
USER=user
GNOME_TERMINAL_SERVICE=:1.196
PAM_KwALLET5_LOGIN=/run/user/iOOO/kwallets.socket
DISPLAY=:0
SHLVL=1
XDG_VTNR=7
XDG_SESSION_ID=C2
XDG_RUNTIME_DIR=/run/user/lOOO
XDG_DATA_DIRS=/usr/share/gnome:/usr/share/cinnamon:/usr/local/share:/usr/share:/var/lib/snapd/deskt
0P
PATH=/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:/usr/games:/usr/local/games:/snap
/bin
GDMSESSION=cinnamon
DBUS_SESSION_BUS_ADDRESS=unix:path=/run/user/1000/bus
_=/usr/bin/env

$ echo $PATH
/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:/usr/games:/usr/local/games:/snap/bin

$ cat variables.py
#!/usr/bin/env python3
import os
print("HOME: " + os.environ.get("HOME", ""))
print("SHELL: " + os.environ.get("SHELL", ""))
print("FRUIT: " + os.environ.get("FRUIT", ""))

$ ./variables.py
HOME: /home/user
SHELL: /bin/bash
FRUIT:

$ export FRUIT=Pineapple

$ ./variables.py
HOME: /home/user
SHELL: /bin/bash
FRUIT: Pineapple
```

```
$ cat parameters.py
#!lusr/bin/env python3
import sys
print(sys.argv)

$ ./parameters.py
['./parameters.py']

$ ./parameters.py one two three
['./parameters.py', 'one', 'two', 'three']

$ wc variables.py
7 19 174 variables.py

$ echo $
0

$ wc notpresent.py
wc: notpresent.py: No such file or directory

$ echo $
1

$ atom create_file.py
import os
import sys
filename=sys.argv[1]
if not os.path.exists(filename):
  with open(filename, "w") as f:
    f.write("New file created\n")
else:
  print("Error, the file {} already exists!".format(filename))
  sys.exit(1)

$ ./create_file.py example
$ echo $?
0

$ cat example
New file created

$ ./create_file.py example
Error, the file example already exists!

$ echo $?
1
```

```
>>> import subprocess
>>> subprocess.run(["date"])
Tue 07 Jan 2020 02:34:44 PM PST
CompletedProcess<args=['date'], returncode=0>

>>> subprocess.run(["sleep", "2"])
CompletedProcess(args=['sleep', '2'], returncode=0)

>>>" result = subprocess.run('["ls", 7'this_file_does'_not_exist"])
ls: cannot access 'this_file_does_not_exist': No such file or directory
>>> print(result.returncode)
2
```

```
>>> result = subprocess.run(["host", "8.8.8.8"], capture_output=True)
>>> print(result.returncode)
0
>>> print(result.stdout)
b'8.8.8.8.in-addr.arpa domain name pointer dns.google.\n'
>>> print(result.stdout.decode().split())
['8.8.8.8.in-addr.arpa', 'domain', 'name', 'pointer', 'dns.google.']
>>> result = subprocess.run(["rm", "does_not_exist"], capture_output:True)
>>> print(result.returncode)
1
>>> print(result.stdout)
b""
>>> print(result.stderr)
b"rm: cannot remove 'does_not_exist': No such file or directory\n"
```

```
$ atom myapp.py

import os
import subprocess
my_env = os.environ.copy()
my_env["PATH"] = os.pathsep.join(["/opt/myapp/", my_env["PATH"]])
result = subprocess.run(["myapp"], env=my_env)
```

```
import sys
logfile = sys.argv[1]
with open(logfile) as f:
  for line in f:
    print(line.strip())

$ cat syslog
Jul 6 14:01:23 computer.name CRON[29440]: USER (good_user)
Jul 6 14:02:08 computer.name jam_tag=psim[29187]: (UUID:006)
Jul 6 14:02:09 computer.name jam_tag=psim[29187]: (UUID:007)
Jul 6 14:03:01 computer.name CRON[29440]: USER (naughty_user)
Jul 6 14:03:40 computer.name cacheclient[29807]: start syncing from "0XDEADBEEF"
Jul 6 14:04:01 computer.name CRON[29440]: USER (naughty_user)
Jul 6 14:05:01 computer.name CRON[29440]: USER (naughty_user)

import sys
logfile = sys.argv[1]
with open(logfile) as f:
  for line in f:
    if "CRON" not in line: # Değişti
      continue # Değişti
    print(line.strip())

# Çalışıyor mu diye deneme
>>> import re
>>> pattern : r"USER \((\w+)\)$"
>>> line = "Jul 6 14:04:01 computer.name CRON[29440]: USER (naughty_user)"
>>> result = re.search(pattern, line)
>>> print(result[1])
naughty_user

import re # Değişti
import sys
logfile = sys.argv[1]

with open(logfile) as f:
  for line in f:
    if "CRON" not in line: # Değişti
    continue # Değişti
    
    pattern = r"USER \((\w+)\)$" # Değişti
    result = re.search(pattern, line) # Değişti
    print(result[1]) # Değişti

$ chmod +x check_cron.py
$ ./check_cron.py syslog
good_user
naughty_user
naughty_user
naughty_user
```

```
>>> usernames = {}
>>> name = "good_user"
>>> usernames[name] = usernames.get(name, 0) + 1
>>> print(usernames)
{'good_user': 1}
>>> usernames[name] = usernames.get(name, 0) +1
>>> print(usernames)
{'good_user': 2}

import re
import sys
logfile = sys.argv[1]
usernames = {} # eklendi
with open(logfile) as f:
  for line in f:
    if "CRON" not in line:
      continue
    pattern = r"USER \((\w+)\)$"
    result = re.search(pattern, line)!
    if result is None: # eklendi
      continue # eklendi
    name = result[1] # eklendi
    usernames[name] = usernames.get(name, 0) + 1 # eklendi
    print(result[1]) # çıkarıldı
print(usernames)

$ ./check_cron.py syslog
{'good_user': 1, 'naughty_user': 3}

```

```

```
