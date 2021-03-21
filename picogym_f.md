# [PicoCTF](./picoctf.md) PicoGym Forensics

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

~~~
$ strings mystery | grep pico  
~~~

This does not return anything.  The flag is likely encoded in the file.  Two simple strings commands can provide an inidication of the file type:

~~~
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

~~~
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

~~~
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

~~~
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

~~~
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

~~~
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

~~~
$ tcpdump -r capture.pcap -w capture_ip.pcap
$ editcap --novlan -d capture_ip.pcap capture_ip_no_replicas.pcap
$ tcpdump -r capture_ip_no_replicas.pcap -w capture_final.pcap tcp or udp
~~~

This has reduced the total capture size to 101 packets. Looking through the files, we do not see any useful contents:

~~~
$ tshark -r capture_final.pcap -z "follow,udp,ascii,1"
~~~

There are a lot of red herrings in the streams ("picoCTF{N0t_a_fLag}" in udp stream 6, "picoCTF{StaT315e" in udp stream 7, "picoCTF Sure is fun!" in udp stream 9, "I really want to find some picoCTF flags" in udp stream 10).  Reviewing the packet contents is not getting us anywhere.

We can try to export objects from the packet capture using tshark, for example to export imf objects we use:

~~~
$ tshark -r capture_final.pcap --export-objects imf,temp_folder
~~~

No objects are exported.  This challenge must use a more interesting method to hide the flag.

We can look at a summary of the capture using the command:

~~~
$ tshark -r capture_final.pcap
~~~

This shows a lot of information, not much use except there seems to be some strange ports in use.  We can review the tcp ports by filtering tshark and piping to sort and uniq:

~~~
$ tshark -r capture_final.pcap -Y "tcp" -T fields -e tcp.srcport -e tcp.dstport | sort | uniq
60218   80
80      60218
~~~

This shows ports 60218 and 80 are used for tcp conversations.  We can do the same for udp:

~~~
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

~~~
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

~~~
$ tshark -r capture_final.pcap -Y "udp" -T fields -e udp.srcport -Y udp.dstport==22 | awk '{print sprintf("%c",$1-5000)}' | tr -d '\n'
picoCTF{p1Lf3r3d_data_v1a_st3g0}
~~~

This gives us the flag picoCTF{p1Lf3r3d_data_v1a_st3g0}, which is again an incorrect flag due to packet loss in the file reduction.  reusing the above command on the original capture file:

~~~
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

~~~
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

The first 2000Bytes of the original bmp are copied directly into the encoded.bmp file.

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

~~~
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

### [Forensics](#contents) | [PicoCTF](./picoctf.md) | [Home](./index.md)

---

## [djm89uk.github.io](https://djm89uk.github.io)
