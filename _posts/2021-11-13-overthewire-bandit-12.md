---
title: OverTheWire Bandit Level 11 -> 12
date: 2021-11-13 23:10:00 +0000
categories: [OverTheWire, Bandit]
tags: [overthewire, bandit]
description: Solution for OverTheWire Bandit level 12 challenge
media_subpath: /assets/img/overthewire/bandit
---

Solution for the Overthewire.org [Bandit level 11 -> 12](https://overthewire.org/wargames/bandit/bandit12.html){:target="\_blank"}

## Level Goal

The password for the next level is stored in the file data.txt, where all lowercase (a-z) and uppercase (A-Z) letters have been rotated by 13 positions

---

## Walkthrough

Login to the server using the password obtained from the previous level [Bandit level 10 -> 11]({% post_url 2021-11-13-overthewire-bandit-11 %}).  

username: `bandit11`  

```ssh
ssh bandit11@bandit.labs.overthewire.org -p 2220
```

The file `data.txt` is located in the home directory.  

```console
bandit11@bandit:~$ ls
data.txt 
```

We `cat` the contents of the file and can see that it does not make any sense when we try to read.  

```console
bandit11@bandit:~$ cat data.txt
Gur cnffjbeq vf 5Gr8L4qetPEsPk8htqjhRK8XSP6x2RHh
```

Going back to the description it mentions characters being `rotated`, this immediately bring [ROT13](https://en.wikipedia.org/wiki/ROT13) to mind.  
In a [ROT13](https://en.wikipedia.org/wiki/ROT13) cipher characters are rotated 13 places this means  

`a` becomes `n`  
`a` is 1st letter of the alphabet.  
Rotate 13 places  1 + 13 = 14.  
14th letter of alphabet is `n`.

`t` becomes `g`  
`t` is the 20th letter of the alphabet.  
Rotate 13 places 20 + 13 = 33.  
Since 33 is greater then 26 (26 letters in alphabet) we take 26 from 33 to bring it back into the alphabet range.  
33 - 26 = 7  
7th letter of the alphabet is `g`.

### Full ROT13 mappings

| Character | ROT13 | Character | ROT13 | Character |
| :-------: | :---: | :-------: | :---: | :-------: |
|     a     |  ->   |     n     |  ->   |     a     |
|     b     |  ->   |     o     |  ->   |     b     |
|     c     |  ->   |     p     |  ->   |     c     |
|     d     |  ->   |     q     |  ->   |     d     |
|     e     |  ->   |     r     |  ->   |     e     |
|     f     |  ->   |     s     |  ->   |     f     |
|     g     |  ->   |     t     |  ->   |     g     |
|     h     |  ->   |     u     |  ->   |     h     |
|     i     |  ->   |     v     |  ->   |     i     |
|     j     |  ->   |     w     |  ->   |     j     |
|     k     |  ->   |     x     |  ->   |     k     |
|     l     |  ->   |     y     |  ->   |     l     |
|     m     |  ->   |     z     |  ->   |     m     |

---

Now with an understanding of ROT13 we can move onto the level.  

We can use a linux command line tool `tr` (translate) to translate the rotated characters back to their original posistion.

```console
bandit11@bandit:~$ cat data.txt
Gur cnffjbeq vf 5Gr8L4qetPEsPk8htqjhRK8XSP6x2RHh

bandit11@bandit:~$ cat data.txt | tr a-zA-Z n-za-mN-ZA-M
The password is 5Te8Y4##########################
```

Or we can one of many online tools like [CyberChef](https://gchq.github.io/CyberChef/) that have graphical interfaces to solve the ROT13 ciphertext.

![Image of Cyber Chef using ROT13 recipe](/CyberChef%20-%20ROT13.png)
