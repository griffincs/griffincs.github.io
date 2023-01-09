---
layout: page
subheadline: Practice CTF
title:  "Problem Writeup: Python Wrangling, Wave a flag, Static ain't always noise - CTF 8"
teaser: "This problem introduce us to executing Python scripts and BASH scripts in Linux."
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

## Description for Python Wrangling

"Python scripts are invoked kind of like programs in the Terminal... Can you run this Python script using this password to get the flag?"

## Approach

This problem

## Description for Wave a Flag

"Can you invoke help flags for a tool or binary? This program has extraordinarily helpful information..."

## Approach

This problem teaches us how to identify binaries (i.e., programs), how to make them executable with `chmod`, and how to execute them in the Linux shell. We begin, as we often do, by using `wget` to download the file linked in the description. This command downloads a file called `warm`.

We first want to inspect `warm` a bit to learn what kind of file it is. Running `cat` on it doesn't give us anything useful, so let's use the `file` command to learn more about `warm`:

```bash
pimaker-picoctf@webshell:~$ file warm
warm: ELF 64-bit LSB pie executable, x86-64, version 1 (SYSV), dynamically linked, interpreter /lib64/ld-linux-x86-64.so.2, for GNU/Linux 3.2.0, BuildID[sha1]=7b3da2efd83a2b9154697b6c7f6474042e1fd033, with debug_info, not stripped
pimaker-picoctf@webshell:~$
```

Now we know that `warm` is an "executable" file, or a program (a 'binary' in Linux). To run `warm` from the command prompt, we use this command:

```bash
pimaker-picoctf@webshell:~$ ./warm
-bash: ./warm: Permission denied
pimaker-picoctf@webshell:~$
```

But this command tells us we don't have the right permissions to run this file. So, to change the file's "mode", we use the Linux command `chmod`, which is an abbreviation for "change mode":

```bash
pimaker-picoctf@webshell:~$ chmod +x warm
```

In this command `+x` means we are adding (`+`) the permission to execute (`x`) the file called `warm`. (Read more about `chmod` by running `man chmod` in the terminal.)

Now we can try running `warm` again:

```bash
pimaker-picoctf@webshell:~$ ./warm
Hello user! Pass me a -h to learn what I can do!
pimaker-picoctf@webshell:~$
```

Looks like we need to add a `-h` to our execute commmand:

```bash
pimaker-picoctf@webshell:~$ ./warm -h
Oh, help? I actually don't do much, but I do have this flag here: picoCTF{b1scu1ts_4nd_gr4vy_6635aa47}
pimaker-picoctf@webshell:~$
```

And we're done!

## Description for Static ain't always noise

"Can you look at the data in this binary: static? This BASH script might help!"

## Approach

This problem introduces us to bash scripts, which are small Linux shell programs we can run in the terminal. We will first solve this problem using the bash script, then we'll solve it a much faster way.

First, we use `wget` to download the two files:  `static` and `ltdis.sh`. The `.sh` file extension in `ltdis.sh` tells us it is a bash script. Let's begin by investigating what kind of file `static` is:

```bash
pimaker-picoctf@webshell:~$ file static
static: ELF 64-bit LSB pie executable, x86-64, version 1 (SYSV), dynamically linked, interpreter /lib64/ld-linux-x86-64.so.2, for GNU/Linux 3.2.0, BuildID[sha1]=7eb9ee1907cc878f15f9949988893b1f0ab1ebdf, not stripped
pimaker-picoctf@webshell:~$
```

Since `static` is an executable (and it's from a trusted source), let's make sure it's executable with `chmod` and then run it:

```bash
pimaker-picoctf@webshell:~$ chmod +x static
pimaker-picoctf@webshell:~$ ./static
Oh hai! Wait what? A flag? Yes, it's around here somewhere!
pimaker-picoctf@webshell:~$
```

That didn't get us very far, so let's investigate `ltdis.sh` next with `cat`:

```bash
pimaker-picoctf@webshell:~$ cat ltdis.sh 
#!/bin/bash



echo "Attempting disassembly of $1 ..."


#This usage of "objdump" disassembles all (-D) of the first file given by 
#invoker, but only prints out the ".text" section (-j .text) (only section
#that matters in almost any compiled program...

objdump -Dj .text $1 > $1.ltdis.x86_64.txt


#Check that $1.ltdis.x86_64.txt is non-empty
#Continue if it is, otherwise print error and eject

if [ -s "$1.ltdis.x86_64.txt" ]
then
        echo "Disassembly successful! Available at: $1.ltdis.x86_64.txt"

        echo "Ripping strings from binary with file offsets..."
        strings -a -t x $1 > $1.ltdis.strings.txt
        echo "Any strings found in $1 have been written to $1.ltdis.strings.txt with file offset"



else
        echo "Disassembly failed!"
        echo "Usage: ltdis.sh <program-file>"
        echo "Bye!"
fi
pimaker-picoctf@webshell:~$ 
```

The variable `$1` in this file refers to the file name we pass in with the script command. So, to run this bash script on `static`, we use the command `bash ltdis.sh static`:

```bash
pimaker-picoctf@webshell:~$ bash ltdis.sh static
Attempting disassembly of static ...
Disassembly successful! Available at: static.ltdis.x86_64.txt
Ripping strings from binary with file offsets...
Any strings found in static have been written to static.ltdis.strings.txt with file offset
pimaker-picoctf@webshell:~$
```

Based on this output, we should search in `static.ltdis.strings.txt` for the flag. We can use `cat` and `grep` to make this much easier:

```bash
pimaker-picoctf@webshell:~$ cat static.ltdis.strings.txt | grep pico
   1020 picoCTF{d15a5m_t34s3r_ae0b3ef2}
pimaker-picoctf@webshell:~$
```

And we are done! Now, let's consider a much faster solution to this problem.

## The Approach #2

Remember back a few problems to the "Strings It" problem? We solved it using the command `strings` and `grep`. Let's try a similar approach here with `static`:

```bash
pimaker-picoctf@webshell:~$ strings static | grep pico
picoCTF{d15a5m_t34s3r_ae0b3ef2}
pimaker-picoctf@webshell:~$
```

In this case, remembering a previous solution makes this new problem trivial (though we still learned some important things about bash scripts.)