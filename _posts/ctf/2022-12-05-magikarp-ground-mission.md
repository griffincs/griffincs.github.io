---
layout: page
subheadline: Practice CTF
title:  "Problem Writeup: Magikarp Ground Mission - CTF 7"
teaser: "This problem introduces us to ssh and changing directories in Linux."
meta_teaser: 
breadcrumb: true
categories:
    - ctf
tags:
    - blog
    - content
    - practice
image:
    title: 
    caption: 
    caption_url: 
author: mrk
---

Category: General Skills

## Description for Magikarp Ground Mission

"Do you know how to move between directories and read files in the shell? Start the container, `ssh` to it, and then `ls` once connected to begin. Login via `ssh` as `ctf-player` with the password, `6dee9772`."

## Approach

`ssh` stands for Secure Shell, and it is a Linux tool that is similar to `netcat` in function:  both `ssh` and `netcat` allow us to connect remotely to another computer. The essential difference is that `ssh` allows us to make an encrypted connection (which is why it is called "secure shell").

Once we've established an `ssh` connection, we have essentially used our computer to access a shell on another computer. To do this we'll need 1) a user account on the host machine, 2) a password to that account so we can login remotely.

## Opening the `ssh` Connection

For this problem, we first need to click the blue "Start Instance" button in the problem box and wait a few seconds until the "Challenge Endpoint" information appears. Copy this command and paste it into your webshell. When asked if you want to continue connecting, type "yes" and hit enter. When asked for the password, copy and paste the password from the problem statement:

```
pimaker-picoctf@webshell:~$ ssh ctf-player@venus.picoctf.net -p 54085
The authenticity of host '[venus.picoctf.net]:54085 ([3.131.124.143]:54085)' can't be established.
ED25519 key fingerprint is SHA256:P1f6h95BrSVnJbm2AKhphfHHGEyAeThib/rN/AwKs24.
This host key is known by the following other names/addresses:
    ~/.ssh/known_hosts:1: [hashed name]
Are you sure you want to continue connecting (yes/no/[fingerprint])? yes
Warning: Permanently added '[venus.picoctf.net]:54085' (ED25519) to the list of known hosts.
ctf-player@venus.picoctf.net's password:
```

Once we enter the correct password, the `ssh` connection is completed and our command prompt changed to match the user account we have accessed--in this case, `ctf-player@pico-chall`:

```
Welcome to Ubuntu 18.04.5 LTS (GNU/Linux 5.4.0-1041-aws x86_64)

 * Documentation:  https://help.ubuntu.com
 * Management:     https://landscape.canonical.com
 * Support:        https://ubuntu.com/advantage
This system has been minimized by removing packages and content that are
not required on a system that users do not log into.

To restore this content, you can run the 'unminimize' command.

The programs included with the Ubuntu system are free software;
the exact distribution terms for each program are described in the
individual files in /usr/share/doc/*/copyright.

Ubuntu comes with ABSOLUTELY NO WARRANTY, to the extent permitted by
applicable law.

ctf-player@pico-chall$
```

## Finding the Flag

Once connected, the first step is to explore our working directory (the directory we are currently in) by typing `ls`. We have two files in our directory;

```bash
ctf-player@pico-chall$ ls
1of3.flag.txt  instructions-to-2of3.txt
ctf-player@pico-chall$ 
```

Let's use `cat` to explore each file:

```bash
ctf-player@pico-chall$ cat 1of3.flag.txt 
picoCTF{xxsh_
ctf-player@pico-chall$ cat instructions-to-2of3.txt 
Next, go to the root of all things, more succinctly `/`
ctf-player@pico-chall$ 
```

The first file contains what we might expect:  1/3 of the flag. The other file tells us to go to the root directory (`/`), where all the system files are stored. We can do this with the change directory command:  `cd /`

```bash
ctf-player@pico-chall$ cd /
ctf-player@pico-chall$ ls
2of3.flag.txt  bin  boot  dev  etc  home  instructions-to-3of3.txt  lib  lib64  media  mnt  opt  proc  root  run  sbin  srv  sys  tmp  usr  var
ctf-player@pico-chall$ 
```

When we list the files of the root directory, we see the usual directories found here on a Linux system. But we also have two new files to explore:

```bash
ctf-player@pico-chall$ cat 2of3.flag.txt 
0ut_0f_\/\/4t3r_
ctf-player@pico-chall$ cat instructions-to-3of3.txt 
Lastly, ctf-player, go home... more succinctly `~`
ctf-player@pico-chall$ 
```

We found the second 1/3 of the flag, and need to change to the home directory (`~`) with the command `cd ~`:

```bash
ctf-player@pico-chall$ cd ~
ctf-player@pico-chall$ ls
3of3.flag.txt  drop-in
ctf-player@pico-chall$ cat 3of3.flag.txt 
540e4e79}
ctf-player@pico-chall$ 
```

When we explore the final in the home directory, we have the last part of the flag. Combining all three of the pieces into one string gives us the final and correct flag:  `picoCTF{xxsh_0ut_0f_\/\/4t3r_540e4e79}`.

