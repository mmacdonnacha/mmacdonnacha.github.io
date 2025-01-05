---
title: Overthewire Bandit Level 3 -> 4
date: 2021-11-02 22:15:00 +0000
categories: [OverTheWire, Bandit]
tags: [overthewire, bandit]
description: Solution for Overthewire Bandit level 4 challenge
---

Solution for the Overthewire.org [Bandit level 3 -> 4](https://overthewire.org/wargames/bandit/bandit4.html){:target="\_blank"}  

## Level Goal

The password for the next level is stored in a hidden file in the `inhere` directory.

---

## Walkthrough

Login to the server using the password obtained from the previous level [Bandit level 2 -> 3]({% post_url 2021-11-02-overthewire-bandit-03 %}).

username: `bandit3`

```ssh
ssh bandit3@bandit.labs.overthewire.org -p 2220
```

Change directory into `inhere`, running `ls` command will show no files.  

```console
bandit3@bandit:~$ ls
inhere
bandit3@bandit:~$ cd inhere/
bandit3@bandit:~/inhere$ ls  

```

Running `ls -a` will let us see all files including hidden files.  
`ls` list all files  
`-a` all files including hidden files  
We can then see a file named `.hidden`.  
The you can print to screen using `cat` command.

```console
bandit3@bandit:~/inhere$ ls -a
.  ..  .hidden
bandit3@bandit:~/inhere$ cat ./.hidden
pIwrPr##########################
```
