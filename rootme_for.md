# [Root-Me](./rootme.md) Root-Me Forensics [0/28]

Train digital investigation skills by analyzing memory dumps, log files, network captures...

## Contents

1. [Command & Control - level 2](#command-and-control-level-2)
2. [Logs analysis - web attack](#logs-analysis-web-attack)
3. [Command & Control - level 5](#command-control-level-5)
4. [Find the cat](#find-the-cat)
5. [Ugly Duckling](#ugly-duckling)
6. [Active Directory - GPO](#active-directory-gpo)
7. [Command & Control - level 3](#command-control-level-3)
8. [DNS exfiltration](#dns-exfiltration)
9. [Command & Control - level 4](#command-control-level-4)
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
20. [Command & Control - level 6](#command-control-level-6)
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

Last updated Jan 2022.

## [djm89uk.github.io](https://djm89uk.github.io)
