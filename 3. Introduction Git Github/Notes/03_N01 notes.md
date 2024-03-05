# Introduction to GitHub

## Basic Interaction with GitHub

```
$ git clone https://github.com/redquinoa/health-checks.git 
Cloning into 'health-checks'...
Username for 'https://github.com': redquinoa
Password for 'https://redquinoa@github.com':
remote: Enumerating objects: 3, done.
remote: Counting objects: 100% (3/3), done.
remote: Compressing objects: 100% (2/2), done.
remote: Total 3 (delta 0), reused 0 (delta 0), pack-reused 0
Unpacking objects: 100% (3/3), done.


$ cd health-checks/


health-checks$ ls -l
total 4
-rw-r--r-- 1 user user 62 Jan_ 6 14:06 README.md


health-checks$ atom README.md
# health-checks
Scripts that check the health of my computers

This repo will be populated with lots of fancy checks.


health-checks$ git commit -a -m "Add one more line to README.md"
[master 807cb50] Add one more line to README.md
1 file changed, 2 insertions(+)


health-checks$ git push # değişiklik github'a eklendi
Username for 'https://github.com': redquinoa
Password for 'https://redquinoa@github.com':
Enumerating objects: 5, done.
Counting objects: 100% (5/5), done.
Delta compression using up to 4 threads
Compressing objects: 100% (2/2), done.
Writing objects: 100% (3/3), 347 bytes | 347.00 KiB/s, done.
total 3 (delta 0), reused 0 (delta 0)
To https://github.com/redquinoa/health-checks.git
    3d9f86c..807cb50 master -> master 


health-checks$ git config --global credential.helper cache #şifre sormasın diye


health-checks$ git pull
Username for 'https://github.com': redquinoa
Password for 'https://redquinoa@github.com':
Already up to date.


health-checks$ git pull # önceki sorgudan dolayı şifre sormadı.
Already up to date.
```

<br>
 
# Using a Remote Repository

## Working with Remotes

```
health-checks$ git remote -v

origin https://github.com/redquinoa/health-checks.git (fetch)
origin https://github.com/redquinoa/health-checks.git (push) 


health-checks$ git remote show origin
*   remote origin
    Fetch URL: https://github.com/redquinoa/health-checks.git
    Push URL: https://github.com/redquinoa/health-checks.git
    HEAD branch: master
    Remote branch:
        master tracked
    Local branch configured for 'git pull':
        master merges with remote master
    Local ref configured for 'git push':
        master pushes to master (2p to date)


health-checks$ git branch -r
origin/HEAD -> origin/master
origin/master


health-checks$ git status
On branch master
Your branch is up to date with 'origin/master'.

nothing to commit, working tree clean
```

<br>

## Fetching New Changes 

```
health-checks$ git remote show origin
* remote origin
  Fetch URL: https://github.com/redquinoa/health-checks.git
  Push URL: https://github.com/redquinoa/health-checks.git
  HEAD branch: master
  Remote branch:
    master tracked
  Local branch configured for 'git pull':
    master merges with remote master
  Local ref configured for 'git push':
    master pushes to master (tocal out of date)


health-checks$ git log origin/master
commit b62dc2eacfa820cd9a762adab9213305d1c8d344 (origin/HEAD, origin/master)
Author: Blue Kale <bluekale@example.com>
Date: Mon Jan 6 14:32:45 2020 -0800
    Add initial files for the checks

commit 807cb5037ccac5512ba583e782c35f4e114f8599 (HEAD -> master)
Author: My name <me@example.com>
Date: Mon Jan 6 14:09:41 2020 -0800
    Add one more line to README.md

commit 3d9f86c50b8651d41adabdaebd04530f4694efb5
Author: Red Quinoa <55592533+redquinoa@users.noreply.github.com>
Date: Sat Sep 21 14:04:15 2019 -0700
    Initial commit 


health-checks$ git status
On branch master
Your branch is behind 'origin/master' by 1 commit, and can be fast-forwarded.
    (use "git pull" to update your local branch)

nothing to commit, working tree clean 


health-checks$ git merge origin/master
Updating 807cb50..b62dc2e
Fast-forward
    all_checks.py | 18 ++w+v+w+sww+vww+s+
    disk_usage.py | 24 ++++++++++++++++++++~+++
    2 files changed, 42 insertions(+)
    create mode 100755 all_checks.py
    create mode 100644 disk_usage.py


health-checks$ git log

commit b62dc2eacfa820cd9a762adab9213305d1c8d344 (HEAD -> master, origin/HEAD, origin/master)
Author: Blue Kale <bluekale@example.com>
Date: Mon Jan 6 14:32:45 2020 -0800
    Add initial files for the checks

commit 807cb5037ccac5512ba583e782c35f4e114f8599
Author: My name <me@example.com>
Date: Mon Jan 6 14:09:41 2020 -0800
    Add one more line to README.md

commit 3d9f86c50b8651d41adabdaebd04530f4694efb5
Author: Red Quinoa <55592533+redquinoa@users.noreply.github.com>
Date: Sat Sep 21 14:04:15 2019 -0700
    Initial commit
```
<br>

## Updating the Local Repository

```
health-checks$ git pull
remote: Enumerating objects: 8, done.
remote: Counting objects: 100% (8/8), done.
remote: Compressing objects: 100% (5/5), done.
Unpacking objects: 100% (6/6), done.
remote: Total 6 (delta 1), reused 6 (delta 1), pack-reused 0
From https://github.com/redquinoa/health-checks
    b62dc2e..922d659 master -> origin/master
    * [new branch] experimental -> origin/experimental
Updating b62dc2e..922d659
Fast-forward
    all_checks.py | 15 +++++++++++++++
    1 file changed, 15 insertions(+)


health-checks$ git log -p -1
commit 922d65950b5325109525a24b71d8df8346412d04 (HEAD -> master, origin/master, origin/HEAD)
Author: Blue Kale <bluekale@example.com>

Date: Mon Jan 6 14:42:44 2020 -0800

Add disk full check to all_checks.py

diff --git a/all_checks.py b/all_checks.py
index fdc4476..e46cdae 100755
--- a/all_checks.py
+++ b/all_checks.py
@@ -1,16 +1,31 @@
#l/usr/bin/env python3

  import os
+ import shutil
  import sys

def check_reboot():
    """Returns True if the computer has a pending reboot."""
    return os.path.exists("/run/reboot-required")

+ def Check_disk_full(disk, min_absolute, min_percent):
+ """Returns True if there isn‘t enough disk space, False otherwise."""
+ du = shutil.disk_usage(disk)
+ # Calculate the percentage of free space
+ percentage_free = 100 * du.free / du.total


health-checks$ git remote show origin
* remote origin
  Fetch URL: https://github.com/redquinoa/health-checks.git
  Push URL: https://github.com/redquinoa/health-checks.git
  HEAD branch: master
  Remote branches:
    experimental tracked
    master tracked
  Local branch configured for 'git pull':
    master merges with remote master
  Local ref configured for 'git push':
    master pushes to master (up to date)


health-checks$ git checkout experimental
Branch 'experimental' set up to track remote branch 'experimental' from 'origin'.
Switched to a new branch 'experimental'
```

<br>

# Solving Conflicts

## The Pull-Merge-Push Workflow

```
health-checks$ atom all_checks.py

import os
import shutil
import sys

def check_reboot():
  """Returns True if the computer has a pending reboot."""
  return os.path.exists("/run/reboot-required")

def check_disk_full(disk, min_gb, min_percent): # absolute gb olarak değiştirildi
  """Returns True if there isn't enough disk space, False otherwise."""

  du = shutil.disk_usage(disk)
  # Calculate the percentage of free space
  percent_free = 100 * du.free / du.total
  # Calculate how many free gigabytes
  gigabytes_free = du.free / 2**30
  if percent_free < min_percent or gigabytes_free < min_gb: # absolute gb olarak değiştirildi
    return True
  return False

def main():
  
  if check_reboot():
    print("Pending Reboot.")
    sys.exit(1)
  
  if check_disk_full(disk="/", min_gb=2, min_percent=10): # "/", 2, 10 kısmı disk="/", min_gb=2, min_percent=10 olarak değiştirildi.
    print("Disk full.")
    sys.exit(1)

  print("Everything ok.")
  sys.exit(0)

main()


health-checks$ git add -p
diff --git a/all_checks.py b/all_checks.py
index e46cdae..a40047c 100755
--- a/all_checks.py
+++ b/all_checks.py
@@ -8_14 +8,14 30 @@ check_reboot():
"""Returns True if the computer has a pending reboot."""
return os.path.exists("/run/reboot-required")
-def check_disk_full(disk, min_absolute, min_percent):
+def check_disk_full(disk, min_gb, min_percent):
"""Returns True if there isn't enough disk space, False otherwise."""
du = shutil.disk_usage(disk)
# Calculate the percentage of free space
percent_free = 100 * du.free / du.total
# Calculate how many free gigabytes
gigabytes_free = du.free / 2**30
- if percent_free < min_percent or gigabytes_free < min_absolute:
+ if percent_free < min_percent or gigabytes_free < min_gb:
    return True
  return False

stage this hunk? [y,n,q,a,d,j,J,g,/,s,e,?]? y

@@-23,7 +23,7@@ def main():
if check_reboot():
  print("Pending Reboot.")
  sys.exit(1)
- if check_disk_full("/", 2, 10 ):
+ if check_disk_full(disk="/", min_gb=2, min_percent=10):
    print("Disk full.")
    sys.exit(1)

stage this hunk? [y,n,q,a,d,j,J,g,/,s,e,?]? y


health-checks$ git commit -m 'Rename min_absolute to min_gb, use parameter names'
[master 03d23d0] Rename min_absolute to min_gb, use parameter names
1 file changed, 3 insertions(+), 3 deletions(-)


health-checks$ git push
Username for 'https://github.com': redquinoa
Password for 'https://redquinoa@github.com':
To https://github.com/redquinoa/health-checks.git

! [rejected] master -> master (fetch first)
error: failed to push some refs to 'https://github.com/redquinoa/health-checks.git'
hint: Updates were rejected because the remote contains work that you do
hint: not have locally. This is usually caused by another repository pushing
hint: to the same ref. You may want to first integrate the remote changes
hint: (e.g., 'git pull ...') before pushing again.
hint: See the 'Note about fast—forwards' in 'git push --help' for details.


health-checks$ git pull
remote: Enumerating objects: 5, done.
remote: Counting objects: 100% (5/5), done.
remote: Compressing objects: 100% (2/2), done.
remote: Total 3 (delta 1), reused 3 (delta 1), pack-reused 0
Unpacking objects: 100% (3/3), done.
From https://github.com/redquinoa/health-checks
  922d659..a2dc118 master -> origin/master
Auto-merging all_checks.py
CONFLICT (content): Merge conflict in all_checks.py
Automatic merge failed; fix conflicts and then commit the result.


health-checks$ git log —-graph --oneline --all
* 03d23d0 (HEAD -> master) Rename min_absolute to min_gb, use parameter names
| * a2dc118 (origin/master, origin/HEAD) Reorder conditional to match parameter order
|/
| * 4d99c56 (origin/experimental, experimental) Empty check_load function
|/
* 922d659 Add disk full check to all_checks.py
* b62dc2e Add initial files for the checks
* 807cb50 Add one more line to README.md
* 3d9f86c Initial commit


health-checks$ git log -p origin/master
commit a2dc1181e5cccf36fec30d6eeefbe569a13883d2 (origin/master, origin/HEAD)
Author: Blue Kale <bluekale@example.com>
Date: Mon Jan 6 14:52:23 2020 -0800
  Reorder conditional to match parameter order
diff --git a/all_checks.py b/all_checks.py
index e46cdae..6dda356 100755
--- a/all_checks.py
+++ b/all_checks.py
@@ -15,7 +15,7 @@ def check_disk_full(disk, min_absolute, min_percent):
percent_free = 100 * du.free / du.total
# Calculate how many free gigabytes
gigabytes_free = du.free / 2**30
- if percent_free < min_percent or gigabytes_free < min_absolute:
+ if percent_free < min_percent or gigabytes_free < min_gb:
  return True
return False


health-checks$ atom all_checks.py
```
![Ekran görüntüsü 2024-02-01 105911](https://github.com/kemda2/Google-Courses/assets/19648132/8beff1a3-d55d-431a-bceb-5ac25239c6ec)
```
health-checks$ git commit
Merge branch 'master' of https://github.com/redquinoa/health-checks
Fixed check_disk_usage conditional to use the new order and new variable name.

# Conflicts:
# all_checks.py
#
# It looks like you may be committing a merge.
# If this is not correct, please remove the file
# .git/MERGE_HEAD
# and try again.
# Please enter the commit message for your changes. Lines starting
# with '#' will be ignored, and an empty message aborts the commit.
#
# On branch master
# Your branch and 'origin/master' have diverged,
# and have 1 and 1 different commits each, respectively.
# (use "git pull" to merge the remote branch into yours)
#
# All conflicts fixed but you are still merging.
#
# Changes to be committed:
# modified: all_checks py


health-checks$ git push
Enumerating objects: 10, done.
Counting objects: 100% (10/10), done.
Delta compression using up to 4 threads
Compressing objects: 100% (6/6), done.
Writing objects: 100% (6/6), 876 bytes | 876.00 KiB/s, done.
Total 6 (delta 2), reused 0 (delta 0)
remote: Resolving deltas: 100% (2/2), completed with 1 local object. 
  a2dc118..58351ff master -> master


health-checks$ git log --graph --oneline
* 58351ff (HEAD -> master, origin/master, origin/HEAD) Merge branch 'master' of https://github.com/redquinoa/health-checks
|\
| * a2dc118 Reorder conditional to match parameter order
* | 03d23d0 Rename min_absolute to min_gb, use parameter names
|/
* 922d659 Add disk full check to all_checks.py
* b62dc2e Add initial files for the checks
* 807cb50 Add one more line to README.md
* 3d9f86c Initial commit


health-checks$ atom all_checks.py
import os
import shutil
import sys

def check_reboot():
  """Returns True if the computer has a pending reboot."""
  return os.path.exists("/run/reboot-required")

def check_disk_full(disk, min_gb, min_percent):
  """Returns True if there isn't enough disk space, False otherwise."""

  du = shutil.disk_usage(disk)
  # Calculate the percentage of free space
  percent_free = 100 * du.free / du.total
  # Calculate how many free gigabytes
  gigabytes_free = du.free / 2**30
  if percent_free < min_percent or gigabytes_free < min_gb: 
    return True
  return False

def check_root_full():
"""Returns True if the root partition is full, False otherwise."""
  return check_disk_full(disk="/", min_gb=2, min_percent=10)

def main():
  checks=[
        (check_reboot, "Pending Reboot"),
        (check_root_full, "Root partition full"),
  ]

  everything_ok= True
  for check, msg in checks:
    if check():
      print(msg)
      everything_ok = False
    if not everything_ok:
      sys.exit(1)

main()


health-checks$ git commit -a -m 'Allow printing more than one error message'
[refactor cbee3f7] Allow printing more than one error message
1 file changed, 7 insertions(+), 1 deletion(-)


health-checks$ git push -u origin refactor
Username for 'https://github.com': redquinoa
Password for 'https://redquinoa@github.com':
Enumerating objects: 11, done.
Counting objects: 100% (11/11), done.
Delta compression using up to 4 threads
Compressing objects: 100% (9/9), done.
Writing objects: 100% (9/9), 1.34 KiB | 1.34 MiB/s, done.
Total 9 (delta 3), reused 0 (delta 0)
remote: Resolving deltas: 100% (3/3), completed with 1 local object.
remote:
remote: Create a pull request for 'refactor' on GitHub by visiting:
remote: https://github.com/redquinoa/health-checks/pull/new/refactor
remote:
To https://github.com/redquinoa/health—checks.git
* [new branch] refactor -> refactor
Branch 'refactor' set up to track remote branch 'refactor' from 'origin'.
```

## Rebasing Your Changes

```
health-checks$ git checkout master
Switched to branch 'master'
Your branch is up to date with 'origin/master'.


```

![Ekran görüntüsü 2024-02-01 121205](https://github.com/kemda2/Google-Courses/assets/19648132/0bf4cb4a-e065-420c-985c-c8e248254f66)

```
health-checks$ git checkout refactor
Switched to branch 'refactor'
Your branch is up to date with 'origin/refactor'.


health-checks$ git rebase master
First, rewinding head to replay your work on top of it...
Applying: Create wrapper function for check_disk_full
Applying: Iterate over a list of checks and messages to avoid code duplication
Applying: Allow printing more_than one error message

```

![Ekran görüntüsü 2024-02-01 121](https://github.com/kemda2/Google-Courses/assets/19648132/4f28e878-97f7-410a-906c-6cc076541cdb)

```
health-checks$ git checkout master
Switched to branch 'master'
Your branch is up to date with 'origin/master'.


health-checks$ git merge refactor
Updating 0789f64..f5813b1
Fast-forward
all_checks.py | 24 ++¢+++e+++++++e+++~
1 file changed, 19 insertions(+), 5 deletions(-)


health-checks$ git branch -d refactor
Deleted branch refactor (was f5813b1).


health-checks$ git push
Enumerating objects: 11, done.
Counting objects: 100% (11/11), done.
Delta compression using up to 4 threads
Compressing objects: 100% (9/9), done.
Writing objects: 100% (9/9), 1.37 KiB | 1.37 MiB/s, done.
Total 9 (delta 3), reused 0 (delta 0) y
remote: Resolving deltas: 100% (3/3), completed with 1 local object. 


health-checks$ git push
Enumerating objects: 11, done.
Counting objects: 100% (11/11), done.
Delta compression using up to 4 threads
Compressing objects: 100% (9/9), done.
Writing objects: 100% (9/9), 1.37 KiB | 1.37 MiB/s, done.
Total 9 (delta 3), reused 0 (delta 0)
remote: Resolving deltas: 100% (3/3), completed with 1 local object.
To https://github.com/redquinoa/health-checks.git y
0789f64..f5813b1 master -> master 
```

## Another Rebasing Example

```
health-checks$ atom all_checks.py
import os
import shutil
import sys
+ import socket 

def check_reboot():
  """Returns True if the computer has a pending reboot."""
  return os.path.exists("/run/reboot-required")

def check_disk_full(disk, min_gb, min_percent):
  """Returns True if there isn't enough disk space, False otherwise."""

  du = shutil.disk_usage(disk)
  # Calculate the percentage of free space
  percent_free = 100 * du.free / du.total
  # Calculate how many free gigabytes
  gigabytes_free = du.free / 2**30
  if percent_free < min_percent or gigabytes_free < min_gb: 
    return True
  return False

def check_root_full():
"""Returns True if the root partition is full, False otherwise."""
  return check_disk_full(disk="/", min_gb=2, min_percent=10)

+def check_no_network():
+  """Returns True if it fails to resolve Google's URL, False otherwise"""
+  try:
+    socket.gethostbyname("www.google.com")
+    return False
+  except:
+    return True

def main():
  checks=[
        (check_reboot, "Pending Reboot"),
        (check_root_full, "Root partition full"),
      + (check_no_network, "No working network"),
  ]

  everything_ok= True
  for check, msg in checks:
    if check():
      print(msg)
      everything_ok = False
    if not everything_ok:
      sys.exit(1)

main()


health-checks$ git commit -a -m 'Add a simple network connectivity check'
[master aa8da6f] Add a simple network connectivity check
1 file changed, 10 insertions(+), 1 deletion(-)


health-checks$ git fetch
remote: Enumerating objects: 6, done.
remote: Counting objects: 100% (6/6), done.
remote: Compressing objects: 100% (4/4), done.
remote: Total 5 (delta 1), reused 5 (delta 1), pack-reused 0
Unpacking objects: 100% (5/5), done.
From https://github.com/redquinoa/health-checks
  f5813b1..d8c8fcd master -> origin/master


health-checks$ git rebase origin/master
First, rewinding head to replay your work on top of it...
Applying: Add a simple network connectivity check
Using index info to reconstruct a base tree...
A       all_checks.py
Falling back to patching base and 3-way merge...
Auto-merging health_checks.py
CONFLICT (content): Merge conflict in health_checks.py
error: Failed to merge in the changes.
Patch failed at 0001 Add a simple network connectivity check
hint: Use 'git am --show-current-patch' to see the failed patch

Resolve all conflicts manually, mark them as resolved with
"git add/rm <conflicted_files>", then run "git rebase --continue".
You can instead skip this commit: run "git rebase --skip".
To abort and get back to the state before "git rebase", run "git rebase --abort".
```

<br>

![Ekran görüntüsü 2024-02-01 125039](https://github.com/kemda2/Google-Courses/assets/19648132/051aa16f-1c1f-4bac-bbf9-674938681183)

<br>

```
health-checks$ ./health_checks.py
Traceback (most recent call last):
  File "./health_checks.py", line 61, in <module>
    main()
  File "./health_checks.py", line 49, in main
    if check():
  File "./health_checks.py", line 30, in check_cpu_constrained
    return psutil.cpu_percent(1) > 75
NameError: name 'psutil' is not defined


health-checks$ atom health_checks.py
```

<br>

![Ekran görüntüsü 2024-02-01 125752](https://github.com/kemda2/Google-Courses/assets/19648132/751fd7a8-5c26-4191-97e6-6b790e73b80d)

<br>

```
health-checks$ ./health_checks.py
Everything ok. 


health-checks$ git add health_checks.py


health-checks$ git rebase --continue
Applying: Add a simple network connectivity check


health-checks$ git log --graph --oneline
* 160b5f3 (HEAD -> master) Add a simple network connectivity check
* b52b7a2 (origin/master, origin/HEAD) Add cpu_constrained check
* 9fc7275 Rename all_checks.py to health_checks.py
* f5813b1 Allow printing more than one error message
* 18257a0 Iterate over a list of checks and messages to avoid code duplication
* Sd2e3eb Create wrapper function for check_disk_full
* 0789f64 Add reference to all_checks.py to README
* 58351ff Merge branch 'master' of https://github.com/redquinoa/health-checks
|\
| * a2dc118 Reorder conditional to match parameter order
* | 03d23d0 Rename min_absolute to min_gb, use parameter names
|/
* 922d659 Add disk full check to all_checks.py
* b62dc2e Add initial files for the checks
* 807cb50 Add one more line to README.md
* 3d9f86c Initial commit 


health-checks$ git push
Username for 'https://github.com': redquinoa
Password for 'https://redquinoa@github.com':
Enumerating objects: 5, done.
Counting objects: 100% (5/5), done.
Delta compression using up to 4 threads
Compressing objects: 100% (3/3), done.
Writing objects: 100% (3/3), 501 bytes | 501.00 KiB/s, done.
Total 3 (delta 2), reused 0 (delta 0)
remote: Resolving deltas: 100% (2/2), completed with 2 local objects.
```