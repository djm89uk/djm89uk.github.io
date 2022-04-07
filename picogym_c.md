# [PicoCTF](./picoctf.md) PicoGym Cryptography [33/50]

Cryptography is essential to many models of cyber security. Cryptography applies algorithms to shuffle the bits that represent data in such a way that only authorized users can unshuffle them to obtain the original data. 

## Contents

- [Useful References](#useful-references)
- [The Numbers (2019)](#the-numbers) ✓
- [caesar (2019)](#caesar) ✓
- [Easy1 (2019)](#easy1) ✓
- [13 (2019)](#thirteen) ✓
- [la cifra de (2019)](#la-cifra-de) ✓
- [rsa pop quiz (2019)](#rsa-pop-quiz) ✓
- [Tapping (2019)](#tapping) ✓
- [Mr-Worldwide (2019)](#mr-worldwide) ✓
- [Flags (2019)](#flags) ✓
- [waves over lambda (2019)](#waves-over-lambda) ✓
- [miniRSA (2019)](#minirsa) ✓
- [b00tl3gRSA2 (2019)](#b00tl3grsa2) ✓
- [AES-ABC (2019)](#aes-abc) ✓
- [b00tl3gRSA3 (2019)](#b00tl3grsa3) ✓
- [john_pollard (2019)](#john-pollard) ✓
- [Mod 26 (2021)](#mod-26) ✓
- [Mind your Ps and Qs (2021)](#mind-your-ps-and-qs) ✓
- [Easy Peasy (2021)](#easy-peasy) ✓
- [New Caesar (2021)](#new-caesar) ✓
- [Mini RSA (2021)](#mini-rsa) ✓
- [Dachshund Attacks (2021)](#dachshund-attacks) ✓
- [No Padding, No Problem (2021)](#no-padding-no-problem) ✓
- [Pixelated (2021)](#pixelated) ✓
- [Play Nice (2021)](#play-nice) ✓
- [Double DES (2021)](#double-des) ✓
- [Compress and Attack (2021)](#compress-and-attack) ✓
- [Scrambled: RSA (2021)](#scrambled-rsa) ✓
- [It's Not My Fault 1 (2021)](#its-not-my-fault-1) ✓
- [New Vignere (2021)](#new-vignere) ✓
- [Clouds (2021)](#clouds)
- [Spelling-Quiz (2021)](#spelling-quiz) ✓
- [XtraORdinary (2021)](#xtraordinary) ✓
- [Triple-Secure (2021)](#triple-secure) ✓
- [College-Rowing-Team (2021)](#college-rowing-team) ✓
- [Corrupt-key-1 (2021)](#corrupt-key-1)
- [Corrupt-key-2 (2021)](#corrupt-key-2)
- [basic-mod1 (2022)](#basic-mod1)
- [basic-mod2 (2022)](#basic-mod2)
- [credstuff (2022)](#credstuff)
- [morse-code (2022)](#morse-code)
- [rail-fence (2022)](#rail-fence)
- [substitution0 (2022)](#substitution0)
- [substitution1 (2022)](#substitution1)
- [substitution2 (2022)](#substitution2)
- [transposition-trial (2022)](#transposition-trial)
- [Vigenere (2022)](#vigenere)
- [Very Smooth (2022)](#very-smooth)
- [Sequences (2022)](#sequences)
- [Sum-O-Primes (2022)](#sum-o-primes)
- [NSA Backdoor (2022)](#nsa-backdoor)

---

### [Cryptography](#contents) | [PicoCTF](./picoctf.md) | [Home](./index.md)

---

## Useful References

| Link | Description |
|------|-------------|
| [privacycanada.net](https://privacycanada.net/classical-encryption/caesar-cipher/) | Caesar Cipher Overview. |
| [Caesar Cipher wiki](https://en.wikipedia.org/wiki/Caesar_cipher) | Caesar Cipher Overview. |
| [dcode.fr](https://www.dcode.fr/caesar-cipher) | Caesar Cipher decoder. |
| [boxentriq.com](https://www.boxentriq.com/code-breaking/one-time-pad) | OTP encoder/decoder. |
| [ROT13 Wiki](https://en.wikipedia.org/wiki/ROT13) | ROT13 Overview. |
| [ROT13.com](https://rot13.com/) | ROT13 Encoder/Decoder. |
| [Vigenere Cipher Wiki](https://en.wikipedia.org/wiki/Vigen%C3%A8re_cipher) | Vigenere Cipher Overview. |
| [guballa.de](https://www.guballa.de/vigenere-solver) | Vigenere Cipher solver. |
| [guballa.de](https://www.guballa.de/substitution-solver) | Substitution Cipher solver. |
| [RSA Wiki](https://simple.wikipedia.org/wiki/RSA_algorithm) | RSA Encryption Overview. |
| [asecuritysite.com](https://asecuritysite.com/encryption/rsa12_2) | RSA Decryption Tool. |
| [morsecode.world](https://morsecode.world/international/translator.html) | Morse Code Translator. |
| [gps-coordinates.net](https://www.gps-coordinates.net/) | Lat/Long Address Lookup Tool. |
| [IMSF Wiki](https://en.wikipedia.org/wiki/International_maritime_signal_flags) | Maritime Signal Flags Reference. |
| [Dan Boneh Paper](https://crypto.stanford.edu/~dabo/pubs/papers/RSA-survey.pdf) | Paper detailing vulnerabilities of RSA algorithm. |
| [Wiener's Attack Wiki](https://en.wikipedia.org/wiki/Wiener%27s_attack) | Wiener's Attack overview. |
| [Block Cipher Wiki](https://en.wikipedia.org/wiki/Block_cipher_mode_of_operation) | Block Cipher Overview. |
| [openssl.org](https://wiki.openssl.org/index.php/Command_Line_Utilities) | Linux openssl command guide. |
| [alpertron.com](https://www.alpertron.com.ar/ECM.HTM) | Integer factorisation. |

---

### [Cryptography](#contents) | [PicoCTF](./picoctf.md) | [Home](./index.md)

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

![numbers.png](./resources/picoctf/picogym/attachments/cryptography/the-numbers/the_numbers.png)

</div>

</details>

### Solutions

<details>

<summary markdown="span">Solution 1</summary>

This challenge provides the following decimal integer string:

~~~
16 9 3 15 3 20 6 { 20 8 5 14 21 13 2 5 18 19 13 1 19 15 14 }
~~~

This is a simple substitution cipher.  Each alphabetical letter has been replaced by its corresponding integer:

~~~
 A  B  C  D  E  F  G  H  I  J  K  L  M  N  O  P  Q  R  S  T  U  V  W  X  Y  Z
01 02 03 04 05 06 07 08 09 10 11 12 13 14 15 16 17 18 19 20 21 22 23 24 25 26
~~~

The numbers from the image can be replaced with their corresponding letters:

~~~
P I C O C T F { T H E N U M B E R S M A S O N }
~~~

This gives us the flag: PICOCTF{THENUMBERSMASON}

</details>

### Answer

<details>

<summary markdown="span">Flag</summary>

~~~
PICOCTF{THENUMBERSMASON}
~~~

</details>

---

### [Cryptography](#contents) | [PicoCTF](./picoctf.md) | [Home](./index.md)

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

This is a simple Caesar cipher and can be solved using an online Caesar deciphering tools such as the one available at [dcode.fr](https://www.dcode.fr/caesar-cipher).

Entering the enciphered text, the decipher returns:

~~~
crossingtherubicondjneoach
~~~

</details>

### Answer

<details>

<summary markdown="span">Flag</summary>

~~~
picoCTF{crossingtherubicondjneoach}
~~~

</details>

---

### [Cryptography](#contents) | [PicoCTF](./picoctf.md) | [Home](./index.md)

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

This is a simple problem to complete by hand.  To speed up the solution we can use an OTP decipher tool such as the one available at [boxentriq.com](https://www.boxentriq.com/code-breaking/one-time-pad).

Entering the scrambled flag and the key, we get:

~~~
CRYPTOISFUN
~~~

</details>

### Answer

<details>

<summary markdown="span">Flag</summary>

~~~
picoCTF{CRYPTOISFUN}
~~~

</details>

---

### [Cryptography](#contents) | [PicoCTF](./picoctf.md) | [Home](./index.md)

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

[ROT13](https://en.wikipedia.org/wiki/ROT13) is a simple letter substitution cipher.  We can use an online solver such as the one available at [rot13.com](https://rot13.com/) to solve this challenge.

Entering the ciphertext, the flag is returned:

~~~
picoCTF{not_too_bad_of_a_problem}
~~~

</details>

### Answer

<details>

<summary markdown="span">Flag</summary>

~~~
picoCTF{not_too_bad_of_a_problem}
~~~

</details>

---

### [Cryptography](#contents) | [PicoCTF](./picoctf.md) | [Home](./index.md)

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

Connecting using netcat:

~~~shell
$ nc jupiter.challenges.picoctf.org 5726 
~~~

We get a ciphertext return:

~~~
Encrypted message:
Ne iy nytkwpsznyg nth it mtsztcy vjzprj zfzjy rkhpibj nrkitt ltc tnnygy ysee itd tte cxjltk

Ifrosr tnj noawde uk siyyzre, yse Bnretèwp Cousex mls hjpn xjtnbjytki xatd eisjd

Iz bls lfwskqj azycihzeej yz Brftsk ip Volpnèxj ls oy hay tcimnyarqj dkxnrogpd os 1553 my Mnzvgs Mazytszf Merqlsu ny hox moup Wa inqrg ipl. Ynr. Gotgat Gltzndtg Gplrfdo 

Ltc tnj tmvqpmkseaznzn uk ehox nivmpr g ylbrj ts ltcmki my yqtdosr tnj wocjc hgqq ol fy oxitngwj arusahje fuw ln guaaxjytrd catizm tzxbkw zf vqlckx hizm ceyupcz yz tnj fpvjc hgqqpohzCZK{m311a50_0x_a1rn3x3_h1ah3x6kp60egf}

Ehk ktryy herq-ooizxetypd jjdcxnatoty ol f aordllvmlbkytc inahkw socjgex, bls sfoe gwzuti 1467 my Rjzn Hfetoxea Gqmexyt.

Tnj Gimjyèrk Htpnjc iy ysexjqoxj dosjeisjd cgqwej yse Gqmexyt Doxn ox Fwbkwei Inahkw.

Tn 1508, Ptsatsps Zwttnjxiax tnbjytki ehk xz-cgqwej ylbaql rkhea (g rltxni ol xsilypd gqahggpty) ysaz bzuri wazjc bk f nroytcgq nosuznkse ol yse Bnretèwp Cousex.

Gplrfdo’y xpcuso butvlky lpvjlrki tn 1555 gx l cuseitzltoty ol yse lncsz. Yse rthex mllbjd ol yse gqahggpty fce tth snnqtki cemzwaxqj, bay ehk fwpnfmezx lnj yse osoed qptzjcs gwp mocpd hd xegsd ol f xnkrznoh vee usrgxp, wnnnh ify bk itfljcety hizm paim noxwpsvtydkse.
~~~

A web search for la cifra de points us to the Vigenere Cipher.  We can use an online solver to break the cipher such as the one available at [guballa.de](https://www.guballa.de/vigenere-solver).  This returns:

~~~
It is interesting how in history people often receive credit for things they did not create

During the course of history, the Vigenère Cipher has been reinvented many times

It was falsely attributed to Blaise de Vigenère as it was originally described in 1553 by Giovan Battista Bellaso in his book La cifra del. Sig. Giovan Battista Bellaso 

For the implementation of this cipher a table is formed by sliding the lower half of an ordinary alphabet for an apparently random number of places with respect to the upper halfpicoCTF{b311a50_0r_v1gn3r3_c1ph3r6fe60eaa}

The first well-documented description of a polyalphabetic cipher however, was made around 1467 by Leon Battista Alberti.

The Vigenère Cipher is therefore sometimes called the Alberti Disc or Alberti Cipher.

In 1508, Johannes Trithemius invented the so-called tabula recta (a matrix of shifted alphabets) that would later be a critical component of the Vigenère Cipher.

Bellaso’s second booklet appeared in 1555 as a continuation of the first. The lower halves of the alphabets are now shifted regularly, but the alphabets and the index letters are mixed by means of a mnemonic key phrase, which can be different with each correspondent.
~~~

Within which the flag is written picoCTF{b311a50_0r_v1gn3r3_c1ph3r6fe60eaa}.

</details>

### Answer

<details>

<summary markdown="span">Flag</summary>

~~~
picoCTF{b311a50_0r_v1gn3r3_c1ph3r6fe60eaa}
~~~

</details>

---

### [Cryptography](#contents) | [PicoCTF](./picoctf.md) | [Home](./index.md)

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

Using netcat to connect to the challenge server, we are posed a series of questions regarding RSA encryption.  This can be solved in python relatively easily.

Question 1 provides p and q and requests n:

~~~py
p = 60413
q = 76753
n = p*q
~~~

Question 2 provides p and n and requests q:

~~~py
p = 54269
n = 5051846941
q = int(n/p)
~~~

Question 4 provides p and q and requests totient(n):

~~~py
q = 66347
p = 12611
totn = int((p-1)*(q-1))
~~~

Question 5 provides a plaintext message, e and n and requests the ciphertext encrypted message:

~~~py
pt = 6357294171489311547190987615544575133581967886499484091352661406414044440475205342882841236357665973431462491355089413710392273380203038793241564304774271529108729717
e = 3
n = 29129463609326322559521123136222078780585451208149138547799121083622333250646678767769126248182207478527881025116332742616201890576280859777513414460842754045651093593251726785499360828237897586278068419875517543013545369871704159718105354690802726645710699029936754265654381929650494383622583174075805797766685192325859982797796060391271817578087472948205626257717479858369754502615173773514087437504532994142632207906501079835037052797306690891600559321673928943158514646572885986881016569647357891598545880304236145548059520898133142087545369179876065657214225826997676844000054327141666320553082128424707948750331
ct = int(pt**e%n)
~~~

Question 7 provides p, q and e and requests d:

~~~py
def getModInverse(a, m):
    if math.gcd(a, m) != 1:
        return None
    u1, u2, u3 = 1, 0, a
    v1, v2, v3 = 0, 1, m

    while v3 != 0:
        q = u3 // v3
        v1, v2, v3, u1, u2, u3 = (
            u1 - q * v1), (u2 - q * v2), (u3 - q * v3), v1, v2, v3
    return u1 % m
    
q = 92092076805892533739724722602668675840671093008520241548191914215399824020372076186460768206814914423802230398410980218741906960527104568970225804374404612617736579286959865287226538692911376507934256844456333236362669879347073756238894784951597211105734179388300051579994253565459304743059533646753003894559
p = 97846775312392801037224396977012615848433199640105786119757047098757998273009741128821931277074555731813289423891389911801250326299324018557072727051765547115514791337578758859803890173153277252326496062476389498019821358465433398338364421624871010292162533041884897182597065662521825095949253625730631876637
e = 65537
n = int(p*q)
totn = (p-1)*(q-1)
d = getModInverse(e, totn)
~~~

Question 8 provides a ciphertext encrypted message, p, n and e and requests the message.  This can be efficiently calulated using an online decryption tool such as one found at [asecuritysite.com](https://asecuritysite.com/encryption/rsa12_2).

When decrypted we get the flag picoCTF{wA8_th4t$_ill3aGal..ode01e4bb}.

</details>

### Answer

<details>

<summary markdown="span">Flag</summary>

~~~
picoCTF{wA8_th4t$_ill3aGal..ode01e4bb}
~~~

</details>

---

### [Cryptography](#contents) | [PicoCTF](./picoctf.md) | [Home](./index.md)

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

Using netcat, we can connect to the program:

~~~shell
$ nc jupiter.challenges.picoctf.org 48247
~~~

This returns a string of dots and dashes:

~~~
.--. .. -.-. --- -.-. - ..-. { -- ----- .-. ... ...-- -.-. ----- -.. ...-- .---- ... ..-. ..- -. .---- ..--- -.... .---- ....- ...-- ---.. .---- ---.. .---- } 
~~~

This looks like a Morse code string. We can use an online tool to translate this into ASCII chcracters. [morsecode.world](https://morsecode.world/international/translator.html)

~~~
PICOCTF{M0RS3C0D31SFUN1261438181}
~~~

</details>

### Answer

<details>

<summary markdown="span">Flag</summary>

~~~
PICOCTF{M0RS3C0D31SFUN1261438181}
~~~

</details>

---

### [Cryptography](#contents) | [PicoCTF](./picoctf.md) | [Home](./index.md)

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

This challenge provides longitude and latitude Decimal Degree coordinates.  We can lookup the addresses for each location using online gps tool such as [gps-coordinates.net](https://www.gps-coordinates.net/).

| Coordinates              | City          | Letter |
|--------------------------|---------------|--------|
| (35.028309, 135.753082)  | Kyoto         | K      |
| (46.469391, 30.740883)   | Odessa        | O      |
| (39.758949, -84.191605)  | Dayton        | D      |
| (41.015137, 28.979530)   | Istanbul      | I      |
| (24.466667, 54.366669)   | Abu Dhabi     | A      |
| (3.140853, 101.693207)   | Kuala Lumpur  | K      |
| (9.005401, 38.763611)    | Addis Ababa   | A      |
| (-3.989038, -79.203560)  | Loja          | L      |
| (52.377956, 4.897070)    | Amsterdam     | A      |
| (41.085651, -73.858467)  | Sleepy Hollow | S      |
| (57.790001, -152.407227) | Kodiak        | K      |
| (31.205753, 29.924526)   | Alexandria    | A      |

This gives us the flag picoCTF{KODIAK_ALASKA}.

</details>

### Answer

<details>

<summary markdown="span">Flag</summary>

~~~
picoCTF{KODIAK_ALASKA}
~~~

</details>

---

### [Cryptography](#contents) | [PicoCTF](./picoctf.md) | [Home](./index.md)

---
## Flags

- Author: Danny
- 200 points

### Description

What do the flags mean?

### Hints

1. The flag is in the format PICOCTF{}

### Attachments

<details>

<summary markdown="span">flag.png</summary>

<div markdonw="1">

![flag.png](./resources/picoctf/picogym/attachments/cryptography/flags/flag.png)

</div>

</details>

### Solutions

<details>

<summary markdown="span">Solution 1</summary>

This challenge provides an image of [international maritime signal flags](https://en.wikipedia.org/wiki/International_maritime_signal_flags).

We can lookup each flag to find its corresponding alphanumeric character:

~~~
PICOCTF{F1AG5AND5TUFF}
~~~

</details>

### Answer

<details>

<summary markdown="span">Flag</summary>

~~~
PICOCTF{F1AG5AND5TUFF}
~~~

</details>

---

### [Cryptography](#contents) | [PicoCTF](./picoctf.md) | [Home](./index.md)

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

When connecting to the challenge server:

~~~shell
$ nc jupiter.challenges.picoctf.org 39894
~~~

We get the following response:

~~~shell
-------------------------------------------------------------------------------
xmqfhgre zwhw ae smnh tvgf - thwknwqxs_ae_x_muwh_vgybpg_gftvxfrsnw
-------------------------------------------------------------------------------
bwrowwq ne rzwhw oge, ge a zguw gvhwgps egap emywozwhw, rzw bmqp mt rzw ewg. bweapwe zmvpaqf mnh zwghre rmfwrzwh rzhmnfz vmqf lwhampe mt ewlghgramq, ar zgp rzw wttwxr mt ygdaqf ne rmvwhgqr mt wgxz mrzwh'e sghqegqp wuwq xmquaxramqe. rzw vgoswhrzw bwer mt mvp twvvmoezgp, bwxgnew mt zae ygqs swghe gqp ygqs uahrnwe, rzw mqvs xnezamq mq pwxd, gqp oge vsaqf mq rzw mqvs hnf. rzw gxxmnqrgqr zgp bhmnfzr mnr gvhwgps g bmc mt pmyaqmwe, gqp oge rmsaqf ghxzarwxrnhgvvs oarz rzw bmqwe. yghvmo egr xhmee-vwffwp hafzr gtr, vwgqaqf gfgaqer rzw yaiiwq-yger. zw zgp enqdwq xzwwde, g swvvmo xmylvwcamq, g erhgafzr bgxd, gq gexwrax gelwxr, gqp, oarz zae ghye phmllwp, rzw lgvye mt zgqpe mnroghpe, hwewybvwp gq apmv. rzw pahwxrmh, egraetawp rzw gqxzmh zgp fmmp zmvp, ygpw zae ogs gtr gqp egr pmoq gymqfer ne. ow wcxzgqfwp g two omhpe vgiavs. gtrwhoghpe rzwhw oge eavwqxw mq bmghp rzw sgxzr. tmh emyw hwgemq mh mrzwh ow pap qmr bwfaq rzgr fgyw mt pmyaqmwe. ow twvr ywpargrauw, gqp tar tmh qmrzaqf bnr lvgxap erghaqf. rzw pgs oge wqpaqf aq g ewhwqars mt eravv gqp wcknaearw bhavvagqxw. rzw ogrwh ezmqw lgxataxgvvs; rzw eds, oarzmnr g elwxd, oge g bwqafq ayywqears mt nqergaqwp vafzr; rzw uwhs yaer mq rzw weewc yghez oge vadw g fgnis gqp hgpagqr tgbhax, znqf thmy rzw ommpwp haewe aqvgqp, gqp phglaqf rzw vmo ezmhwe aq paglzgqmne tmvpe. mqvs rzw fvmmy rm rzw ower, bhmmpaqf muwh rzw nllwh hwgxzwe, bwxgyw ymhw emybhw wuwhs yaqnrw, ge at gqfwhwp bs rzw gllhmgxz mt rzw enq.
~~~

This is an enciphered message.  We can try to break the cipher using online tool at [guballa.de](https://www.guballa.de/substitution-solver).  This returns a message:

~~~
-------------------------------------------------------------------------------
congrats here is your flag - frequency_is_c_over_lambda_agflcgtyue
-------------------------------------------------------------------------------
between us there was, as i have already said somewhere, the bond of the sea. besides holding our hearts together through long periods of separation, it had the effect of making us tolerant of each other's yarnsand even convictions. the lawyerthe best of old fellowshad, because of his many years and many virtues, the only cushion on deck, and was lying on the only rug. the accountant had brought out already a box of dominoes, and was toying architecturally with the bones. marlow sat cross-legged right aft, leaning against the mizzen-mast. he had sunken cheeks, a yellow complexion, a straight back, an ascetic aspect, and, with his arms dropped, the palms of hands outwards, resembled an idol. the director, satisfied the anchor had good hold, made his way aft and sat down amongst us. we exchanged a few words lazily. afterwards there was silence on board the yacht. for some reason or other we did not begin that game of dominoes. we felt meditative, and fit for nothing but placid staring. the day was ending in a serenity of still and exquisite brilliance. the water shone pacifically; the sky, without a speck, was a benign immensity of unstained light; the very mist on the essex marsh was like a gauzy and radiant fabric, hung from the wooded rises inland, and draping the low shores in diaphanous folds. only the gloom to the west, brooding over the upper reaches, became more sombre every minute, as if angered by the approach of the sun.
~~~

This gives us the flag frequency_is_c_over_lambda_agflcgtyue.

</details>

### Answer

<details>

<summary markdown="span">Flag</summary>

~~~
frequency_is_c_over_lambda_agflcgtyue
~~~

</details>

---

### [Cryptography](#contents) | [PicoCTF](./picoctf.md) | [Home](./index.md)

---

## miniRSA

- Author: speeeday/Danny
- 300 points

### Description

Let's decrypt this: ciphertext? Something seems a bit small.

### Hints

1. RSA [tutorial](#https://en.wikipedia.org/wiki/RSA_(cryptosystem)).
3. How could having too small an e affect the security of this 2048 bit key?
4. Make sure you don't lose precision, the numbers are pretty big (besides the e value).

### Attachments

<details>

<summary markdown="span"> ciphertext </summary>

~~~
N: 29331922499794985782735976045591164936683059380558950386560160105740343201513369939006307531165922708949619162698623675349030430859547825708994708321803705309459438099340427770580064400911431856656901982789948285309956111848686906152664473350940486507451771223435835260168971210087470894448460745593956840586530527915802541450092946574694809584880896601317519794442862977471129319781313161842056501715040555964011899589002863730868679527184420789010551475067862907739054966183120621407246398518098981106431219207697870293412176440482900183550467375190239898455201170831410460483829448603477361305838743852756938687673
e: 3

ciphertext (c): 2205316413931134031074603746928247799030155221252519872650080519263755075355825243327515211479747536697517688468095325517209911688684309894900992899707504087647575997847717180766377832435022794675332132906451858990782325436498952049751141 
~~~

</details>

### Solutions

<details>

<summary markdown="span">Solution 1</summary>

This challenge uses the known exploit of RSA encryption when using a low private exponent.  This is detailed in full by [Dan Boneh](https://crypto.stanford.edu/~dabo/pubs/papers/RSA-survey.pdf).

We can review the RSA algorithm to understand how to exploit this in more detail.

We know:

~~~
m**e = c mod(n)
~~~

Since n is much larger than c:

~~~
m**e = c mod(n) = c
~~~

The message can be recovered by:

~~~
m = c**(1/e)
~~~

So we can retrieve the message by taking the cube root of the ciphertext.  This should be easy, however due to the size of the ciphertext integer, we can not simply calculate this using native numerical libraries.  We must use an iterative approach.  Using a very simple iteration, we can find the cube root:

~~~py
n = 29331922499794985782735976045591164936683059380558950386560160105740343201513369939006307531165922708949619162698623675349030430859547825708994708321803705309459438099340427770580064400911431856656901982789948285309956111848686906152664473350940486507451771223435835260168971210087470894448460745593956840586530527915802541450092946574694809584880896601317519794442862977471129319781313161842056501715040555964011899589002863730868679527184420789010551475067862907739054966183120621407246398518098981106431219207697870293412176440482900183550467375190239898455201170831410460483829448603477361305838743852756938687673
e = 3
ct = 2205316413931134031074603746928247799030155221252519872650080519263755075355825243327515211479747536697517688468095325517209911688684309894900992899707504087647575997847717180766377832435022794675332132906451858990782325436498952049751141 

guessmax = int(1)
while (guessmax**3 < ct): guessmax *= 10
guessmin = int(guessmax/10)
guess = int((guessmin+guessmax)/2)

while guess**3 != ct:
    if guess**3 > ct:
        guessmax = int(guess)
        guessmean = int((guessmax-guessmin)/2)
        guess = int(guessmin + guessmean)
    elif guess**3<ct:
        guessmin = int(guess)
        guessmean = int((guessmax-guessmin)/2)
        guess = int(guessmin + guessmean)

print(bytearray.fromhex(hex(guess)[2:]).decode())

~~~

The first part of this program specifies the variables for the encryption.  The algorithm then finds the order of the cube root and uses this for the initial limits for a simple iterative search.

The program returns:

~~~shell
In [1]: runfile('miniRSA.py')
picoCTF{n33d_a_lArg3r_e_d0cd6eae}
~~~

</details>


### Answer

<details>

<summary markdown="span">Flag</summary>

~~~
picoCTF{n33d_a_lArg3r_e_d0cd6eae}
~~~

</details>

---

### [Cryptography](#contents) | [PicoCTF](./picoctf.md) | [Home](./index.md)

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

We can connect to the challenge server:

~~~shell
$ nc jupiter.challenges.picoctf.org 57464 
~~~

We get the following response:

~~~
c: 5351990119264486021463998259577857389550091734808220411064077869828812176996909544383783074826646696108064448056820831412294611898158753108119448190141507706042099890106893843045866585460884966070672896816037637660536676352569715620543182957282271937741435772097855328237136757638982049772724745947605550233
n: 93123034013868694006606723954789943852610266852458894799067594150615348603292064418212629387080142285353017615980435683446631913045985007905376417762198502350230741528560878286561404585080829746766718177257420963269383093720995140541068257486692897521854354301844900303193098387225483419011018793145419683591
e: 76687217079336762676603520024413892453505288646523437940486718285986700094903225912857402810942143814036381902352321800442722803104991239706626260991895450098849184887766980715855450271648611083591538859159565182698138127318299641760540363042629704348736122997013083809394208508947068400282409515628665228193
~~~

This is likely a form of RSA encryption with the flag encrypted in the ciphertext, c.  This challenge requires an understanding of the Wiener's Attack](https://en.wikipedia.org/wiki/Wiener%27s_attack).

The public and private keys have the following relationship:

$${ed=1{\bmod {\lambda }}(N)},$$

When e is sufficiently large, it is possible to find d using Wiener's attack method where d will be significantly smaller.

We can use the Python library owiener to automate this exploit:

~~~py
import owiener

n = 93123034013868694006606723954789943852610266852458894799067594150615348603292064418212629387080142285353017615980435683446631913045985007905376417762198502350230741528560878286561404585080829746766718177257420963269383093720995140541068257486692897521854354301844900303193098387225483419011018793145419683591
e = 76687217079336762676603520024413892453505288646523437940486718285986700094903225912857402810942143814036381902352321800442722803104991239706626260991895450098849184887766980715855450271648611083591538859159565182698138127318299641760540363042629704348736122997013083809394208508947068400282409515628665228193
ct = 5351990119264486021463998259577857389550091734808220411064077869828812176996909544383783074826646696108064448056820831412294611898158753108119448190141507706042099890106893843045866585460884966070672896816037637660536676352569715620543182957282271937741435772097855328237136757638982049772724745947605550233 

d = owiener.attack(e,n)

if d is None:
    print("Failed")
else:
    print("Hacked d={}".format(d))
    
pt = (ct**d)%n

print(bytearray.fromhex(hex(pt)[2:]).decode())
~~~

This produces the private key, d and the flag:

~~~shell
In [1]: runfile('b00tl3rsa2.py')
Hacked d=65537
picoCTF{bad_1d3a5_2152720}
~~~

This gives us the flag picoCTF{bad_1d3a5_2152720}.

</details>

### Answer

<details>

<summary markdown="span">Flag</summary>

~~~
picoCTF{bad_1d3a5_2152720}
~~~

</details>

---

### [Cryptography](#contents) | [PicoCTF](./picoctf.md) | [Home](./index.md)

---

## AES-ABC

- Author: waituckw
- 400 points

### Description

AES-ECB is bad, so I rolled my own cipher block chaining mechanism - Addition Block Chaining! You can find the source here: aes-abc.py. The AES-ABC flag is body.enc.ppm

### Hints

1. You probably want to figure out what the flag looks like in ECB form...

### Attachments

[body.enc.ppm](./resources/picoctf/picogym/attachments/cryptography/aes-abc/body.enc.ppm)

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

This challenge exploits the vulnerabilities of [Block Cipher](https://en.wikipedia.org/wiki/Block_cipher_mode_of_operation) encryption.

We can adapt the given python code to generate an inversion of the encryption algorithm.  We have also fixed issues with the existing code to enable it to run in Python 3.9:

~~~py
#!/usr/bin/env python

import math

BLOCK_SIZE = 16
UMAX = int(math.pow(256, BLOCK_SIZE))


def remove_line(s):
    # returns the header line, and the rest of the file
    return s[:s.index(b'\n') + 1], s[s.index(b'\n')+1:]

def parse_header_ppm(f):
    data = f.read()

    header = b""

    for i in range(3):
        header_i, data = remove_line(data)
        header += header_i

    return header, data

def aes_abc_decrypt(ct):
    ct_blocks = [ct[int(i * BLOCK_SIZE):int((i+1) * BLOCK_SIZE)] for i in range(int(len(ct) / BLOCK_SIZE))]
    pt_blocks = [0]*len(ct_blocks)
    n_arr = []
    for i in range(0,len(ct_blocks)):
        pt_blocks[i] = int.from_bytes(ct_blocks[i],"big")
    for i in range(len(ct_blocks)-1):
        prev_blk = pt_blocks[i]
        curr_blk = pt_blocks[i+1]
        n_curr_blk = (curr_blk - prev_blk) % UMAX
        n_arr.append(n_curr_blk)
    for i in range(1,len(pt_blocks)):
        pt_blocks[i] = hex(n_arr[i-1])[2:]
        if len(pt_blocks[i])%2!=0:
            pt_blocks[i] = '0'+pt_blocks[i]
    for i in range(1,len(pt_blocks)):
        pt_blocks[i] = bytearray.fromhex(pt_blocks[i])
    pt_blocks = pt_blocks[1:]
    pt = b"".join(pt_blocks)
    return pt 

if __name__=="__main__":
    with open('body.enc.ppm', 'rb') as f:
        header, data = parse_header_ppm(f)
    data = aes_abc_decrypt(data)

    with open('flag.ppm', 'wb') as fw:
        fw.write(header)
        fw.write(data)
~~~

This produces a ppm encrypted image from which the flag picoCTF{d0Nt_r0ll_yoUr_0wN_aES} can be read.

</details>

### Answer

<details>

<summary markdown="span">Flag</summary>

~~~
picoCTF{d0Nt_r0ll_yoUr_0wN_aES}
~~~

</details>

---

### [Cryptography](#contents) | [PicoCTF](./picoctf.md) | [Home](./index.md)

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

We can connect to the challenge server and get the following response:

~~~shell
$ nc jupiter.challenges.picoctf.org 3726                               1 ⨯
c: 6354005985848295437260803658493278225170941006801001877629928065087665830073956807845851151702425409183064037321452016808063060475065513096587358859853841181646032565466406974373779332765137854857858147644515487913045195988785838680047334727698267912458811453391803236081356856092424052143871953445547555941923902509373594471295821510351978635
n: 35899252402586206174061834888616133487496959337016709417230707019606074280411566390651320977959893840094964808181140250583605808219865384962417471318050375343833857361812748594429325642360631005480747859847055801461411261673431986757745695463523535969213048708546634488544830377309773885849132311228250429219422838785232969887164904129186086699
e: 65537   
~~~

This gives us some components of the RSA encryption algorithm. We can generate a list of factors for n using the integer factor tool [alpertron.com](https://www.alpertron.com.ar/ECM.HTM).

This gives us:

~~~
n = 8750 701277 × 8894 545381 × 9119 362829 × 9203 892233 × 9296 200801 × 9491 450153 × 10104 002333 × 10767 228151 × 10770 556843 × 11066 422201 × 11410 051469 × 11498 182687 × 11740 699151 × 11961 834529 × 12227 050399 × 12347 978983 × 12989 353361 × 13298 546879 × 13550 608277 × 13687 212503 × 13732 538357 × 13997 022503 × 14071 217497 × 14345 591963 × 14722 370809 × 15600 358307 × 15860 033491 × 16270 900661 × 16652 711797 × 16695 622843 × 16836 760561 × 16982 846477 × 17164 582333 × 17173 380541 
~~~

This can be solved using a simple python script:

~~~py
ct = 6354005985848295437260803658493278225170941006801001877629928065087665830073956807845851151702425409183064037321452016808063060475065513096587358859853841181646032565466406974373779332765137854857858147644515487913045195988785838680047334727698267912458811453391803236081356856092424052143871953445547555941923902509373594471295821510351978635
n = 35899252402586206174061834888616133487496959337016709417230707019606074280411566390651320977959893840094964808181140250583605808219865384962417471318050375343833857361812748594429325642360631005480747859847055801461411261673431986757745695463523535969213048708546634488544830377309773885849132311228250429219422838785232969887164904129186086699
e = 65537 

factors = [8750701277, 8894545381, 9119362829, 
           9203892233, 9296200801, 9491450153,
           10104002333, 10767228151, 10770556843,
           11066422201, 11410051469, 11498182687,
           11740699151, 11961834529, 12227050399,
           12347978983, 12989353361, 13298546879,
           13550608277, 13687212503, 13732538357,
           13997022503, 14071217497, 14345591963,
           14722370809, 15600358307, 15860033491,
           16270900661, 16652711797, 16695622843,
           16836760561, 16982846477, 17164582333,
           17173380541]

totn = factors[0]-1
for i in range(1,len(factors)):
    totn *= (factors[i]-1)
    
d = pow(e, -1, totn)

pt = pow(ct,d,n)
print(bytearray.fromhex(hex(pt)[2:]).decode())
~~~

This gives us the flag picoCTF{too_many_fact0rs_8606199}:

~~~
In [1]: runfile('b00tl3grsa3.py')
picoCTF{too_many_fact0rs_8606199}
~~~

</details>

### Answer

<details>

<summary markdown="span">Flag</summary>

~~~
picoCTF{too_many_fact0rs_8606199}
~~~

</details>

---

### [Cryptography](#contents) | [PicoCTF](./picoctf.md) | [Home](./index.md)

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

<details>

<summary markdown="span">cert</summary>

~~~
-----BEGIN CERTIFICATE-----
MIIB6zCB1AICMDkwDQYJKoZIhvcNAQECBQAwEjEQMA4GA1UEAxMHUGljb0NURjAe
Fw0xOTA3MDgwNzIxMThaFw0xOTA2MjYxNzM0MzhaMGcxEDAOBgNVBAsTB1BpY29D
VEYxEDAOBgNVBAoTB1BpY29DVEYxEDAOBgNVBAcTB1BpY29DVEYxEDAOBgNVBAgT
B1BpY29DVEYxCzAJBgNVBAYTAlVTMRAwDgYDVQQDEwdQaWNvQ1RGMCIwDQYJKoZI
hvcNAQEBBQADEQAwDgIHEaTUUhKxfwIDAQABMA0GCSqGSIb3DQEBAgUAA4IBAQAH
al1hMsGeBb3rd/Oq+7uDguueopOvDC864hrpdGubgtjv/hrIsph7FtxM2B4rkkyA
eIV708y31HIplCLruxFdspqvfGvLsCynkYfsY70i6I/dOA6l4Qq/NdmkPDx7edqO
T/zK4jhnRafebqJucXFH8Ak+G6ASNRWhKfFZJTWj5CoyTMIutLU9lDiTXng3rDU1
BhXg04ei1jvAf0UrtpeOA6jUyeCLaKDFRbrOm35xI79r28yO8ng1UAzTRclvkORt
b8LMxw7e+vdIntBGqf7T25PLn/MycGPPvNXyIsTzvvY/MXXJHnAqpI5DlqwzbRHz
q16/S1WLvzg4PsElmv1f
-----END CERTIFICATE-----
~~~

</details>

### Solutions

<details>

<summary markdown="span">Solution 1</summary>

We can use [openssl](https://wiki.openssl.org/index.php/Command_Line_Utilities) to extract the keys from the certificate:

~~~shell
$ openssl x509 -pubkey -in cert   
~~~

This gives us the public key:

~~~
-----BEGIN PUBLIC KEY-----
MCIwDQYJKoZIhvcNAQEBBQADEQAwDgIHEaTUUhKxfwIDAQAB
-----END PUBLIC KEY-----
-----BEGIN CERTIFICATE-----
MIIB6zCB1AICMDkwDQYJKoZIhvcNAQECBQAwEjEQMA4GA1UEAxMHUGljb0NURjAe
Fw0xOTA3MDgwNzIxMThaFw0xOTA2MjYxNzM0MzhaMGcxEDAOBgNVBAsTB1BpY29D
VEYxEDAOBgNVBAoTB1BpY29DVEYxEDAOBgNVBAcTB1BpY29DVEYxEDAOBgNVBAgT
B1BpY29DVEYxCzAJBgNVBAYTAlVTMRAwDgYDVQQDEwdQaWNvQ1RGMCIwDQYJKoZI
hvcNAQEBBQADEQAwDgIHEaTUUhKxfwIDAQABMA0GCSqGSIb3DQEBAgUAA4IBAQAH
al1hMsGeBb3rd/Oq+7uDguueopOvDC864hrpdGubgtjv/hrIsph7FtxM2B4rkkyA
eIV708y31HIplCLruxFdspqvfGvLsCynkYfsY70i6I/dOA6l4Qq/NdmkPDx7edqO
T/zK4jhnRafebqJucXFH8Ak+G6ASNRWhKfFZJTWj5CoyTMIutLU9lDiTXng3rDU1
BhXg04ei1jvAf0UrtpeOA6jUyeCLaKDFRbrOm35xI79r28yO8ng1UAzTRclvkORt
b8LMxw7e+vdIntBGqf7T25PLn/MycGPPvNXyIsTzvvY/MXXJHnAqpI5DlqwzbRHz
q16/S1WLvzg4PsElmv1f
-----END CERTIFICATE-----
~~~

We can use this to print the RSA modulus (n):

~~~shell
$ openssl x509 -pubkey -noout -in cert | openssl rsa -pubin -text
RSA Public-Key: (53 bit)
Modulus: 4966306421059967 (0x11a4d45212b17f)
Exponent: 65537 (0x10001)
writing RSA key
-----BEGIN PUBLIC KEY-----
MCIwDQYJKoZIhvcNAQEBBQADEQAwDgIHEaTUUhKxfwIDAQAB
-----END PUBLIC KEY-----
~~~

The modulus is very small and can be trivially factored (e.g. using [alpertron.com](https://www.alpertron.com.ar/ECM.HTM)) to give p and q:

~~~
n = 4966306421059967
p = 67867967
q = 73176001
~~~

From these, we can identify more RSA parameters:

~~~py
import numpy as np

n = 4966306421059967
p = 67867967
q = 73176001
lam_n = np.lcm(p,q)
tot_n = (p-1)*(q-1)

print("n = {}".format(n))
print("p = {}".format(p))
print("q = {}".format(q))
print("phi(n) = {}".format(tot_n))
print("lambda(n) = {}".format(lam_n))
~~~

This produces:

~~~shell
In [1]: ('john_pollard.py')
n = 4966306421059967
p = 67867967
q = 73176001
phi(n) = 4966306280016000
lambda(n) = 4966306421059967
~~~

The flag is the p and q values, picoCTF{73176001,67867967}

</details>

### Answer

<details>

<summary markdown="span">Flag</summary>

~~~
picoCTF{73176001,67867967}
~~~

</details>

---

### [Cryptography](#contents) | [PicoCTF](./picoctf.md) | [Home](./index.md)

---

## Mod 26

- Author: Pandu
- 10 points

### Description

Cryptography can be easy, do you know what ROT13 is? cvpbPGS{arkg_gvzr_V'yy_gel_2_ebhaqf_bs_ebg13_nSkgmDJE}

### Hints

1. This can be solved online if you don't want to do it by hand!

### Solutions

<details>

<summary markdown="span">Solution 1</summary>

This can be solved online using a ROT13 decoder (https://www.boxentriq.com/code-breaking/rot13)

~~~
picoCTF{next_time_I'll_try_2_rounds_of_rot13_aFxtzQWR}
~~~

</details>

### Answer

<details>

<summary markdown="span">Flag</summary>

~~~
picoCTF{next_time_I'll_try_2_rounds_of_rot13_aFxtzQWR}
~~~

</details>

---

### [Cryptography](#contents) | [PicoCTF](./picoctf.md) | [Home](./index.md)

---

## Mind your Ps and Qs

- Author: Sara
- 20 points

### Description

In RSA, a small e value can be problematic, but what about N? Can you decrypt this? values

### Hints

1. Bits are expensive, I used only a little bit over 100 to save money

### Solutions

<details>

<summary markdown="span">Solution 1</summary>

The contents of values can be found using the strings command

~~~shell
$ strings values
c: 843044897663847841476319711639772861390329326681532977209935413827620909782846667
n: 1422450808944701344261903748621562998784243662042303391362692043823716783771691667
e: 65537
~~~

The factors and totient for n can be found using integer factorisation calculator online (https://www.alpertron.com.ar/ECM.HTM)

~~~
p = 2159947535959146091116171018558446546179 
q = 658558036833541874645521278345168572231473
euler_totient = 1422450808944701344261903748621562998783582944057933890341955406374353056752914016
~~~

The carmichael totient can be calculated as the lowest common multiple of p-1 and q-1:

~~~py
#!/usr/bin/env python3
# -*- coding: utf-8 -*-

import numpy as np

p = 2159947535959146091116171018558446546179 
q = 658558036833541874645521278345168572231473

car_t = np.lcm(p-1,q-1)
~~~

This gives the carmichael totient:

~~~
car_t = 237075134824116890710317291436927166463930490676322315056992567729058842792152336
~~~

Using the Euler totient, the decryption key can be calculated:

~~~py
import math

def getModInverse(a, m):
    if math.gcd(a, m) != 1:
        return None
    u1, u2, u3 = 1, 0, a
    v1, v2, v3 = 0, 1, m

    while v3 != 0:
        q = u3 // v3
        v1, v2, v3, u1, u2, u3 = (
            u1 - q * v1), (u2 - q * v2), (u3 - q * v3), v1, v2, v3
    return u1 % m
    
q = 658558036833541874645521278345168572231473
p = 2159947535959146091116171018558446546179
e = 65537
n = 1422450808944701344261903748621562998784243662042303391362692043823716783771691667
totn = (p-1)*(q-1)
d = getModInverse(e, totn)
~~~

~~~
d = 975120122884150896343356420256053234758228648361853546720066993334766006694511009
~~~

We now have all the encryption and decryption elements for the RSA algorithm.  The ciphertext message can be deciphered:

~~~py
ct = 843044897663847841476319711639772861390329326681532977209935413827620909782846667

pt = pow(ct,d,n)
print(bytearray.fromhex(hex(pt)[2:]).decode())
~~~

This returns the flag:

~~~
picoCTF{sma11_N_n0_g0od_00264570}
~~~

</details>

### Answer

<details>

<summary markdown="span">Flag</summary>

~~~
picoCTF{sma11_N_n0_g0od_00264570}
~~~

</details>

---

### [Cryptography](#contents) | [PicoCTF](./picoctf.md) | [Home](./index.md)

---

## Easy Peasy

- Author: MADSTACKS
- 40 points

### Description

A one-time pad is unbreakable, but can you manage to recover the flag? (Wrap with picoCTF{}) nc mercury.picoctf.net 58913 otp.py

### Hints

1. Maybe there's a way to make this a 2x pad.

### Attachments

<details>

<summary markdown="span">otp.py</summary>

~~~py
#!/usr/bin/python
# -*- coding: utf-8 -*-

import os.path

KEY_FILE = "key"
KEY_LEN = 50000
FLAG_FILE = "flag"


def startup(key_location):
    flag = open(FLAG_FILE).read()
    kf = open(KEY_FILE, "rb").read()

    start = key_location
    stop = key_location + len(flag)

    key = kf[start:stop]
    key_location = stop

    result = list(map(lambda p, k: "{:02x}".format(ord(p) ^ k), flag, key))
    print """This is the encrypted flag!{}""".format("".join(result))

    return key_location


def encrypt(key_location):
    ui = input("What data would you like to encrypt? ").rstrip()
    if len(ui) == 0 or len(ui) > KEY_LEN:
        return -1

    start = key_location
    stop = key_location + len(ui)

    kf = open(KEY_FILE, "rb").read()

    if stop >= KEY_LEN:
        stop = stop % KEY_LEN
        key = kf[start:] + kf[:stop]
    else:
        key = kf[start:stop]
    key_location = stop

    result = list(map(lambda p, k: "{:02x}".format(ord(p) ^ k), ui, key))

    print """Here ya go!{}""".format("".join(result))

    return key_location


print "******************Welcome to our OTP implementation!******************"
c = startup(0)
while c >= 0:
    c = encrypt(c)
~~~
 
</details>
 
### Solutions

<details>

<summary markdown="span">Solution 1</summary>

In Python, we can read the encrypted flag and generate an empty buffer to record the key.  Inspecting the source code, we can see each encryption key is taken from a 50,000 long key in series.  We can generate a buffer submission that exceeds this value and sets the key position to 0, the same used to encrypt the flag.  With an empty buffer of the same length as the flag, the key should be returned which can be xor-d with the encrypted flag to return the plaintext flag:
	
~~~py
import socket
import time

# Set key length based on otp.py
KEYLEN = 50000

# initialise connection
s = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
s.connect(("mercury.picoctf.net", 58913))
time.sleep(1)
# receive flag:
recvbuff = s.recv(1000)
print(recvbuff)
cflag_hex = recvbuff[99:-39].decode()
cflag_dec = int(cflag_hex,16)

print("\nencrypted flag \nc_hex = {}".format(cflag_hex))
print("\nencrypted flag \nc_dec = {}".format(cflag_dec))

# find flag length:
flaglen = int(len(cflag_hex)/2)

# set buffer message length and generate empty buffer to reset key start:
mlen = KEYLEN-flaglen
m1 = "\x00"*mlen+"\n"

# empty buffer to retrieve key for flag:
m2 = "\x00"*flaglen+"\n"

# send reset buffer:
s.send(m1.encode())
time.sleep(1)

# for large response
while True:
    buff = s.recv(1024)
    if buff.decode().find("What data would you like") >= 0:
        break

# send empty buffer to receive key:
s.send(m2.encode())
time.sleep(1)
recvbuff = s.recv(1000)
s.close()

# record key:
key_hex = recvbuff[12:-39].decode()
key_dec = int(key_hex,16)

# decipher flag:
pflag_dec = cflag_dec^key_dec

print(bytearray.fromhex(hex(pflag_dec)[2:]).decode())
~~~

This returns 35ecb423b3b43472c35cc2f41011c6d2.	

</details>

### Answer

<details>

<summary markdown="span">Flag</summary>

~~~
picoCTF{35ecb423b3b43472c35cc2f41011c6d2}
~~~

</details>

---

### [Cryptography](#contents) | [PicoCTF](./picoctf.md) | [Home](./index.md)

---

## New Caesar

- Author: MADSTACKS
- 60 points

### Description

We found a brand new type of encryption, can you break the secret code? (Wrap with picoCTF{}) lkmjkemjmkiekeijiiigljlhilihliikiliginliljimiklligljiflhiniiiniiihlhilimlhijil new_caesar.py

### Hints

1. How does the cipher work if the alphabet isn't 26 letters?
2. Even though the letters are split up, the same paradigms still apply

### Attachments

<details>

<summary markdown="span">new_caesar.py</summary>

~~~py
import string

LOWERCASE_OFFSET = ord("a")
ALPHABET = string.ascii_lowercase[:16]

def b16_encode(plain):
	enc = ""
	for c in plain:
		binary = "{0:08b}".format(ord(c))
		enc += ALPHABET[int(binary[:4], 2)]
		enc += ALPHABET[int(binary[4:], 2)]
	return enc

def shift(c, k):
	t1 = ord(c) - LOWERCASE_OFFSET
	t2 = ord(k) - LOWERCASE_OFFSET
	return ALPHABET[(t1 + t2) % len(ALPHABET)]

flag = "redacted"
key = "redacted"
assert all([k in ALPHABET for k in key])
assert len(key) == 1

b16 = b16_encode(flag)
enc = ""
for i, c in enumerate(b16):
	enc += shift(c, key[i % len(key)])
print(enc)
~~~
 
</details>
 
### Solutions

<details>

<summary markdown="span">Solution 1</summary>

We can reverse the encryption python code:
	
~~~py
import string

LOWERCASE_OFFSET = ord("a")
ALPHABET = string.ascii_lowercase[:16]

def b16_encode(plain):
	enc = ""
	for c in plain:
		binary = "{0:08b}".format(ord(c))
		enc += ALPHABET[int(binary[:4], 2)]
		enc += ALPHABET[int(binary[4:], 2)]
	return enc

def b16_decode(plain):
    dec = ""
    for i in range(int(len(plain)/2)):
        a = plain[2*i]
        b = plain[2*i+1]
        a_int = ALPHABET.index(a)
        b_int = ALPHABET.index(b)
        a_bin = "{0:04b}".format(a_int)
        b_bin = "{0:04b}".format(b_int)
        dec += chr(int(a_bin+b_bin,2))
    return dec

def shift(c, k):
	t1 = ord(c) - LOWERCASE_OFFSET
	t2 = ord(k) - LOWERCASE_OFFSET
	return ALPHABET[(t1 + t2) % len(ALPHABET)]

def unshift(c, k):
    t1 = ord(c) + LOWERCASE_OFFSET
    t2 = ord(k) + LOWERCASE_OFFSET
    return ALPHABET[(t1 - t2) % len(ALPHABET)]

def is_ascii(s):
    return len(s) == len(s.encode())

flag = "a"
key = "a"

enc = "gb"

b16 = b16_encode(flag)

encrypted = "lkmjkemjmkiekeijiiigljlhilihliikiliginliljimiklligljiflhiniiiniiihlhilimlhijil"
for i, c in enumerate(b16):
	encrypted += shift(c, key[i % len(key)])
print(enc)

for a in ALPHABET:
    b16dec = ""
    for i,c in enumerate(encrypted):
        b16dec += unshift(c, a)
    flag = b16_decode(b16dec)
    if is_ascii(flag) and " " not in flag:
        print("Flag: picoCTF{}".format(flag))
~~~

This returns the flag.

</details>

### Answer

<details>

<summary markdown="span">Flag</summary>

~~~
picoCTF{et_tu?_431db62c5618cd75f1d0b83832b67b46}
~~~

</details>

---

### [Cryptography](#contents) | [PicoCTF](./picoctf.md) | [Home](./index.md)

---
 
## Mini RSA

- Author: SARA
- 70 points

### Description

What happens if you have a small exponent? There is a twist though, we padded the plaintext so that (M ** e) is just barely larger than N. Let's decrypt this: ciphertext

### Hints

1. RSA [tutorial](#https://en.wikipedia.org/wiki/RSA_(cryptosystem))
2. How could having too small of an e affect the security of this key?
3. Make sure you don't lose precision, the numbers are pretty big (besides the e value)
4. You shouldn't have to make too many guesses
5. pico is in the flag, but not at the beginning

### Attachments

<details>

<summary markdown="span">ciphertext</summary>

~~~
N: 1615765684321463054078226051959887884233678317734892901740763321135213636796075462401950274602405095138589898087428337758445013281488966866073355710771864671726991918706558071231266976427184673800225254531695928541272546385146495736420261815693810544589811104967829354461491178200126099661909654163542661541699404839644035177445092988952614918424317082380174383819025585076206641993479326576180793544321194357018916215113009742654408597083724508169216182008449693917227497813165444372201517541788989925461711067825681947947471001390843774746442699739386923285801022685451221261010798837646928092277556198145662924691803032880040492762442561497760689933601781401617086600593482127465655390841361154025890679757514060456103104199255917164678161972735858939464790960448345988941481499050248673128656508055285037090026439683847266536283160142071643015434813473463469733112182328678706702116054036618277506997666534567846763938692335069955755244438415377933440029498378955355877502743215305768814857864433151287
e: 3

ciphertext (c): 1220012318588871886132524757898884422174534558055593713309088304910273991073554732659977133980685370899257850121970812405700793710546674062154237544840177616746805668666317481140872605653768484867292138139949076102907399831998827567645230986345455915692863094364797526497302082734955903755050638155202890599808154558034707767377524500302754459807923331810585173010977657982069888996945830789092526932364658459034145456505057469113036134559745659079236466119515004648189278227777550415021840140147319061470183840214034417917161940379351273394212022847037696265532968684592354941479799473941357715953204487236888712642494877545201005807776354854390358015733495331101077851132489983665939643188064986446883595239842621440918456201787168234988410659153219277329426230136499096098072681939491840913961290536851217677043565743644469862992310241563891464225935615676242084658617931225618537173689559419607688905143683603007487996422560430269750305079282818976557285786253025774883158125978164878245223052992502106
~~~
 
</details>
 
### Solutions

<details>

<summary markdown="span">Solution 1</summary>

With a small e, the plaintext message can be recovered using a simple iteration: m = (c+i*N)^1/e.  This can be solved in python:
	
~~~py
import gmpy2 as gp

N= 1615765684321463054078226051959887884233678317734892901740763321135213636796075462401950274602405095138589898087428337758445013281488966866073355710771864671726991918706558071231266976427184673800225254531695928541272546385146495736420261815693810544589811104967829354461491178200126099661909654163542661541699404839644035177445092988952614918424317082380174383819025585076206641993479326576180793544321194357018916215113009742654408597083724508169216182008449693917227497813165444372201517541788989925461711067825681947947471001390843774746442699739386923285801022685451221261010798837646928092277556198145662924691803032880040492762442561497760689933601781401617086600593482127465655390841361154025890679757514060456103104199255917164678161972735858939464790960448345988941481499050248673128656508055285037090026439683847266536283160142071643015434813473463469733112182328678706702116054036618277506997666534567846763938692335069955755244438415377933440029498378955355877502743215305768814857864433151287
e= 3

c = 1220012318588871886132524757898884422174534558055593713309088304910273991073554732659977133980685370899257850121970812405700793710546674062154237544840177616746805668666317481140872605653768484867292138139949076102907399831998827567645230986345455915692863094364797526497302082734955903755050638155202890599808154558034707767377524500302754459807923331810585173010977657982069888996945830789092526932364658459034145456505057469113036134559745659079236466119515004648189278227777550415021840140147319061470183840214034417917161940379351273394212022847037696265532968684592354941479799473941357715953204487236888712642494877545201005807776354854390358015733495331101077851132489983665939643188064986446883595239842621440918456201787168234988410659153219277329426230136499096098072681939491840913961290536851217677043565743644469862992310241563891464225935615676242084658617931225618537173689559419607688905143683603007487996422560430269750305079282818976557285786253025774883158125978164878245223052992502106

for i in range(10000):
    m, root = gp.iroot(c+i*N,e)
    if root:
        print(bytearray.fromhex(hex(m)[2:]).decode())
        break
~~~

</details>

### Answer

<details>

<summary markdown="span">Flag</summary>

~~~
picoCTF{e_sh0u1d_b3_lArg3r_aef7377d}
~~~

</details>

---

### [Cryptography](#contents) | [PicoCTF](./picoctf.md) | [Home](./index.md)

---

## Dachshund Attacks

- Author: SARA
- 80 points

### Description

What if d is too small? Connect with nc mercury.picoctf.net 62786.

### Hints

1. What do you think about my pet? [dachshund.jpg](https://mercury.picoctf.net/static/c459cf0a2492fe5cc92d536a4e5b2293/dachshund.jpg)

### Attachments

None.
 
### Solutions

<details>

<summary markdown="span">Solution 1</summary>

Connecting to the challenge server, we get the following response:

~~~bash
$ nc mercury.picoctf.net 62786
Welcome to my RSA challenge!
e: 11837488215721744069772222345144402152404223679287539314178965839209604720837298973752527734448240650188901153352621505252808362581923167279970597541333924808324057073578538596216402380632161383131578005918161883422376292563622321863270212026477624494910048391769590007627866882345829334562367361915869731979
n: 122771138486469957400941324727990830080092678014948516950951572316770505352515815682155457034994546533341827642884963423771910055154560942798532931347020499103967608469288985263410230425958376575250958527772829641946831426878162530602268209668706321488097870833500950358173441586682016871709863771927776780383
c: 56513358621462857330291123787527774412184622936417370082596507998651614074391773321448976537220395441479671799148659358198162070662201800080102854509952739460730968931932080583379776856604311854915339966267677769791455835565063461259117374652564385695643358865764199949492074681957943417708327389271803995620
~~~

The challenge suggests the decryption key, d, is small. The hint points to a Dachshund (or wiener dog) - this suggests the wiener exploit may work. This can be implemented very simply in python using the owiener library:
	
~~~py
import owiener
import gmpy2 as gp

e = 11837488215721744069772222345144402152404223679287539314178965839209604720837298973752527734448240650188901153352621505252808362581923167279970597541333924808324057073578538596216402380632161383131578005918161883422376292563622321863270212026477624494910048391769590007627866882345829334562367361915869731979
n = 122771138486469957400941324727990830080092678014948516950951572316770505352515815682155457034994546533341827642884963423771910055154560942798532931347020499103967608469288985263410230425958376575250958527772829641946831426878162530602268209668706321488097870833500950358173441586682016871709863771927776780383
c = 56513358621462857330291123787527774412184622936417370082596507998651614074391773321448976537220395441479671799148659358198162070662201800080102854509952739460730968931932080583379776856604311854915339966267677769791455835565063461259117374652564385695643358865764199949492074681957943417708327389271803995620

d = owiener.attack(e,n)

if d is None:
    print("Failed")
else:
    print("d={}".format(d))

m = gp.powmod(c,d,n)
print(bytearray.fromhex(format(m,'x')).decode())
~~~
	
</details>

### Answer

<details>

<summary markdown="span">Flag</summary>

~~~
picoCTF{proving_wiener_5086186}
~~~

</details>

---

### [Cryptography](#contents) | [PicoCTF](./picoctf.md) | [Home](./index.md)

---

## No Padding No Problem

- Author: SARA
- 90 points

### Description

Oracles can be your best friend, they will decrypt anything, except the flag's ciphertext. How will you break it? Connect with nc mercury.picoctf.net 2671.

### Hints

1. What can you do with a different pair of ciphertext and plaintext? What if it is not so different after all...

### Attachments

None.
 
### Solutions

<details>

<summary markdown="span">Solution 1</summary>

Connecting to the challenge server, we get the following response:

~~~bash
$ nc mercury.picoctf.net 2671
Welcome to the Padding Oracle Challenge
This oracle will take anything you give it and decrypt using RSA. It will not accept the ciphertext with the secret message... Good Luck!


n: 99345616404160490581924979307217066304514899976392862432192189435489707011150641968260746491133766160143208534578405024325415750584779502596181917376115542179416018462368341791998700722878732164984548531802239356053300645320494212879410772889712714079244827669972559526542309563525101021029142183754472726969
e: 65537
ciphertext: 42059054525445512344438316796946837936571047540289800758221524321039138442057165001570454931163368770427152975820819525787276768725630752904270411977284309302007528246321343918872064638118021772231426448575387859094853698608669832859926530020028404969343380031068185811013922571183738200553831606632689991632


Give me ciphertext to decrypt:
~~~

These encryption parameters change for each connection. This can be implemented in Python to extract the key values:

~~~py
import socket
import time

s = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
s.connect(("mercury.picoctf.net", 2671))
time.sleep(5)
recvstr = s.recv(1000).decode()
nloc = recvstr.find("n:")
eloc = recvstr.find("e:")
cloc = recvstr.find("ciphertext:")
nstr = recvstr[nloc+3:eloc-1]
estr = recvstr[eloc+3:cloc-1]
cstr = recvstr[cloc+12:-34]
n = int(nstr)
e = int(estr)
c = int(cstr)
~~~

This implementation of RSA (unpadded) is homomorphic, we can therefore use an encrypted constant to decrypt the ciphertext:

~~~py
K = gp.powmod(2,e,n)
c2 = int(c*K)
~~~

decrypting the response and dividing by our constant will provide the plaintext message:
	
~~~py
s.send(str(c2).encode())
s.send("\n".encode())
time.sleep(5)
resp = s.recv(1000).decode()
s.close()

m2loc = resp.find("go:")
m2str = resp[m2loc+4:-32]
m2 = int(m2str)

m = m2//2

print(bytearray.fromhex(hex(m)[2:]).decode())
~~~

The entire python code is:

~~~py
import gmpy2 as gp
import socket
import time

s = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
s.connect(("mercury.picoctf.net", 2671))
time.sleep(5)
recvstr = s.recv(1000).decode()
nloc = recvstr.find("n:")
eloc = recvstr.find("e:")
cloc = recvstr.find("ciphertext:")
nstr = recvstr[nloc+3:eloc-1]
estr = recvstr[eloc+3:cloc-1]
cstr = recvstr[cloc+12:-34]
n = int(nstr)
e = int(estr)
c = int(cstr)

K = gp.powmod(2,e,n)
c2 = int(c*K)

s.send(str(c2).encode())
s.send("\n".encode())
time.sleep(5)
resp = s.recv(1000).decode()
s.close()

m2loc = resp.find("go:")
m2str = resp[m2loc+4:-32]
m2 = int(m2str)

m = m2//2

print(bytearray.fromhex(hex(m)[2:]).decode())
~~~
	
</details>

### Answer

<details>

<summary markdown="span">Flag</summary>

~~~
picoCTF{m4yb3_Th0se_m3s54g3s_4r3_difurrent_5814368}
~~~

</details>

---

### [Cryptography](#contents) | [PicoCTF](./picoctf.md) | [Home](./index.md)

---
	
## Pixelated

- Author: SARA
- 100 points

### Description

I have these 2 images, can you make a flag out of them? scrambled1.png scrambled2.png

### Hints

1. [https://en.wikipedia.org/wiki/Visual_cryptography](https://en.wikipedia.org/wiki/Visual_cryptography)
2. Think of different ways you can "stack" images

### Attachments

1. scrambled1.png
2. scrambled2.png
 
### Solutions

<details>

<summary markdown="span">Solution 1</summary>

Reading the wikipedia article for visual cryptography, you can see that the manipulation of pixels from 2 images can be used to decipher a secret.  From this challenge, the two scrambled images can be imported and combined in Python:
	
~~~py
from PIL import Image as im
import numpy as np

scr1 = im.open("scrambled1.png")
scr2 = im.open("scrambled2.png")

scr1_arr = np.array(scr1)
scr2_arr = np.array(scr2)

comb_arr = scr1_arr + scr2_arr

out = im.fromarray(comb_arr).save("flag.png")
~~~

This produces an image with the flag.
	
</details>

### Answer

<details>

<summary markdown="span">Flag</summary>

~~~
picoCTF{7188864c}
~~~

</details>

---

### [Cryptography](#contents) | [PicoCTF](./picoctf.md) | [Home](./index.md)

---

## Play Nice

- Author: madStacks
- 110 points

### Description

Not all ancient ciphers were so bad... The flag is not in standard format. nc mercury.picoctf.net 19354 playfair.py

### Hints

None.

### Attachments

1. [playfair.py](https://mercury.picoctf.net/static/9ea1604c8767cd6545948ad54670c2bf/playfair.py)
 
### Solutions

<details>

<summary markdown="span">Solution 1</summary>

The source code provides the enciphering algorithm used for the message, this algorithm finds each message letter in an alphabet matrix and substitutes the value based on the index:
	
~~~py
#!/usr/bin/python3 -u
import signal

SQUARE_SIZE = 6


def generate_square(alphabet):
	assert len(alphabet) == pow(SQUARE_SIZE, 2)
	matrix = []
	for i, letter in enumerate(alphabet):
		if i % SQUARE_SIZE == 0:
			row = []
		row.append(letter)
		if i % SQUARE_SIZE == (SQUARE_SIZE - 1):
			matrix.append(row)
	return matrix

def get_index(letter, matrix):
	for row in range(SQUARE_SIZE):
		for col in range(SQUARE_SIZE):
			if matrix[row][col] == letter:
				return (row, col)
	print("letter not found in matrix.")
	exit()

def encrypt_pair(pair, matrix):
	p1 = get_index(pair[0], matrix)
	p2 = get_index(pair[1], matrix)

	if p1[0] == p2[0]:
		return matrix[p1[0]][(p1[1] + 1)  % SQUARE_SIZE] + matrix[p2[0]][(p2[1] + 1)  % SQUARE_SIZE]
	elif p1[1] == p2[1]:
		return matrix[(p1[0] + 1)  % SQUARE_SIZE][p1[1]] + matrix[(p2[0] + 1)  % SQUARE_SIZE][p2[1]]
	else:
		return matrix[p1[0]][p2[1]] + matrix[p2[0]][p1[1]]

def encrypt_string(s, matrix):
	result = ""
	if len(s) % 2 == 0:
		plain = s
	else:
		plain = s + "n5vgru7ehz1klja8s9340m2wcxbd6pqfitoy"[0]
	for i in range(0, len(plain), 2):
		result += encrypt_pair(plain[i:i + 2], matrix)
	return result

alphabet = open("key").read().rstrip()
m = generate_square(alphabet)
msg = open("msg").read().rstrip()
enc_msg = encrypt_string(msg, m)
print("Here is the alphabet: {}\nHere is the encrypted message: {}".format(alphabet, enc_msg))
signal.alarm(18)
resp = input("What is the plaintext message? ").rstrip()
if resp and resp == msg:
	print("Congratulations! Here's the flag: {}".format(open("flag").read()))

# https://en.wikipedia.org/wiki/Playfair_cipher
~~~

Connecting to the challenge host, we get the following:

~~~bash
$ nc mercury.picoctf.net 19354
Here is the alphabet: n5vgru7ehz1klja8s9340m2wcxbd6pqfitoy
Here is the encrypted message: hnjm2e4t51v16gsg104i4oi9wmrqli
What is the plaintext message?
~~~

We can simply reverse the python algorithm to generate the plaintext message:

~~~py
SQUARE_SIZE = 6

def generate_square(alphabet):
	assert len(alphabet) == pow(SQUARE_SIZE, 2)
	matrix = []
	for i, letter in enumerate(alphabet):
		if i % SQUARE_SIZE == 0:
			row = []
		row.append(letter)
		if i % SQUARE_SIZE == (SQUARE_SIZE - 1):
			matrix.append(row)
	return matrix

def get_index(letter, matrix):
	for row in range(SQUARE_SIZE):
		for col in range(SQUARE_SIZE):
			if matrix[row][col] == letter:
				return (row, col)
	print("letter not found in matrix.")
	exit()
    
def decrypt_pair(pair, matrix):
	p1 = get_index(pair[0], matrix)
	p2 = get_index(pair[1], matrix)

	if p1[0] == p2[0]:
		return matrix[p1[0]][(p1[1] - 1)  % SQUARE_SIZE] + matrix[p2[0]][(p2[1] - 1)  % SQUARE_SIZE]
	elif p1[1] == p2[1]:
		return matrix[(p1[0] - 1)  % SQUARE_SIZE][p1[1]] + matrix[(p2[0] - 1)  % SQUARE_SIZE][p2[1]]
	else:
		return matrix[p1[0]][p2[1]] + matrix[p2[0]][p1[1]]

def decrypt_string(s, matrix):
	result = ""
	for i in range(0, len(s), 2):
		result += decrypt_pair(s[i:i + 2], matrix)
	return result

alphabet = "n5vgru7ehz1klja8s9340m2wcxbd6pqfitoy"
c_message = "hnjm2e4t51v16gsg104i4oi9wmrqli"
m = generate_square(alphabet)

dec_msg = decrypt_string(c_message,m)
print(dec_msg)
~~~

This returns 7v8441mfrerhdr8rh20f2fya20noaq which can be submitted to the challenge host:

~~~bash
$ nc mercury.picoctf.net 19354
Here is the alphabet: n5vgru7ehz1klja8s9340m2wcxbd6pqfitoy
Here is the encrypted message: hnjm2e4t51v16gsg104i4oi9wmrqli
What is the plaintext message? 7v8441mfrerhdr8rh20f2fya20noaq
Congratulations! Here's the flag: dbc8bf9bae7152d35d3c200c46a0fa30
~~~

This can be directly submitted as the flag.

</details>

### Answer

<details>

<summary markdown="span">Flag</summary>

~~~
dbc8bf9bae7152d35d3c200c46a0fa30
~~~

</details>

---

### [Cryptography](#contents) | [PicoCTF](./picoctf.md) | [Home](./index.md)

---

## Double DES

- Author: madStacks
- 120 points

### Description

I wanted an encryption service that's more secure than regular DES, but not as slow as 3DES... The flag is not in standard format. nc mercury.picoctf.net 29980 ddes.py
	
### Hints

1. How large is the keyspace?

### Attachments

1. [ddes.py](https://mercury.picoctf.net/static/234355303e00119853580a394796e0d4/ddes.py)
 
### Solutions

<details>

<summary markdown="span">Solution 1</summary>

Reviewing the python code, we can see the program opens the flag, pads it to a fixed length of 8 Bytes and encrypts it twice using DEC mode ECB:
	
~~~py
#!/usr/bin/python3 -u
from Crypto.Cipher import DES
import binascii
import itertools
import random
import string


def pad(msg):
    block_len = 8
    over = len(msg) % block_len
    pad = block_len - over
    return (msg + " " * pad).encode()

def generate_key():
    return pad("".join(random.choice(string.digits) for _ in range(6)))


FLAG = open("flag").read().rstrip()
KEY1 = generate_key()
KEY2 = generate_key()


def get_input():
    try:
        res = binascii.unhexlify(input("What data would you like to encrypt? ").rstrip()).decode()
    except:
        res = None
    return res

def double_encrypt(m):
    msg = pad(m)

    cipher1 = DES.new(KEY1, DES.MODE_ECB)
    enc_msg = cipher1.encrypt(msg)
    cipher2 = DES.new(KEY2, DES.MODE_ECB)
    return binascii.hexlify(cipher2.encrypt(enc_msg)).decode()


print("Here is the flag:")
print(double_encrypt(FLAG))

while True:
    inputs = get_input()
    if inputs:
        print(double_encrypt(inputs))
    else:
        print("Invalid input.")
~~~

We can start our python solution by retrieving the CT flag and encrypting a test string:

~~~py
import socket
import time

URL = "mercury.picoctf.net"
PORT = 29980
PT_TEST = "123456"

def load_flag():
    global CT_FLAG, PT_TEST, CT_TEST
    s = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
    s.connect((URL,PORT))
    time.sleep(1)
    recvbuff = s.recv(1000).decode()
    CT_FLAG = recvbuff[18:-38]
    print("Encrypted Flag: \n{}\n".format(CT_FLAG))
    s.send((PT_TEST+"\n").encode())
    time.sleep(1)
    recvbuff = s.recv(1000).decode()
    s.close()
    CT_TEST = recvbuff[:-38]
    print("Test string: \n{}\n".format(PT_TEST))
    print("Encrypted Test string: \n{}\n".format(CT_TEST))
    
    
if __name__ == "__main__":
    load_flag()
~~~
	
This provides a PT and CT test and the CT flag:

~~~
Encrypted Flag: 
7ab0bbc231e8335e773294578e4d49261ddfbf5d71775c03e3da32aef2e3fdb84b9026af70b4f02d

Test string: 
123456

Encrypted Test string: 
ad611a15c759418a
~~~

The encryption script generates a random key of length up to 6 and pads it with 2 spaces:

~~~py
def pad(msg):
    block_len = 8
    over = len(msg) % block_len
    pad = block_len - over
    return (msg + " " * pad).encode()

def generate_key():
    return pad("".join(random.choice(string.digits) for _ in range(6)))
~~~

We can generate a KEYLIST of all possible keys:

~~~py
def pad(msg):
    block_len = 8
    over = len(msg) % block_len
    pad = block_len - over
    return (msg + " " * pad).encode()

def key_dict():
    global KEYLIST
    KEYLIST = []
    for i in range(1000000):
        keystr = f"{i:06}"
        KEYLIST.append(pad(keystr))

if __name__ == "__main__":
    key_dict()
~~~
	
Using our test string, we can find both encryption keys using the keylist.  The plaintext string will be encrypted with all keys in keylist and the ciphertext string will be decoded by iterating through the keylist until a matching message is found:
	
~~~py
def find_keys(pt_string,ct_string):
    key_dict()
    msg = pad(binascii.unhexlify(pt_string).decode())
    ct_array = []
    print("Generating CT strings:")
    for i in range(len(KEYLIST)):
        cipher = DES.new(KEYLIST[i], DES.MODE_ECB)
        enc_msg = cipher.encrypt(msg)
        ct_array.append(enc_msg)
    print("All CT strings generated.\n")
    enc_msg = binascii.unhexlify(ct_string)
    print("Generating PT strings:")
    for i in range(len(KEYLIST)):
        cipher = DES.new(KEYLIST[i], DES.MODE_ECB)
        pt_msg = cipher.decrypt(enc_msg)
        if pt_msg in ct_array:
            print("Keys found!")
            key2 = KEYLIST[i]
            key1 = KEYLIST[ct_array.index(pt_msg)]
            break
    print("KEY1 = {}\n".format(key1))
    print("KEY2 = {}\n".format(key2))
    return key1, key2
~~~

Once both keys are found, we can decrypt the flag using these keys:

~~~py
def double_decrypt(key1, key2, ct_string):
    cipher1 = DES.new(key1,DES.MODE_ECB)
    cipher2 = DES.new(key2,DES.MODE_ECB)
    enc_msg = binascii.unhexlify(ct_string)
    pt_buff = cipher2.decrypt(enc_msg)
    pt_msg = cipher1.decrypt(pt_buff)
    return pt_msg.decode()
~~~

Our complete python solution:
	
~~~py
#!/usr/bin/env python3
# -*- coding: utf-8 -*-

import socket
import time
from Crypto.Cipher import DES
import binascii

URL = "mercury.picoctf.net"
PORT = 29980
PT_TEST = "123456"

def load_flag():
    global CT_FLAG, PT_TEST, CT_TEST
    s = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
    s.connect((URL,PORT))
    time.sleep(1)
    recvbuff = s.recv(1000).decode()
    CT_FLAG = recvbuff[18:-38]
    print("Encrypted Flag: \n{}\n".format(CT_FLAG))
    s.send((PT_TEST+"\n").encode())
    time.sleep(1)
    recvbuff = s.recv(1000).decode()
    s.close()
    CT_TEST = recvbuff[:-38]
    print("Test string: \n{}\n".format(PT_TEST))
    print("Encrypted Test string: \n{}\n".format(CT_TEST))

def pad(msg):
    block_len = 8
    over = len(msg) % block_len
    pad = block_len - over
    return (msg + " " * pad).encode()

def key_dict():
    global KEYLIST
    KEYLIST = []
    for i in range(1000000):
        keystr = f"{i:06}"
        KEYLIST.append(pad(keystr))
    
def find_keys(pt_string,ct_string):
    key_dict()
    msg = pad(binascii.unhexlify(pt_string).decode())
    ct_array = []
    print("Generating CT strings:")
    for i in range(len(KEYLIST)):
        cipher = DES.new(KEYLIST[i], DES.MODE_ECB)
        enc_msg = cipher.encrypt(msg)
        ct_array.append(enc_msg)
    print("All CT strings generated.\n")
    enc_msg = binascii.unhexlify(ct_string)
    print("Generating PT strings:")
    for i in range(len(KEYLIST)):
        cipher = DES.new(KEYLIST[i], DES.MODE_ECB)
        pt_msg = cipher.decrypt(enc_msg)
        if pt_msg in ct_array:
            print("Keys found!")
            key2 = KEYLIST[i]
            key1 = KEYLIST[ct_array.index(pt_msg)]
            break
    print("KEY1 = {}\n".format(key1))
    print("KEY2 = {}\n".format(key2))
    return key1, key2

def double_decrypt(key1, key2, ct_string):
    cipher1 = DES.new(key1,DES.MODE_ECB)
    cipher2 = DES.new(key2,DES.MODE_ECB)
    enc_msg = binascii.unhexlify(ct_string)
    pt_buff = cipher2.decrypt(enc_msg)
    pt_msg = cipher1.decrypt(pt_buff)
    return pt_msg.decode()

if __name__ == "__main__":
    load_flag()
    k1, k2 = find_keys(PT_TEST, CT_TEST)
    flag = double_decrypt(k1,k2,CT_FLAG)
    print("Flag = {}".format(flag))
~~~

This provides the following output:

~~~
Encrypted Flag: 
5ff2c69ec4167ca5de8d06944c66c60f229496a7184c0db70a75829a5f0b10406ee2b45bf0089215

Test string: 
123456

Encrypted Test string: 
4488dffb358d8a31

Generating CT strings:
All CT strings generated.

Generating PT strings:
Keys found!
KEY1 = b'240662  '

KEY2 = b'404262  '

Flag = 45d6631b0c4d52b801a0fa7f6d3bda3c
~~~
	
</details>

### Answer

<details>

<summary markdown="span">Flag</summary>

~~~
45d6631b0c4d52b801a0fa7f6d3bda3c
~~~

</details>

---

### [Cryptography](#contents) | [PicoCTF](./picoctf.md) | [Home](./index.md)

---
	
## Compress and Attack

- Author: Jake Beley
- 130 points

### Description

Your goal is to find the flag. compress_and_attack.py nc mercury.picoctf.net 29858

### Hints

1. The flag only contains uppercase and lowercase letters, underscores, and braces (curly brackets)

### Attachments

1. [compress_and_attack.py](https://mercury.picoctf.net/static/04d2020011483caf8c9d8fb9fa54d4f5/compress_and_attack.py)
 
### Solutions

<details>

<summary markdown="span">Solution 1</summary>

We are given the file [compress_and_attack.py](https://mercury.picoctf.net/static/04d2020011483caf8c9d8fb9fa54d4f5/compress_and_attack.py):
	
~~~py
#!/usr/bin/python3 -u

import zlib
from random import randint
import os
from Crypto.Cipher import Salsa20

flag = open("./flag").read()


def compress(text):
    return zlib.compress(bytes(text.encode("utf-8")))

def encrypt(plaintext):
    secret = os.urandom(32)
    cipher = Salsa20.new(key=secret)
    return cipher.nonce + cipher.encrypt(plaintext)

def main():
    while True:
        usr_input = input("Enter your text to be encrypted: ")
        compressed_text = compress(flag + usr_input)
        encrypted = encrypt(compressed_text)
        
        nonce = encrypted[:8]
        encrypted_text =  encrypted[8:]
        print(nonce)
        print(encrypted_text)
        print(len(encrypted_text))

if __name__ == '__main__':
    main()
~~~

This script takes a user text string and appends it to the flag.  This is compressed using zlib.compress and encrypted using Salsa20 with a random 32-byte unsigned integer key.  The code then assigns the first 8 characters to the variable nonce and the remaining characters to the variable encrypted_text which are both printed.
	
We can retrieve the nonce, encrypted text and encrypted text length in Python; note: since the response is a string of bytes, we need to correct for hex and ascii characters:

~~~py
import socket
import time
import binascii

URL = "mercury.picoctf.net"
PORT = 29858
PT_TEST = "aaaaaaaaaaaaaaaaaaaa"

def str2bytes(messy_string):
    output_string = ""
    messy_array = messy_string.split("\\x")
    for i in range(len(messy_array)):
        if len(messy_array[i])>=2:
            hexletters = messy_array[i][0:2]
            output_string += hexletters
            if len(messy_array[i])>=3:
                letters = messy_array[i][2:]
                hexletters = binascii.hexlify(letters.encode()).decode()
                output_string += hexletters
        else:
            letters = messy_array[i]
            hexletters = binascii.hexlify(letters.encode()).decode()
            output_string += hexletters
    output_bytes = binascii.unhexlify(output_string)
    return output_bytes

def load_flag():
    global CT_MSG
    s = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
    s.connect((URL,PORT))
    time.sleep(1)
    recvbuff = s.recv(1000).decode()
    s.send((PT_TEST+"\n").encode())
    time.sleep(1)
    recvbuff = s.recv(1000).decode()
    print(recvbuff+"\n")
    recvbuff = recvbuff.splitlines()
    noncebuff = recvbuff[0][2:-1]
    nonce = str2bytes(noncebuff)
    enc_text_buff = recvbuff[1][2:-1]
    enc_text = str2bytes(enc_text_buff)
    enc_text_len = int(recvbuff[2])
    s.close()
    return nonce, enc_text, enc_text_len

if __name__ == "__main__":
    a, b, c = load_flag()
    print("nonce = {}\n".format(a))
    print("enc_text = {}\n".format(b))
    print("enc_text_length = {}".format(c))
~~~

This provides the following output:

~~~
b'\xe02\x91\x95\x0b\x0c\xd9\x91'
b"\xd7!I\xd8s\x05Wx\xc6\x95E\xf0?\x98kp\xe1'\xe1\xefq`\xe1\xb4\xf2(\xb2\xb5Ttmx\xa310\x8fW\xaaS\xda_\xb5|0\x07~\x82"
47
Enter your text to be encrypted: 

nonce = b'\xe02\x91\x95\x0b\x0c\xd9\x91'

enc_text = b"\xd7!I\xd8s\x05Wx\xc6\x95E\xf0?\x98kp\xe1'\xe1\xefq`\xe1\xb4\xf2(\xb2\xb5Ttmx\xa310\x8fW\xaaS\xda_\xb5|0\x07~\x82"

enc_text_length = 47
~~~

The [Salsa20](https://en.wikipedia.org/wiki/Salsa20) stream cipher enables us to determine the approximate length of the plaintext input from the cipher text output. The use of the zlib compression enables us to attempt to find repeatable characters that will not increase the length of the ciphertext response. 

We can test this with netcat:

~~~shell
$ nc mercury.picoctf.net 29858
Enter your text to be encrypted: picoCTFa
b'\xf2\xfe\x8e\x18\xde\xa8K\xbc'
b"o\n\xbb\x0c\x81\xed\xd4\xe9\xfa\xaf'e\xccs\xbd\xed\xf2\xc1BmR\x1f\xde\xb2R0W\xcc$\x99\x83\x8e\x90k\xe9\x13\x19\xbd\xf8I\xc1!\xbcgf\xa7\xa8\x92\x81"
49
Enter your text to be encrypted: picoCTFb
b'\x83M\x0fz\xc3gcP'
b'\r\x89\xfe\x07E\xa6\t\xa8\xc7\xfb\x8f)\xb4\xa3\x024\x8f\x93\x05\x01\xaf\xec\xa0W\xdaf\x1e\x98Y\xaa\xa4\xf8\x8c\xd6\xe3\t\x16:z\x93\x96eb\x83\xb5O\xdb\xf7q'
49
Enter your text to be encrypted: picoCTF{
b'\xf4\xdc\xcf~\x9a\xa3\x97\x13'
b'\xa6\xed\xd4C\xbfS7a\'\xe9\xd5\xd2\xb6\x16\x12\x8d\x1f\xef\xe2\xe1\x85=\xca\xfa\xd20\x97\x1e\xa3\xdb\xc7>\xc4&\xdaE\xbe3K\x89\xc7\x96ec\xcff"K'
48
~~~

With the correct flag characters, the encrypted response will not increase in length.  Using python, we can write a code that iterates through the allowed characters and appends correct characters to a flag string:

~~~py
import socket
import time

URL = "mercury.picoctf.net"
PORT = 29858
FLAG = "picoCTF{"
alphabet = "abcdefghijklmnopqrstuvwxyzABCDEFGHIJKLMNOPQRSTUVWXYZ_{}"

def reconnect(s):
    if(s):
        s.close()
    time.sleep(5)
    s = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
    s.connect((URL, PORT))
    time.sleep(1)
    s.recv(1000).decode()
    return s

def find_flag():
    s = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
    s.connect((URL, PORT))
    time.sleep(1)
    recvbuff = s.recv(1000).decode()
    global FLAG
    while(FLAG[:-1]!="}"):
        try:
            s.send((FLAG+"\n").encode())
            time.sleep(0.5)
            recvbuff = s.recv(1000).decode()
            recvbuff = recvbuff.splitlines()
            reflen = int(recvbuff[2])
        except:
            s = reconnect(s)
        for letter in alphabet:
            test = FLAG + letter
            try:
                s.send((test+"\n").encode())
                time.sleep(0.5)
                recvbuff = s.recv(1000).decode()
                recvbuff = recvbuff.splitlines()
                testlen = int(recvbuff[2])
                if testlen == reflen:
                    FLAG += letter
                    print(FLAG)
                    break
            except:
                s = reconnect(s)
    return FLAG

if __name__ == "__main__":
    flag = find_flag()
    print(flag)
~~~

This provides the flag.

</details>

### Answer

<details>

<summary markdown="span">Flag</summary>

~~~
picoCTF{sheriff_you_solved_the_crime}
~~~

</details>

---

### [Cryptography](#contents) | [PicoCTF](./picoctf.md) | [Home](./index.md)

---

## Scrambled RSA

- Author: Sara
- 140 points

### Description

Hmmm I wonder if you have learned your lesson... Let's see if you understand RSA and how the encryption works. Connect with nc mercury.picoctf.net 58251.

### Hints

1. Look at the ciphertext, anything fishy, maybe a little bit long?
2. What happens if you encrypt the same input multiple times?
3. Is RSA deterministic, why would outputs vary?

### Attachments

None.
 
### Solutions

<details>

<summary markdown="span">Solution 1</summary>

When connecting to the server, we are given the encrypted flag and a prompt to encypt any text value.  The encrypted flag is very large but we notice the encrypted response from the server appears to grow linearly with the string length.  Using python, we can find the relationship between the plaintext string and ciphertext string lengths:

~~~py
import socket
import time

URL = "mercury.picoctf.net"
PORT = 58251
FLAG = "picoCTF{"
alphabet = "abcdefghijklmnopqrstuvwxyzABCDEFGHIJKLMNOPQRSTUVWXYZ_{}"

s = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
s.connect((URL, PORT))
time.sleep(1)
recvbuff = s.recv(100000000).decode()
time.sleep(1)
for i in range(1,5,1):
    s.send(("a"*i+"\n").encode())
    time.sleep(1)
    recvbuff = s.recv(100000).decode()
    recvbuff = recvbuff[13:-38]
    enc_len = len(recvbuff)
    print("a"*i+" encrypted has ct length: "+str(enc_len))
s.close()
~~~

This provides the response:

~~~
a encrypted has ct length: 308
aa encrypted has ct length: 616
aaa encrypted has ct length: 924
aaaa encrypted has ct length: 1233
~~~

It seems the ciphertext is 308 times the length of the plaintext.  Running a similar script, we can find the total pt flag length:

~~~py
import socket
import time

URL = "mercury.picoctf.net"
PORT = 58251
FLAG = "picoCTF{"
alphabet = "abcdefghijklmnopqrstuvwxyzABCDEFGHIJKLMNOPQRSTUVWXYZ_{}"

s = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
s.connect((URL, PORT))
time.sleep(1)
recvbuff = s.recv(10000000000).decode()
recvbuff = recvbuff.splitlines()
ctflaglen = len(recvbuff[0][3:])
ptflaglen = int(ctflaglen/308)
print("CT Flag Length = {}".format(ctflaglen))
print("PT Flag Length = {}".format(ptflaglen))
time.sleep(1)
for i in range(1,5,1):
    s.send(("a"*i+"\n").encode())
    time.sleep(1)
    recvbuff = s.recv(100000).decode()
    recvbuff = recvbuff[13:-38]
    enc_len = len(recvbuff)
    print("a"*i+" encrypted has ct length: "+str(enc_len))
s.close()
~~~

This shows us the flag is 26 characters long. Using the hints, we can see that individual characters when encrypted provide a single ciphertext, however when the string is more than 1 character long, we find the ciphertext changes:

~~~shell
I will encrypt whatever you give me: a
Here you go: 93173283230164554261622370285013636516433899330798519414933760030978723854653511573596456735831042000643840882479843089871583208430072334681656027571332694482359363802225623135712599097419127600856555591086730333960617869699671545840669917723905644766111621169008833808566715172392600058868783983577994658103
I will encrypt whatever you give me: a
Here you go: 93173283230164554261622370285013636516433899330798519414933760030978723854653511573596456735831042000643840882479843089871583208430072334681656027571332694482359363802225623135712599097419127600856555591086730333960617869699671545840669917723905644766111621169008833808566715172392600058868783983577994658103
I will encrypt whatever you give me: ab
Here you go: 93173283230164554261622370285013636516433899330798519414933760030978723854653511573596456735831042000643840882479843089871583208430072334681656027571332694482359363802225623135712599097419127600856555591086730333960617869699671545840669917723905644766111621169008833808566715172392600058868783983577994658103103183667509717853616779950348597809579007053737505176656774350801600521708433029837337268137167287738142659942293004245748056777996393736220304496789681540572796924270472060872888015830277847340115536848315916238995925655773134745996522851474425146755949714769528033583054608627688943835872117081048801319427
I will encrypt whatever you give me: ab
Here you go: 93173283230164554261622370285013636516433899330798519414933760030978723854653511573596456735831042000643840882479843089871583208430072334681656027571332694482359363802225623135712599097419127600856555591086730333960617869699671545840669917723905644766111621169008833808566715172392600058868783983577994658103103183667509717853616779950348597809579007053737505176656774350801600521708433029837337268137167287738142659942293004245748056777996393736220304496789681540572796924270472060872888015830277847340115536848315916238995925655773134745996522851474425146755949714769528033583054608627688943835872117081048801319427
~~~

using the characters pico; we can assign the strings to variables p, i, c, o, pi, pic and pico, in Python we find that pi contains p and another variable but does not contain i:

~~~
p in pi
Out[370]: True

i in pi
Out[371]: False
~~~

When remove p from pi, we get a variable we can assign to i2 which is in variable pic.
	
~~~py
i2 = "".join(pi.split(p))
i2 in pi
Out[375]: True

i2 in pic
Out[376]: True

p in pic
Out[377]: True
~~~
	
Using this logic, we can iterate through the encrypted flag to find the flag:

~~~py
#!/usr/bin/env python3
# -*- coding: utf-8 -*-

import socket
import time
import string

URL = "mercury.picoctf.net"
PORT = 58251
FLAG = "picoCTF{"
alphabet = string.printable

def reconnect(s):
    print("reconnecting:")
    global CTFLAG
    if(s):
        s.close()
        print("session closed")
    time.sleep(10)
    s = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
    s.connect((URL, PORT))
    print("reconnected")
    time.sleep(1)
    recvbuff = s.recv(10000000000).decode()
    recvbuff = recvbuff.splitlines()
    CTFLAG = recvbuff[0][6:]
    print("CT Flag loaded")
    print("CTFLAG length = {}".format(len(CTFLAG)))
    s = load_flag(s)
    return s

def load_flag(s):
    global letter_CT, CTFLAG
    letter_CT = []
    buffer = ""
    for letter in FLAG:
        buffer += letter
        s.send((buffer+"\n").encode())
        time.sleep(1)
        newct = s.recv(10000000000).decode()[13:-38]
        if len(letter_CT)==0:
            letter_CT.append(newct)
            CTFLAG = "".join(CTFLAG.split(newct))
            print("CTFLAG length = {}".format(len(CTFLAG)))
        else:
            for i in range(len(letter_CT)):
                newct = "".join(newct.split(letter_CT[i]))
            letter_CT.append(newct)
            CTFLAG = "".join(CTFLAG.split(newct))
            print("CTFLAG length = {}".format(len(CTFLAG)))
    print("flag loaded")
    print(FLAG)
    return s

def find_flag(s):
    global FLAG, letter_CT, CTFLAG
    while FLAG[-1]!="}":
        try:
            for letter in alphabet:
                newstr = FLAG + letter
                s.send((newstr+"\n").encode())
                time.sleep(1)
                newct = s.recv(10000000000).decode()[13:-38]
                for i in range(len(letter_CT)):
                    newct = "".join(newct.split(letter_CT[i]))
                if newct in CTFLAG:
                    CTFLAG = "".join(CTFLAG.split(newct))
                    FLAG += letter
                    letter_CT.append(newct)
                    print("flag = {}".format(FLAG))
                    print("CTFLAG length = {}".format(len(CTFLAG)))
                    break
        except:
            s = reconnect(s)
    return FLAG

if __name__ == "__main__":
    s = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
    s.connect((URL, PORT))
    s = reconnect(s)
    flag = find_flag(s)
    print("flag found: {}".format(flag))
~~~

This returns the flag

</details>

### Answer

<details>

<summary markdown="span">Flag</summary>

~~~
picoCTF{bad_1d3a5_1314164}
~~~

</details>

---

### [Cryptography](#contents) | [PicoCTF](./picoctf.md) | [Home](./index.md)

---

## Its Not My Fault 1

- Author: rkm0959
- 300 points

### Description

What do you mean RSA with CRT has an attack that's not a fault attack? Connect with nc mercury.picoctf.net 10055. not_my_fault.py

### Hints

None.

### Attachments

1. [not_my_fault.py](https://mercury.picoctf.net/static/409ca1fa5f6a8277796504778c074f03/not_my_fault.py)
 
### Solutions

<details>

<summary markdown="span">Solution</summary>

The source code can be reviewed to see that there are several levels to this problem.  First, the user is required to generate an md5 hash of a string in which the start of the pt ascii conforms to a random string and the end of the hash conforms to another random string:
	
~~~py
vals1 = "".join([random.choice(string.digits) for _ in range(5)])
vals2 = "".join([random.choice(string.hexdigits.lower()) for _ in range(6)])
user_input = input("Enter a string that starts with \"{}\" (no quotes) which creates an md5 hash that ends in these six hex digits: {}\n".format(vals1, vals2))
user_hash = hashlib.md5(user_input.encode()).hexdigest()
~~~
	
This can be solved iteratively in Python:

~~~py
def md5Solver(start,hashend):
    print("Solving md5 hash")
    end = 0
    while True:
        pt_str = start + str(end)
        newhash = hashlib.md5(pt_str.encode()).hexdigest()
        if newhash[-6:]==hashend:
            print("Solution String = {}".format(pt_str))
            print("MD5 Hash = {}".format(newhash))
            return(pt_str)
        end += 1
~~~

After this the python code sends returns the public key.  This provides the exploit; both n and e are significantly large, the private key component d will be relatively small.  We can brute-force the private key in Python using the multiprocessing library to reduce the execution time.  This generates the prime numbers p and q which we require to solve the challenge:
	
~~~py
def dp_test(d_p, e, n, m):
    p = gmpy2.gcd(m - pow(m, e * d_p, n), n)
    if p > 1:
        q = n // p
        return True, (p,q)
    return False

def rsaSolver(e,n,maxd):
    m = random.randint(1000,100000)
    _dp_test = partial(dp_test,e=e,n=n,m=m)
    numP = mp.cpu_count()
    pool = mp.Pool(numP)
    for ret in pool.imap(_dp_test,range(maxd),chunksize=1000):
        if ret[0]:
            return ret[1]
~~~

The primes are added and returned to the challenge server to get the flag.  The complete python code is:
	
~~~py
#!/usr/bin/env python3
# -*- coding: utf-8 -*-

import socket
import time
import hashlib
import random
from functools import partial
import multiprocessing as mp
import gmpy2
from Crypto.Util.number import inverse, getPrime, bytes_to_long, GCD

def md5Solver(start,hashend):
    print("Solving md5 hash")
    end = 0
    while True:
        pt_str = start + str(end)
        newhash = hashlib.md5(pt_str.encode()).hexdigest()
        if newhash[-6:]==hashend:
            print("Solution String = {}".format(pt_str))
            print("MD5 Hash = {}".format(newhash))
            return(pt_str)
        end += 1

def dp_test(d_p, e, n, m):
    p = gmpy2.gcd(m - pow(m, e * d_p, n), n)
    if p > 1:
        q = n // p
        return True, (p,q)
    return False, (0,0)

def rsaSolver(e,n,maxd):
    m = random.randint(1000,100000)
    _dp_test = partial(dp_test,e=e,n=n,m=m)
    numP = mp.cpu_count()
    pool = mp.Pool(numP)
    for ret in pool.imap(_dp_test,range(maxd),chunksize=1000):
        if ret[0]:
            return ret[1]
    
host = "mercury.picoctf.net"
port = 10055
bits = 20
maxr = 1<<bits

s = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
s.connect((host,port))
time.sleep(1)

recvbuff1 = s.recv(1000).decode()
start = recvbuff1.split('\"')[1]
hashend = recvbuff1.split('digits: ')[1].split("\n")[0]

print("Solution string must start {}".format(start))
print("MD5 hash must end {}".format(hashend))

pt_str = md5Solver(start,hashend)
s.send((pt_str+"\n").encode())
time.sleep(2)
recvbuff2 = s.recv(100000).decode()

n = int(recvbuff2.split("\n")[0].split(" : ")[1])
e = int(recvbuff2.split("\n")[1].split(" : ")[1])

print("n = {}".format(n))
print("e = {}".format(e))

# Exploit small d; initial value m<n:
p, q = rsaSolver(e, n, maxr)
print("p = {}".format(p))
print("q = {}".format(q))
ans = p+q
s.send((str(ans)+"\n").encode())
time.sleep(2)
recvbuff3 = s.recv(1000).decode()
print(recvbuff3)
s.close()
~~~
	
</details>

### Answer

<details>

<summary markdown="span">Flag</summary>

~~~
picoCTF{1_c4n'7_b3l13v3_17'5_n07_f4ul7_4774ck!!!}
~~~

</details>

---

### [Cryptography](#contents) | [PicoCTF](./picoctf.md) | [Home](./index.md)

---

## New Vignere

- Author: madStacks
- 300 points

### Description

Another slight twist on a classic, see if you can recover the flag. (Wrap with picoCTF{}) ilnipdjheipnenhhedionepegiejmleoehejfcnimdgehimnepedhhfbafmcgdek new_vignere.py

### Hints

1. [https://en.wikipedia.org/wiki/Vigen%C3%A8re_cipher#Cryptanalysis](https://en.wikipedia.org/wiki/Vigen%C3%A8re_cipher#Cryptanalysis)

### Attachments

1. [new_vignere.py](https://mercury.picoctf.net/static/d86ead586609c44b84b04e08966a4d35/new_vignere.py)
 
### Solutions

<details>

<summary markdown="span">Solution 1</summary>

This challenge can be solved by reverse engineering the Python source code to decrypt and encrypt a string using an unknown key:
	
~~~py
import string

LOWERCASE_OFFSET = ord("a")
ALPHABET = string.ascii_lowercase[:16]

def b16_encode(plain):
	enc = ""
	for c in plain:
		binary = "{0:08b}".format(ord(c))
		enc += ALPHABET[int(binary[:4], 2)]
		enc += ALPHABET[int(binary[4:], 2)]
	return enc

def shift(c, k):
	t1 = ord(c) - LOWERCASE_OFFSET
	t2 = ord(k) - LOWERCASE_OFFSET
	return ALPHABET[(t1 + t2) % len(ALPHABET)]

def b16_decode(encoded):
    pln = ""
    for i in range(0,len(encoded),2):
        idx1 = ALPHABET.index(encoded[i])
        idx2 = ALPHABET.index(encoded[i+1])
        bin1 = "{0:04b}".format(idx1)
        bin2 = "{0:04b}".format(idx2)
        pln += chr(int(bin1+bin2,2))
    return pln

def unshift(c, k):
	t1 = ord(c) - LOWERCASE_OFFSET
	t2 = ord(k) - LOWERCASE_OFFSET
	return ALPHABET[(t1 - t2) % len(ALPHABET)]

def encrypt_string(string,key):
    assert all([k in ALPHABET for k in key]) and len(key) < 15
    assert all([c in "abcdef0123456789" for c in string])
    print("flag = {}".format(string))
    b16 = b16_encode(string)
    print("b16string = {}".format(b16))
    enc = ""
    for i, c in enumerate(b16):
         enc += shift(c, key[i % len(key)])
    print("Encrypted string = {}".format(enc))
    return(enc)

def decrypt_string(string,key):
    print("Encrypted string = {}".format(string))
    b16 = ""
    for i in range(len(string)):
        b16 += unshift(string[i], key[i%len(key)])
    print("b16string = {}".format(b16))
    dec = b16_decode(b16)
    print("flag = {}".format(dec))
    return(dec)
~~~
							      
To find the key, we can identify all valid chars have b16 encoding starting with "d" or "g"; we can use a simple for loop to find the key length:
							     
~~~py
enc_flag_pairs = chr_pairs(enc_flag)
b16_flag_alph = b16_encode(flg_alph)
key = []
for i in range(len(enc_flag_pairs)):
    keyidx = unshift(enc_flag_pairs[i][0],"d")
    keyidx += unshift(enc_flag_pairs[i][0],"g")
    key.append(keyidx)
keylen = list(range(1,16))
for i in range(1,16):
    for j in range(len(key)):
        a = key[j][0]
        b = key[j][1]
        if a in key[j%i] or b in key[j%i]:
            continue
        else:
            keylen.pop(keylen.index(i))
            break
~~~
							      
This identifies the key has length 9;  we can then use a simple brute-force iteration to identify possibel key characters, generate an iteration across all variants and solve for a functional key:

~~~py
keyops = []
for l in keylen:
    key = []
    for i in range(0,l):
        keyx = ""
        for a in ALPHABET:
            win = 1
            for j in range(len(enc_flag)//l):
                enc = enc_flag[j*l+i]
                if unshift(enc,a) in b16_flag_alph:
                    continue
                else:
                    win = 0
                    break
            if win == 1:
                keyx += a
        key.append(keyx)
    keyops.append(key)
goodkeys = []
for key in keyops:
    keydict = [""]
    for keyx in key:
        keylist = []
        for keys in keydict:
            for c in keyx:
                keylist.append(keys+c)
        keydict = keylist
    for keys in keydict:
        try:
            assert all([k in ALPHABET for k in keys]) and len(keys) < 15
            dec = ""
            for i, c in enumerate(enc_flag):
                 dec += unshift(c, keys[i % len(keys)])
            f2 = b16_decode(dec)
            assert all([c in "abcdef0123456789" for c in f2])
            goodkeys.append(keys)
        except:
            continue
~~~

This returns the only valid key, "cjkbjbdbb"  which can be used with the encrypted flag and reverse-engineered decryption algorithm to solve the challenge.
	
</details>

### Answer

<details>

<summary markdown="span">Flag</summary>

~~~
picoCTF{b7bf6c4d2e3c7715489723f360f8d128}
~~~

</details>

---

### [Cryptography](#contents) | [PicoCTF](./picoctf.md) | [Home](./index.md)

---

## Clouds

- Author: madStacks
- 500 points

### Description

Cloud watching is a lot of fun! There are so many different shapes you see in them, and so many different types. They even inspired me to dig up an old cipher I once found to store notes about them. See if you can decrypt them! nc mercury.picoctf.net 10304 clouds.py
The flag for this challenge does not include the standard picoCTF{} wrapper.

### Hints

1. Have you heard of differential cryptanalysis?

### Attachments

1. [clouds.py](https://mercury.picoctf.net/static/0628a018490772c4cf32356734fad366/clouds.py)
 
### Solutions

<details>

<summary markdown="span">Solution 1</summary>

</details>

### Answer

<details>

<summary markdown="span">Flag</summary>

~~~
picoCTF{}
~~~

</details>

---

### [Cryptography](#contents) | [PicoCTF](./picoctf.md) | [Home](./index.md)

---

## spelling-quiz

- Author: BrownieInMotion
- 100 points

### Description

I found the flag, but my brother wrote a program to encrypt all his text files. He has a spelling quiz study guide too, but I don't know if that helps.

### Hints

None.

### Attachments

1. [public.zip](https://artifacts.picoctf.net/picoMini+by+redpwn/Cryptography/spelling-quiz/public.zip)
 
### Solutions

<details>

<summary markdown="span">Solution 1</summary>

Reviewing the python code, we can see the program opens all local txt files and encrypts them using a simple substitution cipher:
	
~~~py
import random
import os

files = [
    os.path.join(path, file)
    for path, dirs, files in os.walk('.')
    for file in files
    if file.split('.')[-1] == 'txt'
]

alphabet = list('abcdefghijklmnopqrstuvwxyz')
random.shuffle(shuffled := alphabet[:])
dictionary = dict(zip(alphabet, shuffled))

for filename in files:
    text = open(filename, 'r').read()
    encrypted = ''.join([
        dictionary[c]
        if c in dictionary else c
        for c in text
    ])
    open(filename, 'w').write(encrypted)
~~~

Luckily, we have a dictionary of enciphered words (study-guide.txt) which we can use to find the key using an [online substitution cipher solver](https://www.guballa.de/substitution-solver).
	
This provides the following cipher key:

~~~txt
abcdefghijklmnopqrstuvwxyz
xunmrydfwhglstibjcavopezqk
~~~

We can write a simple python script to decipher the flag:

~~~py	
ALPHABET = list('abcdefghijklmnopqrstuvwxyz')
KEY = list('xunmrydfwhglstibjcavopezqk')


f1 = open("flag.txt",'r')
enc_flag = f1.read()
f1.close()

flag = ""

for a in enc_flag:
    if a == "_":
        flag += "_"
    elif a == "\n":
        break
    else:
        flag += ALPHABET[KEY.index(a)]

print(flag)
~~~

This provides the flag.

</details>

### Answer

<details>

<summary markdown="span">Flag</summary>

~~~
picoCTF{perhaps_the_dog_jumped_over_was_just_tired}
~~~

</details>

---

### [Cryptography](#contents) | [PicoCTF](./picoctf.md) | [Home](./index.md)

---

## XtraORdinary

- Author: Boolean
- 150 points

### Description

Check out my new, never-before-seen method of encryption! I totally invented it myself. I added so many for loops that I don't even know what it does. It's extraordinarily secure!

### Hints

None.

### Attachments

1. [output.txt](https://artifacts.picoctf.net/picoMini+by+redpwn/Cryptography/xtraordinary/output.txt)
2. [encrypt.py](https://artifacts.picoctf.net/picoMini+by+redpwn/Cryptography/xtraordinary/encrypt.py)
 
### Solutions

<details>

<summary markdown="span">Solution 1</summary>

We are given two files,
	
1. output.txt:
	
~~~
57657535570c1e1c612b3468106a18492140662d2f5967442a2960684d28017931617b1f3637
~~~

2. encrypt.py

~~~py
#!/usr/bin/env python3

from random import randint

with open('flag.txt', 'rb') as f:
    flag = f.read()

with open('secret-key.txt', 'rb') as f:
    key = f.read()

def encrypt(ptxt, key):
    ctxt = b''
    for i in range(len(ptxt)):
        a = ptxt[i]
        b = key[i % len(key)]
        ctxt += bytes([a ^ b])
    return ctxt

ctxt = encrypt(flag, key)

random_strs = [
    b'my encryption method',
    b'is absolutely impenetrable',
    b'and you will never',
    b'ever',
    b'ever',
    b'ever',
    b'ever',
    b'ever',
    b'ever',
    b'break it'
]

for random_str in random_strs:
    for i in range(randint(0, pow(2, 8))):
        for j in range(randint(0, pow(2, 6))):
            for k in range(randint(0, pow(2, 4))):
                for l in range(randint(0, pow(2, 2))):
                    for m in range(randint(0, pow(2, 0))):
                        ctxt = encrypt(ctxt, random_str)

with open('output.txt', 'w') as f:
    f.write(ctxt.hex())
~~~

This is a simple set of xors.  We can find the key by iterating all possible solutions from encrypt,  full solution:

~~~py
import binascii

ctflag = binascii.unhexlify("57657535570c1e1c612b3468106a18492140662d2f5967442a2960684d28017931617b1f3637")

def encrypt(ptxt, key):
    ctxt = b''
    for i in range(len(ptxt)):
        a = ptxt[i]
        b = key[i % len(key)]
        ctxt += bytes([a ^ b])
    return ctxt

random_strs = [
    b'my encryption method',
    b'is absolutely impenetrable',
    b'and you will never',
    b'ever',
    b'break it'
]

if __name__ == "__main__":
    solutions = [ctflag]
    for rstring in random_strs:
        for i in range(len(solutions)):
            ctxt = encrypt(solutions[i],rstring)
            solutions.append(ctxt)
    solutions = list(set(solutions))
    keys = []
    for i in range(len(solutions)):
        newkey = encrypt(solutions[i],b"picoCTF{")
        newkey = newkey[:7]
        keys.append(newkey)
    keys = list(set(keys))
    flags = []
    for key in keys:
        for soln in solutions:
            newflag = encrypt(soln,key).decode()
            if ("picoCTF{" in newflag) and ("}" in newflag):
                print(newflag)
                flags.append(newflag)
~~~

Returns the flag.
	
</details>

### Answer

<details>

<summary markdown="span">Flag</summary>

~~~
picoCTF{w41t_s0_1_d1dnt_1nv3nt_x0r???}
~~~

</details>

---

### [Cryptography](#contents) | [PicoCTF](./picoctf.md) | [Home](./index.md)

---

## triple-secure

- Author: Boolean
- 150 points

### Description

To get the flag, you must break RSA not once, but three times!

### Hints

None. 

### Attachments

1. [public-key.txt](https://artifacts.picoctf.net/picoMini+by+redpwn/Cryptography/triple-secure/public-key.txt)
2. [encrypt.py](https://artifacts.picoctf.net/picoMini+by+redpwn/Cryptography/triple-secure/encrypt.py)
 
### Solutions

<details>

<summary markdown="span">Solution 1</summary>

We are given two files, the encryption algorithm encrypt.py:

~~~py
#!/usr/bin/env python3

from Crypto.Util.number import getPrime, bytes_to_long

with open('flag.txt', 'rb') as f:
    flag = f.read()

p = getPrime(1024)
q = getPrime(1024)
r = getPrime(1024)

n1 = p * q
n2 = p * r
n3 = q * r

moduli = [n1, n2, n3]

e = 65537
c = bytes_to_long(flag)

for n in moduli:
    c = pow(c, e, n)

with open('public-key.txt', 'w') as f:
    f.write(f'n1: {n1}\n')
    f.write(f'n2: {n2}\n')
    f.write(f'n3: {n3}\n')
    f.write(f'e: {e}\n')
    f.write(f'c: {c}\n')
~~~

and the public key, public-key.txt:

~~~
n1: 15192492059814175574941055248891268822162533520576381643453916855435310880285336743521199057138647926712835561752909538944229702432795423884081992987060760867003375755338557996965825324749221386675061886921763747311599846248565297387814717840084998677273427776535730840343260681623323972936404815862969684384733188827100528542007213405382537935243645704237369770300643318878176739181891072725262069278646319502747718264711249767568106460533935904219027313131270918072460753061248221785076571054217566164086518459844527639082962818865640864990672033657423448004651989761933295878220596871163544315057550871764431562609
n2: 15896482259608901559307142941940447232781986632502572991096358742354276347180855512281737388865155342941898447990281534875563129451327818848218781669275420292448483501384399236235069545630630803245125324540747189305877026874280373084005881976783826855683894679886076284892158862128016644725623200756074647449586448311069649515124968073653962156220351541159266665209363921681260367806445996085898841723209546021525012849575330252109081102034217511126192041193752164593519033112893785698509908066978411804133407757110693612926897693360335062446358344787945536573595254027237186626524339635916646549827668224103778645691
n3: 16866741024290909515057727275216398505732182398866918550484373905882517578053919415558082579015872872951000794941027637288054371559194213756955947899010737036612882434425333227722062177363502202508368233645194979635011153509966453453939567651558628538264913958577698775210185802686516291658717434986786180150155217870273053289491069438118831268852205061142773994943387097417127660301519478434586738321776681183207796708047183864564628638795241493797850819727510884955449295504241048877759144706319821139891894102191791380663609673212846473456961724455481378829090944739778647230176360232323776623751623188480059886131
e: 65537
c: 5527557130549486626868355638343164556636640645975070563878791684872084568660950949839392805902757480207470630636669246237037694811318758082850684387745430679902248681495009593699928689084754915870981630249821819243308794164014262751330197659053593094226287631278905866187610594268602850237495796773397013150811502709453828013939726304717253858072813654392558403246468440154864433527550991691477685788311857169847773031859714215539719699781912119479668386111728900692806809163838659848295346731226661208367992168348253106720454566346143578242135426677554444162371330348888185625323879290902076363791018691228620744490
~~~

We can very simply decrypt this using the common factors of n:

~~~py
from math import gcd
from numpy import lcm
import binascii

n1 = 15192492059814175574941055248891268822162533520576381643453916855435310880285336743521199057138647926712835561752909538944229702432795423884081992987060760867003375755338557996965825324749221386675061886921763747311599846248565297387814717840084998677273427776535730840343260681623323972936404815862969684384733188827100528542007213405382537935243645704237369770300643318878176739181891072725262069278646319502747718264711249767568106460533935904219027313131270918072460753061248221785076571054217566164086518459844527639082962818865640864990672033657423448004651989761933295878220596871163544315057550871764431562609
n2 = 15896482259608901559307142941940447232781986632502572991096358742354276347180855512281737388865155342941898447990281534875563129451327818848218781669275420292448483501384399236235069545630630803245125324540747189305877026874280373084005881976783826855683894679886076284892158862128016644725623200756074647449586448311069649515124968073653962156220351541159266665209363921681260367806445996085898841723209546021525012849575330252109081102034217511126192041193752164593519033112893785698509908066978411804133407757110693612926897693360335062446358344787945536573595254027237186626524339635916646549827668224103778645691
n3 = 16866741024290909515057727275216398505732182398866918550484373905882517578053919415558082579015872872951000794941027637288054371559194213756955947899010737036612882434425333227722062177363502202508368233645194979635011153509966453453939567651558628538264913958577698775210185802686516291658717434986786180150155217870273053289491069438118831268852205061142773994943387097417127660301519478434586738321776681183207796708047183864564628638795241493797850819727510884955449295504241048877759144706319821139891894102191791380663609673212846473456961724455481378829090944739778647230176360232323776623751623188480059886131
e = 65537
c = 5527557130549486626868355638343164556636640645975070563878791684872084568660950949839392805902757480207470630636669246237037694811318758082850684387745430679902248681495009593699928689084754915870981630249821819243308794164014262751330197659053593094226287631278905866187610594268602850237495796773397013150811502709453828013939726304717253858072813654392558403246468440154864433527550991691477685788311857169847773031859714215539719699781912119479668386111728900692806809163838659848295346731226661208367992168348253106720454566346143578242135426677554444162371330348888185625323879290902076363791018691228620744490

p = gcd(n1,n2)
r = gcd(n2,n3)
q = gcd(n3,n1)


lambda1 = lcm((p-1),(q-1))
lambda2 = lcm((p-1),(r-1))
lambda3 = lcm((q-1),(r-1))

d1 = pow(e,-1,lambda1)
d2 = pow(e,-1,lambda2)
d3 = pow(e,-1,lambda3)

c = pow(c,d3,n3)
c = pow(c,d2,n2)
c = pow(c,d1,n1)

flag = binascii.unhexlify(hex(c)[2:]).decode()
print(flag)
~~~

This provides the flag.

</details>

### Answer

<details>

<summary markdown="span">Flag</summary>

~~~
picoCTF{1_gu3ss_tr1pl3_rs4_1snt_tr1pl3_s3cur3!!!!!!}
~~~

</details>

---

### [Cryptography](#contents) | [PicoCTF](./picoctf.md) | [Home](./index.md)

---

## college-rowing-team

- Author: Boolean
- 250 points

### Description

I just joined my college's rowing team! To make a good first impression, I started sending my teammates positive automated messages every day. I even send them flags from time to time!

### Hints

None.

### Attachments

1. [encrypted-messages.txt](https://artifacts.picoctf.net/picoMini+by+redpwn/Cryptography/college-rowing-team/encrypted-messages.txt)
2. [encrypt.py](https://artifacts.picoctf.net/picoMini+by+redpwn/Cryptography/college-rowing-team/encrypt.py)
 
### Solutions

<details>

<summary markdown="span">Solution 1</summary>

Reviewing the encryption code, we can see that the same message has been sent to multiple people with the key 3.  As per the chinese remainder theorem, we can recover the PT message by simply taking the cube root of the message:

~~~py
import binascii

def nth_root(x, n):
    # Start with some reasonable bounds around the nth root.
    upper_bound = 1
    while upper_bound ** n <= x:
        upper_bound *= 2
    lower_bound = upper_bound // 2
    # Keep searching for a better result as long as the bounds make sense.
    while lower_bound < upper_bound:
        mid = (lower_bound + upper_bound) // 2
        mid_nth = mid ** n
        if lower_bound < mid and mid_nth < x:
            lower_bound = mid
        elif upper_bound > mid and mid_nth > x:
            upper_bound = mid
        else:
            # Found perfect nth root.
            return mid
    return mid + 1

c = [5065488652323342174251548936130018278628515304559137485528400780060697119682927936946069625772269234638180036633146283242714689277793018059046463458498115311853401434289264038408827377579534270489217094049453933816452196508276029690068611901872786195723358744119490651499187556193711866091991489262948739533990000464588752544599393,
     86893891006724995283854813014390877172735163869036169496565461737741926829273252426484138905500712279566881578262823696620415864916590651557711035982810690227377784525466265776922625254135896966472905776613722370871107640819140591627040592402867504449339363559108090452141753194477174987394954897424151839006206598186417617292433784471465084923195909989,
     86893891006724995283854813014390877172735163869036169496565461737741926829273252426484138905500712279566881578262823696620415864916590651557711035982810690227377784525466265776922625254135896966472905776613722370871107640819140591627040592402867504449339363559108090452141753194477174987394954897424151839006206598186417617292433784471465084923195909989,
     5065488652323342174251548936130018278628515304559137485528400780060697119682927936946069625772269234638180036633146283242714689277793018059046463458498115311853401434289264038408827377579534270489217094049453933816452196508276029690068611901872786195723358744119490651499187556193711866091991489262948739533990000464588752544599393,
     301927034179130315172951479434750678833634853032331571873622664841337454556713005601858152523700291841415874274186191308636935232309742600657257783870282807784519336918511713958804608229440141151963841588389502276162366733982719267670094167338480873020791643860930493832853048467543729024717103511475500012196697609001154401,
     38999477927573480744724357594313956376612559501982863881503907194813646795174312444340693051072410232762895994061399222849450325021561935979706475527169503326744567478138877010606365500800690273,
     38999477927573480744724357594313956376612559501982863881503907194813646795174312444340693051072410232762895994061399222849450325021561935979706475527169503326744567478138877010606365500800690273,
     38999477927573480744724357594313956376612559501982863881503907194813646795174312444340693051072410232762895994061399222849450325021561935979706475527169503326744567478138877010606365500800690273,
     301927034179130315172951479434750678833634853032331571873622664841337454556713005601858152523700291841415874274186191308636935232309742600657257783870282807784519336918511713958804608229440141151963841588389502276162366733982719267670094167338480873020791643860930493832853048467543729024717103511475500012196697609001154401,
     5065488652323342174251548936130018278628515304559137485528400780060697119682927936946069625772269234638180036633146283242714689277793018059046463458498115311853401434289264038408827377579534270489217094049453933816452196508276029690068611901872786195723358744119490651499187556193711866091991489262948739533990000464588752544599393,
     301927034179130315172951479434750678833634853032331571873622664841337454556713005601858152523700291841415874274186191308636935232309742600657257783870282807784519336918511713958804608229440141151963841588389502276162366733982719267670094167338480873020791643860930493832853048467543729024717103511475500012196697609001154401,
     86893891006724995283854813014390877172735163869036169496565461737741926829273252426484138905500712279566881578262823696620415864916590651557711035982810690227377784525466265776922625254135896966472905776613722370871107640819140591627040592402867504449339363559108090452141753194477174987394954897424151839006206598186417617292433784471465084923195909989
     ]
m = []
mstr = []
for i in range(len(c)):
    msg = nth_root(c[i],3)
    m.append(msg)
    mstr.append(binascii.unhexlify(hex(msg)[2:]))
~~~
	
This returns the flag.

</details>

### Answer

<details>

<summary markdown="span">Flag</summary>

~~~
picoCTF{1_gu3ss_p30pl3_p4d_m3ss4g3s_f0r_4_r34s0n}
~~~

</details>

---

### [Cryptography](#contents) | [PicoCTF](./picoctf.md) | [Home](./index.md)

---

## corrupt-key-1

- Author: Tux
- 350 points

### Description

How to fix corrupted key???

### Hints

None.

### Attachments

1. [private.key](https://artifacts.picoctf.net/picoMini+by+redpwn/Cryptography/corrupt-key-1/private.key)
2. [msg.enc](https://artifacts.picoctf.net/picoMini+by+redpwn/Cryptography/corrupt-key-1/msg.enc)
 
### Solutions

<details>

<summary markdown="span">Solution 1</summary>

</details>

### Answer

<details>

<summary markdown="span">Flag</summary>

~~~
picoCTF{}
~~~

</details>

---

### [Cryptography](#contents) | [PicoCTF](./picoctf.md) | [Home](./index.md)

---

## corrupt-key-2

- Author: Tux
- 500 points

### Description

Key corrupted again...

### Hints

None.

### Attachments

1. [private.key](https://artifacts.picoctf.net/picoMini+by+redpwn/Cryptography/corrupt-key-2/private.key)
2. [msg.enc](https://artifacts.picoctf.net/picoMini+by+redpwn/Cryptography/corrupt-key-2/msg.enc)
 
### Solutions

<details>

<summary markdown="span">Solution 1</summary>

</details>

### Answer

<details>

<summary markdown="span">Flag</summary>

~~~
picoCTF{}
~~~

</details>

---

### [Cryptography](#contents) | [PicoCTF](./picoctf.md) | [Home](./index.md)

---

## basic mod1

- Author: Will Hong
- 100 points

### Description

We found this weird message being passed around on the servers, we think we have a working decrpytion scheme. Download the message [here](https://artifacts.picoctf.net/c/397/message.txt). Take each number mod 37 and map it to the following character set: 0-25 is the alphabet (uppercase), 26-35 are the decimal digits, and 36 is an underscore. Wrap your decrypted message in the picoCTF flag format (i.e. picoCTF{decrypted_message})

### Hints

1. Do you know what mod 37 means?
2. mod 37 means modulo 37. It gives the remainder of a number after being divided by 37.

### Attachments

1. [message.txt](https://artifacts.picoctf.net/c/397/message.txt)
 
### Solutions

<details>

<summary markdown="span">Solution 1</summary>

</details>

### Answer

<details>

<summary markdown="span">Flag</summary>

~~~
picoCTF{}
~~~

</details>

---

### [Cryptography](#contents) | [PicoCTF](./picoctf.md) | [Home](./index.md)

---


## basic mod2

- Author: Will Hong
- 100 points

### Description

A new modular challenge! Download the message [here](https://artifacts.picoctf.net/c/503/message.txt). Take each number mod 41 and find the modular inverse for the result. Then map to the following character set: 1-26 are the alphabet, 27-36 are the decimal digits, and 37 is an underscore. Wrap your decrypted message in the picoCTF flag format (i.e. picoCTF{decrypted_message})

### Hints

1. Do you know what the modular inverse is?
2. The inverse modulo z of x is the number, y that when multiplied by x is 1 modulo z
3. It's recommended to use a tool to find the modular inverses

### Attachments

1. [message.txt](https://artifacts.picoctf.net/c/503/message.txt)
 
### Solutions

<details>

<summary markdown="span">Solution 1</summary>

</details>

### Answer

<details>

<summary markdown="span">Flag</summary>

~~~
picoCTF{}
~~~

</details>

---

### [Cryptography](#contents) | [PicoCTF](./picoctf.md) | [Home](./index.md)

---

## credstuff

- Author: Will Hong / LT 'syreal' Jones
- 100 points

### Description

We found a leak of a blackmarket website's login credentials. Can you find the password of the user cultiris and successfully decrypt it? Download the leak [here](https://artifacts.picoctf.net/c/534/leak.tar). The first user in usernames.txt corresponds to the first password in passwords.txt. The second user corresponds to the second password, and so on.

### Hints

1. Maybe other passwords will have hints about the leak?

### Attachments

1. [leak.tar](https://artifacts.picoctf.net/c/534/leak.tar)
 
### Solutions

<details>

<summary markdown="span">Solution 1</summary>

</details>

### Answer

<details>

<summary markdown="span">Flag</summary>

~~~
picoCTF{}
~~~

</details>

---

### [Cryptography](#contents) | [PicoCTF](./picoctf.md) | [Home](./index.md)

---

## morse code

- Author: Will Hong
- 100 points

### Description

Morse code is well known. Can you decrypt this? Download the file [here](https://artifacts.picoctf.net/c/235/morse_chal.wav). Wrap your answer with picoCTF{}, put underscores in place of pauses, and use all lowercase.

### Hints

1. Audacity is a really good program to analyze morse code audio.

### Attachments

1. [morse_chal.wav](https://artifacts.picoctf.net/c/235/morse_chal.wav)
 
### Solutions

<details>

<summary markdown="span">Solution 1</summary>

</details>

### Answer

<details>

<summary markdown="span">Flag</summary>

~~~
picoCTF{}
~~~

</details>

---

### [Cryptography](#contents) | [PicoCTF](./picoctf.md) | [Home](./index.md)

---

## rail fence

- Author: Will Hong
- 100 points

### Description

A type of transposition cipher is the rail fence cipher, which is described [here](https://en.wikipedia.org/wiki/Rail_fence_cipher). Here is one such cipher encrypted using the rail fence with 4 rails. Can you decrypt it? Download the message [here](https://artifacts.picoctf.net/c/276/message.txt). Put the decoded message in the picoCTF flag format, picoCTF{decoded_message}.

### Hints

1. Once you've understood how the cipher works, it's best to draw it out yourself on paper

### Attachments

1. [message.txt](https://artifacts.picoctf.net/c/276/message.txt)
 
### Solutions

<details>

<summary markdown="span">Solution 1</summary>

</details>

### Answer

<details>

<summary markdown="span">Flag</summary>

~~~
picoCTF{}
~~~

</details>

---

### [Cryptography](#contents) | [PicoCTF](./picoctf.md) | [Home](./index.md)

---

## substitution0

- Author: Will Hong
- 100 points

### Description

A message has come in but it seems to be all scrambled. Luckily it seems to have the key at the beginning. Can you crack this substitution cipher? Download the message [here](https://artifacts.picoctf.net/c/383/message.txt).

### Hints

1. Try a frequency attack. An online tool might help.

### Attachments

1. [message.txt](https://artifacts.picoctf.net/c/383/message.txt)
 
### Solutions

<details>

<summary markdown="span">Solution 1</summary>

</details>

### Answer

<details>

<summary markdown="span">Flag</summary>

~~~
picoCTF{}
~~~

</details>

---

### [Cryptography](#contents) | [PicoCTF](./picoctf.md) | [Home](./index.md)

---

## substitution1

- Author: Will Hong
- 100 points

### Description

A second message has come in the mail, and it seems almost identical to the first one. Maybe the same thing will work again. Download the message [here](https://artifacts.picoctf.net/c/418/message.txt).

### Hints

1. Try a frequency attack
2. Do the punctuation and the individual words help you make any substitutions?

### Attachments

1. [message.txt](https://artifacts.picoctf.net/c/418/message.txt)
 
### Solutions

<details>

<summary markdown="span">Solution 1</summary>

</details>

### Answer

<details>

<summary markdown="span">Flag</summary>

~~~
picoCTF{}
~~~

</details>

---

### [Cryptography](#contents) | [PicoCTF](./picoctf.md) | [Home](./index.md)

---

## substitution2

- Author: Will Hong
- 100 points

### Description

It seems that another encrypted message has been intercepted. The encryptor seems to have learned their lesson though and now there isn't any punctuation! Can you still crack the cipher? Download the message [here](https://artifacts.picoctf.net/c/111/message.txt).

### Hints

1. Try refining your frequency attack, maybe analyzing groups of letters would improve your results?

### Attachments

1. [message.txt](https://artifacts.picoctf.net/c/111/message.txt)
 
### Solutions

<details>

<summary markdown="span">Solution 1</summary>

</details>

### Answer

<details>

<summary markdown="span">Flag</summary>

~~~
picoCTF{}
~~~

</details>

---

### [Cryptography](#contents) | [PicoCTF](./picoctf.md) | [Home](./index.md)

---

## transposition trial

- Author: Will Hong
- 100 points

### Description

Our data got corrupted on the way here. Luckily, nothing got replaced, but every block of 3 got scrambled around! The first word seems to be three letters long, maybe you can use that to recover the rest of the message. Download the corrupted message [here](https://artifacts.picoctf.net/c/460/message.txt).

### Hints

1. Split the message up into blocks of 3 and see how the first block is scrambled

### Attachments

1. [message.txt](https://artifacts.picoctf.net/c/460/message.txt)
 
### Solutions

<details>

<summary markdown="span">Solution 1</summary>

</details>

### Answer

<details>

<summary markdown="span">Flag</summary>

~~~
picoCTF{}
~~~

</details>

---

### [Cryptography](#contents) | [PicoCTF](./picoctf.md) | [Home](./index.md)

---

## Vigenere

- Author: Mubarak Mikail
- 100 points

### Description

Can you decrypt this message? Decrypt this [message](https://artifacts.picoctf.net/c/531/cipher.txt) using this key "CYLAB".

### Hints

1. [https://en.wikipedia.org/wiki/Vigen%C3%A8re_cipher](https://en.wikipedia.org/wiki/Vigen%C3%A8re_cipher)

### Attachments

1. [cipher.txt](https://artifacts.picoctf.net/c/531/cipher.txt)
 
### Solutions

<details>

<summary markdown="span">Solution 1</summary>

</details>

### Answer

<details>

<summary markdown="span">Flag</summary>

~~~
picoCTF{}
~~~

</details>

---

### [Cryptography](#contents) | [PicoCTF](./picoctf.md) | [Home](./index.md)

---

## Very Smooth

- Author: Joshua Inscoe
- 300 points

### Description

Forget safe primes... Here, we like to live life dangerously... >:)

### Hints

1. Don't look at me... Go ask Mr. Pollard if you need a hint!

### Attachments

1. [gen.py](https://artifacts.picoctf.net/c/133/gen.py)
2. [output.txt](https://artifacts.picoctf.net/c/133/output.txt)
 
### Solutions

<details>

<summary markdown="span">Solution 1</summary>

</details>

### Answer

<details>

<summary markdown="span">Flag</summary>

~~~
picoCTF{}
~~~

</details>

---

### [Cryptography](#contents) | [PicoCTF](./picoctf.md) | [Home](./index.md)

---

## Sequences

- Author: Anish Singhani
- 400 points

### Description

I wrote this linear recurrence function, can you figure out how to make it run fast enough and get the flag? Download the code here [sequences.py](https://artifacts.picoctf.net/c/510/sequences.py) Note that even an efficient solution might take several seconds to run. If your solution is taking several minutes, then you may need to reconsider your approach.

### Hints

1. Google "matrix diagonalization". Can you figure out how to apply it to this function?

### Attachments

1. [sequences.py](https://artifacts.picoctf.net/c/510/sequences.py)
 
### Solutions

<details>

<summary markdown="span">Solution 1</summary>

</details>

### Answer

<details>

<summary markdown="span">Flag</summary>

~~~
picoCTF{}
~~~

</details>

---

### [Cryptography](#contents) | [PicoCTF](./picoctf.md) | [Home](./index.md)

---

## Sum O Primes

- Author: Joshua Inscoe
- 400 points

### Description

We have so much faith in RSA we give you not just the product of the primes, but their sum as well!

### Hints

1. I love squares :)

### Attachments

1. [gen.py](https://artifacts.picoctf.net/c/182/gen.py)
2. [output.txt](https://artifacts.picoctf.net/c/182/output.txt)
 
### Solutions

<details>

<summary markdown="span">Solution 1</summary>

</details>

### Answer

<details>

<summary markdown="span">Flag</summary>

~~~
picoCTF{}
~~~

</details>

---

### [Cryptography](#contents) | [PicoCTF](./picoctf.md) | [Home](./index.md)

---

## NSA Backdoor

- Author: Joshua Inscoe
- 500 points

### Description

I heard someone has been sneakily installing backdoors in open-source implementations of Diffie-Hellman... I wonder who it could be... ;)

### Hints

1. Look for Mr. Wong's whitepaper... His work has helped so many cats!

### Attachments

1. [gen.py](https://artifacts.picoctf.net/c/261/gen.py)
2. [output.txt](https://artifacts.picoctf.net/c/261/output.txt)
 
### Solutions

<details>

<summary markdown="span">Solution 1</summary>

</details>

### Answer

<details>

<summary markdown="span">Flag</summary>

~~~
picoCTF{}
~~~

</details>

---

### [Cryptography](#contents) | [PicoCTF](./picoctf.md) | [Home](./index.md)

---
	
Page last updated Jan 2021.

## [djm89uk.github.io](https://djm89uk.github.io)
