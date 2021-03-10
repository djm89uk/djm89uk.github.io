# [PicoGym](./picogym.md) Forensics

"Forensics" challenges can include file format analysis, steganography, memory dump analysis, or network packet capture analysis.

## Contents

- [Glory of the Garden](#glory-of-the-garden)
- [So Meta](#so-meta)
- [extensions](#extensions)
- [shark on wire 1](#shark-on-wire-1)
- [What Lies Within](#what-lies-within)
- [Pitter, Patter, Platters](#pitter-patter-platters)
- [c0rrupt](#c0rrupt)
- [WhitePages](#whitepages)
- [m00nwalk](#m00nwalk)
- [like1000](#like1000)
- [shark on wire 2](#shark-on-wire-2)
- [m00nwalk2](#m00nwalk2)
- [Investigative Reversing 0](#investigative-reversing-0)
- [WebNet0](#webnet0)
- [Investigative Reversing 1](#investigative-reversing-1)
- [Investigative Reversing 2](#investigative-reversing-2)
- [Investigative Reversing 3](#investigative-reversing-3)
- [Investigative Reversing 4](#investigative-reversing-4)
- [investigation_encoded_1](#investigation-encoded-1)
- [WebNet1](#webnet1)
- [investigation_encoded_2](#investigation-encoded-2)
- [B1g_Mac](#b1g-mac)


---

### [Forensics](#contents) | [PicoGym](./picogym.md) | [PicoCTF](./picoctf.md) | [Home](./index.md)

---

## Glory of the Garden

- Author: jedavis/Danny
- 50 Points

### Description

This garden contains more than it seems.

### Hints

1. What is a hex editor?

### Attachments

<details>

<summary markdown="span">garden.jpg</summary>

<div markdonw="1">

![garden.jpg](./resources/picoctf/picogym/attachments/forensics/glory-of-the-garden/garden.jpg)

</div>

</details>

### Solutions

<details>

<summary markdown="span">Solution 1</summary>

This challenge can be solved with the in-built linux command strings and can be optimised using grep:

~~~
$ strings garden.jpg | grep pico
~~~

This searches the hex values for a string including the substring "pico".  The command returns:

~~~
Here is a flag "picoCTF{more_than_m33ts_the_3y33dd2eEF5}"
~~~

The flag is therefore picoCTF{more_than_m33ts_the_3y33dd2eEF5}

</details>

### Answer

<details>

<summary markdown="span">Flag</summary>

~~~
picoCTF{more_than_m33ts_the_3y33dd2eEF5}
~~~

</details>

---

### [Forensics](#contents) | [PicoGym](./picogym.md) | [PicoCTF](./picoctf.md) | [Home](./index.md)

---

## So Meta

- Author: Kevin Cooper/Danny
- 150 points

### Description

Find the flag in this picture.

### Hints

1. What does meta mean in the context of files?
2. Ever heard of metadata?

### Attachments

<details>

<summary markdown="span">pico_img.png</summary>

<div markdonw="1">

![pico_img.png](./resources/picoctf/picogym/attachments/forensics/so-meta/pico_img.png)

</div>

</details>

### Solutions

<details>

<summary markdown="span">Solution 1</summary>

This challenge suggests we review the meta data for the image.  A useful tool for extracting meta data from photographs is [Exiftool](https://exiftool.org/).  We can combine this with grep to deliver a concise solution:

~~~
$ exiftool pico_img.png | grep pico
~~~

This returns:

~~~
File Name                       : pico_img.png
Artist                          : picoCTF{s0_m3ta_d8944929}
~~~

Which give us the flag.

</details>

### Answer

<details>

<summary markdown="span">Flag</summary>

~~~
picoCTF{s0_m3ta_d8944929}
~~~

</details>

---

### [Forensics](#contents) | [PicoGym](./picogym.md) | [PicoCTF](./picoctf.md) | [Home](./index.md)

---

## extensions

- Author: Sanjay C/Danny
- 150 points

### Description

This is a really weird text file TXT? Can you find the flag?

### Hints

1. How do operating systems know what kind of file it is? (It's not just the ending!
2. Make sure to submit the flag as picoCTF{XXXXX}.

### Attachments

[flag.txt](./resources/picoctf/picogym/attachments/forensics/extensions/flag.txt)

### Solutions

<details>

<summary markdown="span">Solution 1</summary>

THis challenge provides a file, flag.txt.  When we open the file, we can safely assume this is not a text file.

A quick review of the hex strings returns us the first five lines:

~~~
$ strings flag.txt 
IHDR
sRGB
gAMA
        pHYs
IDATx^
~~~

We can see gAMA and sRGB strings, so we can assume this is an image file which has had the file signature corrupted.

This file can be opened in a hex editor such as [GHex](https://wiki.gnome.org/Apps/Ghex) to view and edit the hex bytes in the file signature.

The first 4 Bytes of the file are:

~~~
89 50 4E 47
. P N G
~~~

This suggests that the file is likely a png image.  We can find a detail of the PNG signature header at [filesignatures.net](https://www.filesignatures.net/index.php?page=search&search=PNG&mode=EXT).

This gives us the first 8 Bytes of a PNG file:

~~~
89 50 4E 47 0D 0A 1A 0A 
~~~

Reviewing the Bytes in GHex shows that all 8 Bytes are matched.  This is definitely a PNG file.

The extension can be changed from .txt to .png:

~~~
$ cp flag.txt flag.png
~~~

When opened, the image shows the flag:

<details>

<summary markdown="span">flag.png</summary>

![flag.png](./resources/picoctf/picogym/solutions/forensics/extensions/flag.png)

</details>

</details>

### Answer

<details>

<summary markdown="span">Flag</summary>

~~~
picoCTF{now_you_know_about_extensions}
~~~

</details>

---

### [Forensics](#contents) | [PicoGym](./picogym.md) | [PicoCTF](./picoctf.md) | [Home](./index.md)

---

## shark on wire 1

- We found this packet capture. Recover the flag.
- 150 points

### Description

We found this packet capture. Recover the flag.

### Hints

1. Try using a tool like Wireshark.
2. What are streams?

### Attachments

[capture.pcap](./resources/picoctf/picogym/attachments/forensics/shark-on-wire-1/capture.pcap)

### Solutions

<details>

<summary markdown="span">Solution 1</summary>

In this challenge, we are provided a packet capture file, capture.pcap, that contains the flag.

Two common programs that can open and view this packet capture are wireshark and tcpdump.  Using tcpdump we can load all packets and check the packet datagram for strings that may return the flag:

~~~
$ tcpdump -r capture.pcap -A | grep pico 
~~~

This returns:

~~~
reading from file capture.pcap, link-type EN10MB (Ethernet), snapshot length 262144
.....'....Upico..............
.....'....Upico..............
.....'....Upico..............
.....'....Upico..............
~~~

The flag is likely fragmented across multiple packets in the capture and therefore cannot be read directly.  Wireshark provides a tool to review data streams (IP conversations) in which the flag will likely be found, however we need to locate which conversation contains the flag which cannot be achieved in Wireshark, we can simplify this by filtering the pcap until we have a more manageable capture.

To reduce the size of the file, we can extract IP only captures, removing all ARP and ICMP packets:

~~~
$ tcpdump -r capture.pcap -w capture_ip.pcap ip
~~~

This reduces capture.pcap from 2,317 packets to 1,230 IP packets.

This can be reduced further using editcap to remove packet replicas from the capture file:

~~~
$ editcap --novlan -d capture_ip.pcap capture_ip_no_replicas.pcap 
~~~

This reduces the packet capture from 1,230 to 561.

Finally, we can filter for just UDP and TCP:

~~~
$ tcpdump -r capture_ip_no_replicas.pcap -w capture_final.pcap tcp or udp
~~~

This gives us a capture file, capture_final.pcap with only 493 captured packets of interest.

We can now interrogate the conversations using the wireshark command line utility, tshark:

~~~
$ tshark -r capture_final.pcap -z "follow,udp,ascii,1"
~~~

This isolates the udp conversation with index 1 and displays the contents in ascii format to the terminal.  As we work our way up through the various conversations, we can see the flag is identifiable in UDP stream 5:

~~~
$ tshark -r capture_final.pcap -z "follow,udp,ascii,5"
~~~

It is given in a rather illegible format with interruoting characters between each data segment.  We can open wireshark GUI program and filter using:

~~~
udp.stream eq 5
~~~

We can then use the follow udp stream function to read:

~~~
picoCTF{StaT315_63fee}
~~~

Which is NOT the flag.  The removal of repeated characters has reduced the flag length.  We can record the checksum for the UDP segment, for the first packet in this conversation this is 0x458e.

In the original capture.pcap, we can filter to find this packet:

~~~
udp.checksum eq 0x458e
~~~

We can then view the udp conversation using follow stream and get the correct flag:

~~~
picoCTF{StaT31355_636f6e6e}
~~~

</details>

### Answer

<details>

<summary markdown="span">Flag</summary>

~~~
picoCTF{StaT31355_636f6e6e}
~~~

</details>

---

### [Forensics](#contents) | [PicoGym](./picogym.md) | [PicoCTF](./picoctf.md) | [Home](./index.md)

---

## What Lies Within

- Author: Julio/Danny
- 150 points

### Description

There's something in the building. Can you retrieve the flag?

### Hints

1. There is data encoded somewhere... there might be an online decoder.

### Attachments

<details>

<summary markdown="span">buildings.png</summary>

<div markdonw="1">

![buildings.png](./resources/picoctf/picogym/attachments/forensics/what-lies-within/buildings.png)

</div>

</details>

### Solutions

<details>

<summary markdown="span">Solution 1</summary>

A quick online search finds a useful tool for decoding messages within images.  Stylesuxx's [steganography tool](https://stylesuxx.github.io/steganography/) can be used to decode the image and returns:

~~~
picoCTF{h1d1ng_1n_th3_b1t5}
~~~

Giving us the flag.

</details>

### Answer

<details>

<summary markdown="span">Flag</summary>

~~~
picoCTF{h1d1ng_1n_th3_b1t5}
~~~

</details>

---

### [Forensics](#contents) | [PicoGym](./picogym.md) | [PicoCTF](./picoctf.md) | [Home](./index.md)

---

## Pitter Patter Platters

- Author: syreal
- 200 points

### Description

'Suspicious' is written all over this disk image. Download suspicious.dd.sda1

### Hints

1. It may help to analyze this image in multiple ways: as a blob, and as an actual mounted disk.
2. Have you heard of slack space? There is a certain set of tools that now come with Ubuntu that I'd recommend for examining that disk space phenomenon...

### Attachments

suspicious.dd.sda1

### Solutions

<details>

<summary markdown="span">Solution 1</summary>

This dd file can be mounted to a loop partition to inspect files, however this may interfere with the data in the image file.  Alternatively, the program Autopsy can be used to load the image and inspect the contents.

After creating a new case file, the image can be mounted as a volume image.  Autopsy detects this image uses ext partition.  Opening the file analysis tool, we can see 3 sub directories, boot/, lost+found/ and tce/ and 1 file, suspicious-file.txt.

![autopsy_01.png](./resources/picoctf/picogym/solutions/forensics/pitter-patter-platters/autopsy_01.png)

We can inspect the contents of the file in autopsy:

~~~
Contents Of File: /1/suspicious-file.txt


Nothing to see here! But you may want to look here -->
~~~

This is interesting.  Selecting the inode id (12) from the file analysis tool we get more information on the file:

![autopsy_02.png](./resources/picoctf/picogym/solutions/forensics/pitter-patter-platters/autopsy_02.png)

From here, we can access the data blocks for the file directly (2049):

![autopsy_03.png](./resources/picoctf/picogym/solutions/forensics/pitter-patter-platters/autopsy_03.png)

This shows the ASCII contents of the 2049 fragment including the slack space, in which we can see what appears to be an inverted flag:

~~~
ASCII Contents of Fragment 2049 in suspicious.dd.sda1-0-0


Nothing to see here! But you may want to look here -->
}.6.f.a.0.9.2.5.f._.3.<._.|.L.m._.1.1.1.t.5._.3.b.{.F.T.C.o.c.i.p........................................................................................................................................................................................................................................................................................................................................................................................................................................................................................................................................................................................................................................................................................................................................................................................................................................................................................................................................
~~~

This can be reversed to give the flag: 

~~~
picoCTF{b3_5t111_mL|_<3_f5290af6}
~~~

</details>

### Answer

<details>

<summary markdown="span">Flag</summary>

~~~
picoCTF{b3_5t111_mL|_<3_f5290af6}
~~~

</details>

---

### [Forensics](#contents) | [PicoGym](./picogym.md) | [PicoCTF](./picoctf.md) | [Home](./index.md)

---

## c0rrupt

- Author: Danny
- 250 points

### Description

We found this file. Recover the flag.

### Hints

1. Try fixing the file header.

### Attachments

[mystery](./resources/picoctf/picogym/attachments/forensics/c0rrupt/mystery)

### Solutions

<details>

<summary markdown="span">Solution 1</summary>

Solution here

</details>

### Answer

<details>

<summary markdown="span">Flag</summary>

~~~
picoCTF{}
~~~

</details>

---

### [Forensics](#contents) | [PicoGym](./picogym.md) | [PicoCTF](./picoctf.md) | [Home](./index.md)

---

## WhitePages

- Author: John Hammond
- 250 points

### Description

I stopped using YellowPages and moved onto WhitePages... but the page they gave me is all blank!

### Hints

None

### Attachments

<details>

<summary markdown="span">whitepages.txt</summary>

~~~
                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                
~~~

</details>

### Solutions

<details>

<summary markdown="span">Solution 1</summary>

Solution here

</details>

### Answer

<details>

<summary markdown="span">Flag</summary>

~~~
picoCTF{}
~~~

</details>

---

### [Forensics](#contents) | [PicoGym](./picogym.md) | [PicoCTF](./picoctf.md) | [Home](./index.md)

---
## m00nwalk

- Author: Joon
- 250 points

### Description

Decode this message from the moon.

### Hints

1. How did pictures from the moon landing get sent back to Earth?
2. What is the CMU mascot?, that might help select a RX option.

### Attachments

[message.wav](./resources/picoctf/picogym/attachments/forensics/m00nwalk/message.wav)

### Solutions

<details>

<summary markdown="span">Solution 1</summary>

Solution here

</details>

### Answer

<details>

<summary markdown="span">Flag</summary>

~~~
picoCTF{}
~~~

</details>

---

### [Forensics](#contents) | [PicoGym](./picogym.md) | [PicoCTF](./picoctf.md) | [Home](./index.md)

---
## like1000

- Author: Danny
- 250 points

### Description

This .tar file got tarred a lot.

### Hints

1. Try and script this, it'll save you a lot of time.

### Attachments

[1000.tar](./resources/picoctf/picogym/attachments/forensics/like1000/1000.tar)

### Solutions

<details>

<summary markdown="span">Solution 1</summary>

Solution here

</details>

### Answer

<details>

<summary markdown="span">Flag</summary>

~~~
picoCTF{}
~~~

</details>

---

### [Forensics](#contents) | [PicoGym](./picogym.md) | [PicoCTF](./picoctf.md) | [Home](./index.md)

---
## shark on wire 2

- Author: Danny
- 300 points

### Description

We found this packet capture. Recover the flag that was pilfered from the network.

### Hints

None

### Attachments

[capture.pcap](./resources/picoctf/picogym/attachments/forensics/shark-on-wire-2/capture.pcap)

### Solutions

<details>

<summary markdown="span">Solution 1</summary>

Solution here

</details>

### Answer

<details>

<summary markdown="span">Flag</summary>

~~~
picoCTF{}
~~~

</details>

---

### [Forensics](#contents) | [PicoGym](./picogym.md) | [PicoCTF](./picoctf.md) | [Home](./index.md)

---
## m00nwalk2

- Author: Joon
- 300 points

### Description

Revisit the last transmission. We think this transmission contains a hidden message. There are also some clues clue 1, clue 2, clue 3.

### Hints

1. Use the clues to extract the another flag from the .wav file

### Attachments

[message.wav](./resources/picoctf/picogym/attachments/forensics/m00nwalk2/message.wav)

[clue1.wav](./resources/picoctf/picogym/attachments/forensics/m00nwalk2/clue1.wav)

[clue2.wav](./resources/picoctf/picogym/attachments/forensics/m00nwalk2/clue2.wav)

[clue3.wav](./resources/picoctf/picogym/attachments/forensics/m00nwalk2/clue3.wav)

### Solutions

<details>

<summary markdown="span">Solution 1</summary>

Solution here

</details>

### Answer

<details>

<summary markdown="span">Flag</summary>

~~~
picoCTF{}
~~~

</details>

---

### [Forensics](#contents) | [PicoGym](./picogym.md) | [PicoCTF](./picoctf.md) | [Home](./index.md)

---
## Investigative Reversing 0

- Author: Danny Tunitis
- 300 points

### Description

We have recovered a binary and an image. See what you can make of it. There should be a flag somewhere.

### Hints

1. Try using some forensics skills on the image.
2. This problem requires both forensics and reversing skills.
3. A hex editor may be helpful.

### Attachments

[mystery](./resources/picoctf/picogym/attachments/forensics/investigative-reversing-0/mystery)

<details>

<summary markdown="span">mystery.png</summary>

<div markdonw="1">

![mystery.png](./resources/picoctf/picogym/attachments/forensics/investigative-reversing-0/mystery.png)

</div>

</details>

### Solutions

<details>

<summary markdown="span">Solution 1</summary>

Solution here

</details>

### Answer

<details>

<summary markdown="span">Flag</summary>

~~~
picoCTF{}
~~~

</details>

---

### [Forensics](#contents) | [PicoGym](./picogym.md) | [PicoCTF](./picoctf.md) | [Home](./index.md)

---
## WebNet0

- Author: Jason
- 350 points

### Description

We found this packet capture and key. Recover the flag.

### Hints

1. Try using a tool like Wireshark.
2. How can you decrypt the TLS stream?

### Attachments

[capture.pcap](./resources/picoctf/picogym/attachments/forensics/webnet0/capture.pcap)

<details>

<summary markdown="span">picopico.key</summary>

~~~
-----BEGIN PRIVATE KEY-----
MIIEvQIBADANBgkqhkiG9w0BAQEFAASCBKcwggSjAgEAAoIBAQCwKlFPNKjseJF5
puCJU5x38XcT1eQge5zOKNahAlYudvGVOEs61TnIgvcER4ko8i3OCwak2/atcGk3
oz9jFKep7XFEYNP31IwwD9j/YazlKy4DRLGObOyIZUU1f2WRA7Uhf0POQXsDT1oU
X32jMKZkQSSDW4MRZd9trJYdO2TrcEPMsBiZQlFlvgnNwl3QlawozTHLAJKI36j1
cPwSMMeNca1e0Zi1s7R5IxfhpNXOBF0FmxiWvmeOHbaspyHg8UEmGBrkd4k4wXSK
GQvrc8QjycP4ScEdquxJiYnDT8iEbAq70/7f/5NIN1DE9YoGJqKYjTS9nRPB4Yvj
JN/SJnhvAgMBAAECggEACCnd3LrG/TZVH3sROqvqO1CwQPYPfUXdLVyNHab7EWon
pc+XBOHurJENG2CpRYF7h+nQ5ADhfIYSCicBf/jsEB7VueJ20CxEVtHVL3h6R6Bp
oHMle0Em8OcofuMpdL/kO+om3T8BkVSzCvCl5NMTUuAF7iRmfX7oDLALwM0IzzQv
2un+2UmT15rgAZfl3IL1PGvJhbhLxfeeyPE9MBy1SqBjQ9rNFn8sQv959J6BHz4b
EpK//ErtNP2yh7oiVBBgKEQ1gEuOjQC/4oxoqCFfZaf9XNRCxB/zY1nUprvJyz09
NMQWNF2EmvmBVGfoTxmuut5N0GbVr2UyHxWMKm2sOQKBgQDpb2+AWgWlGtetuLKJ
fJs8dnd6LhnafbKCOXMOT68qMBRoTpBtVTLRVSNvWCm8m4TTEazX4+ZA+bJFwUFw
aATDmHcr6lMI3tNKrcsnY2F7o5I4z6mwuRuSeszq/ndxZqCzwCu4nKixh3cznp7j
JiElNG0d8Lu5eQgmVAK1AhWXfQKBgQDBMa9ga7VJUP4pzcHnWAoi34OpfjvQYeGl
IKL3AKO4OedaHdH9qid41PQHnL7O3xzN669SkLZ5s0d88A/LFLk4oZNMKdkSTQIQ
+AMbXH01HGFvnCOuPg/FbNp1wS7zJEg5u5HFQWyMPNJLr/hZ6g2Yp+UGpAcGTwM/
RCPVAPhLWwKBgQDAB0OaOnPaVjKGXiHAqBirrGiswa/S5QQrzEaxxys5cUPYaoi0
6BldysPTnJr45JZna2rcTkXjvYTBjTDf3zHMFWgzYBfefC8kh8NPK5nNs8ldorbd
AemEnjBkP+DSELKyK6vLulOrdtzAQgRCp+MsT+xTbO2ArefeX826SXSpoQKBgC2v
nDOHBQXje1dTawlUToFUrgQE8AwlOYEdKKyUoCLOvqEW8DO2a0MtyM+MB6tQI7Wm
iH1T73L0LHGlK3bw3aRAwV5/fu/O+jAdFk8AHjPTFE+acu2fi4c6aKb0GjAxYksU
yjIFeK/pKinv4SESMkjpW0WowGiDgtcRPBAA/LaFAoGAfEM1rfM0v3UmB7PS6u0m
P3ckP2CFCdaryXPfC52GBcJ3Q46YpsQvLTVotM+teHvTjNw2jwwZxIl4NenGSEj3
KDhQoOiQC9BrDD+DB4I9+T9nxT3g7R6MrgITghB4We7TVhL/PljnJTyDqpjNA4kY
TveAJPv6Xq1ERt5PUtX3BqQ=
-----END PRIVATE KEY-----
~~~

</details>

### Solutions

<details>

<summary markdown="span">Solution 1</summary>

Solution here

</details>

### Answer

<details>

<summary markdown="span">Flag</summary>

~~~
picoCTF{}
~~~

</details>

---

### [Forensics](#contents) | [PicoGym](./picogym.md) | [PicoCTF](./picoctf.md) | [Home](./index.md)

---
## Investigative Reversing 1

- Author: Danny Tunitis
- 350 points

### Description

We have recovered a binary and a few images: image, image2, image3. See what you can make of it. There should be a flag somewhere.

### Hints

1. Try using some forensics skills on the image.
2. This problem requires both forensics and reversing skills.
3. A hex editor may be helpful.

### Attachments

[mystery](./resources/picoctf/picogym/attachments/forensics/investigative-reversing-1/mystery)

<details>

<summary markdown="span">mystery.png</summary>

<div markdonw="1">

![mystery.png](./resources/picoctf/picogym/attachments/forensics/investigative-reversing-1/mystery.png)

</div>

</details>

<details>

<summary markdown="span">mystery2.png</summary>

<div markdonw="1">

![mystery.png](./resources/picoctf/picogym/attachments/forensics/investigative-reversing-1/mystery2.png)

</div>

</details>

<details>

<summary markdown="span">mystery3.png</summary>

<div markdonw="1">

![mystery.png](./resources/picoctf/picogym/attachments/forensics/investigative-reversing-1/mystery3.png)

</div>

</details>

### Solutions

<details>

<summary markdown="span">Solution 1</summary>

Solution here

</details>

### Answer

<details>

<summary markdown="span">Flag</summary>

~~~
picoCTF{}
~~~

</details>

---

### [Forensics](#contents) | [PicoGym](./picogym.md) | [PicoCTF](./picoctf.md) | [Home](./index.md)

---
## Investigative Reversing 2

- Author: Santiago C/Danny T
- 350 points

### Description

We have recovered a binary and an image See what you can make of it. There should be a flag somewhere.

### Hints

1. Try using some forensics skills on the image.
2. This problem requires both forensics and reversing skills.
3. What is LSB encoding?

### Attachments

[mystery](./resources/picoctf/picogym/attachments/forensics/investigative-reversing-2/mystery)

[encoded.bmp](./resources/picoctf/picogym/attachments/forensics/investigative-reversing-2/encoded.bmp)

### Solutions

<details>

<summary markdown="span">Solution 1</summary>

Solution here

</details>

### Answer

<details>

<summary markdown="span">Flag</summary>

~~~
picoCTF{}
~~~

</details>

---

### [Forensics](#contents) | [PicoGym](./picogym.md) | [PicoCTF](./picoctf.md) | [Home](./index.md)

---
## Investigative Reversing 3

- Author: Santiago C/Danny T
- 400 points

### Description

We have recovered a binary and an image See what you can make of it. There should be a flag somewhere.

### Hints

1. You will want to reverse how the LSB encoding works on this problem.

### Attachments

[mystery](./resources/picoctf/picogym/attachments/forensics/investigative-reversing-3/mystery)

[encoded.bmp](./resources/picoctf/picogym/attachments/forensics/investigative-reversing-3/encoded.bmp)

### Solutions

<details>

<summary markdown="span">Solution 1</summary>

Solution here

</details>

### Answer

<details>

<summary markdown="span">Flag</summary>

~~~
picoCTF{}
~~~

</details>

---

### [Forensics](#contents) | [PicoGym](./picogym.md) | [PicoCTF](./picoctf.md) | [Home](./index.md)

---
## Investigative Reversing 4

- Author: Santiago C/Danny T
- 400 points

### Description

We have recovered a binary and 5 images: image01, image02, image03, image04, image05. See what you can make of it. There should be a flag somewhere.

### Hints

None

### Attachments

[mystery](./resources/picoctf/picogym/attachments/forensics/investigative-reversing-4/mystery)

[Item01_cp.bmp](./resources/picoctf/picogym/attachments/forensics/investigative-reversing-4/Item01_cp.bmp)

[Item02_cp.bmp](./resources/picoctf/picogym/attachments/forensics/investigative-reversing-4/Item02_cp.bmp)

[Item03_cp.bmp](./resources/picoctf/picogym/attachments/forensics/investigative-reversing-4/Item03_cp.bmp)

[Item04_cp.bmp](./resources/picoctf/picogym/attachments/forensics/investigative-reversing-4/Item04_cp.bmp)

[Item05_cp.bmp](./resources/picoctf/picogym/attachments/forensics/investigative-reversing-4/Item05_cp.bmp)

### Solutions

<details>

<summary markdown="span">Solution 1</summary>

Solution here

</details>

### Answer

<details>

<summary markdown="span">Flag</summary>

~~~
picoCTF{}
~~~

</details>

---

### [Forensics](#contents) | [PicoGym](./picogym.md) | [PicoCTF](./picoctf.md) | [Home](./index.md)

---
## investigation-encoded-1

- Author: Santiago C
- 450 points

### Description

We have recovered a binary and 1 file: image01. See what you can make of it. NOTE: The flag is not in the normal picoCTF{XXX} format.

### Hints

None

### Attachments

[mystery](./resources/picoctf/picogym/attachments/forensics/investigation_encoded_1/mystery)

[output](./resources/picoctf/picogym/attachments/forensics/investigation_encoded_1/output)

### Solutions

<details>

<summary markdown="span">Solution 1</summary>

Solution here

</details>

### Answer

<details>

<summary markdown="span">Flag</summary>

~~~
picoCTF{}
~~~

</details>

---

### [Forensics](#contents) | [PicoGym](./picogym.md) | [PicoCTF](./picoctf.md) | [Home](./index.md)

---
## WebNet1

- Author: Jason
- 450 points

### Description

We found this packet capture and key. Recover the flag.

### Hints

1. Try using a tool like Wireshark.
2. How can you decrypt the TLS stream?

### Attachments

[capture.pcap](./resources/picoctf/picogym/attachments/forensics/webnet1/capture.pcap)

<details>

<summary markdown="span">picopico.key</summary>

~~~
-----BEGIN PRIVATE KEY-----
MIIEvQIBADANBgkqhkiG9w0BAQEFAASCBKcwggSjAgEAAoIBAQCwKlFPNKjseJF5
puCJU5x38XcT1eQge5zOKNahAlYudvGVOEs61TnIgvcER4ko8i3OCwak2/atcGk3
oz9jFKep7XFEYNP31IwwD9j/YazlKy4DRLGObOyIZUU1f2WRA7Uhf0POQXsDT1oU
X32jMKZkQSSDW4MRZd9trJYdO2TrcEPMsBiZQlFlvgnNwl3QlawozTHLAJKI36j1
cPwSMMeNca1e0Zi1s7R5IxfhpNXOBF0FmxiWvmeOHbaspyHg8UEmGBrkd4k4wXSK
GQvrc8QjycP4ScEdquxJiYnDT8iEbAq70/7f/5NIN1DE9YoGJqKYjTS9nRPB4Yvj
JN/SJnhvAgMBAAECggEACCnd3LrG/TZVH3sROqvqO1CwQPYPfUXdLVyNHab7EWon
pc+XBOHurJENG2CpRYF7h+nQ5ADhfIYSCicBf/jsEB7VueJ20CxEVtHVL3h6R6Bp
oHMle0Em8OcofuMpdL/kO+om3T8BkVSzCvCl5NMTUuAF7iRmfX7oDLALwM0IzzQv
2un+2UmT15rgAZfl3IL1PGvJhbhLxfeeyPE9MBy1SqBjQ9rNFn8sQv959J6BHz4b
EpK//ErtNP2yh7oiVBBgKEQ1gEuOjQC/4oxoqCFfZaf9XNRCxB/zY1nUprvJyz09
NMQWNF2EmvmBVGfoTxmuut5N0GbVr2UyHxWMKm2sOQKBgQDpb2+AWgWlGtetuLKJ
fJs8dnd6LhnafbKCOXMOT68qMBRoTpBtVTLRVSNvWCm8m4TTEazX4+ZA+bJFwUFw
aATDmHcr6lMI3tNKrcsnY2F7o5I4z6mwuRuSeszq/ndxZqCzwCu4nKixh3cznp7j
JiElNG0d8Lu5eQgmVAK1AhWXfQKBgQDBMa9ga7VJUP4pzcHnWAoi34OpfjvQYeGl
IKL3AKO4OedaHdH9qid41PQHnL7O3xzN669SkLZ5s0d88A/LFLk4oZNMKdkSTQIQ
+AMbXH01HGFvnCOuPg/FbNp1wS7zJEg5u5HFQWyMPNJLr/hZ6g2Yp+UGpAcGTwM/
RCPVAPhLWwKBgQDAB0OaOnPaVjKGXiHAqBirrGiswa/S5QQrzEaxxys5cUPYaoi0
6BldysPTnJr45JZna2rcTkXjvYTBjTDf3zHMFWgzYBfefC8kh8NPK5nNs8ldorbd
AemEnjBkP+DSELKyK6vLulOrdtzAQgRCp+MsT+xTbO2ArefeX826SXSpoQKBgC2v
nDOHBQXje1dTawlUToFUrgQE8AwlOYEdKKyUoCLOvqEW8DO2a0MtyM+MB6tQI7Wm
iH1T73L0LHGlK3bw3aRAwV5/fu/O+jAdFk8AHjPTFE+acu2fi4c6aKb0GjAxYksU
yjIFeK/pKinv4SESMkjpW0WowGiDgtcRPBAA/LaFAoGAfEM1rfM0v3UmB7PS6u0m
P3ckP2CFCdaryXPfC52GBcJ3Q46YpsQvLTVotM+teHvTjNw2jwwZxIl4NenGSEj3
KDhQoOiQC9BrDD+DB4I9+T9nxT3g7R6MrgITghB4We7TVhL/PljnJTyDqpjNA4kY
TveAJPv6Xq1ERt5PUtX3BqQ=
-----END PRIVATE KEY-----
~~~

</details>

### Solutions

<details>

<summary markdown="span">Solution 1</summary>

Solution here

</details>

### Answer

<details>

<summary markdown="span">Flag</summary>

~~~
picoCTF{}
~~~

</details>

---

### [Forensics](#contents) | [PicoGym](./picogym.md) | [PicoCTF](./picoctf.md) | [Home](./index.md)

---
## investigation-encoded-2

- Author: Santiago C
- 500 points

### Description

We have recovered a binary and 1 file: image01. See what you can make of it. NOTE: The flag is not in the normal picoCTF{XXX} format.

### Hints

1. Only use lower case letters and numbers

### Attachments

[mystery](./resources/picoctf/picogym/attachments/forensics/investigation_encoded_2/mystery)

[output](./resources/picoctf/picogym/attachments/forensics/investigation_encoded_2/output)

### Solutions

<details>

<summary markdown="span">Solution 1</summary>

Solution here

</details>

### Answer

<details>

<summary markdown="span">Flag</summary>

~~~
picoCTF{}
~~~

</details>

---

### [Forensics](#contents) | [PicoGym](./picogym.md) | [PicoCTF](./picoctf.md) | [Home](./index.md)

---
## B1g-Mac

- Author: Santiago C
- 500 points

### Description

Here's a zip file.

### Hints

None

### Attachments

[b1g_mac.zip](./resources/picoctf/picogym/attachments/forensics/b1g_mac/b1g_mac.zip)

### Solutions

<details>

<summary markdown="span">Solution 1</summary>

Solution here

</details>

### Answer

<details>

<summary markdown="span">Flag</summary>

~~~
picoCTF{}
~~~

</details>

---

### [Forensics](#contents) | [PicoGym](./picogym.md) | [PicoCTF](./picoctf.md) | [Home](./index.md)

---

## [djm89uk.github.io](https://djm89uk.github.io)
