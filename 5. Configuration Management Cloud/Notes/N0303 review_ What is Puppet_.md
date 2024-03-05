# Review: What is Puppet?

This reading contains the code used in the instructional videos from ~[What is puppet?](https://www.coursera.org/lecture/configuration-management-cloud/what-is-puppet-wAyPs.)~

## Introduction

This follow-along reading is organized to match the content in the video that follows. It contains the same code shown in the next video. These code blocks will provide you with the opportunity to see how the code is written, allow you to practice running it, and can be used as a reference to refer back to. 

You can follow along in the reading as the instructor discusses the code or review the code after watching the video.

 
```
class sudo {

  package { 'sudo':

    ensure => present,

  }

}
```


## About this code

This block of code is saying that the package 'sudo' should be present on every computer where the rule gets applied. If this rule is applied on 100 computers, it would automatically install the package in all of them. This is a small and simple block but can already give us a basic impression of how rules are written in puppet.
