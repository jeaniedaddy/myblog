---
title: git SSH setup
date: 2018-09-26 08:15:56
categories: work
tags: [work, SSH]
---


### 1. how to configure SSH
```
$ ls -al ~/.ssh
$ ssh-keygen -t rsa -b 4096 -C 'name@email.com'
$ ls -al ~/.ssh
$ eval "$(ssh-agent -s)"
$ ssh-add ~/.ssh/id_rsa
$ pbcopy < ~/.ssh/id_rsa.pub
$ ssh -T git@github.com
$ 
```
Adding a new SSH key to Github account
