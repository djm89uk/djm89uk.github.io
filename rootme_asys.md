# [Root-Me](./rootme.md) Root-Me App - System Challenges [0/83]

These challenges will help you understand applicative vulnerabilities. 

## Contents

1. [ELF x86 - Stack buffer overflow basic 1](#elf-x86-stack-buffer-overflow-basic-1)
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
22. [ELF x86 - Stack buffer overflow - C++ vtables](#elf-x86-stack-buffer-overflow-c-vtables)
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
81. [ELF x64 - Advanced Heap Exploitation - Heap Leakless & Fortified](#elf-x64-advanced-heap-exploitation-heap-leakless-&-fortified)
82. [ELF x64 - Blind ROP](#elf-x64-blind-rop)
83. [ELF x64 - Browser exploit - BitString](#elf-x64-browser-exploit-bitstring)

---

### [App - System](#contents) | [Root-Me](./rootme.md) | [Home](./index.md)

---

## ChallengeName

- Author: name
- X Points

### Description

Description Here

### Hints

1. Hint 1

### Connection Details

1. Detail 1

### Attachments

1. Attachment 1

### Solutions

<details>

<summary markdown="span">Solution 1</summary>

Detail here

</details>

### Answer

<details>

<summary markdown="span">Answer</summary>

~~~

~~~

</details>

---

### [App - System](#contents) | [Root-Me](./rootme.md) | [Home](./index.md)

---

Last updated Jan 2021.

## [djm89uk.github.io](https://djm89uk.github.io)