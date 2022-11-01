---
layout: page
subheadline: Practice CTF
title:  "Problem Writeup: Nice Netcat and Let's Warm Up - CTF 3"
teaser: "This problem introduces us to the Linux tool `netcat`, a powerful tool for connecting to other computers, port scanning, and port listening."
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

"There is a nice program that you can talk to by using this command in a shell: `$ nc mercury.picoctf.net 49039`, but it doesn't speak English..."


## Approach

This problem introduces us to the Linux tool `netcat`, a powerful tool for connecting to other computers, port scanning, and port listening.

### Running netcat

When we run the given `netcat` command, we get a bunch of numbers:

```
pimaker-picoctf@webshell:~$ nc mercury.picoctf.net 49039
112 
105 
99 
111 
67 
84 
70 
123 
103 
48 
48 
100 
95 
107 
49 
116 
116 
121 
33 
95 
110 
49 
99 
51 
95 
107 
49 
116 
116 
121 
33 
95 
51 
100 
56 
52 
101 
100 
99 
56 
125 
10
```

The numbers don't seem to follow any pattern, and the hints point us to solving another CTF problem "Let's Warm Up." Before looking at that problem, let's save the output of this netcat connection to a file so we don't have to run the netcat command again.

To do this, press CTRL + C to end the current netcat connection, the hit the UP arrow to recall the last netcat command. Before pressing enter, we want to add ` > file.txt` to this command. This will tell the shell to save the netcat output to a file named `file.txt` instead of printing it to the screen. When we run the command, it looks like nothing happens at first.

```
pimaker-picoctf@webshell:~$ nc mercury.picoctf.net 49039 > file.txt

```

But if we cancel the netcat connection and run `cat file.txt`, we see that we now have a `file.txt` with all the numbers in it. Let's go to the "Let's Warm Up" problem to see if it can help us figure out what to do with these numbers.

### Description for Let's Warm Up

"If I told you a word started with 0x70 in hexadecimal, what would it start with in ASCII?"

### Approach

This looks like a pretty straightforward problem of translating a hexadecimal value into a keyboard (or ASCII) character. At the most basic level, computers represent all information in binary, a number system that uses only 1's and 0's. So every keyboard character is assigned a number--a number than can be expressed in the decimal system, the hexadecimal system, or the binary system.

In this can we have "0x70", a hexadecimal number, that stands for a certain keyboard character. We just need to translate this number to the right character. To do this, let's use CyberChef.

The recipe we need is "From Hex", and the input is just `0x70`. This gives us the output `p`. If we wrap this letter in the normal CTF flag notation, we get "picoCTF{p}", which is the correct answer to this problem.

### Back to Nice Netcat

Since "Let's Warm Up" was the hint for the "Nice Netcat" problem, we should expect our list of numbers in `file.txt` to be a list of numbers representing keyboard characters. But instead of hexadecimal numbers, these are plain decimal numbers.

So, let's change our CyberChef recipe to "From Decimal" and paste the list of numbers in `file.txt` into the Output box in CyberChef. CyberChef automatically turns the new lines into spaces and gives us our flag.