# [PicoCTF](./picoctf.md) Binary Exploitation

Binary exploitation is the process of subverting a compiled application such that it violates some trust boundary in a way that is advantageous to you, the attacker.

## Contents

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
- [cutter-overflow (2021)](#cutter-overflow)
- [fermat-strings (2021)](#fermat-strings)
- [SaaS (2021)](#saas)
- [homework (2021)](#homework)
- [lockdown-horses (2021)](#lockdown-horses)
- [vr-school (2021)](#vr-school)

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

attachment

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

## clutter overflow

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

## [djm89uk.github.io](https://djm89uk.github.io)
