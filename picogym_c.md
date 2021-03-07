# [PicoGym](./picogym.md) Cryptography

Cryptography is essential to many models of cyber security. Cryptography applies algorithms to shuffle the bits that represent data in such a way that only authorized users can unshuffle them to obtain the original data. 

## Contents

- [The Numbers](#the-numbers)
- [caesar](#caesar)
- [Easy1](#easy1)
- [13](#thirteen)
- [la cifra de](#la-cifra-de)
- [rsa pop quiz](#rsa-pop-quiz)
- [Tapping](#tapping)
- [Mr-Worldwide](#mr-worldwide)
- [Flags](#flags)
- [waves over lambda](#waves-over-lambda)
- [miniRSA](#minirsa)
- [b00tl3gRSA2](#b00tl3grsa2)
- [AES-ABC](#aes-abc)
- [b00tl3gRSA3](#b00tl3grsa3)
- [john_pollard](#john-pollard)

---

### [Cryptography](#contents) | [PicoGym](./picogym.md) | [PicoCTF](./picoctf.md) | [Home](./index.md)

---

## The Numbers

- Author: Danny
- 50 Points

### Description

The numbers... what do they mean?

### Hints

1. The flag is in the format PICOCTF{}

### Attachments

<details>

<summary markdown="span">numbers.png</summary>

<div markdonw="1">

![numbers.png]({{site.url}}/resources/picoctf/picogym/attachments/cryptography/the-numbers/numbers.png)

</div>

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

### [Cryptography](#contents) | [PicoGym](./picogym.md) | [PicoCTF](./picoctf.md) | [Home](./index.md)

---

## caesar

- Author: Sanjay C/Daniel Tunitis
- 100 points

### Description

Decrypt this message.

### Hints

1. caesar cipher [tutorial](https://learncryptography.com/classical-encryption/caesar-cipher)

### Attachments

<details>

<summary markdown="span">ciphertext</summary>

~~~
picoCTF{gvswwmrkxlivyfmgsrhnrisegl}
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

### [Cryptography](#contents) | [PicoGym](./picogym.md) | [PicoCTF](./picoctf.md) | [Home](./index.md)

---

## Easy1

- Author: Alex Fulton/Danny
- 100 points

### Description

The one time pad can be cryptographically secure, but not when you know the key. Can you solve this? We've given you the encrypted flag, key, and a table to help UFJKXQZQUNB with the key of SOLVECRYPTO. Can you use this table to solve it?. 

### Hints

1. Submit your answer in our flag format. For example, if your answer was 'hello', you would submit 'picoCTF{HELLO}' as the flag.
2. Please use all caps for the message.

### Attachments

<details>

<summary markdown="span">table.txt</summary>

~~~
    A B C D E F G H I J K L M N O P Q R S T U V W X Y Z 
   +----------------------------------------------------
A | A B C D E F G H I J K L M N O P Q R S T U V W X Y Z
B | B C D E F G H I J K L M N O P Q R S T U V W X Y Z A
C | C D E F G H I J K L M N O P Q R S T U V W X Y Z A B
D | D E F G H I J K L M N O P Q R S T U V W X Y Z A B C
E | E F G H I J K L M N O P Q R S T U V W X Y Z A B C D
F | F G H I J K L M N O P Q R S T U V W X Y Z A B C D E
G | G H I J K L M N O P Q R S T U V W X Y Z A B C D E F
H | H I J K L M N O P Q R S T U V W X Y Z A B C D E F G
I | I J K L M N O P Q R S T U V W X Y Z A B C D E F G H
J | J K L M N O P Q R S T U V W X Y Z A B C D E F G H I
K | K L M N O P Q R S T U V W X Y Z A B C D E F G H I J
L | L M N O P Q R S T U V W X Y Z A B C D E F G H I J K
M | M N O P Q R S T U V W X Y Z A B C D E F G H I J K L
N | N O P Q R S T U V W X Y Z A B C D E F G H I J K L M
O | O P Q R S T U V W X Y Z A B C D E F G H I J K L M N
P | P Q R S T U V W X Y Z A B C D E F G H I J K L M N O
Q | Q R S T U V W X Y Z A B C D E F G H I J K L M N O P
R | R S T U V W X Y Z A B C D E F G H I J K L M N O P Q
S | S T U V W X Y Z A B C D E F G H I J K L M N O P Q R
T | T U V W X Y Z A B C D E F G H I J K L M N O P Q R S
U | U V W X Y Z A B C D E F G H I J K L M N O P Q R S T
V | V W X Y Z A B C D E F G H I J K L M N O P Q R S T U
W | W X Y Z A B C D E F G H I J K L M N O P Q R S T U V
X | X Y Z A B C D E F G H I J K L M N O P Q R S T U V W
Y | Y Z A B C D E F G H I J K L M N O P Q R S T U V W X
Z | Z A B C D E F G H I J K L M N O P Q R S T U V W X Y

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

### [Cryptography](#contents) | [PicoGym](./picogym.md) | [PicoCTF](./picoctf.md) | [Home](./index.md)

---

## thirteen

- Author: Alex Fulton/Daniel Tunitis
- 100 points

### Description

Cryptography can be easy, do you know what ROT13 is? cvpbPGS{abg_gbb_onq_bs_n_ceboyrz}

### Hints

1. This can be solved online if you don't want to do it by hand!

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

### [Cryptography](#contents) | [PicoGym](./picogym.md) | [PicoCTF](./picoctf.md) | [Home](./index.md)

---

## la cifra de

- Author: Alex Fulton/Daniel Tunitis
- 200 points

### Description

I found this cipher in an old book. Can you figure out what it says? Connect with nc jupiter.challenges.picoctf.org 5726.

### Hints

1. There are tools that make this easy.
2. Perhaps looking at history will help

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

### [Cryptography](#contents) | [PicoGym](./picogym.md) | [PicoCTF](./picoctf.md) | [Home](./index.md)

---

## rsa-pop-quiz

- Author: wparks/nmontierth
- 200 points

### Description

Class, take your seats! It's PRIME-time for a quiz... nc jupiter.challenges.picoctf.org 1981

### Hints

1. [RSA info](https://simple.wikipedia.org/wiki/RSA_algorithm).

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

### [Cryptography](#contents) | [PicoGym](./picogym.md) | [PicoCTF](./picoctf.md) | [Home](./index.md)

---

## Tapping

- Author: Danny
- 200 points

### Description

heres tapping coming in from the wires. What's it saying nc jupiter.challenges.picoctf.org 48247.

### Hints

1. What kind of encoding uses dashes and dots?
2. The flag is in the format PICOCTF{}

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

### [Cryptography](#contents) | [PicoGym](./picogym.md) | [PicoCTF](./picoctf.md) | [Home](./index.md)

---

## Mr-Worldwide

- Author: Danny
- 200 points

### Description

A musician left us a message. What's it mean?

### Hints

None

### Attachments

<details>

<summary markdown="span">message.txt</summary>

~~~
picoCTF{(35.028309, 135.753082)(46.469391, 30.740883)(39.758949, -84.191605)(41.015137, 28.979530)(24.466667, 54.366669)(3.140853, 101.693207)_(9.005401, 38.763611)(-3.989038, -79.203560)(52.377956, 4.897070)(41.085651, -73.858467)(57.790001, -152.407227)(31.205753, 29.924526)}
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

### [Cryptography](#contents) | [PicoGym](./picogym.md) | [PicoCTF](./picoctf.md) | [Home](./index.md)

---
## Flags

- Author: Danny
- 200 points

### Description

What do the flags mean?

### Hints

1. The flag is in the format PICOCTF{}

### Attachments

- flags.png

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

### [Cryptography](#contents) | [PicoGym](./picogym.md) | [PicoCTF](./picoctf.md) | [Home](./index.md)

---
## waves over lambda

- Author: invisibility/danny
- 300 points

### Description

We made a lot of substitutions to encrypt this. Can you decrypt it? Connect with nc jupiter.challenges.picoctf.org 39894.

### Hints

1. Flag is not in the usual flag format

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

### [Cryptography](#contents) | [PicoGym](./picogym.md) | [PicoCTF](./picoctf.md) | [Home](./index.md)

---
## miniRSA

- Author: speeeday/Danny
- 300 points

### Description

Let's decrypt this: ciphertext? Something seems a bit small.

### Hints

1. RSA [tutorial](https://en.wikipedia.org/wiki/RSA_(cryptosystem)).
2. How could having too small an e affect the security of this 2048 bit key?
3. Make sure you don't lose precision, the numbers are pretty big (besides the e value).

### Attachments

<details>

<summary markdown="span">ciphertext</summary>

~~~

N: 29331922499794985782735976045591164936683059380558950386560160105740343201513369939006307531165922708949619162698623675349030430859547825708994708321803705309459438099340427770580064400911431856656901982789948285309956111848686906152664473350940486507451771223435835260168971210087470894448460745593956840586530527915802541450092946574694809584880896601317519794442862977471129319781313161842056501715040555964011899589002863730868679527184420789010551475067862907739054966183120621407246398518098981106431219207697870293412176440482900183550467375190239898455201170831410460483829448603477361305838743852756938687673
e: 3

ciphertext (c): 2205316413931134031074603746928247799030155221252519872650080519263755075355825243327515211479747536697517688468095325517209911688684309894900992899707504087647575997847717180766377832435022794675332132906451858990782325436498952049751141 
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

### [Cryptography](#contents) | [PicoGym](./picogym.md) | [PicoCTF](./picoctf.md) | [Home](./index.md)

---
## b00tl3gRSA2

- Author: invisibility
- 400 points

### Description

In RSA d is a lot bigger than e, why don't we use d to encrypt instead of e? Connect with nc jupiter.challenges.picoctf.org 57464.

### Hints

1. What is e generally?

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

### [Cryptography](#contents) | [PicoGym](./picogym.md) | [PicoCTF](./picoctf.md) | [Home](./index.md)

---
## AES-ABC

- Author: waituckw
- 400 points

### Description

AES-ECB is bad, so I rolled my own cipher block chaining mechanism - Addition Block Chaining! You can find the source here: aes-abc.py. The AES-ABC flag is body.enc.ppm

### Hints

1. You probably want to figure out what the flag looks like in ECB form...

### Attachments

- body.enc.ppm

<details>

<summary markdown="span">aes-abc.py</summary>

~~~py
#!/usr/bin/env python
from Crypto.Cipher import AES
from key import KEY
import os
import math
BLOCK_SIZE = 16
UMAX = int(math.pow(256, BLOCK_SIZE))
def to_bytes(n):
    s = hex(n)
    s_n = s[2:]
    if 'L' in s_n:
        s_n = s_n.replace('L', '')
    if len(s_n) % 2 != 0:
        s_n = '0' + s_n
    decoded = s_n.decode('hex')
    pad = (len(decoded) % BLOCK_SIZE)
    if pad != 0: 
        decoded = "\0" * (BLOCK_SIZE - pad) + decoded
    return decoded
def remove_line(s):
    # returns the header line, and the rest of the file
    return s[:s.index('\n') + 1], s[s.index('\n')+1:]
def parse_header_ppm(f):
    data = f.read()
    header = ""
    for i in range(3):
        header_i, data = remove_line(data)
        header += header_i
    return header, data
def pad(pt):
    padding = BLOCK_SIZE - len(pt) % BLOCK_SIZE
    return pt + (chr(padding) * padding)
def aes_abc_encrypt(pt):
    cipher = AES.new(KEY, AES.MODE_ECB)
    ct = cipher.encrypt(pad(pt))
    blocks = [ct[i * BLOCK_SIZE:(i+1) * BLOCK_SIZE] for i in range(len(ct) / BLOCK_SIZE)]
    iv = os.urandom(16)
    blocks.insert(0, iv)
    for i in range(len(blocks) - 1):
        prev_blk = int(blocks[i].encode('hex'), 16)
        curr_blk = int(blocks[i+1].encode('hex'), 16)
        n_curr_blk = (prev_blk + curr_blk) % UMAX
        blocks[i+1] = to_bytes(n_curr_blk)
    ct_abc = "".join(blocks)
    return iv, ct_abc, ct
if __name__=="__main__":
    with open('flag.ppm', 'rb') as f:
        header, data = parse_header_ppm(f)
    iv, c_img, ct = aes_abc_encrypt(data)
    with open('body.enc.ppm', 'wb') as fw:
        fw.write(header)
        fw.write(c_img)
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

### [Cryptography](#contents) | [PicoGym](./picogym.md) | [PicoCTF](./picoctf.md) | [Home](./index.md)

---
## b00tl3gRSA3

- Author: invisibility
- 450 points

### Description

Why use p and q when I can use more? Connect with nc jupiter.challenges.picoctf.org 3726.

### Hints

1. There's more prime factors than p and q, finding d is going to be different.

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

### [Cryptography](#contents) | [PicoGym](./picogym.md) | [PicoCTF](./picoctf.md) | [Home](./index.md)

---
## john-pollard

- Author: Samuel S
- 500 points

### Description

Sometimes RSA certificates are breakable.

### Hints

1. The flag is in the format picoCTF{p,q}.
2. Try swapping p and q if it does not work.

### Attachments

- cert

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

### [Cryptography](#contents) | [PicoGym](./picogym.md) | [PicoCTF](./picoctf.md) | [Home](./index.md)

---

## [djm89uk.github.io](https://djm89uk.github.io)
