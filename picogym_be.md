# [PicoCTF](./picoctf.md) Binary Exploitation

Binary exploitation is the process of subverting a compiled application such that it violates some trust boundary in a way that is advantageous to you, the attacker.

## Contents

- [messy-malloc (2019)](#messy-malloc)
- [seed-sPRiNG (2019)](#seed-spring)
- [sice_cream (2019)](#sice-cream)
- [zero_to_hero (2019)](#zero-to-hero)
- [Guessing Game 1 (2020)](#guessing-game-1)
- [Guessing Game 2 (2020)](#guessing-game-2)
- [Stonks (2021)](#stonks)
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
- [clutter-overflow (2021)](#clutter-overflow)
- [fermat-strings (2021)](#fermat-strings)
- [SaaS (2021)](#saas)
- [homework (2021)](#homework)
- [lockdown-horses (2021)](#lockdown-horses)
- [vr-school (2021)](#vr-school)

---

### [Binary Exploitation](#contents) | [PicoCTF](./picoctf.md) | [Home](./index.md)

---

## Guessing Game 1

- Author: madStacks
- 250 Points

### Description

I made a simple game to show off my programming skills. See if you can beat it! vuln vuln.c Makefile nc jupiter.challenges.picoctf.org 28953

### Hints

1. Tools can be helpful, but you may need to look around for yourself.
2. Remember, in CTF problems, if something seems weird it probably means something...

### Attachments

[vuln](./resources/picoctf/picogym/attachments/binary-exploitation/guessing-game-1/vuln)

<details>

<summary markdown="span">vuln.c</summary>

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

</details>

<details>

<summary markdown="span">Makefile</summary>

~~~
all:
	gcc -m64 -fno-stack-protector -O0 -no-pie -static -o vuln vuln.c

clean:
	rm vuln
~~~

</details>

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

## Guessing Game 2

- Author: madStacks
- 300 points

### Description

It's the Return of your favorite game! vuln vuln.c Makefile nc jupiter.challenges.picoctf.org 13610

### Hints

1. No longer a static binary, but maybe this will help https://libc.blukat.me/
2. Check out the other differences in the Makefile as well.

### Attachments

[vuln](./resources/picoctf/picogym/attachments/binary-exploitation/guessing-game-2/vuln)

<details>

<summary markdown="span">vuln.c</summary>

~~~c
#include <stdio.h>
#include <stdlib.h>
#include <unistd.h>
#include <sys/types.h>
#include <sys/stat.h>
#define BUFSIZE 512
long get_random() {
	return rand;
}
int get_version() {
	return 2;
}
int do_stuff() {
	long ans = (get_random() % 4096) + 1;
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
	gets(winner);
	printf("Congrats: ");
	printf(winner);
	printf("\n\n");
}
int main(int argc, char **argv){
	setvbuf(stdout, NULL, _IONBF, 0);
	// Set the gid to the effective gid
	// this prevents /bin/sh from dropping the privileges
	gid_t gid = getegid();
	setresgid(gid, gid, gid);
	int res;
	printf("Welcome to my guessing game!\n");
	printf("Version: %x\n\n", get_version());
	while (1) {
		res = do_stuff();
		if (res) {
			win();
		}
	}
	return 0;
}
~~~

</details>

<details>

<summary markdown="span">Makefile</summary>

~~~
all:
	gcc -m32 -no-pie -Wl,-z,relro,-z,now -o vuln vuln.c

clean:
	rm vuln
~~~

</details>

### Solutions

<details>

<summary markdown="span">Solution 1</summary>

Solution here

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

## messy-malloc

- Author: Sanjay C.
- 300 points

### Description

Can you take advantage of misused malloc calls to leak the secret through this [service](https://jupiter.challenges.picoctf.org/static/dc29193cdec351ca7dbb3e931eee6a83/auth) and get the flag? Connect with nc jupiter.challenges.picoctf.org 1541. Source.

### Hints

1. If only the program used calloc to zero out the memory...

### Attachments

[auth](./resources/picoctf/picogym/attachments/binary-exploitation/messy-malloc/auth)

<details>

<summary markdown="span">auth.c</summary>

~~~c
#include <stdio.h>
#include <stdlib.h>
#include <stdint.h>
#include <string.h>
#define LINE_MAX 256
#define ACCESS_CODE_LEN 16
#define FLAG_SIZE 64
struct user {
  char *username;
  char access_code[ACCESS_CODE_LEN];
  char *files;
};
struct user anon_user;
struct user *u;
void print_flag() {
  char flag[FLAG_SIZE];
  FILE *f = fopen("flag.txt", "r");
  if (f == NULL) {
    printf("Please make sure flag.txt exists\n");
    exit(0);
  }
  if ((fgets(flag, FLAG_SIZE, f)) == NULL){
    puts("Couldn't read flag file.");
    exit(1);
  };
  unsigned long ac1 = ((unsigned long *)u->access_code)[0];
  unsigned long ac2 = ((unsigned long *)u->access_code)[1];
  if (ac1 != 0x4343415f544f4f52 || ac2 != 0x45444f435f535345) {
    fprintf(stdout, "Incorrect Access Code: \"");
    for (int i = 0; i < ACCESS_CODE_LEN; i++) {
      putchar(u->access_code[i]);
    }
    fprintf(stdout, "\"\n");
    return;
  } 
  puts(flag);
  fclose(f);
}
void menu() {
  puts("Commands:");
  puts("\tlogin - login as a user");
  puts("\tprint-flag - print the flag");
  puts("\tlogout - log out");
  puts("\tquit - exit the program");
}
const char *get_username(struct user *u) {
  if (u->username == NULL) {
    return "anon";
  }
  else {
    return u->username;
  }
}
int login() {
  u = malloc(sizeof(struct user));
  int username_len;
  puts("Please enter the length of your username");
  scanf("%d", &username_len);
  getc(stdin);
  char *username = malloc(username_len+1);
  u->username = username;
  puts("Please enter your username");
  if (fgets(username, username_len, stdin) == NULL) {
    puts("fgets failed");
    exit(-1);
  }
  char *end;
  if ((end=strchr(username, '\n')) != NULL) {
    end[0] = '\0';
  }
  return 0; 
}
int logout() {
  char *user = u->username;
  if (u == &anon_user) {
    return -1;
  }
  else {
    free(u);
    free(user);
    u = &anon_user;
  }
  return 0;
}
int main(int argc, char **argv) {
  setbuf(stdout, NULL);
  char buf[LINE_MAX];
  memset(anon_user.access_code, 0, ACCESS_CODE_LEN);
  anon_user.username = NULL;
  u = &anon_user;
  menu();
  while(1) {
    puts("\nEnter your command:");
    fprintf(stdout, "[%s]> ", get_username(u));
    if(fgets(buf, LINE_MAX, stdin) == NULL)
      break;
    if (!strncmp(buf, "login", 5)){
      login();
    }
    else if(!strncmp(buf, "print-flag", 10)){
      print_flag();
    }
    else if(!strncmp(buf, "logout", 6)){
      logout();
    }
    else if(!strncmp(buf, "quit", 4)){
      return 0;
    }
    else{
      puts("Invalid option");
      menu();
    }
  }
}
~~~

</details>

### Solutions

<details>

<summary markdown="span">Solution 1</summary>

Solution here

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

## seed-sPRiNG

- Author: John Hammond
- 350 points

### Description

The most revolutionary game is finally available: seed sPRiNG is open right now! seed_spring. Connect to it with nc jupiter.challenges.picoctf.org 34558.

### Hints

1. How is that program deciding what the height is?
2. You and the program should sync up!

### Attachments

[seed_spring](./resources/picoctf/picogym/attachments/binary-exploitation/seed-spring/seed_spring)

### Solutions

<details>

<summary markdown="span">Solution 1</summary>

Solution here

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

## sice-cream

- Author: Samuel
- 500 points

### Description

Just pwn this program and get a flag. Connect with nc jupiter.challenges.picoctf.org 39673. libc.so.6 ld-2.23.so.

### Hints

1. Make sure to both files are in the same directory as the executable, and set LD_PRELOAD to the path of libc.so.6

### Attachments

[sice_cream](./resources/picoctf/picogym/attachments/binary-exploitation/sice_cream/sice_cream)

[libc.so.6](./resources/picoctf/picogym/attachments/binary-exploitation/sice_cream/libc.so.6)

[ld-2.23.so](./resources/picoctf/picogym/attachments/binary-exploitation/sice_cream/ld-2.23.so)

### Solutions

<details>

<summary markdown="span">Solution 1</summary>

Solution here

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

## zero-to-hero

- Author: Claude
- 500 points

### Description

Now you're really cooking. Can you pwn this service?. Connect with nc jupiter.challenges.picoctf.org 22056. libc.so.6 ld-2.29.so

### Hints

1. Make sure to both files are in the same directory as the executable, and set LD_PRELOAD to the path of libc.so.6

### Attachments

[zero_to_hero](./resources/picoctf/picogym/attachments/binary-exploitation/zero-to-hero/zero_to_hero)

[libc.so.6](./resources/picoctf/picogym/attachments/binary-exploitation/zero-to-hero/libc.so.6)

[ld-2.29.so](./resources/picoctf/picogym/attachments/binary-exploitation/zero-to-hero/ld-2.29.so)

### Solutions

<details>

<summary markdown="span">Solution 1</summary>

Solution here

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

## [djm89uk.github.io](https://djm89uk.github.io)
