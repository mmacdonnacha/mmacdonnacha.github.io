---
title: OverTheWire Leviathan Level 7
date: 2022-03-02 23:45:00 +0000
categories: [OverTheWire, Leviathan]
tags: [overthewire, leviathan]
description: Solution for OverTheWire Leviathan level 7 challenge
---

## Level Goal  

There is no information for this level, intentionally.

---

## Walkthrough  

Solution for the Overthewire.org [Leviathan level 7](https://overthewire.org/wargames/leviathan/leviathan7.html){:target="\_blank"}

Login to the server using the password obtained from the previous level [Leviathan level 6]({% post_url 2022-03-02-overthewire-leviathan-6 %}).  

username: `leviathan7`  

```ssh
ssh leviathan7@leviathan.labs.overthewire.org -p 2223
```

This is not an actual challenge so there is nothing to do except read a file.

Checking the home directory there is a file `CONGRATUALATION` and reading the file will give a congratulation message.

```console
leviathan7@leviathan:~$ ls
CONGRATULATIONS

leviathan7@leviathan:~$ cat CONGRATULATIONS 
Well Done, you seem to have used a *nix system before, now try something more serious.
```

That is the Leviathan series of challenges complete.
