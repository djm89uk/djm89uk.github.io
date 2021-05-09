# [PicoCTF](./picoctf.md) PicoGym Cryptography

Cryptography is essential to many models of cyber security. Cryptography applies algorithms to shuffle the bits that represent data in such a way that only authorized users can unshuffle them to obtain the original data. 

## Contents

- [Useful References (2019)](#useful-references)
- [The Numbers (2019)](#the-numbers)
- [caesar (2019)](#caesar)
- [Easy1 (2019)](#easy1)
- [13 (2019)](#thirteen)
- [la cifra de (2019)](#la-cifra-de)
- [rsa pop quiz (2019)](#rsa-pop-quiz)
- [Tapping (2019)](#tapping)
- [Mr-Worldwide (2019)](#mr-worldwide)
- [Flags (2019)](#flags)
- [waves over lambda (2019)](#waves-over-lambda)
- [miniRSA (2019)](#minirsa)
- [b00tl3gRSA2 (2019)](#b00tl3grsa2)
- [AES-ABC (2019)](#aes-abc)
- [b00tl3gRSA3 (2019)](#b00tl3grsa3)
- [john_pollard (2019)](#john-pollard)
- [Mod 26 (2021)](#mod26)
- [Mind your Ps and Qs (2021)](#mind-your-ps-and-qs)
- [Easy Peasy (2021)](#easy-peasy)
- [New Ceasar (2021)](#new-ceasar)
- [Mini RSA (2021)](#mini-rsa)
- [Dachshund Attacks (2021)](#dachshund-attacks)
- [No Padding, No Problem (2021)](#no-padding-no-problem)
- [Pixelated (2021)](#pixelated)
- [Play Nice (2021)](#play-nice)
- [Double DES (2021)](#double-des)
- [Compress and Attack (2021)](#compress-and-attack)
- [Scrambled: RSA (2021)](#scrambled-rsa)
- [It's Not My Fault 1 (2021)](#its-not-my-fault-1)
- [New Vignere (2021)](#new-vignere)
- [Clouds (2021)](#clouds)


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

This challenge uses the known exploit of RSA encryption when using a low private exponent.  This is detailed in full by [Dan Boneh](https://crypto.stanford.edu/~dabo/pubs/papers/RSA-survey.pdf).

We can review the RSA algorithm to understand how to exploit this in more detail.

We know:

$$m^e = c (\mathrm{mod} n)$$

Since n is much larger than c:

$$m^e = c (\mathrm{mod} n) = c$$

The message can be recovered by:

$$m = c^{1/e}$$

So we can retrieve the message by taking the cube root of the ciphertext.  This should be easy, however due to the size of the ciphertext integer, we can not simply calculate this using native numerical libraries.  We must use an iterative approach.  Using a very simple iteration, we can find the cube root:

~~~py
n = 29331922499794985782735976045591164936683059380558950386560160105740343201513369939006307531165922708949619162698623675349030430859547825708994708321803705309459438099340427770580064400911431856656901982789948285309956111848686906152664473350940486507451771223435835260168971210087470894448460745593956840586530527915802541450092946574694809584880896601317519794442862977471129319781313161842056501715040555964011899589002863730868679527184420789010551475067862907739054966183120621407246398518098981106431219207697870293412176440482900183550467375190239898455201170831410460483829448603477361305838743852756938687673
e = 3
ct = 2205316413931134031074603746928247799030155221252519872650080519263755075355825243327515211479747536697517688468095325517209911688684309894900992899707504087647575997847717180766377832435022794675332132906451858990782325436498952049751141 

guessmax = int(1)

while guessmax**3 < ct:
    guessmax *= 10

guessmin = int(guessmax/10)

guess = int((guessmin+guessmax)/2)

while guess**3 != ct:
    if guess**3 > ct:
        guessmax = int(guess)
        guess = int(guessmin + int((guessmax-guessmin)/2))
    elif guess**3<ct:
        guessmin = int(guess)
        guess = int(guessmin + int((guessmax-guessmin)/2))

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

Last updated 09 May 2021.

## [djm89uk.github.io](https://djm89uk.github.io)
