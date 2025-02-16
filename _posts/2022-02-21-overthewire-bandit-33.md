---
title: OverTheWire Bandit Level 32 -> 33
date: 2022-02-21 23:50:00 +0000
categories: [OverTheWire, Bandit]
tags: [overthewire, bandit, git]
description: Solution for OverTheWire Bandit level 33 challenge
---

## Level Goal

After all this git stuff its time for another escape. Good luck!
Commands you may need to solve this level

---

## Walkthrough

Solution for the Overthewire.org [Bandit level 32 -> 33](https://overthewire.org/wargames/bandit/bandit33.html){:target="\_blank"}

Login to the server using the password obtained from the previous level [Bandit level 31 -> 32]({% post_url 2022-02-20-overthewire-bandit-32 %}).  

username: `bandit32`  

```ssh
ssh bandit32@bandit.labs.overthewire.org -p 2220
```

After logging in we can see a different welcome message and prompt.

```console
WELCOME TO THE UPPERCASE SHELL
>>
```

Any command that is typed into this prompt will be changed to upper case. This is an issue since linux commands are case sensitive and mostly lower case.

There are a few commands that are upper case by default that we can test.  

```console
>> $SHELL
WELCOME TO THE UPPERCASE SHELL
>> 
```

`$SHELL` worked so what other environment variables can we use to.

We can run `$0` which is generally the first argument of a script, which basically it is its name.

```console
>> $0
$ 
```

Now we have a normal prompt again we can enter commands as normal.

```console
$ ls -la 
total 28
drwxr-xr-x  2 root     root     4096 May  7  2020 .
drwxr-xr-x 41 root     root     4096 May  7  2020 ..
-rw-r--r--  1 root     root      220 May 15  2017 .bash_logout
-rw-r--r--  1 root     root     3526 May 15  2017 .bashrc
-rw-r--r--  1 root     root      675 May 15  2017 .profile
-rwsr-x---  1 bandit33 bandit32 7556 May  7  2020 uppershell
```

We can see an `uppershell` script and its SUID bit is set. So `uppershell` is run as user `bandit33`.  

```console
$ id
uid=11033(bandit33) gid=11032(bandit32) groups=11032(bandit32)
```

Using the `id` command we can see we have a uid for bandit33.
Since we are running as `bandit33` all we have to do now is read the `/etc/bandit_password/bandit33` to get the password.

```console
$ cat /etc/bandit_pass/bandit33
c9c319##########################
```
