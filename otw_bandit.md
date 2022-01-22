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
8. [Level 8](#level-8)
9. [Level 9](#level-9)
10. [Level 10](#level-10)
11. [Level 11](#level-11)
12. [Level 12](#level-12)
13. [Level 13](#level-13)
14. [Level 14](#level-14)
15. [Level 15](#level-15)
16. [Level 16](#level-16)
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

Page last updated Jan 2021.

## [djm89uk.github.io](https://djm89uk.github.io)
