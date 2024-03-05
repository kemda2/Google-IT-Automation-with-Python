# Diffing Files

```
$ cat rearrange1.py
#!/usr/bin/env python3
import re
def rearrange_name(name):
  result = re.search(r"^([\w .]*), ([\w .]*)$", name)
  if result == None:
    return result
  return "{} {}".format(result[2], result[1])

$ cat rearrange2.py
#!/usr/bin/env python3
import re
def rearrange_name(name):
  result = re.search(r""([\w .-]*), ([\w .-]*)$", name) # "-" EKLENMİŞ
  if result == None:
    return result
  return "{} {}".format(result[2], result[1])

$ diff rearrange1.py rearrange2.py
6C6
< result = re.search(r"^([\w .]*), ([\w .]*)$", name)
---
> result = re.search(r"^(|\w .-|*), ([3w .-|*)$", name)



$ diff validations1.py validations2.py

5c5,6 # 5 satır değişti, 6 satır eklendi.

< assert (type(username) == str), "username must be a string"
> if type(username) != str:
> raise TypeError("username must be a string")

11a13,15

>   return False
> # Usernames can't begin with a number
> if username[0].isnumeric():


$ diff -u validations1.py validations2.py # -u daha detaylı bir anlatım sağlıyor
--- validations1.py 2020-01-05 07:03:46.999900910 -0800
+++ validations2.py 2020-01-05 07:03:46.999900910 -0800

@@ -2,7 +2,8 @@
def validate_user(username, minlen):
- assert (type(username) == str), "username must be a string"
+ if type(username) != str:
+ raise TypeError("username must be a string")
if minlen < 1:
raise ValueError("minlen must be at least 1")

@@ -10,5 +11,8 @@
    return False
  if not username.isalnum():
    return False
+ # Usernames can't begin with a number
+ if username[0].isnumeric():
+   return False
  return True
```


# Applying The Changes

```
$ cat cpu_usage.py
import psutil
def check_cpu_usage(percent):
  usage = psutil.cpu_percent()
  return usage < percent
if not check_cpu_usage(75):
  print("ERROR! CPU is overloaded")
else:
  print("Everything ok")

diff -u old_file new_file > change.diff

$ cat cpu_usage.diff

--- cpu_usage.py 2019-06-23 08:16:04.666457429 -0700
+++ cpu_usage_fixed.py 2019-06-23 08:15:37.534370071 -0700
@@ "2:7 +2:8 @@

import psutil

def check_cpu_usage(percent):

- usage = psutil.cpu_percent(1)
+ usage = psutil.cpu_percent(1)
+ print("DEBUG: usage: {}".format(usage)) # ekleme yapılan kısım

return usage < percent
if not check_cpu_usage(75):



$ patch cpu_usage.py < cpu_usage.diff
patching file cpu_usage.py


$ cat cpu_usage.py
import psutil
def check_cpu_usage(percent):
  usage = psutil.cpu_percent(1)
  print("DEBUG: usage: {}".format(usage)) # değişiklik uygulandı
  return usage < percent
if not check_cpu_usage(75):
  print("ERROR! CPU is overloaded")
else:
  print("Everything ok")
```

# Practical Application of diff and patch

```
$ cp disk_usage.py disk_usage_original.py
$ cp disk_usage.py disk_usage_fixed.py

$ cat disk_usage.py
import shutil
def check_disk_usage(disk, min_absolute, min_percent):
  ""Returns True if there is enough free disk space, false otherwise.""'
  du = shutil.disk_usage(disk)
  percent_free = 166 * du.free / du.tota1
  gigabytes_free = du.free / 2**30
  if percent_free < min_percent or gigabytes_free < min_absolute:
    return False
  return True

if not check_disk_usage("/", 2*2**30, 10):
  print("ERROR: Not enough disk space")
  return 1
print("Everything ok")
return 0



$ ./disk_usage_fixed.py
File "./disk_usage_fixed.py", line 19
return 1
^
SyntaxError: 'return' outside function


$ cat disk_usage_fixed.py
import shutil
import sys
def check_disk_usage(disk, min_absolute, min_percent):
  """Returns True if there is enough free disk space, false otherwise.'""
  du = shutil.disk_usage(disk)
  percent_free = 100 * du.free / du.total
  gigabytes_free = du.free / 2**30
  if percent_free < min_percent or gigabytes_free < min_absolute:
    return False
  return True
if not check_disk_usage("/", 2*2**30, 10):
  print("ERROR: Not enough disk space")
  sys.exit(1)
print("Everything ok")
sys.exit(0)



$ ./disk_usage_fixed.py
ERROR: Not enough disk space



$ cat disk_usage_fixed.py
import shutil
import sys
def check_disk_usage(disk, min_absolute, min_percent):
  """Returns True if there is enough free disk space, false otherwise.'""
  du = shutil.disk_usage(disk)
  percent_free = 100 * du.free / du.total
  gigabytes_free = du.free / 2**30
  if percent_free < min_percent or gigabytes_free < min_absolute:
    return False
  return True
if not check_disk_usage("/", 2, 10):
  print("ERROR: Not enough disk space")
  sys.exit(1)
print("Everything ok")
sys.exit(0)



$ ./disk_usage_fixed.py
Everything ok



$ diff -u disk_usage_original.py disk_usage_fixed.py > disk_usage.diff 



$ cat disk_usage.diff
--- disk_usage_original.py 2020-01-05 14:04:32.7485
+++ disk_usage_fixed.py 2020-01-05 14:04:32.7485
66252 -0800

@@ -1,6 +1,7 @@

import shutil
+import sys
def check_disk_usage(disk, min_absolute, min_percent):
"""Returns True if there is enough free disk space, false otherwise."""

@@ -14,9 +15,9 @@
return True

# Check for at least 2 GB and 10% free
-if not check_disk_usage("l", 2*2**30, 10):
+if not check_disk_usage("l", 2, 10):
print("ERROR: Not enough disk space")
- return 1
+ sys.exit(1)

print("Everything ok")
-return 0 9
+sys.exit(0)


$ patch disk_usage.py < disk_usage.diff
patching file disk_usage.py



$ ./disk_usage.py
Everything ok 
```

# First Steps with Git

```
checks$ cp ../disk_usage.py 

checks$ ls -l
total 4
-rwxr-xr-x 1 user user 656 Jan 5 14:25 'i::_":¢_e _~



checks$ git add disk_usage.py



checks$ git status

On branch master

No commits yet

Changes to be committed:

  (use "git rm --cached <file>..." to unstage)

  new file: diskusage.py



checks$ git commit
Add new disk_usage check. # yorum
# Please enter the commit message for your changes. Lines starting
# with '#' will be ignored, and an empty message aborts the commit.
# On branch master
# Initial commit
# Changes to be committed:
# new file: disk_usage.py
```

# Tracking Files

```
$ cd checks



checks$ ls -l
total 4
-rwxr-xr-x 1 user user 656 Jan 5 14:25 disk_usage.py



$ git status
On branch master
nothing to commit, working tree clean


checks$ atom disk_usage.py
import shutil
import sys
def check_disk_usage(disk, min_absolute, min_percent):
  """Returns True if there is enough free disk space, false otherwise."""
  du = shutil.disk_usage(disk)
  percent_free = 160 * du.free / du.total
  gigabytes_free = du.free / 2**30
  if percent_free < min_percent or gigabytes_free < min_absolute:
    return False
  return True

if not check_disk_usage("l", 2, 10): # 2GB or %10 Free
  print("ERROR: Not enough disk space.") # space'ten sonra nokta koyduk
  sys.exit(1)

print("Everything ok")
sys.exit(O)



checks$ git status
On branch master
Changes not staged for commit:
(use "git add <file>..." to update what will be committed)
(use "git checkout -- <file>..." to discard changes in working directory)
  modified: disk_usage.py
no changes added to commit (use "git add" and/or "git commit -a")



checks$ git add disk_usage.py



checks$ git status



checks$ git status
On branch master
Changes to be committed:
(use "git reset HEAD <file>..." to unstage)
modified: disk_usage.py



checks$ git commit -m 'Add periods to the end of sentences.'
[master cfb2b8e] Add periods to the end of sentences.
1 file changed, 2 insertions(+), 2 deletions(-)
```

# The Basic Git Workflow

```
$ mkdir scripts



$ cd scripts



scripts$ git init
Initialized empty Git repository in /home/user/scripts/.git/



scripts$ git config -l
user.email=me@example.com
user.name=My name
core.repositoryformatversion=0
core.filemode=true
core.bare=false
core.logallrefupdates=true



scripts$ cat all_checks.py
def main():
  pass

main()



scripts$ chmod +x all_checks.py



scripts$ git status
On branch master
No commits yet
Untracked files:
(use "git add <file>..." to include in what will be committed)
  all_checks.py
nothing added to commit_but untracked files present (use "git add" to track)



scripts$ git add all_checks.py



scripts$ git commit
' Create an empty all_checks.py
# Please enter the commit message for your changes. Lines starting
# with '#‘ will be ignored, and an empty message aborts the commit.
#
# 0n branch master
#
# Initial commit
#
# Changes to be committed:
# new file: all_checks.py



scripts$ cat all_checks.py
# check_reboot eklendi
import os
def check_reboot():
  """Returns True if the computer has a pending reboot."""
  return os.path.exist("/run/reboot-required")

def main(): 
  pass

main()



scripts$ git status
On branch master
Changes not staged for commit:
(use "git add <file>..." to update what will be committed)
  modified: all_checks.py
(use "git checkout -- <file>..." to discard changes in working directory)
no changes added to commit (use "git add" and/or "git commit -a")



scripts$ git add all_checks.py



scripts$ git status
On branch master
Changes to be committed:
(use "git reset HEAD <file>..." to unstage)
  modified: all_checks.py



scripts$ git commit -m 'Add a check_reboot function'
[master 4a713b8] Add a check_reboot function
1 file changed, 6 insegtions(+), 1 deletion(-)
```

# Anatomy of a Commit Message

```
$ cat example_commit.txt

Provide a good commit message example

The purpose of this commit is to provide an example of a hand-crafted,
artisanal commit message. The first line is a short, approximately 50 character
summary, followed by an empty line. The subsequent paragraphs are jam-packed
with descriptive information about the change, but each line is kept under 72
characters in length.

If even more information is needed to explain the change, more paragraphs can
be added after blank lines, with links to issues, tickets, or bugs. Remember
that future you will thank current you for your thoughtfulness and foresight!
# Please enter the commit message for your changes. Lines starting

# with '#' will be ignored, and an empty message aborts the commit.
#
# On branch master
#
# Changes to be committed:
# new file: super_script.py
# new file: cool_config.txt



$  cd scripts



scripts$ git log
commit 4a713b8df5cc6dcde7a7435e103952fe03866cc2 (READ ~> master)
Author: My name <me@example.com>
Date: Sun Jan 5 15:34:16 2020 -0800
Add a check_reboot function

commit 46a2a6fcb685471c9539e7025700eae4927fec3e
Author: My name <me@example.com>
\Date: Sun Jan 5 15:26:16 2020 -0800
Create an empty all_checks.py
```
