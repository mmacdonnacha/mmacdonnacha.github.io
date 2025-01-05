---
title: Overthewire Bandit Level 0 -> 1
date: 2021-11-02 20:41:00 +0000
categories: [OverTheWire, Bandit]
tags: [overthewire, bandit]
description: Solution for Overthewire Bandit level 1 challenge
---

Solution for the Overthewire.org [Bandit level 0 -> 1](https://overthewire.org/wargames/bandit/bandit1.html){:target="\_blank"}

## Level Goal

The password for the next level is stored in a file called `readme` located in the home directory.
Use this password to log into `bandit1` using SSH. Whenever you find a password for a level, use SSH (on port 2220) to log into that level and continue the game.

## Walkthrough

Login to the server using the provided username and password.

username: `bandit0`  
password: `bandit0`

```ssh
ssh bandit0@bandit.labs.overthewire.org -p 2220
```

Enter the password when prompted to login to the level.

The Level Goal states the password for the next level in the file `readme`.
Reading the contents of readme to get the password.

There are multiple ways to read the contents of a file `less` and `cat` are two ways.  
`less` will display the contents of the file in a paginated style which is good for viewing large files.  
`cat` on the other hand will display all the contents of the file to the screen without using pagination.

```console
bandit0@bandit:~$ ls
readme
bandit0@bandit:~$ cat readme
boJ9jb##########################
```
