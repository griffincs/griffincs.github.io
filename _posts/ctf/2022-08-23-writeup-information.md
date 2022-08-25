---
layout: page
subheadline: Practice CTF
title:  "Problem Writeup: Information"
teaser: "Category: Forensics"
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
author: mo
---

Category: Forensics

## Description
```
Files can always be changed in a secret way. Can you find the flag? cat.jpg
```

## Approach
First, grab the `cat.jpg` file using `wget`. Next, run `file` to make sure it's an image:

```bash
pimaker-picoctf@webshell:~$ file cat.jpg
cat.jpg: JPEG image data, JFIF standard 1.02, aspect ratio, density 1x1, segment length 16, baseline, precision 8, 2560x1598, components 3
pimaker-picoctf@webshell:~$ 
```
Then, run `binwalk` to check for hidden files:

```bash
pimaker-picoctf@webshell:~$ binwalk cat.jpg

DECIMAL       HEXADECIMAL     DESCRIPTION
--------------------------------------------------------------------------------
0             0x0             JPEG image data, JFIF standard 1.02

pimaker-picoctf@webshell:~$ 
```
Then, run `strings` with `grep` to check for the flag:

```bash
pimaker-picoctf@webshell:~$ strings cat.jpg |grep picoCTF{
pimaker-picoctf@webshell:~$ 
```

Finally, open the file in a hex editor in Visual Code Studio to check the header and examine the contents.

```bash
......JFIF......
.......0Photosho
p 3.0.8BIM......
....t..PicoCTF..
..........http:/
/ns.adobe.com/xa
p/1.0/.<?xpacket
begin='...' id=
'W5M0MpCehiHzreS
zNTczkc9d'?>.<x:
xmpmeta xmlns:x=
'adobe:ns:meta/'
x:xmptk='Image:
:ExifTool 10.80'
>.<rdf:RDF xmlns
:rdf='http://www
.w3.org/1999/02/
22-rdf-syntax-ns
#'>.. <rdf:Descr
iption rdf:about
=''.  xmlns:cc='
http://creativec
ommons.org/ns#'>
.  <cc:license r
df:resource='cGl
jb0NURnt0aGVfbTN
0YWRhdGFfMXNfbW9
kaWZpZWR9'/>. </
rdf:Description>
.. <rdf:Descript
ion rdf:about=''
.  xmlns:dc='htt
p://purl.org/dc/
elements/1.1/'>.
 <dc:rights>.
<rdf:Alt>.    <
rdf:li xml:lang=
'x-default'>Pico
CTF</rdf:li>.
</rdf:Alt>.  </d
c:rights>. </rdf
:Description>.</
rdf:RDF>.</x:xmp
meta>
```

Two strings look like they might be in base64: `W5M0MpCehiHzreSzNTczkc9d` and `cGljb0NURnt0aGVfbTN0YWRhdGFfMXNfbW9kaWZpZWR9`. We can convert them in Linux with `echo`. The first string gives us gibberish; the second gives us the flag: 

```bash
samkoenen@PM-MacBook-Pro griffincs.github.io % echo W5M0MpCehiHzreSzNTczkc9d | base64 -d                                                                                                                                   
[�42���!��573��]%                                                                                                                                                                                                          
samkoenen@PM-MacBook-Pro griffincs.github.io % echo cGljb0NURnt0aGVfbTN0YWRhdGFfMXNfbW9kaWZpZWR9 | base64 -d                        
picoCTF{the_m3tadata_1s_modified}%                                                                                                                                                                                         
samkoenen@PM-MacBook-Pro griffincs.github.io %
```