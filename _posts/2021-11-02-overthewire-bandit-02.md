---
title: Overthewire Bandit Level 1 -> 2
date: 2021-11-02 20:46:00 +0000
categories: [OverTheWire, Bandit]
tags: [overthewire, bandit]
description: Solution for Overthewire Bandit level 2 challenge
---

Solution for the Overthewire.org [Bandit level 1 -> 2](https://overthewire.org/wargames/bandit/bandit2.html){:target="\_blank"}  

## Level Goal  

The password for the next level is stored in a file called `-` located in the home directory

## Walkthrough

Login to the server using the password obtained from the previous level [Bandit level 0 -> 1]({% post_url 2021-11-02-overthewire-bandit-01 %}).  

username: `bandit1`  

```ssh
ssh bandit1@bandit.labs.overthewire.org -p 2220
```

Running `ls` command we can see a single file with the name `-`.  

```console
bandit1@bandit:~$ ls 
-
```

Running `cat -` does not print the contents of the file `-` as the cat command thinks you are setting an option like `-n` for line numbers.  
We need to give the path to the file for the cat command to print the contents.

```console
bandit1@bandit:~$ cat ./-  
CV1Dtq##########################
```
