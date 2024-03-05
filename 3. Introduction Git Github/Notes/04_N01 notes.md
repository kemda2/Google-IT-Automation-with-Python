# Pull Requests

## The Typical Pull Request Workflow on GitHub

```
rearrange$ atom README.md
Rearrange
=========

This module is used for rearranging names.



rearrange$ git add README.md


rearrange$ git commit -m 'Add a simple README.md file'
[add-readme 736d754] Add a simple README.md file
1 file changed, 4 insertions(+)
create mode 100644 README.md


rearrange$ git push -u origin add-readme
Username for 'https://github.com': redquinoa
Password for 'https://redquinoa@github.com':
Enumerating objects: 4, done.
Counting objects: 100% (4/4), done.
Delta compression using up to 4 threads
Compressing objects: 100% (3/3), done.
Writing objects: 100% (3/3), 400 bytes | 400.00 KiB/s, done.
Total 3 (delta 0), reused 0 (delta 0)
remote:
remote: Create a pull request for 'add-readme' on GitHub by visiting:
remote: https://github.com/redquinoa/rearrange/pull/new/add-readme
remote:
To https://github.com/redquinoa/rearrange.git
* [new branch] add-readme -> add-readme
Branch 'add-readme' set up to track remote branch 'add-readme' from 'origin'.
```

<br>
<br>

## Updating an Existing Pull Request

```
rearrange$ atom README.md
Rearrange
=========

This module is used for rearranging names.
+ Turns "LastName, FirstName" into "FirstName LastName"
+ # Example
+ Calling `rearrange_name("Turing, Alan")` will return `"Alan Turing"`


rearrange$ git commit -a -m 'Add more information to the README'
[add-readme 01231b0] Add more information to the README
1 file changed, 5 insertions(+)


rearrange$ git push
Username for 'https://github.com': redquinoa
Password for 'https://redquinoa@github.com':
Enumerating objects: 5, done.
Counting objects: 100% (5/5), done.
Delta compression using up to 4 threads
Compressing objects: 100% (3/3), done.
Writing objects: 100% (3/3), 407 bytes | 407.00 KiB/s, done.
Total 3 (delta 1), reused 0 (delta 0)
remote: Resolving deltas: 100% (1/1), completed with 1 local object.
To https://github.com/redquinoa/rearrange.git
    736d754..01231b0 add-readme -> add-readme
```

<br>
<br>

## Squashing Changes

```
rearrange$ git rebase -i master
pick 736d754 Add a simple README.md file
squash 01231b0 Add more information to the README

# Rebase 367a127..01231b0 onto 367a127 (2 commands)
#
# Commands:
# p, pick <commit> = use commit
# r, reword <commit> = use commit, but edit the commit message
# e, edit <commit> = use commit, but stop for amending
# s, squash <commit> = use commit, but meld into previous commit
# f, fixup <commit> = like "squash", but discard this commit's log message
# x, exec <command> 2 run command (the rest of the line) using shell
# b, break = stop here (continue rebase later with 'git rebase --continue')
# d, drop <commit> 2 remove commit
# l, label <label> : label current HEAD with a name
# t, reset <label> = reset HEAD to a label
# m, merge [—C <commit> | -c <commit>] <label> [# <oneline>]
# .         create a merge commit using the original merge commit's
# .         message (or the oneline, if no original merge commit was
# .         specified). Use -c <commit> to reword the commit message.
#
# These lines can be re-ordered; they are executed from top to bottom.


# This is a combination of 2 commits.
# This is the 1st commit message:
    Add a simple README.md file
# This is the commit message #2:
    Add more information to the README
# Please enter the commit message for your changes. Lines starting
# with '#' will be ignored, and an empty message aborts the commit.
#
# Date: Tue Jan 7 09:47:17 2020 -0800
#
# interactive rebase in progress; onto 367a127
# Last commands done (2 commands done):
# pick 736d754 Add a simple README.md file
# squash 01231b0 Add more information to the README
# No commands remaining.
# You are currently rebasing branch 'add-readme' on '367a127'.
#
# Changes to be committed:


rearrange$ git show

commit ae779e430288b082a19062ed087c547e1051a981 (HEAD -> add-readme)
Author: My name <me@example.com>
Date: Tue Jan 7 09:47:17 2020 -0800
    Add a simple README.md file including an example use case
diff --git a/README.md b/README.md
new file mode 100644
index 0000000..311fc65
--- Idev/null
+++ b/README.md
@@ —0,0 +1,9 @@
+Rearrange
+=========
+
+This module is used for rearranging names.
+ Turns "LastName, FirstName" into "FirstName LastName"
+ # Example
+ Calling `rearrange_name("Turing, Alan")` will return `"Alan Turing"`


rearrange$ git status
```

<br>
<br>

![Ekran görüntüsü 2024-02-01 152538](https://github.com/kemda2/Google-Courses/assets/19648132/eb6c7b13-2905-459f-8e19-b40705842cfa)

<br>
<br>

```
rearrange$ git push
Username for 'https://github.com': redquinoa
Password for 'https://redquinoa@github.com':
To https://github.com/redquinoa/rearrange.git
! [rejected] add-readme -> add-readme (non-fast-forward)
error= failed to push some refs to 'https://github.com/redquinoa/rearrange.git'
hint: Updates were rejected because the tip of your current branch is behind
hint: its remote counterpart. Integrate the remote changes (e.g.
hint: 'git pull ...') before pushing again.
hint: See the 'Note about_fast-forwards' in 'git push --help' for details.


rearrange$ git push -f
Enumerating objects: 4, done.
Counting objects: 100% (4/4), done.
Delta compression using up to 4 threads
Compressing objects: 100% (3/3), done.
Writing objects: 100% (3/3), 510 bytes | 510.00 KiB/s, done 3,.
Total 3 (delta 0), reused 0 (delta 0) 
To https://github.com/redquinoa/rearrange.git 
    + 01231b0...ae779e4 add-readme -> add-readme (forced update)


rearrange$ git log --graph --oneline --all -4
* ae779e4 (HEAD -> add-readme) Add a simple README.md file including an example use case
* 367a127 (origin/master, origin/HEAD, master) Add tests for the rearrange module
* c89805e Add the rearrange module
* f4ddbc7 Initial commit
```
<br>
<br>

# Code Reviews

## How to Use Code Reviews in GitHub

```
rearrange$ atom README.md
Rearrange
=========

This module is used for rearranging names.

Turns "LastName, FirstName" into "FirstName LastName"

- # Example
+ ## Examples

- Calling `rearrange_name("Turing, Alan")` will return `"Alan Turing"`
+ * Calling `rearrange_name("Turing, Alan")` will return `"Alan Turing"`
+ * Calling `rearrange_name("Turing, Alan")` will return `"Alan Turing"`
+ * Calling `rearrange_name("Turing, Alan")` will return `"Alan Turing"`


rearrange$ git commit -a --amend

Add a simple README.md file including an example use case

# Please enter the commit message for your changes. Lines starting
# with '#' will be ignored, and an empty message aborts the commit.
#
# Date: Tue Jan 7 09:47:17 2020 -0800
#
# 0n branch add-readme
# Your branch is up to date with 'origin/add-readme'.
#
# Changes to be committed:
# new file: README.md
#

[add-readme 55e32ed] Add a simple README.md file including an example use case
Date: Tue Jan 7 09:47:17 2020 ~0800
1 file changed, 11 insertions(+)
create mode 100644 README.md


rearrange$ git status

On branch add-readme

Your branch and 'origin/add-readme' have diverged,
and have 1 and 1 different commits each, respectively.
    (use "git pull" to merge the remote branch into yours)

nothing to commit, working tree clean


rearrange$ git push -f

Username for 'https://github.com': redquinoa
Password for 'https://redquinoa@github.com':
Enumerating objects: 4, done.
Counting objects: 100% (4/4), done.
Delta compression using up to 4 threads
Compressing objects: 100% (3/3), done.
Writing objects: 100% (3/3), 553 bytes | 553.00 KiB/s, done.
Total 3 (delta 0), reused 0 (delta 0)
To https://github.com/redquinoa/rearrange.git
    + ae779e4...55e32ed add-readme -> add-readme (forced update)
```

<br>
<br>

# Managing Projects

## Tracking Issues

```
health-checks$ atom README.md

# health-checks

Scripts that check the health of my computers

This repo will be populated with lots of fancy checks.
Currently the main script is health_checks.py

This script will print "Everything ok" if all checks pass,
or the corresponding error messages if some checks fail.


health-checks$ git commit -a

Update README to use the new name of the script

Also add more information about how this works.
Closes #1 # Bunu yazınca problem çözüldü olarak anlaşılıyor.
# Please enter the commit message for your changes. Lines starting
# with '#' will be ignored, and an empty message aborts the commit.
#
# On branch master
# Your branch is up to date with 'origin/master'.
#
# Changes to be committed:
#   modified: README.md
#


health-checks$ git push
Username for 'https://github.com': redquinoa
Password for 'https://redquinoa@github.com':
Enumerating objects: 5, done.
Counting objects: 100% (5/5), done.
Delta compression using up to 4 threads
Compressing objects: 100% (3/3), done.
Writing objects: 100% (3/3), 564 bytes | 564.00 KiB/s, done.
Total 3 (delta 0), reused 0 (delta 0)
To https://github.com/redquinoa/health-checks.git
    160b5f3..8981efe master -> master
```