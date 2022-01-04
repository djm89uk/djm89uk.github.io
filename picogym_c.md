# [PicoCTF](./picoctf.md) PicoGym Cryptography [26/36]

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
- [Mod 26 (2021)](#mod26) ✓
- [Mind your Ps and Qs (2021)](#mind-your-ps-and-qs) ✓
- [Easy Peasy (2021)](#easy-peasy) ✓
- [New Caesar (2021)](#new-caesar) ✓
- [Mini RSA (2021)](#mini-rsa) ✓
- [Dachshund Attacks (2021)](#dachshund-attacks) ✓
- [No Padding, No Problem (2021)](#no-padding-no-problem) ✓
- [Pixelated (2021)](#pixelated) ✓
- [Play Nice (2021)](#play-nice) ✓
- [Double DES (2021)](#double-des) ✓
- [Compress and Attack (2021)](#compress-and-attack)
- [Scrambled: RSA (2021)](#scrambled-rsa)
- [It's Not My Fault 1 (2021)](#its-not-my-fault-1)
- [New Vignere (2021)](#new-vignere)
- [Clouds (2021)](#clouds)
- [Spelling-Quiz (2021)](#spelling-quiz) ✓
- [XtraORdinary (2021)](#xtraordinary)
- [Triple-Secure (2021)](#triple-secure)
- [College-Rowing-Team (2021)](#college-rowing-team)
- [Corrupt-key-1 (2021)](#corrupt-key-1)
- [Corrupt-key-2 (2021)](#corrupt-key-2)

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
#!/usr/bin/env python3
# -*- coding: utf-8 -*-
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
        print("Flag: picoCTF{%s}"%flag)
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
	
Page last updated Jan 2021.

## [djm89uk.github.io](https://djm89uk.github.io)
