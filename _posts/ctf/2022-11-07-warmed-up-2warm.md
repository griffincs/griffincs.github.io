---
layout: page
subheadline: Practice CTF
title:  "Problem Writeup: Let's Warm Up, Warmed Up, and 2Warm - CTF 6"
teaser: "This problem has us explore numbers in different bases (or encodings)."
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

## Description for Let's Warm Up

"If I told you a word started with 0x70 in hexadecimal, what would it start with in ASCII?"

## Approach

Since we'll be converting bases for this problem, CyberChef will be our tool of choice. Remembering all numbers, letters, and symbols from the keyboard have a numerical value attached to them, and that ASCII is the "keyboard equivalent" of the numbers, we can use CyberChef to convert `0x70` from hexadecimal to ASCII with one recipe.

First, we copy `0x70` from the problem statement and paste it into the CyberChef input field. Then we search for the "From Hex" recipe and drag it into the Recipe field. As soon as we do that, we get `p` in the Output field. Wrapping `p` in the usual `picoCTF{}` gives us the correct flag.

---
## Description for Warmed Up

"What is `0x3D` (base 16) in decimal (base 10)?"

## Approach

Again, CyberChef is the tool we want to use for this problem. We use the same steps from the "Let's Warm Up" problem, but there isn't a "From Base16" option. However, there is a "From Base" recipe with an option to adjust the Radix (or "root", another name for "base"). If we drag this recipe into the Recipe field and adjust the Radix to `16`, we get the right conversion in the output (`61`).

Wrapping `61` in the usual `picoCTF{}` gives us the correct flag.

---
## Description for 2Warm

"Can you convert the number 42 (base 10) to binary (base 2)?"

## Approach

Once again, we'll use CyberChef for this problem. There is a "To Binary" recipe, but this returns `4` in binary and `2` in binary, which isn't what we want. The recipe we're looking for is "To Base" with a Radix of `2`. This gives us `101010`, which gives us the correct flag when we wrap it with `picoCTF{}`.