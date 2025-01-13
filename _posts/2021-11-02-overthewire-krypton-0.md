---
title: Overthewire Krypton Level 0 -> 1
date: 2021-11-02 23:14:00 +0000
categories: [OverTheWire, Krypton]
tags: [overthewire, krypton]
description: Solution for Overthewire Krypton level 1 challenge
---

Solution for the Overthewire.org [Krypton level 0 -> 1](https://overthewire.org/wargames/krypton/krypton0.html){:target="\_blank"}

## Level Info  

Welcome to Krypton! The first level is easy. The following string encodes the password using Base64:  

`S1JZUFRPTklTR1JFQVQ=`  

Use this password to log in to krypton.labs.overthewire.org with username krypton1 using SSH on port 2231. You can find the files for other levels in /krypton/  

## Walkthrough

The description tells us the password has been encoded using base64 encoding. So we only need to decode the string to obtain the password. Linux terminal has a base64 command that can be used to decode the password.

```console
~$ echo S1JZUFRPTklTR1JFQVQ= | base64 -d
KRYPTON*******
```
