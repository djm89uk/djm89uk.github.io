# [PicoCTF](./picoctf.md) PicoGym Forensics

"Forensics" challenges can include file format analysis, steganography, memory dump analysis, or network packet capture analysis.

## Contents

- [Glory of the Garden (2019)](#glory-of-the-garden)
- [So Meta (2019)](#so-meta)
- [extensions (2019)](#extensions)
- [shark on wire 1 (2019)](#shark-on-wire-1)
- [What Lies Within (2019)](#what-lies-within)
- [c0rrupt (2019)](#c0rrupt)
- [WhitePages (2019)](#whitepages)
- [m00nwalk (2019)](#m00nwalk)
- [like1000 (2019)](#like1000)
- [shark on wire 2 (2019)](#shark-on-wire-2)
- [m00nwalk2 (2019)](#m00nwalk2)
- [Investigative Reversing 0 (2019)](#investigative-reversing-0)
- [WebNet0 (2019)](#webnet0)
- [Investigative Reversing 1 (2019)](#investigative-reversing-1)
- [Investigative Reversing 2 (2019)](#investigative-reversing-2)
- [Investigative Reversing 3 (2019)](#investigative-reversing-3)
- [Investigative Reversing 4 (2019)](#investigative-reversing-4)
- [investigation_encoded_1 (2019)](#investigation-encoded-1)
- [WebNet1 (2019)](#webnet1)
- [investigation_encoded_2 (2019)](#investigation-encoded-2)
- [B1g_Mac (2019)](#b1g-mac)
- [Pitter, Patter, Platters (2020)](#pitter-patter-platters)
- [Information (2021)](#information)
- [Matryoshka doll (2021)](#matryoshka-doll)
- [tunn3l v1s10n (2021)](#tunn3l-v1s10n)
- [Wireshark doo dooo do doo (2021)](#wireshark-doo-dooo-do-doo)
- [MacroHard WeakEdge (2021)](#macrohard-weakedge)
- [Trivial Flag Transfer Protocol (2021)](#trivial-flag-transfer-protocol)
- [Wireshark twoo twooo two twoo (2021)](#wireshark-twoo-twooo-two-twoo)
- [Disk, disk, sleuth! (2021)](#disk-disk-sleuth)
- [Milkslap (2021)](#milkslap)
- [Disk,disk, sleauth II (2021)](#disk-disk-sleuth-ii)
- [Surfing the Waves (2021)](#surfing-the-waves)
- [Very very very Hidden (2021)](#very-very-very-hidden)


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

We can import the mystery binary and decompile in Ghidra.  The main function is decompiled:

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
    iVar3 = local_10 + *(int *)(matrix + (long)(flag_char - 97) * 8);
    while (i < iVar3) {
      flag_int = getValue(i);
      save((byte)flag_int);
      i++;
    }
  }
}
~~~

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
decoded flag: picoCTF{the_m3tadata_1s_modified}
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

~~~
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

This gives us a full image with the flag:

~~~
picoCTF{qu1t3_a_v13w_2020}
~~~

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

~~~
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

Using this for the alphabetic characters we get:

~~~
picoCTF{p33kab00_1_s33_u_deadbeef}
~~~

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

This is likely the flag string encoded in base64.  Decoding online, we get:

~~~
flag: picoCTF{D1d_u_kn0w_ppts_r_z1p5}
~~~

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

~~~
instructions.txt:
GSGCQBRFAGRAPELCGBHEGENSSVPFBJRZHFGQVFTHVFRBHESYNTGENAFSRE.SVTHERBHGNJNLGBUVQRGURSYNTNAQVJVYYPURPXONPXSBEGURCYNA
TFTPDOESNTENCRYPTOURTRAFFICSOWEMUSTDISGUISEOURFLAGTRANSFER.FIGUREOUTAWAYTOHIDETHEFLAGANDIWILLCHECKBACKFORTHEPLAN
~~~

This provides the instruction: TFTP doesnt encrypt your traffic so we must disguise our flag transfer. Figure out a way to hide the flag and I will check back for the plan.

Similarly, for the plan file:

~~~
plan
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

We find a hidden file, flag.txt in the third bitmap.  We can view the contents of the flag.txt file to retrieve the flag:

~~~shell
$ cat flag.txt
picoCTF{h1dd3n_1n_pLa1n_51GHT_18375919}
~~~

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

This appears to be base64 which we can attempt to decode:

~~~
picoCTF{dns_3xf1l_ftw_deadbeef}
~~~

which is the flag.

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

This provides the flag hidden in /boot/syslinux.cfg:

~~~
picoCTF{f0r3ns1c4t0r_n30phyt3_267e38f6}
~~~

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

This gives us the flag:

~~~
picoCTF{f0r3ns1c4t0r_n0v1c3_0d9d9ecb}
~~~

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

~~~shell$ exiftool main.wav 
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

try_me.pcap

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


Page last updated 10 May 2021.

## [djm89uk.github.io](https://djm89uk.github.io)
