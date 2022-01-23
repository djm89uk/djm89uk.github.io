# [OverTheWire](./overthewire.md) Bandit

The Bandit wargame is aimed at absolute beginners. It will teach the basics needed to be able to play other wargames. 

## Contents

0. [Level 0](#level-0) 🗸
1. [Level 1](#level-1) 🗸
2. [Level 2](#level-2) 🗸
3. [Level 3](#level-3) 🗸
4. [Level 4](#level-4) 🗸
5. [Level 5](#level-5) 🗸
6. [Level 6](#level-6) 🗸
7. [Level 7](#level-7) 🗸
8. [Level 8](#level-8) 🗸
9. [Level 9](#level-9) 🗸
10. [Level 10](#level-10) 🗸
11. [Level 11](#level-11) 🗸
12. [Level 12](#level-12) 🗸
13. [Level 13](#level-13) 🗸
14. [Level 14](#level-14) 🗸
15. [Level 15](#level-15) 🗸
16. [Level 16](#level-16) 🗸
17. [Level 17](#level-17)
18. [Level 18](#level-18)
19. [Level 19](#level-19)
20. [Level 20](#level-20)
21. [Level 21](#level-21)
22. [Level 22](#level-22)
23. [Level 23](#level-23)
24. [Level 24](#level-24)
25. [Level 25](#level-25)
26. [Level 26](#level-26)
27. [Level 27](#level-27)
28. [Level 28](#level-28)
29. [Level 29](#level-29)
30. [Level 30](#level-30)
31. [Level 31](#level-31)
32. [Level 32](#level-32)
33. [Level 33](#level-33)
34. [Level 34](#level-34)

---

### [Bandit](#contents) | [OverTheWire](./overthewire.md) | [Home](./index.md)

---

## Level 0

The goal of this level is for you to log into the game using SSH. The host to which you need to connect is bandit.labs.overthewire.org, on port 2220. The username is bandit0 and the password is bandit0. Once logged in, go to the Level 1 page to find out how to beat Level 1.

### Solution

<details>

<summary markdown="span">Solution</summary>

~~~shell
$ sshpass -p "bandit0" ssh -p 2220 bandit0@bandit.labs.overthewire.org
~~~

</details>

## Level 1

The password for the next level is stored in a file called readme located in the home directory. Use this password to log into bandit1 using SSH. Whenever you find a password for a level, use SSH (on port 2220) to log into that level and continue the game.

### Solution

<details>

<summary markdown="span">Solution</summary>

~~~shell
bandit0@bandit:~$ ls
readme
bandit0@bandit:~$ cat readme 
boJ9jbbUNNfktd78OOpsqOltutMc3MY1
~~~

</details>

### Answer

<details>

<summary markdown="span">Flag</summary>

~~~
$ sshpass -p "boJ9jbbUNNfktd78OOpsqOltutMc3MY1" ssh -p 2220 bandit1@bandit.labs.overthewire.org
~~~

</details>

## Level 2

The password for the next level is stored in a file called - located in the home directory

### Solution

<details>

<summary markdown="span">Solution</summary>

~~~shell
bandit1@bandit:~$ ls
-
bandit1@bandit:~$ cat ./-
CV1DtqXWVFXTvM2F0k09SHz0YwRINYA9
~~~

</details>

### Answer

<details>

<summary markdown="span">Flag</summary>

~~~
$ sshpass -p "CV1DtqXWVFXTvM2F0k09SHz0YwRINYA9" ssh -p 2220 bandit2@bandit.labs.overthewire.org
~~~

</details>

## Level 3

The password for the next level is stored in a file called spaces in this filename located in the home directory

### Solution

<details>

<summary markdown="span">Solution</summary>

~~~shell
bandit2@bandit:~$ ls
spaces in this filename
bandit2@bandit:~$ cat spaces\ in\ this\ filename 
UmHadQclWmgdLOKQ3YNgjWxGoRMb5luK
~~~

</details>

### Answer

<details>

<summary markdown="span">Flag</summary>

~~~
$ sshpass -p "UmHadQclWmgdLOKQ3YNgjWxGoRMb5luK" ssh -p 2220 bandit3@bandit.labs.overthewire.org
~~~

</details>

## Level 4

The password for the next level is stored in a hidden file in the inhere directory.

### Solution

<details>

<summary markdown="span">Solution</summary>

~~~shell
bandit3@bandit:~$ ls
inhere
bandit3@bandit:~$ cd inhere/
bandit3@bandit:~/inhere$ ls -a
.  ..  .hidden
bandit3@bandit:~/inhere$ cat .hidden
pIwrPrtPN36QITSp3EQaw936yaFoFgAB
~~~

</details>

### Answer

<details>

<summary markdown="span">Flag</summary>

~~~
$ sshpass -p "pIwrPrtPN36QITSp3EQaw936yaFoFgAB" ssh -p 2220 bandit4@bandit.labs.overthewire.org
~~~

</details>

## Level 5

The password for the next level is stored in the only human-readable file in the inhere directory. Tip: if your terminal is messed up, try the “reset” command.

### Solution

<details>

<summary markdown="span">Solution</summary>

~~~shell
bandit4@bandit:~$ ls
inhere
bandit4@bandit:~$ cd inhere/
bandit4@bandit:~/inhere$ ls -a
.  ..  -file00  -file01  -file02  -file03  -file04  -file05  -file06  -file07  -file08  -file09
bandit4@bandit:~/inhere$ find . -type f -exec cat {} +
?�koReBOKuIDDepwhWk7jZC0RTdopnAYKhx,��/`2ғ�%��rL~5�g��� �����ly���~��A�f����-E�{���m�����ܗM������h!TQO�`�4"aל�߂phT��,�A�r�l$�?h�9('���!y�e�#�x�O��=���T�?�i��j��îP�F�l�n��J����{��@i�4�ו$����I&������c���ގ.�
e�)�#��5����p��V�_���ׯ�mm�e�0$�in=��_b�5FA�P7sz��gN
bandit4@bandit:~/inhere$ grep "Depw" ~/inhere/*
/home/bandit4/inhere/-file07:koReBOKuIDDepwhWk7jZC0RTdopnAYKh
bandit4@bandit:~/inhere$ cat ./-file07
koReBOKuIDDepwhWk7jZC0RTdopnAYKh
~~~

</details>

### Answer

<details>

<summary markdown="span">Flag</summary>

~~~
$ sshpass -p "koReBOKuIDDepwhWk7jZC0RTdopnAYKh" ssh -p 2220 bandit5@bandit.labs.overthewire.org
~~~

</details>

## Level 6

The password for the next level is stored in a file somewhere under the inhere directory and has all of the following properties:

- human-readable
- 1033 bytes in size
- not executable

### Solution

<details>

<summary markdown="span">Solution</summary>

~~~shell
bandit5@bandit:~$ cd inhere/
bandit5@bandit:~/inhere$ du -a -b | grep 1033
1033	./maybehere07/.file2
bandit5@bandit:~/inhere$ cat ./maybehere07/.file2
DXjZPULLxYr17uwoI01bNLQbtFemEgo7
~~~

</details>

### Answer

<details>

<summary markdown="span">Flag</summary>

~~~
$ sshpass -p "DXjZPULLxYr17uwoI01bNLQbtFemEgo7" ssh -p 2220 bandit6@bandit.labs.overthewire.org
~~~

</details>

## Level 7

The password for the next level is stored somewhere on the server and has all of the following properties:

- owned by user bandit7
- owned by group bandit6
- 33 bytes in size

### Solution

<details>

<summary markdown="span">Solution</summary>

~~~shell
bandit6@bandit:~$ find / -type f -size 33c -user bandit7 -group bandit6
find: ‘/root’: Permission denied
find: ‘/home/bandit28-git’: Permission denied
find: ‘/home/bandit30-git’: Permission denied
find: ‘/home/bandit5/inhere’: Permission denied
find: ‘/home/bandit27-git’: Permission denied
find: ‘/home/bandit29-git’: Permission denied
find: ‘/home/bandit31-git’: Permission denied
find: ‘/lost+found’: Permission denied
find: ‘/etc/ssl/private’: Permission denied
find: ‘/etc/polkit-1/localauthority’: Permission denied
find: ‘/etc/lvm/archive’: Permission denied
find: ‘/etc/lvm/backup’: Permission denied
find: ‘/sys/fs/pstore’: Permission denied
find: ‘/proc/tty/driver’: Permission denied
find: ‘/proc/24049/task/24049/fdinfo/6’: No such file or directory
find: ‘/proc/24049/fdinfo/5’: No such file or directory
find: ‘/cgroup2/csessions’: Permission denied
find: ‘/boot/lost+found’: Permission denied
find: ‘/tmp’: Permission denied
find: ‘/run/lvm’: Permission denied
find: ‘/run/screen/S-bandit0’: Permission denied
find: ‘/run/screen/S-bandit9’: Permission denied
find: ‘/run/screen/S-bandit28’: Permission denied
find: ‘/run/screen/S-bandit18’: Permission denied
find: ‘/run/screen/S-bandit1’: Permission denied
find: ‘/run/screen/S-bandit20’: Permission denied
find: ‘/run/screen/S-bandit12’: Permission denied
find: ‘/run/screen/S-bandit5’: Permission denied
find: ‘/run/screen/S-bandit7’: Permission denied
find: ‘/run/screen/S-bandit16’: Permission denied
find: ‘/run/screen/S-bandit26’: Permission denied
find: ‘/run/screen/S-bandit8’: Permission denied
find: ‘/run/screen/S-bandit15’: Permission denied
find: ‘/run/screen/S-bandit4’: Permission denied
find: ‘/run/screen/S-bandit3’: Permission denied
find: ‘/run/screen/S-bandit19’: Permission denied
find: ‘/run/screen/S-bandit31’: Permission denied
find: ‘/run/screen/S-bandit17’: Permission denied
find: ‘/run/screen/S-bandit2’: Permission denied
find: ‘/run/screen/S-bandit22’: Permission denied
find: ‘/run/screen/S-bandit21’: Permission denied
find: ‘/run/screen/S-bandit14’: Permission denied
find: ‘/run/screen/S-bandit13’: Permission denied
find: ‘/run/screen/S-bandit25’: Permission denied
find: ‘/run/screen/S-bandit24’: Permission denied
find: ‘/run/screen/S-bandit23’: Permission denied
find: ‘/run/shm’: Permission denied
find: ‘/run/lock/lvm’: Permission denied
find: ‘/var/spool/bandit24’: Permission denied
find: ‘/var/spool/cron/crontabs’: Permission denied
find: ‘/var/spool/rsyslog’: Permission denied
find: ‘/var/tmp’: Permission denied
find: ‘/var/lib/apt/lists/partial’: Permission denied
find: ‘/var/lib/polkit-1’: Permission denied
/var/lib/dpkg/info/bandit7.password
find: ‘/var/log’: Permission denied
find: ‘/var/cache/apt/archives/partial’: Permission denied
find: ‘/var/cache/ldconfig’: Permission denied
bandit6@bandit:~$ cat /var/lib/dpkg/info/bandit7.password 
HKBPTKQnIay4Fw76bEy8PVxKEDQRKTzs
~~~

</details>

### Answer

<details>

<summary markdown="span">Flag</summary>

~~~
$ sshpass -p "HKBPTKQnIay4Fw76bEy8PVxKEDQRKTzs" ssh -p 2220 bandit7@bandit.labs.overthewire.org
~~~

</details>

## Level 8

The password for the next level is stored in the file data.txt next to the word millionth

### Solution

<details>

<summary markdown="span">Solution</summary>

~~~shell
bandit7@bandit:~$ ls
data.txt
bandit7@bandit:~$ grep millionth data.txt
millionth	cvX2JJa4CFALtqS87jk27qwqGhBM9plV
~~~

</details>

### Answer

<details>

<summary markdown="span">Flag</summary>

~~~
$ sshpass -p "cvX2JJa4CFALtqS87jk27qwqGhBM9plV" ssh -p 2220 bandit8@bandit.labs.overthewire.org
~~~

</details>

## Level 9

The password for the next level is stored in the file data.txt and is the only line of text that occurs only once

### Solution

<details>

<summary markdown="span">Solution</summary>

~~~shell
bandit8@bandit:~$ ls
data.txt
bandit8@bandit:~$ sort -r data.txt | uniq -u
UsvVyFSfZZWbi6wgC7dAFyFuR6jQQUhR
~~~

</details>

### Answer

<details>

<summary markdown="span">Flag</summary>

~~~
$ sshpass -p "UsvVyFSfZZWbi6wgC7dAFyFuR6jQQUhR" ssh -p 2220 bandit9@bandit.labs.overthewire.org
~~~

</details>

## Level 10

The password for the next level is stored in the file data.txt in one of the few human-readable strings, preceded by several ‘=’ characters.

### Solution

<details>

<summary markdown="span">Solution</summary>

~~~shell
bandit9@bandit:~$ strings data.txt | grep =
========== the*2i"4
=:G e
========== password
I=zsGi
Z)========== is
A=|t&E
Zdb=
c^ LAh=3G
*SF=s
&========== truKLdjsbJ5g7yyJ2X2R0o3a5HQJFuLk
S=A.H&^
~~~

</details>

### Answer

<details>

<summary markdown="span">Flag</summary>

~~~
$ sshpass -p "truKLdjsbJ5g7yyJ2X2R0o3a5HQJFuLk" ssh -p 2220 bandit10@bandit.labs.overthewire.org
~~~

</details>

## Level 11

The password for the next level is stored in the file data.txt, which contains base64 encoded data

### Solution

<details>

<summary markdown="span">Solution</summary>

~~~shell
bandit10@bandit:~$ cat data.txt | base64 --decode
The password is IFukwKGsFW8MOq3IRFqrxE1hxTNEbUPR
~~~

</details>

### Answer

<details>

<summary markdown="span">Flag</summary>

~~~
$ sshpass -p "IFukwKGsFW8MOq3IRFqrxE1hxTNEbUPR" ssh -p 2220 bandit11@bandit.labs.overthewire.org
~~~

</details>

## Level 12

The password for the next level is stored in the file data.txt, where all lowercase (a-z) and uppercase (A-Z) letters have been rotated by 13 positions

### Solution

<details>

<summary markdown="span">Solution</summary>

~~~shell
bandit11@bandit:~$ cat data.txt | tr '[A-Za-z]' '[N-ZA-Mn-za-m]'
The password is 5Te8Y4drgCRfCx8ugdwuEX8KFC6k2EUu
~~~

</details>

### Answer

<details>

<summary markdown="span">Flag</summary>

~~~
$ sshpass -p "5Te8Y4drgCRfCx8ugdwuEX8KFC6k2EUu" ssh -p 2220 bandit12@bandit.labs.overthewire.org
~~~

</details>

## Level 13

The password for the next level is stored in the file data.txt, which is a hexdump of a file that has been repeatedly compressed. For this level it may be useful to create a directory under /tmp in which you can work using mkdir. For example: mkdir /tmp/myname123. Then copy the datafile using cp, and rename it using mv (read the manpages!)

### Solution

<details>

<summary markdown="span">Solution</summary>

~~~shell
bandit12@bandit:~$ xxd -r data.txt | zcat | bzcat | zcat | tar xvf - -O | tar xvf - -O | bzcat | tar xvf - -O | zcat
data5.bin
data6.bin
data8.bin
The password is 8ZjyCRiBWFYkneahHwxCv3wb2a1ORpYL
~~~

</details>

### Answer

<details>

<summary markdown="span">Flag</summary>

~~~
$ sshpass -p "8ZjyCRiBWFYkneahHwxCv3wb2a1ORpYL" ssh -p 2220 bandit13@bandit.labs.overthewire.org
~~~

</details>

## Level 14

The password for the next level is stored in /etc/bandit_pass/bandit14 and can only be read by user bandit14. For this level, you don’t get the next password, but you get a private SSH key that can be used to log into the next level. Note: localhost is a hostname that refers to the machine you are working on

### Solution

<details>

<summary markdown="span">Solution</summary>

~~~shell
bandit13@bandit:~$ ls
sshkey.private
bandit13@bandit:~$ ssh -i sshkey.private  bandit14@localhost
bandit14@bandit:~$ cat /etc/bandit_pass/bandit14
4wcYUJFw0k0XLShlDzztnTBHiqxU3b3e
~~~

</details>

### Answer

<details>

<summary markdown="span">Flag</summary>

~~~
4wcYUJFw0k0XLShlDzztnTBHiqxU3b3e
~~~

</details>

## Level 15

The password for the next level can be retrieved by submitting the password of the current level to port 30000 on localhost.

### Solution

<details>

<summary markdown="span">Solution</summary>

~~~shell
bandit14@bandit:~$ nc localhost 30000
4wcYUJFw0k0XLShlDzztnTBHiqxU3b3e                                                                                                   
Correct!
BfMYroe26WYalil77FoDi9qh59eK5xNr
~~~

</details>

### Answer

<details>

<summary markdown="span">Flag</summary>

~~~
BfMYroe26WYalil77FoDi9qh59eK5xNr
~~~

</details>

## Level 16

The password for the next level can be retrieved by submitting the password of the current level to port 30001 on localhost using SSL encryption.

Helpful note: Getting “HEARTBEATING” and “Read R BLOCK”? Use -ign_eof and read the “CONNECTED COMMANDS” section in the manpage. Next to ‘R’ and ‘Q’, the ‘B’ command also works in this version of that command…

### Solution

<details>

<summary markdown="span">Solution</summary>

~~~shell
bandit14@bandit:~$ openssl s_client -ign_eof -connect localhost:30001
CONNECTED(00000003)
depth=0 CN = localhost
verify error:num=18:self signed certificate
verify return:1
depth=0 CN = localhost
verify return:1
---
Certificate chain
 0 s:/CN=localhost
   i:/CN=localhost
---
Server certificate
-----BEGIN CERTIFICATE-----
MIICBjCCAW+gAwIBAgIEZOzuVDANBgkqhkiG9w0BAQUFADAUMRIwEAYDVQQDDAls
b2NhbGhvc3QwHhcNMjEwOTMwMDQ0NTU0WhcNMjIwOTMwMDQ0NTU0WjAUMRIwEAYD
VQQDDAlsb2NhbGhvc3QwgZ8wDQYJKoZIhvcNAQEBBQADgY0AMIGJAoGBAM9En7CC
uPr6cVPATLAVhWMU1hggfIJEp5sZN9RPUbK0zKBv802yD54ObHYmIge6lqqkgXOz
2AuI4UfCG4iMb0UYUCA/wISwNqUQrjcja0OnqzCTRscXzzoIsHbC8lGFzMDRz3Jw
8nBD6/2jvFt1rnBtZ4ghibNn5rFHRi5EC+K/AgMBAAGjZTBjMBQGA1UdEQQNMAuC
CWxvY2FsaG9zdDBLBglghkgBhvhCAQ0EPhY8QXV0b21hdGljYWxseSBnZW5lcmF0
ZWQgYnkgTmNhdC4gU2VlIGh0dHBzOi8vbm1hcC5vcmcvbmNhdC8uMA0GCSqGSIb3
DQEBBQUAA4GBAD7/moj14DUI6/D6imJ8pQlAy/8lZlsrbyRnqpzjWaATShDYr7k3
umdRg+36MciNFAglE7nGYZroTSDCm650D81+797owSXLPAdp1Q6JfQH5LOni2kbw
UHcO9hwQ+rJzEgIlfGOic7dC5lj8DBU5tugY87RZGKiZ2GG77WXas9Iz
-----END CERTIFICATE-----
subject=/CN=localhost
issuer=/CN=localhost
---
No client certificate CA names sent
Peer signing digest: SHA512
Server Temp Key: X25519, 253 bits
---
SSL handshake has read 1019 bytes and written 269 bytes
Verification error: self signed certificate
---
New, TLSv1.2, Cipher is ECDHE-RSA-AES256-GCM-SHA384
Server public key is 1024 bit
Secure Renegotiation IS supported
Compression: NONE
Expansion: NONE
No ALPN negotiated
SSL-Session:
    Protocol  : TLSv1.2
    Cipher    : ECDHE-RSA-AES256-GCM-SHA384
    Session-ID: 8FBD74F767591D1CCDC05215BB8247CD380A7D4FEF6CAEE5BF210EC3949DC742
    Session-ID-ctx: 
    Master-Key: DDB2E6FE9645779EEC64D36DE2BDB0FD5078568AF70770707DB9C5B72EE7B9F8FB0FECE326325D9904ED5602FE2F1287
    PSK identity: None
    PSK identity hint: None
    SRP username: None
    TLS session ticket lifetime hint: 7200 (seconds)
    TLS session ticket:
    0000 - 8a eb e8 f5 31 15 46 ad-b2 a8 10 c1 51 b9 66 14   ....1.F.....Q.f.
    0010 - f0 77 50 4b 76 da 29 00-3e f2 5c e8 00 17 3d 7e   .wPKv.).>.\...=~
    0020 - 63 ea cd f9 01 32 7c 19-19 88 1f 8b a5 57 50 67   c....2|......WPg
    0030 - 00 8a d6 7f 3f 09 5d 4d-ac 31 ff 99 2e f8 2d 5c   ....?.]M.1....-\
    0040 - 3e fd 35 43 f9 ff 27 99-80 0e e3 91 dd b7 b3 a7   >.5C..'.........
    0050 - 91 d7 24 5d ca f9 ae d6-ad 0c ae fd 41 d5 43 ce   ..$]........A.C.
    0060 - 23 18 a2 fb 08 60 13 82-96 fc 85 b5 9e b3 be 7e   #....`.........~
    0070 - 5a c8 72 0b 47 5e 9c b4-fc 51 aa ff cb 7b d5 c0   Z.r.G^...Q...{..
    0080 - 63 62 02 f1 08 56 4e 89-7f 78 2e e2 50 f2 8d 62   cb...VN..x..P..b
    0090 - 3b 78 af 13 1a 5b 66 1b-f3 c5 53 45 89 0b 24 19   ;x...[f...SE..$.

    Start Time: 1642933341
    Timeout   : 7200 (sec)
    Verify return code: 18 (self signed certificate)
    Extended master secret: yes
---
BfMYroe26WYalil77FoDi9qh59eK5xNr
Correct!
cluFn7wTiGryunymYOu4RcffSxQluehd
~~~

</details>

### Answer

<details>

<summary markdown="span">Flag</summary>

~~~
cluFn7wTiGryunymYOu4RcffSxQluehd
~~~

</details>

## Level 17

The credentials for the next level can be retrieved by submitting the password of the current level to a port on localhost in the range 31000 to 32000. First find out which of these ports have a server listening on them. Then find out which of those speak SSL and which don’t. There is only 1 server that will give the next credentials, the others will simply send back to you whatever you send to it.

### Solution

<details>

<summary markdown="span">Solution</summary>

~~~shell

~~~

</details>

### Answer

<details>

<summary markdown="span">Flag</summary>

~~~
$ sshpass -p "" ssh -p 2220 @bandit.labs.overthewire.org
~~~

</details>

## Level 18

### Solution

<details>

<summary markdown="span">Solution</summary>

~~~shell

~~~

</details>

### Answer

<details>

<summary markdown="span">Flag</summary>

~~~
$ sshpass -p "" ssh -p 2220 @bandit.labs.overthewire.org
~~~

</details>

## Level 19

### Solution

<details>

<summary markdown="span">Solution</summary>

~~~shell

~~~

</details>

### Answer

<details>

<summary markdown="span">Flag</summary>

~~~
$ sshpass -p "" ssh -p 2220 @bandit.labs.overthewire.org
~~~

</details>

## Level 20

### Solution

<details>

<summary markdown="span">Solution</summary>

~~~shell

~~~

</details>

### Answer

<details>

<summary markdown="span">Flag</summary>

~~~
$ sshpass -p "" ssh -p 2220 @bandit.labs.overthewire.org
~~~

</details>

## Level 21

### Solution

<details>

<summary markdown="span">Solution</summary>

~~~shell

~~~

</details>

### Answer

<details>

<summary markdown="span">Flag</summary>

~~~
$ sshpass -p "" ssh -p 2220 @bandit.labs.overthewire.org
~~~

</details>

## Level 22

### Solution

<details>

<summary markdown="span">Solution</summary>

~~~shell

~~~

</details>

### Answer

<details>

<summary markdown="span">Flag</summary>

~~~
$ sshpass -p "" ssh -p 2220 @bandit.labs.overthewire.org
~~~

</details>

## Level 23

### Solution

<details>

<summary markdown="span">Solution</summary>

~~~shell

~~~

</details>

### Answer

<details>

<summary markdown="span">Flag</summary>

~~~
$ sshpass -p "" ssh -p 2220 @bandit.labs.overthewire.org
~~~

</details>

## Level 24

### Solution

<details>

<summary markdown="span">Solution</summary>

~~~shell

~~~

</details>

### Answer

<details>

<summary markdown="span">Flag</summary>

~~~
$ sshpass -p "" ssh -p 2220 @bandit.labs.overthewire.org
~~~

</details>

## Level 25

### Solution

<details>

<summary markdown="span">Solution</summary>

~~~shell

~~~

</details>

### Answer

<details>

<summary markdown="span">Flag</summary>

~~~
$ sshpass -p "" ssh -p 2220 @bandit.labs.overthewire.org
~~~

</details>

## Level 26

### Solution

<details>

<summary markdown="span">Solution</summary>

~~~shell

~~~

</details>

### Answer

<details>

<summary markdown="span">Flag</summary>

~~~
$ sshpass -p "" ssh -p 2220 @bandit.labs.overthewire.org
~~~

</details>

## Level 27

### Solution

<details>

<summary markdown="span">Solution</summary>

~~~shell

~~~

</details>

### Answer

<details>

<summary markdown="span">Flag</summary>

~~~
$ sshpass -p "" ssh -p 2220 @bandit.labs.overthewire.org
~~~

</details>

## Level 28

### Solution

<details>

<summary markdown="span">Solution</summary>

~~~shell

~~~

</details>

### Answer

<details>

<summary markdown="span">Flag</summary>

~~~
$ sshpass -p "" ssh -p 2220 @bandit.labs.overthewire.org
~~~

</details>

## Level 29

### Solution

<details>

<summary markdown="span">Solution</summary>

~~~shell

~~~

</details>

### Answer

<details>

<summary markdown="span">Flag</summary>

~~~
$ sshpass -p "" ssh -p 2220 @bandit.labs.overthewire.org
~~~

</details>

## Level 30

### Solution

<details>

<summary markdown="span">Solution</summary>

~~~shell

~~~

</details>

### Answer

<details>

<summary markdown="span">Flag</summary>

~~~
$ sshpass -p "" ssh -p 2220 @bandit.labs.overthewire.org
~~~

</details>

## Level 31

### Solution

<details>

<summary markdown="span">Solution</summary>

~~~shell

~~~

</details>

### Answer

<details>

<summary markdown="span">Flag</summary>

~~~
$ sshpass -p "" ssh -p 2220 @bandit.labs.overthewire.org
~~~

</details>

## Level 32

### Solution

<details>

<summary markdown="span">Solution</summary>

~~~shell

~~~

</details>

### Answer

<details>

<summary markdown="span">Flag</summary>

~~~
$ sshpass -p "" ssh -p 2220 @bandit.labs.overthewire.org
~~~

</details>

## Level 33

### Solution

<details>

<summary markdown="span">Solution</summary>

~~~shell

~~~

</details>

### Answer

<details>

<summary markdown="span">Flag</summary>

~~~
$ sshpass -p "" ssh -p 2220 @bandit.labs.overthewire.org
~~~

</details>

## Level 34

### Solution

<details>

<summary markdown="span">Solution</summary>

~~~shell

~~~

</details>

### Answer

<details>

<summary markdown="span">Flag</summary>

~~~
$ sshpass -p "" ssh -p 2220 @bandit.labs.overthewire.org
~~~

</details>

## Level 35

### Solution

<details>

<summary markdown="span">Solution</summary>

~~~shell

~~~

</details>

### Answer

<details>

<summary markdown="span">Flag</summary>

~~~
$ sshpass -p "" ssh -p 2220 @bandit.labs.overthewire.org
~~~

</details>

Page last updated Jan 2021.

## [djm89uk.github.io](https://djm89uk.github.io)
