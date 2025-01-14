---
title: OverTheWire Bandit Level 2 -> 3
date: 2021-11-02 22:05:00 +0000
categories: [OverTheWire, Bandit]
tags: [overthewire, bandit]
description: Solution for OverTheWire Bandit level 3 challenge
---

Solution for the Overthewire.org [Bandit level 2 -> 3](https://overthewire.org/wargames/bandit/bandit3.html){:target="\_blank"}  

## Level Goal

The password for the next level is stored in a file called `spaces in this filename` located in the home directory

## Walkthrough  

Login to the server using the password obtained from the previous level [Bandit level 1 -> 2]({% post_url 2021-11-02-overthewire-bandit-02 %}).

username: `bandit2`

```ssh
ssh bandit2@bandit.labs.overthewire.org -p 2220
```

This time there is a file with spaces in the name.  

```console
bandit2@bandit:~$ ls 
spaces in this filename 
```

Running `cat spaces in the filename` will cause errors as it will think each word in `spaces in the filename` is its own separate file.  

```console
bandit2@bandit:~$ cat spaces in this filename
cat: spaces: No such file or directory 
cat: in: No such file or directory 
cat: this: No such file or directory
cat: filename: No such file or directory
```

Printing the contents of the file can be done 2 ways.  
One using `\` before each space to indicate to the terminal that the filename continues and the other is surrounding the file name with quotes `'` or `"`.

```console
bandit2@bandit:~$ cat 'spaces in this filename'
UmHadQ##########################

bandit2@bandit:~$ cat spaces\ in\ this\ filename
UmHadQ##########################
```
