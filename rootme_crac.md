# [Root-Me](./rootme.md) Root-Me Cracking [3/46]

Reverse binaries and crack executables. 

## Contents

1. [ELF x86 - 0 protection](#elf-x86-0-protection) 🗸
2. [ELF x86 - Basic](#elf-x86-basic) 🗸
3. [PE x86 - 0 protection](#pe-x86-0-protection) 🗸
4. [ELF C++ - 0 protection](#elf-cpp-0-protection)
5. [PE DotNet - 0 protection](#pe-dotnet-0-protection)
6. [ELF MIPS - Basic Crackme](#elf-mips-basic-crackme)
7. [ELF x64 - Golang basic](#elf-x64-golang-basic)
8. [ELF x86 - Fake Instructions](#elf-x86-fake-instructions)
9. [ELF x86 - Ptrace](#elf-x86-ptrace)
10. [WASM - Introduction](#wasm-introduction)
11. [ELF ARM - Basic Crackme](#elf-arm-basic-crackme)
12. [ELF x64 - Basic KeygenMe](#elf-x64-basic-keygenme)
13. [PE DotNet - Basic Anti-Debug](#pe-dotnet-basic-anti-debug)
14. [PE DotNet - Basic Crackme](#pe-dotnet-basic-crackme)
15. [PYC - ByteCode](#pyc-bytecode)
16. [ELF x86 - No software breakpoints](#elf-x86-no-software-breakpoints)
17. [Lua - Bytecode](#lua-bytecode)
18. [MachO x64 - keygenme or not](#macho-x64-keygenme-or-not)
19. [ELF ARM - crackme 1337](#elf-arm-crackme-1337)
20. [ELF x86 - CrackPass](#elf-x86-crackpass)
21. [ELF x86 - ExploitMe](#elf-x86-exploitme)
22. [ELF x86 - Random Crackme](#elf-x86-random-crackme)
23. [GB - Basic GameBoy crackme](#gb-basic-gameboy-crackme)
24. [PDF - Javascript](#pdf-javascript)
25. [PE x86 - Xor Madness](#pe-x86-xor-madness)
26. [ELF ARM - Crypted](#elf-arm-crypted)
27. [ELF x64 - Crackme automating](#elf-x64-crackme-automating)
28. [PE x86 - SEHVEH](#pe-x86-sehveh)
29. [Powershell DeObfuscation](#powershell-deobfuscation)
30. [APK - Anti-debug](#apk-anti-debug)
31. [ELF x64 - Nanomites - Introduction](#elf-x64-nanomites-introduction)
32. [ELF x86 - Anti-debug](#elf-x86-anti-debug)
33. [PE DotNet - KeygenMe](#pe-dotnet-keygenme)
34. [PE x86 - AutoPE](#pe-x86-autope)
35. [ELF x86 - KeygenMe](#elf-x86-keygenme)
36. [WASM - Find the NPC](#wasm-find-the-npc)
37. [Bash - VM](#bash-vm)
38. [ELF x64 - KeyGenMe](#elf-x64-keygenme)
39. [ELF x64 - Anti-debug and equations](#elf-x64-anti-debug-and-equations)
40. [ELF x64 - Nanomites](#elf-x64-nanomites)
41. [ELF x86 - Packed](#elf-x86-packed)
42. [PE x86 - RunPE](#pe-x86-runpe)
43. [ELF x86 - VM](#elf-x86-vm)
44. [ELF x64 - Hidden Control Flow](#elf-x64-hidden-control-flow)
45. [Ringgit](#ringgit)
46. [White-Box Cryptography #2](#white-box-cryptography-#2)

---

### [Cracking](#contents) | [Root-Me](./rootme.md) | [Home](./index.md)

---

## ELF x86 - 0 protection

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

## ELF x86 - Basic

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

Last updated Jan 2022.

## [djm89uk.github.io](https://djm89uk.github.io)
