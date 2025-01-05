---
title: Overthewire Bandit Level 4 -> 5
date: 2021-11-02 22:20:00 +0000
categories: [OverTheWire, Bandit]
tags: [overthewire, bandit]
description: Solution for Overthewire Bandit level 5 challenge
---

Solution for the Overthewire.org [Bandit level 4 -> 5](https://overthewire.org/wargames/bandit/bandit5.html){:target="\_blank"}

## Level Goal

The password for the next level is stored in the only human-readable file in the `inhere` directory.

---

## Walkthrough

Login to the server using the password obtained from the previous level [Bandit level 3 -> 4]({% post_url 2021-11-02-overthewire-bandit-04 %}).  

username: `bandit4`  

```ssh
ssh bandit4@bandit.labs.overthewire.org -p 2220
```

We run `ls inhere` to see what files are in the `inhere` directory.  

```console
bandit4@bandit:~$ ls inhere/
-file00  -file01  -file02  -file03  -file04  -file05  -file06  -file07  -file08  -file09
```

There are 10 files which have names that are not descriptive.  
We can use `cat` on each file to find the human readable file but can use another command to see what information is in each file without reading the contents.  
The `file` command can be used to find out what data is stored in a file.  

Now we use the `file` command to get information on each file in the `inhere` directory.  

```console
bandit4@bandit:~$ file inhere/*  
inhere/-file00: data 
inhere/-file01: data  
inhere/-file02: data
inhere/-file03: data
inhere/-file04: data 
inhere/-file05: data 
inhere/-file06: data
inhere/-file07: ASCII text
inhere/-file08: data
inhere/-file09: data
```

We can see one file contains ASCII text which is human readable.  
Use `cat` command to print the contents of the file which is the password for the next level.

```console
bandit4@bandit:~$ cat ./inhere/-file07
koReBO##########################
```
