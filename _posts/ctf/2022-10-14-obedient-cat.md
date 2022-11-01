---
layout: page
subheadline: Practice CTF
title:  "Problem Writeup: Obedient Cat - CTF 1"
teaser: "This is a very simple problem that introduces us to the webshell and to two important Linux commands:  `wget` and `cat`."
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

## Description

"This file has a flag in plain sight (aka "in-the-clear"). Download flag."

## Approach

This is a very simple problem that introduces us to the webshell and to two important Linux commands:  `wget` and `cat`.

### wget

`wget` is a Linux tool for retrieving files from the internet (it is short for "web get"). Instead of downloading the file linked in the problem description, we will download it into the webshell. Though it is coming from a pretty trusted source, it's good not to download the mystery file directly into our Downloads folder, if we can help it.

To download the file, we first right-click on the link, then select "Copy Link Address". This copies the URL to our clipboard. Then in the webshell, type `wget`, a space, and paste in the URL we just copied:

```
pimaker-picoctf@webshell:~$ wget https://mercury.picoctf.net/static/a5683698ac318b47bd060cb786859f23/flag
--2022-10-17 22:37:09--  https://mercury.picoctf.net/static/a5683698ac318b47bd060cb786859f23/flag
Resolving mercury.picoctf.net (mercury.picoctf.net)... 18.189.209.142
Connecting to mercury.picoctf.net (mercury.picoctf.net)|18.189.209.142|:443... connected.
HTTP request sent, awaiting response... 200 OK
Length: 34 [application/octet-stream]
Saving to: 'flag.1'

flag              100%[==================>]      34  --.-KB/s    in 0s      

2022-10-17 22:37:10 (12.7 MB/s) - 'flag.1' saved [34/34]

pimaker-picoctf@webshell:~$ 
```

### ls

When we hit ENTER, a lot of things happen almost instantly. `wget` connects to the URL we pasted, requests the file, then saves it to the webshell (in our user directory). To see the file that was downloaded, enter `ls` (short for "list") in the command prompt:

```
pimaker-picoctf@webshell:~$ ls
README.txt  flag
pimaker-picoctf@webshell:~$ 
```

There are currently two files in our user directory. The `README.txt` file contains a lot of useful tips and information for using the pico webshell; you'll be able to read it after finishing the next step.

### cat

To read the contents of the `flag` file, we will use `cat`, another Linux tool that shows us the contents of a file or allows us to add to the file ("cat" is short for "concatenate", which means to join together). To see the contents of the file we just downloaded, we enter `cat flag`:

```
pimaker-picoctf@webshell:~$ cat flag
picoCTF{s4n1ty_v3r1f13d_4a2b35fd}
pimaker-picoctf@webshell:~$ 
```

The weird string that displays is the flag we are looking for. All the flags in picoCTF are in this format. We copy and paste it into the problem box and click "Submit" to finish this problem.