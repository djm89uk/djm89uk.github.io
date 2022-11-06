# [Root-Me](./rootme.md) Root-Me Cracking [10/46]

Reverse binaries and crack executables. 

## Contents

1. [ELF x86 - 0 protection](#elf-x86-0-protection) 🗸
2. [ELF x86 - Basic](#elf-x86-basic) 🗸
3. [PE x86 - 0 protection](#pe-x86-0-protection) 🗸
4. [ELF C++ - 0 protection](#elf-cpp-0-protection) 🗸
5. [Godot - 0 protection](#godot-0-protection)
6. [PE DotNet - 0 protection](#pe-dotnet-0-protection) 🗸
7. [APK - Introduction](#apk-introduction)
8. [ELF MIPS - Basic Crackme](#elf-mips-basic-crackme) 🗸
9. [ELF x64 - Golang basic](#elf-x64-golang-basic) 🗸
10. [ELF x86 - Fake Instructions](#elf-x86-fake-instructions) 🗸
11. [ELF x86 - Ptrace](#elf-x86-ptrace) 🗸
12. [WASM - Introduction](#wasm-introduction)
13. [ELF ARM - Basic Crackme](#elf-arm-basic-crackme)
14. [ELF x64 - Basic KeygenMe](#elf-x64-basic-keygenme)
15. [PE DotNet - Basic Anti-Debug](#pe-dotnet-basic-anti-debug)
16. [PE DotNet - Basic Crackme](#pe-dotnet-basic-crackme)
17. [PYC - ByteCode](#pyc-bytecode)
18. [ELF x86 - No software breakpoints](#elf-x86-no-software-breakpoints)
19. [Lua - Bytecode](#lua-bytecode)
20. [MachO x64 - keygenme or not](#macho-x64-keygenme-or-not)
21. [ELF ARM - crackme 1337](#elf-arm-crackme-1337)
22. [ELF x86 - CrackPass](#elf-x86-crackpass) 🗸
23. [ELF x86 - ExploitMe](#elf-x86-exploitme)
24. [ELF x86 - Random Crackme](#elf-x86-random-crackme)
25. [GB - Basic GameBoy crackme](#gb-basic-gameboy-crackme)
26. [PDF - Javascript](#pdf-javascript)
27. [PE x86 - Xor Madness](#pe-x86-xor-madness)
28. [ELF ARM - Crypted](#elf-arm-crypted)
29. [ELF x64 - Crackme automating](#elf-x64-crackme-automating)
30. [PE x86 - SEHVEH](#pe-x86-sehveh)
31. [Powershell DeObfuscation](#powershell-deobfuscation)
32. [APK - Anti-debug](#apk-anti-debug)
33. [ELF x64 - Nanomites - Introduction](#elf-x64-nanomites-introduction)
34. [ELF x86 - Anti-debug](#elf-x86-anti-debug)
35. [PE DotNet - KeygenMe](#pe-dotnet-keygenme)
36. [PE x86 - AutoPE](#pe-x86-autope)
37. [ELF x86 - KeygenMe](#elf-x86-keygenme)
38. [WASM - Find the NPC](#wasm-find-the-npc)
39. [Bash - VM](#bash-vm)
40. [ELF x64 - KeyGenMe](#elf-x64-keygenme)
41. [ELF x64 - Anti-debug and equations](#elf-x64-anti-debug-and-equations)
42. [ELF x64 - Nanomites](#elf-x64-nanomites)
43. [ELF x86 - Packed](#elf-x86-packed)
44. [PE x86 - RunPE](#pe-x86-runpe)
45. [ELF x86 - VM](#elf-x86-vm)
46. [ELF x64 - Hidden Control Flow](#elf-x64-hidden-control-flow)
47. [Ringgit](#ringgit)
48. [White-Box Cryptography #2](#white-box-cryptography-#2)

---

### [Cracking](#contents) | [Root-Me](./rootme.md) | [Home](./index.md)

---

## ELF x86 0 protection

- Author: g0uZ
- Date: 7 October 2006
- Points: 5
- Level: 1

### Statement

None.

### Attachments

1. [ch1.zip](http://challenge01.root-me.org/cracking/ch1/ch1.zip).

### Resources

1. [The GNU binary utils](https://repository.root-me.org/Administration/Unix/Linux/EN%20-%20The%20GNU%20binary%20utils.pdf).
2. [Reverse Engineering poour Debutants](https://repository.root-me.org/Reverse%20Engineering/FR%20-%20Reverse%20Engineering%20pour%20D%C3%A9butants%20-%20Dennis%20Yurichev.pdf).
3. [Executable and Linkable Format ELF](https://repository.root-me.org/Reverse%20Engineering/x86/Unix/EN%20-%20Executable%20and%20Linkable%20Format%20ELF.pdf).
4. [Reverse Engineering for Beginners](https://repository.root-me.org/Reverse%20Engineering/EN%20-%20Reverse%20Engineering%20for%20Beginners%20-%20Dennis%20Yurichev.pdf).

### Solutions

<details>

<summary markdown="span">Solution 1</summary>

We are given a zip file containing a binary, ch1.zip.  We can extract and run the binary:

~~~shell
$ unzip ch1.zip 
Archive:  ch1.zip
  inflating: ch1.bin   
$ chmod +x ch1.bin
$ ./ch1.bin
############################################################
##        Bienvennue dans ce challenge de cracking        ##
############################################################

Veuillez entrer le mot de passe : 1
Dommage, essaye encore une fois.
~~~

We can see the programme asks for a password and rejects an incorrect password.  We can decompile in Ghidra and we find the main function:

~~~c

undefined4 main(undefined1 param_1)

{
  char *__s1;
  int iVar1;
  undefined4 local_14;
  
  puts("############################################################");
  puts("##        Bienvennue dans ce challenge de cracking        ##");
  puts("############################################################\n");
  printf("Veuillez entrer le mot de passe : ");
  __s1 = (char *)getString(local_14);
  iVar1 = strcmp(__s1,"123456789");
  if (iVar1 == 0) {
    printf("Bien joue, vous pouvez valider l\'epreuve avec le pass : %s!\n","123456789");
  }
  else {
    puts("Dommage, essaye encore une fois.");
  }
  return 0;
}
~~~

We can see the user input is compared with the string 123456789.  Re-running with the password, we get the challenge solution.

</details>

### Answer

<details>

<summary markdown="span">Answer</summary>

~~~
123456789
~~~

</details>

---

### [Cracking](#contents) | [Root-Me](./rootme.md) | [Home](./index.md)

---

## ELF x86 Basic

- Author: g0uZ
- Date: 7 October 2006
- Points: 5
- Level: 1

### Statement

Find the validation password.

### Attachments

1. [ch2.zip](http://challenge01.root-me.org/cracking/ch2/ch2.zip).

### Resources

1. [The GNU binary utils](https://repository.root-me.org/Administration/Unix/Linux/EN%20-%20The%20GNU%20binary%20utils.pdf).
2. [Reverse Engineering poour Debutants](https://repository.root-me.org/Reverse%20Engineering/FR%20-%20Reverse%20Engineering%20pour%20D%C3%A9butants%20-%20Dennis%20Yurichev.pdf).
3. [Executable and Linkable Format ELF](https://repository.root-me.org/Reverse%20Engineering/x86/Unix/EN%20-%20Executable%20and%20Linkable%20Format%20ELF.pdf).
4. [Reverse Engineering for Beginners](https://repository.root-me.org/Reverse%20Engineering/EN%20-%20Reverse%20Engineering%20for%20Beginners%20-%20Dennis%20Yurichev.pdf).

### Solutions

<details>

<summary markdown="span">Solution 1</summary>

We are given a zip file containing a binary, ch2.zip.  We can extract and run the binary:

~~~shell
$ unzip ch2.zip 
Archive:  ch2.zip
  inflating: ch2.bin                 
$ chmod +x ch2.bin
$ ./ch2.bin
############################################################
##        Bienvennue dans ce challenge de cracking        ##
############################################################

username: admin
Bad username
~~~

We can see the programme asks for a username and terminates with an incorrect input.  We can decompile in Ghidra and we find the main function:

~~~c
undefined4 main(undefined1 param_1)

{
  char *pcVar1;
  int iVar2;
  undefined4 local_10;
  
  puts("############################################################");
  puts("##        Bienvennue dans ce challenge de cracking        ##");
  puts("############################################################\n");
  printf("username: ");
  pcVar1 = (char *)getString(local_10);
  iVar2 = strcmp(pcVar1,"john");
  if (iVar2 == 0) {
    printf("password: ");
    pcVar1 = (char *)getString(pcVar1);
    iVar2 = strcmp(pcVar1,"the ripper");
    if (iVar2 == 0) {
      printf("Bien joue, vous pouvez valider l\'epreuve avec le mot de passe : %s !\n","987654321");
    }
    else {
      puts("Bad password");
    }
  }
  else {
    puts("Bad username");
  }
  return 0;
}
~~~

We can see the user input username is compared with the string "john" and a second input for password is compared with the string "the ripper".  Re-running with the password, we get the challenge solution.

</details>

### Answer

<details>

<summary markdown="span">Answer</summary>

~~~
987654321
~~~

</details>

---

### [Cracking](#contents) | [Root-Me](./rootme.md) | [Home](./index.md)

---

## PE x86 0 protection

- Author: alejandr0
- Date: 11 November 2012
- Points: 5
- Level: 1

### Statement

Find the validation password.

### Attachments

1. [ch15.exe](http://challenge01.root-me.org/cracking/ch15/ch15.exe).

### Resources

1. [Microsoft Portable Executable and Common Object File Format Specification](https://repository.root-me.org/Programmation/Windows/EN%20-%20Microsoft%20Portable%20Executable%20and%20Common%20Object%20File%20Format%20Specification.docx).
2. [Reverse Engineering pour Debutants](https://repository.root-me.org/Reverse%20Engineering/FR%20-%20Reverse%20Engineering%20pour%20D%C3%A9butants%20-%20Dennis%20Yurichev.pdf).
3. [Introduction au format Portable Executable PE](https://repository.root-me.org/Reverse%20Engineering/x86/Microsoft/FR%20-%20Introduction%20au%20format%20Portable%20Executable%20PE.pdf).
4. [Reverse Engineering for Beginners](https://repository.root-me.org/Reverse%20Engineering/EN%20-%20Reverse%20Engineering%20for%20Beginners%20-%20Dennis%20Yurichev.pdf).

### Solutions

<details>

<summary markdown="span">Solution 1</summary>

We are given an exe binary file we can run using wine:

~~~shell
$ wine ./ch15.exe 
Usage: Z:\home\derek\Downloads\ch15.exe pass
$ wine ./ch15.exe 123
Wrong password
~~~

We can see the programme requires a password input and terminates if the input is not correct.  We can decompile in Ghidra.  We find a subfunction that compares the input to specific characters:

~~~c
void FUN_00401726(char *param_1,int param_2)

{
  if (((((param_2 == 7) && (*param_1 == 'S')) && (param_1[1] == 'P')) &&
      ((param_1[2] == 'a' && (param_1[3] == 'C')))) &&
     ((param_1[4] == 'I' && ((param_1[5] == 'o' && (param_1[6] == 'S')))))) {
    printf("Gratz man :)");
                    /* WARNING: Subroutine does not return */
    exit(0);
  }
  puts("Wrong password");
  return;
}
~~~

We can see the string the input is compared against is "SPaCIoS".  We rerun the program with this input:

~~~shell
$ wine ./ch15.exe SPaCIoS
Gratz man :)
~~~

This is the challenge solution

</details>

### Answer

<details>

<summary markdown="span">Answer</summary>

~~~
SPaCIoS
~~~

</details>

---

### [Cracking](#contents) | [Root-Me](./rootme.md) | [Home](./index.md)

---

## ELF CPP 0 Protection

- Author: sourcePerrier
- Date: 13 July 2016
- Points: 10
- Level: 1

### Statement

Find the validation password.

### Attachments

1. [ch25.exe](http://challenge01.root-me.org/cracking/ch25/ch25.bin).

### Resources

1. [Reversing C___](https://repository.root-me.org/Reverse%20Engineering/EN%20-%20Reversing%20C++%20-%20Blackhat%20-%20Yason%20Sabanal%20-%20paper.pdf)

### Solutions

<details>

<summary markdown="span">Solution 1</summary>

We can retreive the binary file using wget:

~~~shell
$ wget http://challenge01.root-me.org/cracking/ch25/ch25.bin
--2022-02-27 10:31:46--  http://challenge01.root-me.org/cracking/ch25/ch25.bin
Resolving challenge01.root-me.org (challenge01.root-me.org)... 212.129.38.224, 2001:bc8:35b0:c166::151
Connecting to challenge01.root-me.org (challenge01.root-me.org)|212.129.38.224|:80... connected.
HTTP request sent, awaiting response... 200 OK
Length: 12751 (12K) [application/octet-stream]
Saving to: ‘ch25.bin’

ch25.bin                                                    100%[=========================================================================================================================================>]  12.45K  --.-KB/s    in 0s      

2022-02-27 10:31:46 (116 MB/s) - ‘ch25.bin’ saved [12751/12751]
~~~

We can use ltrace to review the program:

~~~shell
$ ltrace -C ./ch25.bin FOO 2>&1
__libc_start_main(0x8048a86, 2, 0xff92c454, 0x8048d20 <unfinished ...>
std::ios_base::Init::Init()(0x804b18d, 0xf7e7bed0, 0xf7ef2a38, 0xf7b47402)                                                                         = 0xf7efaeec
__cxa_atexit(0x80487e0, 0x804b18d, 0x804b058, 0xf7b47402)                                                                                          = 0
std::allocator<char>::allocator()(0xff92c393, 0xf7ef90ec, 2, 0x8048d72)                                                                            = 0xff92c393
...
std::basic_string<char, std::char_traits<char>, std::allocator<char> >::~basic_string()(0xff92c394, 0x8048850, 0xff92c39c, 0x8048d72)              = 0
std::ios_base::Init::~Init()(0x804b18d, 0, 0, 0xf7b47133)                                                                                          = 0xf7ef9840
+++ exited (status 0) +++
~~~

We can see a string generated through character concatenation using += operator.  We can extract these in ltrace:

~~~shell
$ ltrace -C ./ch25.bin FOO 2>&1 | grep operator+=
std::string::operator+=(char)(0xff995ec4, 72, 0xff995e8b, 0xf7f52000) = 0xff995ec4
std::string::operator+=(char)(0xff995ec4, 101, 0xff995e8b, 0xf7f52000) = 0xff995ec4
...
std::string::operator+=(char)(0xff995ec4, 102, 0xff995e8b, 0xf7f52000) = 0xff995ec4
std::string::operator+=(char)(0xff995ec4, 115, 0xff995e8b, 0xf7f52000) = 0xff995ec4
~~~

These appear to be ascii characters, we can extract the decimal values:

~~~shell
$ ltrace -C ./ch25.bin FOO 2>&1 | grep operator+ | cut -f2 -d' '|tr -d "\n"
72,101,114,101,95,121,111,117,95,104,97,118,101,95,116,111,95,117,110,100,101,114,115,116,97,110,100,95,97,95,108,105,116,116,108,101,95,67,43,43,95,115,116,117,102,102,115
$ ltrace -C ./ch25.bin FOO 2>&1 | grep operator+ | cut -f2 -d' '|tr -d "," > string.txt
~~~

Using python we can decode into ascii:

~~~py
f = open("string.txt","r")
dec_str = f.read()
dec_str = dec_str.split("\n")[:-1]
ascii_str = ""
for element in dec_str:
    ascii_str += chr(int(element))

print(ascii_str)
~~~

</details>

### Answer

<details>

<summary markdown="span">Answer</summary>

~~~
Here_you_have_to_understand_a_little_C++_stuffs
~~~

</details>

---

### [Cracking](#contents) | [Root-Me](./rootme.md) | [Home](./index.md)

---

## PE DotNet 0 Protection

- Author: Geluchat
- Date: 15 September 2014
- Points: 10
- Level: 1

### Statement

Retrieve the password asked by this binary.

### Attachments

1. [ch22.exe](http://challenge01.root-me.org/cracking/ch22/ch22.exe).

### Resources

1. [https://www.go4expert.com/articles/introduction-cracking-part-i-t17368/](https://www.go4expert.com/articles/introduction-cracking-part-i-t17368/)
2. [https://resources.infosecinstitute.com/topic/demystifying-dot-net-reverse-engineering-part-1-big-introduction/](https://resources.infosecinstitute.com/topic/demystifying-dot-net-reverse-engineering-part-1-big-introduction/)

### Solutions

<details>

<summary markdown="span">Solution 1</summary>

We can retrieve the executable using wget:

~~~shell
$ wget http://challenge01.root-me.org/cracking/ch22/ch22.exe
--2022-02-27 10:44:16--  http://challenge01.root-me.org/cracking/ch22/ch22.exe
Resolving challenge01.root-me.org (challenge01.root-me.org)... 212.129.38.224, 2001:bc8:35b0:c166::151
Connecting to challenge01.root-me.org (challenge01.root-me.org)|212.129.38.224|:80... connected.
HTTP request sent, awaiting response... 200 OK
Length: 26624 (26K) [application/octet-stream]
Saving to: ‘ch22.exe’

ch22.exe                                                    100%[=========================================================================================================================================>]  26.00K  --.-KB/s    in 0.03s   

2022-02-27 10:44:16 (935 KB/s) - ‘ch22.exe’ saved [26624/26624]
~~~

We can decompile using ikdasm:

~~~shell
$ ikdasm ch22.exe > ch22decompile.txt
~~~

reviewing the decompiled code, we find the password validation:

~~~
  .method private instance void  Button1_Click(object sender,
                                               [mscorlib]System.EventArgs e) cil managed
  {
    // Code size       54 (0x36)
    .maxstack  8
    IL_0000:  ldarg.0
    IL_0001:  callvirt   instance [System.Windows.Forms]System.Windows.Forms.TextBox CrackMe.Form1::get_TextBox1()
    IL_0006:  callvirt   instance string [System.Windows.Forms]System.Windows.Forms.TextBox::get_Text()
    IL_000b:  ldstr      "DotNetOP"
    IL_0010:  ldc.i4.0
    IL_0011:  call       int32 [Microsoft.VisualBasic]Microsoft.VisualBasic.CompilerServices.Operators::CompareString(string,
                                                                                                                      string,
                                                                                                                      bool)
    IL_0016:  ldc.i4.0
    IL_0017:  bne.un.s   IL_0028

    IL_0019:  ldstr      "Bravo! Vous pouvez valider avec ce mot de passe\r\nW"
    + "ell done! You can validate with this password"
~~~

This compares a user input to the ldstr at IL_000b which is the challenge solution

</details>

### Answer

<details>

<summary markdown="span">Answer</summary>

~~~
DotNetOP
~~~

</details>

---

### [Cracking](#contents) | [Root-Me](./rootme.md) | [Home](./index.md)

---

## ELF MIPS Basic Crackme

- Author: sar
- Date: 9 July 2018
- Points: 15
- Level: 2

### Statement

Find the validation password.

### Attachments

1. [ch27.bin](http://challenge01.root-me.org/cracking/ch27/ch27.bin).

### Resources

1. [Exploiting buffer overflows on MIPS archietctures](https://repository.root-me.org/Exploitation%20-%20Syst%C3%A8me/Unix/EN%20-%20Exploiting%20Buffer%20Overflows%20on%20MIPS%20Architectures%20-%20Lyon%20Yang.pdf).
2. [Taming wild nanomite-protected MIPS Binary with Symbolic Execution](https://repository.root-me.org/Reverse%20Engineering/EN%20-%20Taming%20a%20Wild%20Nanomite-protected%20MIPS%20Binary%20With%20Symbolic%20Execution%20-%20Diary%20of%20a%20reverse-engineer.pdf).
3. [MIPS Green Sheet](https://repository.root-me.org/Reverse%20Engineering/EN%20-%20MIPS%20Green%20Sheet.pdf).
4. [MIPS Assembly Tutorial](https://repository.root-me.org/Reverse%20Engineering/MIPS/EN%20-%20MIPS%20Assembly%20Tutorial.pdf).

### Solutions

<details>

<summary markdown="span">Solution 1</summary>

We can retrieve the executable using wget:

~~~shell
$ wget http://challenge01.root-me.org/cracking/ch22/ch22.exe
--2022-02-27 10:44:16--  http://challenge01.root-me.org/cracking/ch22/ch22.exe
Resolving challenge01.root-me.org (challenge01.root-me.org)... 212.129.38.224, 2001:bc8:35b0:c166::151
Connecting to challenge01.root-me.org (challenge01.root-me.org)|212.129.38.224|:80... connected.
HTTP request sent, awaiting response... 200 OK
Length: 26624 (26K) [application/octet-stream]
Saving to: ‘ch22.exe’

ch22.exe                                                    100%[=========================================================================================================================================>]  26.00K  --.-KB/s    in 0.03s   

2022-02-27 10:44:16 (935 KB/s) - ‘ch22.exe’ saved [26624/26624]
~~~

We can view the assembly using radare2:

~~~shell
$ r2 -a mips -A ch27.bin > ass_ch27.txt
~~~

reviewing the assembly code, we see the password length is compared against 19; we can determine the password is 19 characters long:

~~~
|           0x0040093c      13000224       addiu v0, zero, 0x13
|       ,=< 0x00400940      07006210       beq v1, v0, 0x400960
~~~

The assembly shows the program will compare characters at different locations in the string to defined values e.g.:

~~~
| `-------> 0x00400af0      2000c383       lb v1, 0x20(fp)
|  ||||||   0x00400af4      72000224       addiu v0, zero, 0x72        ; 'r'
| ,=======< 0x00400af8      07006210       beq v1, v0, 0x400b18
~~~

reviewing these calls the challenge solution can be found.

</details>

### Answer

<details>

<summary markdown="span">Answer</summary>

~~~
cantrunmiiiiiiiiips
~~~

</details>

---

### [Cracking](#contents) | [Root-Me](./rootme.md) | [Home](./index.md)

---

## ELF x64 Golang basic

- Author: jenaye
- Date: 8 November 2018
- Points: 15
- Level: 2

### Statement

Find the validation password.

### Attachments

1. [ch27.bin](http://challenge01.root-me.org/cracking/ch32/ch32.bin).

### Resources

1. [Reversing Goland Binaries like a Pro](https://repository.root-me.org/Reverse%20Engineering/EN%20-%20Reversing%20Golang%20Binaries%20Like%20a%20Pro%20-%20RedNaga.pdf)
2. [Golang Reverse](https://repository.root-me.org/Reverse%20Engineering/EN%20-%20Golang%20Reverse%20-%20Zaytsev.pdf)

### Solutions

<details>

<summary markdown="span">Solution 1</summary>

We can retrieve the executable using wget:

~~~shell
$ wget http://challenge01.root-me.org/cracking/ch32/ch32.bin
--2022-02-27 11:01:07--  http://challenge01.root-me.org/cracking/ch32/ch32.bin
Resolving challenge01.root-me.org (challenge01.root-me.org)... 212.129.38.224, 2001:bc8:35b0:c166::151
Connecting to challenge01.root-me.org (challenge01.root-me.org)|212.129.38.224|:80... connected.
HTTP request sent, awaiting response... 200 OK
Length: 1968737 (1.9M) [application/octet-stream]
Saving to: ‘ch32.bin’

ch32.bin                                                    100%[=========================================================================================================================================>]   1.88M  4.22MB/s    in 0.4s    

2022-02-27 11:01:08 (4.22 MB/s) - ‘ch32.bin’ saved [1968737/1968737]
~~~

We can disassemble using gdb:

~~~shell
(gdb) disassemble main
Dump of assembler code for function main:
   0x0000000000452310 <+0>:	lea    -0x3857(%rip),%rax        # 0x44eac0 <runtime.rt0_go>
   0x0000000000452317 <+7>:	jmpq   *%rax
End of assembler dump.
~~~

Disassembling main.main:

~~~shell
(gdb) disassemble main.main
Dump of assembler code for function main.main:
   0x0000000000492e70 <+0>:	mov    %fs:0xfffffffffffffff8,%rcx
   0x0000000000492e79 <+9>:	lea    -0x38(%rsp),%rax
   0x0000000000492e7e <+14>:	cmp    0x10(%rcx),%rax
   0x0000000000492e82 <+18>:	jbe    0x49310a <main.main+666>
   0x0000000000492e88 <+24>:	sub    $0xb8,%rsp
   0x0000000000492e8f <+31>:	mov    %rbp,0xb0(%rsp)
   0x0000000000492e97 <+39>:	lea    0xb0(%rsp),%rbp
   0x0000000000492e9f <+47>:	lea    0x1053a(%rip),%rax        # 0x4a33e0
   0x0000000000492ea6 <+54>:	mov    %rax,(%rsp)
   0x0000000000492eaa <+58>:	callq  0x40ec00 <runtime.newobject>
   0x0000000000492eaf <+63>:	mov    0x8(%rsp),%rax
   0x0000000000492eb4 <+68>:	mov    %rax,0x78(%rsp)
   0x0000000000492eb9 <+73>:	movq   $0x0,0x80(%rsp)
   0x0000000000492ec5 <+85>:	movq   $0x0,0x88(%rsp)
   0x0000000000492ed1 <+97>:	lea    0xbea8(%rip),%rcx        # 0x49ed80
   0x0000000000492ed8 <+104>:	mov    %rcx,0x80(%rsp)
   0x0000000000492ee0 <+112>:	mov    %rax,0x88(%rsp)
   0x0000000000492ee8 <+120>:	lea    0x80(%rsp),%rcx
   0x0000000000492ef0 <+128>:	mov    %rcx,(%rsp)
   0x0000000000492ef4 <+132>:	movq   $0x1,0x8(%rsp)
   0x0000000000492efd <+141>:	movq   $0x1,0x10(%rsp)
   0x0000000000492f06 <+150>:	callq  0x48d970 <fmt.Scanln>
   0x0000000000492f0b <+155>:	mov    0x4312e(%rip),%rax        # 0x4d6040 <main.statictmp_2>
   0x0000000000492f12 <+162>:	mov    0x4312d(%rip),%rcx        # 0x4d6046 <main.statictmp_2+6>
   0x0000000000492f19 <+169>:	mov    %rax,0x42(%rsp)
   0x0000000000492f1e <+174>:	mov    %rcx,0x48(%rsp)
   0x0000000000492f23 <+179>:	lea    0x50(%rsp),%rax
   0x0000000000492f28 <+184>:	mov    %rax,(%rsp)
   0x0000000000492f2c <+188>:	lea    0x3153a(%rip),%rax        # 0x4c446d
   0x0000000000492f33 <+195>:	mov    %rax,0x8(%rsp)
   0x0000000000492f38 <+200>:	movq   $0x6,0x10(%rsp)
   0x0000000000492f41 <+209>:	callq  0x43ed90 <runtime.stringtoslicebyte>
   0x0000000000492f46 <+214>:	mov    0x18(%rsp),%rax
   0x0000000000492f4b <+219>:	mov    %rax,0x70(%rsp)
   0x0000000000492f50 <+224>:	mov    0x20(%rsp),%rcx
   0x0000000000492f55 <+229>:	mov    %rcx,0x38(%rsp)
   0x0000000000492f5a <+234>:	mov    0x78(%rsp),%rdx
   0x0000000000492f5f <+239>:	mov    0x8(%rdx),%rbx
   0x0000000000492f63 <+243>:	lea    0x11756(%rip),%rsi        # 0x4a46c0
   0x0000000000492f6a <+250>:	mov    %rsi,(%rsp)
   0x0000000000492f6e <+254>:	mov    %rbx,0x8(%rsp)
   0x0000000000492f73 <+259>:	mov    %rbx,0x10(%rsp)
   0x0000000000492f78 <+264>:	callq  0x43b1a0 <runtime.makeslice>
   0x0000000000492f7d <+269>:	mov    0x28(%rsp),%rax
   0x0000000000492f82 <+274>:	mov    0x20(%rsp),%rcx
   0x0000000000492f87 <+279>:	mov    0x18(%rsp),%rdx
   0x0000000000492f8c <+284>:	mov    0x78(%rsp),%rbx
   0x0000000000492f91 <+289>:	mov    0x8(%rbx),%rsi
   0x0000000000492f95 <+293>:	mov    (%rbx),%rbx
   0x0000000000492f98 <+296>:	mov    0x38(%rsp),%rdi
   0x0000000000492f9d <+301>:	mov    0x70(%rsp),%r8
   0x0000000000492fa2 <+306>:	xor    %r9d,%r9d
   0x0000000000492fa5 <+309>:	jmp    0x492fb7 <main.main+327>
   0x0000000000492fa7 <+311>:	mov    %r10b,(%r12,%r9,1)
   0x0000000000492fab <+315>:	inc    %rbx
   0x0000000000492fae <+318>:	inc    %r9
   0x0000000000492fb1 <+321>:	mov    %r11,%rax
   0x0000000000492fb4 <+324>:	mov    %r12,%rdx
   0x0000000000492fb7 <+327>:	cmp    %rsi,%r9
   0x0000000000492fba <+330>:	jge    0x492fff <main.main+399>
   0x0000000000492fbc <+332>:	movzbl (%rbx),%r10d
   0x0000000000492fc0 <+336>:	test   %rdi,%rdi
   0x0000000000492fc3 <+339>:	je     0x493103 <main.main+659>
   0x0000000000492fc9 <+345>:	mov    %rax,%r11
   0x0000000000492fcc <+348>:	mov    %r9,%rax
   0x0000000000492fcf <+351>:	mov    %rdx,%r12
   0x0000000000492fd2 <+354>:	cmp    $0xffffffffffffffff,%rdi
   0x0000000000492fd6 <+358>:	je     0x492fdf <main.main+367>
   0x0000000000492fd8 <+360>:	cqto   
   0x0000000000492fda <+362>:	idiv   %rdi
   0x0000000000492fdd <+365>:	jmp    0x492fe4 <main.main+372>
   0x0000000000492fdf <+367>:	neg    %rax
   0x0000000000492fe2 <+370>:	xor    %edx,%edx
   0x0000000000492fe4 <+372>:	cmp    %rdi,%rdx
   0x0000000000492fe7 <+375>:	jae    0x4930fc <main.main+652>
   0x0000000000492fed <+381>:	movzbl (%r8,%rdx,1),%edx
   0x0000000000492ff2 <+386>:	xor    %edx,%r10d
   0x0000000000492ff5 <+389>:	cmp    %rcx,%r9
   0x0000000000492ff8 <+392>:	jb     0x492fa7 <main.main+311>
   0x0000000000492ffa <+394>:	jmpq   0x4930fc <main.main+652>
   0x0000000000492fff <+399>:	lea    0x42(%rsp),%rbx
   0x0000000000493004 <+404>:	mov    %rbx,(%rsp)
   0x0000000000493008 <+408>:	movq   $0xe,0x8(%rsp)
   0x0000000000493011 <+417>:	movq   $0xe,0x10(%rsp)
   0x000000000049301a <+426>:	mov    %rdx,0x18(%rsp)
   0x000000000049301f <+431>:	mov    %rcx,0x20(%rsp)
   0x0000000000493024 <+436>:	mov    %rax,0x28(%rsp)
   0x0000000000493029 <+441>:	callq  0x4510d0 <bytes.Compare>
   0x000000000049302e <+446>:	mov    0x30(%rsp),%rax
   0x0000000000493033 <+451>:	test   %rax,%rax
   0x0000000000493036 <+454>:	jne    0x4930a1 <main.main+561>
   0x0000000000493038 <+456>:	movq   $0x0,0xa0(%rsp)
   0x0000000000493044 <+468>:	movq   $0x0,0xa8(%rsp)
   0x0000000000493050 <+480>:	lea    0x11529(%rip),%rax        # 0x4a4580
   0x0000000000493057 <+487>:	mov    %rax,0xa0(%rsp)
   0x000000000049305f <+495>:	lea    0x4306a(%rip),%rax        # 0x4d60d0 <main.statictmp_0>
   0x0000000000493066 <+502>:	mov    %rax,0xa8(%rsp)
   0x000000000049306e <+510>:	lea    0xa0(%rsp),%rax
   0x0000000000493076 <+518>:	mov    %rax,(%rsp)
   0x000000000049307a <+522>:	movq   $0x1,0x8(%rsp)
   0x0000000000493083 <+531>:	movq   $0x1,0x10(%rsp)
   0x000000000049308c <+540>:	callq  0x486bc0 <fmt.Print>
   0x0000000000493091 <+545>:	mov    0xb0(%rsp),%rbp
   0x0000000000493099 <+553>:	add    $0xb8,%rsp
   0x00000000004930a0 <+560>:	retq   
   0x00000000004930a1 <+561>:	movq   $0x0,0x90(%rsp)
   0x00000000004930ad <+573>:	movq   $0x0,0x98(%rsp)
   0x00000000004930b9 <+585>:	lea    0x114c0(%rip),%rax        # 0x4a4580
   0x00000000004930c0 <+592>:	mov    %rax,0x90(%rsp)
   0x00000000004930c8 <+600>:	lea    0x43011(%rip),%rax        # 0x4d60e0 <main.statictmp_1>
   0x00000000004930cf <+607>:	mov    %rax,0x98(%rsp)
   0x00000000004930d7 <+615>:	lea    0x90(%rsp),%rax
   0x00000000004930df <+623>:	mov    %rax,(%rsp)
   0x00000000004930e3 <+627>:	movq   $0x1,0x8(%rsp)
   0x00000000004930ec <+636>:	movq   $0x1,0x10(%rsp)
   0x00000000004930f5 <+645>:	callq  0x486bc0 <fmt.Print>
   0x00000000004930fa <+650>:	jmp    0x493091 <main.main+545>
   0x00000000004930fc <+652>:	callq  0x425a40 <runtime.panicindex>
   0x0000000000493101 <+657>:	ud2    
   0x0000000000493103 <+659>:	callq  0x425b20 <runtime.panicdivide>
   0x0000000000493108 <+664>:	ud2    
   0x000000000049310a <+666>:	callq  0x44ef70 <runtime.morestack_noctxt>
   0x000000000049310f <+671>:	jmpq   0x492e70 <main.main>
End of assembler dump.
~~~

Inserting a breakpoint at 0x4510d0 before the xor, we can see the comparison string:

~~~
gdb) b* 0x4510d0
Breakpoint 4 at 0x4510d0: file /usr/lib/go/src/runtime/asm_amd64.s, line 1493.
(gdb) run
Starting program: ch32.bin 
[New LWP 6904]
[New LWP 6905]
[New LWP 6906]
[New LWP 6907]
test

Thread 1 "ch32.bin" hit Breakpoint 4, bytes.Compare () at /usr/lib/go/src/runtime/asm_amd64.s:1493
1493	/usr/lib/go/src/runtime/asm_amd64.s: No such file or directory.
(gdb) x/s $rbx
0xc420059f02:	";\002#\033\033\f\034\b(\033!\004\034\vrootme"
~~~

This shows the input is xord with "rootme" before the compare call. Taking rootme and the comparator, these can be xord to get the solution 

</details>

### Answer

<details>

<summary markdown="span">Answer</summary>

~~~
ImLovingGoLand
~~~

</details>

---

### [Cracking](#contents) | [Root-Me](./rootme.md) | [Home](./index.md)

---

## ELF x86 Fake Instructions

- Author: kmkz
- Date: 21 February 2010
- Points: 15
- Level: 2

### Statement

Some fakes instructions.

- Compiled with gcc 4.3.2 on Xubuntu 8.04.
- Proc : 32bits x86.

### Attachments

1. [ch4.zip](http://challenge01.root-me.org/cracking/ch4/ch4.zip).

### Resources

1. [GNU Binary Utils](https://repository.root-me.org/Administration/Unix/Linux/EN%20-%20The%20GNU%20binary%20utils.pdf)
2. [Executable and Linkable Format ELF](https://repository.root-me.org/Reverse%20Engineering/x86/Unix/EN%20-%20Executable%20and%20Linkable%20Format%20ELF.pdf)
3. [Reverse engineering Linux ELF binaries on the x86 platform](https://repository.root-me.org/Reverse%20Engineering/x86/Unix/EN%20-%20Reverse%20engineering%20Linux%20ELF%20binaries%20on%20the%20x86%20platform.pdf)

### Solutions

<details>

<summary markdown="span">Solution 1</summary>

We can retrieve the zipfile using wget:

~~~shell
$ wget http://challenge01.root-me.org/cracking/ch4/ch4.zip
--2022-02-27 11:31:49--  http://challenge01.root-me.org/cracking/ch4/ch4.zip
Resolving challenge01.root-me.org (challenge01.root-me.org)... 212.129.38.224, 2001:bc8:35b0:c166::151
Connecting to challenge01.root-me.org (challenge01.root-me.org)|212.129.38.224|:80... connected.
HTTP request sent, awaiting response... 200 OK
Length: 3847 (3.8K) [application/zip]
Saving to: ‘ch4.zip’

ch4.zip                                                     100%[=========================================================================================================================================>]   3.76K  --.-KB/s    in 0s      

2022-02-27 11:31:49 (141 MB/s) - ‘ch4.zip’ saved [3847/3847]

~~~

We can unzip and inspect:

~~~shell
$ unzip ch4.zip 
Archive:  ch4.zip
  inflating: crackme  
$ file crackme 
crackme: ELF 32-bit LSB executable, Intel 80386, version 1 (SYSV), dynamically linked, interpreter /lib/ld-linux.so.2, for GNU/Linux 2.6.8, with debug_info, not stripped     
~~~

Using Ghidra, we can see the main function calls a subroutine, WPA to compare two strings.  The function blowfish() is called:

~~~c
void blowfish(void)

{
  uint uVar1;
  int in_GS_OFFSET;
  uint local_50;
  undefined4 local_44;
  undefined4 local_40;
  undefined4 local_3c;
  undefined4 local_38;
  undefined2 uStack52;
  undefined auStack50 [17];
  undefined4 local_21;
  undefined4 local_1d;
  undefined4 local_19;
  undefined4 local_15;
  undefined4 local_11;
  undefined4 local_d;
  undefined local_9;
  undefined4 local_8;
  
  local_8 = *(undefined4 *)(in_GS_OFFSET + 0x14);
  local_44 = 0x6562696c;
  local_40 = 0xa9c37472;
  local_3c = 0x21;
  local_50 = 0;
  uVar1 = local_50;
  do {
    local_50 = uVar1;
    *(undefined4 *)((int)&local_38 + local_50) = 0;
    uVar1 = local_50 + 4;
  } while (local_50 + 4 < 0x14);
  *(undefined2 *)(auStack50 + (local_50 - 2)) = 0;
  auStack50[local_50] = 0;
  local_21 = 0x4763305f;
  local_1d = 0x6d35636a;
  local_19 = 0x54352e5f;
  local_15 = 0x3887c333;
  local_11 = 0xc3304a43;
  local_d = 0x39483980;
  local_9 = 0;
  printf(&DAT_08048998,&local_44);
                    /* WARNING: Subroutine does not return */
  exit(0);
}
~~~

This prints &DAT_08048998 and the local_44 variable:

~~~
'+) Authentification r  ussie...
 U'r root! 
 
 sh 3.0 # password:
~~~

The local44 variable can be inspected from the declaration:

~~~
  local_44 = 0x6562696c;
  local_40 = 0xa9c37472;
  local_3c = 0x21;
  local_50 = 0;
~~~

Converting these to ASCII:

~~~
  local_44 = "ebil";
  local_40 = "©Ãtr";
  local_3c = "!";
~~~

These are held in memory addresses 0x0804873d - 0x0804874b.  In gdb, we can place a break at the printf command and run:

~~~
(gdb) b* printf
Breakpoint 1 at 0x804843c
(gdb) run
Starting program: crackme 

Breakpoint 1, 0xf7dcc340 in printf () from /lib/i386-linux-gnu/libc.so.6
~~~

We can print this memory address:

~~~
(gdb) x/s 0x0804873d
0x804873d <blowfish+17>:	"\307E\300libe\307E\304rté\307E\310!"
~~~

Removing the superfluous string commands, we can get the solution.

</details>

### Answer

<details>

<summary markdown="span">Answer</summary>

~~~
liberté!
~~~

</details>

---

### [Cracking](#contents) | [Root-Me](./rootme.md) | [Home](./index.md)

---


## ELF x86 Ptrace

- Author: g0uZ
- Date: 27 November 2009
- Points: 15
- Level: 2

### Statement

-

### Attachments

1. [ch3.bin](http://challenge01.root-me.org/cracking/ch3/ch3.bin).

### Resources

1. [GNU Binary Utils](https://repository.root-me.org/Administration/Unix/Linux/EN%20-%20The%20GNU%20binary%20utils.pdf)
2. [Ptrace](https://repository.root-me.org/Reverse%20Engineering/x86/Unix/EN%20-%20Ptrace%20-%20process%20trace.pdf)

### Solutions

<details>

<summary markdown="span">Solution 1</summary>

We can retrieve the binary using wget:

~~~shell
$ wget http://challenge01.root-me.org/cracking/ch3/ch3.bin
--2022-02-27 11:48:57--  http://challenge01.root-me.org/cracking/ch3/ch3.bin
Resolving challenge01.root-me.org (challenge01.root-me.org)... 212.129.38.224, 2001:bc8:35b0:c166::151
Connecting to challenge01.root-me.org (challenge01.root-me.org)|212.129.38.224|:80... connected.
HTTP request sent, awaiting response... 200 OK
Length: 708072 (691K) [application/octet-stream]
Saving to: ‘ch3.bin’

ch3.bin                                                     100%[=========================================================================================================================================>] 691.48K  2.21MB/s    in 0.3s    

2022-02-27 11:48:58 (2.21 MB/s) - ‘ch3.bin’ saved [708072/708072]
~~~

Decompiling and analysing in Ghidra, we find the main function compares the user input to a defined string:

~~~c
  local_14 = "ksuiealohgy";
  lVar1 = ptrace(PTRACE_TRACEME,0,1,0);
  if (lVar1 < 0) {
    puts(&DAT_080c2894);
    uVar2 = 1;
  }
  else {
    puts("############################################################");
    puts("##        Bienvennue dans ce challenge de cracking        ##");
    puts("############################################################\n");
    printf("Password : ");
    fgets(&local_1e,9,(FILE *)stdin);
    if ((((local_1e == local_14[4]) && (local_1d == local_14[5])) && (local_1c == local_14[1])) &&
       (local_1b == local_14[10])) {
      puts("\nGood password !!!\n");
~~~

Simplifying, we get:

~~~
local_1e = local_14[4] = "e"
local_1d = local_14[5] = "a"
local_1c = local_14[1] = "s"
local_1b = local_14[10] = "y"
~~~

</details>

### Answer

<details>

<summary markdown="span">Answer</summary>

~~~
easy
~~~

</details>

---

### [Cracking](#contents) | [Root-Me](./rootme.md) | [Home](./index.md)

---


Last updated Nov 2022.

## [djm89uk.github.io](https://djm89uk.github.io)
