# Skipping the Staging Area

```
$ cd scripts


scripts$ atom all_checks.py
import os
impodt sys # eklendi

def check_reboot():
  """Returns True if the computer has a pending reboot."""
  return os.path.exist("/run/reboot-required")

def main():
  if check_reboot():
    print("Pending Reboot.") # değişti
    sys.exit(1) # değişti

main()


scripts$ git commit -a -m "Call check_reboot from main, exit with 1 on error"
[master fd0b38f] Call check_reboot from main, exit with 1 on error
1 file changed, 4 inseetions(+), 1 deletion(-)


scripts$ git log
commit fd0b38f72fd36d1ef764bba509F543e3b4d4406f (HEAD -> master)
Author: My name <me@example.com>
Date: Sun Jan 5 16:14:18 2020 -0800

  Call check_reboot from main, exit with 1 on error

commit 4a713b8df5cc6dcde7a7435e103952fe03866cc2
Author: My name <me@example.com>
Date: Sun Jan 5 15:34:16 2020 ~0800

  Add a check_reboot function

commit 46a2a6fcb685471c9539e7025700eae4927fec3e
Author: My name <me@example.com>
Date: Sun Jan 5 15:26:16 2020 -0800

  Create an empty all_checks.py
```
 
<br>
 
# Getting More Information About Our Changes

```
scripts$ git log -p
commit fd0b38f72fd36d1ef764bba509f543e3b4d4406f (HEAD -> master)
Author: My name <me@example.com>
Date: Sun Jan 5 16:14:18 2020 -0800
  Call check_reboot from main, exit with 1 on error

diff --git a/all_checks.py b/all_checks.py
index 69b2337..0e1677c 100755
--- a/all_checks.py
+++ b/all_checks.py
#!/usr/bin/env python3
import os
import sys

def check_reboot():
  """Returns True if the computer has a pending reboot."""
  return os.path.exist("/run/reboot-required")
def main():
  - pass
  + print("Pending Reboot.") 
  + sys.exit(1) 

main()


scripts$ git log
commit fd0b38f72fd36d1ef764bba509f543e3b4d4406f (HEAD -> master)
Author: My name <me@example.com>
Date: Sun Jan 5 16:14:18 2020 -0800

  Call check_reboot from main, exit with 1 on error

commit 4a713b8df5cc6dcde7a7435e103952fe03866cc2
Author: My name <me@example.com>
Date: Sun Jan 5 15:34:16 2020 -0800

  Add a check_reboot function

commit 46a2a6fcb685471c9539e7025700eae4927fec3e
Author: My name <me@example.com>
Date: Sun Jan 5 15:26:16 2020 -0800

  Create an empty all_checks.py


scripts$ git show 4a713b8df5cc6dcde7a7435e103952fe03866cc2|
commit 4a713b8df5cc6dcde7a7435e103952fe03866cc2
Author: My name <me@example.com>
Date: Sun Jan 5 15:34:16 2020 -0800

  Add a check_reboot function

diff --git a/all_checks.py b/all_checks.py

index 1fa2598..69b2337 100755

--- a/all_checks.py
+++ b/all_checks.py
@@ -1,6 +1,11 @@

#!/usr/bin/env python3

+ import os 
+ 
+ 
+  """Returns True if the computer has a pending reboot."""
+  return os.path.exist("/run/reboot-required")

def main():
  pass

- main()
+ main()


scripts$ git log --stat
commit fd0b38f72fd36d1ef764bba509f543e3b4d4406f (HEAD -> master)
Author: My name <me@example.com>
Date: Sun Jan 5 16:14:18 2020 -0800

  Call check_reboot from main, exit with 1 on error

all_checks.py | 5 ++++-
1 file changed, 4 insertions(+), 1 deletion(-)

commit 4a713b8df5cc6dcde7a7435e103952fe03866cc2
Author: My name <me@example.com>
Date: Sun Jan 5 15:34:16 2020 -0800

  Add a check_reboot function

all_checks.py | 7 ++++++-
1 file changed, 6 insertions(+), 1 deletion(-)

commit 46a2a6fcb685471c9539e7025700eae4927fec3e
Author: My name <me@example.com>
Date: Sun Jan 5 15:26:16 2020 -0800

  Create an empty all_checks.py

all_checks.py | 6 ++++++
1 file changed, 6 insertions(+)


scripts$ atom all_checks.py
import os
import sys

def check_reboot():
  """Returns True if the computer has a pending reboot."""
  return os.path.exist("/run/reboot-required")

def main():
  if check_reboot():
    print("Pending Reboot.")
    sys.exit(1)
  print("Everything ok.") # eklendi
  sys.exit(0) # eklendi
main()


scripts$ git diff
diff --git a/all_checks.py b/all_checks.py
index 0e1677c..ded7196 100755
--- a/all_checks.py
+++ b/all_checks.py

@@-10,5 +10,7@@ def main():

if check_reboot():

print("Pending Reboot.")
sys.exit(1)

main() 


scripts$ git add -p
diff --git a/all_checks.py b/all_checks.py
index 0e1677c..ded7196 100755
--- a/all_checks.py
+++ b/all_checks.py

@@-10,5 +10,7@@ def main():

if check_reboot():

print("Pending Reboot.")
sys.exit(1)

main() 

Stage this hunk [y,n,q,a,d,e,?]? y


scripts$ git diff --staged
diff --git a/all_checks.py b/all_checks.py
index 0e1677c..ded7196 100755
--- a/all_checks.py
+++ b/all_checks.py

@@-10,5 +10,7@@ def main():

if check_reboot():

print("Pending Reboot.")
sys.exit(1)

main() 


scripts$ git commit -m 'Add a message when everything is ok'
[master 536558e] Add a message when everything is ok
1 file changed, 2 insegtions(+)
```
 
<br>
 
# Deleting and Renaming Files

```
$ cd checks/


checks$ ls -l
total 8
-rwxr-xr—x 1 user user 658 Jan 5 14:47 disk_usage.py
-rwxr—xr-x 1 user user 658 Jan 6 07:13 process.py


checks$ git rm process.py
rm 'process.py'


checks$ ls -l
total 4
-rwxr-xr—x 1 user user 658 Jan 5 14:47 disk_usage.py


checks$ git status
On branch master
Changes to be committed:
(use "git reset HEAD <file>..." to unstage)
  deleted: process.py


checks$ git commit -m 'Delete unneeded processes file'
[master 0d5a271] Delete unneeded processes file
1 file changed, 23 deletions(-)
delete mode 100755 process.py


checks$ git mv disk_usage.py check_free_space.py


checks$ git status
On branch master
Changes to be committed:
(use "git reset HEAD <file>..." to unstage)
  renamed: disk_usage.py -> check_free_space.py


checks$ git commit -m 'New name for disk_usage.py'
[master 30e7071] New name for disk_usage.py —
1 file changed, 0 insertions(+), 0 deletions(-)
rename disk_usage.py => check_free_space.py (100%)


checks$ echo .DS_STORE > .gitignore


checks$ ls -la
total 20
drwxr-xr-x 3 user user 4096 Jan 6 07:41 .
drwxr—xr-x 30 user user 4096 Jan 5 15:18 ..
-rwxr-xr-x 1 user user 658 Jan 5 14:47 check_free_space.py
drwxr-xr-x 8 user user 4096 Jan 6 07:37 .git
-rw-r--r—- 1 user use: 10 Jan 6 07:41 .gitignore


checks$ git add .gitignore


checks$ git commit -m 'Add a gitignore file, ignoring .DS_STORE files'
[master bb9bd78] Add a gitignore file, ignoring .DS_STORE files
1 file changed, 1 insertion(+)
create mode 100644 .gitignore
```
 
<br>
 
# Undoing Changes Before Committing

```
$ cd scripts


scripts$ atom all_checks.py
import os
import sys

# check_reboot silindi.
def check_reboot():
  """Returns True if the computer has a pending reboot."""
  return os.path.exist("/run/reboot-required")
  
def main():
  if check_reboot():
    print("Pending Reboot.")
    sys.exit(1)
  
  print("Everything ok.")
  sys.exit(0)

main()


scripts$ ./all_checks.py
Traceback (most recent call last):
  File "./all_checks.py", line 12, in <module>
    main()
  File "./all_checks.py", line 6, in main
    if check_reboot():
NameError: name 'check_reboot' is not defined


# hata alındığı için işlemi iptal edeceğiz.
scripts$ git status
On branch master
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git checkout -- <file>..." to discard changes in working directory)
    modified: all_checks.py
no changes added to commit (use "git add" and/or "git commit -a")


# işlemler geri çekildi.
scripts$ git checkout all_checks.py 


scripts$ git status
On branch master
nothing to commit, working tree clean


# Hala hata devam ediyor
scripts$ ./all_checks.py
Traceback (most recent call last):
  File "./all_checks.py", line 16, in <module>
    main()
  File "./all_checks.py", line 10, in main
    if check_reboot():
  File "./all_checks.py", line 7, in check_reboot
    return os.path.exist("/run/reboot-required")
AttributeError: module 'posixpath' has no attribute 'exist'


# exist kısmı exists olarak değiştirildi.
scripts$ atom all_checks.py
import os
import sys

def check_reboot():
  """Returns True if the computer has a pending reboot."""
  return os.path.exists("/run/reboot-required")

def main():
  if check_reboot():
    print("Pending Reboot.")
    sys.exit(1)
  print("Everything ok")
  sys.exit(0)

main()


scripts$ ./all_checks.py
Everything ok.


scripts$ ./all_checks.py > output.txt


scripts$ git add *


scripts$ git status
On branch master
Changes to be committed:
(use "git reset HEAD <file>..." to unstage)
  modified: all_checks.py
  new file: output.txt


scripts$ git reset HEAD output.txt


scripts$ git status 
On branch master
Changes to be committed:
(use "git reset HEAD <file>..." to unstage)
  modified: all_checks.py
Untracked files:
(use "git add <file>..." to include in what will be committed)
  output.txt


scripts$ git commit -m "it should be os.path.exists"
```
 
<br>
 
# Amending Commits

Avoid amending commits that have already
been made public.

```
$ Cd scripts/


scripts$ touch auto-update.py


scripts$ touch gather-information.sh


scripts$ ls -l
total 8
-rwxr-xr-x 1 user user 317 Jan 6 08:08 all_checks.py
-rw-r--r-- 1 user user 0 Jan 6 08:27 auto-update.py
-rw-r--r-- 1 user user 0 Jan 6 08:27 gather-information.sh
-rw-r--r-- 1 user user _15 Jan 6 08:14 output.txt


scripts$ git add auto-update.py # auto-update eklendi ama gather-information eklenmedi.


scripts$ git commit -m 'Add two new scripts'
[master 919d809] Add two new scripts
1 file changed, 0 insertions(+), 0 deletions(-)
create mode 100644 auto-update.py


scripts$ git add gather-information.sh


scripts$ $ git commit --amend # amend ile daha önce eklemediğimiz gather-informationdosyasını ekledik.
Add two new scripts
gather-information.sh will be used to collect information in case of errors.
auto-update.py will be run daily to update computers automatically.
# Please enter the commit message for your changes. Lines starting
# with '#' will be ignored, and an empty message aborts the commit.
#
# Date: Mon Jan 6 08:28:17 2020 ~0800
#
# 0n branch master
# Changes to be committed:
# new file: auto-update.py
# new file: gather-information.sh
#
# Untracked files:
# output.txt
#

[master f910c59] Add two new scripts.
Date: Mon Jan 6 08:28:17 2020 -0800
2 files changed, 0 insertions(+), 0 deletions(~)
create mode 100644 auto-update.py
create mode 100644 gather-information.sh
```
 
<br>
 
# Rollbacks

```
$ cd scripts


scripts$ cat all_checks.py
import os
import sys

def check_reboot():
  """Returns True if the computer has a pending reboot."""
  return os.path.exists("/run/reboot-required")

def main():
  if check_reboot():
    print("Pending Reboot.")
    sys.exit(1) 
  # if disk_full eklendi.
  if disk_full():
    print("Disk Full.")
    sys.exit(1) 
  print("Everything ok.")
  sys.exit(0)

main()


scripts$ git commit -a -m 'Add call to disk_full function'
[master 5aab0fd] Add call to disk_full function
1 file changed, 3 insertions(+)


scripts$ ./all_checks.py # disk_full tanımlı değil
Traceback (most recent call last):
  File "./all_checks.py", line 19, in <module>
    main()
  File "./all_checks.py", line 13, in main
    if disk_full():
NameError: name 'disk_full' is not defined


scripts$ git revert HEAD
Revert "Add call to disk_full function"

Reason for rollback: the disk_full function is undefined.

This reverts commit 5aab0fd2579f187728d8aff556c3a67e73becfc5.

# Please enter the commit message for your changes. Lines starting
# with '#' will be ignored, and an empty message aborts the commit.
#
# On branch master
# Changes to be committed:
#   modified: all_checks.py
# Untracked files:
# output.txt
#


[master 0832461] Revert "Add call to disk_full function"
1 file changed, 3 deletions(-)


scripts$ git log -p -2
commit 0832461c845b98c7a58fc8c26922fe47eab2b8c4 (HEAD -> master)
Author: My name <me@example.com>
Date: Mon Jan 6 08:41:17 2020 -0800
  Revert "Add call to disk_full function"
  Reason for rollback: the disk_full function is undefined.
  This reverts commit Saab0fd2579f187728d8aff556c3a67e73becfc5.
diff —-git a/all_checks.py b/all_checks.py
index 21058b4..6e2b66b 100755
--- a/all_checks.py
+++ b/all_checks.py
@@ -10,9 +10,6 @@ def main():
if check_reboot():
  print("Pending Reboot.")
  sys.exit(1),
- if disk_full():
-     print("Disk Full.")
-     sys.exit(1) 
print("Everything ok.")
sys.exit(0)


commit Saab0fd2S79f187728d8aff556c3a67e73becfc5
Author: My name <me@example.com>
Date: Mon Jan 6 08:40:18 2020 -0800
  all to disk_full function
diff --git a/all_checks.py b/all_checks.py
index 6e2b66b..21058b4 100755
--- a/all_checks.py
+++ b/all_checks.py
@@ -10,9 +10,6 @@ def main():
if check_reboot():
  print("Pending Reboot.")
  sys.exit(1)
+ if disk_full():
+     print("Disk Full.")
+     sys.exit(1) 
print("Everything ok.") 
sys.exit(0)
```
 
<br>
 
# Identifying a Commit


```
checks$ git log -2
commit bb9bd7872709e9f2bbf58bf7f76203c8017b1503 (HEAD -> master)
Author: My name <me@example.com>
Date: Mon Jan 6 07:43:32 2020 -0800
Add a gitignore file, ignoring .DS_STORE files

commit 30e70712882267ca2dd749acfa02ea3aacfd0b24
Author: My name <me@example.com>
Date: Mon Jan 6 07:37:24 2020 -0800
New name for disk_usage.py


checks$ git show 30e70712882267ca2dd749acf302ea3aacfd0b24
commit 30e70712882267ca2dd749acf802ea3aacfd0b24
Author: My name <me@example.com>
Date: Mon Jan 6 07:37:24 2020 -0800
  New name for disk_usage.py
diff --git a/disk_usage.py b/check_free_space.py
similarity index 100%
rename from disk_usage.py
rename to check_free_space.py


checks$ git revert 30e70712882267ca2dd749acf302ea3aacfd0b24
Revert "New name for disk_usage.py"

Rollback reason: the previous name was actually better :)

This reverts commit 30e70712882267ca2dd749acfa02ea3aacfd0b24.
# Please enter the commit message for your changes. Lines starting
# with '#' will be ignored, and an empty message aborts the commit.
#
# On branch master
# Changes to be committed:
# renamed: check_free_space.py -> disk_usage.py
#


[master 7d1de19] Revert "New name for disk_usage.py"
1 file changed, 0 insertions(+), 0 deletions(-) 
rename check_free_space.py => disk_usage.gy (100%)"


checks$ git show 7d1de19
commit 7d1de19371d54966bb5e374f3c78f38520918114 (HEAD -> master)
Author: My name <me@example.com>
Date: Mon Jan 6 09:15:58 2020 -0800
  Revert "New name for disk_usage.py"
  Rollback reason: the previous name was actually better :)
  This reverts commit 30e70712882267ca2dd749acfa02ea3aacfd0b24.
diff --git a/check_free_space.py b/disk_usage.py
similarity index 100%
rename from check_free_space.py
rename to disk usage.py
```

<br>
 
# Creating New Branches

```
$ cd checks


checks$ git branch
* master


checks$ git branch new-feature


checks$ git branch
* master
new-feature


checks$ git checkout new-feature
Switched to branch 'new-feature'


checks$ git checkout -b even-better-feature
Switched to a new branch 'even-better-feature'


checks$ atom free_memory.py
def main():
  pass

main()


checks$ git add free_memory.py


checks$ git commit -m 'Add an empty free_memory.py'
[even-better-feature 4361880] Add an empty free_memory.py
1 file changed, 6 insertions(+)
create mode 100644 free_memory.py


checks$ git log -2 
commit 436188012f633b773eb6034fc02051e34da05134 (HEAD -> even-better-feature)
Author: My name <me@example.com>
Date: Mon Jan 6 09:47:07 2020 -0800

  Add an empty free_memory.py

commit 7d1de19371dS4966bb5e374f3c78f38520918114 (new-feature, master)
Author: My name <me@example.com>
Date: Mon Jan 6 09:15:58 2020 -0800

  Revert "New name for disk_usage.py"

  Rollback reason: the previous name was actually better :)

  This reverts commit 30e70712882267ca2dd749acfa02ea3aacfd0b24. 
```

<br>
 
# Working with Branches

```
$ cd checks


checks$ git status # even-better-feature dayız.  
On branch even-better-feature
nothing to commit, working tree clean


checks$ ls -l
total 8
-rwxr-xr-x 1 user user 658 Jan 6 09:15 disk_usage.py
~rw-r--r-- 1 user user_ 57 Jan 6 09:46 free_memory.py


checks$ git checkout master 
Switched to branch 'master'


checks$ git log -2
commit 7d1de19371dS4966bb5e374f3c78f38520918114 (HEAD -> master, new-feature)
Author: My name <me@example.com>
Date: Mon Jan 6 09:15:58 2020 -0800
  Revert "New name for disk_usage.py"
  Rollback reason: the previous name was actually better :)
  This reverts commit 30e70712882267ca2dd749acfa02ea3aacfd0b24.

commit bb9bd7872709e9f2bbf58bf7f76203c8017b1503
Author: My name <me@example.com>
Date: Mon Jan 6 07:43:32 2020 -0800
  Add a gitignore file, ignoring .DS_STORE files


checks$ ls -l # even-better-feature'da oluşturduğumuz free_memory.py master'da gözükmüyor.
total 4 n
-rwxr-xr-x 1 user user_658 Jan 6 09:15 disk_usage.py


checks$ git branch -d new-feature # branch silme
Deleted branch new-feature (was 7d1de19).


checks$ git branch # new feature silindi.
even-better-feature
* master


checks$ git branch -d even-better-feature # Yapılan çalışma master'a eklenmediği için teyit alıyor. Sileceksek 'git branch -D even-better-feature' yazarak silebiliriz.
error: The branch 'even-better-feature' is not fully merged.
If you are sure you want to delete it, run 'git branch -D even-better-feature'.
```

<br>
 
# Merging

```
checks$ git merge even-better-feature
Updating 7d1de19..4361880

Fast-forward
  free_memory.py | 6 ++++.x
  1 file changed, 6 insertions(+)
  create mode 100644 free_memory.py


checks$ git log

commit 436188012f633b773eb6034fc02051e34da05134 (HEAD, master, even-better-feature)
Author: My name <me@example.com>
Date: Mon Jan 6 09:47:07 2020 -0800
  Add an empty free_memory.py

commit 7d1de19371d54966bb5e374f3c78f38520918114
Author: My name <me@example.com>
Date: Mon Jan 6 09:15:58 2020 -0800
  Revert "New name for disk_usage.py"
  Rollback reason: the previous name was actually better :)
  This reverts comit 30e70712882267ca2dd749acfa02ea3aacfd0b24.

commit bb9bd7872709e9f2bbf58bf7f76203c8017b1503
Author: My name <me@example.com>
Date: Mon Jan 6 07:43:32 2020 -0800
  Add a gitignore file, ignoring .DS_STORE files

commit 30e70712882267ca2dd749acfa02ea3aacfd0b24
Author: My name <me@example.com>
Date: Mon Jan 6 07:37:24 2020 -0800
  New name for disk_usage.py 
```

<br>
 
# Merge Conflicts

```
checks$ atom free_memory.py
def main():
  """Checks if there's enough free memory in the computer."""

main()


checks$ git commit -a -m 'Add comment to main()'
[master fe2fc5b] Add comment to main()
1 file changed, 2 insertions(+), 2 deletions(-)


checks$ git checkout even-better-feature
Switched to branch 'even-better-feature'


checks$ atom free_memory.py
def main():
  print("Everything is ok.")

main()


checks$ git commit -a -m 'Print everything ok'


checks$ git checkout master
Switched to branch 'master'


checks$ git merge even-better-feature
Auto-merging free_memory.py
CONFLICT (content): Merge conflict in free_memory.py
Automatic merge failed; fix conflicts and then commit the result.


checks$ git status # iki branch'ta da değişiklik olduğu için çakışma var.
On branch master
You have unmerged paths.
(fix conflicts and run "git commit")
(use "git merge --abort" to abort the merge)
Unmerged paths:
(use "git add <file>..." to mark resolution)
  both modified: free_memory.py
It also tells us that we need to
no changes added to commit (use "git add" and/or "git commit -a")


checks$ atom free_memory.py
```
![Ekran görüntüsü 2024-01-31 120614](https://github.com/kemda2/Google-Courses/assets/19648132/53747a3b-3c40-4a67-9c0e-1101d87481fb)

![Ekran görüntüsü 2024-01-31 1206](https://github.com/kemda2/Google-Courses/assets/19648132/72596cda-d4ee-4b71-ac5e-5266ff7a1f04)
```
checks$ git add free_memory.py


checks$ git status
On branch master
All conflicts fixed but you are still merging.
  (use "git commit" to conclude merge)
Changes to be committed: 
  modified: free_memory.py


checks$ git commit
Merge branch 'even-better-feature'
Kept lines from both branches.

# Conflicts:
# free_memory.py
#
# It looks like you may be committing a merge.
# If this is not correct, please remove the file
# .git/MERGE_HEAD
# and try again.

# Please enter the commit message for your changes. Lines starting
# with '#' will be ignored, and an empty message aborts the commit.
#
# On branch master
# All conflicts fixed but you are still merging.
#
# Changes to be committed:
# modified: free_memory.py
#


checks$ git log --graph --oneline
* 8cb5e62 (HZRJ A; H? is?) Merge branch 'even-better-feature'
|\
|* ca6de99 (ewe:~fletfaiwf:sfris) Print everything ok
*| fe2fc5b Add comment to main()
|/ fl
* 4361880 Add an empty free_memory.py
* 7d1de19 Revert "New name for disk_usage.py"
* bb9bd78 Add a gitignore file, ignoring .DS_STORE files
* 30e7071 New name for disk_usage.py
* 0d5a271 Delete unneeded processes file
* Saada26 Adding file to delete it later
* cfb2b8e Add periods to the end of sentences.
* 21e6a1a Add new disk_usage check.
```
