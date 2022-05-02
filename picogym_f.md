# [PicoCTF](./picoctf.md) PicoGym Forensics [50/50]

"Forensics" challenges can include file format analysis, steganography, memory dump analysis, or network packet capture analysis.

## Contents

1. [Glory of the Garden (2019)](#glory-of-the-garden) ✓
2. [So Meta (2019)](#so-meta) ✓
3. [extensions (2019)](#extensions) ✓
4. [shark on wire 1 (2019)](#shark-on-wire-1) ✓
5. [What Lies Within (2019)](#what-lies-within) ✓
6. [c0rrupt (2019)](#c0rrupt) ✓
7. [WhitePages (2019)](#whitepages) ✓
8. [m00nwalk (2019)](#m00nwalk) ✓
9. [like1000 (2019)](#like1000) ✓
10. [shark on wire 2 (2019)](#shark-on-wire-2) ✓
11. [m00nwalk2 (2019)](#m00nwalk2) ✓
12. [Investigative Reversing 0 (2019)](#investigative-reversing-0) ✓
13. [WebNet0 (2019)](#webnet0) ✓
14. [Investigative Reversing 1 (2019)](#investigative-reversing-1) ✓
15. [Investigative Reversing 2 (2019)](#investigative-reversing-2) ✓
16. [Investigative Reversing 3 (2019)](#investigative-reversing-3) ✓
17. [Investigative Reversing 4 (2019)](#investigative-reversing-4) ✓
18. [investigation_encoded_1 (2019)](#investigation-encoded-1) ✓
19. [WebNet1 (2019)](#webnet1) ✓
20. [investigation_encoded_2 (2019)](#investigation-encoded-2) ✓
21. [B1g_Mac (2019)](#b1g-mac) ✓
22. [Pitter, Patter, Platters (2020)](#pitter-patter-platters) ✓
23. [Information (2021)](#information) ✓
24. [Matryoshka doll (2021)](#matryoshka-doll) ✓
25. [tunn3l v1s10n (2021)](#tunn3l-v1s10n) ✓
26. [Wireshark doo dooo do doo (2021)](#wireshark-doo-dooo-do-doo) ✓
27. [MacroHard WeakEdge (2021)](#macrohard-weakedge) ✓
28. [Trivial Flag Transfer Protocol (2021)](#trivial-flag-transfer-protocol) ✓
29. [Wireshark twoo twooo two twoo (2021)](#wireshark-twoo-twooo-two-twoo) ✓
30. [Disk, disk, sleuth! (2021)](#disk-disk-sleuth) ✓
31. [Milkslap (2021)](#milkslap) ✓
32. [Disk,disk, sleauth II (2021)](#disk-disk-sleuth-ii) ✓
33. [Surfing the Waves (2021)](#surfing-the-waves) ✓
34. [Very very very Hidden (2021)](#very-very-very-hidden) ✓
35. [Advanced-potion-making (2021)](#advanced-potion-making) ✓
36. [Scrambled-bytes (2021)](#scrambled-bytes) ✓
37. [WPA-ing Out](#wpa-ing-out) ✓
38. [Enhance! (2022)](#enhance) ✓
39. [File Types (2022)](#file-types) ✓
40. [Lookey Here (2022)](#lookey-here) ✓
41. [Packets Primer (2022)](#packets-primer) ✓
42. [Redaction Gone Wrong  (2022)](#redaction-gone-wrong) ✓
43. [Sleuthkit Intro (2022)](#sleuthkit-intro) ✓
44. [Sleuthkit Apprentice (2022)](#sleuthkit-apprentice) ✓
45. [Eavesdrop (2022)](#eavesdrop) ✓
46. [Operation Oni (2022)](#operation-oni) ✓
47. [St3g0 (2022)](#st3g0) ✓
48. [Operation Orchid (2022)](#operation-orchid) ✓
49. [Sidechannel (2022)](#sidechannel) ✓
50. [Torrent Analyze (2022)](#torrent-analyze) ✓

---

### [Forensics](#contents) | [PicoCTF](./picoctf.md) | [Home](./index.md)

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

![garden.jpg](./resources/picoctf/picogym/attachments/forensics/glory-of-the-garden/garden.jpg)

</details>

### Solutions

<details>

<summary markdown="span">Solution 1</summary>

This challenge can be solved with the in-built linux command strings and can be optimised using grep:

~~~shell
$ strings garden.jpg | grep pico
~~~

This searches the hex values for a string including the substring "pico".  The command returns:

~~~shell
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

### [Forensics](#contents) | [PicoCTF](./picoctf.md) | [Home](./index.md)

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

![pico_img.png](./resources/picoctf/picogym/attachments/forensics/so-meta/pico_img.png)

</details>

### Solutions

<details>

<summary markdown="span">Solution 1</summary>

This challenge suggests we review the meta data for the image.  A useful tool for extracting meta data from photographs is [Exiftool](https://exiftool.org/).  We can combine this with grep to deliver a concise solution:

~~~shell
$ exiftool pico_img.png | grep pico
~~~

This returns:

~~~shell
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

### [Forensics](#contents) | [PicoCTF](./picoctf.md) | [Home](./index.md)

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

~~~shell
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

~~~shell
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

### [Forensics](#contents) | [PicoCTF](./picoctf.md) | [Home](./index.md)

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

~~~shell
$ tcpdump -r capture.pcap -A | grep pico 
~~~

This returns:

~~~shell
reading from file capture.pcap, link-type EN10MB (Ethernet), snapshot length 262144
.....'....Upico..............
.....'....Upico..............
.....'....Upico..............
.....'....Upico..............
~~~

The flag is likely fragmented across multiple packets in the capture and therefore cannot be read directly.  Wireshark provides a tool to review data streams (IP conversations) in which the flag will likely be found, however we need to locate which conversation contains the flag which cannot be achieved in Wireshark, we can simplify this by filtering the pcap until we have a more manageable capture.

To reduce the size of the file, we can extract IP only captures, removing all ARP and ICMP packets:

~~~shell
$ tcpdump -r capture.pcap -w capture_ip.pcap ip
~~~

This reduces capture.pcap from 2,317 packets to 1,230 IP packets.

This can be reduced further using editcap to remove packet replicas from the capture file:

~~~shell
$ editcap --novlan -d capture_ip.pcap capture_ip_no_replicas.pcap 
~~~

This reduces the packet capture from 1,230 to 561.

Finally, we can filter for just UDP and TCP:

~~~shell
$ tcpdump -r capture_ip_no_replicas.pcap -w capture_final.pcap tcp or udp
~~~

This gives us a capture file, capture_final.pcap with only 493 captured packets of interest.

We can now interrogate the conversations using the wireshark command line utility, tshark:

~~~shell
$ tshark -r capture_final.pcap -z "follow,udp,ascii,1"
~~~

This isolates the udp conversation with index 1 and displays the contents in ascii format to the terminal.  As we work our way up through the various conversations, we can see the flag is identifiable in UDP stream 5:

~~~shell
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

### [Forensics](#contents) | [PicoCTF](./picoctf.md) | [Home](./index.md)

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

![buildings.png](./resources/picoctf/picogym/attachments/forensics/what-lies-within/buildings.png)

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

### [Forensics](#contents) | [PicoCTF](./picoctf.md) | [Home](./index.md)

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

In this challenge, we have a binary file without an extension.  Inspecting the binary data, we do not find the string:

~~~shell
$ strings mystery | grep pico  
~~~

This does not return anything.  The flag is likely encoded in the file.  Two simple strings commands can provide an inidication of the file type:

~~~shell
$ strings mystery | grep RGB                                           1 ⨯
sRGB
$ strings mystery | grep gAMA                                          1 ⨯
gAMA
~~~

This shows that it is likely an image file.  We can open the file in a hex editor to attempt to identify the file type.

The last 8 Bytes of the file are:

~~~
IEND\UffffffffB`
~~~

A quick google of "IEND" suggests this may be a PNG file, we can find the ONG specification at [w3.org](https://www.w3.org/TR/PNG-Structure.html).  We will be editing the file Bytes directly, so we will create a copy to work on in the hex editor:

~~~shell
$ cp mystery mystery01.png
~~~

We can attempt to open this file but get an error.  We still have further steps to take.

The PNG specification states "The first eight bytes of a PNG file always contain the following (decimal) values:"

~~~
137 80 78 71 13 10 26 10
~~~

In hex, these are:

~~~
89  50  4e  47  0d  0a  1a  0a
~~~

in ASCII:

~~~
.PNG....
~~~

our file, mystery01.png has the following 8-Byte header:

~~~
89 65 4E 34 0D 0A B0 AA
~~~

in ASCII:

~~~
.eN4....
~~~

We will change these to match the PNG standard and save the file.  With this corrected, the file will still not open. [w3.org](https://www.w3.org/TR/PNG-Chunks.html) provides details of the PNG chunks that should be present.  The first chunk must be the IHDR detail providing dimensions, palette , compression and interlacing details of the file.  Opening another png file, we see the header looks like:

~~~
89  50  4e  47  0d  0a  1a  0a 00 00 00 0d 49 48 44 00 00 02 93 00 00 02 81 08 02 00 00 00
~~~

in ASCII:

~~~
.PNG........IHDR.............
~~~

mystery01.png has the following header:

~~~
89  50  4e  47  0d  0a  1a  0a 00 00 00 0d 43 22 44 52 00 06 6A 00 00 04 47 08 02 00 00 00
~~~

in ASCII:

~~~
.PNG........C"DR.............
~~~

Since we do not know the dimensions, palette, compression or interlacing information for our file, we will only ammend the IHDR bytes. Our header now appears:

~~~
89  50  4e  47  0d  0a  1a  0a 00 00 00 0d 43 22 44 52 00 06 6A 00 00 04 47 08 02 00 00 00
~~~

in ASCII:

~~~
.PNG........IHDR.............
~~~

We still cannot open the file.  We need to make some more changes.  We can use a tool, [pngcheck](http://www.libpng.org/pub/png/apps/pngcheck.html) to identify issues with the file contents:

~~~shell
$ pngcheck mystery01.png                                             127 ⨯
mystery01.png  CRC error in chunk pHYs (computed 38d82c82, expected 495224f0)
ERROR: mystery01.png
~~~

This highlights a CRC error in the "pHYs" chunk.  pHYs is a chunk in png files detailing the pixel relative dimension size.  Details of the pHYs chunk can be found at [libpng.org](http://www.libpng.org/pub/png/book/chapter11.html#png.ch11.div.8).

The pHYs chunk in our file is:

~~~
09 70 48 59 73 aa 00 16 25 00 00 16 25 01
~~~

or in ASCII:

~~~
.pHYs.........
~~~

The pHYs block definition from [libpng.org](http://www.libpng.org/pub/png/book/chapter11.html#png.ch11.div.8) shows the chunk fields:

| Field                   | Length  | Minimum Value | Maximum Value | mystery01.png |
|-------------------------|---------|---------------|---------------|---------------|
| pixels per unit, x axis | 4 Bytes | 0             | 2,147,483,647 | 2,852,132,389 |
| pixels per unit, y axis | 4 Bytes | 0             | 2,147,483,647 | 5,669         |
| Unit specifier          | 1 Byte  | 0             | 1             | 1             |

As can be seen, the first field, pixels per unit x-axis, is outside of the valid range for the png standard.  Inspecting the Byte data, we can see the pixels per field in the x-axis is:

~~~
AA 00 16 25
~~~

Whereas the y-axis field is:

~~~
00 00 16 25
~~~

We can assume the first Byte is corrupted and should be 00, effectively both x and y resolution are identical, as could be expected in a normal picture.  Once ammended, the block becomes:

~~~
09 70 48 59 73 00 00 16 25 00 00 16 25 01
~~~

We still cannot open the png file, however running the pngcheck there is no longer a CRC error with the pHYs chunk:

~~~shell
$ pngcheck mystery01.png                                               2 ⨯
mystery01.png  invalid chunk length (too large)
ERROR: mystery01.png
~~~

This shows an invalid chunk length.  Inspecting the hex editor, we can see the next chunk:

~~~
AA AA FF A5 AB 44 45 54
~~~

in ASCII:

~~~
.....DET
~~~

No chunk is provided for DET in the png standard.  This is likely another corrupted section of the file.  The closest chunk is the IDAT (image data) chunk.  We can ammend this in the file:

~~~
AA AA FF A5 49 44 41 54
~~~

in ASCII:

~~~
....IDAT
~~~

The Bytes preceding the IDAT string define the chunk size.  In this case, the chunk size is defined as 0xaaaaffa5, or 2,863,333,285 Bytes.  This is larger than the file itself, and is therefore incorrect.  The correct size can be determined by locating the next chunk.  In GHex we can search for the IDAT string and see the next IDAT chunk starts at 0x10004. The chunk data we are fixing starts at 0x5B and ends at 0x10000 (4 Byte trailer), the chunk size is therefore: 0x10000 - 0x5B =  65536 - 91 = 65445 = 0xFFA5.

We can now change the IDAT header to match the block size:

~~~
00 00 FF A5 49 44 41 54
~~~

We can now open the image file:

<details>

<summary markdown="span">mystery.png</summary>

![mystery01.png](./resources/picoctf/picogym/solutions/forensics/c0rrupt/mystery01.png)

</details>

The flag can be read from the image: picoCTF{c0rrupt10n_1847995}.

</details>

### Answer

<details>

<summary markdown="span">Flag</summary>

~~~
picoCTF{c0rrupt10n_1847995}
~~~

</details>

---

### [Forensics](#contents) | [PicoCTF](./picoctf.md) | [Home](./index.md)

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

On inspection, this file is constructed from two characters, spaces and tabs.  A simple substitution throughout the file can generate the following binary string:

~~~
00001010000010010000100101110000011010010110001101101111010000110101010001000110000010100000101000001001000010010101001101000101010001010010000001010000010101010100001001001100010010010100001100100000010100100100010101000011010011110101001001000100010100110010000000100110001000000100001001000001010000110100101101000111010100100100111101010101010011100100010000100000010100100100010101010000010011110101001001010100000010100000100100001001001101010011000000110000001100000010000001000110011011110111001001100010011001010111001100100000010000010111011001100101001011000010000001010000011010010111010001110100011100110110001001110101011100100110011101101000001011000010000001010000010000010010000000110001001101010011001000110001001100110000101000001001000010010111000001101001011000110110111101000011010101000100011001111011011011100110111101110100010111110110000101101100011011000101111101110011011100000110000101100011011001010111001101011111011000010111001001100101010111110110001101110010011001010110000101110100011001010110010001011111011001010111000101110101011000010110110001011111001101110011000100110000001100000011100000110110001100000110001000110000011001100110000100110111001101110011100101100001001101010110001001100100001110000110001101100101001100100011100101100110001100100011010001100110001101010011100000110110011001000110001101111101000010100000100100001001
~~~

Using the binary to ascii online [translator](https://www.rapidtables.com/convert/number/binary-to-ascii.html), we can recover the ASCII text:

~~~

		picoCTF

		SEE PUBLIC RECORDS & BACKGROUND REPORT
		5000 Forbes Ave, Pittsburgh, PA 15213
		picoCTF{not_all_spaces_are_created_equal_7100860b0fa779a5bd8ce29f24f586dc}
		
~~~


</details>

The flag is therefore picoCTF{not_all_spaces_are_created_equal_7100860b0fa779a5bd8ce29f24f586dc}.

### Answer

<details>

<summary markdown="span">Flag</summary>

~~~
picoCTF{not_all_spaces_are_created_equal_7100860b0fa779a5bd8ce29f24f586dc}
~~~

</details>

---

### [Forensics](#contents) | [PicoCTF](./picoctf.md) | [Home](./index.md)

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

This challenge provides a wav audio file from which we are required to retrieve the flag.  The hints suggest that we should look at the NASA moon missions to understand how pictures were transmitted back to earth.  A quick web search leads us to [Slow-Scan Television](https://en.wikipedia.org/wiki/Slow-scan_television#Early_usage_in_space_exploration).  SSTV uses voice frequencies to transmit pictures.

Another web search leads us to an [amateur radio website](https://www.amateur-radio-wiki.net/sstv-software/) that suggests [qsstv](http://users.telenet.be/on4qz/qsstv/index.html) can be used to decode SSTV broadcasts:

~~~shell
$ sudo apt install qsstv
~~~

Loading QSSTV, we ensure the program is receiving from our active audio interface.  In QSSTV we can set Auto Slant on and set the mode to Auto.

Playing the wav file will show a waterfall of the audio and decode the SSTV image using Scottie 1:

<details>

<summary markdown="span">flag.png</summary>

![flag.png](./resources/picoctf/picogym/solutions/forensics/m00nwalk/flag.png)

</details>

This gives us the flag: picoCTF{beep_boop_im_in_space}.

</details>

### Answer

<details>

<summary markdown="span">Flag</summary>

~~~
picoCTF{beep_boop_im_in_space}
~~~

</details>

---

### [Forensics](#contents) | [PicoCTF](./picoctf.md) | [Home](./index.md)

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

This challenge has the flag held in a compressed folder that has been tar-compressed 1000 times.  To solve this, we can write a simple bash command:

~~~bash
#!/bin/bash 

echo "picoCTF like1000 solution."

FILE="1000.tar"
i="1000"
while (($i > 0));
do

tar -xvf $FILE
rm $FILE
i=$[$i-1]
FILE="${i}.tar"

done
~~~

We must enable this bash file to be executed:

~~~shell
$ chmod +x untar.sh
~~~

We can execute the above bash script.  Once complete, we will have a png flag file:

<details>

<summary markdown="span">mystery.png</summary>

![flag.png](./resources/picoctf/picogym/solutions/forensics/like1000/flag.png)

</details>

This gives us the flag picoCTF{l0t5_0f_TAR5}.

</details>

### Answer

<details>

<summary markdown="span">Flag</summary>

~~~
picoCTF{l0t5_0f_TAR5}
~~~

</details>

---

### [Forensics](#contents) | [PicoCTF](./picoctf.md) | [Home](./index.md)

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

This challenge provides a packet capture file, similar to the previous shark on the wire challenge.

The capture file has 1326 packets.  We can again reduce the capture file size using the following commands:

~~~shell
$ tcpdump -r capture.pcap -w capture_ip.pcap
$ editcap --novlan -d capture_ip.pcap capture_ip_no_replicas.pcap
$ tcpdump -r capture_ip_no_replicas.pcap -w capture_final.pcap tcp or udp
~~~

This has reduced the total capture size to 101 packets. Looking through the files, we do not see any useful contents:

~~~shell
$ tshark -r capture_final.pcap -z "follow,udp,ascii,1"
~~~

There are a lot of red herrings in the streams ("picoCTF{N0t_a_fLag}" in udp stream 6, "picoCTF{StaT315e" in udp stream 7, "picoCTF Sure is fun!" in udp stream 9, "I really want to find some picoCTF flags" in udp stream 10).  Reviewing the packet contents is not getting us anywhere.

We can try to export objects from the packet capture using tshark, for example to export imf objects we use:

~~~shell
$ tshark -r capture_final.pcap --export-objects imf,temp_folder
~~~

No objects are exported.  This challenge must use a more interesting method to hide the flag.

We can look at a summary of the capture using the command:

~~~shell
$ tshark -r capture_final.pcap
~~~

This shows a lot of information, not much use except there seems to be some strange ports in use.  We can review the tcp ports by filtering tshark and piping to sort and uniq:

~~~shell
$ tshark -r capture_final.pcap -Y "tcp" -T fields -e tcp.srcport -e tcp.dstport | sort | uniq
60218   80
80      60218
~~~

This shows ports 60218 and 80 are used for tcp conversations.  We can do the same for udp:

~~~shell
$ tshark -r capture_final.pcap -Y "udp" -T fields -e udp.srcport -e udp.dstport | sort | uniq
1234    123
1234    1234
49852   1900
5000    22
5000    8888
5000    8990
5000    9999
5048    22
5049    22
5051    22
5067    22
5070    22
5076    22
5084    22
50845   1900
5095    22
5097    100
5097    22
5097    80
5099    22
5100    22
5102    22
5103    22
5105    22
5111    22
5112    22
5114    22
5115    22
5116    22
5118    22
5123    22
5125    22
51736   1900
52219   1900
52274   5355
52318   1900
52759   1900
5353    5353
54450   1900
56287   1900
56624   1900
58515   1900
~~~

There are some interesting source port numbers in use with the conversation to port 22.  We can filter these:

~~~shell
$ tshark -r capture_final.pcap -Y "udp" -T fields -e udp.srcport -Y udp.dstport==22
5000
5112
5105
5099
5111
5067
5084
5070
5123
5112
5049
5076
5102
5051
5114
5051
5100
5095
5100
5097
5116
5097
5095
5118
5049
5097
5095
5115
5116
5051
5103
5048
5125
5000
~~~

It appears each source port uses a slightly different 5000 port number.  We can do some piping and basic maths to see if the decimal integers can represent ascii characters for the flag:

~~~shell
$ tshark -r capture_final.pcap -Y "udp" -T fields -e udp.srcport -Y udp.dstport==22 | awk '{print sprintf("%c",$1-5000)}' | tr -d '\n'
picoCTF{p1Lf3r3d_data_v1a_st3g0}
~~~

This gives us the flag picoCTF{p1Lf3r3d_data_v1a_st3g0}, which is again an incorrect flag due to packet loss in the file reduction.  reusing the above command on the original capture file:

~~~shell
$ tshark -r capture.pcap -Y "udp" -T fields -e udp.srcport -Y udp.dstport==22 | awk '{print sprintf("%c",$1-5000)}' | tr -d '\n'
picoCTF{p1LLf3r3d_data_v1a_st3g0}
~~~

Gives us the flag picoCTF{p1LLf3r3d_data_v1a_st3g0}.

</details>

### Answer

<details>

<summary markdown="span">Flag</summary>

~~~
picoCTF{p1LLf3r3d_data_v1a_st3g0}
~~~

</details>

---

### [Forensics](#contents) | [PicoCTF](./picoctf.md) | [Home](./index.md)

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

As in m00nwalk, we play these wav files and decode them using QSSTV.

message.wav provides the same image as before, decoded using [Scottie 1](https://radio.clubs.etsit.upm.es/blog/2019-08-10-sstv-scottie1-encoder/):

<details>

<summary markdown="span">message.png</summary>

![message.png](./resources/picoctf/picogym/solutions/forensics/m00nwalk2/message.png)

</details>

clue1.wav provides a new image with the words "Password hidden_stegosaurus" using [Martin 1](https://www.sstv-handbook.com/download/sstv_04.pdf):

<details>

<summary markdown="span">clue1.png</summary>

![clue1.png](./resources/picoctf/picogym/solutions/forensics/m00nwalk2/clue1.png)

</details>

clue2.wav provides a new image with the words "The quieter you are the more you can HEAR" using [Scottie 2](https://www.sstv-handbook.com/download/sstv_04.pdf):

<details>

<summary markdown="span">clue2.png</summary>

![clue2.png](./resources/picoctf/picogym/solutions/forensics/m00nwalk2/clue2.png)

</details>

clue3.wav provides a new image with the words "Alan Eliasen the Future Boy" using [Martin 2](https://www.sstv-handbook.com/download/sstv_04.pdf):

<details>

<summary markdown="span">clue3.png</summary>

![clue3.png](./resources/picoctf/picogym/solutions/forensics/m00nwalk2/clue3.png)

</details>

A quick web search for Alan Eliasen leads us to a steganography tools website at [futureboy.us](https://futureboy.us/stegano/).  We can submit the message.wav file to this site and enter a password: hidden_stegosaurus to decode a hidden message in the file, picoCTF{the_answer_lies_hidden_in_plain_sight}.

</details>

### Answer

<details>

<summary markdown="span">Flag</summary>

~~~
picoCTF{the_answer_lies_hidden_in_plain_sight}
~~~

</details>

---

### [Forensics](#contents) | [PicoCTF](./picoctf.md) | [Home](./index.md)

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

![mystery.png](./resources/picoctf/picogym/attachments/forensics/investigative-reversing-0/mystery.png)

</details>

### Solutions

<details>

<summary markdown="span">Solution 1</summary>

We can open the mystery binary and deocmpile it in Ghidra.  We find the main function:

~~~c
void main(void)

{
  FILE * __stream;
  FILE * __stream_00;
  size_t sVar1;
  long in_FS_OFFSET;
  int local_54;
  int local_50;
  char local_38[4];
  char local_34;
  char local_33;
  char local_29;
  long local_10;

  local_10 = * (long * )(in_FS_OFFSET + 0x28);
  __stream = fopen("flag.txt", "r");
  __stream_00 = fopen("mystery.png", "a");
  if (__stream == (FILE * ) 0x0) {
    puts("No flag found, please make sure this is run on the server");
  }
  if (__stream_00 == (FILE * ) 0x0) {
    puts("mystery.png is missing, please run this on the server");
  }
  sVar1 = fread(local_38, 0x1a, 1, __stream);
  if ((int) sVar1 < 1) {
    /* WARNING: Subroutine does not return */
    exit(0);
  }
  puts("at insert");
  fputc((int) local_38[0], __stream_00);
  fputc((int) local_38[1], __stream_00);
  fputc((int) local_38[2], __stream_00);
  fputc((int) local_38[3], __stream_00);
  fputc((int) local_34, __stream_00);
  fputc((int) local_33, __stream_00);
  local_54 = 6;
  while (local_54 < 0xf) {
    fputc((int)(char)(local_38[local_54] + '\x05'), __stream_00);
    local_54 = local_54 + 1;
  }
  fputc((int)(char)(local_29 + -3), __stream_00);
  local_50 = 0x10;
  while (local_50 < 0x1a) {
    fputc((int) local_38[local_50], __stream_00);
    local_50 = local_50 + 1;
  }
  fclose(__stream_00);
  fclose(__stream);
  if (local_10 != * (long * )(in_FS_OFFSET + 0x28)) {
    /* WARNING: Subroutine does not return */
    __stack_chk_fail();
  }
  return;
}
~~~

We can see a flag.txt file is read and the bytes are manipulated and appended to the png file.  Opening the png file in a hex editor, we see the last 26 bytes are:

~~~
picoCTK\x80k5zsid6q_3d659f57}
~~~

after the first 6 characters are appended to the file, the next 9 characters are read from the flag.txt file, 5 is added to the Byte value, and they are appended to the png file. Character 15 is appended from another non-flag variable subtracted by 3, and 16-26 are appended without manipulation from the flag.txt file.

| Index | Value | Manipulation | flag.txt |
|-------|-------|--------------|----------|
|  0    | p     | +0           | p        |
|  1    | i     | +0           | i        |
|  2    | c     | +0           | c        |
|  3    | o     | +0           | o        |
|  4    | C     | +0           | C        |
|  5    | T     | +0           | T        |
|  6    | K     | +5           | F        |
|  7    | \x80  | +5           | {        |
|  8    | k     | +5           | f        |
|  9    | 5     | +5           | 0        |
| 10    | z     | +5           | u        |
| 11    | s     | +5           | n        |
| 12    | i     | +5           | d        |
| 13    | d     | +5           | _        |
| 14    | 6     | +5           | 1        |
| 15    | q     | -3           | t        |
| 16    | _     | +0           | _        |
| 17    | 3     | +0           | 3        |
| 18    | d     | +0           | d        |
| 19    | 6     | +0           | 6        |
| 20    | 5     | +0           | 5        |
| 21    | 9     | +0           | 9        |
| 22    | f     | +0           | f        |
| 23    | 5     | +0           | 5        |
| 24    | 7     | +0           | 7        |
| 25    | }     | +0           | }        |

This gives us our flag:

picoCTF{f0und_1t_3d659f57}

</details>

### Answer

<details>

<summary markdown="span">Flag</summary>

~~~
picoCTF{f0und_1t_3d659f57}
~~~

</details>

---

### [Forensics](#contents) | [PicoCTF](./picoctf.md) | [Home](./index.md)

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

This challenge can be solved very simply using the [ssldump](http://ssldump.sourceforge.net/) tool.  Using ssldump, we can import the capture file, import a key and decrypt application data for SSL and TLS conversations.  We use flags: "-r" to point to the packet capture file, "-k" to point to the keyfile, "-A" to print all record fields, "-e" to print the absolite timestamps and "-d" to display the application data traffic.  We can use an extended grep command to search for the flag:

~~~shell
$ ssldump -Aed -nr ./capture.pcap -k ./picopico.key | grep -A2 pico
    61 67 3a 20 70 69 63 6f 43 54 46 7b 6e 6f 6e 67    ag: picoCTF{nong
    73 68 69 6d 2e 73 68 72 69 6d 70 2e 63 72 61 63    shim.shrimp.crac
    6b 65 72 73 7d 0d 0a 43 6f 6e 74 65 6e 74 2d 4c    kers}..Content-L
--
    67 3a 20 70 69 63 6f 43 54 46 7b 6e 6f 6e 67 73    g: picoCTF{nongs
    68 69 6d 2e 73 68 72 69 6d 70 2e 63 72 61 63 6b    him.shrimp.crack
    65 72 73 7d 0d 0a 43 6f 6e 74 65 6e 74 2d 4c 65    ers}..Content-Le
~~~

This gives us the flag picoCTF{nongshim.shrimp.crackers}.

</details>

### Answer

<details>

<summary markdown="span">Flag</summary>

~~~
picoCTF{nongshim.shrimp.crackers}
~~~

</details>

---

### [Forensics](#contents) | [PicoCTF](./picoctf.md) | [Home](./index.md)

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

![mystery.png](./resources/picoctf/picogym/attachments/forensics/investigative-reversing-1/mystery.png)

</details>

<details>

<summary markdown="span">mystery2.png</summary>

![mystery.png](./resources/picoctf/picogym/attachments/forensics/investigative-reversing-1/mystery2.png)

</details>

<details>

<summary markdown="span">mystery3.png</summary>

![mystery.png](./resources/picoctf/picogym/attachments/forensics/investigative-reversing-1/mystery3.png)

</details>

### Solutions

<details>

<summary markdown="span">Solution 1</summary>

We can again open the mystery binary in Ghidra and recompile it.  We find the main function:

~~~c
void main(void)

{
  FILE * __stream;
  FILE * __stream_00;
  FILE * __stream_01;
  FILE * __stream_02;
  long in_FS_OFFSET;
  char local_6b;
  int local_68;
  int local_64;
  int local_60;
  char local_38[4];
  char local_34;
  char local_33;
  long local_10;

  local_10 = * (long * )(in_FS_OFFSET + 0x28);
  __stream = fopen("flag.txt", "r");
  __stream_00 = fopen("mystery.png", "a");
  __stream_01 = fopen("mystery2.png", "a");
  __stream_02 = fopen("mystery3.png", "a");
  if (__stream == (FILE * ) 0x0) {
    puts("No flag found, please make sure this is run on the server");
  }
  if (__stream_00 == (FILE * ) 0x0) {
    puts("mystery.png is missing, please run this on the server");
  }
  fread(local_38, 0x1a, 1, __stream);
  fputc((int) local_38[1], __stream_02);
  fputc((int)(char)(local_38[0] + '\x15'), __stream_01);
  fputc((int) local_38[2], __stream_02);
  local_6b = local_38[3];
  fputc((int) local_33, __stream_02);
  fputc((int) local_34, __stream_00);
  local_68 = 6;
  while (local_68 < 10) {
    local_6b = local_6b + '\x01';
    fputc((int) local_38[local_68], __stream_00);
    local_68 = local_68 + 1;
  }
  fputc((int) local_6b, __stream_01);
  local_64 = 10;
  while (local_64 < 0xf) {
    fputc((int) local_38[local_64], __stream_02);
    local_64 = local_64 + 1;
  }
  local_60 = 0xf;
  while (local_60 < 0x1a) {
    fputc((int) local_38[local_60], __stream_00);
    local_60 = local_60 + 1;
  }
  fclose(__stream_00);
  fclose(__stream);
  if (local_10 != * (long * )(in_FS_OFFSET + 0x28)) {
    /* WARNING: Subroutine does not return */
    __stack_chk_fail();
  }
  return;
}
~~~

This a similar program to before, we have a file reading flag.txt and appending the data to 3 separate png files.

We  identifying where each value will be stored, how it was manipulated and what the original format was:

| Flag Index | Mainpulation | Location  | PNG value | Original |
|------------|--------------|-----------|-----------|----------|
|  0         | +0x15 = +21  | png 1:+1  | \x85      | p        |
|  1         | +0           | png 2:+1  | i         | i        |
|  2         | +0           | png 2:+2  | c         | c        |
|  3         | +4           | png 1:+2  | s         | o        |
|  4         | +0           | png 0:+1  | C         | C        |
|  5         | +0           | png 2:+3  | T         | T        |
|  6         | +0           | png 0:+2  | F         | F        |
|  7         | +0           | png 0:+3  | {         | {        |
|  8         | +0           | png 0:+4  | A         | A        |
|  9         | +0           | png 0:+5  | n         | n        |
| 10         | +0           | png 2:+4  | 0         | 0        |
| 11         | +0           | png 2:+5  | t         | t        |
| 12         | +0           | png 2:+6  | h         | h        |
| 13         | +0           | png 2:+7  | a         | a        |
| 14         | +0           | png 2:+8  | _         | _        |
| 15         | +0           | png 0:+6  | 1         | 1        |
| 16         | +0           | png 0:+7  | _         | _        |
| 17         | +0           | png 0:+8  | e         | e        |
| 18         | +0           | png 0:+9  | 2         | 2        |
| 19         | +0           | png 0:+10 | 6         | 6        |
| 20         | +0           | png 0:+11 | 3         | 3        |
| 21         | +0           | png 0:+12 | 0         | 0        |
| 22         | +0           | png 0:+13 | 7         | 7        |
| 23         | +0           | png 0:+14 | 2         | 2        |
| 24         | +0           | png 0:+15 | 5         | 5        |
| 25         | +0           | png 0:+16 | }         | }        |

This gives us the flag:

picoCTF{An0tha_1_e2630725}

</details>

### Answer

<details>

<summary markdown="span">Flag</summary>

~~~
picoCTF{An0tha_1_e2630725}
~~~

</details>

---

### [Forensics](#contents) | [PicoCTF](./picoctf.md) | [Home](./index.md)

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

We can again import and decompile the mystery binary in Ghidra.  The main function is shown below.

~~~c
undefined8 main(void)

{
  size_t sVar1;
  long in_FS_OFFSET;
  byte local_7e;
  byte local_7d;
  int local_7c;
  int local_78;
  int local_74;
  int local_70;
  undefined4 local_6c;
  int local_68;
  int local_64;
  FILE * local_60;
  FILE * local_58;
  FILE * local_50;
  char local_48[56];
  long local_10;

  local_10 = * (long * )(in_FS_OFFSET + 0x28);
  local_6c = 0;
  local_60 = fopen("flag.txt", "r");
  local_58 = fopen("original.bmp", "r");
  local_50 = fopen("encoded.bmp", "a");
  if (local_60 == (FILE * ) 0x0) {
    puts("No flag found, please make sure this is run on the server");
  }
  if (local_58 == (FILE * ) 0x0) {
    puts("original.bmp is missing, please run this on the server");
  }
  sVar1 = fread( & local_7e, 1, 1, local_58);
  local_7c = (int) sVar1;
  local_68 = 2000;
  local_78 = 0;
  while (local_78 < local_68) {
    fputc((int)(char) local_7e, local_50);
    sVar1 = fread( & local_7e, 1, 1, local_58);
    local_7c = (int) sVar1;
    local_78 = local_78 + 1;
  }
  sVar1 = fread(local_48, 0x32, 1, local_60);
  local_64 = (int) sVar1;
  if (local_64 < 1) {
    puts("flag is not 50 chars");
    /* WARNING: Subroutine does not return */
    exit(0);
  }
  local_74 = 0;
  while (local_74 < 0x32) {
    local_70 = 0;
    while (local_70 < 8) {
      local_7d = codedChar(local_70, local_48[local_74] - 5, local_7e);
      fputc((int)(char) local_7d, local_50);
      fread( & local_7e, 1, 1, local_58);
      local_70 = local_70 + 1;
    }
    local_74 = local_74 + 1;
  }
  while (local_7c == 1) {
    fputc((int)(char) local_7e, local_50);
    sVar1 = fread( & local_7e, 1, 1, local_58);
    local_7c = (int) sVar1;
  }
  fclose(local_50);
  fclose(local_58);
  fclose(local_60);
  if (local_10 == * (long * )(in_FS_OFFSET + 0x28)) {
    return 0;
  }
  /* WARNING: Subroutine does not return */
  __stack_chk_fail();
}
~~~

This is a bit more complicated than the previous 2 investigative reversing challenges. Lets clean things up, remove error checking, stack protection and rename variables:

~~~c
int main(void)

{
  size_t sVar1;
  byte bmp_buffer;
  byte otp_buffer;
  FILE * file_flag;
  FILE * file_original_bmp;
  FILE * file_encoded_bmp;
  char flag_buffer[56];

  file_flag = fopen("flag.txt", "r");
  file_original_bmp = fopen("original.bmp", "r");
  file_encoded_bmp = fopen("encoded.bmp", "a");

  sVar1 = fread( & bmp_buffer, 1, 1, file_original_bmp);
  for(int i=0; i<2000; i++){
    fputc((int)(char) bmp_buffer, file_encoded_bmp);
    sVar1 = fread( &bmp_buffer, 1, 1, file_original_bmp);
  }
  sVar1 = fread(flag_buffer, 0x32, 1, file_flag);

  for(int i=0;i<50;i++){
    for(int j=0; j<8; j++){
      otp_buffer = codedChar(j, flag_buffer[i] - 5, bmp_buffer);
      fputc((int)(char) otp_buffer, file_encoded_bmp);
      fread( & bmp_buffer, 1, 1, file_original_bmp);
    }
  }
  while ((int) sVar1 == 1) {
    fputc((int)(char) bmp_buffer, file_encoded_bmp);
    sVar1 = fread( &bmp_buffer, 1, 1, file_original_bmp);
  }
  fclose(file_encoded_bmp);
  fclose(file_original_bmp);
  fclose(file_flag);
  
  return 0;
}
~~~

We can see that 3 files are opened by the program, flag.txt is opened in read-only mode, original.bmp is opened in read-only mode and encoded.bmp is opened in appending mode.  

The first 2000 Bytes of the original bmp are copied directly into the encoded.bmp file.

The flag.txt is read into a 56-Byte character array. This is appended to the encoded.bmp file with each character encoded using the codedChar subroutine that will append an encoded char generated from the original bmp and the flag contents.  This will fill the next 400 Bytes of the encoded bmp.

The remainder of the original bmp is copied to the encoded bmp file in the final while loop.  We are therefore only interested in the encoded.bmp Bytes 2000-2400.

We can separate these Bytes using dd:

~~~shell
$ dd skip=2000 count=400 if=encoded.bmp of=output.binary bs=1
400+0 records in
400+0 records out
400 bytes copied, 0.00173631 s, 230 kB/s
~~~

We should take a look at the codedChar subroutine in Ghidra:

~~~c
byte codedChar(int param_1, byte param_2, byte param_3)
{
  byte local_20;
  local_20 = param_2;
  if (param_1 != 0) {
    local_20 = (byte)((int)(char) param_2 >> ((byte) param_1 & 0x1f));
  }
  return param_3 & 0xfe | local_20 & 1;
}
~~~

we can tidy this up:


~~~c
byte codedChar(int j, byte flag_buff_edit, byte bmp_buff)
{
  byte flag_code_buff;
  flag_code_buff = flag_buff_edit;
  if (j != 0) {
    flag_code_buff = (byte)((int)(char) flag_buff_edit >> ((byte) j & 0x1f));
  }
  return bmp_buff & 0xfe | flag_code_buff & 1;
}
~~~

We can reverse this function in python:

~~~py
bin_str = ['']*50
int_str = [0]*50
flag = ''

file = open("output.binary","rb")
byte = file.read(1)

i = 0
for i in range(0,50):
    for j in range(0,8):
        bin_val = ord(byte)&0x1
        bin_str[i] = str(bin_val) +bin_str[i]
        byte = file.read(1)

for i in range(0,50,1):
    int_str[i] = int(bin_str[i],2)+5
    newchar = chr(int_str[i])
    flag += newchar

print(flag)
~~~


Running, we get the output:

~~~shell
In [1]: runfile('InvestigativeReversing2.py')
picoCTF{n3xt_0n300000000000000000000000000394060c}
~~~

This is our flag.

</details>

### Answer

<details>

<summary markdown="span">Flag</summary>

~~~
picoCTF{n3xt_0n300000000000000000000000000394060c}
~~~

</details>

---

### [Forensics](#contents) | [PicoCTF](./picoctf.md) | [Home](./index.md)

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

This challenge is very similar to the previous Investigative Reversing challenge.  We can import and decompile in Ghidra, giving us the main function:

~~~c
undefined8 main(void)

{
  size_t sVar1;
  long in_FS_OFFSET;
  byte local_7e;
  byte local_7d;
  int local_7c;
  int local_78;
  uint local_74;
  int local_70;
  undefined4 local_6c;
  int local_68;
  int local_64;
  FILE * local_60;
  FILE * local_58;
  FILE * local_50;
  byte local_48[56];
  long local_10;

  local_10 = * (long * )(in_FS_OFFSET + 0x28);
  local_6c = 0;
  local_60 = fopen("flag.txt", "r");
  local_58 = fopen("original.bmp", "r");
  local_50 = fopen("encoded.bmp", "a");
  if (local_60 == (FILE * ) 0x0) {
    puts("No flag found, please make sure this is run on the server");
  }
  if (local_58 == (FILE * ) 0x0) {
    puts("No output found, please run this on the server");
  }
  sVar1 = fread( & local_7e, 1, 1, local_58);
  local_7c = (int) sVar1;
  local_68 = 0x2d3;
  local_78 = 0;
  while (local_78 < local_68) {
    fputc((int)(char) local_7e, local_50);
    sVar1 = fread( & local_7e, 1, 1, local_58);
    local_7c = (int) sVar1;
    local_78 = local_78 + 1;
  }
  sVar1 = fread(local_48, 0x32, 1, local_60);
  local_64 = (int) sVar1;
  if (local_64 < 1) {
    puts("Invalid Flag");
    /* WARNING: Subroutine does not return */
    exit(0);
  }
  local_74 = 0;
  while ((int) local_74 < 100) {
    if ((local_74 & 1) == 0) {
      local_70 = 0;
      while (local_70 < 8) {
        local_7d = codedChar(local_70, local_48[(int) local_74 / 2], local_7e);
        fputc((int)(char) local_7d, local_50);
        fread( & local_7e, 1, 1, local_58);
        local_70 = local_70 + 1;
      }
    } else {
      fputc((int)(char) local_7e, local_50);
      fread( & local_7e, 1, 1, local_58);
    }
    local_74 = local_74 + 1;
  }
  while (local_7c == 1) {
    fputc((int)(char) local_7e, local_50);
    sVar1 = fread( & local_7e, 1, 1, local_58);
    local_7c = (int) sVar1;
  }
  fclose(local_50);
  fclose(local_58);
  fclose(local_60);
  if (local_10 == * (long * )(in_FS_OFFSET + 0x28)) {
    return 0;
  }
  /* WARNING: Subroutine does not return */
  __stack_chk_fail();
}
~~~

This can be cleaned up for simplicity:

~~~c
int main(void)

{
  size_t sVar1;
  byte bmp_buffer;
  byte otp_buffer;
  FILE * file_flag;
  FILE * file_bitmap;
  FILE * file_encoded;
  byte flag_buffer[56];


  file_flag = fopen("flag.txt", "r");
  file_bitmap = fopen("original.bmp", "r");
  file_encoded = fopen("encoded.bmp", "a");
  sVar1 = fread( &bmp_buffer, 1, 1, file_bitmap);
  for (int i=0; i < 723; i++){
    fputc((int)(char) bmp_buffer, file_encoded);
    sVar1 = fread( &bmp_buffer, 1, 1, file_bitmap);
  }
  sVar1 = fread(flag_buffer, 50, 1, file_flag);

  for (int i=0; i<100; i++){
    if ((i & 1) == 0) {
      for(int j=0; j<8; j++){
        otp_buff = codedChar(j, flag_buffer[(int) i/2], bmp_buffer);
        fputc((int)(char) otp_buffer, file_encoded);
        fread( &bmp_buffer, 1, 1, file_bitmap);
      }
    } else {
      fputc((int)(char) bmp_buffer, file_encoded);
      fread( &bmp_buffer, 1, 1, file_bitmap);
    }
  }
  while ((int) sVar1 == 1) {
    fputc((int)(char) bmp_buffer, file_encoded);
    sVar1 = fread( & bmp_buffer, 1, 1, file_bitmap);
  }
  fclose(file_encoded);
  fclose(file_bitmap);
  fclose(file_flag);

  return 0;
}
~~~

We can see that the Bytes of interest start at Byte 723 and continue for 450 Bytes.  We can extract these Bytes using dd:

~~~shell
$ dd skip=723 count=450 if=encoded.bmp of=output.binary bs=1
450+0 records in
450+0 records out
450 bytes copied, 0.00426108 s, 106 kB/s
~~~

We can make some minor adjustments to the python code used in invetsigative reversing 2:

~~~py
bin_str = ['']*50
int_str = [0]*50
flag = ''

file = open("output.binary","rb")
byte = file.read(1)

i = 0
for i in range(0,100,1):
    if i%2==0:
        for j in range(0,8,1):
            bin_val = ord(byte)&0x1
            bin_str[int(i/2)] = str(bin_val) + bin_str[int(i/2)]
            byte = file.read(1)
    else:
        byte = file.read(1)

for i in range(0,50,1):
    int_str[i] = int(bin_str[i],2)
    newchar = chr(int_str[i])
    flag += newchar

print(flag)
~~~

This returns:

~~~shell
In [1]: runfile('InvestigativeReversing3.py')
picoCTF{4n0th3r_L5b_pr0bl3m_0000000000000dec3960d}
~~~

</details>

### Answer

<details>

<summary markdown="span">Flag</summary>

~~~
picoCTF{4n0th3r_L5b_pr0bl3m_0000000000000dec3960d}
~~~

</details>

---

### [Forensics](#contents) | [PicoCTF](./picoctf.md) | [Home](./index.md)

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

This is the 4th Investigative Reporting challenge.  We can import the mystery binary and decompile it in Ghidra again:

~~~c
undefined8 main(void)
{
  size_t sVar1;
  undefined4 local_4c;
  undefined local_48 [52];
  int local_14;
  FILE *local_10;
  
  flag = local_48;
  local_4c = 0;
  flag_index = &local_4c;
  local_10 = fopen("flag.txt","r");
  if (local_10 == (FILE *)0x0) {
    puts("No flag found, please make sure this is run on the server");
  }
  sVar1 = fread(flag,0x32,1,local_10);
  local_14 = (int)sVar1;
  if (local_14 < 1) {
    puts("Invalid Flag");
                    /* WARNING: Subroutine does not return */
    exit(0);
  }
  fclose(local_10);
  encodeAll();
  return 0;
}
~~~

This can be simplified as before:

~~~c
int main(void)
{
  size_t sVar1;
  int index;
  char flag [52];
  FILE *flag_file;
  
  index = 0;
  flag_index = &index;
  flag_file = fopen("flag.txt","r");
  sVar1 = fread(flag,50,1,flag_file);

  fclose(flag_file);
  encodeAll();
  return 0;
}
~~~

The main function reads the flags.txt into a new 50-character array, flag. The main function then calls the encodeAll function:

~~~c
void encodeAll(void)
{
  ulong local_48;
  undefined8 local_40;
  undefined4 local_38;
  ulong local_28;
  undefined8 local_20;
  undefined4 local_18;
  char local_9;
  local_28 = 0x635f31306d657449;
  local_20 = 0x706d622e70;
  local_18 = 0;
  local_48 = 0x622e31306d657449;
  local_40 = 0x706d;
  local_38 = 0;
  local_9 = '5';
  while ('0' < local_9) {
    local_48._0_6_ = CONCAT15(local_9,(undefined5)local_48);
    local_48 = local_48 & 0xffff000000000000 | (ulong)(uint6)local_48;
    local_28._0_6_ = CONCAT15(local_9,(undefined5)local_28);
    local_28 = local_28 & 0xffff000000000000 | (ulong)(uint6)local_28;
    encodeDataInFile((char *)&local_48,(char *)&local_28);
    local_9 = local_9 + -1;
  }
  return;
}
~~~

This function generates concatenated strings for passing to the encodedDataInFile function:

~~~c
void encodeDataInFile(char *param_1,char *param_2)
{
  size_t sVar1;
  byte local_2e;
  byte local_2d;
  int local_2c;
  FILE *local_28;
  FILE *local_20;
  int local_18;
  int local_14;
  int local_10;
  int local_c;
  
  local_20 = fopen(param_1,"r");
  local_28 = fopen(param_2,"a");
  if (local_20 != (FILE *)0x0) {
    sVar1 = fread(&local_2e,1,1,local_20);
    local_c = (int)sVar1;
    local_2c = 0x7e3;
    local_10 = 0;
    while (local_10 < local_2c) {
      fputc((int)(char)local_2e,local_28);
      sVar1 = fread(&local_2e,1,1,local_20);
      local_c = (int)sVar1;
      local_10 = local_10 + 1;
    }
    local_14 = 0;
    while (local_14 < 0x32) {
      if (local_14 % 5 == 0) {
        local_18 = 0;
        while (local_18 < 8) {
          local_2d = codedChar(local_18,*(byte *)(*flag_index + flag),local_2e);
          fputc((int)(char)local_2d,local_28);
          fread(&local_2e,1,1,local_20);
          local_18 = local_18 + 1;
        }
        *flag_index = *flag_index + 1;
      }
      else {
        fputc((int)(char)local_2e,local_28);
        fread(&local_2e,1,1,local_20);
      }
      local_14 = local_14 + 1;
    }
    while (local_c == 1) {
      fputc((int)(char)local_2e,local_28);
      sVar1 = fread(&local_2e,1,1,local_20);
      local_c = (int)sVar1;
    }
    fclose(local_28);
    fclose(local_20);
    return;
  }
  puts("No output found, please run this on the server");
                    /* WARNING: Subroutine does not return */
  exit(0);
}
~~~

This function appends the flag encoded to the file with name passed from the calling function.  We can simplify the function:

~~~c
void encodeDataInFile(char *param_1,char *param_2)

{
  size_t sVar1;
  byte bmp_buff;
  byte enc_buff;
  FILE *enc_file;
  FILE *bmp_file;
  
  bmp_file = fopen(param_1,"r");
  enc_file = fopen(param_2,"a");
  if (bmp_file != (FILE *)0x0) {
    sVar1 = fread(&bmp_buff,1,1,bmp_file);
    for(int i=0; i<2019; i++){
      fputc((int)(char)bmp_buff,enc_file);
      sVar1 = fread(&bmp_buff,1,1,bmp_file);
    }
    for(int i=0; i<50; i++){
      if (i % 5 == 0) {
	for(int j=0; j<8; j++){
          enc_buff = codedChar(j,*(byte *)(*flag_index + flag),bmp_buff);
          fputc((int)(char)enc_buff,enc_file);
          fread(&bmp_buff,1,1,bmp_file);
        }
        *flag_index = *flag_index + 1;
      }
      else {
        fputc((int)(char)bmp_buff,enc_file);
        fread(&bmp_buff,1,1,bmp_file);
      }
    }
    while ((int) sVar1 == 1) {
      fputc((int)(char)bmp_buff,enc_file);
      sVar1 = fread(&bmp_buff,1,1,bmp_file);
    }
    fclose(enc_file);
    fclose(bmp_file);
    return;
  }
}
~~~

This function copies the first 2019 bytes directly from the source bitmap to the encoded bitmap.  Following this, the source bitmap is copied with an encoded flag iterating 5 Bytes of the bitmap, followed by 8 Bytes with the encoded flag.  The data we are interested in is stored in the encoded bitmaps starting at 2019B for 120B.  We can isolate these segments using dd:

~~~shell
$ for ((i=1; i<=5; i++)); do infile="Item0"$i"_cp.bmp"; outfile="output_0"$i".binary"; dd skip=2019 count=120 if=$infile of=$outfile bs=1; done
120+0 records in
120+0 records out
120 bytes copied, 0.000354645 s, 338 kB/s
120+0 records in
120+0 records out
120 bytes copied, 0.000345508 s, 347 kB/s
120+0 records in
120+0 records out
120 bytes copied, 0.000603438 s, 199 kB/s
120+0 records in
120+0 records out
120 bytes copied, 0.000637103 s, 188 kB/s
120+0 records in
120+0 records out
120 bytes copied, 0.000292808 s, 410 kB/s

61440 bytes (61 kB, 60 KiB) copied, 0.000273198 s, 225 MB/s
~~~

We can extract the flag characters from these binary files by reversing the c algorithm in Python:

~~~py
bin_str  = ['']*50
int_str  = [0]*50
flag     = ''
x = int(0)
for i in range(0,5,1):
    file_index = int(5-i)
    file = open("output_0{}.binary".format(file_index),"rb")
    for j in range(0,50,1):
        if(j%5==0):
            for k in range(0,8,1):
                byte = file.read(1)
                binval = ord(byte)&0x01
                bin_str[x] = str(binval) + bin_str[x]
            x += 1
        else:
            byte = file.read(1)
    file.close()

for i in range(0,50,1):
    int_str[i] = int(bin_str[i],2)
    newchar = chr(int_str[i])
    flag += newchar

print(flag)
~~~

Executing this provides the following:

~~~shell
$ python InvestigativeReversing04.py
picoCTF{N1c3_R3ver51ng_5k1115_00000000000f9d605bf}
~~~

This provides the flag picoCTF{N1c3_R3ver51ng_5k1115_00000000000f9d605bf}.

</details>

### Answer

<details>

<summary markdown="span">Flag</summary>

~~~
picoCTF{N1c3_R3ver51ng_5k1115_00000000000f9d605bf}
~~~

</details>

---

### [Forensics](#contents) | [PicoCTF](./picoctf.md) | [Home](./index.md)

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

Using file, we can identify the file types:

~~~shell
$ file *
mystery: ELF 64-bit LSB shared object, x86-64, version 1 (SYSV), dynamically linked, interpreter /lib64/ld-linux-x86-64.so.2, for GNU/Linux 3.2.0, BuildID[sha1]=29b4dba83a1a5a26d76e122ad48d63cff886b075, not stripped
output:  Non-ISO extended-ASCII text, with no line terminators
~~~

It appears mystery is an [Executable and Linkable Format (ELF)](https://www.opensourceforu.com/2020/02/understanding-elf-the-executable-and-linkable-format/) file and output is a nonstandard ASCII text file.

Using readelf, we can investigate mystery further:

~~~shell
$ readelf -h mystery 
ELF Header:
  Magic:   7f 45 4c 46 02 01 01 00 00 00 00 00 00 00 00 00 
  Class:                             ELF64
  Data:                              2's complement, little endian
  Version:                           1 (current)
  OS/ABI:                            UNIX - System V
  ABI Version:                       0
  Type:                              DYN (Shared object file)
  Machine:                           Advanced Micro Devices X86-64
  Version:                           0x1
  Entry point address:               0x7c0
  Start of program headers:          64 (bytes into file)
  Start of section headers:          11448 (bytes into file)
  Flags:                             0x0
  Size of this header:               64 (bytes)
  Size of program headers:           56 (bytes)
  Number of program headers:         9
  Size of section headers:           64 (bytes)
  Number of section headers:         30
  Section header string table index: 29
~~~

This shows us the entrypoint for the ELF is x7c0.  This can be confirmed using objdump:

~~~shell
$ objdump -f mystery

mystery:     file format elf64-x86-64
architecture: i386:x86-64, flags 0x00000150:
HAS_SYMS, DYNAMIC, D_PAGED
start address 0x00000000000007c0
~~~

We can either use gdb to investigate the assembly or we can decompile. Using Ghildra, we can import the mystery binary and decompile.  The main function is decompiled:

~~~c
undefined8 main(void)

{
  long lVar1;
  size_t sVar2;
  undefined4 local_18;
  int local_14;
  FILE *local_10;
  
  local_10 = fopen("flag.txt","r");
  if (local_10 == (FILE *)0x0) {
    fwrite("./flag.txt not found\n",1,0x15,stderr);
                    /* WARNING: Subroutine does not return */
    exit(1);
  }
  flag_size = 0;
  fseek(local_10,0,2);
  lVar1 = ftell(local_10);
  flag_size = (int)lVar1;
  fseek(local_10,0,0);
  if (0xfffe < flag_size) {
    fwrite("Error, file bigger that 65535\n",1,0x1e,stderr);
                    /* WARNING: Subroutine does not return */
    exit(1);
  }
  flag = malloc((long)flag_size);
  sVar2 = fread(flag,1,(long)flag_size,local_10);
  local_14 = (int)sVar2;
  if (local_14 < 1) {
                    /* WARNING: Subroutine does not return */
    exit(0);
  }
  local_18 = 0;
  flag_index = &local_18;
  output = fopen("output","w");
  buffChar = 0;
  remain = 7;
  fclose(local_10);
  encode();
  fclose(output);
  fwrite("I\'m Done, check ./output\n",1,0x19,stderr);
  return 0;
}
~~~

We can tidy this up:

~~~c
int main(void)
{
  undefined4 local_18;
  int local_14;
  FILE *flag_file = fopen("flag.txt","r");
  fseek(flag_file,0,2);
  int flag_size = (int) ftell(flag_file);
  fseek(flag_file,0,0);
  flag = malloc((long)flag_size);
  size_t sVar2 = fread(flag,1,(long)flag_size,flag_file);
  local_14 = (int)sVar2;
  output = fopen("output","w");
  buffChar = 0;
  remain = 7;
  fclose(flag_file);
  encode();
  fclose(output);
  return 0;
}
~~~

The main function opens the file containing the flag, reads the flag and sets some global variables, then opens a writable file (output) closes the flag_file and calls the function "encode()":
	
~~~c
void encode(void)
{
  byte bVar1;
  uint uVar2;
  int iVar3;
  undefined8 uVar4;
  int local_10;
  char local_9;
  
  while( true ) {
    if (flag_size <= *flag_index) {
      while (remain != 7) {
        save(0);
      }
      return;
    }
    bVar1 = *(byte *)(*flag_index + flag);
    uVar4 = isValid(bVar1);
    if ((char)uVar4 != '\x01') break;
    uVar2 = lower(bVar1);
    local_9 = (char)uVar2;
    if (local_9 == ' ') {
      local_9 = '{';
    }
    local_10 = *(int *)(matrix + (long)(local_9 + -0x61) * 8 + 4);
    iVar3 = local_10 + *(int *)(matrix + (long)(local_9 + -0x61) * 8);
    while (local_10 < iVar3) {
      uVar2 = getValue(local_10);
      save((byte)uVar2);
      local_10 = local_10 + 1;
    }
    *flag_index = *flag_index + 1;
  }
  fwrite("Error, I don\'t know why I crashed\n",1,0x22,stderr);
                    /* WARNING: Subroutine does not return */
  exit(1);
}
~~~

Simplifying this makes it easier to understand:
	
~~~c
void encode(void)
{
  byte flag_byte;
  uint flag_int;
  int iVar3;
  undefined8 uVar4;
  int i;
  char flag_char;
  
  for(int flag_index=0; flag_index<flag_size; flag_index++){
    flag_byte = *(byte *)(flag_index + flag);
    flag_int = lower(flag_byte);
    flag_char = (char)flag_int;
    if (flag_char == ' ') {
      flag_char = '{';
    }
    i = *(int *)(matrix + (long)(flag_char - 97) * 8 + 4);
    iVar3 = i + *(int *)(matrix + (long)(flag_char - 97) * 8);
    while (i < iVar3) {
      flag_int = getValue(i);
      save((byte)flag_int);
      i++;
    }
  }
}
~~~
	
encode() iterates through the flag using flag_index. The characters at each index are read and converted to lower-case and if the character is " " it is substituted for "{".  Two variables, i and iVar3 are calculated using a variable "matrix". This provides the iteration limits for the while loop in which the value i is given to flag int and sent to another subroutine, "save()".
	
We can import the matrix and secret into python and generate output codes for the alphabet.  This can be used to iterate backwards to solve the flag, since the output may have null characters appended at the beginning:

~~~py
#!/usr/bin/env python3
# -*- coding: utf-8 -*-
"""
Created on Sun Jan  2 11:36:14 2022

@author: derek
"""

matrix = [ 8,           0,       0,      0,   0, 201326592,  786432, 3072, 
          12,   134217728,  524288,   2048,   8, 234881024,  917504, 3584, 
          14,   335544320, 1310720,   5120,  20, 167772160,  655360, 2560, 
          10,   570425344, 2228224,   8704,  34,  67108864,  262144, 1024, 
           4,   738197504, 2883584,  11264,  44, 201326592,  786432, 3072, 
          12,   805306368, 3145728,  12288,  48, 201326592,  786432, 3072, 
          12,  1006632960, 3932160,  15360,  60, 167772160,  655360, 2560, 
          10,  1207959552, 4718592,  18432,  72, 100663296,  393216, 1536, 
           6,  1375731712, 5373952,  20992,  82, 268435456, 1048576, 4096, 
          16,  1476395008, 5767168,  22528,  88, 201326592,  786432, 3072, 
          12,  1744830464, 6815744,  26624, 104, 201326592,  786432, 3072, 
          12,  1946157056, 7602176,  29696, 116, 167772160,  655360, 2560, 
          10, -2147483648, 8388608,  32768, 128, 134217728,  524288, 2048, 
           8, -1979711488, 9043968,  35328, 138, 234881024,  917504, 3584, 
          14, -1845493760, 9568256,  37376, 146, 234881024,  917504, 3584, 
          14, -1610612736, 10485760, 40960, 160, 268435456, 1048576, 4096, 
          16, -1375731712, 11403264, 44544, 174, 167772160,  655360, 2560, 
          10, -1107296256, 12451840, 48640, 190, 134217728,  524288, 2048, 
           8,  -939524096, 13107200, 51200, 200, 100663296,  393216, 1536, 
           6,  -805306368, 13631488, 53248, 208, 167772160,  655360, 2560, 
          10,  -704643072, 14024704, 54784, 214, 201326592,  786432, 3072, 
          12,  -536870912, 14680064, 57344, 224, 201326592,  786432, 3072, 
          12,  -335544320, 15466496, 60416, 236, 234881024,  917504, 3584, 
          14,  -134217728, 16252928, 63488, 248, 268435456, 1048576, 4096, 
          16,   100663296, 17170432, 67072, 262, 234881025,  917504, 3584, 
          14,   369098752, 18219008, 71168, 278,  67108865,  262144, 1024, 
           4,   603979776, 19136512, 74752, 292,         1,       0,    0]

secret = [0xb8, 0xea, 0x8e, 0xba, 0x3a, 0x88, 0xae, 0x8e, 0xe8, 0xaa,
          0x28, 0xbb, 0xb8, 0xeb, 0x8b, 0xa8, 0xee, 0x3a, 0x3b, 0xb8,
          0xbb, 0xa3, 0xba, 0xe2, 0xe8, 0xa8, 0xe2, 0xb8, 0xab, 0x8b,
          0xb8, 0xea, 0xe3, 0xae, 0xe3, 0xba, 0x80]

def getValue(a):
    b = int(a)
    if (a<0):
        b = int(a+7)
    c = a>>0x37
    secret_buff = secret[b>>3]
    shift = 7-((a+(c>>5)&7)-(c>>5))&0x1f
    d = (secret_buff >> shift)&1
    return d

def encode_char(letter):
    output = ""
    if letter == " ":
        letter = "{"
    letter = letter.lower()
    letter = letter.encode()
    letter = ord(letter)
    index1 = (letter-0x61)*8 + 4
    index2 = (letter-0x61)*8
    a = matrix[index1]
    b1 = matrix[index2]
    b = a + b1
    while a < b:
        c = getValue(a)
        output += str(c)
        a += 1
    return output
    
def encode_flag(flag):
    output = ""
    for i in range(8-len(flag)%8):
        output += str(0)
    for letter in flag:
        output += encode_char(letter)
    return output

def dictionary():
    abc = "abcdefghijklmnopqrstuvwxyz"
    abc_dict = []
    for i in range(len(abc)):
        enc_letter = encode_char(abc[i])
        abc_dict.append(enc_letter)
        print("{} encoded is {}".format(abc[i],enc_letter))
    return abc_dict

def decode_flag(enc_flag):
    abc = "abcdefghijklmnopqrstuvwxyz"
    d = dictionary()
    for i in range(len(d)):
        d[i] = d[i][::-1]
    enc_flag = enc_flag[::-1]
    solution_letters = [""]
    solution_binary = [""]
    done = 0
    while done == 0:
        new_solution_letters = []
        new_solution_binary = []
        for i in range(len(solution_letters)):
            for j in range(len(abc)):
                binattempt = solution_binary[i]+d[j]
                letattempt = solution_letters[i]+abc[j]
                if binattempt == enc_flag[:len(binattempt)]:
                    new_solution_binary.append(binattempt)
                    new_solution_letters.append(letattempt)
                    if (len(enc_flag)-len(binattempt)) < 8:
                        if(len(enc_flag)-len(binattempt)) == 0:
                            answer = letattempt[::-1]
                            done = 1
                        elif int(enc_flag[len(binattempt):])==0:
                            answer = letattempt[::-1]
                            done = 1
        solution_letters = new_solution_letters
        solution_binary = new_solution_binary
    return answer
    
if __name__ == "__main__":
    #testflag = "testCTFthisIsAteSt"
    #testout = encode_flag(testflag)
    #findflag = decode_flag(testout)
    #print(testflag)
    #print(testout)
    #print(findflag)
    
    file = open("output","rb")
    encflag = file.read()
    file.close()
    encflag_bin = ""
    for i in range(len(encflag)):
        buff = encflag[i]
        a = buff >> 7
        encflag_bin += str(a)
        buff = buff - (a << 7)
        a = buff >> 6
        encflag_bin += str(a)
        buff = buff - (a << 6)
        a = buff >> 5
        encflag_bin += str(a)
        buff = buff - (a << 5)
        a = buff >> 4
        encflag_bin += str(a)
        buff = buff - (a << 4)
        a = buff >> 3
        encflag_bin += str(a)
        buff = buff - (a << 3)
        a = buff >> 2
        encflag_bin += str(a)
        buff = buff - (a << 2)
        a = buff >> 1
        encflag_bin += str(a)
        buff = buff - (a << 1)
        encflag_bin += str(buff)
        
    flag = decode_flag(encflag_bin)
    print("flag is: "+flag)
~~~

This provides the flag.

</details>

### Answer

<details>

<summary markdown="span">Flag</summary>

~~~
encodedyizvbdqluv
~~~

</details>

---

### [Forensics](#contents) | [PicoCTF](./picoctf.md) | [Home](./index.md)

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

We can solve this with the exact command used for WebNet0 challenge:

~~~shell
$ ssldump -Aed -nr ./capture.pcap -k ./picopico.key | grep -A2 pico
    61 67 3a 20 70 69 63 6f 43 54 46 7b 74 68 69 73    ag: picoCTF{this
    2e 69 73 2e 6e 6f 74 2e 79 6f 75 72 2e 66 6c 61    .is.not.your.fla
    67 2e 61 6e 79 6d 6f 72 65 7d 0d 0a 43 6f 6e 74    g.anymore}..Cont
--
    67 3a 20 70 69 63 6f 43 54 46 7b 74 68 69 73 2e    g: picoCTF{this.
    69 73 2e 6e 6f 74 2e 79 6f 75 72 2e 66 6c 61 67    is.not.your.flag
    2e 61 6e 79 6d 6f 72 65 7d 0d 0a 43 6f 6e 74 65    .anymore}..Conte
--
    Pico-Flag: picoCTF{this.is.not.your.flag.anymore}
    Keep-Alive: timeout=5, max=99
    Connection: Keep-Alive
--
    00 00 00 01 00 00 00 01 70 69 63 6f 43 54 46 7b    ........picoCTF{
    68 6f 6e 65 79 2e 72 6f 61 73 74 65 64 2e 70 65    honey.roasted.pe
    61 6e 75 74 73 7d 00 00 ff e2 02 1c 49 43 43 5f    anuts}......ICC_
~~~

We get two red-herring flags and the flag picoCTF{honey.roasted.peanuts}

</details>

### Answer

<details>

<summary markdown="span">Flag</summary>

~~~
picoCTF{honey.roasted.peanuts}
~~~

</details>

---

### [Forensics](#contents) | [PicoCTF](./picoctf.md) | [Home](./index.md)

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

Similar to investigation encoded 2, we get a binary "mystery" and an output file:
	
~~~shell
mystery: ELF 64-bit LSB shared object, x86-64, version 1 (SYSV), dynamically linked, interpreter /lib64/ld-linux-x86-64.so.2, for GNU/Linux 3.2.0, BuildID[sha1]=b3214ef986bc85652feb1040e5970f356b56dd71, not stripped
output:  Non-ISO extended-ASCII text, with no line terminators
~~~

Decompiling in Ghidra, we can see a main function:

~~~c
undefined8 main(void)

{
  long lVar1;
  size_t sVar2;
  undefined4 local_18;
  int local_14;
  FILE *local_10;
  
  badChars = '\0';
  local_10 = fopen("flag.txt","r");
  if (local_10 == (FILE *)0x0) {
    fwrite("Error: file ./flag.txt not found\n",1,0x21,stderr);
                    /* WARNING: Subroutine does not return */
    exit(1);
  }
  flag_size = 0;
  fseek(local_10,0,2);
  lVar1 = ftell(local_10);
  flag_size = (int)lVar1;
  fseek(local_10,0,0);
  login();
  if (0xfffe < flag_size) {
    fwrite("Error, file bigger than 65535\n",1,0x1e,stderr);
                    /* WARNING: Subroutine does not return */
    exit(1);
  }
  flag = malloc((long)flag_size);
  sVar2 = fread(flag,1,(long)flag_size,local_10);
  local_14 = (int)sVar2;
  if (local_14 < 1) {
                    /* WARNING: Subroutine does not return */
    exit(0);
  }
  local_18 = 0;
  flag_index = &local_18;
  output = fopen("output","w");
  buffChar = 0;
  remain = 7;
  fclose(local_10);
  encode();
  fclose(output);
  if (badChars == '\x01') {
    fwrite("Invalid Characters in flag.txt\n./output is corrupted\n",1,0x35,stderr);
  }
  else {
    fwrite("I\'m Done, check file ./output\n",1,0x1e,stderr);
  }
  return 0;
}
~~~
	
The first part of this program imports the flag.txt file, creates a file handle, handles errors in the flag (missing file or missing content (size < 1) or excessively large (>65535)) and loads variables with the file contents and flag size, we can rewrite in pseudo-code removing the error handling:

~~~
main():
  flag_file = open(flag.txt)
  flag_size = size(flag_file)
  login()
  flag = int(read(flag_file))
  flag_index = 0;
  output_file = open(output);
  buffchar = 0
  remain = 7
  close(flag_file)
  encode()
  close(output_file)
  return 0;
}
~~~

As can be seen, two external functions are called: login() and encode().  The login() function likely stops the execution of the file without authentication.  We will look at encode():

~~~c

void encode(void)

{
  byte bVar1;
  uint uVar2;
  int iVar3;
  int local_10;
  char local_9;
  
  while (*flag_index < flag_size) {
    uVar2 = lower(*(byte *)(*flag_index + flag));
    local_9 = (char)uVar2;
    if (local_9 == ' ') {
      local_9 = -0x7b;
    }
    else if (('/' < local_9) && (local_9 < ':')) {
      local_9 = local_9 + 'K';
    }
    local_9 = local_9 + -0x61;
    if ((local_9 < '\0') || ('$' < local_9)) {
      badChars = 1;
    }
    if (local_9 != '$') {
      iVar3 = (local_9 + 0x12) % 0x24;
      bVar1 = (byte)(iVar3 >> 0x1f);
      local_9 = ((byte)iVar3 ^ bVar1) - bVar1;
    }
    iVar3 = *(int *)(indexTable + (long)(local_9 + 1) * 4);
    for (local_10 = *(int *)(indexTable + (long)(int)local_9 * 4); local_10 < iVar3;
        local_10 = local_10 + 1) {
      uVar2 = getValue(local_10);
      save((byte)uVar2);
    }
    *flag_index = *flag_index + 1;
  }
  while (remain != 7) {
    save(0);
  }
  return;
}
~~~

This function iterates through the flag, changes all characters to lower case and replaces certain non alphanumeric characters before calling external functions getValue() and save().  We can rewrite in pseudo-code removing the error checking:
										   
~~~
encode():
  while(flag_index < flag_size):
    flagint = lower(flag[flag_index])
    if flagint == 32:
      flagint = -123
    elif 47 < flagint < 58:
      flagint = flagint + 75
    flagint = flagint - 97
    if flagint != 36:
      A = (flagint + 18)%36
      B = A >> 31
      flagint = (A^B)-B
    C = indexTable[(flagint+1)*4]
    D = indexTable[flagint*4]
    for (i = D, i < C, i++):
      E = getValue(i)
      save(E)
    flag_index++
  while (remain != 7):
    save(0)
  return
~~~
		     
As can be seen, the encode function iterates through the flag object and generates a related integer which is used to look up a value from indexTable which is used to call the function getValue:
		     
~~~c
uint getValue(int param_1)

{
  byte bVar1;
  int iVar2;
  
  iVar2 = param_1;
  if (param_1 < 0) {
    iVar2 = param_1 + 7;
  }
  bVar1 = (byte)(param_1 >> 0x37);
  return (int)(uint)(byte)secret[iVar2 >> 3] >>
         (7 - (((char)param_1 + (bVar1 >> 5) & 7) - (bVar1 >> 5)) & 0x1f) & 1;
}
~~~

Again, this can be simplified:

~~~
getValue(X):
  Y = X
  if X < 0:
    Y = X+7
  A = X >> 55
  B = Y >> 3
  C = 7 - (X + (A>>5)&7-(A>>5))&31
  D = secret[B]>>(C&1)
  return D
~~~

We also have a "secret" global variable.  The two global variables can be found in Ghidra:

1. indexTable:

~~~
[0x00, 0x00, 0x00, 0x00, 0x04, 0x00, 0x00, 0x00, 0x12, 0x00, 0x00, 0x00, 0x28, 0x00, 0x00, 0x00, 0x3c, 0x00, 0x00, 0x00,
 0x52, 0x00, 0x00, 0x00, 0x64, 0x00, 0x00, 0x00, 0x78, 0x00, 0x00, 0x00, 0x8e, 0x00, 0x00, 0x00, 0x9e, 0x00, 0x00, 0x00,
 0xb4, 0x00, 0x00, 0x00, 0xc8, 0x00, 0x00, 0x00, 0xda, 0x00, 0x00, 0x00, 0xea, 0x00, 0x00, 0x00, 0xfc, 0x00, 0x00, 0x00,
 0x0e, 0x01, 0x00, 0x00, 0x1e, 0x01, 0x00, 0x00, 0x34, 0x01, 0x00, 0x00, 0x48, 0x01, 0x00, 0x00, 0x5a, 0x01, 0x00, 0x00,
 0x6a, 0x01, 0x00, 0x00, 0x78, 0x01, 0x00, 0x00, 0x80, 0x01, 0x00, 0x00, 0x8c, 0x01, 0x00, 0x00, 0x9a, 0x01, 0x00, 0x00,
 0xaa, 0x01, 0x00, 0x00, 0xbc, 0x01, 0x00, 0x00, 0xc8, 0x01, 0x00, 0x00, 0xd6, 0x01, 0x00, 0x00, 0xe0, 0x01, 0x00, 0x00, 
 0xea, 0x01, 0x00, 0x00, 0xf0, 0x01, 0x00, 0x00, 0x00, 0x02, 0x00, 0x00, 0x0a, 0x02, 0x00, 0x00, 0x16, 0x02, 0x00, 0x00,
 0x22, 0x02, 0x00, 0x00, 0x30, 0x02, 0x00, 0x00, 0x34, 0x02, 0x00, 0x00]
~~~

2. secret:
	
~~~
[0x8b, 0xaa, 0x2e, 0xee, 0xe8, 0xbb, 0xae, 0x8e, 0xbb, 0xae, 
 0x3a, 0xee, 0x8e, 0xee, 0xa8, 0xee, 0xae, 0xe3, 0xaa, 0xe3,
 0xae, 0xbb, 0x8b, 0xae, 0xb8, 0xea, 0xae, 0x2e, 0xba, 0x2e,
 0xae, 0x8a, 0xee, 0xa3, 0xab, 0xa3, 0xbb, 0xbb, 0x8b, 0xbb,
 0xb8, 0xae, 0xee, 0x2a, 0xee, 0x2e, 0x2a, 0xb8, 0xaa, 0x8e, 
 0xaa, 0x3b, 0xaa, 0x3b, 0xba, 0x8e, 0xa8, 0xeb, 0xa3, 0xa8,
 0xaa, 0x28, 0xbb, 0xb8, 0xae, 0x2a, 0xe2, 0xee, 0x3a, 0xb8, 
 0x00]
~~~

This challenge includes numerical characters in the encoding scheme.  We can adapt our previous python code to solve:

~~~py
#!/usr/bin/env python3
# -*- coding: utf-8 -*-
"""
Created on Sun Jan  2 11:36:14 2022

@author: derek
"""

indexTable = [0x00000000, 0x00000004, 0x00000012, 0x00000028,
              0x0000003c, 0x00000052, 0x00000064, 0x00000078,
              0x0000008e, 0x0000009e, 0x000000b4, 0x000000c8,
              0x000000da, 0x000000ea, 0x000000fc, 0x0000010e,
              0x0000011e, 0x00000134, 0x00000148, 0x0000015a,
              0x0000016a, 0x00000178, 0x00000180, 0x0000018c,
              0x0000019a, 0x000001aa, 0x000001bc, 0x000001c8,
              0x000001d6, 0x000001e0, 0x000001ea, 0x000001f0,
              0x00000200, 0x0000020a, 0x00000216, 0x00000222,
              0x00000230, 0x00000234]

secret = [0x8b, 0xaa, 0x2e, 0xee, 0xe8, 0xbb, 0xae, 0x8e, 0xbb, 0xae, 
          0x3a, 0xee, 0x8e, 0xee, 0xa8, 0xee, 0xae, 0xe3, 0xaa, 0xe3,
          0xae, 0xbb, 0x8b, 0xae, 0xb8, 0xea, 0xae, 0x2e, 0xba, 0x2e,
          0xae, 0x8a, 0xee, 0xa3, 0xab, 0xa3, 0xbb, 0xbb, 0x8b, 0xbb,
          0xb8, 0xae, 0xee, 0x2a, 0xee, 0x2e, 0x2a, 0xb8, 0xaa, 0x8e, 
          0xaa, 0x3b, 0xaa, 0x3b, 0xba, 0x8e, 0xa8, 0xeb, 0xa3, 0xa8,
          0xaa, 0x28, 0xbb, 0xb8, 0xae, 0x2a, 0xe2, 0xee, 0x3a, 0xb8, 
          0x00]

def getValue(a):
    b = int(a)
    if (a<0):
        b = int(a+7)
    c = a >> 55
    secret_buff = secret[ b >> 3 ]
    shift = 7 - ( a + ( c >> 5 ) & 7 - ( c >> 5 )) & 31
    d = secret_buff >> shift &1
    return d

def encode_char(letter):
    output = ""
    letter = letter.lower()
    letter = letter.encode()
    letter = ord(letter)
    if letter == 32:
        letter = -132
    elif 47 < letter < 58:
        letter += 75
    letter = letter - 97
    if letter != 36:
        a = (letter+18)%36
        b = a >> 31
        letter = (a^b)-b
    index1 = (letter+1)
    index2 = letter
    c = indexTable[index1]
    d = indexTable[index2]
    while d < c:
        e = getValue(d)
        output += str(e)
        d += 1
    return output
    
def encode_flag(flag):
    output = ""
    for i in range(8-len(flag)%8):
        output += str(0)
    for letter in flag:
        output += encode_char(letter)
    return output

def dictionary():
    abc = "abcdefghijklmnopqrstuvwxyz0123456789"
    abc_dict = []
    for i in range(len(abc)):
        enc_letter = encode_char(abc[i])
        abc_dict.append(enc_letter)
        print("{} encoded is {}".format(abc[i],enc_letter))
    return abc_dict

def decode_flag(enc_flag):
    abc = "abcdefghijklmnopqrstuvwxyz0123456789"
    d = dictionary()
    for i in range(len(d)):
        d[i] = d[i][::-1]
    enc_flag = enc_flag[::-1]
    solution_letters = [""]
    solution_binary = [""]
    done = 0
    while done == 0:
        new_solution_letters = []
        new_solution_binary = []
        for i in range(len(solution_letters)):
            for j in range(len(abc)):
                binattempt = solution_binary[i]+d[j]
                letattempt = solution_letters[i]+abc[j]
                if binattempt == enc_flag[:len(binattempt)]:
                    new_solution_binary.append(binattempt)
                    new_solution_letters.append(letattempt)
                    if (len(enc_flag)-len(binattempt)) < 8:
                        if(len(enc_flag)-len(binattempt)) == 0:
                            answer = letattempt[::-1]
                            done = 1
                        elif int(enc_flag[len(binattempt):])==0:
                            answer = letattempt[::-1]
                            done = 1
        solution_letters = new_solution_letters
        solution_binary = new_solution_binary
    return answer
    
if __name__ == "__main__":
    #testflag = "testCTFthisIsAteSt"
    #testout = encode_flag(testflag)
    #findflag = decode_flag(testout)
    #print(testflag)
    #print(testout)
    #print(findflag)
    
    file = open("output","rb")
    encflag = file.read()
    file.close()
    encflag_bin = ""
    for i in range(len(encflag)):
        buff = encflag[i]
        a = buff >> 7
        encflag_bin += str(a)
        buff = buff - (a << 7)
        a = buff >> 6
        encflag_bin += str(a)
        buff = buff - (a << 6)
        a = buff >> 5
        encflag_bin += str(a)
        buff = buff - (a << 5)
        a = buff >> 4
        encflag_bin += str(a)
        buff = buff - (a << 4)
        a = buff >> 3
        encflag_bin += str(a)
        buff = buff - (a << 3)
        a = buff >> 2
        encflag_bin += str(a)
        buff = buff - (a << 2)
        a = buff >> 1
        encflag_bin += str(a)
        buff = buff - (a << 1)
        encflag_bin += str(buff)
        
    flag = decode_flag(encflag_bin)
    print("flag is: "+flag)
~~~

This returns the flag.

</details>

### Answer

<details>

<summary markdown="span">Flag</summary>

~~~
t1m3f1i35000000000008eb3f829
~~~

</details>

---

### [Forensics](#contents) | [PicoCTF](./picoctf.md) | [Home](./index.md)

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

We are given a zip file with no hints or description:

~~~shell
$ file b1g_mac.zip 
b1g_mac.zip: Zip archive data, at least v2.0 to extract
~~~

We can extract the directory:

~~~shell
$ unzip b1g_mac.zip 
Archive:  b1g_mac.zip
  inflating: main.exe                
   creating: test/
  inflating: test/Item01 - Copy.bmp  
  inflating: test/Item01.bmp         
  inflating: test/Item02 - Copy.bmp  
  inflating: test/Item02.bmp         
  inflating: test/Item03 - Copy.bmp  
  inflating: test/Item03.bmp         
  inflating: test/Item04 - Copy.bmp  
  inflating: test/Item04.bmp         
  inflating: test/Item05 - Copy.bmp  
  inflating: test/Item05.bmp         
  inflating: test/Item06 - Copy.bmp  
  inflating: test/Item06.bmp         
  inflating: test/Item07 - Copy.bmp  
  inflating: test/Item07.bmp         
  inflating: test/Item08 - Copy.bmp  
  inflating: test/Item08.bmp         
  inflating: test/ItemTest - Copy.bmp  
  inflating: test/ItemTest.bmp     
~~~

We are given a main.exe executable and a directory "test":

~~~shell
$ file *
main.exe: PE32 executable (console) Intel 80386, for MS Windows
test:     directory
~~~

In the test directory, we have 19 bitmaps:

~~~shell
$ file *
Item01.bmp:          PC bitmap, Windows 3.x format, 432 x 293 x 8, image size 126576, cbSize 127654, bits offset 1078
Item01 - Copy.bmp:   PC bitmap, Windows 3.x format, 432 x 293 x 8, image size 126576, cbSize 127654, bits offset 1078
Item02.bmp:          PC bitmap, Windows 3.x format, 432 x 293 x 8, image size 126576, cbSize 127654, bits offset 1078
Item02 - Copy.bmp:   PC bitmap, Windows 3.x format, 432 x 293 x 8, image size 126576, cbSize 127654, bits offset 1078
Item03.bmp:          PC bitmap, Windows 3.x format, 432 x 293 x 8, image size 126576, cbSize 127654, bits offset 1078
Item03 - Copy.bmp:   PC bitmap, Windows 3.x format, 432 x 293 x 8, image size 126576, cbSize 127654, bits offset 1078
Item04.bmp:          PC bitmap, Windows 3.x format, 432 x 293 x 8, image size 126576, cbSize 127654, bits offset 1078
Item04 - Copy.bmp:   PC bitmap, Windows 3.x format, 432 x 293 x 8, image size 126576, cbSize 127654, bits offset 1078
Item05.bmp:          PC bitmap, Windows 3.x format, 432 x 293 x 8, image size 126576, cbSize 127654, bits offset 1078
Item05 - Copy.bmp:   PC bitmap, Windows 3.x format, 432 x 293 x 8, image size 126576, cbSize 127654, bits offset 1078
Item06.bmp:          PC bitmap, Windows 3.x format, 432 x 293 x 8, image size 126576, cbSize 127654, bits offset 1078
Item06 - Copy.bmp:   PC bitmap, Windows 3.x format, 432 x 293 x 8, image size 126576, cbSize 127654, bits offset 1078
Item07.bmp:          PC bitmap, Windows 3.x format, 432 x 293 x 8, image size 126576, cbSize 127654, bits offset 1078
Item07 - Copy.bmp:   PC bitmap, Windows 3.x format, 432 x 293 x 8, image size 126576, cbSize 127654, bits offset 1078
Item08.bmp:          PC bitmap, Windows 3.x format, 432 x 293 x 8, image size 126576, cbSize 127654, bits offset 1078
Item08 - Copy.bmp:   PC bitmap, Windows 3.x format, 432 x 293 x 8, image size 126576, cbSize 127654, bits offset 1078
ItemTest.bmp:        PC bitmap, Windows 3.x format, 432 x 293 x 8, image size 126576, cbSize 127654, bits offset 1078
ItemTest - Copy.bmp: PC bitmap, Windows 3.x format, 432 x 293 x 8, image size 126576, cbSize 127654, bits offset 1078
~~~

The main.exe can be decompiled in Ghidra,  we get the main program:

~~~c
int __cdecl _main(int _Argc,char **_Argv,char **_Env)

{
  undefined4 local_60;
  undefined local_5a [50];
  undefined4 local_28;
  undefined4 local_24;
  undefined4 local_20;
  size_t local_1c;
  FILE *local_18;
  int local_14;
  
  __main();
  _isOver = 0;
  local_28 = 0x65742f2e;
  local_24 = 0x7473;
  local_20 = 0;
  _folderName = &local_28;
  local_14 = 0;
  _pLevel = 0;
  local_18 = _fopen("flag.txt","r");
  if (local_18 == (FILE *)0x0) {
    _puts("No flag found, please make sure this is run on the server");
  }
  local_1c = _fread(local_5a,1,0x12,local_18);
  if ((int)local_1c < 1) {
                    /* WARNING: Subroutine does not return */
    _exit(0);
  }
  _flag = local_5a;
  _flag_size = 0x12;
  local_60 = 0;
  _flag_index = &local_60;
  _puts("Work is done!");
  _listdir(local_14,_folderName);
  _puts("Wait for 5 seconds to exit.");
  sleep(5);
  return 2;
}
~~~
		
We can see the program opens the flag.txt file, loads a flag object and calls a function "listdir":
		
~~~
main(argc,argv,env):
  main()
  flag_file = open(flag.txt)
  flag = read(flag_file,18)
  flag_size = 18
  flag_index = 0
  listdir()
  return
~~~
		
listdir:

~~~c
void __cdecl _listdir(int param_1,undefined4 param_2)

{
  int iVar1;
  BOOL BVar2;
  char local_958 [2048];
  _WIN32_FIND_DATAA local_158;
  HANDLE local_18;
  undefined local_11;
  int local_10;
  
  local_18 = (HANDLE)0x0;
  _sprintf(local_958,"%s\\*.*",param_2);
  local_18 = FindFirstFileA(local_958,&local_158);
  if (local_18 == (HANDLE)0xffffffff) {
    _printf("Path not found: [%s]\n",param_2);
  }
  else {
    local_10 = 1;
    local_11 = true;
    while ((bool)local_11 != false) {
      iVar1 = _strcmp(local_158.cFileName,".");
      if ((iVar1 != 0) && (iVar1 = _strcmp(local_158.cFileName,".."), iVar1 != 0)) {
        _sprintf(local_958,"%s\\%s",param_2,local_158.cFileName);
        if ((local_158.dwFileAttributes & 0x10) == 0) {
          if (local_10 == 1) {
            if (param_1 == 0) {
              _hideInFile(local_958);
            }
            else if (param_1 == 1) {
              _decodeBytes(local_958);
            }
          }
          local_10 = 1 - local_10;
        }
        else {
          _printf("Folder: %s\n",local_958);
          _listdir(param_1,local_958);
        }
      }
      if (_isOver != '\0') break;
      BVar2 = FindNextFileA(local_18,&local_158);
      local_11 = BVar2 != 0;
    }
    FindClose(local_18);
  }
  return;
}
~~~
		
This iterates through the directory and calls "hideInFile" - likely how the flag is stored in the test directory:

~~~c

void __cdecl _hideInFile(LPCSTR param_1)

{
  BOOL BVar1;
  _FILETIME local_2c;
  _FILETIME local_24;
  _FILETIME local_1c;
  char local_12;
  char local_11;
  HANDLE local_10;
  
  local_10 = CreateFileA(param_1,0x100,0,(LPSECURITY_ATTRIBUTES)0x0,3,0,(HANDLE)0x0);
  _DoNotUpdateLastAccessTime(local_10);
  if (local_10 == (HANDLE)0xffffffff) {
    _printf("Error:INVALID_HANDLED_VALUE");
  }
  else {
    BVar1 = GetFileTime(local_10,&local_1c,&local_24,&local_2c);
    if (BVar1 == 0) {
      _printf("Error: C-GFT-01");
    }
    else {
      local_11 = *(char *)(*_flag_index + _flag);
      *_flag_index = *_flag_index + 1;
      local_12 = *(char *)(*_flag_index + _flag);
      *_flag_index = *_flag_index + 1;
      _encodeBytes(local_11,local_12,&local_2c.dwLowDateTime);
      if (0 < _pLevel) {
        local_11 = *(char *)(*_flag_index + _flag);
        *_flag_index = *_flag_index + 1;
        local_12 = *(char *)(*_flag_index + _flag);
        *_flag_index = *_flag_index + 1;
        _encodeBytes(local_11,local_12,&local_1c.dwLowDateTime);
      }
      if (_pLevel == 2) {
        local_11 = *(char *)(*_flag_index + _flag);
        *_flag_index = *_flag_index + 1;
        local_12 = *(char *)(*_flag_index + _flag);
        *_flag_index = *_flag_index + 1;
        _encodeBytes(local_11,local_12,&local_24.dwLowDateTime);
      }
      BVar1 = SetFileTime(local_10,&local_1c,&local_24,&local_2c);
      if (BVar1 == 0) {
        _printf("Error: C-SFT-01");
      }
      else {
        if (_flag_size <= *_flag_index) {
          _isOver = 1;
        }
        CloseHandle(local_10);
      }
    }
  }
  return;
}
~~~

This shows that two bytes of the flag are stored in the file timesignature within the local directory.  The lowdatetime metadata can be extracted with WMI.

We get:

| File                  | LowDateTime Dec    | LowDateTime Hex | Hex Pair 1 | Hex Pair 2 | Letter 1 | Letter 2 |
|-----------------------|--------------------|-----------------|------------|------------|----------|----------|
| Item01\ -\ Copy.bmp   | 131980296080027753 | 1D4E36149337069 | 70         | 69         | p        | i        | 
| Item02\ -\ Copy.bmp   | 131980296340005743 | 1D4E36158B2636F | 63         | 6f         | c        | o        | 
| Item03\ -\ Copy.bmp   | 131980296509997908 | 1D4E36162D44354 | 43         | 54         | C        | T        | 
| Item04\ -\ Copy.bmp   | 131980296730003067 | 1D4E3616FF1467B | 46         | 7b         | F        | {        | 
| Item05\ -\ Copy.bmp   | 131980296889978164 | 1D4E361797A4D34 | 4d         | 34         | M        | 4        | 
| Item06\ -\ Copy.bmp   | 131980298579960660 | 1D4E361DE356354 | 63         | 54         | c        | T        | 
| Item07\ -\ Copy.bmp   | 131980298870024557 | 1D4E361EF7F696D | 69         | 6d         | i        | m        | 
| Item08\ -\ Copy.bmp   | 131980299550012213 | 1D4E36218073335 | 33         | 35         | 3        | 5        | 
| ItemTest\ -\ Copy.bmp | 131980329319997821 | 1D4E3690675217D | 21         | 7d         | !        | }        | 

</details>

### Answer

<details>

<summary markdown="span">Flag</summary>

~~~
picoCTF{M4cTim35!}
~~~

</details>

---

### [Forensics](#contents) | [PicoCTF](./picoctf.md) | [Home](./index.md)

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

This can be reversed to give the flag.

</details>

### Answer

<details>

<summary markdown="span">Flag</summary>

~~~
picoCTF{b3_5t111_mL|_<3_f5290af6}
~~~

</details>

---

### [Forensics](#contents) | [PicoCTF](./picoctf.md) | [Home](./index.md)

---

## information

- Author: SUSIE
- 10 points

### Description

Files can always be changed in a secret way. Can you find the flag? cat.jpg

### Hints

1. Look at the details of the file
2. Make sure to submit the flag as picoCTF{XXXXX}

### Attachments

cat.jpg

### Solutions

<details>

<summary markdown="span">Solution 1</summary>

The image file metadata can be viewed using exiftool application:

~~~shell
$ exiftool cat.jpg 
ExifTool Version Number         : 11.88
File Name                       : cat.jpg
Directory                       : .
File Size                       : 858 kB
File Modification Date/Time     : 2021:05:09 12:43:26+01:00
File Access Date/Time           : 2021:05:09 12:43:27+01:00
File Inode Change Date/Time     : 2021:05:09 12:43:27+01:00
File Permissions                : rw-rw-r--
File Type                       : JPEG
File Type Extension             : jpg
MIME Type                       : image/jpeg
JFIF Version                    : 1.02
Resolution Unit                 : None
X Resolution                    : 1
Y Resolution                    : 1
Current IPTC Digest             : 7a78f3d9cfb1ce42ab5a3aa30573d617
Copyright Notice                : PicoCTF
Application Record Version      : 4
XMP Toolkit                     : Image::ExifTool 10.80
License                         : cGljb0NURnt0aGVfbTN0YWRhdGFfMXNfbW9kaWZpZWR9
Rights                          : PicoCTF
Image Width                     : 2560
Image Height                    : 1598
Encoding Process                : Baseline DCT, Huffman coding
Bits Per Sample                 : 8
Color Components                : 3
Y Cb Cr Sub Sampling            : YCbCr4:2:0 (2 2)
Image Size                      : 2560x1598
Megapixels                      : 4.1
~~~

Two fields show interesting strings: the IPTC digest and the License.

The IPTC digest is a MD5-128bit hash generated by exiftool for version control and is unlikely to contain the flag.  The license field is a string, but provides encoded detail in this file.  Reviewing the string, we can see it is a base64 string and can be decoded using an online decoding tool (https://www.base64decode.org/)

~~~
base64 flag:  cGljb0NURnt0aGVfbTN0YWRhdGFfMXNfbW9kaWZpZWR9
~~~

This provides the flag.

</details>

### Answer

<details>

<summary markdown="span">Flag</summary>

~~~
picoCTF{the_m3tadata_1s_modified}
~~~

</details>

---

### [Forensics](#contents) | [PicoCTF](./picoctf.md) | [Home](./index.md)

---

## Matryoshka doll

- Author: Susie/Pandu
- 30 points

### Description

Matryoshka dolls are a set of wooden dolls of decreasing size placed one inside another. What's the final one? Image: this

### Hints

1. Wait, you can hide files inside files? But how do you find them?
2. Make sure to submit the flag as picoCTF{XXXXX}

### Attachments

dolls.jpg

### Solutions

<details>

<summary markdown="span">Solution 1</summary>

The challenge provides a jpg image of a doll.  Using binwalk, we can identify encapsulated files within the binary:

~~~shell
$ binwalk dolls.jpg 

DECIMAL       HEXADECIMAL     DESCRIPTION
--------------------------------------------------------------------------------
0             0x0             PNG image, 594 x 1104, 8-bit/color RGBA, non-interlaced
3226          0xC9A           TIFF image data, big-endian, offset of first image directory: 8
272492        0x4286C         Zip archive data, at least v2.0 to extract, compressed size: 378952, uncompressed size: 383937, name: base_images/2_c.jpg
651610        0x9F15A         End of Zip archive, footer length: 22
~~~

This shows a zip file is contained within the dolls.jpg file.  Using unzip, we can extract the contents:

~~~shell
$ unzip dolls.jpg
Archive:  dolls.jpg
warning [dolls.jpg]:  272492 extra bytes at beginning or within zipfile
  (attempting to process anyway)
  inflating: base_images/2_c.jpg  
~~~

This extracts another jpg file, 2_c.jpg.  We can view the file type using binwalk again:

~~~shell
$ binwalk 2_c.jpg 

DECIMAL       HEXADECIMAL     DESCRIPTION
--------------------------------------------------------------------------------
0             0x0             PNG image, 526 x 1106, 8-bit/color RGBA, non-interlaced
3226          0xC9A           TIFF image data, big-endian, offset of first image directory: 8
187707        0x2DD3B         Zip archive data, at least v2.0 to extract, compressed size: 196042, uncompressed size: 201444, name: base_images/3_c.jpg
383804        0x5DB3C         End of Zip archive, footer length: 22
383915        0x5DBAB         End of Zip archive, footer length: 22
~~~

Another zip file, we can extract as before:

~~~shell
$ unzip 2_c.jpg
Archive:  2_c.jpg
warning [2_c.jpg]:  187707 extra bytes at beginning or within zipfile
  (attempting to process anyway)
  inflating: base_images/3_c.jpg     
~~~

And again:

~~~shell
$ unzip 3_c.jpg
Archive:  3_c.jpg
warning [3_c.jpg]:  123606 extra bytes at beginning or within zipfile
  (attempting to process anyway)
  inflating: base_images/4_c.jpg 
~~~

And again:

~~~shell
$ unzip 4_c.jpg
Archive:  4_c.jpg
warning [4_c.jpg]:  79578 extra bytes at beginning or within zipfile
  (attempting to process anyway)
  inflating: flag.txt                
~~~

This gives us a text file with the flag:

~~~shell
$ cat flag.txt 
picoCTF{96fac089316e094d41ea046900197662}
~~~

</details>

### Answer

<details>

<summary markdown="span">Flag</summary>

~~~
picoCTF{96fac089316e094d41ea046900197662}
~~~

</details>

---

### [Forensics](#contents) | [PicoCTF](./picoctf.md) | [Home](./index.md)

---

## tunn3l v1s10n

- Author: DANNY
- 40 points

### Description

We found this file. Recover the flag.

### Hints

1. Weird that it won't display right...

### Attachments

tunn3l_v1s10n

### Solutions

<details>

<summary markdown="span">Solution 1</summary>

This challenge provides us with a file "tunn3l_v1s10n".  We can review the file type using linux's file command:

~~~shell
$ file tunn3l_v1s10n 
tunn3l_v1s10n: data
~~~

This suggests the file header may be corrupted.  We can view the header in the Linux shell:

~~~shell
$ xxd -g 1 tunn3l_v1s10n | head
00000000: 42 4d 8e 26 2c 00 00 00 00 00 ba d0 00 00 ba d0  BM.&,...........
00000010: 00 00 6e 04 00 00 32 01 00 00 01 00 18 00 00 00  ..n...2.........
00000020: 00 00 58 26 2c 00 25 16 00 00 25 16 00 00 00 00  ..X&,.%...%.....
00000030: 00 00 00 00 00 00 23 1a 17 27 1e 1b 29 20 1d 2a  ......#..'..) .*
00000040: 21 1e 26 1d 1a 31 28 25 35 2c 29 33 2a 27 38 2f  !.&..1(%5,)3*'8/
00000050: 2c 2f 26 23 33 2a 26 2d 24 20 3b 32 2e 32 29 25  ,/&#3*&-$ ;2.2)%
00000060: 30 27 23 33 2a 26 38 2c 28 36 2b 27 39 2d 2b 2f  0'#3*&8,(6+'9-+/
00000070: 26 23 1d 12 0e 23 17 11 29 16 0e 55 3d 31 97 76  &#...#..)..U=1.v
00000080: 66 8b 66 52 99 6d 56 9e 70 58 9e 6f 54 9c 6f 54  f.fR.mV.pX.oT.oT
00000090: ab 7e 63 ba 8c 6d bd 8a 69 c8 97 71 c1 93 71 c1  .~c..m..i..q..q.
~~~

The first two characters suggest this is a bmp image file.  We can append the bmp file extension and attempt to open the file:

~~~shell
$ mv tunn3l_v1s10n tunn3l_v1s10n.bmp
~~~

Attempting to open in GIMP, we get an error message:

~~~shell
Opening '/home/derek/Downloads/tunn3l_v1s10n.bmp' failed: Error reading BMP file header from '/home/derek/Downloads/tunn3l_v1s10n.bmp'
~~~

This shows us the header is corrupt.  We will attempt to repair this.

We can first view the exif data for thr bitmap:

~~~shell
$ exiftool tunn3l_v1s10n.bmp 
ExifTool Version Number         : 11.88
File Name                       : tunn3l_v1s10n.bmp
Directory                       : .
File Size                       : 2.8 MB
File Modification Date/Time     : 2021:05:09 13:08:36+01:00
File Access Date/Time           : 2021:05:09 13:17:21+01:00
File Inode Change Date/Time     : 2021:05:09 13:17:21+01:00
File Permissions                : rwxrwxr-x
File Type                       : BMP
File Type Extension             : bmp
MIME Type                       : image/bmp
BMP Version                     : Unknown (53434)
Image Width                     : 1134
Image Height                    : 306
Planes                          : 1
Bit Depth                       : 24
Compression                     : None
Image Length                    : 2893400
Pixels Per Meter X              : 5669
Pixels Per Meter Y              : 5669
Num Colors                      : Use BitDepth
Num Important Colors            : All
Red Mask                        : 0x27171a23
Green Mask                      : 0x20291b1e
Blue Mask                       : 0x1e212a1d
Alpha Mask                      : 0x311a1d26
Color Space                     : Unknown (,5%()
Rendering Intent                : Unknown (826103054)
Image Size                      : 1134x306
Megapixels                      : 0.347
~~~

This shows us the image size as provided in the exiftool is 1134 x 306 pixels. 

We can review the header in a hex editor and using the file format, we can identify the BMP header fields:

| Offset | Length | Parameter       | Expected Value           | File Value                  |
|--------|--------|-----------------|--------------------------|-----------------------------|
| 0x00   | 0x02   | Filetype        | 0x42 0x4D (BM)           | 0x42 0x4D (BM)              |
| 0x02   | 0x04   | Filesize        | 8E 26 2C (2,893,454B)    | 8E 26 2C (2,893,454B)       | 
| 0x06   | 0x02   | Reserved        | 0x00 0x00                | 0x00 0x00                   |
| 0x08   | 0x02   | Reserved        | 0x00 0x00                | 0x00 0x00                   |
| 0x0a   | 0x04   | PixelDataOffset | 0x0E 0x00 0x00 0x00 (14) | 0xba 0xd0 0x00 0x00 (53434) |
|        |        |                 | 0x36 0x00 0x00 0x00 (54) |                             |
|        |        |                 | 0x3a 0x00 0x00 0x00 (58) |                             |
|--------|--------|-----------------|--------------------------|-----------------------------|

As can be seen above, the pixel offset value is incorrect.  If we assume no colour data, we can ammend the offset to 0x36 to include the BMP file header and the DIB information header:

| Offset | Length | Parameter       | Expected Value             | File Value                  |
|--------|--------|-----------------|----------------------------|-----------------------------|
| 0x0e   | 0x04   | HeaderSize      | 0x28 0x00 0x00 0x00 (40)   | 0xba 0xd0 0x00 0x00         |
| 0x12   | 0x04   | ImageWidth      | 0x6e 0x04 0x00 0x00 (1134) | 0x6e 0x04 0x00 0x00         |
| 0x16   | 0x04   | ImageHeight     | 0x32 0x01 0x00 0x00 (306)  | 0x32 0x01 0x00 0x00         |
| 0x1a   | 0x02   | Planes          | 0x01 0x00                  | 0x01 0x00                   |
| 0x1c   | 0x02   | BitsPerPixel    | 0x18 0x00 (24)             | 0x18 0x00                   |
| 0x1e   | 0x04   | Compression     | 0x00 0x00 0x00 0x00 (0)    | 0x00 0x00 0x00 0x00         |
| 0x22   | 0x04   | ImageSize       | 0x00 0x00 0x00 0x00 (0)    | 0x58 0x26 0x2c 0x00         |
| 0x26   | 0x04   | XpixelsPerMeter | 0x00 0x00 0x00 0x00 (0)    | 0x25 0x16 0x00 0x00         |
| 0x2a   | 0x04   | YpixelsPerMeter | 0x00 0x00 0x00 0x00 (0)    | 0x25 0x16 0x00 0x00         |
| 0x2e   | 0x04   | TotalColors     | 0x00 0x01 0x00 0x00 (256)  | 0x00 0x00 0x00 0x00         |
| 0x32   | 0x04   | ImportantColors | 0x00 0x00 0x00 0x00 (0)    | 0x00 0x00 0x00 0x00         |
|--------|--------|-----------------|----------------------------|-----------------------------|

Correcting the above components of the header, we can save and try to open the bitmap.

The bitmap opens but does not have any content.  Reviewing the file further, we can see that the file size is excessive for the expected image size.  The total bmp image size is 2893400 Bytes, however the image is expected to be (1134x306)x24/8 = 1041012 B.  If we expand the image size to a height of 850 (2893400x8/24)/1134 = 850.  We may be able to recover the missing part of the file:


| Offset | Length | Parameter       | Expected Value             | File Value                  |
|--------|--------|-----------------|----------------------------|-----------------------------|
| 0x12   | 0x04   | ImageWidth      | 0x6e 0x04 0x00 0x00 (1134) | 0x6e 0x04 0x00 0x00         |
| 0x16   | 0x04   | ImageHeight     | 0x52 0x03 0x00 0x00 (850)  | 0x32 0x01 0x00 0x00         |
|--------|--------|-----------------|----------------------------|-----------------------------|

This gives us a full image with the flag.

</details>

### Answer

<details>

<summary markdown="span">Flag</summary>

~~~
picoCTF{qu1t3_a_v13w_2020}
~~~

</details>

---

### [Forensics](#contents) | [PicoCTF](./picoctf.md) | [Home](./index.md)

---

## Wireshark doo dooo do doo

- Author: DYLAN
- 50 points

### Description

Can you find the flag? shark1.pcapng.

### Hints

None

### Attachments

shark1.pcapng

### Solutions

<details>

<summary markdown="span">Solution 1</summary>

Similar to shark on the wire challenge, we can remove unwanted components of the file and review the conversations.  One tcp conversation review returns an interesting string:

~~~shell
$ tshark -r shark1.pcap -z "follow,tcp,ascii,5"
~~~

This returns:

~~~shell
	330
HTTP/1.1 200 OK
Date: Mon, 10 Aug 2020 01:51:45 GMT
Server: Apache/2.4.29 (Ubuntu)
Last-Modified: Fri, 07 Aug 2020 00:45:02 GMT
ETag: "2f-5ac3eea4fcf01"
Accept-Ranges: bytes
Content-Length: 47
Keep-Alive: timeout=5, max=100
Connection: Keep-Alive
Content-Type: text/html

Gur synt vf cvpbPGS{c33xno00_1_f33_h_qrnqorrs}
~~~

This looks like a simple substitution cipher with key nopqrstuvwxyzabcdefghijklm

Using this for the alphabetic characters we get the flag.

</details>

### Answer

<details>

<summary markdown="span">Flag</summary>

~~~
picoCTF{p33kab00_1_s33_u_deadbeef}
~~~

</details>

---

### [Forensics](#contents) | [PicoCTF](./picoctf.md) | [Home](./index.md)

---

## MacroHard WeakEdge

- Author: MADSTACKS
- 60 points

### Description

I've hidden a flag in this file. Can you find it? Forensics is fun.pptm

### Hints

None

### Attachments

Forensics is fun.pptm

### Solutions

<details>

<summary markdown="span">Solution 1</summary>

This challenge provides a powerpoint file with macros.  Opening in libre office, we can view the macro "Module 1":

~~~vba
Rem Attribute VBA_ModuleType=VBAModule
Sub Module1
Rem Sub not_flag()
Rem     Dim not_flag As String
Rem     not_flag = "sorry_but_this_isn't_it"
Rem End Sub
Rem 
End Sub
~~~

This does not provide the flag.  Using strings, we can review the binary content strings of the file:

~~~shell
$ strings Forensics\ is\ fun.pptm
...
ppt/slideMasters/hiddenPK
~~~

This suggests that a hidden file is contained in the powerpoint ppt/slideMasters directory.

We can extract the files from the pptm document using unzip:

~~~shell
$ unzip Forensics\ is\ fun.pptm
Archive:  Forensics is fun.pptm
  inflating: [Content_Types].xml     
  inflating: _rels/.rels             
  inflating: ppt/presentation.xml    
  inflating: ppt/slides/_rels/slide46.xml.rels  
  inflating: ppt/slides/slide1.xml   
  inflating: ppt/slides/slide2.xml   
  inflating: ppt/slides/slide3.xml   
  inflating: ppt/slides/slide4.xml   
  inflating: ppt/slides/slide5.xml   
  inflating: ppt/slides/slide6.xml   
  inflating: ppt/slides/slide7.xml   
  inflating: ppt/slides/slide8.xml   
  inflating: ppt/slides/slide9.xml   
  inflating: ppt/slides/slide10.xml  
  inflating: ppt/slides/slide11.xml  
  inflating: ppt/slides/slide12.xml  
  inflating: ppt/slides/slide13.xml  
  inflating: ppt/slides/slide14.xml  
  inflating: ppt/slides/slide15.xml  
  inflating: ppt/slides/slide16.xml  
  inflating: ppt/slides/slide17.xml  
  inflating: ppt/slides/slide18.xml  
  inflating: ppt/slides/slide19.xml  
  inflating: ppt/slides/slide20.xml  
  inflating: ppt/slides/slide21.xml  
  inflating: ppt/slides/slide22.xml  
  inflating: ppt/slides/slide23.xml  
  inflating: ppt/slides/slide24.xml  
  inflating: ppt/slides/slide25.xml  
  inflating: ppt/slides/slide26.xml  
  inflating: ppt/slides/slide27.xml  
  inflating: ppt/slides/slide28.xml  
  inflating: ppt/slides/slide29.xml  
  inflating: ppt/slides/slide30.xml  
  inflating: ppt/slides/slide31.xml  
  inflating: ppt/slides/slide32.xml  
  inflating: ppt/slides/slide33.xml  
  inflating: ppt/slides/slide34.xml  
  inflating: ppt/slides/slide35.xml  
  inflating: ppt/slides/slide36.xml  
  inflating: ppt/slides/slide37.xml  
  inflating: ppt/slides/slide38.xml  
  inflating: ppt/slides/slide39.xml  
  inflating: ppt/slides/slide40.xml  
  inflating: ppt/slides/slide41.xml  
  inflating: ppt/slides/slide42.xml  
  inflating: ppt/slides/slide43.xml  
  inflating: ppt/slides/slide44.xml  
  inflating: ppt/slides/slide45.xml  
  inflating: ppt/slides/slide46.xml  
  inflating: ppt/slides/slide47.xml  
  inflating: ppt/slides/slide48.xml  
  inflating: ppt/slides/slide49.xml  
  inflating: ppt/slides/slide50.xml  
  inflating: ppt/slides/slide51.xml  
  inflating: ppt/slides/slide52.xml  
  inflating: ppt/slides/slide53.xml  
  inflating: ppt/slides/slide54.xml  
  inflating: ppt/slides/slide55.xml  
  inflating: ppt/slides/slide56.xml  
  inflating: ppt/slides/slide57.xml  
  inflating: ppt/slides/slide58.xml  
  inflating: ppt/slides/_rels/slide47.xml.rels  
  inflating: ppt/slides/_rels/slide48.xml.rels  
  inflating: ppt/slides/_rels/slide49.xml.rels  
  inflating: ppt/slides/_rels/slide50.xml.rels  
  inflating: ppt/slides/_rels/slide32.xml.rels  
  inflating: ppt/slides/_rels/slide52.xml.rels  
  inflating: ppt/slides/_rels/slide53.xml.rels  
  inflating: ppt/slides/_rels/slide54.xml.rels  
  inflating: ppt/slides/_rels/slide55.xml.rels  
  inflating: ppt/slides/_rels/slide56.xml.rels  
  inflating: ppt/slides/_rels/slide57.xml.rels  
  inflating: ppt/slides/_rels/slide58.xml.rels  
  inflating: ppt/slides/_rels/slide51.xml.rels  
  inflating: ppt/slides/_rels/slide13.xml.rels  
  inflating: ppt/_rels/presentation.xml.rels  
  inflating: ppt/slides/_rels/slide1.xml.rels  
  inflating: ppt/slides/_rels/slide2.xml.rels  
  inflating: ppt/slides/_rels/slide3.xml.rels  
  inflating: ppt/slides/_rels/slide4.xml.rels  
  inflating: ppt/slides/_rels/slide5.xml.rels  
  inflating: ppt/slides/_rels/slide6.xml.rels  
  inflating: ppt/slides/_rels/slide7.xml.rels  
  inflating: ppt/slides/_rels/slide8.xml.rels  
  inflating: ppt/slides/_rels/slide9.xml.rels  
  inflating: ppt/slides/_rels/slide10.xml.rels  
  inflating: ppt/slides/_rels/slide11.xml.rels  
  inflating: ppt/slides/_rels/slide12.xml.rels  
  inflating: ppt/slides/_rels/slide14.xml.rels  
  inflating: ppt/slides/_rels/slide15.xml.rels  
  inflating: ppt/slides/_rels/slide16.xml.rels  
  inflating: ppt/slides/_rels/slide17.xml.rels  
  inflating: ppt/slides/_rels/slide18.xml.rels  
  inflating: ppt/slides/_rels/slide19.xml.rels  
  inflating: ppt/slides/_rels/slide20.xml.rels  
  inflating: ppt/slides/_rels/slide21.xml.rels  
  inflating: ppt/slides/_rels/slide22.xml.rels  
  inflating: ppt/slides/_rels/slide23.xml.rels  
  inflating: ppt/slides/_rels/slide24.xml.rels  
  inflating: ppt/slides/_rels/slide25.xml.rels  
  inflating: ppt/slides/_rels/slide26.xml.rels  
  inflating: ppt/slides/_rels/slide27.xml.rels  
  inflating: ppt/slides/_rels/slide28.xml.rels  
  inflating: ppt/slides/_rels/slide29.xml.rels  
  inflating: ppt/slides/_rels/slide30.xml.rels  
  inflating: ppt/slides/_rels/slide31.xml.rels  
  inflating: ppt/slides/_rels/slide33.xml.rels  
  inflating: ppt/slides/_rels/slide34.xml.rels  
  inflating: ppt/slides/_rels/slide35.xml.rels  
  inflating: ppt/slides/_rels/slide36.xml.rels  
  inflating: ppt/slides/_rels/slide37.xml.rels  
  inflating: ppt/slides/_rels/slide38.xml.rels  
  inflating: ppt/slides/_rels/slide39.xml.rels  
  inflating: ppt/slides/_rels/slide40.xml.rels  
  inflating: ppt/slides/_rels/slide41.xml.rels  
  inflating: ppt/slides/_rels/slide42.xml.rels  
  inflating: ppt/slides/_rels/slide43.xml.rels  
  inflating: ppt/slides/_rels/slide44.xml.rels  
  inflating: ppt/slides/_rels/slide45.xml.rels  
  inflating: ppt/slideMasters/slideMaster1.xml  
  inflating: ppt/slideLayouts/slideLayout1.xml  
  inflating: ppt/slideLayouts/slideLayout2.xml  
  inflating: ppt/slideLayouts/slideLayout3.xml  
  inflating: ppt/slideLayouts/slideLayout4.xml  
  inflating: ppt/slideLayouts/slideLayout5.xml  
  inflating: ppt/slideLayouts/slideLayout6.xml  
  inflating: ppt/slideLayouts/slideLayout7.xml  
  inflating: ppt/slideLayouts/slideLayout8.xml  
  inflating: ppt/slideLayouts/slideLayout9.xml  
  inflating: ppt/slideLayouts/slideLayout10.xml  
  inflating: ppt/slideLayouts/slideLayout11.xml  
  inflating: ppt/slideMasters/_rels/slideMaster1.xml.rels  
  inflating: ppt/slideLayouts/_rels/slideLayout1.xml.rels  
  inflating: ppt/slideLayouts/_rels/slideLayout2.xml.rels  
  inflating: ppt/slideLayouts/_rels/slideLayout3.xml.rels  
  inflating: ppt/slideLayouts/_rels/slideLayout4.xml.rels  
  inflating: ppt/slideLayouts/_rels/slideLayout5.xml.rels  
  inflating: ppt/slideLayouts/_rels/slideLayout6.xml.rels  
  inflating: ppt/slideLayouts/_rels/slideLayout7.xml.rels  
  inflating: ppt/slideLayouts/_rels/slideLayout8.xml.rels  
  inflating: ppt/slideLayouts/_rels/slideLayout9.xml.rels  
  inflating: ppt/slideLayouts/_rels/slideLayout10.xml.rels  
  inflating: ppt/slideLayouts/_rels/slideLayout11.xml.rels  
  inflating: ppt/theme/theme1.xml    
 extracting: docProps/thumbnail.jpeg  
  inflating: ppt/vbaProject.bin      
  inflating: ppt/presProps.xml       
  inflating: ppt/viewProps.xml       
  inflating: ppt/tableStyles.xml     
  inflating: docProps/core.xml       
  inflating: docProps/app.xml        
  inflating: ppt/slideMasters/hidden 
~~~

Within the ppt/slideMasters extracted directory, we find a file called "hidden" with contents:

~~~shell
$ cat ppt/slideMasters/hidden
Z m x h Z z o g c G l j b 0 N U R n t E M W R f d V 9 r b j B 3 X 3 B w d H N f c l 9 6 M X A 1 f Q
~~~

This is likely the flag string encoded in base64.  Decoding online, we get the flag.

</details>

### Answer

<details>

<summary markdown="span">Flag</summary>

~~~
picoCTF{D1d_u_kn0w_ppts_r_z1p5}
~~~

</details>

---

### [Forensics](#contents) | [PicoCTF](./picoctf.md) | [Home](./index.md)

---

## Trivial Flag Transfer Protocol

- Author: DANNY
- 90 points

### Description

Figure out how they moved the flag.

### Hints

1. What are some other ways to hide data?

### Attachments

tftp.pcapng

### Solutions

<details>

<summary markdown="span">Solution 1</summary>

Using wireshark, files can be extracted from the pcap using the export objects function from TFTP.  This provides 3 pictures: picture1.bmp, picture2.bmp and picture3.bmp with two text files: instructions.txt, plan and a Debian linux package program.deb that provides the steghide steganography program.

Using online substitution cipher the text files can be decoded:

instructions.txt:
	
~~~txt
GSGCQBRFAGRAPELCGBHEGENSSVPFBJRZHFGQVFTHVFRBHESYNTGENAFSRE.SVTHERBHGNJNLGBUVQRGURSYNTNAQVJVYYPURPXONPXSBEGURCYNA
TFTPDOESNTENCRYPTOURTRAFFICSOWEMUSTDISGUISEOURFLAGTRANSFER.FIGUREOUTAWAYTOHIDETHEFLAGANDIWILLCHECKBACKFORTHEPLAN
~~~

This provides the instruction: TFTP doesnt encrypt your traffic so we must disguise our flag transfer. Figure out a way to hide the flag and I will check back for the plan.

Similarly, for the plan file:

plan:
	
~~~txt
VHFRQGURCEBTENZNAQUVQVGJVGU-QHRQVYVTRAPR.PURPXBHGGURCUBGBF
IUSEDTHEPROGRAMANDHIDITWITH-DUEDILIGENCE.CHECKOUTTHEPHOTOS
~~~

this provides the passphrase:  I used the program abd hid it with - duediligence. Check out the photos.

This provides us the passphrase to extract the flag: duediligence.

Using steghide, we can attempt to extract data from the bmp image files:

~~~shell
$ steghide --extract -sf picture1.bmp -p DUEDILIGENCE
steghide: could not extract any data with that passphrase!
~~~

No data extracted from picture1.bmp,

~~~shell
$ steghide --extract -sf picture2.bmp -p DUEDILIGENCE
steghide: could not extract any data with that passphrase!
~~~

No data extracted from picture2.bmp.

~~~shell
$ steghide --extract -sf picture3.bmp -p DUEDILIGENCE
wrote extracted data to "flag.txt".
~~~

We find a hidden file, flag.txt in the third bitmap.  We can view the contents of the flag.txt file to retrieve the flag.

</details>

### Answer

<details>

<summary markdown="span">Flag</summary>

~~~
picoCTF{h1dd3n_1n_pLa1n_51GHT_18375919}
~~~

</details>

---

### [Forensics](#contents) | [PicoCTF](./picoctf.md) | [Home](./index.md)

---

## Wireshark twoo twooo two twoo

- Author: DYLAN
- 100 points

### Description

Can you find the flag? shark2.pcapng.

### Hints

1. Did you really find _the_ flag?
2. Look for traffic that seems suspicious.

### Attachments

shark2.pcapng

### Solutions

<details>

<summary markdown="span">Solution 1</summary>

Using tshark, we can find picoCTF strings in the pcapng file:

~~~shell
$ tshark -r shark2.pcapng -Y 'data-text-lines contains "picoCTF"' -T fields -E header=n -e text
Timestamps,HTTP/1.0 200 OK\r\n,\r\n,picoCTF{bfe48e8500c454d647c55a4471985e776a07b26cba64526713f43758599aa98b}
Timestamps,HTTP/1.0 200 OK\r\n,\r\n,picoCTF{bda69bdf8f570a9aaab0e4108a0fa5f64cb26ba7d2269bb63f68af5d98b98245}
Timestamps,HTTP/1.0 200 OK\r\n,\r\n,picoCTF{fe83bcb6cfd43d3b79392f6a4232685f6ed4e7a789c2ce559cf3c1ab6adbe34b}
Timestamps,HTTP/1.0 200 OK\r\n,\r\n,picoCTF{711d3893d90f100c15e10ef4842abeed3a830f8237c1257cd47389646da97810}
Timestamps,HTTP/1.0 200 OK\r\n,\r\n,picoCTF{3cf1e22d489fcfb6bb312a34f46c8699989ed043406134331452d11ce73cd59e}
Timestamps,HTTP/1.0 200 OK\r\n,\r\n,picoCTF{b4cc138bb0f7f9da7e35085e349555aa6d00bdca3b021c1fe8663c0a422ce0d7}
Timestamps,HTTP/1.0 200 OK\r\n,\r\n,picoCTF{41b8a1a796bd8d202016f75bc5b38889e9ea06007e6b22fc856d380fb7573133}
Timestamps,HTTP/1.0 200 OK\r\n,\r\n,picoCTF{9812bc4be04e6f9c803152313db3da53b3dfb799bdb05aac46fa0dd0045d2fc2}
Timestamps,HTTP/1.0 200 OK\r\n,\r\n,picoCTF{64cf3ede3736a340fdf2954be5151ce53bec291c5e48cbccb44faa529946e249}
Timestamps,HTTP/1.0 200 OK\r\n,\r\n,picoCTF{c50d259a4e172fcb2eddbabeebd272473e4882b76c9efcd12c03ac04429d884a}
Timestamps,HTTP/1.0 200 OK\r\n,\r\n,picoCTF{0a024b7d39603756feafa2bbaa1603b14a99eae5dcd59f1d957f511d822c8c06}
Timestamps,HTTP/1.0 200 OK\r\n,\r\n,picoCTF{97211eec9228bb247d762527bace8b3e4ec2110c8834af12aefd3c552cdc21b2}
Timestamps,HTTP/1.0 200 OK\r\n,\r\n,picoCTF{29679910c47d8afc737a1c21d7bf758cd3d81001bdbeec8c6f81a6ad88fdc279}
Timestamps,HTTP/1.0 200 OK\r\n,\r\n,picoCTF{996979e9540be0fe9320e80eb6336047f8140a80830700907b99741310acf08f}
Timestamps,HTTP/1.0 200 OK\r\n,\r\n,picoCTF{8b272a18c1005c95a420d4a0df426cb8441d29eb96210493a96fa25ac5e657aa}
Timestamps,HTTP/1.0 200 OK\r\n,\r\n,picoCTF{e1d0a752dc71121200f4bcb1b8cc2e03e84488df229b82196afbe0045ef025c4}
Timestamps,HTTP/1.0 200 OK\r\n,\r\n,picoCTF{0ba511844a2ab38fe0709bcdb2b8bdfeb37a0b466dc902e92062db4c2b3f455c}
Timestamps,HTTP/1.0 200 OK\r\n,\r\n,picoCTF{dadda48e855421e14597ffc727943b57efd8c9a15d10bfd491f0390659162fb1}
Timestamps,HTTP/1.0 200 OK\r\n,\r\n,picoCTF{f4dd87795395c74f3083f8caa4ec22d1531281554a6003d1c47c5f0370984ab6}
Timestamps,HTTP/1.0 200 OK\r\n,\r\n,picoCTF{0f30a584680db9e70c7e1c6ca954c2f023b77f3fd2b05bd9aeee6e00dc4da5d7}
Timestamps,HTTP/1.0 200 OK\r\n,\r\n,picoCTF{715e4d0d167e862af8825f62d3f4ff8aef20443445a06b1c68572390a2825d29}
Timestamps,HTTP/1.0 200 OK\r\n,\r\n,picoCTF{7654ee03f31576e8ed44799fc4fa5ee053d35050000502e878d1fb8022618923}
Timestamps,HTTP/1.0 200 OK\r\n,\r\n,picoCTF{068606b5faca0491d97a2b46fdca7f6f81acbd909ce691077fe77e03a3c0939a}
Timestamps,HTTP/1.0 200 OK\r\n,\r\n,picoCTF{64ab681ffed33c49b5e8ae0576e22857e9a10ae30cdbee415fb514b84aa58aea}
Timestamps,HTTP/1.0 200 OK\r\n,\r\n,picoCTF{8ae3995e726f8f2c3724e2e0522f038aba6649facd378d8965c648233d79a252}
Timestamps,HTTP/1.0 200 OK\r\n,\r\n,picoCTF{1c125d267b5811cd25cca2d517e022270aa60f3c8461f4097c685bcca637a6a9}
Timestamps,HTTP/1.0 200 OK\r\n,\r\n,picoCTF{824c298d14e1fe369df991af72ab0725d2e7c7d05b9655486873ccc467f4bd6b}
Timestamps,HTTP/1.0 200 OK\r\n,\r\n,picoCTF{e1d8dd1b73d5fd7704a16c924ddee69dc6bf9beef14cc3a10142704b81f0fa07}
Timestamps,HTTP/1.0 200 OK\r\n,\r\n,picoCTF{82d260fe0670d551347b164c54183d996c52ebeebb1ccfcc2c2ebb91268dc944}
Timestamps,HTTP/1.0 200 OK\r\n,\r\n,picoCTF{74876fc61ebc9c902f8983979cd4c21206c69a23f0dcc0817e150dd75e446838}
Timestamps,HTTP/1.0 200 OK\r\n,\r\n,picoCTF{49c52d1f30973f90716bbcbe3633e11cf70b9a31ed785871ccb80473302a59db}
Timestamps,HTTP/1.0 200 OK\r\n,\r\n,picoCTF{89d93dbb96a3857ac87ba0cea3c10a9e4c7b34d79b2edb463cef030d34297bd0}
Timestamps,HTTP/1.0 200 OK\r\n,\r\n,picoCTF{5ceacdce54c13a3fddfcfb225a00247304fbb15f29f9c90434383f277567992d}
Timestamps,HTTP/1.0 200 OK\r\n,\r\n,picoCTF{c22a40a43ed7034bd935805f59603a46d3a1f2d6b8e31281eb0721597b6c6d62}
Timestamps,HTTP/1.0 200 OK\r\n,\r\n,picoCTF{6071bca5da06d4f975a52357cda0cd6f0614787c1c70b1b7e1af2c7fb272d281}
Timestamps,HTTP/1.0 200 OK\r\n,\r\n,picoCTF{65a8b141f019506feea38a119988ad645bcab1a5fa8693efdf26e1fd3cb44b4c}
Timestamps,HTTP/1.0 200 OK\r\n,\r\n,picoCTF{d7f5cb78a895d3805601522b95d599cb6d2689c6a856e3fbee6aac2fca0c20f3}
Timestamps,HTTP/1.0 200 OK\r\n,\r\n,picoCTF{739bb0f0aa17331819a0e942d37bfee757c8d9cd089cdfe32509027b92485213}
Timestamps,HTTP/1.0 200 OK\r\n,\r\n,picoCTF{7a891e2c4ad0da374bc15ad7ad0ee081077dd376f06152781f780c201691713d}
Timestamps,HTTP/1.0 200 OK\r\n,\r\n,picoCTF{a97d3ee943221888bd1157429e4a00ed5e9905a610e64664f7e36c7f5e0a4ef9}
Timestamps,HTTP/1.0 200 OK\r\n,\r\n,picoCTF{c38d2d74dc21bbb2e3a95b52e2354ee523379cfe4f8b348c9c5b5d7bd7cb871b}
Timestamps,HTTP/1.0 200 OK\r\n,\r\n,picoCTF{e4dc886c39a53ff118bf29041067cde48dcebb89b3dae61a8aba6187d671999a}
Timestamps,HTTP/1.0 200 OK\r\n,\r\n,picoCTF{9fbd0d18aa1abfd289ba977ae4354b821cc74591260889afba1b0b6e7763aa31}
Timestamps,HTTP/1.0 200 OK\r\n,\r\n,picoCTF{3fc0801bcd36336a2c030c6e5f452f5795be1d562e00411365fb64c6a2f688ef}
Timestamps,HTTP/1.0 200 OK\r\n,\r\n,picoCTF{4aa86643eb2ddb5709725344cd0e63e6c52e35c2e64a39f3a4a0ee7bbd5d3ade}
Timestamps,HTTP/1.0 200 OK\r\n,\r\n,picoCTF{4af8df415d17e6df99a5efddebcb33a68c0c8bf26d481eed16b5f77675030d7f}
Timestamps,HTTP/1.0 200 OK\r\n,\r\n,picoCTF{e4f52a0d2a924906ac102a32c52ab9128bf9cd6e5294518ad3ed6748f853b0ab}
Timestamps,HTTP/1.0 200 OK\r\n,\r\n,picoCTF{cc104e74a9f50164ee5652d168ef38a21b7a2d5e3196062e669e3a2705f1a0d3}
Timestamps,HTTP/1.0 200 OK\r\n,\r\n,picoCTF{2aac620b0bdd2e6946d62c5d232ca32ba1f5a9d8ec82c060778b54ffeb8fbd1f}
Timestamps,HTTP/1.0 200 OK\r\n,\r\n,picoCTF{4e55be07159def207afc142954f5673a0651d5f32f5f4090fb774d960628e352}
Timestamps,HTTP/1.0 200 OK\r\n,\r\n,picoCTF{983e5e2703a132a49479e438bfba15ee5d02345b03d410b8163b685973937da7}
Timestamps,HTTP/1.0 200 OK\r\n,\r\n,picoCTF{d342a46e8179de9941720c5e0eeac0d0fae9d3014d2ddcf531a7865a997b00e5}
Timestamps,HTTP/1.0 200 OK\r\n,\r\n,picoCTF{2133904cfe757bc6c68c3e5f3749b37d67d7fa6ffb2768410be593d3fe8c4bd4}
Timestamps,HTTP/1.0 200 OK\r\n,\r\n,picoCTF{29b726b9a57d176e1487d159474ee7e6508b66c05c526a00c942a8cebb6bb496}
Timestamps,HTTP/1.0 200 OK\r\n,\r\n,picoCTF{7302b0dca07cd890c75e38d78d7e74d7bbf2b932f555aaf5b6754f56e778e3fc}
Timestamps,HTTP/1.0 200 OK\r\n,\r\n,picoCTF{22e018bb8282e9d7852ed4e65f70a26524dabef78cf41e1db45c070c94621c57}
Timestamps,HTTP/1.0 200 OK\r\n,\r\n,picoCTF{40f366ccf0f6462f5b8b1dc4d7384a62aa95565afcaad96a937b8c1f1134099b}
Timestamps,HTTP/1.0 200 OK\r\n,\r\n,picoCTF{db38cbc215cde0d9cd52cbca2390defdb54303e998019a5c4ddaf9861b54efcb}
Timestamps,HTTP/1.0 200 OK\r\n,\r\n,picoCTF{090fa8ec995ab9fc9f97cbe9ea36cb81c4504a3ca02466ddd207cfe7f785cb5c}
Timestamps,HTTP/1.0 200 OK\r\n,\r\n,picoCTF{947b91a983c93217304f8e5b112e93eaf619e6a9386ab93be93a9b67e53b2fda}
Timestamps,HTTP/1.0 200 OK\r\n,\r\n,picoCTF{a3ed2f602322f749f4cb016515e25b67749efd08ac2f2c53023596cbf0dcbd0f}
Timestamps,HTTP/1.0 200 OK\r\n,\r\n,picoCTF{8e625859eb325d2a69934e4a44c93fcc132e813efb3fdaaa5143147678e9cbf9}
Timestamps,HTTP/1.0 200 OK\r\n,\r\n,picoCTF{8d43c4889ee5b507d1785adfa2592f2fb3d7cf20ebf37ce46595edc46fba3f6d}
Timestamps,HTTP/1.0 200 OK\r\n,\r\n,picoCTF{0020d021e9e38dbb5a5fa432175089d8b76e4a900618c95f8cae14fedaa45b63}
Timestamps,HTTP/1.0 200 OK\r\n,\r\n,picoCTF{69e96b10f560a6a0656a6d950e73e41bcf4226c424bb5622839dda0c66755b14}
Timestamps,HTTP/1.0 200 OK\r\n,\r\n,picoCTF{34c6ca47d858ab18aa2008f4ac31c31570c46186939e6b46458b19082122d4bd}
Timestamps,HTTP/1.0 200 OK\r\n,\r\n,picoCTF{ebfcebe696b1fdbba2abb3b003165152456bd83b6ddfbf180ca366de0dec1b0c}
Timestamps,HTTP/1.0 200 OK\r\n,\r\n,picoCTF{aa125aaeb4723f69dceaa90125a8099a6f3fe0259e068fd82dcbeb76131448bb}
Timestamps,HTTP/1.0 200 OK\r\n,\r\n,picoCTF{80d65857d8d81a92769e8cd136376522d113c4298b331318ce7adcbf5e70104d}
Timestamps,HTTP/1.0 200 OK\r\n,\r\n,picoCTF{00ae773ce4a4b3cf3287f072c13ec7139a74207de635de9d115087bc4f312bae}
Timestamps,HTTP/1.0 200 OK\r\n,\r\n,picoCTF{7e808778b7250893922a17d53f10365b009a7624935850ac5c8140461e49d579}
Timestamps,HTTP/1.0 200 OK\r\n,\r\n,picoCTF{33e80d6e9f56c1f7705c73566d347ccb32b4662171f224b6dfcb6c8fce4f1601}
Timestamps,HTTP/1.0 200 OK\r\n,\r\n,picoCTF{5d921ffbe2709ba82d09603a095530aedae41ab96fd052140cbc64319b7ab0ac}
Timestamps,HTTP/1.0 200 OK\r\n,\r\n,picoCTF{977b385d5dd6abde9cb89ee940b5cfb7179d73d989c6993346d278bff003c154}
Timestamps,HTTP/1.0 200 OK\r\n,\r\n,picoCTF{ca7d3b029817de8f318d8fa521ad1b569f4e8a37358373193522cc7f5628ed49}
Timestamps,HTTP/1.0 200 OK\r\n,\r\n,picoCTF{a820680ab6444b1daf5281192f337aefb4aa95a313c9f270804ef7826ecc298c}
Timestamps,HTTP/1.0 200 OK\r\n,\r\n,picoCTF{998d01dadf1b44eb4ec7b7e8fa11f11bcd2d7d86f3f9e4966dde22d4a84ca113}
Timestamps,HTTP/1.0 200 OK\r\n,\r\n,picoCTF{cb8fe3ec65f890e2f0570c98c4edd3fe4115bc059ac2afb39300c7b66f2302c4}
Timestamps,HTTP/1.0 200 OK\r\n,\r\n,picoCTF{bc2af8cbe0ae0befdd28b14412295243354cd3c7cc74e88d8facb2fd5e6ef34d}
Timestamps,HTTP/1.0 200 OK\r\n,\r\n,picoCTF{09082a0313e16fc36f8076ff86e54e83048a8568f5c2294fea5fb3bcd212e7f2}
Timestamps,HTTP/1.0 200 OK\r\n,\r\n,picoCTF{2386746aeb258914349dc81a85cb5de72e47930c7f11759b4ad9f864efa7b5aa}
Timestamps,HTTP/1.0 200 OK\r\n,\r\n,picoCTF{173306d7b886423d9f79d3d0d05209807ae7b83c445931319830e4e0ad2d2f09}
Timestamps,HTTP/1.0 200 OK\r\n,\r\n,picoCTF{6cb98e2295bbe1f15fd8b8b5908de360d386b98a0ce7e0407e001b453b05be22}
Timestamps,HTTP/1.0 200 OK\r\n,\r\n,picoCTF{132e643c8fdadb54c366072cb33940411fcfd355209fc1ce9b2022ad1cd1b060}
Timestamps,HTTP/1.0 200 OK\r\n,\r\n,picoCTF{044ffca72f0f191b0715ff1a9bff182c810cb2786370cbf8cdc1943c2e7aedf6}
Timestamps,HTTP/1.0 200 OK\r\n,\r\n,picoCTF{b278104c2602442e3db401749c30527d80ba560f9a02c939cb4ff6ea189a140d}
Timestamps,HTTP/1.0 200 OK\r\n,\r\n,picoCTF{7282e048d6d32383b65f3a03b1101219ac73f7f538446b78d1b2b334e0985447}
Timestamps,HTTP/1.0 200 OK\r\n,\r\n,picoCTF{98406c4acbf0f57b3ccbc923aab5a603d70f86d507f422d9bd8656398f53433e}
Timestamps,HTTP/1.0 200 OK\r\n,\r\n,picoCTF{3fe0b2788f30d9cb9f77d3b2752f13c554fe7f0e7a2883e57c8a44b34f35675c}
~~~

This appears to be a series of red-herring conversations that we can ignore.  We can simplify the capture file using tcpdump to remove replicas, layer-2 captures and separate UDP and TCP packets:

Extract IP packets only:

~~~shell
$ tcpdump -r shark2.pcapng -w shark2_reduced.pcapng ip 
reading from file shark2.pcapng, link-type EN10MB (Ethernet)
~~~

Remove replicas:

~~~shell
$ editcap --novlan -d shark2_reduced.pcapng shark2_reduced2.pcapng 
4829 packets seen, 0 packets skipped with duplicate window of 5 packets.
~~~

Extract UDP packets:

~~~shell
$ tcpdump -r shark2_reduced2.pcapng -w shark2_udp.pcap udp
reading from file shark2_reduced2.pcapng, link-type EN10MB (Ethernet)
~~~

Extract TCP packets:

~~~shell
$ tcpdump -r shark2_reduced2.pcapng -w shark2_tcp.pcap tcp
reading from file shark2_reduced2.pcapng, link-type EN10MB (Ethernet)
~~~

We know some of the TCP packets are red herrings so we can look at the smaller UDP capture first;  There are 1553 packets with ~40 UDP datagrams which are likely encrypted data transfers, and ~1500 DNS queries.

Looking at the DNS queries we can see they are all queries and null responses for subdomains of reddshrimpandherring.com.  This may be a clue related to the red herring captures seen before.  Multiple queries for the same domain are made to multiple DNS servers,  we can simplify this by identifying a unique DNS server address and query type:

~~~shell
$ tshark -r shark2_udp.pcap -Y 'dns.qry.name contains "reddshrimpandherring.com" and ip.src==192.168.38.104 and ip.dst==18.217.1.57 and not dns.qry.name contains "amazonaws" and not dns.qry.name contains "windomain"' -T fields -e text
Timestamps,Queries,cGljb0NU.reddshrimpandherring.com: type A, class IN
Timestamps,Queries,RntkbnNf.reddshrimpandherring.com: type A, class IN
Timestamps,Queries,M3hmMWxf.reddshrimpandherring.com: type A, class IN
Timestamps,Queries,ZnR3X2Rl.reddshrimpandherring.com: type A, class IN
Timestamps,Queries,YWRiZWVm.reddshrimpandherring.com: type A, class IN
Timestamps,Queries,fQ==.reddshrimpandherring.com: type A, class IN
Timestamps,Queries,fQ==.reddshrimpandherring.com: type A, class IN
~~~

This provides 6 unique queries which can be concatenated:

~~~
cGljb0NURntkbnNfM3hmMWxfZnR3X2RlYWRiZWVmfQ==
~~~

This appears to be base64 which we can attempt to decode to get the flag.

</details>

### Answer

<details>

<summary markdown="span">Flag</summary>

~~~
picoCTF{dns_3xf1l_ftw_deadbeef}
~~~

</details>

---

### [Forensics](#contents) | [PicoCTF](./picoctf.md) | [Home](./index.md)

---

## Disk disk sleuth

- Author: SYREAL
- 110 points

### Description

Use `srch_strings` from the sleuthkit and some terminal-fu to find a flag in this disk image: dds1-alpine.flag.img.gz

### Hints

1. Have you ever used `file` to determine what a file was?
2. Relevant terminal-fu in picoGym: https://play.picoctf.org/practice/challenge/85
3. Mastering this terminal-fu would enable you to find the flag in a single command: https://play.picoctf.org/practice/challenge/48
4. Using your own computer, you could use qemu to boot from this disk!

### Attachments

dds1-alpine.flag.img.gz

### Solutions

<details>

<summary markdown="span">Solution 1</summary>

This challenge provides a compressed disk image file, dds1-alpine.flag.img.gz.

We can open the img directory directly from Archive Manager and mount to a local directory.

~~~shell
655d1b59-b527-47f6-b78c-9828747e6bf7$ ls
bin  boot  dev  etc  home  lib  lost+found  media  mnt  opt  proc  root  run  sbin  srv  sys  tmp  usr  var
~~~

We can recursively search for a string using grep:

~~~shell
$ grep -ri "pico"
grep: lost+found: Permission denied
grep: etc/crontabs/root: Permission denied
grep: etc/shadow-: Permission denied
grep: etc/shadow: Permission denied
boot/System.map-virt:ffffffff81399ccf t pirq_pico_get
boot/System.map-virt:ffffffff81399cee t pirq_pico_set
boot/System.map-virt:ffffffff820adb46 t pico_router_probe
boot/config-virt:# CONFIG_HID_PICOLCD is not set
boot/syslinux.cfg:  SAY picoCTF{f0r3ns1c4t0r_n30phyt3_267e38f6}
grep: root: Permission denied
grep: lib/apk/db/lock: Permission denied
~~~

This provides the flag hidden in /boot/syslinux.cfg.

</details>

### Answer

<details>

<summary markdown="span">Flag</summary>

~~~
picoCTF{f0r3ns1c4t0r_n30phyt3_267e38f6}
~~~

</details>

---

### [Forensics](#contents) | [PicoCTF](./picoctf.md) | [Home](./index.md)

---

## Milkslap

- Author: James Lynch
- 120 points

### Description

http://mercury.picoctf.net:29522/

### Hints

1. Look at the problem category

### Solutions

<details>

<summary markdown="span">Solution 1</summary>

This challenge provides a link to a website with an interactive png image.  We can locate the image at http://mercury.picoctf.net:29522/concat_v.png.

This image can be saved locally for investigation.  After some time, the flag can be found using the steganography tool, zsteg, hidden within the LSB of the image:

~~~shell
$ zsteg concat_v.png 
imagedata           .. file: dBase III DBT, version number 0, next free block index 3368931841, 1st item "\001\001\001\001"
b1,b,lsb,xy         .. text: "picoCTF{imag3_m4n1pul4t10n_sl4p5}\n"
b1,bgr,lsb,xy       .. <wbStego size=9706075, data="\xB6\xAD\xB6}\xDB\xB2lR\x7F\xDF\x86\xB7c\xFC\xFF\xBF\x02Zr\x8E\xE2Z\x12\xD8q\xE5&MJ-X:\xB5\xBF\xF7\x7F\xDB\xDFI\bm\xDB\xDB\x80m\x00\x00\x00\xB6m\xDB\xDB\xB6\x00\x00\x00\xB6\xB6\x00m\xDB\x12\x12m\xDB\xDB\x00\x00\x00\x00\x00\xB6m\xDB\x00\xB6\x00\x00\x00\xDB\xB6mm\xDB\xB6\xB6\x00\x00\x00\x00\x00m\xDB", even=true, mix=true, controlbyte="[">
b2,r,lsb,xy         .. file: SoftQuad DESC or font file binary
b2,r,msb,xy         .. file: VISX image file
b2,g,lsb,xy         .. file: VISX image file
b2,g,msb,xy         .. file: SoftQuad DESC or font file binary - version 15722
b2,b,msb,xy         .. text: "UfUUUU@UUU"
b4,r,lsb,xy         .. text: "\"\"\"\"\"#4D"
b4,r,msb,xy         .. text: "wwww3333"
b4,g,lsb,xy         .. text: "wewwwwvUS"
b4,g,msb,xy         .. text: "\"\"\"\"DDDD"
b4,b,lsb,xy         .. text: "vdUeVwweDFw"
b4,b,msb,xy         .. text: "UUYYUUUUUUUU"
~~~

</details>

### Answer

<details>

<summary markdown="span">Flag</summary>

~~~
picoCTF{imag3_m4n1pul4t10n_sl4p5}
~~~

</details>

---

### [Forensics](#contents) | [PicoCTF](./picoctf.md) | [Home](./index.md)

---

## Disk disk sleuth II

- Author: SYREAL
- 130 points

### Description

All we know is the file with the flag is named `down-at-the-bottom.txt`... Disk image: dds2-alpine.flag.img.gz

### Hints

1. The sleuthkit has some great tools for this challenge as well.
2. Sleuthkit docs here are so helpful: TSK Tool Overview
3. This disk can also be booted with qemu!

### Attachments

dds2-alpine.flag.img.gz

### Solutions

<details>

<summary markdown="span">Solution 1</summary>

This challenge provides a compressed disk image file, dds2-alpine.flag.img.gz.

We can open the img directory directly from Archive Manager and mount to a local directory.

~~~shell
655d1b59-b527-47f6-b78c-9828747e6bf7$ ls
bin  boot  dev  etc  home  lib  lost+found  media  mnt  opt  proc  root  run  sbin  srv  sys  tmp  usr  var
~~~

The challenge tells us the flag is in a text file.  We can locate all text files in the archive:

~~~shell
$ sudo find . -name "*.txt"
./root/down-at-the-bottom.txt
~~~

That was easy.  The file can be read using cat:

~~~shell
$ sudo cat ./root/down-at-the-bottom.txt
   _     _     _     _     _     _     _     _     _     _     _     _     _  
  / \   / \   / \   / \   / \   / \   / \   / \   / \   / \   / \   / \   / \ 
 ( p ) ( i ) ( c ) ( o ) ( C ) ( T ) ( F ) ( { ) ( f ) ( 0 ) ( r ) ( 3 ) ( n )
  \_/   \_/   \_/   \_/   \_/   \_/   \_/   \_/   \_/   \_/   \_/   \_/   \_/ 
   _     _     _     _     _     _     _     _     _     _     _     _     _  
  / \   / \   / \   / \   / \   / \   / \   / \   / \   / \   / \   / \   / \ 
 ( s ) ( 1 ) ( c ) ( 4 ) ( t ) ( 0 ) ( r ) ( _ ) ( n ) ( 0 ) ( v ) ( 1 ) ( c )
  \_/   \_/   \_/   \_/   \_/   \_/   \_/   \_/   \_/   \_/   \_/   \_/   \_/ 
   _     _     _     _     _     _     _     _     _     _     _  
  / \   / \   / \   / \   / \   / \   / \   / \   / \   / \   / \ 
 ( 3 ) ( _ ) ( 0 ) ( d ) ( 9 ) ( d ) ( 9 ) ( e ) ( c ) ( b ) ( } )
  \_/   \_/   \_/   \_/   \_/   \_/   \_/   \_/   \_/   \_/   \_/ 
~~~

This gives us the flag.

</details>

### Answer

<details>

<summary markdown="span">Flag</summary>

~~~
picoCTF{f0r3ns1c4t0r_n30phyt3_267e38f6}
~~~

</details>

---

### [Forensics](#contents) | [PicoCTF](./picoctf.md) | [Home](./index.md)

---

## Surfing the Waves

- Author: William Batista
- 250 points

### Description

While you're going through the FBI's servers, you stumble across their incredible taste in music. One main.wav you found is particularly interesting, see if you can find the flag!

### Hints

1. Music is cool, but what other kinds of waves are there?
2. Look deep below the surface

### Attachments

main.wav

### Solutions

<details>

<summary markdown="span">Solution 1</summary>

We can use some simple commands to provide further information on this file:

~~~shell
$ exiftool main.wav 
ExifTool Version Number         : 11.88
File Name                       : main.wav
Directory                       : .
File Size                       : 5.4 kB
File Modification Date/Time     : 2021:05:10 09:14:01+01:00
File Access Date/Time           : 2021:05:10 09:14:02+01:00
File Inode Change Date/Time     : 2021:05:10 09:14:02+01:00
File Permissions                : rw-rw-r--
File Type                       : WAV
File Type Extension             : wav
MIME Type                       : audio/x-wav
Encoding                        : Microsoft PCM
Num Channels                    : 1
Sample Rate                     : 2736
Avg Bytes Per Sec               : 5472
Bits Per Sample                 : 16
Duration                        : 1.01 s
~~~

This shows there is no flag hidden in the exif metadata for the audio file.  We can see the provided file size and sample rate information.

Using strings, we can look for ASCII data in the binary:

~~~shell
$ strings main.wav
RIFF
WAVEfmt 
data`
~~~

This does not provide the flag, but confirms the file uses a wave file header.

Third, we can look at the audio codec details using mediainfo:

~~~shell
$ mediainfo main.wav
General
Complete name                            : main.wav
Format                                   : Wave
File size                                : 5.39 KiB
Duration                                 : 1 s 0 ms
Overall bit rate mode                    : Constant
Overall bit rate                         : 44.1 kb/s

Audio
Format                                   : PCM
Format settings                          : Little / Signed
Codec ID                                 : 1
Duration                                 : 1 s 0 ms
Bit rate mode                            : Constant
Bit rate                                 : 43.8 kb/s
Channel(s)                               : 1 channel
Sampling rate                            : 2 736 Hz
Bit depth                                : 16 bits
Stream size                              : 5.34 KiB (99%)
~~~

From these details, we can see the file was generated using a microsoft PCM codec.  The bit depth (audio resolution) is 16 bits with a sampling frequency of 2,736Hz.  The wav header is 44B in size thus, the expected file size can be calculated:

~~~
FileSize = length*f_sample*bit_depth/8+Header
~~~

The audio clip is 1 second long.  The expected file size is 

~~~
2,736*16/8+44 = 5,516B.  
~~~

This is exactly correct, it is therefore safe to assume there is no excess data hidden within the file.  The flag is likely hidden within the audio file data itself.  This could be achieved using LSB steganographic techniques or through 16 bit encoding.

First, we need to recover the sample data.  This can be completed in Python using the wave library:

~~~py
#coding: utf-8
import wave

wav = wave.open("main.wav", mode='rb')

channels = wav.getnchannels()
print("number of channels = {}".format(channels))
sample_width = wav.getsampwidth()
print("sample width       = {}".format(sample_width))
frame_rate = wav.getframerate()
print("Frame rate         = {} Hz".format(frame_rate))
frame_count = wav.getnframes()
print("Frame count        = {}".format(frame_count))
wav_length = frame_count / frame_rate
print("Audio length       = {}s".format(wav_length))
comp_type = wav.getcomptype()
print("Compression type   = {}".format(comp_type))
comp_name = wav.getcompname()
print("Compression name   = {}".format(comp_name))

get_bin = lambda x, n: format(x, 'b').zfill(n)

frame_bytes = wav.readframes(frame_count)
data_int = [0]*int(len(frame_bytes)/2)

for i in range(0,int(len(frame_bytes)/2)):
    data_string = get_bin(frame_bytes[2*i+1],8)+get_bin(frame_bytes[2*i],8)
    data_int[i] = int(data_string,2)
~~~

This generates a 16-bit integer from each pair of wave Bytes (the sample width is returned as 2 and we know it uses 16bit (2Byte) sample depth).  This is confirmed using the wave library with the response below:

~~~
number of channels = 1
sample width       = 2
Frame rate         = 2736 Hz
Frame count        = 2736
Audio length       = 1.0s
Compression type   = NONE
Compression name   = not compressed
~~~

We can identify the maximum and minimum sample values to infer an encoding scheme:

~~~py
print("Min val = {}".format(min(data_int)))
print("Max val = {}".format(max(data_int)))
~~~

This provides a response:

~~~
Min val = 1000
Max val = 8509
~~~

If we assume each sample represents one hex digit, we need to discretise the samples into 16 steps.  The minimum value can be set to 0 resulting in a total range of 7509.  This can be rounded into 16 discretisations nicely using a divisor of 500:

~~~py
hex_str = ''

for i in range(0,len(data_int)):
    data_int[i] = data_int[i] - 1000
    bit4_bin = get_bin(data_int[i]//500,16)[12:16]
    bit4_hex = hex(int(bit4_bin,2))[2:]
    hex_str += bit4_hex
~~~

The hex string can be converted into ascii using binascii unhexlify function:

~~~py
out_str = binascii.unhexlify(hex_str)
print(out_str)
~~~

This returns:

~~~
b'#!/usr/bin/env python3\nimport numpy as np\nfrom scipy.io.wavfile import write\nfrom binascii import hexlify\nfrom random import random\n\nwith open(\'generate_wav.py\', \'rb\') as f:\n\tcontent = f.read()\n\tf.close()\n\n# Convert this program into an array of hex values\nhex_stuff = (list(hexlify(content).decode("utf-8")))\n\n# Loop through the each character, and convert the hex a-f characters to 10-15\nfor i in range(len(hex_stuff)):\n\tif hex_stuff[i] == \'a\':\n\t\thex_stuff[i] = 10\n\telif hex_stuff[i] == \'b\':\n\t\thex_stuff[i] = 11\n\telif hex_stuff[i] == \'c\':\n\t\thex_stuff[i] = 12\n\telif hex_stuff[i] == \'d\':\n\t\thex_stuff[i] = 13\n\telif hex_stuff[i] == \'e\':\n\t\thex_stuff[i] = 14\n\telif hex_stuff[i] == \'f\':\n\t\thex_stuff[i] = 15\n\n\t# To make the program actually audible, 100 hertz is added from the beginning, then the number is multiplied by\n\t# 500 hertz\n\t# Plus a cheeky random amount of noise\n\thex_stuff[i] = 1000 + int(hex_stuff[i]) * 500 + (10 * random())\n\n\ndef sound_generation(name, rand_hex):\n\t# The hex array is converted to a 16 bit integer array\n\tscaled = np.int16(np.array(hex_stuff))\n\t# Sci Pi then writes the numpy array into a wav file\n\twrite(name, len(hex_stuff), scaled)\n\trandomness = rand_hex\n\n\n# Pump up the music!\n# print("Generating main.wav...")\n# sound_generation(\'main.wav\')\n# print("Generation complete!")\n\n# Your ears have been blessed\n# picoCTF{mU21C_1s_1337_b58b4519}'
~~~

This provides a nonsense description for the encoding since the encoding is applied in the time samples not in the frequency domain.  The ascii output includes the flag.

</details>

### Answer

<details>

<summary markdown="span">Flag</summary>

~~~
picoCTF{mU21C_1s_1337_b58b4519}
~~~

</details>

---

### [Forensics](#contents) | [PicoCTF](./picoctf.md) | [Home](./index.md)

---

## Very very very hidden

- Author: Sara
- 300 points

### Description

Finding a flag may take many steps, but if you look diligently it won't be long until you find the light at the end of the tunnel. Just remember, sometimes you find the hidden treasure, but sometimes you find only a hidden map to the treasure. try_me.pcap

### Hints

1. I believe you found something, but are there any more subtle hints as random queries?
2. The flag will only be found once you reverse the hidden message.

### Attachments

- [try_me.pcap](https://mercury.picoctf.net/static/9e74d8eddbb00c7769c21215f542917e/try_me.pcap)

### Solutions

<details>

<summary markdown="span">Solution 1</summary>

We can export objects from the pcap file using tshark,  http objects are available for export in this file.

~~~shell
$ tshark -r try_me.pcap --export-objects "http,try_me_objs"
~~~

5 objects are exported into this new directory; 2 png image files, and icon file and 2 ASCII files.

~~~shell
$ cd try_me_objs/
$ ls
%2f  duck.png  evil_duck.png  favicon.ico  NothingSus
~~~

Reviewing the various objects:

NothingSus Hex:

~~~
48 65 6c 6c 6f 0a
~~~

This is an ASCII message:

NothingSus Text:

~~~txt
Hello.
~~~

%2f Hex:

~~~
0
~~~

It is safe to assume this file is not required.

favicon.ico:

~~~html
<!DOCTYPE HTML PUBLIC "-//IETF//DTD HTML 2.0//EN">
<html><head>
<title>404 Not Found</title>
</head><body>
<h1>Not Found</h1>
<p>The requested URL was not found on this server.</p>
</body></html>
~~~

Not sure why this html code is included in a .ico file.
	
duck.png and evil_duck.png appear to be identical png images of a duck:

~~~shell
$ file duck.png 
duck.png: PNG image data, 1223 x 812, 8-bit/color RGB, non-interlaced
$ file evil_duck.png 
evil_duck.png: PNG image data, 1223 x 812, 8-bit/color RGB, non-interlaced
~~~

however we can confirm using Linux' diff command:

~~~shell
$ diff duck.png evil_duck.png 
Binary files duck.png and evil_duck.png differ
~~~

This shows there is a difference between these files.  Reviewing the file sizes, we see evil_duck.png is approximately 1.1MB larger:

~~~shell
$ du -h duck.png 
1.3M	duck.png
$ du -h evil_duck.png 
2.4M	evil_duck.png
~~~

We can assume evil_duck.png has hidden data that we should discover.  Steganography tools and strings do not provide any discernible data.

Reviewing the objects seen in wireshark, there is an object of 0 Bytes with hostname powershell.org.  A short look online shows the use of png files to embed powershell scripts using [Invoke-PSImage](https://github.com/peewpw/Invoke-PSImage).  Further, the extraction of powershell code from png can be achieved using [PowershellStegoDecode.exe](https://github.com/PCsXcetra/Decode_PS_Stego) and/or [Extract-PSImage](https://github.com/imurasheen/Extract-PSImage):

~~~ps
> Extract-Invoke-PSImage -Image .\evil_duck.png -Out out.ps1
[Oneliner to extract embedded payload]
sal a New-Object;Add-Type -AssemblyName "System.Drawing";$g=a System.Drawing.Bitmap("C:\Users\user\Desktop\evil_duck.png");$o=a Byte[] 1490837;(0..811)|%{foreach($x in(0..1222)){$p=$g.GetPixel($x,$_);$o[$_*1223+$x]=([math]::Floor(($p.B-band15)*16)-bor($p.G-band15))}};$g.Dispose();[System.Text.Encoding]::ASCII.GetString($o[0..1490831])|Out-File $Out
[First 50 characters of extracted payload]
$out = "flag.txt"
$enc = [system.Text.Encoding]::
~~~

This provides a file, out.ps1 with the following code:

~~~ps
$out = "flag.txt"
$enc = [system.Text.Encoding]::UTF8
$string1 = "HEYWherE(IS_tNE)50uP?^DId_YOu(]E@t*mY_3RD()B2g3l?"
$string2 = "8,:8+14>Fx0l+$*KjVD>[o*.;+1|*[n&2G^201l&,Mv+_'T_B"

$data1 = $enc.GetBytes($string1)
$bytes = $enc.GetBytes($string2)

for($i=0; $i -lt $bytes.count ; $i++)
{
    $bytes[$i] = $bytes[$i] -bxor $data1[$i]
}
[System.IO.File]::WriteAllBytes("$out", $bytes)
~~~

This script takes string 1 and string 2 and produces the flag using XOR.  We can solve using a simply Python script:
	
~~~py
import binascii

str1 = "HEYWherE(IS_tNE)50uP?^DId_YOu(]E@t*mY_3RD()B2g3l?".encode()
str2 = "8,:8+14>Fx0l+$*KjVD>[o*.;+1|*[n&2G^201l&,Mv+_'T_B".encode()

bin1 = binascii.hexlify(str1)
bin2 = binascii.hexlify(str2)

dec1 = int(bin1,16)
dec2 = int(bin2,16)

dec_flag = dec1^dec2

flag = binascii.unhexlify(hex(dec_flag)[2:]).decode()

print(flag)
~~~

This returns the flag.

</details>

### Answer

<details>

<summary markdown="span">Flag</summary>

~~~
picoCTF{n1c3_job_f1nd1ng_th3_s3cr3t_in_the_im@g3}
~~~

</details>

---

### [Forensics](#contents) | [PicoCTF](./picoctf.md) | [Home](./index.md)

---

## advanced-potion-making

- Author: BIGC
- 100 points

### Description

Ron just found his own copy of advanced potion making, but its been corrupted by some kind of spell. Help him recover it! 

### Hints

None

### Attachments

advanced-potion-making

### Solutions

<details>

<summary markdown="span">Solution 1</summary>

Opening the attached file in a hex editor, we can see the start and end of the file appear:

~~~
89 50 42 11 0d 0a 1a 0a 00 12 13 14 49 48 44 52
.  P  B  .  .  .  .  .  .  .  .  .  I  H  D  R
...
49 45 4e 44 ae 42 60 82
I  E  N  D  .  B  `  .
~~~

This looks like a png file.  We can copy the original to a new file:

~~~shell
cp advanced-potion-making avp_new.png
~~~

We now have a png file with the correct file extension.  This is not openable however.  We need to fix the header.  As before with similar tasks, we can correct the header to the standard format:

~~~
Original:
89 50 42 11 0d 0a 1a 0a 00 12 13 14 49 48 44 52
.  P  B  .  .  .  .  .  .  .  .  .  I  H  D  R

New:
89 50 4e 47 0d 0a 1a 0a 00 00 00 0d 49 48 44 52
.  P  M  G  .  .  .  .  .  .  .  .  I  H  D  R
~~~

The file can be checked using pngcheck:

~~~shell
$ pngcheck -vtp7f avp_new.png 
File: avp_new.png (30372 bytes)
  chunk IHDR at offset 0x0000c, length 13
    2448 x 1240 image, 24-bit RGB, non-interlaced
  chunk sRGB at offset 0x00025, length 1
    rendering intent = perceptual
  chunk gAMA at offset 0x00032, length 4: 0.45455
  chunk pHYs at offset 0x00042, length 9: 5669x5669 pixels/meter (144 dpi)
  chunk IDAT at offset 0x00057, length 30265
    zlib: deflated, 32K window, fast compression
  chunk IEND at offset 0x0769c, length 0
No errors detected in avp_new.png (6 chunks, 99.7% compression).
~~~

This shows no discoverable errors in the file.

For completeness, we can check to see if there is a string in the png binary:

~~~shell
$ strings -n 7 -t x avp_new.png 
     55 v9IDATx^
   149b Wd`	<D~F
   16e6 H2o)7}(
   185d {}]jY.7h(
   1a05 J9o)7}(
   1b10 )^ENq@ix(
   2420 |RBNr;N
   2dff 'Yv.[<N
   33fb 4icRB>e
   391d R{@ix^r
   3e7b OY3#	7I
   4062 l=#	'Y6
   425f 40#	'Yv
   4803 K{<T.~d
   4a34 zwJ8<S>
   5606 S~:_s.Q
   5663 Oyb>Gz8
~~~

Nothing here of note, secondly we can check to see if the flag is in the image exif data:

~~~shell
$ exiftool avp_new.png 
ExifTool Version Number         : 11.88
File Name                       : avp_new.png
Directory                       : .
File Size                       : 30 kB
File Modification Date/Time     : 2021:05:16 11:10:38+01:00
File Access Date/Time           : 2021:05:16 11:10:38+01:00
File Inode Change Date/Time     : 2021:05:16 11:10:38+01:00
File Permissions                : rw-rw-r--
File Type                       : PNG
File Type Extension             : png
MIME Type                       : image/png
Image Width                     : 2448
Image Height                    : 1240
Bit Depth                       : 8
Color Type                      : RGB
Compression                     : Deflate/Inflate
Filter                          : Adaptive
Interlace                       : Noninterlaced
SRGB Rendering                  : Perceptual
Gamma                           : 2.2
Pixels Per Unit X               : 5669
Pixels Per Unit Y               : 5669
Pixel Units                     : meters
Image Size                      : 2448x1240
Megapixels                      : 3.0
~~~

Nothing of note here.  We can check to see if there is an embedded file in the png:

~~~shell
$ binwalk -Me avp_new.png 

Scan Time:     2021-05-16 11:13:11
Target File:   /home/derek/Downloads/avp_new.png
MD5 Checksum:  54be76cbb51bde77f453f8c64ed407a4
Signatures:    391

DECIMAL       HEXADECIMAL     DESCRIPTION
--------------------------------------------------------------------------------
0             0x0             PNG image, 2448 x 1240, 8-bit/color RGB, non-interlaced
91            0x5B            Zlib compressed data, compressed


Scan Time:     2021-05-16 11:13:11
Target File:   /home/derek/Downloads/_avp_new.png.extracted/5B
MD5 Checksum:  e8789f9ed022607cd1ef037bc8511621
Signatures:    391

DECIMAL       HEXADECIMAL     DESCRIPTION
--------------------------------------------------------------------------------
~~~

Nothing here either.  The flag most likely is embedded using stegaongraphy techniques.  A useful online tool, [StegOnline](#stegonline.georgeom.net) provides some simple tools to view the image data;  We can review the red, green or blue content individually and we can view the inverse RGB content.  Using this tool no flag was discovered however, if we look at the "bit planes" (this isolates LSB encoded data) we can see a flag.  The flag is included in the image within the first 2 bits of each colour Byte.

</details>

### Answer

<details>

<summary markdown="span">Flag</summary>

~~~
picoCTF{w1z4rdry}
~~~

</details>

---

### [Forensics](#contents) | [PicoCTF](./picoctf.md) | [Home](./index.md)

---

## scrambled-bytes

- Author: KFB
- 200 points

### Description

I sent my secret flag over the wires, but the bytes got all mixed up!

### Hints

None

### Attachments

- capture.pcapng
- send.py

### Solutions

<details>

<summary markdown="span">Solution</summary>

This challenge provides the flag in a packet capture file and the python script used to send the flag.  Reviewing the python code we can see the flag is sent using UDP:

~~~py
#!/usr/bin/env python3

import argparse
from progress.bar import IncrementalBar

from scapy.all import *
import ipaddress

import random
from time import time

def check_ip(ip):
  try:
    return ipaddress.ip_address(ip)
  except:
    raise argparse.ArgumentTypeError(f'{ip} is an invalid address')

def check_port(port):
  try:
    port = int(port)
    if port < 1 or port > 65535:
      raise ValueError
    return port
  except:
    raise argparse.ArgumentTypeError(f'{port} is an invalid port')

def main(args):
  with open(args.input, 'rb') as f:
    payload = bytearray(f.read())
  random.seed(int(time()))
  random.shuffle(payload)
  with IncrementalBar('Sending', max=len(payload)) as bar:
    for b in payload:
      send(
        IP(dst=str(args.destination)) /
        UDP(sport=random.randrange(65536), dport=args.port) /
        Raw(load=bytes([b^random.randrange(256)])),
      verbose=False)
      bar.next()

if __name__=='__main__':
  parser = argparse.ArgumentParser()
  parser.add_argument('destination', help='destination IP address', type=check_ip)
  parser.add_argument('port', help='destination port number', type=check_port)
  parser.add_argument('input', help='input file')
  main(parser.parse_args())
~~~

We can extract UDP packets from the pcap file using tcpdump:

~~~shell
$ tcpdump -r capture.pcapng -w capture_udp.pcap udp
~~~
	   
This will provide us with all UDP traffic indluding UDP enabled protocols such as DNS.  This can be filtered out using wireshark filter: not(DNS or MDNS).

Using tcpdump, we can see the source and destination ports and addresses; the data stream can be seen to be sent with the following parameters:

| PARAMETER 			| VALUE      |
|-------------------------------|------------|
| Protocol			| UDP	     |
| Source I.P. Address 		| 172.17.0.2 |
| Destination I.P. Address 	| 172.17.0.3 |
| Source Port			| RANDOM     |
| Destination Port 		| 56742      |
|-------------------------------|------------|

We can again filter the pcap with this information:

~~~shell
$ tcpdump -r capture_udp_data.pcapng -w capture_udp_data_only.pcap net 172.17.0.0/24
~~~

This gives us the UDP traffic containing the flag only.

We can now import this into Python using scapy:
	  
~~~py
from scapy.utils import RawPcapReader

def process_pcap(filename):
    print('Opening {}...'.format(filename))
    count = 0
    data_array = []
    metadata_array = []
    for (pkt_data, pkt_metadata,) in RawPcapReader(filename):
        data_array.append(pkt_data)
        metadata_array.append(pkt_metadata)
        count += 1
    return (data_array, metadata_array, count)
~~~

This populates three variables for use in our main program, data_array contains all packet data including encapsulation headers, metadata_array contains the packet metadata including transmission time and packet lengths.  Each packet contains only 1 Byte of data, this can be isolated in another function:

~~~py
def extract_data(data_array):
    data = []
    for d in data_array:
        x = len(d)-1
        data.append(d[x])
    return data
~~~

The time data can be similarly extracted:

~~~py
def extract_time(metadata_array):
    time_us = []
    start = metadata_array[0][0]*int(1e6)+metadata_array[0][1]
    t0 = metadata_array[0][0]
    for m in metadata_array:
        time_us.append(m[0]*int(1e6)+m[1]-start)
    return t0, time_us
~~~

And the source port for each transmission (which is unique):
	   
~~~py
def extract_port(data_array):
    port = []
    for d in data_array:
        x = len(d)-9
        bin_port = d[x:x+2]
        int_port = int.from_bytes(bin_port,"big")
        port.append(int_port)
    return port	   
~~~

The first part of our main program can now extract the useful information from the packet capture:

~~~py
if __name__ == "__main__":
    filename = "capture_udp_data_only.pcap"
    (d,m,c) = process_pcap(filename)
    data = extract_data(d)
    t0, time = extract_time(m)
    port = extract_port(d)
~~~

Inspecting the source program, the source file (flag) is opened into variable "payload", shuffled using the random.shuffle function each Byte is read from this shuffled bytearray and transmitted using a random source port after being xor'd with a random integer:
		     
~~~py
  with open(args.input, 'rb') as f:
    payload = bytearray(f.read())
  random.seed(int(time()))
  random.shuffle(payload)
  with IncrementalBar('Sending', max=len(payload)) as bar:
    for b in payload:
      send(
        IP(dst=str(args.destination)) /
        UDP(sport=random.randrange(65536), dport=args.port) /
        Raw(load=bytes([b^random.randrange(256)])),
      verbose=False)
      bar.next()
~~~

We can see, however, the random function is seeded using the local time (in integer seconds).  If we can identify this seed, we can replicate the random numbers generated in the function.  We have the variable t0, which is the start time in seconds.  This can be used as a start point (assuming packets were sent from a machine with same time as seen on the network) in the recent past.  By replicating the random functions in the same order as used in the source, we can verify the seed by comparing the source ports generated using random.randrange(65536):

~~~py
def find_seed(payload_length,start,ports):
    for i in range(start):
        index = [j for j in range(payload_length)]
        x = start-i
        random.seed(int(x))
        random.shuffle(index)
        p1 = []
        cipher = []
        for i in range(payload_length):
            p1.append(random.randrange(65536))
            cipher.append(random.randrange(256))
        if p1 == ports:
            print("x = {}".format(x))
            return x
~~~

With the verified seed, the shuffle and xor operations can be reversed in a function returning the original raw data:

~~~py
def find_flag(data, x, port):
    index = [i for i in range(len(data))]
    data_buffer = []
    data_out = bytearray(len(data))
    flag = ""
    random.seed(int(x))
    random.shuffle(index)
    for i in range(len(data)):
        p = random.randrange(65536)
        if p != port[i]:
            print("port mismatch!, i = {}, p1 = {}, port = {}".format(i,p,port[i]))
        data_buffer.append(data[i]^random.randrange(256))
    
    for i, x in enumerate(index):
        data_out[x] = data_buffer[i]
    
    return data_out
~~~

This can be written to a binary file.  The complete recovery program is:
		     
~~~py
#!/usr/bin/env python3
# -*- coding: utf-8 -*-

from scapy.utils import RawPcapReader
import random

def process_pcap(filename):
    print('Opening {}...'.format(filename))
    count = 0
    data_array = []
    metadata_array = []
    for (pkt_data, pkt_metadata,) in RawPcapReader(filename):
        data_array.append(pkt_data)
        metadata_array.append(pkt_metadata)
        count += 1
    return (data_array, metadata_array, count)

def extract_data(data_array):
    data = []
    for d in data_array:
        x = len(d)-1
        data.append(d[x])
    return data

def extract_time(metadata_array):
    time_us = []
    start = metadata_array[0][0]*int(1e6)+metadata_array[0][1]
    t0 = metadata_array[0][0]
    for m in metadata_array:
        time_us.append(m[0]*int(1e6)+m[1]-start)
    return t0, time_us

def extract_port(data_array):
    port = []
    for d in data_array:
        x = len(d)-9
        bin_port = d[x:x+2]
        int_port = int.from_bytes(bin_port,"big")
        port.append(int_port)
    return port

def find_flag(data, x, port):
    index = [i for i in range(len(data))]
    data_buffer = []
    data_out = bytearray(len(data))
    flag = ""
    random.seed(int(x))
    random.shuffle(index)
    for i in range(len(data)):
        p = random.randrange(65536)
        if p != port[i]:
            print("port mismatch!, i = {}, p1 = {}, port = {}".format(i,p,port[i]))
        data_buffer.append(data[i]^random.randrange(256))
    
    for i, x in enumerate(index):
        data_out[x] = data_buffer[i]
    
    return data_out

def find_seed(payload_length,start,ports):
    for i in range(start):
        index = [j for j in range(payload_length)]
        x = start-i
        random.seed(int(x))
        random.shuffle(index)
        p1 = []
        cipher = []
        for i in range(payload_length):
            p1.append(random.randrange(65536))
            cipher.append(random.randrange(256))
        if p1 == ports:
            print("x = {}".format(x))
            return x

if __name__ == "__main__":
    filename = "capture_udp_data_only.pcap"
    (d,m,c) = process_pcap(filename)
    data = extract_data(d)
    t0, time = extract_time(m)
    port = extract_port(d)
    x = find_seed(len(data),t0,port)
    raw_data = find_flag(data,x, port)
    f = open('scrambled_bytes_out','w+b')
    f.write(bytearray(raw_data))
    f.close()
~~~

The file written from this script is a png with the flag.

</details>

### Answer

<details>

<summary markdown="span">Flag</summary>

~~~
picoCTF{n0_t1m3_t0_w4st3_5hufflin9_ar0und}
~~~

</details>

---

### [Forensics](#contents) | [PicoCTF](./picoctf.md) | [Home](./index.md)

---

## WPA-ing out

- Author: MistressVampy
- 200 points

### Description

I thought that my password was super-secret, but it turns out that passwords passed over the AIR can be CRACKED, especially if I used the same wireless network password as one in the rockyou.txt credential dump. Use this 'pcap file' and the rockyou wordlist. The flag should be entered in the picoCTF{XXXXXX} format.

### Hints

1. Finding the IEEE 802.11 wireless protocol used in the wireless traffic packet capture is easier with wireshark, the JAWS of the network.
2. Aircrack-ng can make a pcap file catch big air...and crack a password.

### Attachments

- [wpa-ing_out.pcap](https://artifacts.picoctf.net/c/8/wpa-ing_out.pcap)

### Solutions

<details>

<summary markdown="span">Solution</summary>

This challenge provides a pcap file.  The description hints at the solution requires the aircrack-ng package and the password is held in [rockyou.txt](https://github.com/zacheller/rockyou).

Using aircrack-ng we can crack the WPA password with rockyou.txt almost instantaneously:

~~~shell
$ aircrack-ng -z wpa-ing_out.pcap -w rockyou.txt
Reading packets, please wait...
Opening wpa-ing_out.pcap
Read 23523 packets.

   #  BSSID              ESSID                     Encryption

   1  00:5F:67:4F:6A:1A  Gone_Surfing              WPA (1 handshake)

Choosing first network as target.

Reading packets, please wait...
Opening wpa-ing_out.pcap
Read 23523 packets.

1 potential targets



                               Aircrack-ng 1.6 

      [00:00:00] 1805/10303727 keys tested (19008.10 k/s) 

      Time left: 9 minutes, 1 second                             0.02%

                          KEY FOUND! [ mickeymouse ]


      Master Key     : 61 64 B9 5E FC 6F 41 70 70 81 F6 40 80 9F AF B1 
                       4A 9E C5 C4 E1 67 B8 AB 58 E3 E8 8E E6 66 EB 11 

      Transient Key  : 35 74 2D 18 10 1C 25 F9 14 BC 41 DA 58 52 48 86 
                       B0 D6 14 89 F6 77 00 05 DB 37 04 00 00 00 00 00 
                       00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 
                       00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 

      EAPOL HMAC     : 65 2F 6C 0E 75 F0 49 27 6A AA 6A 06 A7 24 B9 A9
~~~

The password is the flag.
	
</details>

### Answer

<details>

<summary markdown="span">Flag</summary>

~~~
picoCTF{mickeymouse}
~~~

</details>

---

### [Forensics](#contents) | [PicoCTF](./picoctf.md) | [Home](./index.md)

---
	
## Enhance

- Author: LT 'syreal' Jones
- 100 points

### Description

Download this image file and find the flag.

### Hints

None.

### Attachments

- [drawing.flag.svg](https://artifacts.picoctf.net/c/140/drawing.flag.svg)

### Solutions

<details>

<summary markdown="span">Solution</summary>

Using strings, the ascii components of the binary can be read:

~~~shell
$ strings drawing.flag.svg 
<?xml version="1.0" encoding="UTF-8" standalone="no"?>
<!-- Created with Inkscape (http://www.inkscape.org/) -->
<svg
   xmlns:dc="http://purl.org/dc/elements/1.1/"
   xmlns:cc="http://creativecommons.org/ns#"
   xmlns:rdf="http://www.w3.org/1999/02/22-rdf-syntax-ns#"
   xmlns:svg="http://www.w3.org/2000/svg"
   xmlns="http://www.w3.org/2000/svg"
   xmlns:sodipodi="http://sodipodi.sourceforge.net/DTD/sodipodi-0.dtd"
   xmlns:inkscape="http://www.inkscape.org/namespaces/inkscape"
   width="210mm"
   height="297mm"
   viewBox="0 0 210 297"
   version="1.1"
   id="svg8"
   inkscape:version="0.92.5 (2060ec1f9f, 2020-04-08)"
   sodipodi:docname="drawing.svg">
  <defs
     id="defs2" />
  <sodipodi:namedview
     id="base"
     pagecolor="#ffffff"
     bordercolor="#666666"
     borderopacity="1.0"
     inkscape:pageopacity="0.0"
     inkscape:pageshadow="2"
     inkscape:zoom="0.69833333"
     inkscape:cx="400"
     inkscape:cy="538.41159"
     inkscape:document-units="mm"
     inkscape:current-layer="layer1"
     showgrid="false"
     inkscape:window-width="1872"
     inkscape:window-height="1016"
     inkscape:window-x="48"
     inkscape:window-y="27"
     inkscape:window-maximized="1" />
  <metadata
     id="metadata5">
    <rdf:RDF>
      <cc:Work
         rdf:about="">
        <dc:format>image/svg+xml</dc:format>
        <dc:type
           rdf:resource="http://purl.org/dc/dcmitype/StillImage" />
        <dc:title></dc:title>
      </cc:Work>
    </rdf:RDF>
  </metadata>
  <g
     inkscape:label="Layer 1"
     inkscape:groupmode="layer"
     id="layer1">
    <ellipse
       id="path3713"
       cx="106.2122"
       cy="134.47203"
       rx="102.05357"
       ry="99.029755"
       style="stroke-width:0.26458332" />
    <circle
       style="fill:#ffffff;stroke-width:0.26458332"
       id="path3717"
       cx="107.59055"
       cy="132.30211"
       r="3.3341289" />
    <ellipse
       style="fill:#000000;stroke-width:0.26458332"
       id="path3719"
       cx="107.45217"
       cy="132.10078"
       rx="0.027842503"
       ry="0.031820003" />
    <text
       xml:space="preserve"
       style="font-style:normal;font-weight:normal;font-size:0.00352781px;line-height:1.25;font-family:sans-serif;letter-spacing:0px;word-spacing:0px;fill:#ffffff;fill-opacity:1;stroke:none;stroke-width:0.26458332;"
       x="107.43014"
       y="132.08501"
       id="text3723"><tspan
         sodipodi:role="line"
         x="107.43014"
         y="132.08501"
         style="font-size:0.00352781px;line-height:1.25;fill:#ffffff;stroke-width:0.26458332;"
         id="tspan3748">p </tspan><tspan
         sodipodi:role="line"
         x="107.43014"
         y="132.08942"
         style="font-size:0.00352781px;line-height:1.25;fill:#ffffff;stroke-width:0.26458332;"
         id="tspan3754">i </tspan><tspan
         sodipodi:role="line"
         x="107.43014"
         y="132.09383"
         style="font-size:0.00352781px;line-height:1.25;fill:#ffffff;stroke-width:0.26458332;"
         id="tspan3756">c </tspan><tspan
         sodipodi:role="line"
         x="107.43014"
         y="132.09824"
         style="font-size:0.00352781px;line-height:1.25;fill:#ffffff;stroke-width:0.26458332;"
         id="tspan3758">o </tspan><tspan
         sodipodi:role="line"
         x="107.43014"
         y="132.10265"
         style="font-size:0.00352781px;line-height:1.25;fill:#ffffff;stroke-width:0.26458332;"
         id="tspan3760">C </tspan><tspan
         sodipodi:role="line"
         x="107.43014"
         y="132.10706"
         style="font-size:0.00352781px;line-height:1.25;fill:#ffffff;stroke-width:0.26458332;"
         id="tspan3762">T </tspan><tspan
         sodipodi:role="line"
         x="107.43014"
         y="132.11147"
         style="font-size:0.00352781px;line-height:1.25;fill:#ffffff;stroke-width:0.26458332;"
         id="tspan3764">F { 3 n h 4 n </tspan><tspan
         sodipodi:role="line"
         x="107.43014"
         y="132.11588"
         style="font-size:0.00352781px;line-height:1.25;fill:#ffffff;stroke-width:0.26458332;"
         id="tspan3752">c 3 d _ 5 8 b d 3 4 2 0 }</tspan></text>
  </g>
</svg>
~~~

This shows the flag split across multiple tspan fields.
	
</details>

### Answer

<details>

<summary markdown="span">Flag</summary>

~~~
picoCTF{3nh4nc3d_58bd3420}
~~~

</details>

---

### [Forensics](#contents) | [PicoCTF](./picoctf.md) | [Home](./index.md)

---

## File Types

- Author: Geoffrey Njogu
- 100 points

### Description

This file was found among some files marked confidential but my pdf reader cannot read it, maybe yours can. You can download the file from [here](https://artifacts.picoctf.net/c/327/Flag.pdf).

### Hints

1. Remember that some file types can contain and nest other files.

### Attachments

- [Flag.pdf](https://artifacts.picoctf.net/c/327/Flag.pdf)

### Solutions

<details>

<summary markdown="span">Solution</summary>

Using cat, we can view the contents of the file and see it is a bash file:

~~~shell
$ cat Flag.pdf 
#!/bin/sh
# This is a shell archive (produced by GNU sharutils 4.15.2).
# To extract the files from this archive, save it to some FILE, remove
# everything before the '#!/bin/sh' line above, then type 'sh FILE'.
#
lock_dir=_sh00047
# Made on 2022-03-15 06:50 UTC by <root@0dc4bcba500b>.
# Source directory was '/app'.
#
# Existing files will *not* be overwritten, unless '-c' is specified.
#
# This shar contains:
# length mode       name
# ------ ---------- ------------------------------------------
#   1092 -rw-r--r-- flag
#
...
~~~

The file can be renamed and run in linux:

~~~shell
$ cp Flag.pdf Flag.sh
$ chmod +x Flag.sh 
$ ./Flag.sh 
x - created lock directory _sh00047.
x - extracting flag (text)
x - removed lock directory _sh00047.
~~~

This generates a new file in the directory, flag; which we can see is an archive:

~~~shell
$ ls
flag  Flag.pdf  Flag.sh
$ file flag
flag: current ar archive
~~~

The contents of this archive can be extracted using the ar tool in Linux.  We first rename the archive to avoid overwriting the file during extract:

~~~shell
$ mv flag flag_ar
$ ar xv flag_ar
x - flag
$ ls
flag  flag_ar  Flag.pdf  Flag.sh
$ file flag
flag: cpio archive
~~~

We work our way through the multiple levels of compression:

~~~shell
$ mv flag flag_cpio
$ cpio -iv < flag_cpio
flag
2 blocks
$ ls
flag  flag_ar  flag_cpio  Flag.pdf  Flag.sh
$ file flag
flag: bzip2 compressed data, block size = 900k
$ mv flag flag.bz2
$ bunzip2 flag.bz2
$ ls
flag  flag_ar  flag_cpio  Flag.pdf  Flag.sh
$ file flag
flag: gzip compressed data, was "flag", last modified: Tue Mar 15 06:50:46 2022, from Unix, original size modulo 2^32 330
$ mv flag flag.gz
$ gzip -d flag.gz
$ ls
flag  flag_ar  flag_cpio  Flag.pdf  Flag.sh
$ file flag
flag: lzip compressed data, version: 1
$ mv flag flag.lz
$ lzip -d flag.lz
$ ls
flag  flag_ar  flag_cpio  Flag.pdf  Flag.sh
$ file flag
flag: LZ4 compressed data (v1.4+)
$ mv flag flag.lz4
$ unlz4 flag.lz4
Decoding file flag 
flag.lz4             : decoded 266 bytes 
$ ls
flag  flag_ar  flag_cpio  flag.lz4  Flag.pdf  Flag.sh
$ file flag
flag: LZMA compressed data, non-streamed, size 255
$ mv flag flag.lzma
$ xz --decompress flag.lzma
$ ls
flag  flag_ar  flag_cpio  flag.lz4  Flag.pdf  Flag.sh
$ file flag
flag: lzop compressed data - version 1.040, LZO1X-1, os: Unix
$ mv flag flag.lzop
$ lzop -d flag.lzop
$ ls
flag  flag_ar  flag_cpio  flag.lz4  flag.lzop  Flag.pdf  Flag.sh
$ file flag
flag: lzip compressed data, version: 1
$ mv flag flag.lzip
$ lzip -d flag.lzip
$ ls
flag_ar  flag_cpio  flag.lz4  flag.lzip.out  flag.lzop  Flag.pdf  Flag.sh
$ file flag.lzip.out
flag.lzip.out: XZ compressed data
$ mv flag.lzip.out flag.xz
$ xz -d flag.xz
$ ls
flag  flag_ar  flag_cpio  flag.lz4  flag.lzop  Flag.pdf  Flag.sh
$ file flag
flag: ASCII text
$ cat flag
7069636f4354467b66316c656e406d335f6d406e3170756c407431306e5f
6630725f3062326375723137795f35613833373565307d0a
~~~

This hex string can be converted to ascii using an [online tool](https://www.rapidtables.com/convert/number/hex-to-ascii.html) to provide the flag.

	
</details>

### Answer

<details>

<summary markdown="span">Flag</summary>

~~~
picoCTF{f1len@m3_m@n1pul@t10n_f0r_0b2cur17y_5a8375e0}

~~~

</details>

---

### [Forensics](#contents) | [PicoCTF](./picoctf.md) | [Home](./index.md)

---

## Lookey here

- Author: LT 'syreal' Jones / Mubarak Mikail
- 100 points

### Description

Attackers have hidden information in a very large mass of data in the past, maybe they are still doing it. Download the data [here](https://artifacts.picoctf.net/c/298/anthem.flag.txt).

### Hints

1. Download the file and search for the flag based on the known prefix.

### Attachments

- [anthem.flag.txt](https://artifacts.picoctf.net/c/298/anthem.flag.txt)

### Solutions

<details>

<summary markdown="span">Solution</summary>

Using basic linux cat and grep tools, the flag can be found:

~~~shell
$ cat anthem.flag.txt | grep pico
      we think that the men of picoCTF{gr3p_15_@w3s0m3_429334b2}
~~~
	
</details>

### Answer

<details>

<summary markdown="span">Flag</summary>

~~~
picoCTF{gr3p_15_@w3s0m3_429334b2}
~~~

</details>

---

### [Forensics](#contents) | [PicoCTF](./picoctf.md) | [Home](./index.md)

---

## Packets Primer

- Author: LT 'syreal' Jones
- 100 points

### Description

Download the packet capture file and use packet analysis software to find the flag.

### Hints

1. Wireshark, if you can install and use it, is probably the most beginner friendly packet analysis software product.

### Attachments

- [network-dump.flag.pcap](https://artifacts.picoctf.net/c/203/network-dump.flag.pcap)

### Solutions

<details>

<summary markdown="span">Solution</summary>

Using tshark, the flag can be extracted from the data fields of the captured packets:

~~~shell
$ tshark -r network-dump.flag.pcap -T fields -e data.text



p i c o C T F { p 4 c k 3 7 _ 5 h 4 r k _ 7 d 3 2 b 1 d e }\n

~~~
	
</details>

### Answer

<details>

<summary markdown="span">Flag</summary>

~~~
picoCTF{p4ck37_5h4rk_7d32b1de}
~~~

</details>

---

### [Forensics](#contents) | [PicoCTF](./picoctf.md) | [Home](./index.md)

---

## Redaction gone wrong

- Author: Mubarak Mikail
- 100 points

### Description

Now you DON’T see me. This [report](https://artifacts.picoctf.net/c/264/Financial_Report_for_ABC_Labs.pdf) has some critical data in it, some of which have been redacted correctly, while some were not. Can you find an important key that was not redacted properly?

### Hints

1. How can you be sure of the redaction?

### Attachments

- [Financial_Report_for_ABC_Labs.pdf](https://artifacts.picoctf.net/c/264/Financial_Report_for_ABC_Labs.pdf)

### Solutions

<details>

<summary markdown="span">Solution</summary>

Opening the file, the text can be read directly from the redacted blocks.  This includes the flag:

~~~
Financial Report for ABC Labs, Kigali, Rwanda for the year 2021.
Breakdown - Just painted over in MS word.
Cost Benefit Analysis
Credit Debit
This is not the flag, keep looking
Expenses from the
picoCTF{C4n_Y0u_S33_m3_fully}
Redacted document.
~~~
	
</details>

### Answer

<details>

<summary markdown="span">Flag</summary>

~~~
picoCTF{C4n_Y0u_S33_m3_fully}
~~~

</details>

---

### [Forensics](#contents) | [PicoCTF](./picoctf.md) | [Home](./index.md)

---

## Sleuthkit Intro

- Author: LT 'syreal' Jones
- 100 points

### Description

Download the disk image and use mmls on it to find the size of the Linux partition. Connect to the remote checker service to check your answer and get the flag. Note: if you are using the webshell, download and extract the disk image into /tmp not your home directory.

- [Download disk image](https://artifacts.picoctf.net/c/114/disk.img.gz)
- Access checker program: nc saturn.picoctf.net 52279

### Hints

None.

### Attachments

- [disk.img.gz](https://artifacts.picoctf.net/c/114/disk.img.gz)

### Solutions

<details>

<summary markdown="span">Solution</summary>

The disk image can be decompressed and reviewed using mmls:

~~~shell
$ ls
disk.img.gz
$ file disk.img.gz 
disk.img.gz: gzip compressed data, was "disk.img", last modified: Tue Sep 21 19:34:53 2021, from Unix, original size modulo 2^32 104857600
$ gunzip disk.img.gz 
$ ls
disk.img
$ file disk.img 
disk.img: DOS/MBR boot sector; partition 1 : ID=0x83, active, start-CHS (0x0,32,33), end-CHS (0xc,190,50), startsector 2048, 202752 sectors
$ mmls disk.img 
DOS Partition Table
Offset Sector: 0
Units are in 512-byte sectors

      Slot      Start        End          Length       Description
000:  Meta      0000000000   0000000000   0000000001   Primary Table (#0)
001:  -------   0000000000   0000002047   0000002048   Unallocated
002:  000:000   0000002048   0000204799   0000202752   Linux (0x83)
~~~

Connecting to the challenge server, we can enter the Linux sector size (202752) to get the flag:

~~~shell
$ nc saturn.picoctf.net 52279
What is the size of the Linux partition in the given disk image?
Length in sectors: 202752
202752
Great work!
picoCTF{mm15_f7w!}
exit
~~~
	
</details>

### Answer

<details>

<summary markdown="span">Flag</summary>

~~~
picoCTF{mm15_f7w!}
~~~

</details>

---

### [Forensics](#contents) | [PicoCTF](./picoctf.md) | [Home](./index.md)

---

## Sleuthkit Apprentice

- Author: LT 'syreal' Jones
- 200 points

### Description

Download this disk image and find the flag. Note: if you are using the webshell, download and extract the disk image into /tmp not your home directory.

- [Download compressed disk image](https://artifacts.picoctf.net/c/334/disk.flag.img.gz)

### Hints

None.

### Attachments

- [disk.flag.img.gz](https://artifacts.picoctf.net/c/334/disk.flag.img.gz)

### Solutions

<details>

<summary markdown="span">Solution</summary>

The disk image can be decompressed and reviewed using mmls:

~~~shell
$ ls
disk.flag.img.gz
$ gunzip disk.flag.img.gz 
$ ls
disk.flag.img
$ mmls disk.flag.img 
DOS Partition Table
Offset Sector: 0
Units are in 512-byte sectors

      Slot      Start        End          Length       Description
000:  Meta      0000000000   0000000000   0000000001   Primary Table (#0)
001:  -------   0000000000   0000002047   0000002048   Unallocated
002:  000:000   0000002048   0000206847   0000204800   Linux (0x83)
003:  000:001   0000206848   0000360447   0000153600   Linux Swap / Solaris x86 (0x82)
004:  000:002   0000360448   0000614399   0000253952   Linux (0x83)
~~~

We can mount the image in linux using kpartx:

~~~shell
$ sudo mkdir /mnt/tmp/
$ sudo mkdir /mnt/tmp/lo1
$ sudo mkdir /mnt/tmp/lo2
$ sudo kpartx -a -v disk.flag.img 
add map loop29p1 (253:0): 0 204800 linear 7:29 2048
add map loop29p2 (253:1): 0 153600 linear 7:29 206848
add map loop29p3 (253:2): 0 253952 linear 7:29 360448
$ sudo mount /dev/mapper/loop29p1 /mnt/tmp/lo1
$ sudo mount /dev/mapper/loop29p3 /mnt/tmp/lo2
~~~

To simplify the search for the flag, all empty files and directories in the mounted image can be deleted:

~~~shell
$ sudo find /mnt/tmp -empty -type f -delete
$ sudo find /mnt/tmp -empty -type d -delete
~~~

Using find, we can look for the flag:

~~~shell
$ sudo find /mnt/tmp -name "*flag*" -print
/mnt/tmp/lo2/root/my_folder/flag.uni.txt
$ sudo cat /mnt/tmp/lo2/root/my_folder/flag.uni.txt
picoCTF{by73_5urf3r_42028120}
~~~

To clean up:

~~~shell
$ sudo umount /mnt/tmp/*
$ sudo rmdir /mnt/tmp/lo*
$ sudo rmdir /mnt/tmp
$ sudo kpartx -d -v disk.flag.img
del devmap : loop29p1
del devmap : loop29p2
del devmap : loop29p3
loop deleted : /dev/loop29
$ rm disk.flag.img
~~~
	
</details>

### Answer

<details>

<summary markdown="span">Flag</summary>

~~~
picoCTF{by73_5urf3r_42028120}
~~~

</details>

---

### [Forensics](#contents) | [PicoCTF](./picoctf.md) | [Home](./index.md)

---

## Eavesdrop

- Author: LT 'syreal' Jones
- 300 points

### Description

Download this packet capture and find the flag.

### Hints

1. All we know is that this packet capture includes a chat conversation and a file transfer.

### Attachments

- [capture.flag.pcap](https://artifacts.picoctf.net/c/362/capture.flag.pcap)

### Solutions

<details>

<summary markdown="span">Solution</summary>

Using tshark, we can see the data content of the capture that includes the chat conversation:

~~~shell
$ tshark -r capture.flag.pcap -T fields -e data.text | sed -z 's/\n/ /g' 
           Hey, how do you decrypt this file again?\n  You're serious?\n  Yeah, I'm serious\n  *sigh* openssl des3 -d -salt -in file.des3 -out file.txt -k supersecretpassword123\n      Ok, great, thanks.\n  Let's use Discord next time, it's more secure.\n  C'mon, no one knows we use this program like this!\n  Whatever.\n  Hey.\n  Yeah?\n  Could you transfer the file to me again?\n            Oh great. Ok, over 9002?\n    Yeah, listening.\n     Salted__��,�_5*�1W\rcl��g�&HbZ�H�T��������  Sent it\n     Got it.\n        You're unbelievable\n
~~~

We can see the password for the des3 file is "supersecretpassword123".  The file can be exported from wireshark and we can use openssl to decrypt the file to get the flag:

~~~shell
$ openssl des3 -d -salt -in file.des3 -out file.txt -k supersecretpassword123
*** WARNING : deprecated key derivation used.
Using -iter or -pbkdf2 would be better.
$ ls
capture.flag.pcap  file.des3  file.txt
$ cat file.txt
picoCTF{nc_73115_411_77b05957}
~~~
	
</details>

### Answer

<details>

<summary markdown="span">Flag</summary>

~~~
picoCTF{nc_73115_411_77b05957}
~~~

</details>

---

### [Forensics](#contents) | [PicoCTF](./picoctf.md) | [Home](./index.md)

---

## Operation Oni

- Author: LT 'syreal' Jones
- 300 points

### Description

Download this disk image, find the key and log into the remote machine. Note: if you are using the webshell, download and extract the disk image into /tmp not your home directory.

### Hints

None.

### Attachments

- disk.img.gz

### Solutions

<details>

<summary markdown="span">Solution</summary>

The disk image can be extracted and inspected:

~~~shell
$ ls
disk.img.gz
$ gunzip disk.img.gz 
$ file disk.img 
disk.img: DOS/MBR boot sector; partition 1 : ID=0x83, active, start-CHS (0x0,32,33), end-CHS (0xc,223,19), startsector 2048, 204800 sectors; partition 2 : ID=0x83, start-CHS (0xc,223,20), end-CHS (0x1d,81,52), startsector 206848, 264192 sectors
$ mmls disk.img 
DOS Partition Table
Offset Sector: 0
Units are in 512-byte sectors

      Slot      Start        End          Length       Description
000:  Meta      0000000000   0000000000   0000000001   Primary Table (#0)
001:  -------   0000000000   0000002047   0000002048   Unallocated
002:  000:000   0000002048   0000206847   0000204800   Linux (0x83)
003:  000:001   0000206848   0000471039   0000264192   Linux (0x83)
~~~

The linux partition can be mounted, cleaned and the ssh key can be found:

~~~shell
$ sudo mkdir /mnt/tmp
$ sudo kpartx -a -v disk.img 
add map loop29p1 (253:0): 0 204800 linear 7:29 2048
add map loop29p2 (253:1): 0 264192 linear 7:29 206848
$ sudo mount /dev/mapper/loop29p2 /mnt/tmp
$ sudo find /mnt/tmp -empty -type f -delete
$ sudo find /mnt/tmp -empty -type d -delete
$ ls /mnt/tmp
bin  etc  lib  root  sbin  usr  var
$ sudo find /mnt/tmp -name "*id_*" -print
/mnt/tmp/root/.ssh/id_ed25519.pub
/mnt/tmp/root/.ssh/id_ed25519
/mnt/tmp/lib/modules/5.10.61-0-virt/kernel/drivers/scsi/raid_class.ko
$ sudo cp /mnt/tmp/root/.ssh/id_ed25519 ~/Downloads/key_file
$ sudo umount /mnt/tmp
$ sudo rmdir /mnt/tmp
$ sudo kpartx -d -v disk.img 
del devmap : loop29p1
del devmap : loop29p2
loop deleted : /dev/loop29
$ rm disk.img 
~~~

We can now connect to the remote machine:

~~~shell
$ ssh -i key_file -p 53146 ctf-player@saturn.picoctf.net
Welcome to Ubuntu 20.04.3 LTS (GNU/Linux 5.13.0-1017-aws x86_64)

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

ctf-player@challenge:~$ ls
flag.txt
ctf-player@challenge:~$ cat flag.txt 
picoCTF{k3y_5l3u7h_af277f77}ctf-player@challenge:~$ exit
logout
Connection to saturn.picoctf.net closed.
~~~
	
</details>

### Answer

<details>

<summary markdown="span">Flag</summary>

~~~
picoCTF{k3y_5l3u7h_af277f77}
~~~

</details>

---

### [Forensics](#contents) | [PicoCTF](./picoctf.md) | [Home](./index.md)

---

## St3g0

- Author: LT 'syreal' Jones (ft. djrobin17)
- 300 points

### Description

Download this image and find the flag.

### Hints

1. We know the end sequence of the message will be $t3g0.

### Attachments

- [pico.flag.png](https://artifacts.picoctf.net/c/425/pico.flag.png)

### Solutions

<details>

<summary markdown="span">Solution</summary>

Using zsteg the flag can be recovered:

~~~shell
$ zsteg pico.flag.png 
b1,r,lsb,xy         .. text: "~__B>wR?G@"
b1,g,lsb,xy         .. file: dBase III DBT, version number 0, next free block index 3549684369
b1,g,msb,xy         .. file: dBase III DBT, version number 0, next free block index 3418965897
b1,b,lsb,xy         .. file: dBase III DBT, version number 0, next free block index 2623130757
b1,rgb,lsb,xy       .. text: "picoCTF{7h3r3_15_n0_5p00n_87ef5b0b}$t3g0"
b1,abgr,lsb,xy      .. text: "E2A5q4E%uSA"
b2,b,lsb,xy         .. text: "AAPAAQTAAA"
b2,b,msb,xy         .. text: "HWUUUUUU"
b3,r,lsb,xy         .. file: gfxboot compiled html help file
b3,b,msb,xy         .. file: StarOffice Gallery theme @\002 H\200\004H\002\004H\200$H\022\004H\200\004\010, 0 objects
b4,r,lsb,xy         .. file: Targa image data (16-273) 65536 x 4097 x 1 +4352 +4369 - 1-bit alpha - right "\021\020\001\001\021\021\001\001\021\021\001"
b4,g,lsb,xy         .. file: 0420 Alliant virtual executable not stripped
b4,b,lsb,xy         .. file: Targa image data - Map 272 x 17 x 16 +257 +272 - 1-bit alpha "\020\001\021\001\021\020\020\001\020\001\020\001"
b4,bgr,lsb,xy       .. file: Targa image data - Map 273 x 272 x 16 +1 +4113 - 1-bit alpha "\020\001\001\001"
b4,rgba,lsb,xy      .. file: Novell LANalyzer capture file
b4,rgba,msb,xy      .. file: Applesoft BASIC program data, first line number 8
b4,abgr,lsb,xy      .. file: Novell LANalyzer capture file

~~~
	
</details>

### Answer

<details>

<summary markdown="span">Flag</summary>

~~~
picoCTF{7h3r3_15_n0_5p00n_87ef5b0b}
~~~

</details>

---

### [Forensics](#contents) | [PicoCTF](./picoctf.md) | [Home](./index.md)

---

## Operation Orchid

- Author: LT 'syreal' Jones (ft. djrobin17)
- 400 points

### Description

Download this disk image and find the flag. Note: if you are using the webshell, download and extract the disk image into /tmp not your home directory.

### Hints

None.

### Attachments

- [disk.flag.img.gz](https://artifacts.picoctf.net/c/240/disk.flag.img.gz)

### Solutions

<details>

<summary markdown="span">Solution</summary>

The disk image can be extracted and inspected:

~~~shell
$ ls
disk.flag.img.gz
$ gunzip disk.flag.img.gz 
$ mmls disk.flag.img 
DOS Partition Table
Offset Sector: 0
Units are in 512-byte sectors

      Slot      Start        End          Length       Description
000:  Meta      0000000000   0000000000   0000000001   Primary Table (#0)
001:  -------   0000000000   0000002047   0000002048   Unallocated
002:  000:000   0000002048   0000206847   0000204800   Linux (0x83)
003:  000:001   0000206848   0000411647   0000204800   Linux Swap / Solaris x86 (0x82)
004:  000:002   0000411648   0000819199   0000407552   Linux (0x83)
~~~

The linux partition can be mounted, cleaned and the encrypted flag file can be found:

~~~shell
$ sudo mkdir /mnt/tmp
$ sudo kpartx -a -v disk.flag.img 
add map loop29p1 (253:0): 0 204800 linear 7:29 2048
add map loop29p2 (253:1): 0 204800 linear 7:29 206848
add map loop29p3 (253:2): 0 407552 linear 7:29 411648
$ sudo mount /dev/mapper/loop29p3 /mnt/tmp
$ ls /mnt/tmp
bin  boot  dev  etc  home  lib  lost+found  media  mnt  opt  proc  root  run  sbin  srv  swap  sys  tmp  usr  var
$ sudo find /mnt/tmp -empty -type f -delete
$ sudo find /mnt/tmp -empty -type d -delete
$ ls /mnt/tmp
bin  etc  lib  root  sbin  usr  var
$ sudo find /mnt/tmp -name "*flag*" -print
/mnt/tmp/root/flag.txt.enc
$ sudo cp /mnt/tmp/root/flag.txt.enc ~/Downloads/flag.enc
$ sudo chown user flag.enc
~~~

This is found in the root directory, the bash history can be reviewed to see if there is a recent operation on this file that might help decrypt it:

~~~shell
$ sudo ls -a /mnt/tmp/root
.  ..  .ash_history  flag.txt.enc
$ sudo cat /mnt/tmp/root/.ash_history
touch flag.txt
nano flag.txt 
apk get nano
apk --help
apk add nano
nano flag.txt 
openssl
openssl aes256 -salt -in flag.txt -out flag.txt.enc -k unbreakablepassword1234567
shred -u flag.txt
ls -al
halt
~~~

Using the openssl aes256 encryption password, we can attempt to recover the flag:

~~~shell
$ openssl aes256 -d -in flag.enc -k unbreakablepassword1234567 > flag_out.txt
*** WARNING : deprecated key derivation used.
Using -iter or -pbkdf2 would be better.
bad decrypt
139691943691584:error:06065064:digital envelope routines:EVP_DecryptFinal_ex:bad decrypt:../crypto/evp/evp_enc.c:610:
$ cat flag_out.txt 
picoCTF{h4un71ng_p457_17237fce}
~~~

The flag is recovered.  We can now clean up:

~~~shell
$ sudo umount /mnt/tmp
$ sudo rmdir /mnt/tmp
$ sudo kpartx -d -v disk.flag.img
del devmap : loop29p1
del devmap : loop29p2
del devmap : loop29p3
loop deleted : /dev/loop29
$ rm -r *
~~~
	
</details>

### Answer

<details>

<summary markdown="span">Flag</summary>

~~~
picoCTF{h4un71ng_p457_17237fce}
~~~

</details>

---

### [Forensics](#contents) | [PicoCTF](./picoctf.md) | [Home](./index.md)

---

## SideChannel

- Author: Anish Singhani
- 400 points

### Description

There's something fishy about this PIN-code checker, can you figure out the PIN and get the flag? Download the PIN checker program here [pin_checker](https://artifacts.picoctf.net/c/147/pin_checker) Once you've figured out the PIN (and gotten the checker program to accept it), connect to the master server using nc saturn.picoctf.net 53639 and provide it the PIN to get your flag.

### Hints

1. Read about "timing-based side-channel attacks."
2. Attempting to reverse-engineer or exploit the binary won't help you, you can figure out the PIN just by interacting with it and measuring certain properties about it.
3. Don't run your attacks against the master server, it is secured against them. The PIN code you get from the pin_checker binary is the same as the one for the master server.

### Attachments

- [pin_checker](https://artifacts.picoctf.net/c/147/pin_checker)

### Solutions

<details>

<summary markdown="span">Solution</summary>

Running the pin checker, we see the program provides 2 rejection statements:

~~~shell
$ ./pin_checker 
Please enter your 8-digit PIN code:
00000000
8
Checking PIN...
Access denied.
$ ./pin_checker 
Please enter your 8-digit PIN code:
0
1
Incorrect length.
~~~

After trying several random pins, it can be seen that the execution time increases with specific integers at specific locations in the pin.  Assuming this is due to a correct number placement, this can be exploited in Python using a time-based side channel attack:

~~~py
import subprocess
import time

badstr = "Access denied"

pin = ["0"]*8

for i in range(len(pin)):
    xt = 0
    dig = "0"
    for j in range(10):
        pin[i] = str(j)
        s = ("".join(pin)+"\n").encode()
        t0 = time.time()
        a = subprocess.Popen(["./pin_checker"], stdin = subprocess.PIPE, stdout=subprocess.PIPE, stderr=subprocess.PIPE)
        a.stdin.write(s)
        outputlog, errorlog = a.communicate()
        t1 = time.time()
        print("current pin = "+"".join(pin))
        dt = t1-t0
        if dt>xt:
            xt = dt
            dig = str(j)
        if badstr not in outputlog.decode():
            print("PIN is {}".format(s.decode()))
            break
    pin[i] = dig
~~~

This finds the pin index solution that has the longest response and iterates across all 8 characters.  It provides a solution:

~~~
PIN is 48390513

Total execution time = 37.96782946586609
~~~

This can be confirmed locally:

~~~shell
$ ./pin_checker 
Please enter your 8-digit PIN code:
48390513
8
Checking PIN...
Access granted. You may use your PIN to log into the master server.
~~~

Connecting to the webserver, we are given the flag:

~~~shell
$ nc saturn.picoctf.net 53639
Verifying that you are a human...
Please enter the master PIN code:
48390513
Password correct. Here's your flag:
picoCTF{t1m1ng_4tt4ck_0431e830}

exit
~~~

</details>

### Answer

<details>

<summary markdown="span">Flag</summary>

~~~
picoCTF{t1m1ng_4tt4ck_0431e830}
~~~

</details>

---

### [Forensics](#contents) | [PicoCTF](./picoctf.md) | [Home](./index.md)

---

## Torrent Analyze

- Author: Mubarak Mikail
- 400 points

### Description

SOS, someone is torrenting on our network. One of your colleagues has been using torrent to download some files on the company’s network. Can you identify the file(s) that were downloaded? The file name will be the flag, like picoCTF{filename}. [Captured traffic](https://artifacts.picoctf.net/c/206/torrent.pcap).

### Hints

1. Download and open the file with a packet analyzer like Wireshark.
2. You may want to enable BitTorrent protocol (BT-DHT, etc.) on Wireshark. Analyze -> Enabled Protocols
3. Try to understand peers, leechers and seeds. Article
4. The file name ends with .iso

### Attachments

- [torrent.pcap](https://artifacts.picoctf.net/c/206/torrent.pcap)

### Solutions

<details>

<summary markdown="span">Solution</summary>

Loading the pcap in tshark we can see there is a significant number of packets associated with torrent conversations.

As described in the challenge, we are looking for files downloaded over torrent.  We can filter all torrent traffic:

~~~shell
$ tshark -r torrent.pcap -Y "bt-dht"
    1 0.000000000 79.252.29.145 → 192.168.73.132 BT-DHT 143 BitTorrent DHT Protocol 6889 51413     
    2 0.000123837 192.168.73.132 → 79.252.29.145 BT-DHT 308 BitTorrent DHT Protocol reply=8 nodes  51413 6889     
   35 3.718824097 192.168.73.132 → 151.225.247.46 BT-DHT 100 BitTorrent DHT Protocol 51413 6881     
   37 3.718968245 192.168.73.132 → 187.60.223.123 BT-DHT 308 BitTorrent DHT Protocol reply=8 nodes  51413 52226     
   79 4.864344025 5.189.157.90 → 192.168.73.132 BT-DHT 139 BitTorrent DHT Protocol 12023 51413     
   80 4.864638481 192.168.73.132 → 5.189.157.90 BT-DHT 327 BitTorrent DHT Protocol reply=8 nodes  51413 12023     
  145 5.929073654 192.168.73.132 → 176.9.71.124 BT-DHT 100 BitTorrent DHT Protocol 51413 51413     
  156 6.043222052 192.168.73.132 → 176.9.71.124 BT-uTP 62 uTorrent Transport Protocol Type: State 51413 51413     
  158 6.055061265 176.9.71.124 → 192.168.73.132 BT-DHT 91 BitTorrent DHT Protocol 51413 51413     
  163 6.121902138 192.168.73.132 → 188.143.71.5 BT-DHT 100 BitTorrent DHT Protocol 51413 51413     
  166 6.175180959 192.168.73.132 → 78.139.200.211 BT-DHT 100 BitTorrent DHT Protocol 51413 51413     
  168 6.247034261 188.143.71.5 → 192.168.73.132 BT-DHT 91 BitTorrent DHT Protocol 51413 51413     
  169 6.255228518 192.168.73.132 → 188.143.71.5 BT-DHT 62 BitTorrent DHT Protocol[Malformed Packet] 51413 51413     
  171 6.255531459 192.168.73.132 → 185.205.109.41 BT-DHT 100 BitTorrent DHT Protocol 51413 51412     
  173 6.291562163 192.168.73.132 → 78.139.200.211 BT-uTP 62 uTorrent Transport Protocol Type: State 51413 51413     
  174 6.296537631 192.168.73.132 → 176.9.71.124 BT-uTP 262 uTorrent Transport Protocol Type: Data 51413 51413     
  187 6.358520127 78.139.200.211 → 192.168.73.132 BT-DHT 91 BitTorrent DHT Protocol 51413 51413     
  190 6.397679722 185.205.109.41 → 192.168.73.132 BT-DHT 91 BitTorrent DHT Protocol 51412 51413     
  194 6.404213182 192.168.73.132 → 185.205.109.41 BT-DHT 62 BitTorrent DHT Protocol[Malformed Packet] 51413 51412     
  215 6.612900968 192.168.73.132 → 51.174.215.38 BT-DHT 100 BitTorrent DHT Protocol 51413 6971     
  218 6.639841538 192.168.73.132 → 47.53.234.11 BT-DHT 100 BitTorrent DHT Protocol 51413 54497     
  221 6.708481818 192.168.73.132 → 78.134.14.242 BT-DHT 100 BitTorrent DHT Protocol 51413 49160     
  222 6.749265964 192.168.73.132 → 47.53.234.11 BT-DHT 62 BitTorrent DHT Protocol[Malformed Packet] 51413 54497     
  223 6.749413243 192.168.73.132 → 51.174.215.38 BT-DHT 62 BitTorrent DHT Protocol[Malformed Packet] 51413 6971     
  224 6.755343040 47.53.234.11 → 192.168.73.132 BT-DHT 91 BitTorrent DHT Protocol 54497 51413     
  225 6.755978659 51.174.215.38 → 192.168.73.132 BT-DHT 91 BitTorrent DHT Protocol 6971 51413     
  226 6.797190959 192.168.73.132 → 188.143.71.5 BT-uTP 276 uTorrent Transport Protocol Type: Data 51413 51413     
  227 6.797347389 192.168.73.132 → 78.139.200.211 BT-uTP 276 uTorrent Transport Protocol Type: Data 51413 51413     
  228 6.797425820 192.168.73.132 → 185.205.109.41 BT-DHT 276 BitTorrent DHT Protocol[Malformed Packet] 51413 51412     
  248 6.815375702 192.168.73.132 → 78.134.14.242 BT-DHT 62 BitTorrent DHT Protocol[Malformed Packet] 51413 49160     
  252 6.864135727 78.134.14.242 → 192.168.73.132 BT-DHT 122 BitTorrent DHT Protocol 49160 51413     
  254 6.864416598 192.168.73.132 → 158.69.251.205 BT-DHT 100 BitTorrent DHT Protocol 51413 6881     
  258 6.889466703 158.69.251.205 → 192.168.73.132 BT-DHT 100 BitTorrent DHT Protocol 6881 51413     
  270 7.035595298 185.205.109.41 → 192.168.73.132 BT-DHT 62 BitTorrent DHT Protocol[Malformed Packet] 51412 51413     
  281 7.296692757 192.168.73.132 → 47.53.234.11 BT-DHT 297 BitTorrent DHT Protocol[Malformed Packet] 51413 54497     
  282 7.296749688 192.168.73.132 → 51.174.215.38 BT-DHT 297 BitTorrent DHT Protocol[Malformed Packet] 51413 6971     
  283 7.296772241 192.168.73.132 → 78.134.14.242 BT-uTP 297 uTorrent Transport Protocol Type: Data 51413 49160     
  313 7.519829991 192.168.73.132 → 79.146.67.82 BT-DHT 100 BitTorrent DHT Protocol 51413 6882     
  316 7.538783637 47.53.234.11 → 192.168.73.132 BT-DHT 62 BitTorrent DHT Protocol[Malformed Packet] 54497 51413     
  322 7.566775900 51.174.215.38 → 192.168.73.132 BT-DHT 62 BitTorrent DHT Protocol[Malformed Packet] 6971 51413     
  324 7.641722187 192.168.73.132 → 79.146.67.82 BT-DHT 62 BitTorrent DHT Protocol[Malformed Packet] 51413 6882     
  329 7.660144554 79.146.67.82 → 192.168.73.132 BT-DHT 122 BitTorrent DHT Protocol 6882 51413     
  330 7.660322641 192.168.73.132 → 94.21.242.135 BT-DHT 100 BitTorrent DHT Protocol 51413 50655     
  332 7.681928837 95.146.167.87 → 192.168.73.132 BT-DHT 265 BitTorrent DHT Protocol 16981 51413     
  333 7.682072594 192.168.73.132 → 95.146.167.87 BT-DHT 91 BitTorrent DHT Protocol 51413 16981     
  337 7.765640714 192.168.73.132 → 80.243.101.96 BT-DHT 100 BitTorrent DHT Protocol 51413 51413     
  338 7.777585673 192.168.73.132 → 94.21.242.135 BT-DHT 62 BitTorrent DHT Protocol[Malformed Packet] 51413 50655     
  339 7.777589944 79.146.67.82 → 192.168.73.132 BT-DHT 158 BitTorrent DHT Protocol[Malformed Packet] 6882 51413     
  341 7.787801070 94.21.242.135 → 192.168.73.132 BT-DHT 91 BitTorrent DHT Protocol 50655 51413     
  358 7.875178958 192.168.73.132 → 80.243.101.96 BT-DHT 62 BitTorrent DHT Protocol[Malformed Packet] 51413 51413     
  366 7.942022675 192.168.73.132 → 79.146.67.82 BT-DHT 62 BitTorrent DHT Protocol[Malformed Packet] 51413 6882     
  367 7.951491289 80.243.101.96 → 192.168.73.132 BT-DHT 91 BitTorrent DHT Protocol 51413 51413     
  369 7.965222050 192.168.73.132 → 58.32.67.104 BT-DHT 100 BitTorrent DHT Protocol 51413 51413     
  373 8.087467448 192.168.73.132 → 58.32.67.104 BT-DHT 62 BitTorrent DHT Protocol[Malformed Packet] 51413 51413     
  382 8.238744778 58.32.67.104 → 192.168.73.132 BT-DHT 91 BitTorrent DHT Protocol 51413 51413     
  385 8.295217852 192.168.73.132 → 94.21.242.135 BT-uTP 340 uTorrent Transport Protocol Type: Data 51413 50655     
  387 8.295454628 192.168.73.132 → 58.32.67.104 BT-uTP 347 uTorrent Transport Protocol Type: Data 51413 51413     
  388 8.295529311 192.168.73.132 → 80.243.101.96 BT-DHT 340 BitTorrent DHT Protocol[Malformed Packet] 51413 51413     
  417 8.519644514 80.243.101.96 → 192.168.73.132 BT-DHT 62 BitTorrent DHT Protocol[Malformed Packet] 51413 51413     
  429 8.605862029 186.105.1.103 → 192.168.73.132 BT-DHT 146 BitTorrent DHT Protocol 6881 51413     
  430 8.606025004 192.168.73.132 → 186.105.1.103 BT-DHT 325 BitTorrent DHT Protocol reply=8 nodes  51413 6881     
  436 8.771325275 191.37.246.111 → 192.168.73.132 BT-DHT 146 BitTorrent DHT Protocol 60817 51413     
  437 8.771712131 192.168.73.132 → 191.37.246.111 BT-DHT 325 BitTorrent DHT Protocol reply=8 nodes  51413 60817     
  461 8.843776438 51.174.215.38 → 192.168.73.132 BT-uTP 448 uTorrent Transport Protocol Type: Data 6971 51413     
  477 8.963575817 192.168.73.132 → 71.135.217.90 BT-DHT 100 BitTorrent DHT Protocol 51413 51413     
  480 8.984349794 80.243.101.96 → 192.168.73.132 BT-DHT 239 BitTorrent DHT Protocol[Malformed Packet] 51413 51413     
  481 8.993153065 185.205.109.41 → 192.168.73.132 BT-DHT 190 BitTorrent DHT Protocol[Malformed Packet] 51412 51413     
  487 9.041009726 71.135.217.90 → 192.168.73.132 BT-DHT 91 BitTorrent DHT Protocol 51413 51413     
  490 9.064865980 192.168.73.132 → 71.135.217.90 BT-DHT 62 BitTorrent DHT Protocol[Malformed Packet] 51413 51413     
  496 9.109796684 192.168.73.132 → 185.205.109.41 BT-DHT 62 BitTorrent DHT Protocol[Malformed Packet] 51413 51412     
  497 9.109857873 192.168.73.132 → 80.243.101.96 BT-DHT 62 BitTorrent DHT Protocol[Malformed Packet] 51413 51413     
  500 9.301493384 192.168.73.132 → 71.135.217.90 BT-uTP 362 uTorrent Transport Protocol Type: Data 51413 51413     
  523 9.435696790 192.168.73.132 → 188.242.126.69 BT-DHT 100 BitTorrent DHT Protocol 51413 51413     
  544 9.572480383 188.242.126.69 → 192.168.73.132 BT-DHT 91 BitTorrent DHT Protocol 51413 51413     
  545 9.575805553 192.168.73.132 → 188.242.126.69 BT-DHT 62 BitTorrent DHT Protocol[Malformed Packet] 51413 51413     
  558 9.803191229 192.168.73.132 → 188.242.126.69 BT-uTP 376 uTorrent Transport Protocol Type: Data 51413 51413     
  585 9.874695209 47.53.234.11 → 192.168.73.132 BT-uTP 371 uTorrent Transport Protocol Type: Data 54497 51413     
  631 10.105222985 192.168.73.132 → 104.173.116.244 BT-DHT 100 BitTorrent DHT Protocol 51413 62581     
  722 10.802491841 192.168.73.132 → 79.146.67.82 BT-DHT 190 BitTorrent DHT Protocol[Malformed Packet] 51413 6882     
  777 10.937024205 79.146.67.82 → 192.168.73.132 BT-DHT 62 BitTorrent DHT Protocol[Malformed Packet] 6882 51413     
  784 10.946304920 192.168.73.132 → 94.19.206.85 BT-DHT 100 BitTorrent DHT Protocol 51413 50974     
  789 10.991652717 185.205.109.41 → 192.168.73.132 BT-DHT 67 BitTorrent DHT Protocol[Malformed Packet] 51412 51413     
  796 11.037151777 192.168.73.132 → 93.57.247.235 BT-DHT 100 BitTorrent DHT Protocol 51413 60900     
  799 11.067656027 192.168.73.132 → 94.19.206.85 BT-DHT 62 BitTorrent DHT Protocol[Malformed Packet] 51413 50974     
  805 11.087357045 94.19.206.85 → 192.168.73.132 BT-DHT 122 BitTorrent DHT Protocol 50974 51413     
  810 11.142446250 192.168.73.132 → 185.205.109.41 BT-DHT 62 BitTorrent DHT Protocol[Malformed Packet] 51413 51412     
  812 11.142600582 192.168.73.132 → 93.57.247.235 BT-DHT 62 BitTorrent DHT Protocol[Malformed Packet] 51413 60900     
  814 11.167543502 93.57.247.235 → 192.168.73.132 BT-DHT 122 BitTorrent DHT Protocol 60900 51413     
  818 11.208568356 94.19.206.85 → 192.168.73.132 BT-DHT 328 BitTorrent DHT Protocol[Malformed Packet] 50974 51413     
  821 11.257521348 192.168.73.132 → 86.59.144.16 BT-DHT 100 BitTorrent DHT Protocol 51413 64194     
  824 11.269598861 93.57.247.235 → 192.168.73.132 BT-DHT 293 BitTorrent DHT Protocol[Malformed Packet] 60900 51413     
  858 11.357191656 192.168.73.132 → 94.19.206.85 BT-DHT 62 BitTorrent DHT Protocol[Malformed Packet] 51413 50974     
  866 11.386079478 192.168.73.132 → 86.59.144.16 BT-DHT 62 BitTorrent DHT Protocol[Malformed Packet] 51413 64194     
  867 11.386198844 192.168.73.132 → 93.57.247.235 BT-DHT 62 BitTorrent DHT Protocol[Malformed Packet] 51413 60900     
  869 11.392239753 86.59.144.16 → 192.168.73.132 BT-DHT 122 BitTorrent DHT Protocol 64194 51413     
  894 11.493923965 80.243.101.96 → 192.168.73.132 BT-DHT 67 BitTorrent DHT Protocol[Malformed Packet] 51413 51413     
  898 11.525266454 86.59.144.16 → 192.168.73.132 BT-DHT 272 BitTorrent DHT Protocol[Malformed Packet] 64194 51413     
  907 11.564784472 192.168.73.132 → 77.108.222.246 BT-DHT 100 BitTorrent DHT Protocol 51413 6881     
  909 11.570646414 192.168.73.132 → 93.41.123.45 BT-DHT 100 BitTorrent DHT Protocol 51413 25372     
  912 11.604881092 192.168.73.132 → 94.215.186.125 BT-DHT 100 BitTorrent DHT Protocol 51413 18476     
  914 11.621521969 192.168.73.132 → 90.163.0.193 BT-DHT 100 BitTorrent DHT Protocol 51413 6881     
  915 11.635103353 192.168.73.132 → 80.243.101.96 BT-DHT 62 BitTorrent DHT Protocol[Malformed Packet] 51413 51413     
  916 11.635157499 192.168.73.132 → 86.59.144.16 BT-DHT 62 BitTorrent DHT Protocol[Malformed Packet] 51413 64194     
  921 11.650002308 192.168.73.132 → 64.137.166.8 BT-DHT 100 BitTorrent DHT Protocol 51413 37164     
  924 11.678232023 64.137.166.8 → 192.168.73.132 BT-DHT 122 BitTorrent DHT Protocol 37164 51413     
  927 11.703896173 192.168.73.132 → 77.108.222.246 BT-DHT 62 BitTorrent DHT Protocol[Malformed Packet] 51413 6881     
  930 11.716339536 192.168.73.132 → 206.45.13.100 BT-DHT 100 BitTorrent DHT Protocol 51413 6881     
  931 11.722010839 94.215.186.125 → 192.168.73.132 BT-DHT 122 BitTorrent DHT Protocol 18476 51413     
  932 11.728131186 77.108.222.246 → 192.168.73.132 BT-DHT 122 BitTorrent DHT Protocol 6881 51413     
  934 11.751437673 206.45.13.100 → 192.168.73.132 BT-DHT 122 BitTorrent DHT Protocol 6881 51413     
  936 11.762205248 192.168.73.132 → 91.122.52.237 BT-DHT 100 BitTorrent DHT Protocol 51413 41421     
  937 11.762264180 192.168.73.132 → 64.137.166.8 BT-DHT 62 BitTorrent DHT Protocol[Malformed Packet] 51413 37164     
  939 11.762311020 192.168.73.132 → 94.215.186.125 BT-DHT 62 BitTorrent DHT Protocol[Malformed Packet] 51413 18476     
  941 11.788957115 64.137.166.8 → 192.168.73.132 BT-DHT 158 BitTorrent DHT Protocol[Malformed Packet] 37164 51413     
  967 11.816764584 192.168.73.132 → 206.45.13.100 BT-DHT 62 BitTorrent DHT Protocol[Malformed Packet] 51413 6881     
  979 11.867350469 77.108.222.246 → 192.168.73.132 BT-DHT 342 BitTorrent DHT Protocol[Malformed Packet] 6881 51413     
  980 11.873592448 192.168.73.132 → 91.122.52.237 BT-DHT 62 BitTorrent DHT Protocol[Malformed Packet] 51413 41421     
  981 11.882202204 94.215.186.125 → 192.168.73.132 BT-uTP 279 uTorrent Transport Protocol Type: Data 18476 51413     
  998 11.953394109 192.168.73.132 → 64.137.166.8 BT-DHT 62 BitTorrent DHT Protocol[Malformed Packet] 51413 37164     
 1011 12.001175413 192.168.73.132 → 77.108.222.246 BT-DHT 62 BitTorrent DHT Protocol[Malformed Packet] 51413 6881     
 1013 12.030529793 91.122.52.237 → 192.168.73.132 BT-uTP 151 uTorrent Transport Protocol Type: Data 41421 51413     
 1028 12.176954340 192.168.73.132 → 37.44.103.128 BT-DHT 100 BitTorrent DHT Protocol 51413 21650     
 1030 12.182047623 192.168.73.132 → 188.6.7.124  BT-DHT 100 BitTorrent DHT Protocol 51413 50402     
 1033 12.299445023 192.168.73.132 → 37.44.103.128 BT-DHT 62 BitTorrent DHT Protocol[Malformed Packet] 51413 21650     
 1034 12.299606277 192.168.73.132 → 188.6.7.124  BT-DHT 62 BitTorrent DHT Protocol[Malformed Packet] 51413 50402     
 1038 12.304689899 192.168.73.132 → 206.45.13.100 BT-uTP 558 uTorrent Transport Protocol Type: Data 51413 6881     
 1057 12.315756452  188.6.7.124 → 192.168.73.132 BT-DHT 122 BitTorrent DHT Protocol 50402 51413     
 1063 12.339819550 37.44.103.128 → 192.168.73.132 BT-DHT 122 BitTorrent DHT Protocol 21650 51413     
 1080 12.433541080  188.6.7.124 → 192.168.73.132 BT-DHT 172 BitTorrent DHT Protocol[Malformed Packet] 50402 51413     
 1085 12.446820180 37.44.103.128 → 192.168.73.132 BT-DHT 363 BitTorrent DHT Protocol[Malformed Packet] 21650 51413     
 1091 12.452493241 192.168.73.132 → 84.251.198.103 BT-DHT 100 BitTorrent DHT Protocol 51413 10028     
 1099 12.492069056 192.168.73.132 → 160.2.177.68 BT-DHT 100 BitTorrent DHT Protocol 51413 42696     
 1101 12.498062974 192.168.73.132 → 91.132.136.51 BT-DHT 100 BitTorrent DHT Protocol 51413 25818     
 1104 12.558615990 192.168.73.132 → 84.251.198.103 BT-DHT 62 BitTorrent DHT Protocol[Malformed Packet] 51413 10028     
 1105 12.558663140 192.168.73.132 → 37.44.103.128 BT-DHT 62 BitTorrent DHT Protocol[Malformed Packet] 51413 21650     
 1106 12.558685587 192.168.73.132 → 188.6.7.124  BT-DHT 62 BitTorrent DHT Protocol[Malformed Packet] 51413 50402     
 1113 12.587115785 84.251.198.103 → 192.168.73.132 BT-DHT 122 BitTorrent DHT Protocol 10028 51413     
 1115 12.591596060 192.168.73.132 → 160.2.177.68 BT-DHT 62 BitTorrent DHT Protocol[Malformed Packet] 51413 42696     
 1117 12.598002731 160.2.177.68 → 192.168.73.132 BT-DHT 122 BitTorrent DHT Protocol 42696 51413     
 1120 12.630993477 192.168.73.132 → 77.85.205.111 BT-DHT 100 BitTorrent DHT Protocol 51413 6881     
 1121 12.666430609 192.168.73.132 → 91.132.136.51 BT-DHT 62 BitTorrent DHT Protocol[Malformed Packet] 51413 25818     
 1123 12.691891570 84.251.198.103 → 192.168.73.132 BT-uTP 272 uTorrent Transport Protocol Type: Data 10028 51413     
 1125 12.699788515 160.2.177.68 → 192.168.73.132 BT-uTP 193 uTorrent Transport Protocol Type: Data 42696 51413     
 1129 12.732260482 192.168.73.132 → 77.85.205.111 BT-DHT 62 BitTorrent DHT Protocol[Malformed Packet] 51413 6881     
 1130 12.751497329 91.132.136.51 → 192.168.73.132 BT-DHT 122 BitTorrent DHT Protocol 25818 51413     
 1135 12.804164964 192.168.73.132 → 86.59.144.16 BT-DHT 366 BitTorrent DHT Protocol[Malformed Packet] 51413 64194     
 1136 12.804323075 192.168.73.132 → 94.19.206.85 BT-uTP 331 uTorrent Transport Protocol Type: Data 51413 50974     
 1137 12.804403904 192.168.73.132 → 93.57.247.235 BT-uTP 331 uTorrent Transport Protocol Type: Data 51413 60900     
 1166 12.851610956 192.168.73.132 → 82.235.49.147 BT-DHT 100 BitTorrent DHT Protocol 51413 16881     
 1168 12.872697697 77.85.205.111 → 192.168.73.132 BT-uTP 391 uTorrent Transport Protocol Type: Data 6881 51413     
 1171 12.879765756 192.168.73.132 → 5.135.186.3  BT-DHT 100 BitTorrent DHT Protocol 51413 51413     
 1179 12.923187524 91.132.136.51 → 192.168.73.132 BT-DHT 215 BitTorrent DHT Protocol[Malformed Packet] 25818 51413     
 1187 12.942919124 86.59.144.16 → 192.168.73.132 BT-DHT 62 BitTorrent DHT Protocol[Malformed Packet] 64194 51413     
 1197 12.956871621 192.168.73.132 → 46.234.155.66 BT-DHT 100 BitTorrent DHT Protocol 51413 39042     
 1199 12.969660294  5.135.186.3 → 192.168.73.132 BT-DHT 91 BitTorrent DHT Protocol 51413 51413     
 1203 12.985586807 192.168.73.132 → 82.235.49.147 BT-DHT 62 BitTorrent DHT Protocol[Malformed Packet] 51413 16881     
 1205 12.985676887 192.168.73.132 → 5.135.186.3  BT-DHT 62 BitTorrent DHT Protocol[Malformed Packet] 51413 51413     
 1208 12.997146137 82.235.49.147 → 192.168.73.132 BT-DHT 122 BitTorrent DHT Protocol 16881 51413     
 1212 13.031737579 192.168.73.132 → 172.93.101.97 BT-DHT 100 BitTorrent DHT Protocol 51413 27350     
 1214 13.049380204 192.168.73.132 → 91.132.136.51 BT-DHT 62 BitTorrent DHT Protocol[Malformed Packet] 51413 25818     
 1218 13.062444560 172.93.101.97 → 192.168.73.132 BT-DHT 122 BitTorrent DHT Protocol 27350 51413     
 1220 13.089164092 192.168.73.132 → 46.234.155.66 BT-DHT 62 BitTorrent DHT Protocol[Malformed Packet] 51413 39042     
 1223 13.149388570 46.234.155.66 → 192.168.73.132 BT-DHT 122 BitTorrent DHT Protocol 39042 51413     
 1226 13.149449542 82.235.49.147 → 192.168.73.132 BT-DHT 165 BitTorrent DHT Protocol[Malformed Packet] 16881 51413     
 1228 13.160297387 192.168.73.132 → 172.93.101.97 BT-DHT 62 BitTorrent DHT Protocol[Malformed Packet] 51413 27350     
 1230 13.193650235 172.93.101.97 → 192.168.73.132 BT-DHT 369 BitTorrent DHT Protocol[Malformed Packet] 27350 51413     
 1233 13.211964106 46.234.155.66 → 192.168.73.132 BT-uTP 370 uTorrent Transport Protocol Type: Data 39042 51413     
 1235 13.266790391 192.168.73.132 → 82.235.49.147 BT-DHT 62 BitTorrent DHT Protocol[Malformed Packet] 51413 16881     
 1238 13.306178060 192.168.73.132 → 64.137.166.8 BT-uTP 474 uTorrent Transport Protocol Type: Data 51413 37164     
 1243 13.306330172 192.168.73.132 → 37.44.103.128 BT-DHT 509 BitTorrent DHT Protocol[Malformed Packet] 51413 21650     
 1245 13.306368685 192.168.73.132 → 188.6.7.124  BT-DHT 509 BitTorrent DHT Protocol[Malformed Packet] 51413 50402     
 1255 13.306657462 192.168.73.132 → 185.205.109.41 BT-DHT 62 BitTorrent DHT Protocol[Malformed Packet] 51413 51412     
 1256 13.306697629 192.168.73.132 → 79.146.67.82 BT-DHT 62 BitTorrent DHT Protocol[Malformed Packet] 51413 6882     
 1260 13.319632610 192.168.73.132 → 172.93.101.97 BT-DHT 62 BitTorrent DHT Protocol[Malformed Packet] 51413 27350     
 1287 13.434796654 185.205.109.41 → 192.168.73.132 BT-DHT 62 BitTorrent DHT Protocol[Malformed Packet] 51412 51413     
 1293 13.441857040 79.146.67.82 → 192.168.73.132 BT-DHT 62 BitTorrent DHT Protocol[Malformed Packet] 6882 51413     
 1295 13.444343220  188.6.7.124 → 192.168.73.132 BT-DHT 62 BitTorrent DHT Protocol[Malformed Packet] 50402 51413     
 1296 13.444382202  188.6.7.124 → 192.168.73.132 BT-DHT 112 BitTorrent DHT Protocol[Malformed Packet] 50402 51413     
 1300 13.454637758 37.44.103.128 → 192.168.73.132 BT-DHT 62 BitTorrent DHT Protocol[Malformed Packet] 21650 51413     
 1303 13.456401759  188.6.7.124 → 192.168.73.132 BT-DHT 590 BitTorrent DHT Protocol[Malformed Packet] 50402 51413     
 1304 13.456410812  188.6.7.124 → 192.168.73.132 BT-uTP 1514 uTorrent Transport Protocol Type: Data 50402 51413     
 1312 13.471726890 37.44.103.128 → 192.168.73.132 BT-DHT 112 BitTorrent DHT Protocol[Malformed Packet] 21650 51413     
 1316 13.481446956 37.44.103.128 → 192.168.73.132 BT-DHT 590 BitTorrent DHT Protocol[Malformed Packet] 21650 51413     
 1317 13.481496167 37.44.103.128 → 192.168.73.132 BT-uTP 590 uTorrent Transport Protocol Type: Data 21650 51413     
 1325 13.483656195 192.168.73.132 → 176.114.244.93 BT-DHT 100 BitTorrent DHT Protocol 51413 6881     
 1332 13.499021680 192.168.73.132 → 172.93.101.162 BT-DHT 100 BitTorrent DHT Protocol 51413 9146     
 1333 13.512852544 172.93.101.162 → 192.168.73.132 BT-uTP 590 uTorrent Transport Protocol Type: Data 9146 51413     
 1335 13.518276468 54.247.69.34 → 192.168.73.132 BT-DHT 100 BitTorrent DHT Protocol 33024 51413     
 1336 13.518307317 54.247.69.34 → 192.168.73.132 BT-DHT 100 BitTorrent DHT Protocol 32656 51413     
 1337 13.518309173 54.247.69.34 → 192.168.73.132 BT-DHT 165 BitTorrent DHT Protocol 30283 51413     
 1338 13.518310166 54.247.69.34 → 192.168.73.132 BT-DHT 100 BitTorrent DHT Protocol 33640 51413     
 1339 13.518407416 192.168.73.132 → 54.247.69.34 BT-DHT 91 BitTorrent DHT Protocol 51413 33024     
 1340 13.518455910 192.168.73.132 → 54.247.69.34 BT-DHT 91 BitTorrent DHT Protocol 51413 32656     
 1341 13.518483924 192.168.73.132 → 54.247.69.34 BT-DHT 306 BitTorrent DHT Protocol reply=8 nodes  51413 30283     
 1342 13.518516576 192.168.73.132 → 54.247.69.34 BT-DHT 91 BitTorrent DHT Protocol 51413 33640     
 1369 13.588466356 192.168.73.132 → 176.114.244.93 BT-DHT 62 BitTorrent DHT Protocol[Malformed Packet] 51413 6881     
 1374 13.611396191 176.114.244.93 → 192.168.73.132 BT-DHT 122 BitTorrent DHT Protocol 6881 51413     
 1403 13.686737268 192.168.73.132 → 209.169.85.88 BT-DHT 100 BitTorrent DHT Protocol 51413 54765     
 1447 13.731584310 176.114.244.93 → 192.168.73.132 BT-DHT 256 BitTorrent DHT Protocol[Malformed Packet] 6881 51413     
 1449 13.743637938 209.169.85.88 → 192.168.73.132 BT-DHT 122 BitTorrent DHT Protocol 54765 51413     
 1454 13.762269186 192.168.73.132 → 96.44.144.114 BT-DHT 100 BitTorrent DHT Protocol 51413 6881     
 1456 13.766779968 192.168.73.132 → 91.152.239.46 BT-DHT 100 BitTorrent DHT Protocol 51413 65453     
 1470 13.802873179 192.168.73.132 → 80.243.101.96 BT-DHT 135 BitTorrent DHT Protocol[Malformed Packet] 51413 51413     
 1476 13.803277976 192.168.73.132 → 82.235.49.147 BT-uTP 448 uTorrent Transport Protocol Type: Data 51413 16881     
 1478 13.803417923 192.168.73.132 → 86.59.144.16 BT-DHT 135 BitTorrent DHT Protocol[Malformed Packet] 51413 64194     
 1483 13.803630995 192.168.73.132 → 77.108.222.246 BT-DHT 399 BitTorrent DHT Protocol[Malformed Packet] 51413 6881     
 1486 13.803818839 192.168.73.132 → 5.135.186.3  BT-uTP 448 uTorrent Transport Protocol Type: Data 51413 51413     
 1492 13.804163054 192.168.73.132 → 172.93.101.97 BT-uTP 448 uTorrent Transport Protocol Type: Data 51413 27350     
 1509 13.822614157 192.168.73.132 → 209.169.85.88 BT-DHT 62 BitTorrent DHT Protocol[Malformed Packet] 51413 54765     
 1586 13.885983599 209.169.85.88 → 192.168.73.132 BT-uTP 165 uTorrent Transport Protocol Type: Data 54765 51413     
 1587 13.891232052 212.96.69.84 → 192.168.73.132 BT-DHT 146 BitTorrent DHT Protocol 42291 51413     
 1589 13.891554924 192.168.73.132 → 212.96.69.84 BT-DHT 325 BitTorrent DHT Protocol reply=8 nodes  51413 42291     
 1603 13.899095199 192.168.73.132 → 91.152.239.46 BT-DHT 62 BitTorrent DHT Protocol[Malformed Packet] 51413 65453     
 1604 13.899223324 192.168.73.132 → 176.114.244.93 BT-DHT 62 BitTorrent DHT Protocol[Malformed Packet] 51413 6881     
 1605 13.899706232 91.152.239.46 → 192.168.73.132 BT-DHT 122 BitTorrent DHT Protocol 65453 51413     
 1621 13.948557455 86.59.144.16 → 192.168.73.132 BT-DHT 62 BitTorrent DHT Protocol[Malformed Packet] 64194 51413     
 1622 13.948581544 86.59.144.16 → 192.168.73.132 BT-uTP 590 uTorrent Transport Protocol Type: Data 64194 51413     
 1642 14.016439658 77.108.222.246 → 192.168.73.132 BT-DHT 62 BitTorrent DHT Protocol[Malformed Packet] 6881 51413     
 1644 14.016451188 77.108.222.246 → 192.168.73.132 BT-uTP 107 uTorrent Transport Protocol Type: Data 6881 51413     
 1718 14.035172436 91.152.239.46 → 192.168.73.132 BT-DHT 172 BitTorrent DHT Protocol[Malformed Packet] 65453 51413     
 1721 14.035185453 80.243.101.96 → 192.168.73.132 BT-uTP 1444 uTorrent Transport Protocol Type: Data 51413 51413     
 1739 14.037012941 192.168.73.132 → 37.148.145.12 BT-DHT 100 BitTorrent DHT Protocol 51413 18167     
 1777 14.152842105 192.168.73.132 → 37.148.145.12 BT-DHT 62 BitTorrent DHT Protocol[Malformed Packet] 51413 18167     
 1779 14.153067701 192.168.73.132 → 91.152.239.46 BT-DHT 62 BitTorrent DHT Protocol[Malformed Packet] 51413 65453     
 1843 14.180549828 37.148.145.12 → 192.168.73.132 BT-DHT 122 BitTorrent DHT Protocol 18167 51413     
 1867 14.234778242 192.168.73.132 → 144.76.78.198 BT-DHT 100 BitTorrent DHT Protocol 51413 53415     
 1924 14.300252200 37.148.145.12 → 192.168.73.132 BT-uTP 165 uTorrent Transport Protocol Type: Data 18167 51413     
 1969 14.361076380 144.76.78.198 → 192.168.73.132 BT-DHT 122 BitTorrent DHT Protocol 53415 51413     
 1991 14.381778708 192.168.73.132 → 144.76.78.198 BT-DHT 62 BitTorrent DHT Protocol[Malformed Packet] 51413 53415     
 2173 14.478297420 192.168.73.132 → 173.88.171.180 BT-DHT 100 BitTorrent DHT Protocol 51413 41992     
 2196 14.500946353 192.168.73.132 → 176.63.21.177 BT-DHT 100 BitTorrent DHT Protocol 51413 38955     
 2197 14.508362219 144.76.78.198 → 192.168.73.132 BT-uTP 172 uTorrent Transport Protocol Type: Data 53415 51413     
 2267 14.531850725 192.168.73.132 → 104.254.90.235 BT-DHT 100 BitTorrent DHT Protocol 51413 58467     
 2355 14.588961537 104.254.90.235 → 192.168.73.132 BT-DHT 122 BitTorrent DHT Protocol 58467 51413     
 2357 14.598136788 192.168.73.132 → 173.88.171.180 BT-DHT 62 BitTorrent DHT Protocol[Malformed Packet] 51413 41992     
 2547 14.671712656 173.88.171.180 → 192.168.73.132 BT-uTP 215 uTorrent Transport Protocol Type: Data 41992 51413     
 2553 14.679902151 192.168.73.132 → 104.254.90.235 BT-DHT 62 BitTorrent DHT Protocol[Malformed Packet] 51413 58467     
 2573 14.720365282 192.168.73.132 → 77.123.11.140 BT-DHT 100 BitTorrent DHT Protocol 51413 13797     
 2607 14.731311575 104.254.90.235 → 192.168.73.132 BT-uTP 268 uTorrent Transport Protocol Type: Data 58467 51413     
 2894 14.842332952 192.168.73.132 → 77.123.11.140 BT-uTP 62 uTorrent Transport Protocol Type: State 51413 13797     
 3057 14.920998168 192.168.73.132 → 82.253.50.47 BT-DHT 100 BitTorrent DHT Protocol 51413 36957     
 3407 15.035981797 192.168.73.132 → 82.253.50.47 BT-DHT 62 BitTorrent DHT Protocol[Malformed Packet] 51413 36957     
 3499 15.161592412 192.168.73.132 → 51.235.34.19 BT-DHT 100 BitTorrent DHT Protocol 51413 6881     
 3670 15.227541655 192.168.73.132 → 62.42.97.136 BT-DHT 100 BitTorrent DHT Protocol 51413 40441     
 3676 15.281366335 192.168.73.132 → 51.235.34.19 BT-DHT 62 BitTorrent DHT Protocol[Malformed Packet] 51413 6881     
 3965 15.342023504 192.168.73.132 → 62.42.97.136 BT-DHT 62 BitTorrent DHT Protocol[Malformed Packet] 51413 40441     
 3968 15.356497014 51.235.34.19 → 192.168.73.132 BT-DHT 122 BitTorrent DHT Protocol 6881 51413     
 3999 15.367739447 114.35.63.17 → 192.168.73.132 BT-DHT 157 BitTorrent DHT Protocol 9502 51413     
 4000 15.367844831 192.168.73.132 → 114.35.63.17 BT-DHT 325 BitTorrent DHT Protocol reply=8 nodes  51413 9502     
 4320 15.446620279 62.42.97.136 → 192.168.73.132 BT-DHT 122 BitTorrent DHT Protocol 40441 51413     
 4754 15.588924718 51.235.34.19 → 192.168.73.132 BT-DHT 552 BitTorrent DHT Protocol[Malformed Packet] 6881 51413     
 5030 15.638155410 62.42.97.136 → 192.168.73.132 BT-uTP 286 uTorrent Transport Protocol Type: Data 40441 51413     
 5300 15.708108034 192.168.73.132 → 51.235.34.19 BT-DHT 62 BitTorrent DHT Protocol[Malformed Packet] 51413 6881     
 5336 15.713470577 192.168.73.132 → 136.35.186.94 BT-DHT 100 BitTorrent DHT Protocol 51413 61434     
 5386 15.727170172 82.253.50.47 → 192.168.73.132 BT-DHT 122 BitTorrent DHT Protocol 36957 51413     
 5414 15.735493097 82.253.50.47 → 192.168.73.132 BT-uTP 165 uTorrent Transport Protocol Type: Data 36957 51413     
 5545 15.761359060 136.35.186.94 → 192.168.73.132 BT-DHT 110 BitTorrent DHT Protocol 61434 51413     
 5862 15.803150645 192.168.73.132 → 91.132.136.51 BT-DHT 448 BitTorrent DHT Protocol[Malformed Packet] 51413 25818     
 5870 15.803347093 192.168.73.132 → 176.114.244.93 BT-uTP 443 uTorrent Transport Protocol Type: Data 51413 6881     
 5873 15.803464449 192.168.73.132 → 91.152.239.46 BT-uTP 443 uTorrent Transport Protocol Type: Data 51413 65453     
 5888 15.803636652 192.168.73.132 → 51.235.34.19 BT-uTP 443 uTorrent Transport Protocol Type: Data 51413 6881     
 6016 15.841807775 192.168.73.132 → 136.35.186.94 BT-DHT 62 BitTorrent DHT Protocol[Malformed Packet] 51413 61434     
 7143 16.052886222 91.132.136.51 → 192.168.73.132 BT-DHT 62 BitTorrent DHT Protocol[Malformed Packet] 25818 51413     
 7162 16.057477597 91.132.136.51 → 192.168.73.132 BT-DHT 91 BitTorrent DHT Protocol[Malformed Packet] 25818 51413     
 7462 16.106820019 192.168.73.132 → 105.98.42.105 BT-DHT 100 BitTorrent DHT Protocol 51413 54859     
 7940 16.178860928 192.168.73.132 → 91.132.136.51 BT-DHT 62 BitTorrent DHT Protocol[Malformed Packet] 51413 25818     
 8397 16.250137227 192.168.73.132 → 105.98.42.105 BT-DHT 62 BitTorrent DHT Protocol[Malformed Packet] 51413 54859     
10874 16.509341354 91.132.136.51 → 192.168.73.132 BT-DHT 78 BitTorrent DHT Protocol[Malformed Packet] 25818 51413     
12066 16.609652128 192.168.73.132 → 91.132.136.51 BT-DHT 62 BitTorrent DHT Protocol[Malformed Packet] 51413 25818     
15123 16.886298413 105.98.42.105 → 192.168.73.132 BT-DHT 122 BitTorrent DHT Protocol 54859 51413     
15124 16.886421563 192.168.73.132 → 185.12.227.197 BT-DHT 136 BitTorrent DHT Protocol 51413 3763     
16239 17.008801142 105.98.42.105 → 192.168.73.132 BT-uTP 552 uTorrent Transport Protocol Type: Data 54859 51413     
25176 17.802930095 192.168.73.132 → 136.35.186.94 BT-uTP 524 uTorrent Transport Protocol Type: Data 51413 61434     
32500 18.376719182 192.168.73.132 → 188.232.10.112 BT-DHT 100 BitTorrent DHT Protocol 51413 51413     
33965 18.526578703 192.168.73.132 → 188.232.10.112 BT-DHT 62 BitTorrent DHT Protocol[Malformed Packet] 51413 51413     
36047 18.777347266 5.189.157.90 → 192.168.73.132 BT-DHT 139 BitTorrent DHT Protocol 12057 51413     
36060 18.777685557 192.168.73.132 → 5.189.157.90 BT-DHT 327 BitTorrent DHT Protocol reply=8 nodes  51413 12057     
36377 18.802297541 192.168.73.132 → 188.232.10.112 BT-uTP 961 uTorrent Transport Protocol Type: Data 51413 51413     
41639 19.266624310 188.232.10.112 → 192.168.73.132 BT-DHT 91 BitTorrent DHT Protocol 51413 51413     
41920 19.287101929 188.232.10.112 → 192.168.73.132 BT-DHT 62 BitTorrent DHT Protocol[Malformed Packet] 51413 51413     
47877 19.922378992 192.168.73.132 → 138.197.143.248 BT-DHT 100 BitTorrent DHT Protocol 51413 50367     
49008 20.075652758 192.168.73.132 → 138.197.143.248 BT-DHT 62 BitTorrent DHT Protocol[Malformed Packet] 51413 50367     
49408 20.195734842 138.197.143.248 → 192.168.73.132 BT-DHT 122 BitTorrent DHT Protocol 50367 51413     
50087 20.197595478 138.197.143.248 → 192.168.73.132 BT-DHT 165 BitTorrent DHT Protocol[Malformed Packet] 50367 51413     
50461 20.302260834 192.168.73.132 → 138.197.143.248 BT-uTP 713 uTorrent Transport Protocol Type: Data 51413 50367     
50464 20.316964911 188.232.10.112 → 192.168.73.132 BT-DHT 427 BitTorrent DHT Protocol[Malformed Packet] 51413 51413     
50703 20.439517762 192.168.73.132 → 188.232.10.112 BT-DHT 62 BitTorrent DHT Protocol[Malformed Packet] 51413 51413     
51080 20.689763723 192.168.73.132 → 107.181.231.146 BT-DHT 139 BitTorrent DHT Protocol 51413 2169     
51081 20.689807803 192.168.73.132 → 159.89.144.30 BT-DHT 139 BitTorrent DHT Protocol 51413 6881     
51082 20.689828638 192.168.73.132 → 18.190.61.127 BT-DHT 139 BitTorrent DHT Protocol 51413 6881     
51178 20.747917305 107.181.231.146 → 192.168.73.132 BT-DHT 111 BitTorrent DHT Protocol reply=0 nodes  2169 51413     
51179 20.748056557 192.168.73.132 → 77.183.44.118 BT-DHT 139 BitTorrent DHT Protocol 51413 6881     
51211 20.776208734 159.89.144.30 → 192.168.73.132 BT-DHT 111 BitTorrent DHT Protocol reply=0 nodes  6881 51413     
51212 20.776335262 192.168.73.132 → 181.114.168.101 BT-DHT 139 BitTorrent DHT Protocol 51413 38355     
51463 20.883206268 77.183.44.118 → 192.168.73.132 BT-DHT 354 BitTorrent DHT Protocol reply=8 nodes  6881 51413     
51464 20.883349377 192.168.73.132 → 37.187.123.154 BT-DHT 139 BitTorrent DHT Protocol 51413 51413     
51518 20.909311232 181.114.168.101 → 192.168.73.132 BT-DHT 361 BitTorrent DHT Protocol reply=8 nodes  38355 51413     
51519 20.909443842 192.168.73.132 → 5.167.155.85 BT-DHT 139 BitTorrent DHT Protocol 51413 44256     
51678 20.971741280 37.187.123.154 → 192.168.73.132 BT-DHT 327 BitTorrent DHT Protocol reply=8 nodes  51413 51413     
51679 20.971791283 192.168.73.132 → 92.30.74.80  BT-DHT 139 BitTorrent DHT Protocol 51413 50231     
51881 21.067374281  92.30.74.80 → 192.168.73.132 BT-DHT 379 BitTorrent DHT Protocol reply=8 nodes reply=1 peers  50231 51413     
51883 21.067610254 192.168.73.132 → 141.98.252.166 BT-DHT 139 BitTorrent DHT Protocol 51413 32532     
51885 21.068390653 5.167.155.85 → 192.168.73.132 BT-DHT 361 BitTorrent DHT Protocol reply=8 nodes  44256 51413     
51886 21.068618951 192.168.73.132 → 178.45.34.11 BT-DHT 139 BitTorrent DHT Protocol 51413 11459     
52100 21.163989351 141.98.252.166 → 192.168.73.132 BT-DHT 500 BitTorrent DHT Protocol reply=8 nodes reply=17 peers  32532 51413     
52103 21.164086531 192.168.73.132 → 5.53.229.134 BT-DHT 139 BitTorrent DHT Protocol 51413 33424     
52297 21.238307577 178.45.34.11 → 192.168.73.132 BT-DHT 372 BitTorrent DHT Protocol reply=8 nodes reply=1 peers  11459 51413     
52298 21.238385537 192.168.73.132 → 185.137.175.94 BT-DHT 139 BitTorrent DHT Protocol 51413 51413     
52442 21.318528675 5.53.229.134 → 192.168.73.132 BT-DHT 349 BitTorrent DHT Protocol reply=8 nodes  33424 51413     
52443 21.318654412 192.168.73.132 → 79.6.179.56  BT-DHT 139 BitTorrent DHT Protocol 51413 6889     
52495 21.354587495 185.137.175.94 → 192.168.73.132 BT-DHT 327 BitTorrent DHT Protocol reply=8 nodes  51413 51413     
52497 21.354794488 192.168.73.132 → 75.81.99.69  BT-DHT 139 BitTorrent DHT Protocol 51413 50321     
52727 21.448674974  75.81.99.69 → 192.168.73.132 BT-DHT 380 BitTorrent DHT Protocol reply=8 nodes reply=2 peers  50321 51413     
52728 21.448765976 192.168.73.132 → 73.141.191.74 BT-DHT 139 BitTorrent DHT Protocol 51413 50321     
52748 21.457573966  79.6.179.56 → 192.168.73.132 BT-DHT 370 BitTorrent DHT Protocol reply=8 nodes reply=2 peers  6889 51413     
52750 21.457673439 192.168.73.132 → 185.21.216.144 BT-DHT 139 BitTorrent DHT Protocol 51413 59332     
52997 21.558654923 73.141.191.74 → 192.168.73.132 BT-DHT 354 BitTorrent DHT Protocol reply=8 nodes  50321 51413     
53000 21.558744338 192.168.73.132 → 185.21.216.144 BT-DHT 139 BitTorrent DHT Protocol 51413 58029     
53003 21.559401518 185.21.216.144 → 192.168.73.132 BT-DHT 412 BitTorrent DHT Protocol reply=8 nodes reply=6 peers  59332 51413     
53004 21.559485284 192.168.73.132 → 93.183.220.117 BT-DHT 139 BitTorrent DHT Protocol 51413 36868     
53120 21.606706709 18.190.61.127 → 192.168.73.132 BT-DHT 120 BitTorrent DHT Protocol reply=0 nodes  6881 51413     
53121 21.606834813 192.168.73.132 → 203.63.191.254 BT-DHT 139 BitTorrent DHT Protocol 51413 6881     
53286 21.661200551 185.21.216.144 → 192.168.73.132 BT-DHT 460 BitTorrent DHT Protocol reply=8 nodes reply=12 peers  58029 51413     
53293 21.661333748 192.168.73.132 → 83.251.164.175 BT-DHT 139 BitTorrent DHT Protocol 51413 11640     
53437 21.708716956 93.183.220.117 → 192.168.73.132 BT-DHT 452 BitTorrent DHT Protocol reply=8 nodes reply=11 peers  36868 51413     
53443 21.708851452 192.168.73.132 → 222.117.54.145 BT-DHT 139 BitTorrent DHT Protocol 51413 51413     
53681 21.801507666 83.251.164.175 → 192.168.73.132 BT-DHT 587 BitTorrent DHT Protocol reply=8 nodes reply=27 peers  11640 51413     
53682 21.801628138 192.168.73.132 → 61.147.59.154 BT-DHT 139 BitTorrent DHT Protocol 51413 51413     
53922 21.857492339 203.63.191.254 → 192.168.73.132 BT-DHT 506 BitTorrent DHT Protocol reply=8 nodes reply=19 peers  6881 51413     
53929 21.857749151 192.168.73.132 → 87.74.225.9  BT-DHT 139 BitTorrent DHT Protocol 51413 63405     
54075 21.921514230 222.117.54.145 → 192.168.73.132 BT-DHT 633 BitTorrent DHT Protocol reply=8 nodes reply=37 peers  51413 51413     
54076 21.921602048 192.168.73.132 → 157.45.224.155 BT-DHT 139 BitTorrent DHT Protocol 51413 49640     
54261 21.968371300  87.74.225.9 → 192.168.73.132 BT-DHT 764 BitTorrent DHT Protocol reply=8 nodes reply=50 peers  63405 51413     
54266 21.968537279 192.168.73.132 → 39.50.21.72  BT-DHT 139 BitTorrent DHT Protocol 51413 6881     
54522 22.161979304 61.147.59.154 → 192.168.73.132 BT-DHT 433 BitTorrent DHT Protocol reply=8 nodes reply=12 peers  51413 51413     
54647 22.163300442 192.168.73.132 → 139.210.21.72 BT-DHT 139 BitTorrent DHT Protocol 51413 16316     
56119 22.753127510  39.50.21.72 → 192.168.73.132 BT-DHT 812 BitTorrent DHT Protocol reply=8 nodes reply=56 peers  6881 51413     
56120 22.753261489 192.168.73.132 → 179.198.206.25 BT-DHT 139 BitTorrent DHT Protocol 51413 25311     
56913 22.997520568 179.198.206.25 → 192.168.73.132 BT-DHT 1051 BitTorrent DHT Protocol reply=8 nodes reply=85 peers  25311 51413     
56914 22.997661846 192.168.73.132 → 153.225.15.139 BT-DHT 139 BitTorrent DHT Protocol 51413 8999     
57427 23.187652619 153.225.15.139 → 192.168.73.132 BT-DHT 1164 BitTorrent DHT Protocol reply=8 nodes reply=100 peers  8999 51413     
57448 23.188867642 192.168.73.132 → 177.51.65.1  BT-DHT 139 BitTorrent DHT Protocol 51413 29794     
57857 23.306470659 192.168.73.132 → 188.232.10.112 BT-uTP 279 uTorrent Transport Protocol Type: Data 51413 51413 
~~~

This provides the torrent packet details.  We can identify the unique strings using tshark and sort:

~~~shell
$ tshark -r torrent.pcap -Y "bt-dht" -T fields -e bt-dht.bencoded.string | sort --unique

a,id,078e187bd1d82033f572e8294f9e0453a668cbc8,info_hash,078e18df4efe53eb39d3425e91d1e9f4777d85ac,q,get_peers,t,7c56,v,4c540102,y,q
a,id,0a8c3892819b5045dacc9b1174bbf1047219c684,info_hash,17c0c2c3b7825ba4fbe2f8c8055e000421def12c,noseed,q,get_peers,t,dbb2,v,4c540100,y,q
a,id,17c1ec414b95fc775d7dddcb686693b7863ac1aa,info_hash,e2467cbf021192c241367b892230dc1e05c0580e,q,get_peers,t,6770c723,y,q
a,id,17c1ec414b95fc775d7dddcb686693b7863ac1aa,q,ping,t,706e0000,y,q
a,id,17c1ec414b95fc775d7dddcb686693b7863ac1aa,target,17c19b483ab389824c227ab03832b8e9b603ee90,q,find_node,t,666e0000,y,q
a,id,17c1fb5e7e0ffdb4890fd88121f2634d9889a778,target,17c1fb5e7e0ffdb4890fd88121f2634d9889a778,q,find_node,t,f4a4,v,4c540010,y,q
a,id,320614d6ae529049f1f1bbe9ebb3a6db3c870ce1,implied_port,info_hash,17c1e42e811a83f12c697c21bed9c72b5cb3000d,name,Zoo (2017) 720p WEB-DL x264 ESubs - MkvHub.Com,port,seed,token,cfd76f718b52c968,q,announce_peer,t,ce300000,v,5554b206,y,q
a,id,7af66b61085da78cd4ad2771f2a2a65b79fe1c06,info_hash,7af6be54c2ed4dcb8d17bf599516b97bb66c0bfd,q,get_peers,t,165d,v,4c540101,y,q
a,id,99a047b561fc2b3e22dedcc23a7a237fcbd6c47b,info_hash,17d62de1495d4404f6fb385bdfd7ead5c897ea22,q,get_peers,t,ce83d90f,y,q
a,id,c8e1fb9368b62f6c04838748c83a8ce01ced7cbb,info_hash,17c02f9957ea8604bc5a04ad3b56766a092b5556,q,get_peers,t,94f3c30f,y,q
a,id,e29d2ea7482421b50f55b44da26352f28666ce57,info_hash,d59b1ce3bf41f1d282c1923544629062948afadd,q,get_peers,t,27e1,v,4c540102,y,q
ip,80ed85aee7f5,r,id,00f1ab55c3903f5c4ae598ddcd858d2f57a9523c,p,t,706e0000,v,4c540101,y,r
ip,80ed85aee7f5,r,id,05200df5f5eaadb1116381a973f5eb0d9f8a26e9,p,t,706e0000,v,4c540102,y,r
ip,80ed85aee7f5,r,id,0619137438100cbac1bed58df4be31a54e9394de,p,t,706e0000,v,4c540101,y,r
ip,80ed85aee7f5,r,id,0c0a4825bf5ed3f71538d325ba026be05d57eedc,p,t,706e0000,v,4c540102,y,r
ip,80ed85aee7f5,r,id,0f10f63493adea40cf58360cd388944f1a7683bc,p,t,706e0000,v,4c540102,y,r
ip,80ed85aee7f5,r,id,171a04fc9d9ad42ec9fbac7ef27a505c8b49dca9,p,t,706e0000,v,4c540101,y,r
ip,80ed85aee7f5,r,id,1b4ac796447b59a5318c6074f2c94e142c62b7dc,p,t,706e0000,v,4c540102,y,r
ip,80ed85aee7f5,r,id,1cf9ac7a395b00abbbb60996b9fa92729ae21b42,p,t,706e0000,v,4c540102,y,r
ip,80ed85aee7f5,r,id,1ec76ebfdcf75f197fe654cfa28d8afd22932806,p,t,706e0000,v,4c540102,y,r
ip,80ed85aee7f5,r,id,204e022eb7c7e5ccf3367c24ea921bcd5dc578f1,p,t,706e0000,v,4c540102,y,r
ip,80ed85aee7f5,r,id,24c7233933aaa3fee76c87a532e220071a23322f,p,t,706e0000,v,4c540102,y,r
ip,80ed85aee7f5,r,id,46db14bdae6ad1dccafa5906ed01aa09ca5b12a0,p,t,706e0000,v,4c540102,y,r
ip,80ed85aee7f5,r,id,48255126de65a14f4516333c9ea58a2038770546,p,t,706e0000,v,4c540101,y,r
ip,80ed85aee7f5,r,id,4a75c93a7eb32c07155435c5dc934b7f380fa242,p,t,706e0000,v,4c540100,y,r
ip,80ed85aee7f5,r,id,4dbbfd0123c1df025de659289ac296081bdf2946,p,t,706e0000,v,4c540102,y,r
ip,80ed85aee7f5,r,id,667d3cf525b1a4d09c26dc489abeebf7f63ca6a3,nodes,p,token,a903909b,t,6770c723,v,4c540102,y,r
ip,80ed85aee7f5,r,id,7aa06ce86d7ea3539382394b655d82f3661d86a3,p,t,706e0000,v,4c540102,y,r
ip,80ed85aee7f5,r,id,836636032e8201b51fee20af2af54b66ca504aed,p,t,706e0000,v,4c540102,y,r
ip,80ed85aee7f5,r,id,8d21f6006d4fa894ca4f016a3fe55ec4876084a0,p,t,706e0000,v,4c540102,y,r
ip,80ed85aee7f5,r,id,a19a40367bb1670e3fcf9411b52c2099f910116a,p,t,706e0000,v,4c540102,y,r
ip,80ed85aee7f5,r,id,b1ae07a6430914d4df613af267c60b11634a566e,p,t,706e0000,v,4c540102,y,r
ip,80ed85aee7f5,r,id,bbc004d6ae529049f1f1bbe9ebb3a6db3c870ce1,nodes,token,97fad5fffb5d828f9ec3002267d0f98d05f82d47,t,6770c723,v,5554ad2c,y,r
ip,80ed85aee7f5,r,id,c00e9357ea7701d14abf51f8dc52fbf8da81264c,p,t,706e0000,v,4c540102,y,r
ip,80ed85aee7f5,r,id,c1e255aa5b5845a2c01fdf7bb408e6b93bf4df02,p,t,706e0000,v,4c540102,y,r
ip,80ed85aee7f5,r,id,d484cd1a73a8dbc0af6af0cda55858d6dc0b1367,p,t,706e0000,v,4c540102,y,r
ip,80ed85aee7f5,r,id,e155f549f1f1bbe9ebb3a6db3c870c3e99245e52,nodes,token,19d2d5d2d2cdbfb8246883eda972c0aff03afa5d,values,t,6770c723,v,5554b206,y,r
ip,80ed85aee7f5,r,id,e2428828524334f3bda896727347dc480ac51a89,nodes,token,1b323e34,values,t,6770c723,v,4c540010,y,r
ip,80ed85aee7f5,r,id,e242dae8b395ff2e19253a04cb9a558df7cc5794,nodes,p,token,1591c0e1,values,t,6770c723,v,4c540100,y,r
ip,80ed85aee7f5,r,id,e244568cef3e8600fa3c06896284492c1ad4f2f6,nodes,p,token,0bfee00f,t,6770c723,v,4c540100,y,r
ip,80ed85aee7f5,r,id,e2461b0c5b5d49185eb71c00ae237b22497d10cb,nodes,token,f95b0ffe,values,t,6770c723,v,4c540010,y,r
ip,80ed85aee7f5,r,id,e246221c31f5932989b43cb58afeba72f2295221,nodes,token,612c678177dd2a439968a7812a3052f4260b034f,values,t,6770c723,v,5554b1c1,y,r
ip,80ed85aee7f5,r,id,e24656c990918a7a6c97141268d2efb658eeb01a,nodes,p,token,b957bcb4,values,t,6770c723,v,4c540102,y,r
ip,80ed85aee7f5,r,id,e2465e11f159b59d6b8320c8e97c01914c37654f,nodes,p,token,721d158c,values,t,6770c723,v,4c540101,y,r
ip,80ed85aee7f5,r,id,e24661bb0d9bd62331576669bed6b35b948843e5,nodes,token,7c95592a8a89bbdd165aeefd79f9b4fcd27ce56a,values,t,6770c723,v,5554b1b8,y,r
ip,80ed85aee7f5,r,id,e2466d6bb1b564012061fe9ac6b21195314338d7,nodes,p,token,327cea0a,values,t,6770c723,v,4c540101,y,r
ip,80ed85aee7f5,r,id,e246cc7d830e257d7353ead1cdcd7736433460d2,nodes,p,token,b7ac83c7,values,t,6770c723,v,4c540100,y,r
ip,80ed85aee7f5,r,id,e247531663e5f30a8ecea78e30540d6107adb1bb,nodes,p,token,c0a86037,values,t,6770c723,v,4c540100,y,r
ip,80ed85aee7f5,r,id,e2475632ede1aca2245697c2e93b8ec3f563991b,nodes,p,token,cb9d003e,values,t,6770c723,v,4c540100,y,r
ip,80ed85aee7f5,r,id,e2ac0ff637727dee7e10db7c400f122b5163b929,nodes,p,token,3820880a,values,t,6770c723,v,4c540100,y,r
ip,80ed85aee7f5,r,id,e354d3a4d2b960e721c161fc4649a461a3c74617,nodes,p,token,e738ce89,values,t,6770c723,v,4c540101,y,r
ip,80ed85aee7f5,r,id,ea36476d10cfcc9c8997170d7f1b9d8535dfdfbe,nodes,token,9f2e87158fa1bceded694d44d6f90a2839742564,t,6770c723,v,5554b206,y,r
ip,80ed85aee7f5,r,id,ed6bf1c82dbf7747fd739c537b830067e2b37400,p,t,706e0000,v,4c540102,y,r
ip,80ed85aee7f5,r,id,ef5d3be36ac7115fa4ea0fcbc6d674c6bc1f15a5,p,t,706e0000,v,4c540102,y,r
ip,80ed85aee7f5,r,id,f15a11f1a82134b8ac8562b1163ada6cdcf6059c,p,t,706e0000,v,4c540102,y,r
ip,80ed85aee7f5,r,id,fa5986cb46b729580a7f249df502a96e475c3c49,p,t,706e0000,v,4c540102,y,r
ip,80ed85aee7f5,r,id,ff9e0fa58b94ba97a28db99b64c9f9567e63bb12,p,t,706e0000,v,4c540102,y,r
r,id,172c139ffaa5441d8ffee06882fadf697500a349,t,706e0000,v,6c740d60,y,r
r,id,17c1ec414b95fc775d7dddcb686693b7863ac1aa,nodes,t,2b5f,y,r
r,id,17c1ec414b95fc775d7dddcb686693b7863ac1aa,nodes,t,f4a4,y,r
r,id,17c1ec414b95fc775d7dddcb686693b7863ac1aa,nodes,token,00e95899a8515551,t,27e1,y,r
r,id,17c1ec414b95fc775d7dddcb686693b7863ac1aa,nodes,token,69dda0bbdf3298fe,t,7c56,y,r
r,id,17c1ec414b95fc775d7dddcb686693b7863ac1aa,nodes,token,9765b359d9039b0e,t,ce83d90f,y,r
r,id,17c1ec414b95fc775d7dddcb686693b7863ac1aa,nodes,token,b2ef20b457102370,t,94f3c30f,y,r
r,id,17c1ec414b95fc775d7dddcb686693b7863ac1aa,nodes,token,c7a4851980b17b17,t,dbb2,y,r
r,id,17c1ec414b95fc775d7dddcb686693b7863ac1aa,nodes,token,f5b9c053626f64f4,t,165d,y,r
r,id,17c1ec414b95fc775d7dddcb686693b7863ac1aa,nodes,t,r,id,17c1ec414b95fc775d7dddcb686693b7863ac1aa,nodes,t
r,id,17c1ec414b95fc775d7dddcb686693b7863ac1aa,t,306b308a,y,r
r,id,17c1ec414b95fc775d7dddcb686693b7863ac1aa,t,316b308a,y,r
r,id,17c1ec414b95fc775d7dddcb686693b7863ac1aa,t,326b308a,y,r
r,id,17c1ec414b95fc775d7dddcb686693b7863ac1aa,t,ce300000,y,r
r,id,21ee73ca32f939d1201597b8eabe2bab8b4de500,t,706e0000,y,r
r,id,276c9ab34f1cc36a3d50eda2d3b313eeeaeb62f5,t,706e0000,y,r
r,id,3264eaf8fa9dacfdce1c17142e4c406e05c00794,t,706e0000,y,r
r,id,5a0f14936a244aa0a264fb5cc119e1cc901c3abd,t,706e0000,y,r
r,id,67e66631c1ce415cf9b4a63c8163b197a9c3429f,t,706e0000,y,r
r,id,7245d77fbcd991d7d1be77563e31e7dc7ad986f1,t,706e0000,y,r
r,id,7b4a27233cb595d0352caea1deb1bf2e26f50f26,ip,t,706e0000,v,55546216,y,r
r,id,81572047c83a9cdde0f73a5311218c763c469192,t,706e0000,y,r
r,id,8de5979647307221f353bf4ec0b22ac501554988,t,706e0000,y,r
r,id,9b94c257e2628b4651769920a3045ef60beb2c0c,t,706e0000,y,r
r,id,b29d3d64b7bbba0aba790a153361acfbcac212a0,t,706e0000,y,r
r,id,bc3fe09494682c851daf634a5f76db5ed387041a,t,706e0000,y,r
r,id,c9a8c785e344510760f97754936e81eb6a8d25f3,t,706e0000,y,r
r,id,d23bec7eb1221b6d461d61e55ede0c3b191f8d9d,t,706e0000,y,r
r,id,e201187e24371030829459046e6656b4fecd9a67,nodes,token,9b3a5113ad3df492,t,6770c723,y,r
r,id,e21e7622109d856967adc9c0c85b2ab3980559e9,nodes,token,ca159822bb15e0a3d976a55325cd972cfdfa20ec,t,6770c723,v,55544b30,y,r
r,id,e246343af69cdb5427498f4b330d95aeee635fea,nodes,token,57d67c22a4a4d34a,values,t,6770c723,y,r
r,id,e2464e11deb97ffd721d64ae9ea3a961d9e3c385,nodes,token,6c70906437fa0103,values,t,6770c723,y,r
r,id,e2467cbf021192c241360021b4d995348cb3ae12,nodes,token,e246,t,6770c723,y,r
r,id,e2467cbf021192c2413635eb211cf1ba2ae528bb,nodes,token,e246,t,6770c723,y,r
r,id,e2467cbf021192c2413698c7de89f6dd5d090a62,nodes,token,e246,t,6770c723,v,4c540101,y,r
r,id,eed2305ba027ec18379a2a7dabb15945886520ec,nodes,token,f9caf8a3b3ce01f1,t,6770c723,y,r
t,306b308a,y,q,q,ping,a,id,e8d4a8566283e426c2e01f131c702332ca58e2d5
t,316b308a,y,q,q,ping,a,id,97ec09cbbece6c426ae638e896c2302d5f0795e8
t,326b308a,y,q,q,ping,a,id,5964b1c947ca1ba3a460a2e11079cbb19afdb9db
t,b9d937a013fbbe8ccb1b8d9b7b078eb6f250c12a,y,q,q,find_node,a,want,n4,id,2c731d3a24542f6f6e0914a658884265ba2916b0,target,b9d937a013fbbe8ccb1b8d9b7b078eb6f250c12a
~~~

Some of these packets have an info_hash field that will provide the hash of the transmitted file, these can be isolated using grep:

~~~shell
$ tshark -r torrent.pcap -Y "bt-dht" -T fields -e bt-dht.bencoded.string | sort --unique | grep info_hash
a,id,078e187bd1d82033f572e8294f9e0453a668cbc8,info_hash,078e18df4efe53eb39d3425e91d1e9f4777d85ac,q,get_peers,t,7c56,v,4c540102,y,q
a,id,0a8c3892819b5045dacc9b1174bbf1047219c684,info_hash,17c0c2c3b7825ba4fbe2f8c8055e000421def12c,noseed,q,get_peers,t,dbb2,v,4c540100,y,q
a,id,17c1ec414b95fc775d7dddcb686693b7863ac1aa,info_hash,e2467cbf021192c241367b892230dc1e05c0580e,q,get_peers,t,6770c723,y,q
a,id,320614d6ae529049f1f1bbe9ebb3a6db3c870ce1,implied_port,info_hash,17c1e42e811a83f12c697c21bed9c72b5cb3000d,name,Zoo (2017) 720p WEB-DL x264 ESubs - MkvHub.Com,port,seed,token,cfd76f718b52c968,q,announce_peer,t,ce300000,v,5554b206,y,q
a,id,7af66b61085da78cd4ad2771f2a2a65b79fe1c06,info_hash,7af6be54c2ed4dcb8d17bf599516b97bb66c0bfd,q,get_peers,t,165d,v,4c540101,y,q
a,id,99a047b561fc2b3e22dedcc23a7a237fcbd6c47b,info_hash,17d62de1495d4404f6fb385bdfd7ead5c897ea22,q,get_peers,t,ce83d90f,y,q
a,id,c8e1fb9368b62f6c04838748c83a8ce01ced7cbb,info_hash,17c02f9957ea8604bc5a04ad3b56766a092b5556,q,get_peers,t,94f3c30f,y,q
a,id,e29d2ea7482421b50f55b44da26352f28666ce57,info_hash,d59b1ce3bf41f1d282c1923544629062948afadd,q,get_peers,t,27e1,v,4c540102,y,q
~~~

We now have the following file hashes:

~~~
078e18df4efe53eb39d3425e91d1e9f4777d85ac
17c02f9957ea8604bc5a04ad3b56766a092b5556
17c0c2c3b7825ba4fbe2f8c8055e000421def12c
17c1e42e811a83f12c697c21bed9c72b5cb3000d
17d62de1495d4404f6fb385bdfd7ead5c897ea22
7af6be54c2ed4dcb8d17bf599516b97bb66c0bfd
d59b1ce3bf41f1d282c1923544629062948afadd
e2467cbf021192c241367b892230dc1e05c0580e
~~~


| hash                                     | file                                    | Type  |
|------------------------------------------|-----------------------------------------|-------|
| 078e18df4efe53eb39d3425e91d1e9f4777d85ac | UNK                                     | UNK   |
| 17c02f9957ea8604bc5a04ad3b56766a092b5556 | UNK                                     | UNK   |
| 17c0c2c3b7825ba4fbe2f8c8055e000421def12c | UNK                                     | UNK   |
| 17c1e42e811a83f12c697c21bed9c72b5cb3000d | Zoo (2017) 720p WEB-DL x264 700MB ESubs | Video |
| 17d62de1495d4404f6fb385bdfd7ead5c897ea22 | Awakened.2013.1080p.BluRay.X264-...     | Video |
| 7af6be54c2ed4dcb8d17bf599516b97bb66c0bfd | UNK                                     | UNK   |
| d59b1ce3bf41f1d282c1923544629062948afadd | UNK                                     | UNK   |
| e2467cbf021192c241367b892230dc1e05c0580e | ubuntu-19.10-desktop-amd64.iso          | iso   | 

We have found the iso we are looking for.

</details>

### Answer

<details>

<summary markdown="span">Flag</summary>

~~~
picoCTF{ubuntu-19.10-desktop-amd64.iso}
~~~

</details>

---

### [Forensics](#contents) | [PicoCTF](./picoctf.md) | [Home](./index.md)

---
	
Page last updated Jan 2022.

## [djm89uk.github.io](https://djm89uk.github.io)
