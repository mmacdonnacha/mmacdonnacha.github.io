---
title: OverTheWire Leviathan Level 0
date: 2022-02-28 22:45:00 +0000
categories: [OverTheWire, Leviathan]
tags: [overthewire, leviathan]
description: Solution for OverTheWire Leviathan level 0 challenge
---

## Level Goal  

There is no information for this level, intentionally.

---

## Walkthrough  

Solution for the Overthewire.org [Leviathan level 0](https://overthewire.org/wargames/leviathan/leviathan0.html){:target="\_blank"}

Login to the server using the provided username and password.  

username: `leviathan0`  
password: `leviathan0`

```ssh
ssh leviathan0@leviathan.labs.overthewire.org -p 2223
```

With no description given first thing we do is check what is in the home directory.

```console
leviathan0@leviathan:~$ ls 
leviathan0@leviathan:~$ ls -al
total 24
drwxr-xr-x  3 root       root       4096 Aug 26  2019 .
drwxr-xr-x 10 root       root       4096 Aug 26  2019 ..
drwxr-x---  2 leviathan1 leviathan0 4096 Aug 26  2019 .backup
-rw-r--r--  1 root       root        220 May 15  2017 .bash_logout
-rw-r--r--  1 root       root       3526 May 15  2017 .bashrc
-rw-r--r--  1 root       root        675 May 15  2017 .profile
```

`ls` shows nothing in the home directory.  
When we use `ls -al` to list all files and directories we can now see a directory named `.backup`.

```console
leviathan0@leviathan:~$ cd .backup/
leviathan0@leviathan:~/.backup$ ls
bookmarks.html
```

The only thing inside `.backup` is a html file `bookmarks.html`.

We can now use `grep` to search the file for given words.  
Grep is used in this format `grep <WORD TO BE SEARCHED> <FILE TO BE SEARCH>`

```console
leviathan0@leviathan:~/.backup$ grep password bookmarks.html
<DT><A HREF="http://leviathan.labs.overthewire.org/passwordus.html | This will be fixed later, the password for leviathan1 is rioG******" ADD_DATE="1155384634" LAST_CHARSET="ISO-8859-1" ID="rdf:#$2wIU71">password to leviathan1</A> 

leviathan0@leviathan:~/.backup$
```

We can see that searching for the word `password` found the password for the next challenge.

```text
This will be fixed later, the password for leviathan1 is rioG******
```
