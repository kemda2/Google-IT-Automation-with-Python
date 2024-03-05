# Review: Applying rules locally

This reading contains the code used in the instructional videos from [Applying Rules Locally](https://www.coursera.org/lecture/configuration-management-cloud/applying-rules-locally-Lpu3d.).
 
## Introduction

This follow-along reading is organized to match the content in the video that follows. It contains the same code shown in the next video. These code blocks will provide you with the opportunity to see how the code is written, allow you to practice running it, and can be used as a reference to refer back to. 
You can follow along in the reading as the instructor discusses the code or review the code after watching the video.
Enter in the terminal


```
sudo apt install puppet-master
#(...)
#Processing triggers for systemd (240-6ubuntu5.7) ...
#Processing triggers for man-db (2.8.5-2) ...
#Processing triggers for fontconfig (2.13.1-2ubuntu2) ...
vim tools.pp
htop
#-bash: /usr/bin/htop: No such file or directory
```

**Note:** Command ‘htop’ will not be found. Complete the next steps. 

`sudo puppet apply -v tools.pp` 

**Code output:**

```
Info: Loading facts
Notice: Compiled catalog for ubuntu in environment production in 0.02 seconds
Info: Applying configuration version '1572272642'
Notice: /Stage[main]/Main/Package[htop]/ensure: created
Notice: Applied catalog in 3.81 seconds
```

Note: Now you can try and run ‘htop’ again

`htop`

`sudo puppet apply -v tools.pp` 

**Code output:**
```
Info: Loading facts
Notice: Compiled catalog for ubuntu in environment production in 0.02 seconds
Info: Applying configuration version '1572281655'
Notice: Applied catalog in 0.07 seconds
```

