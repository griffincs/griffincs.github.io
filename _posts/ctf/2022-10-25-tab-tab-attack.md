---
layout: page
subheadline: Practice CTF
title:  "Problem Writeup: Tab, Tab, Attack - CTF 2"
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

## Description

"Using tabcomplete in the Terminal will add years to your life, esp. when dealing with long rambling directory structures and filenames: Addadshashanammu.zip"

## Approach

This problem teaches us the time-saving power of the TAB key and gives us practice navigating a Linux filesystem (using `cd` and `ls`). 

### Unzipping the File

We begin by using `wget` to download the file. Since it's a `.zip` file--a compressed file or folder(s)--we'll begin by unzipping it with Linux's built-in `unzip` tool:

```bash

```
