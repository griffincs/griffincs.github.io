---
layout: page
subheadline: Practice CTF
title:  "Problem Writeup: What's a Netcat? - CTF 3"
teaser: "This problem teaches us the time-saving power of the TAB key and gives us practice navigating a Linux filesystem."
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

## Description for Nice Netcat

"Using netcat (nc) is going to be pretty important. Can you connect to `jupiter.challenges.picoctf.org` at port `25103` to get the flag?"

## Approach

This problem introduces us to the Linux tool `netcat`, a powerful tool for connecting to other computers, port scanning, and port listening.

### Running netcat

We can open the manual page (i.e., the documentation page) for `netcat` by typing `man nc` in the terminal. The page that appears tells us about netcat and--most importantly--how to run a basic netcat command in this format:  `nc [destination] [port]`. So for this problem, we run this command:

```
pimaker-picoctf@webshell:~$ nc jupiter.challenges.picoctf.org 25103
You're on your way to becoming the net cat master
picoCTF{nEtCat_Mast3ry_d0c64587}
```

That was easy!

Press CTRL + C to end the netcat connection.
