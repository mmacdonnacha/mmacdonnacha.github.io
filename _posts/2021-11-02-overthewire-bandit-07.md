---
title: OverTheWire Bandit Level 6 -> 7
date: 2021-11-02 22:27:00 +0000
categories: [OverTheWire, Bandit]
tags: [overthewire, bandit]
description: Solution for OverTheWire Bandit level 7 challenge
---

Solution for the Overthewire.org [Bandit level 6 -> 7](https://overthewire.org/wargames/bandit/bandit7.html){:target="\_blank"}  

## Level Goal

The password for the next level is stored `somewhere on the server` and has all of the following properties:

* owned by user bandit7
* owned by group bandit6
* 33 bytes in size

---

## Walkthrough

Login to the server using the password obtained from the previous level [Bandit level 5 -> 6]({% post_url 2021-11-02-overthewire-bandit-06 %}).  

username: `bandit6`  

```ssh
ssh bandit6@bandit.labs.overthewire.org -p 2220
```

Similar to the previous level we need to use the `find` command to search for a file with specific properties.  

Use `find` again to search the whole server `/`  
Looking for files not directories `-type f`  
Files owned by the user bandit7 `-user bandit7`  
Files owned by the group bandit6 `-group bandit6`  
Files with a size of 33 bytes `-size 33c`.  

```console
bandit6@bandit:~$ find / -type f -user bandit7 -group bandit6 -size 33c
/var/lib/dpkg/info/bandit7.password
bandit6@bandit:~$ cat /var/lib/dpkg/info/bandit7.password
HKBPTKQ##########################
```
