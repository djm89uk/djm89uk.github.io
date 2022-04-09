# [Root-Me](./rootme.md) Root-Me Cryptanalysis [19/56]

Break encryption algorithms.

## Contents

1. [Encoding - ASCII](#encoding-ascii) 🗸
2. [Encoding - UU](#encoding-uu) 🗸
3. [Hash - DCC](#hash-dcc) 🗸
4. [Hash - DCC2](#hash-dcc2) 🗸
5. [Hash - LM](#hash-lm) 🗸
6. [Hash - Message Digest 5](#hash-message-digest-5) 🗸
7. [Hash - NT](#hash-nt) 🗸
8. [Hash - SHA-2](#hash-sha-2) 🗸
9. [Shift cipher](#shift-cipher) 🗸
10. [CISCO - Salted Password](#cisco-salted-password) 🗸
11. [Pixel Madness](#pixel-madness) 🗸
12. [ELF64 - PID encryption](#elf64-pid-encryption) 🗸
13. [File - PKZIP](#file-pkzip) 🗸
14. [Monoalphabetic substitution - Caesar](#monoalphabetic-substitution-caesar) 🗸
15. [Known plaintext - XOR](#known-plaintext-xOr) 🗸
16. [Code - Pseudo Random Number Generator](#code-pseudo-random-number-generator)
17. [File - Insecure storage 1](#file-insecure-storage-1) 🗸
18. [Polyalphabetic substitution - Vigenère](#polyalphabetic-substitution-vigenere) 🗸
19. [System - Android lock pattern](#system-android-lock-pattern) 🗸
20. [Transposition - Rail Fence](#transposition-rail-fence) 🗸
21. [AES - CBC - Bit-Flipping Attack](#aes-cbc-bit-flipping-attack)
22. [AES - ECB](#aes-ecb)
23. [LFSR - Known plaintext](#lfsr-known-plaintext)
24. [RSA - Factorisation](#rsa-factorisation) 🗸
25. [RSA - Decipher Oracle](#rsa-decipher-pracle)
26. [Service - Timing attack](#service-timing-attack)
27. [Monoalphabetic substitution - Polybe](#monoalphabetic-substitution-polybe) 🗸
28. [Twisted secret](#twisted-secret)
29. [Initialisation Vector](#initialisation-vector)
30. [GEDEFU](#gedefu)
31. [OTP - Implementation error](#Otp-implementation-error)
32. [RSA - Corrupted key 1](#rsa-corrupted-key-1)
33. [RSA - Continued fractions](#rsa-continued-fractions)
34. [RSA - Common modulus](#rsa-common-modulus)
35. [Service - Hash length extension attack](#service-hash-length-extension-attack)
36. [AES - 4 Rounds](#aes-4-rounds)
37. [ECDSA - Introduction](#ecdsa-introduction)
38. [RSA - Padding](#rsa-padding)
39. [RSA - Signature](#rsa-signature)
40. [AES128 - CTR](#aes128-ctr)
41. [Discrete logarithm problem](#discrete-logarithm-problem)
42. [RSA - Corrupted key 2](#rsa-corrupted-key-2)
43. [RSA - Corrupted key 3](#rsa-corrupted-key-3)
44. [RSA - Multiple recipients](#rsa-multiple-recipients)
45. [AES - Fault attack #1](#aes-fault-attack-1)
46. [Enigma Machine](#enigma-machine)
47. [ECDHE](#ecdhe)
48. [RSA - Lee cooper](#rsa-lee-cooper)
49. [Service - CBC Padding](#service-cbc-padding)
50. [Polyalphabetic substitution - One Time Pad](#polyalphabetic-substitution-One-time-pad)
51. [White-Box Cryptography](#white-box-cryptography)
52. [AES - Weaker variant](#aes-weaker-variant)
53. [Hash - SHA-3](#hash-sha-3)
54. [AES - Fault attack #2](#aes-fault-attack-2)
55. [AES-PMAC](#aes-pmac)
56. [ECDSA - Implementation error](#ecdsa-implementation-error)


---

### [Cryptanalysis](#contents) | [Root-Me](./rootme.md) | [Home](./index.md)

---

## Encoding ASCII

- Author: Xartrick
- Date: 04 December 2012
- Points: 5
- Level: 1

### Statement

Decode the string.

### Resources

1. [ASCII Table](https://repository.root-me.org/Cryptographie/EN%20-%20ASCII%20Table.gif)

### Attachments

1. [ch8.txt](http://challenge01.root-me.org/cryptanalyse/ch8/ch8.txt).

### Solutions

<details>

<summary markdown="span">Solution 1</summary>

We are given a text string that appears to be hex:
 
~~~
4C6520666C6167206465206365206368616C6C656E6765206573743A203261633337363438316165353436636436383964356239313237356433323465
~~~

We can use the binascii library in python:

~~~py
import binascii

ans_hex = "4C6520666C6167206465206365206368616C6C656E6765206573743A203261633337363438316165353436636436383964356239313237356433323465"
ans_ascii = binascii.unhexlify(ans_hex.encode()).decode()
print(ans_ascii)
~~~
  
This provides output:

~~~
Le flag de ce challenge est: 2ac376481ae546cd689d5b91275d324e
~~~

</details>

### Answer

<details>

<summary markdown="span">Answer</summary>

~~~
2ac376481ae546cd689d5b91275d324e
~~~

</details>

---

### [Cryptanalysis](#contents) | [Root-Me](./rootme.md) | [Home](./index.md)

---

## Encoding UU

- Author: g0uZ
- Date: 07 October 2006
- Points: 5
- Level: 1

### Statement

Get the validation password.

### Resources

1. [Encodings format](https://repository.root-me.org/Cryptographie/EN%20-%20Encodings%20format.pdf).

### Attachments

1. [ch1.txt](http://challenge01.root-me.org/cryptanalyse/ch1/ch1.txt).

### Solutions

<details>

<summary markdown="span">Solution 1</summary>

We are given a text string:
 
~~~
_=_ 
_=_ Part 001 of 001 of file root-me_challenge_uudeview
_=_ 

begin 644 root-me_challenge_uudeview
B5F5R>2!S:6UP;&4@.RD*4$%34R`](%5,5%)!4TE-4$Q%"@``
`
end
~~~

We can use the binascii library in python:

~~~py
import binascii

ans_uu = "B5F5R>2!S:6UP;&4@.RD*4$%34R`](%5,5%)!4TE-4$Q%\"@``"
ans_ascii = binascii.a2b_uu(ans_uu.encode())
print(ans_ascii)
~~~
  
This provides output:

~~~
b'Very simple ;)\nPASS = ULTRASIMPLE\n'
~~~

</details>

### Answer

<details>

<summary markdown="span">Answer</summary>

~~~
ULTRASIMPLE
~~~

</details>

---

### [Cryptanalysis](#contents) | [Root-Me](./rootme.md) | [Home](./index.md)

---

## Hash DCC

- Author: Shutdown, Podalirius
- Date: 13 July 2021
- Points: 5
- Level: 1

### Statement

Retrieve the password of the Administrator user from the information output by the secretsdump tool of the Impacket suite.

### Resources

1. [doku.php?id=example_hashes](https://hashcat.net/wiki/doku.php?id=example_hashes).
2. [cracking](https://www.thehacker.recipes/ad-ds/movement/credentials/cracking).

### Attachments

1. [ch50.txt](http://challenge01.root-me.org/cryptanalyse/ch50/ch50.txt).

### Solutions

<details>

<summary markdown="span">Solution 1</summary>

We are given a text file:
 
~~~
[*] Target system bootKey: 0xf1527e4742bbac097f937cc4ac8508e4
[*] Dumping local SAM hashes (uid:rid:lmhash:nthash)
Administrator:500:aad3b435b51404eeaad3b435b51404ee:31d6cfe0d16ae931b73c59d7e0c089c0:::
Guest:501:aad3b435b51404eeaad3b435b51404ee:31d6cfe0d16ae931b73c59d7e0c089c0:::
ASPNET:1025:aad3b435b51404eeaad3b435b51404ee:31d6cfe0d16ae931b73c59d7e0c089c0:::
DBAdmin:1028:aad3b435b51404eeaad3b435b51404ee:31d6cfe0d16ae931b73c59d7e0c089c0:::
sshd:1037:aad3b435b51404eeaad3b435b51404ee:31d6cfe0d16ae931b73c59d7e0c089c0:::
service_user:1038:aad3b435b51404eeaad3b435b51404ee:31d6cfe0d16ae931b73c59d7e0c089c0:::
[*] Dumping cached domain logon information (domain/username:hash)
ROOTME.LOCAL/PODALIRIUS:$DCC2$10240#PODALIRIUS#9d3e8dbe4d9816fa1a5dda431ef2f6f1
ROOTME.LOCAL/SHUTDOWN:$DCC2$10240#SHUTDOWN#9d3e8dbe4d9816fa1a5dda431ef2f6f1
ROOTME.LOCAL/Administrator:15a57c279ebdfea574ad1ff91eb6ef0c:Administrator
[*] Dumping LSA Secrets
[*] $MACHINE.ACC
ROOTME\PC01$:aes256-cts-hmac-sha1-96:e6d5ab8e29fb4f648490fb1cb099b64dffbd2b9e77d46b8df41bc482d590bfe3
ROOTME\PC01$:aes128-cts-hmac-sha1-96:971589d11f2a62980fcab210fa442f4a
ROOTME\PC01$:des-cbc-md5:f18f6dfb6b197fe9
ROOTME\PC01$:plain_password_hex:a918646aa8406975d5ed97534946ef780d48075e618e309b30bf5c9f
ROOTME\PC01$:88c2213866d15f645295e3ebc8779879:ba380afe874fbc0d99b16f8188968133:::
[*] DPAPI_SYSTEM
dpapi_machinekey:0xf35c35eddeecd7b0da287db2e4f8b89b96387157
dpapi_userkey:0x04b4fb8214fb142f86ca2c34de1866f7e565f6f1
[*] NL$KM
 0000   E4 7B 83 10 D7 9D A9 FE  C5 B7 F9 CB 81 27 2A 13   .{...........'*.
 0010   9B 61 D1 F2 9C 0B 1C 8C  53 55 42 46 02 51 10 AC   .A......SUBF.Q..
 0020   4C 02 88 83 CF 37 C8 0C  D3 16 71 96 9E 0E B5 46   L....7....Q....F
 0030   C5 A4 D0 26 8A 77 40 85  B2 E6 1A 8D CF CB A3 46   ...&.W@........F
NL$KM:e47b8310d79da9fec5b7f9cb81272a139b61d1f29c0b1c8c53554246025110ac4c028883cf37c80cd31671969e0eb546c5a4d0268a774085b2e61a8dcfcba346
[*] _SC_sos_scheduler_scibeta
ELITE\CHOUPAPI:Mdp!1256@
[*] _SC_sshd
service_user:Mdp!1256@
[*] Cleaning up...

~~~

We can use hashcat to decrypt these hashes.  First, we create a hash file, hash.txt:
  
~~~
aad3b435b51404eeaad3b435b51404ee:31d6cfe0d16ae931b73c59d7e0c089c0
15a57c279ebdfea574ad1ff91eb6ef0c:Administrator
~~~

We can use -m 1100 for DCC and run hashcat with rockyou.txt:
 
~~~shell
$ hashcat -m 1100 -a 0 -o cracked.txt hash.txt rockyou.txt --show
~~~
  
This generates a text file, cracked.txt:

~~~
15a57c279ebdfea574ad1ff91eb6ef0c:administrator:ilikethat
~~~

</details>

### Answer

<details>

<summary markdown="span">Answer</summary>

~~~
ilikethat
~~~

</details>

---

### [Cryptanalysis](#contents) | [Root-Me](./rootme.md) | [Home](./index.md)

---

## Hash DCC2

- Author: Shutdown, Podalirius
- Date: 13 July 2021
- Points: 5
- Level: 1

### Statement

Retrieve the password of the Administrator user from the information output by the secretsdump tool of the Impacket suite.

### Resources

1. [doku.php?id=example_hashes](https://hashcat.net/wiki/doku.php?id=example_hashes).
2. [cracking](https://www.thehacker.recipes/ad-ds/movement/credentials/cracking).

### Attachments

1. [ch51txt](http://challenge01.root-me.org/cryptanalyse/ch51/ch51.txt).

### Solutions

<details>

<summary markdown="span">Solution 1</summary>

We are given a text file:
 
~~~
[*] Target system bootKey: 0xf1527e4742bbac097f937cc4ac8508e4
[*] Dumping local SAM hashes (uid:rid:lmhash:nthash)
Administrator:500:aad3b435b51404eeaad3b435b51404ee:31d6cfe0d16ae931b73c59d7e0c089c0:::
Guest:501:aad3b435b51404eeaad3b435b51404ee:31d6cfe0d16ae931b73c59d7e0c089c0:::
ASPNET:1025:aad3b435b51404eeaad3b435b51404ee:31d6cfe0d16ae931b73c59d7e0c089c0:::
DBAdmin:1028:aad3b435b51404eeaad3b435b51404ee:31d6cfe0d16ae931b73c59d7e0c089c0:::
sshd:1037:aad3b435b51404eeaad3b435b51404ee:31d6cfe0d16ae931b73c59d7e0c089c0:::
service_user:1038:aad3b435b51404eeaad3b435b51404ee:31d6cfe0d16ae931b73c59d7e0c089c0:::
[*] Dumping cached domain logon information (domain/username:hash)
ROOTME.LOCAL/PODALIRIUS:$DCC2$10240#PODALIRIUS#9d3e8dbe4d9816fa1a5dda431ef2f6f1
ROOTME.LOCAL/SHUTDOWN:$DCC2$10240#SHUTDOWN#9d3e8dbe4d9816fa1a5dda431ef2f6f1
ROOTME.LOCAL/Administrator:$DCC2$10240#Administrator#23d97555681813db79b2ade4b4a6ff25
[*] Dumping LSA Secrets
[*] $MACHINE.ACC
ROOTME\PC01$:aes256-cts-hmac-sha1-96:e6d5ab8e29fb4f648490fb1cb099b64dffbd2b9e77d46b8df41bc482d590bfe3
ROOTME\PC01$:aes128-cts-hmac-sha1-96:971589d11f2a62980fcab210fa442f4a
ROOTME\PC01$:des-cbc-md5:f18f6dfb6b197fe9
ROOTME\PC01$:plain_password_hex:a918646aa8406975d5ed97534946ef780d48075e618e309b30bf5c9f
ROOTME\PC01$:88c2213866d15f645295e3ebc8779879:ba380afe874fbc0d99b16f8188968133:::
[*] DPAPI_SYSTEM
dpapi_machinekey:0xf35c35eddeecd7b0da287db2e4f8b89b96387157
dpapi_userkey:0x04b4fb8214fb142f86ca2c34de1866f7e565f6f1
[*] NL$KM
 0000   E4 7B 83 10 D7 9D A9 FE  C5 B7 F9 CB 81 27 2A 13   .{...........'*.
 0010   9B 61 D1 F2 9C 0B 1C 8C  53 55 42 46 02 51 10 AC   .A......SUBF.Q..
 0020   4C 02 88 83 CF 37 C8 0C  D3 16 71 96 9E 0E B5 46   L....7....Q....F
 0030   C5 A4 D0 26 8A 77 40 85  B2 E6 1A 8D CF CB A3 46   ...&.W@........F
NL$KM:e47b8310d79da9fec5b7f9cb81272a139b61d1f29c0b1c8c53554246025110ac4c028883cf37c80cd31671969e0eb546c5a4d0268a774085b2e61a8dcfcba346
[*] _SC_sos_scheduler_scibeta
ELITE\CHOUPAPI:Mdp!1256@
[*] _SC_sshd
service_user:Mdp!1256@
[*] Cleaning up...
~~~

We can use hashcat to decrypt these hashes.  First, we create a hash file, hash.txt:
  
~~~
$DCC2$10240#Administrator#23d97555681813db79b2ade4b4a6ff25
~~~

We can use -m 2100 for DCC2 and run hashcat with rockyou.txt:
 
~~~shell
$ hashcat -m 2100 -a 0 -o cracked.txt hash.txt rockyou.txt
~~~
  
This generates a text file, cracked.txt:

~~~
$DCC2$10240#administrator#23d97555681813db79b2ade4b4a6ff25:ihatepasswords
~~~

</details>

### Answer

<details>

<summary markdown="span">Answer</summary>

~~~
ihatepasswords
~~~

</details>

---

### [Cryptanalysis](#contents) | [Root-Me](./rootme.md) | [Home](./index.md)

---

## Hash LM

- Author: Shutdown, Podalirius
- Date: 13 July 2021
- Points: 5
- Level: 1

### Statement

Retrieve the password of the Administrator user from the information output by the secretsdump tool of the Impacket suite.

Note: the flag is in lowercase

### Resources

1. [doku.php?id=example_hashes](https://hashcat.net/wiki/doku.php?id=example_hashes).
2. [cracking](https://www.thehacker.recipes/ad-ds/movement/credentials/cracking).

### Attachments

1. [ch49.txt](http://challenge01.root-me.org/cryptanalyse/ch49/ch49.txt).

### Solutions

<details>

<summary markdown="span">Solution 1</summary>

We are given a text file:
 
~~~
[*] Target system bootKey: 0xf1527e4742bbac097f937cc4ac8508e4
[*] Dumping local SAM hashes (uid:rid:lmhash:nthash)
Administrator:500:d3bf255c530633b9aad3b435b51404ee:31d6cfe0d16ae931b73c59d7e0c089c0:::
Guest:501:aad3b435b51404eeaad3b435b51404ee:31d6cfe0d16ae931b73c59d7e0c089c0:::
ASPNET:1025:aad3b435b51404eeaad3b435b51404ee:31d6cfe0d16ae931b73c59d7e0c089c0:::
DBAdmin:1028:aad3b435b51404eeaad3b435b51404ee:31d6cfe0d16ae931b73c59d7e0c089c0:::
sshd:1037:aad3b435b51404eeaad3b435b51404ee:31d6cfe0d16ae931b73c59d7e0c089c0:::
service_user:1038:aad3b435b51404eeaad3b435b51404ee:31d6cfe0d16ae931b73c59d7e0c089c0:::
[*] Dumping cached domain logon information (domain/username:hash)
ROOTME.LOCAL/PODALIRIUS:$DCC2$10240#PODALIRIUS#9d3e8dbe4d9816fa1a5dda431ef2f6f1
ROOTME.LOCAL/SHUTDOWN:$DCC2$10240#SHUTDOWN#9d3e8dbe4d9816fa1a5dda431ef2f6f1
[*] Dumping LSA Secrets
[*] $MACHINE.ACC
ROOTME\PC01$:aes256-cts-hmac-sha1-96:e6d5ab8e29fb4f648490fb1cb099b64dffbd2b9e77d46b8df41bc482d590bfe3
ROOTME\PC01$:aes128-cts-hmac-sha1-96:971589d11f2a62980fcab210fa442f4a
ROOTME\PC01$:des-cbc-md5:f18f6dfb6b197fe9
ROOTME\PC01$:plain_password_hex:a918646aa8406975d5ed97534946ef780d48075e618e309b30bf5c9f
ROOTME\PC01$:88c2213866d15f645295e3ebc8779879:ba380afe874fbc0d99b16f8188968133:::
[*] DPAPI_SYSTEM
dpapi_machinekey:0xf35c35eddeecd7b0da287db2e4f8b89b96387157
dpapi_userkey:0x04b4fb8214fb142f86ca2c34de1866f7e565f6f1
[*] NL$KM
 0000   E4 7B 83 10 D7 9D A9 FE  C5 B7 F9 CB 81 27 2A 13   .{...........'*.
 0010   9B 61 D1 F2 9C 0B 1C 8C  53 55 42 46 02 51 10 AC   .A......SUBF.Q..
 0020   4C 02 88 83 CF 37 C8 0C  D3 16 71 96 9E 0E B5 46   L....7....Q....F
 0030   C5 A4 D0 26 8A 77 40 85  B2 E6 1A 8D CF CB A3 46   ...&.W@........F
NL$KM:e47b8310d79da9fec5b7f9cb81272a139b61d1f29c0b1c8c53554246025110ac4c028883cf37c80cd31671969e0eb546c5a4d0268a774085b2e61a8dcfcba346
[*] _SC_sos_scheduler_scibeta
ELITE\CHOUPAPI:Mdp!1256@
[*] _SC_sshd
service_user:Mdp!1256@
[*] Cleaning up...
~~~

We can use hashcat to decrypt these hashes.  First, we create a hash file, hash.txt:
  
~~~
Administrator:500:d3bf255c530633b9aad3b435b51404ee:31d6cfe0d16ae931b73c59d7e0c089c0:::
~~~

We can use -m 3000 for LM and run hashcat with rockyou.txt:
 
~~~shell
$ hashcat -m 3000 -a 0 -o cracked.txt hash.txt rockyou.txt
~~~
  
This generates a text file, cracked.txt:

~~~
d3bf255c530633b9:ADMIN!!
~~~

</details>

### Answer

<details>

<summary markdown="span">Answer</summary>

~~~
admin!!
~~~

</details>

---

### [Cryptanalysis](#contents) | [Root-Me](./rootme.md) | [Home](./index.md)

---

## Hash Message Digest 5

- Author: g0uZ
- Date: 31 January 2010
- Points: 5
- Level: 1

### Statement

Crack the given hash.

### Resources

1. [Collisions of MD5](https://repository.root-me.org/Cryptographie/EN%20-%20Collisions%20of%20MD5.pdf).
2. [RFC 1321](https://repository.root-me.org/RFC/EN%20-%20rfc1321.txt).

### Attachments

1. [ch2.txt](http://challenge01.root-me.org/cryptanalyse/ch2/ch2.txt).

### Solutions

<details>

<summary markdown="span">Solution 1</summary>

We are given a text file:
 
~~~
7ecc19e1a0be36ba2c6f05d06b5d3058
~~~

We can use hashcat to decrypt these hashes.  First, we create a hash file, hash.txt:
  
~~~
7ecc19e1a0be36ba2c6f05d06b5d3058
~~~

We can use -m 0 for MD5 and run hashcat with rockyou.txt:
 
~~~shell
$ hashcat -m 0 -a 0 -o cracked.txt hash.txt rockyou.txt
~~~
  
This generates a text file, cracked.txt:

~~~
7ecc19e1a0be36ba2c6f05d06b5d3058:weak
~~~

</details>

### Answer

<details>

<summary markdown="span">Answer</summary>

~~~
weak
~~~

</details>

---

### [Cryptanalysis](#contents) | [Root-Me](./rootme.md) | [Home](./index.md)

---

## Hash NT

- Author: Shutdown, Podalirius
- Date: 13 July 2021
- Points: 5
- Level: 1

### Statement

Retrieve the password of the Administrator user from the information given by the secretsdump tool of the Impacket suite.

### Resources

1. [cracking](https://www.thehacker.recipes/ad-ds/movement/credentials/cracking).

### Attachments

1. [ch48.txt](http://challenge01.root-me.org/cryptanalyse/ch48/ch48.txt).

### Solutions

<details>

<summary markdown="span">Solution 1</summary>

We are given a text file:
 
~~~
[*] Target system bootKey: 0xf1527e4742bbac097f937cc4ac8508e4
[*] Dumping local SAM hashes (uid:rid:lmhash:nthash)
Administrator:500:aad3b435b51404eeaad3b435b51404ee:b4f79698831d92b61f886438e36c0c52:::
Guest:501:aad3b435b51404eeaad3b435b51404ee:31d6cfe0d16ae931b73c59d7e0c089c0:::
ASPNET:1025:aad3b435b51404eeaad3b435b51404ee:31d6cfe0d16ae931b73c59d7e0c089c0:::
DBAdmin:1028:aad3b435b51404eeaad3b435b51404ee:31d6cfe0d16ae931b73c59d7e0c089c0:::
sshd:1037:aad3b435b51404eeaad3b435b51404ee:31d6cfe0d16ae931b73c59d7e0c089c0:::
service_user:1038:aad3b435b51404eeaad3b435b51404ee:31d6cfe0d16ae931b73c59d7e0c089c0:::
[*] Dumping cached domain logon information (domain/username:hash)
ROOTME.LOCAL/PODALIRIUS:$DCC2$10240#PODALIRIUS#9d3e8dbe4d9816fa1a5dda431ef2f6f1
ROOTME.LOCAL/SHUTDOWN:$DCC2$10240#SHUTDOWN#9d3e8dbe4d9816fa1a5dda431ef2f6f1
[*] Dumping LSA Secrets
[*] $MACHINE.ACC
ROOTME\PC01$:aes256-cts-hmac-sha1-96:e6d5ab8e29fb4f648490fb1cb099b64dffbd2b9e77d46b8df41bc482d590bfe3
ROOTME\PC01$:aes128-cts-hmac-sha1-96:971589d11f2a62980fcab210fa442f4a
ROOTME\PC01$:des-cbc-md5:f18f6dfb6b197fe9
ROOTME\PC01$:plain_password_hex:a918646aa8406975d5ed97534946ef780d48075e618e309b30bf5c9f
ROOTME\PC01$:88c2213866d15f645295e3ebc8779879:ba380afe874fbc0d99b16f8188968133:::
[*] DPAPI_SYSTEM
dpapi_machinekey:0xf35c35eddeecd7b0da287db2e4f8b89b96387157
dpapi_userkey:0x04b4fb8214fb142f86ca2c34de1866f7e565f6f1
[*] NL$KM
 0000   E4 7B 83 10 D7 9D A9 FE  C5 B7 F9 CB 81 27 2A 13   .{...........'*.
 0010   9B 61 D1 F2 9C 0B 1C 8C  53 55 42 46 02 51 10 AC   .A......SUBF.Q..
 0020   4C 02 88 83 CF 37 C8 0C  D3 16 71 96 9E 0E B5 46   L....7....Q....F
 0030   C5 A4 D0 26 8A 77 40 85  B2 E6 1A 8D CF CB A3 46   ...&.W@........F
NL$KM:e47b8310d79da9fec5b7f9cb81272a139b61d1f29c0b1c8c53554246025110ac4c028883cf37c80cd31671969e0eb546c5a4d0268a774085b2e61a8dcfcba346
[*] _SC_sos_scheduler_scibeta
ELITE\CHOUPAPI:Mdp!1256@
[*] _SC_sshd
service_user:Mdp!1256@
[*] Cleaning up...
~~~

We can use hashcat to decrypt these hashes.  First, we create a hash file, hash.txt:
  
~~~
Administrator:500:aad3b435b51404eeaad3b435b51404ee:b4f79698831d92b61f886438e36c0c52:::
~~~

We can see the following components of the NTLM hash:

- Username: Administrator
- Relative Identifier: 500 (administrator)
- LM Hash: aad3b435b51404eeaad3b435b51404ee
- NT Hash: b4f79698831d92b61f886438e36c0c52
  
With hashtxt we are unable to find the password with normal dictionaries.  Brute force is an option but will take considerable time. Using online dehasher, [hashes.com](https://hashes.com) we can find the NT hash:
  
~~~
b4f79698831d92b61f886438e36c0c52:iloveyou99!
~~~

</details>

### Answer

<details>

<summary markdown="span">Answer</summary>

~~~
iloveyou99!
~~~

</details>

---

### [Cryptanalysis](#contents) | [Root-Me](./rootme.md) | [Home](./index.md)

---

## Hash SHA 2

- Author: koma
- Date: 03 June 2012
- Points: 5
- Level: 1

### Statement

This hash was stolen during a session interception on a critical application, errors may have occurred during transmission. No crack attempt has resulted so far; hash format seems unknown. Find the corresponding plaintext.

The answer is the SHA-1 of this password.

### Resources

1. [RFC 5754](https://repository.root-me.org/RFC/EN%20-%20rfc5754.txt).

### Attachments

1. [ch13.txt](http://challenge01.root-me.org/cryptanalyse/ch13/ch13.txt).

### Solutions

<details>

<summary markdown="span">Solution 1</summary>

We are given a text file:
 
~~~
96719db60d8e3f498c98d94155e1296aac105ck4923290c89eeeb3ba26d3eef92
~~~

Inspecting the hash, we can see it has a non-hexadecimal character, "k".  removing this character, we can see the hash conforms to the SHA2-256 length.  Attempting to crack using hashcat is unsuccessful, we can however try an online dehashing tool [md5hashing.net](https://md5hashing.net).  We get the plaintext value:
  
~~~
4dM1n
~~~

As detailed in the challenge, we need to submit the SHA1 hash of this as the answer.
  
~~~
a7c9d5a37201c08c5b7b156173bea5ec2063edf9
~~~

</details>

### Answer

<details>

<summary markdown="span">Answer</summary>

~~~
a7c9d5a37201c08c5b7b156173bea5ec2063edf9
~~~

</details>

---

### [Cryptanalysis](#contents) | [Root-Me](./rootme.md) | [Home](./index.md)

---

## Shift Cipher

- Author: m31z0nyx
- Date: 16 February 2011
- Points: 10
- Level: 1

### Statement

Index : keep on turning.

### Attachments

1. [ch7.bin](http://challenge01.root-me.org/cryptanalyse/ch7/ch7.bin).

### Solutions

<details>

<summary markdown="span">Solution 1</summary>

We are given a data file ch7.bin:
 
~~~shell
$ file ch7.bin 
ch7.bin: data
~~~

We can import this in Python and examine, it appears to be a binary file of Bytes which conform to the ASCII table.  We can write a shift cipher for ASCII that identified viable ASCII character solutions:

~~~py
filename = "ch7.bin"
file = open(filename,"r+b")
data_bin = file.read()[:-1]
file.close()
import string

alphabet = string.ascii_letters + string.digits + string.punctuation + " \n"

idx = 0
for i in range(128):
    data_ascii = "" 
    newbin = []
    for j in range(len(data_bin)):
        newbin.append((data_bin[j]+1)%128)
    data_bin = bytearray(newbin)
    idx += 1
    try:
        data_ascii = data_bin.decode()
        if set(data_ascii).issubset(alphabet):
            print("Shift + {} ASCII code found: {}".format(idx,data_ascii))
    except:
        continue
~~~

This provides the solution

</details>

### Answer

<details>

<summary markdown="span">Answer</summary>

~~~
Yolaihu
~~~

</details>

---

### [Cryptanalysis](#contents) | [Root-Me](./rootme.md) | [Home](./index.md)

---

## CISCO Salted Password

- Author: Tidusrose
- Date: 13 July 2021
- Points: 10
- Level: 1

### Statement

Your company’s network administrator forgot his administration passwords. He does however have a backup of his startup-config file. Use it to recover his passwords!

The flag is the concatenation of the "enable" and "administrator" passwords.

Good luck!

### Attachments

1. [ch53.txt](http://challenge01.root-me.org/cryptanalyse/ch53/ch53.txt).

### Solutions

<details>

<summary markdown="span">Solution 1</summary>

We are given a cisco config file:

~~~
{!
version 15.1
no service timestamps log datetime msec
no service timestamps debug datetime msec
no service password-encryption
!
hostname R1
!
enable secret 5 $1$mERr$A419.HL58lq743wXS4kSM1
!
ip cef
no ipv6 cef
!
username administrator secret 5 $1$mERr$yhf7f2RnC74CxKANvoekD.
!
license udi pid CISCO2911/K9 sn FTX1524V4VG-
!
no ip domain-lookup
!
spanning-tree mode pvst
!
interface GigabitEthernet0/0
 ip address 10.0.0.254 255.255.255.0
 no ip proxy-arp
 duplex auto
 speed auto
!
interface GigabitEthernet0/1
 ip address 11.0.0.1 255.255.255.252
 no ip proxy-arp
 duplex auto
 speed auto
!
interface GigabitEthernet0/2
 no ip address
 duplex auto
 speed auto
 shutdown
!
interface Vlan1
 no ip address
 shutdown
!
router bgp 1
 bgp router-id 1.1.1.1
 bgp log-neighbor-changes
 no synchronization
 neighbor 11.0.0.2 remote-as 2
 network 10.0.0.0 mask 255.255.255.0
!
ip classless
!
ip flow-export version 9
!
no cdp run
!
line con 0
 login local
!
line aux 0
!
line vty 0 4
 login
!
!
!
}
~~~

We can see two password hashes that we require to find for this challenge:

~~~
enable secret 5 $1$mERr$A419.HL58lq743wXS4kSM1
username administrator secret 5 $1$mERr$yhf7f2RnC74CxKANvoekD.
~~~

We can use hashcat to find these with the rockyou.txt wordlist:

~~~shell
$ hashcat -m 500 -a 0 -o cracked.txt hash rockyou.txt
~~~

This produces the file cracked.txt with:

~~~
$1$mERr$A419.HL58lq743wXS4kSM1:dolphinsforever
$1$mERr$yhf7f2RnC74CxKANvoekD.:P@ssw0rd!1
~~~

We can concatenate and we have the solution.

</details>

### Answer

<details>

<summary markdown="span">Answer</summary>

~~~
dolphinsforeverP@ssw0rd!1
~~~

</details>

---

### [Cryptanalysis](#contents) | [Root-Me](./rootme.md) | [Home](./index.md)

---

## Pixel Madness

- Author: Ryscrow
- Date: 3 February 2011
- Points: 15
- Level: 2

### Statement

Decrypt the code.

Clue :
0 = #FFFFFF
1 = #000000

Submit password in CAPITAL LETTERS.

### Attachments

1. [ch4.txt](http://challenge01.root-me.org/cryptanalyse/ch4/ch4.txt).

### Solutions

<details>

<summary markdown="span">Solution 1</summary>

We are given a series of numbers that are not hex.  Treating each number pair as a small calculation, we can generate a series of binary strings that can be used to generate a pixel array as per the challenge statement.  This can be used to generate a png in Python:

~~~py
from PIL import Image

PIXELSTR = ["0x3+1x1+0x1+0x1+0x7+1x2+0x15+1x1+0x8+1x1+0x8+1x1+0x1+1x1+0x1+1x1+0x1+1x1+0x1+1x1+0x3+1x1+0x1+1x1+0x3+1x1+0x1+1x4+0x2+1x1+0x25",
    "0x2+1x1+0x4+1x1+0x4+1x3+0x1+1x2+0x2+1x8+0x11+1x4+0x1+1x3+0x6+1x2+0x4+1x1+0x4+1x2+0x7+1x4+0x4+1x2+0x7+1x2+0x3+1x2+0x3",
    "0x3+1x1+0x2+1x1+0x2+1x1+0x11+1x2+0x2+1x3+0x7+1x1+0x4+1x2+0x2+1x2+0x7+1x1+0x6+1x1+0x2+1x1+0x4+1x3+0x1+1x1+0x4+1x1+0x2+1x1+0x2+1x1+0x3+1x1+0x2+1x3+0x2+1x2+0x3",
    "1x1+0x2+1x1+0x4+1x1+0x2+1x1+0x1+1x1+0x2+1x1+0x2+1x1+0x1+1x2+0x2+1x2+0x1+1x2+0x3+1x1+0x3+1x1+0x2+1x2+0x1+1x3+0x3+1x1+0x2+1x1+0x4+1x2+0x1+1x1+0x4+1x1+0x3+1x2+0x12+1x2+0x1+1x1+0x3+1x7+0x3",
    "0x3+1x1+0x7+1x1+0x1+1x1+0x4+1x1+0x2+1x2+0x2+1x2+0x4+1x1+0x2+1x1+0x1+1x2+0x1+1x8+0x1+1x1+0x4+1x1+0x5+1x1+0x3+1x2+0x2+1x1+0x1+1x2+0x2+1x1+0x3+1x2+0x9+1x1+0x1+1x2+0x2+1x3+0x2+1x1",
    "0x7+1x1+0x4+1x1+0x4+1x1+0x1+1x1+0x1+1x7+0x3+1x1+0x1+1x2+0x3+1x1+0x1+1x6+0x1+1x1+0x3+1x1+0x2+1x1+0x14+1x2+0x8+1x1+0x10+1x2+0x3+1x2+0x1+1x1+0x1",
    "0x6+1x5+0x4+1x1+0x7+1x1+0x2+1x1+0x3+1x2+0x4+1x1+0x8+1x1+0x3+1x2+0x1+1x2+0x3+1x1+0x8+1x1+0x2+1x2+0x1+1x1+0x3+1x7+0x5+1x2+0x2+1x1+0x2+1x2+0x3",
    "0x1+1x1+0x2+1x1+0x1+1x2+0x5+1x1+0x6+1x2+0x3+1x1+0x2+1x1+0x1+1x2+0x20+1x8+0x1+1x1+0x1+1x1+0x4+1x2+0x3+1x1+0x2+1x2+0x3+1x2+0x7+1x2+0x3+1x2+0x4",
    "0x2+1x1+0x3+1x5+0x5+1x2+0x7+1x1+0x4+1x2+0x2+1x1+0x2+1x2+0x1+1x1+0x3+1x1+0x6+1x2+0x2+1x2+0x3+1x2+0x2+1x3+0x1+1x1+0x6+1x3+0x3+1x5+0x3+1x1+0x4+1x1+0x5",
    "0x4+1x2+0x3+1x2+0x3+1x1+0x5+1x2+0x2+1x1+0x1+1x1+0x1+1x1+0x1+1x2+0x9+1x1+0x3+1x1+0x2+1x1+0x1+1x1+0x2+1x1+0x1+1x2+0x2+1x1+0x2+1x1+0x1+1x1+0x4+1x3+0x1+1x1+0x2+1x2+0x3+1x2+0x3+1x1+0x5+1x1+0x4+1x1+0x2",
    "0x6+1x5+0x4+1x1+0x1+1x1+0x2+1x2+0x6+1x1+0x1+1x7+0x4+1x3+0x3+1x1+0x4+1x1+0x2+1x2+0x4+1x1+0x6+1x1+0x6+1x8+0x3+1x1+0x5+1x1+0x7",
    "0x2+1x1+0x3+1x6+0x4+1x1+0x1+1x3+0x4+1x1+0x2+1x2+0x4+1x1+0x5+1x1+0x2+1x1+0x3+1x2+0x3+1x1+0x2+1x3+0x1+1x1+0x2+1x2+0x3+1x3+0x2+1x3+0x9+1x1+0x4+1x2+0x7+1x2"]

def pixel_array(x):
    if int(x) == 0:
        pa = ((255, 255, 255))
    else:
        pa = ((0, 0, 0))
    return pa

binarray = []
pixarray = []

for i in range(len(PIXELSTR)):
    binrow = ""
    pixelrow = PIXELSTR[i].split("+")
    for j in range(len(pixelrow)):
        pixels = pixelrow[j].split("x")
        pixel1 = pixels[0]
        pixel2 = pixels[1]
        pixel = pixel1*int(pixel2)
        binrow += str(pixel)
    binarray.append(binrow)
    
imgwidth = len(binrow)
imgheight = len(binarray)

for row in binarray:
    for pix in row:
        pixarray.append(pixel_array(pix))
        
solution = Image.new("RGB",(imgwidth,imgheight+1), "white")
solution.putdata(pixarray)
solution.save('out.png')
~~~

This produces a small png from which we can see the solution.

</details>

### Answer

<details>

<summary markdown="span">Answer</summary>

~~~
SOLUTION
~~~

</details>

---

### [Cryptanalysis](#contents) | [Root-Me](./rootme.md) | [Home](./index.md)

---

## ELF64 PID encryption

- Author: Lu33Y
- Date: 08 February 2012
- Points: 15
- Level: 2

### Statement

<details>

<summary markdown="span">Source Code</summary>

~~~c
#include <stdio.h>
#include <stdlib.h>
#include <string.h>
#include <crypt.h>
#include <sys/types.h>
#include <unistd.h>
 
int main (int argc, char *argv[]) {
    char pid[16];
    char *args[] = { "/bin/bash", "-p", 0 };
 
    snprintf(pid, sizeof(pid), "%i", getpid());
    if (argc != 2)
        return 0;
 
    printf("%s=%s",argv[1], crypt(pid, "$1$awesome"));
 
    if (strcmp(argv[1], crypt(pid, "$1$awesome")) == 0) {
        printf("WIN!\n");
        execve(args[0], &args[0], NULL);
 
    } else {
        printf("Fail... :/\n");
    }
    return 0;
}
~~~

</details>

### Connection Information

- Host: challenge01.root-me.org
- Protocol: SSH
- Port: 2221
- SSH Access: ssh -p 2221 cryptanalyse-ch21@challenge01.root-me.org
- Username: cryptanalyse-ch21
- Password: cryptanalyse-ch21

### Solutions

<details>

<summary markdown="span">Solution 1</summary>

Reviewing the source code, we can see the user input is compared to the encrypted process id salted with "$1$awesome".  We can run this binary and record the hash:

~~~shell
cryptanalyse-ch21@challenge01:~$ ./ch21 1
1=$1$awesome$VY.ZX3OokFeKMv6unhPzB.Fail... :/
~~~

This gives us:

~~~
id  : 1
salt: awesome
enc : VY.ZX3OokFeKMv6unhPzB.
~~~

As detailed in the [crypt.h man page](https://man7.org/linux/man-pages/man3/crypt.3.html), the id defines the algorithm (MD5 in this case).  We can write a decrypt function:

~~~c
#include <stdio.h>
#include <stdlib.h>
#include <string.h>
#include <crypt.h>
#include <sys/types.h>
#include <unistd.h>
 
int main()
{
  char pid[16];
  snprintf(pid, sizeof(pid), "%i", getpid());
  execl("/challenge/cryptanalyse/ch21/ch21", "ch21", crypt(pid, "$1$awesome"), NULL);
}
~~~

This can be saved as /tmp/ch21decrypt.c and compiled using:

~~~shell
cryptanalyse-ch21@challenge01:/tmp$ gcc ch21decrypt.c -o ch21decrypt -lcrypt
cryptanalyse-ch21@challenge01:/tmp$ chmod +x ch21decrypt
~~~

Running the script gives us access to bash, from which we can retrieve the flag:

~~~shell
cryptanalyse-ch21@challenge01:/tmp$ ./ch21decrypt
$1$awesome$DdGvBy31TxzSQB83u6VOc.=$1$awesome$DdGvBy31TxzSQB83u6VOc.WIN!
bash-5.0$ cat ~/.passwd
-/q2/a9d6e31D
~~~

</details>

### Answer

<details>

<summary markdown="span">Answer</summary>

~~~
-/q2/a9d6e31D
~~~

</details>

---

### [Cryptanalysis](#contents) | [Root-Me](./rootme.md) | [Home](./index.md)

---

## File PKZIP

- Author: g0uZ
- Date: 30 August 2010
- Points: 15
- Level: 2

### Statement

None

### Links

1. [ch5.zip](http://challenge01.root-me.org/cryptanalyse/ch5/ch5.zip).

### Resources

1. [Cracking PKZIP file password](https://repository.root-me.org/Cryptographie/EN%20-%20Cracking%20PKZIP%20file's%20password.pdf).

### Solutions

<details>

<summary markdown="span">Solution</summary>

The challenge file can be retrieved and reviewed:

~~~shell
$ wget http://challenge01.root-me.org/cryptanalyse/ch5/ch5.zip
$ file ch5.zip 
ch5.zip: Zip archive data, at least v2.0 to extract
~~~

Attempting to unzip the archive returns a prompt for the password of the readme.txt file contained:

~~~shell
$ unzip ch5.zip 
Archive:  ch5.zip
[ch5.zip] readme.txt password: 
   skipping: readme.txt              incorrect password
~~~

The file hash can be extracted using zip2john:

~~~shell
$ john-the-ripper.zip2john ch5.zip > ch5.hash
Created directory: /home/derek/snap/john-the-ripper/459/.john
ver 2.0 efh 5455 efh 7855 ch5.zip/readme.txt PKZIP Encr: 2b chk, TS_chk, cmplen=99, decmplen=111, crc=EE166206

$ cat ch5.hash 
ch5.zip/readme.txt:$pkzip2$1*2*2*0*63*6f*ee166206*0*3d*8*63*ee16*005c*4cd0f9313784d20fdf0eb52e155682a0444ecadc04d2b2e34778b8aeec2dc025e79e6d9b2f6b3e6ee1c9269a50ff858f75f90c16f8cbe1980fd46747f1b2dbd47b92199a57b3c52f9ffeeb50bcdad0e38c88e3308051f32fde0158941432ab2e3b8c1e*$/pkzip2$:readme.txt:ch5.zip::ch5.zip
~~~

This shows the hash uses pkzip2.  This hashfile can be used directly with john to retrieve the password:

~~~shell
$ john ch5.hash  --show
ch5.zip/readme.txt:14535:readme.txt:ch5.zip::ch5.zip
~~~

The password is 14535 unzipping, the readme.txt file can be inflated and read with cat.


</details>

### Answer

<details>

<summary markdown="span">Answer</summary>

~~~
14535
~~~

</details>

---

### [Cryptanalysis](#contents) | [Root-Me](./rootme.md) | [Home](./index.md)

---

## Monoalphabetic substitution Caesar

- Author: Arod
- Date: 22 October 2011
- Points: 15
- Level: 2

### Statement

We just caught the messenger of the Emperor. He transmitted a coded message to his son. This could be an important message. You’ve to decrypt it ! To validate, you must enter the concatenation of the first letters of each line followed by the concatenation of the last letters of each line (for example : tfhqdlhfpkmeokgq).

### Links

1. [ch10.txt](http://challenge01.root-me.org/cryptanalyse/ch10/ch10.txt).

### Solutions

<details>

<summary markdown="span">Solution</summary>

The cipher can be brute-force solved using [and online shift cipher tool](https://www.dcode.fr/shift-cipher).  This gives us the most likely solution:

~~~
un deux trois
j'irai dans les bois
quatre cinq six
cueillir des cerises
sept huit neuf
dans un panier neuf
dix onze douze
elles seront toutes rouges
~~~

We can build the password as detailed in the challenge statement.

</details>

### Answer

<details>

<summary markdown="span">Answer</summary>

~~~
ujqcsddessxsffes
~~~

</details>

---

### [Cryptanalysis](#contents) | [Root-Me](./rootme.md) | [Home](./index.md)

---

## Known plaintext XOR

- Author: Ryscrow
- Date: 03 February 2011
- Points: 15
- Level: 2

### Statement

This BMP picture was mistakenly encrypted. Can you recover it ?

### Links

1. [ch3.bmp](http://challenge01.root-me.org/cryptanalyse/ch3/ch3.bmp).

### Solutions

<details>

<summary markdown="span">Solution</summary>

The bitmap binary has been manipulated by what appears to be XOR.  Reviewing the header in hex, the incorrect header bytes can be seen:

~~~
24 2C 9A E3 62 6E 66 61 6C 6C 53 6E 66 61 44 6C...
~~~

The standard bmp header can be found [online](https://en.wikipedia.org/wiki/BMP_file_format).  With this the correct Byte values can be identified:

~~~
42 4D F6 8F 07 00 (00) (00) (00) (00) (00) (00) ...
~~~

The bytes marked (00) are likely to be 00 but may be different dependent on the application that generated the original bitmap.  Using this we can XOR the bytes to identify the key:

~~~
66 61 6C 6C 65 6E 66 61 6C 6C 53 6E 66 61 44 6C...
~~~

It would appear that the key is simply: 66 61 6C 6C 65 6E.  The file can be opened in python, manipulated and written to a new file:

~~~py
file = open("ch3.bmp",'rb')
filebytes = bytearray(file.read())
file.close()

keybytes = bytearray([0x66, 0x61, 0x6C, 0x6c, 0x65, 0x6e])

newbytes = bytearray([])

for i in range(len(filebytes)):
    cb = filebytes[i]
    kb = keybytes[i%len(keybytes)]
    newbytes.append(cb^kb)

newfile = open("ch3_fixed.bmp","wb")
newfile.write(newbytes)
~~~

The new bitmap has the password.

</details>

### Answer

<details>

<summary markdown="span">Answer</summary>

~~~
ICONOCLASTE
~~~

</details>

---

### [Cryptanalysis](#contents) | [Root-Me](./rootme.md) | [Home](./index.md)

---

## File Insecure storage 1

- Author: g0uZ
- Date: 6 February 2012
- Points: 20
- Level: 2

### Statement

Retrieve the user’s password.

### Links

1. [ch20.tgz](http://challenge01.root-me.org/cryptanalyse/ch20/ch20.tgz).

### Solutions

<details>

<summary markdown="span">Solution</summary>

Extracting the tgz archive, we find a firefox profile.  Using dumpzilla, we can extract the password:

~~~shell
$ python dumpzilla.py ffdir/.mozilla/firefox/o0s0xxhl.default/ --Passwords
~~~

</details>

### Answer

<details>

<summary markdown="span">Answer</summary>

~~~
F1rstP4sSw0rD
~~~

</details>

---

### [Cryptanalysis](#contents) | [Root-Me](./rootme.md) | [Home](./index.md)

---

## Polyalphabetic substitution Vigenere

- Author: Arod
- Date: 26 October 2011
- Points: 20
- Level: 2

### Statement

We need your expert opinion on this document. This is an old letter and it appears that it is important for the pirates that we are searching for. Your mission is to decipher the text and give us the full name of the author (example : "John Doe").

### Links

1. [ch11.txt](http://challenge01.root-me.org/cryptanalyse/ch11/ch11.txt).

### Solutions

<details>

<summary markdown="span">Solution</summary>

The text file contains a vignere ciphertext:

~~~
Moi Tepdsi Fhrujrlhf

Nu egxex g'vla jmmg ifvgkvq ehcclkk'lgm, p'xgk ihvfshm rrgz pqw whiighyj. "Wptbutsi: Gr nwccxzgqrg tfixai bshk qibti urshfdtamcyr,
"Tfixzxmxvhb u'nu 'lmgxxf' riyie pr iwitaesi q'nbv uhrcyr"...

Loktuie kblgvl, asgw yxg dxtie.

Qnbg rold hshl, rrgz zaxex djrjlapbzwv xu xdsvl dzxji qx ihhix wvajve
hvvoragethzjbi pi 1950, hg xfny tqrfx o ixnedhrk zv fvrpi qxfiblvq prl mvne h'gr utqbxy? 
Rq zbng vmlw hshl xrfhme hrfoewl gq uhb z'rohmf jnbh rzpv, cyrezvl msdgrl z'rohmqrg fcuxsi?
Vi fnwj nu lmgxxf, vgavqd qtbj fvr ysaws...
Cx tmqr rlh lg tszhr jiz vvqyiavs rolg x'iphzv... Cl wgmf izll hwfypbslq xyq pn izlihvf hrl olmyie iayoemz, pqw phbexymqw dn'wcl t'ebtexbexux yi ytgjxux...

Vi fnwj tb gapyxuv hb eg plvsv. C'hm qgbnhv elw bvbysjllydw rqdcbxyqv chii eh ugmaswvfl jamf vcdflrf vrwizkl yzi skotmpsz. 
Nr e'oz vvqbvvl. "Bfg Tqq Hhuczl, qi zi cxio ihw ysamfvk tsz xetjrbs. Nq p'nb trba hmrf fo kxai"
Eegtbv zvweif. Bz c't jidxnbbvflrf gbiwv. Mvye prl avflw.

V'ev yozm brq hrvclolvfi nnxfnyh'tyv. C'oz mysgzr nb fkkmzegxii.
Taxqrql iex tmzygx, q'vla gasy. Vo wtpx oi dns ax cigb. Fb ço wtpx grr xfixbv, o'ifm drkji cyr cs dx zyuw ceoeml.
Tmw ctftx xy'up ax a'rbti bef...
Gw gtygq uh'bz jx zizx zxbrvl tmv zhw...
Eb wedgr ji'ze wizwr jiv cl wgmf iskba jupbnl...
Eb wedgr ji'ze u'euqr ioj xuwqmtgsi xa ug'my gs uxcvmmg ioj xavq pn...
Loktuie kblgvl. Asgx px el'bs jmmg v'sjm qsgie. Mcll sie qrfsj.

Xa exsel q'vla edvvos... lgl tavgx g'vla sgzrkhv lbv xi zhbux...
Zi bvrvwgbaezx n mfrolve pn ewxgl xqprivfgpugi phadx ki x'lrkczgl hmrf esj olmzif w'ie tjgds, hgs zfwyxwvhb velgfvbgwhnl iex rgjfrli,
Ar exqyxygti hg fvybkq e y'bbthttqxrgqv jbsfmqbsegl... yz wrkjvny iex gkclol.

Zayf ocll yibigxn hnl rayf lcdflw fshl drklmxw... 
Bg o vml rayekw r eh tqxvms tnppxiex rv uvyrjr iclk iini n e'sthsi cyngr fg hzmmg yozf k'yz wgxob...
Elw rvnzavgaw pi iboewl ugi y'hb ehbw m pnbgjx lxmmrgh gkl-qmguxg vm zezw thûh.
Fg h ifi qhazgl tmv qxg jtkmcyrl cl bnravr ioi wlw mtnmvzjbie.
Prl gvnsw cyv tjrblrf hrl qyhzie e ahij twtdiawfv mysgzrksem kie iyxjvl csxsamozklw, yevl qvne gu wbgh thtqq hrl ufnaxqw qtbj el hqwfxfk.

V'lwf rbmfv fvrpi ztwemlrmrg... Es dhuhq hr e'scxjxdsa xh ux s'mzxrkfliaigv, yt pvtbxq hh uolw. Usgw hmwcbzszw hg gvkcmoi qxxr xemexngh, Jtuw belxf tx xyu tbnfitpx qxex pfg tedgux gz vl r'qxnbh gtz pm tehdiblxq hr zzfnaszw ckcwbaigvf, xh mhbw zshl ogilpqd pkwdbuixw.
Ahij xetxsehbj... xa zayf gcll htbiyxn tkpqurreg.
Ehbw dipasivoszw yt qfgueuwftbtx... lx hshl bfnz ebtresq vymymaxzj. 
Gvye ikbgkhuw eeal qfnsigv qx dvtb, wmrf gokbvrmpvms, jtuw pstfs ixsmsmrnl... vm csgw ahij twtqprs qibtmziyl.
Jfnz garfmflbzil hrl pffiie eghazjbie, zbng wbuezgrs zvl nyqvexg,
Mhbw zi cnbzlzil tnl zvl wefvbgg ux se yesbo rne vuguxg rovgmxf,
Ocll hweeflwexg if xebqyxg, zayf foebwyxim xh ehbw yiamsq xu iewnroem ki zshl trbyi ovbbfv jbi o'ifm dfny raxex dihwvq fvxb vmyi, qx ahij lvqyif xbthyi pif vfzfprqpf.

Hiz, cl wgmf nb tkpqurre. Afg jvuqr xgk vlpgm qx zr vbvusfbhv.
Fvr ovvfs vla gqphb rv cbkqv yxg xxuw bee vs hn'ppe trggvga if hvls, gtz wqpbg zvny ebtnksevl.
Qar pkwdx lwf hr ocll zydtnlgvk, xyqpdns tavwq uhx jfnz rq qr ioiwvrziexn atteuw.

Wx glbz yz lnvyvk, lx oipb sjm tsz qngwwxzxq.
Zbng ghbzqd nkfvmlv oig bbubcmpy, ztwj ovye rr iclold bef mcll usgw nkfvmlv...
Mtexg khbx, zshl gfftie xbng cxz qqqrl.
~~~

This can be solved using an online solver such as [guballa](https://www.guballa.de/vigenere-solver)

~~~
The Hacker Manifesto

Un autre s'est fait prendre aujourd'hui, c'est partout dans les journaux. "Scandale: Un adolescent arrete pour crime informatique,
"Arrestation d'un 'hacker' apres le piratage d'une banque"...

Satanes gosses, tous les memes.

Mais avez vous, dans votre psychologie en trois piece et votre profil
technocratique de 1950, un jour pense a regarder le monde derriere les yeux d'un hacker? 
Ne vous etes vous jamais demande ce qui l'avait fait agir, quelles forces l'avaient modele?
Je suis un hacker, entrez dans mon monde...
Le mien est un monde qui commence avec l'ecole... Je suis plus astucieux que la plupart des autres enfants, les conneries qu'ils m'apprennent me lassent...

Je suis au college ou au lycee. J'ai ecoute les professeurs expliquer pour la quinzieme fois comment reduire une fraction. 
Je l'ai compris. "Non Mme Dubois, je ne peux pas montrer mon travail. Je l'ai fait dans ma tete"
Satane gosses. Il l'a certainement copie. Tous les memes.

J'ai fait une decouverte aujourd'hui. J'ai trouve un ordinateur.
Attends une minute, c'est cool. Ca fait ce que je veux. Si ça fait une erreur, c'est parce que je me suis plante.
Pas parce qu'il ne m'aime pas...
Ni parce qu'il se sent menace par moi...
Ni parce qu'il pense que je suis petit filoux...
Ni parce qu'il n'aime pas enseigner et qu'il ne devrait pas etre la...
Satanes gosses. Tout ce qu'il fait c'est jouer. Tous les memes.

Et alors c'est arrive... une porte s'est ouverte sur le monde...
Se precipitant a travers la ligne telephonique comme de l'heroine dans les veines d'un accro, une impulsion electronique est envoyee,
On recherche un refuge a l'incompetence quotidienne... un serveur est trouve.

Vous vous repetez que nous sommes tous pareils... 
On a ete nourri a la petite cuillere de bouffe pour bebe a l'ecole quand on avait faim d'un steak...
Les fragments de viande que l'on nous a laisse etaient pre-maches et sans goût.
On a ete domine par des sadiques ou ignore par des apathiques.
Les seuls qui avaient des choses a nous apprendre trouverent des eleves volontaires, mais ceux ci sont comme des gouttes dans le dessert.

C'est notre monde maintenant... Le monde de l'electron et de l'interrupteur, la beaute du baud. Nous utilisons un service deja existant, Sans payer ce qui pourrait etre bon marche si ce n'etait pas la propriete de gloutons profiteurs, et vous nous appelez criminels.
Nous explorons... et vous nous appelez criminels.
Nous recherchons la connaissance... et vous nous appelez criminels. 
Nous existons sans couleur de peau, sans nationalite, sans dogme religieux... et vous nous appelez criminels.
Vous construisez des bombes atomiques, vous financez les guerres,
Vous ne punissez pas les patrons de la mafia aux riches avocats,
Vous assassinez et trichez, vous manipulez et nous mentez en essayant de nous faire croire que c'est pour notre propre bien etre, et nous sommes encore des criminels.

Oui, je suis un criminel. Mon crime est celui de la curiosite.
Mon crime est celui de juger les gens par ce qu'ils pensent et dise, pas selon leur apparence.
Mon crime est de vous surpasser, quelque chose que vous ne me pardonnerez jamais.

Je suis un hacker, et ceci est mon manifeste.
Vous pouvez arreter cet individu, mais vous ne pouvez pas tous nous arreter...
Apres tout, nous sommes tous les memes.
~~~

The key is thementor.  Translating to English we get:

~~~
The Hacker Manifesto

Another one got caught today, it's all over the papers. "Scandal: A teenager arrested for computer crime,
“Hacker arrested after bank hack”...

Damn kids, all the same.

But have you, in your three-piece psychology and your profile
technocratic era of 1950, one day thought of looking at the world behind the eyes of a hacker?
Have you ever wondered what made him act, what forces shaped him?
I am a hacker, enter my world...
Mine is a world that starts with school... I'm smarter than most other kids, the bullshit they teach me tires me...

I am in college or high school. I listened to the teachers explain for the fifteenth time how to reduce a fraction.
I understood it. "No Mrs. Dubois, I can't show my work. I did it in my head"
Damn kids. He certainly copied it. All The same.

I made a discovery today. I found a computer.
Wait a minute, that's cool. It does what I want. If it makes an error, it's because I messed up.
Not because he doesn't love me...
Nor because he feels threatened by me...
Or because he thinks I'm a little trickster...
Or because he doesn't like to teach and he shouldn't be there...
Damn kids. All he does is play. All The same.

And then it happened... a door opened to the world...
Rushing through the phone line like heroin through an addict's veins, an electronic pulse is sent,
We are looking for a refuge from the daily incompetence... a waiter is found.

You tell yourself that we are all the same...
We were spoon-fed baby food at school when we were hungry for a steak...
The meat fragments we were left with were pre-chewed and tasteless.
We have been dominated by sadists or ignored by apathetic people.
The only ones who had things to teach us found volunteer students, but these are like drops in the dessert.

It's our world now... The world of electrons and switches, the beauty of baud. We are using an existing service, Without paying what might be cheap if it wasn't owned by profiteering gluttons, and you call us criminals.
We explore... and you call us criminals.
We seek knowledge... and you call us criminals.
We exist without skin color, without nationality, without religious dogma... and you call us criminals.
You build atomic bombs, you fund wars,
You don't punish mafia bosses to wealthy lawyers,
You murder and cheat, you manipulate and lie to us trying to make us believe it is for our own good, and we are still criminals.

Yes, I am a criminal. My crime is that of curiosity.
My crime is to judge people by what they think and say, not by how they look.
My crime is to outdo you, something you will never forgive me for.

I'm a hacker, and this is my manifesto.
You can stop this individual, but you can't stop all of us...
After all, we are all the same. 
More about this source text
Source text required for additional translation information
Send feedback
Side panels
~~~

A quick google shows this is the manifesto of Loyd Blankenship, a.k.a. "The Mentor".

</details>

### Answer

<details>

<summary markdown="span">Answer</summary>

~~~
Loyd Blankenship
~~~

</details>

---

### [Cryptanalysis](#contents) | [Root-Me](./rootme.md) | [Home](./index.md)

---

## System Android Lock Pattern

- Author: Silentd
- Date: 23 December 2012
- Points: 20
- Level: 2

### Statement

Having doubts about the loyalty of your wife, you’ve decided to read SMS, mail, etc in her smarpthone. Unfortunately it is locked by schema. In spite you still manage to retrieve system files.

You need to find this test scheme to unlock smartphone.

NB : validation password is a number (archive sha256 is 525daa911d4dddb7f3f4b4ec24bff594c4a1994b2e9558ee10329144a6657f98)

### Links

1. [ch17.tbz](http://challenge01.root-me.org/cryptanalyse/ch17/ch17.tbz2).

### Solutions

<details>

<summary markdown="span">Solution</summary>

Decompiling, we can find the gesture.key in android/data/system

~~~shell
/android/data/system$ ls
batterystats.bin      dropbox      gesture.key  locksettings.db      locksettings.db-wal  packages.xml         sync      uiderrors.txt  users
called_pre_boots.dat  entropy.dat  inputmethod  locksettings.db-shm  packages.list        registered_services  throttle  usagestats
~~~

The key can be read in hex:

~~~shell
$ cat gesture.key | xxd -ps
2c3422d33fb9dd9cde87657408e48f4e635713cb
~~~

This can be cracked using hashlib in Python:

~~~py
import itertools
from hashlib import sha1
from binascii import hexlify

def sha1_crack(gesture_hash):
    gesture_chars = ["\x00","\x01","\x02","\x03","\x04","\x05","\x06","\x07","\x08","\x09"]
    print ("hash = {}".format(gesture_hash))
    for i in range(2, 10):
        permutations = itertools.permutations(gesture_chars, i)
        perm_list = map(''.join, permutations)
        for j in perm_list:
            sha_hash = sha1(j.encode('utf-8')).hexdigest()
            if gesture_hash == sha_hash:
                p = hexlify(j.encode('utf-8')).decode('utf-8')
                pt = ''.join([p[o] for o in range(1, len(p), 2)])
                print ("gesture = {}".format(pt))

if __name__ == "__main__":
    hashed = "2c3422d33fb9dd9cde87657408e48f4e635713cb"
    sha1_crack(hashed)
~~~

</details>

### Answer

<details>

<summary markdown="span">Answer</summary>

~~~
145263780
~~~

</details>

---

### [Cryptanalysis](#contents) | [Root-Me](./rootme.md) | [Home](./index.md)

---

## Transposition Rail Fence

- Author: YellowS4
- Date: 6 April 2014
- Points: 20
- Level: 2

### Statement

USA, American Civil War, August 3, 1862. You are on patrol around the camp when you see an enemy rider. Once you intercepted him, you discover that he carries a message but nobody at the camp manages to uncipher it. You are the only hope to find the hidden information. It could be crucial !

### Links

1. [ch19.txt](http://challenge01.root-me.org/cryptanalyse/ch19/ch19.txt).

### Solutions

<details>

<summary markdown="span">Solution</summary>

The ciphertext is described as a rail fence cipher:

~~~
Wnb.r.ietoeh Fo"lKutrts"znl cc hi ee ekOtggsnkidy hini cna neea civo lh
~~~

Using an online [rail-fence transposition cipher solver](https://www.boxentriq.com/code-breaking/rail-fence-cipher), we can iterate through and find the solution with rails=8 and offset=0:

~~~
Will invade Kentucky on October the eighth. signal is "Frozen chicken".
~~~

</details>

### Answer

<details>

<summary markdown="span">Answer</summary>

~~~
Frozen chicken
~~~

</details>

---

### [Cryptanalysis](#contents) | [Root-Me](./rootme.md) | [Home](./index.md)

---

## RSA Factorisation

- Author: HacKSpider
- Date: 12 September 2010
- Points: 25
- Level: 3

### Statement

The validation password was encrypted using this public key.

ciphertext :

~~~
e8oQDihsmkvjT3sZe+EE8lwNvBEsFegYF6+OOFOiR6gMtMZxxba/bIgLUD8pV3yEf0gOOfHuB5bC3vQmo7bE4PcIKfpFGZBA
~~~

### Links

1. [ch6.zip](http://challenge01.root-me.org/cryptanalyse/ch6/ch6.zip).

### Resources

1. [Cryptanalysis of short RSA secret exponents](https://repository.root-me.org/Cryptographie/Asym%C3%A9trique/EN%20-%20Cryptanalysis%20of%20short%20RSA%20secret%20exponents.pdf).
2. [DROWN: Breaking TLS using SSLv2](https://repository.root-me.org/Cryptographie/Asym%C3%A9trique/EN%20-%20DROWN:%20Breaking%20TLS%20using%20SSLv2.pdf).
3. [Chosen siphertext attacks against protocols based on the RSA encryption standard](https://repository.root-me.org/Cryptographie/Asym%C3%A9trique/EN%20-%20Chosen%20ciphertext%20attacks%20against%20protocols%20based%20on%20the%20RSA%20encryption%20standard%20-%20Daniel%20Bleichenbacher.pdf).
4. [Continued Fractions - RSA](https://repository.root-me.org/Cryptographie/Asym%C3%A9trique/EN%20-%20Continued%20Fractions%20-%20RSA.pdf).

### Solutions

<details>

<summary markdown="span">Solution</summary>

Extracting the archive, a public key file is retrieved, pubkey.pem.  Using openssl, the modulus and exponent can be extracted:

~~~shell
$ openssl rsa -pubin -inform PEM -text -noout < pubkey.pem 
RSA Public-Key: (576 bit)
Modulus:
    00:c2:cb:b2:4f:db:f9:23:b6:12:68:e3:f1:1a:38:
    96:de:45:74:b3:ba:58:73:0c:bd:65:29:38:86:4e:
    22:23:ee:eb:70:4a:17:cf:d0:8d:16:b4:68:91:a6:
    14:74:75:99:39:c6:e4:9a:af:e7:f2:59:55:48:c7:
    4c:1d:7f:b8:d2:4c:d1:5c:b2:3b:4c:d0:a3
Exponent: 65537 (0x10001)
~~~

This is a 576 bit RSA for which the primes p and q can be found [online](https://mathworld.wolfram.com/news/2003-12-05/rsa/).  Using Python a simple solver can be written:

~~~py
from Crypto.PublicKey import RSA
from Crypto.Util.number import inverse
import base64 as b64
import binascii

ct_b64 = "e8oQDihsmkvjT3sZe+EE8lwNvBEsFegYF6+OOFOiR6gMtMZxxba/bIgLUD8pV3yEf0gOOfHuB5bC3vQmo7bE4PcIKfpFGZBA"

asciikey = """-----BEGIN PUBLIC KEY-----
MGQwDQYJKoZIhvcNAQEBBQADUwAwUAJJAMLLsk/b+SO2Emjj8Ro4lt5FdLO6WHMM
vWUpOIZOIiPu63BKF8/QjRa0aJGmFHR1mTnG5Jqv5/JZVUjHTB1/uNJM0VyyO0zQ
owIDAQAB
-----END PUBLIC KEY-----"""

n = int(RSA.importKey(asciikey).n)
e = int(65537)

# found online at https://mathworld.wolfram.com/news/2003-12-05/rsa/:
p = 398075086424064937397125500550386491199064362342526708406385189575946388957261768583317
q = 472772146107435302536223071973048224632914695302097116459852171130520711256363590397527

m = (p-1)*(q-1)

d = inverse(e,m)

ct_B = b64.b64decode(ct_b64.encode())
ct_dec = int(binascii.hexlify(ct_B),16)

pt_dec = pow(ct_dec,d,n)
pt_hex = hex(pt_dec)[2:].strip("L")
if len(pt_hex)%2!=0:
    pt_hex = "0"+pt_hex

pt_B = binascii.unhexlify(pt_hex)
pt_ascii = ""

for char in pt_B:
    if (char >31) and (char<127):
        pt_ascii += chr(char)
    else:
        pt_ascii += " "

print(pt_ascii)
~~~

This returns a long string including the original PT message.

</details>

### Answer

<details>

<summary markdown="span">Answer</summary>

~~~
up2l6DnaIhZgxA
~~~

</details>

---

### [Cryptanalysis](#contents) | [Root-Me](./rootme.md) | [Home](./index.md)

---

## Monoalphabetic substitution Polybe

- Author: koma
- Date: 6 December 2011
- Points: 25
- Level: 3

### Statement

A strange person contact you after purchasing a parchment of weird origin ... He count on your quick wit to decrypt this message ! You will need to deploy all your cryptanalyse’s faculties.
 
### Links

1. [ch12.txt](http://challenge01.root-me.org/cryptanalyse/ch12/ch12.txt).

### Resources

None.

### Solutions

<details>

<summary markdown="span">Solution</summary>

Downloading the ciphertext, we see a strange code:

~~~
b3a3d1 c2b1e3d4d3d1 a4e5c5b1e3c2a3d1 b3a4b4e1e3b1a3d1 e3e5 b3a4b1e1d1 b2e5b4e3d2d4 d1a3b4c3c4a3d4a1
d1a4c4d2d3a3d1 b3a4d4d1d2d3a3b1a3d1 d1a3c4a4d4 c4a3d1 c4a4d2d1 d3a3 b3a3a1a1a3 d4e3a1e5b1a3 c1e5d2 d3a3a1b1e5d2a1
c1e5d2 b1e3e1e1a3c4c4a3 a1a4e5a1a3d1 b3b2a4d1a3d1 e3e5 d4a3e3d4a1 d3a4d4a1 a3c4c4a3 c4a3d1 e3 a1d2b1a3a3d1
d2c4d1 d1a4d4a1 c3d2a3d4 e2b1a3c4a3d1 b3a4b4b4a3d4a1 b1d2a3d4 d3 d2b4b4a4b1a1a3c4 a3e5a1d2c4 e1e5 d1a4b1a1d2b1
d3a3 d4a4d1 b4a4b1a1a3c4c4a3d1 b4e3d2d4d1  c4a3d1 d1a3e1a1 e2e3b4a3e5d1a3d1 b4a3b1c5a3d2c4c4a3d1 d3e5
b4a4d4d3a3 a3a1 b3a3 c1e5 e3 e1e5 c3e3a1d2b1 d3a3 e1c4e5d1 e1b1a4d3d2c2d2a3e5b5 a3d4b3a4b1a3 c4e3 c5e3d4d2a1a3
d3a3d1 e3c2a3d1 d1e5d2c5e3d4a1d1 a1a4e5a1 b3a3c4e3 e5d4 a2a4e5b1 a4d4 c4a3 c5a3b1b1e3 b3a4e5b3b2a3 e3e5 d4d2c5a3e3e5
d3e5 d1a4c4 a4e5d2 b1d2a3d4 d4 a3d1a1 e2e3d2a1 e1a4e5b1 d3e5b1a3b1 a1a4e5a2a4e5b1d1 e1b1a3d1c1e5a3
b1d2a3d4 e1a4e5b1 d3e5b1a3b1 c4a4d4c2a1a3b4e1d1 b3b2e3c1e5a3 b3b2a4d1a3 e3 d1a4d4 b3a4a1a3 e2b1e3c2d2c4a3 a3a1
d1d2 c4a3 b4a4d3a3 d3a3 d3a3d1a1b1e5b3a1d2a4d4 c5e3b1d2a3 e3e5 d3a3b4a3e5b1e3d4a1 a1a4e5a1 b3a3 c1e5d2
b3a4b4b4a3d4b3a3 d3a4d2a1 e2d2d4d2b1

c4 e5d4d2c5a3b1d1 e3e5d1d1d2 d1a3c4a4d4 c1e5a3c4c1e5a3d1e5d4d1 a3d1a1
b3a4d4d3e3b4d4a3 e3 e1a3b1d2b1 a3a1 b3a3 c3a3c4 a3d4d1a3b4c3c4a3 c1e5d2 a3b4c3b1e3d1d1a3 a1a4e5a1 b3a3
c1e5d2 a3d1a1 d3d2a3e5 b3a4b4b4a3 a1a4e5a1 b3a3 c1e5d2 a3d1a1 b2a4b4b4a3 e5d4 a2a4e5b1 d1 d2c4 a3d1a1
e1a3b1b4d2d1 d3a3 c4a3 b3b1a4d2b1a3 e5d4 a2a4e5b1 e2e3a1e3c4 c4a3 c5d2a3d4d3b1e3 d3d2d1d1a4e5d3b1a3 a3a1 b1a3e1c4a4d4c2a3b1
d3e3d4d1 c4e3 d4e5d2a1 d3e5 e1b1a3b4d2a3b1 b3b2e3a4d1 a4d1a4d4d1 b4e3d2d4a1a3d4e3d4a1 d4a4e5d1
c4e3b4a3d4a1a3b1 d1e5b1 d3a3d1 b4a4b1a1d1 d2d4d3d2c5d2d3e5a3c4c4a3d1  a4d1a4d4d1 c2a3b4d2b1 d1e5b1 c4e3 b3a3d4d3b1a3
d3a3 b3e3b1a1b2e3c2a3 d3a3 d4e5b4e3d4b3a3 d3a3 b3a4b1d2d4a1b2a3 d3a3 a1a4e5a1a3 c5d2c4c4a3 e1b1a3b3d2e1d2a1a3a3
a3d4b3a4b1a3 d3a3 e1c4e5d1 b2e3e5a1 d1 d2c4 d1a3 e1a3e5a1 c1e5e3d4d3 c4 e5d4d2c5a3b1d1 c1e5d2
d4 e3 e1e3d1 a4e5 a1a4b4c3a3b1 d3a4d2a1 e1a3b1d2b1 b3a4b4b4a3 a3c4c4a3d1  a4d1a4d4d1 d4a4e5d1 e1c4e3d2d4d3b1a3
c1e5a3 c4a3d1 d3a3d1a1d2d4d1 c1e5d2 b3a4d4d1a4b4b4a3b1a4d4a1 b3a3a1a1a3 b1e5d2d4a3 d3a4d4a1 c4e3 e1a3d4d1a3a3
e2e3d2a1 e2b1a3b4d2b1 d4a3 d4a4e5d1 e3d2a3d4a1 e1e3d1 d1a3e5c4d1 a3e1e3b1c2d4a3d1

c1e5a3c4 a3a1b1a3 e3d1d1a3a5 d1e5e1a3b1c3a3 e3d1d1a3a5 a3e2e2b1a3d4a3 d3e3d4d1 d1a3d1 e1b1a3a1a3d4a1d2a4d4d1
c5a4e5d3b1e3d2a1 d1a4e5d1 c4 a3b4e1d2b1a3 d3a3 b3a3a1a1a3 c4a4d2 d3a3 c4e3 d4e3a1e5b1a3 c1e5d2 b1e3b4a3d4a3
a1a4e5a1 e3 c4e3 b4a3b4a3 e2d2d4 c1e5 d2c4 d5 a3e5a1 a3b5b3a3e1a1d2a4d4 e1a4e5b1 c4e5d2 a3a1 c4a3d1
d1d2a3d4d1 a3a1 c1e5a3 d3e3d4d1 c4 d2d4a3c5d2a1e3c3c4a3 d4e3e5e2b1e3c2a3 d3e5 c2b1e3d4d3 a1a4e5a1 e5d4a3
d1a3e5c4a3 e2e3b4d2c4c4a3 e2e5a1 d1e3e5c5a3a3

b3 a3d1a1 d3a4d4b3 e5d4a3 e1e5d2d1d1e3d4a1a3 b3a4d4d1a4c4e3a1d2a4d4
d3a3 d1a4d4c2a3b1 c1e5 d2c4 d4a3 d4a4e5d1 e3b1b1d2c5a3 c1e5a3 b3a3 c1e5 a4d4a1 d1a4e5e2e2a3b1a1 e3c5e3d4a1 d4a4e5d1
a3a1 b3a3 c1e5a3 d1a4e5e2e2b1d2b1a4d4a1 e3e1b1a3d1 d4a4e5d1 a1a4e5d1 c4a3d1 b2a4b4b4a3d1 a3a1 c4e3 d4e3a1e5b1a3
b3a3 b4a3 d1a3b4c3c4a3 a3d4 b1a3d4d3e3d4a1 c2a3d4a3b1e3c4 c4a3 e1c4e5d1 b3b1e5a3c4 d3a3 d1a3d1 b4e3e5b5
e3 c5a4e5c4e5 c1e5a3 d1a4d4 e5d4d2c5a3b1d1e3c4d2a1a3 a3d4 e3d3a4e5b3a1 c4e3 b1d2c2e5a3e5b1

c5a4e5d1 a1b1a4e5c5a3b1a3a5 a3d4b3a4b1a3 e5d4 d1a3d4d1d2c3c4a3 e3c4c4a3c2a3b4a3d4a1 d3e3d4d1 c4e3 e1a3d4d1a3a3
c1e5a3 c5a4a1b1a3 d3a4e5c4a3e5b1 a3d1a1 d1e3d4d1 e2b1e5d2a1 e1a4e5b1 c4 a4c3a2a3a1 d3a3 c5a4d1 b1a3c2b1a3a1d1
b3a4b4b4a3 e1a4e5b1 c5a4e5d1 a3a1 c5a4e5d1 d4a3 c5a4e5d3b1a3a5 e1c4e5d1 e1b1a4c4a4d4c2a3b1 b3a3 c1e5d2
a3d1a1 d2d4e5a1d2c4a3 b3a3b1a1a3d1 d1d2 c4 e3e2e2c4d2b3a1d2a4d4 e1a3e5a1 a3d4 b1d2a3d4 d4a4e5d1 e1b1a4e2d2a1a3b1 a2a3
d4 b2a3d1d2a1a3 e1e3d1  a1a4e5a1 b3a3 c1e5a3 b4a3d1 b4e3c4b2a3e5b1d1 b4 a4d4a1 c4e3d2d1d1a3 d3a3 c4e3b1b4a3d1
a2a3 c4a3d1 b1a3e1e3d4d3b1e3d2 d1e5b1 c4a3 c5a4a1b1a3 a2 a3d4 b1a3a1b1a4e5c5a3b1e3d2 a3d4b3a4b1a3 d3e3d4d1 b3a3d1
d5a3e5b5 a3e1e5d2d1a3d1 e1e3b1 a1e3d4a1 d3a3 e1c4a3e5b1d1 c5a3b1d1a3d1 d1e5b1 b4a3d1 b4e3e5b5 d3a4b4a3d1a1d2c1e5a3d1
e1a4e5b1 e1a3e5 c1e5 d2c4d1 c5a4e5d1 e1e5d2d1d1a3d4a1 a3a1b1a3 d3a3 c1e5a3c4c1e5a3 e3c5e3d4a1e3c2a3

b1a3d3a4e5c3c4a4d4d1 e5d4d2d1d1a4d4d1 d4a4d1 e1c4e3d2d4a1a3d1 a2a3 e1b1a3d4d3d1 a3d4 b4e3d2d4 a1a4e5d1
c5a4d1 c2b1d2a3e2d1  a4 e2a4b1a1e5d4a3 d1d2 d2d4d2c1e5a3 e3e5 a2e5c2a3b4a3d4a1 d3a3 a1a4e5d1 a1e5
d1a3b4c3c4e3d2d1 a2e5d1c1e5 d2b3d2 e3c5a4d2b1 b1a3d1e1a3b3a1a3 e5d4 b2a4b4b4a3 c1e5d2 c2b1e3b3a3 e3 a1a3d1
e2e3c5a3e5b1d1 a3a1e3d2a1 a3d4 e3d1d1a3a5 b2e3e5a1a3 c5a3d4a3b1e3a1d2a4d4 e1a4e5b1 a2a4e5d2b1 d3 e5d4a3 d2b4b4e5d4d2a1a3
e1b1a3d1c1e5a3 d1e3d4d1 a3b5a3b4e1c4a3 e1a4e5b1 c5a4d2b1 d1a4d4 c3a4d4b2a3e5b1 e3 c4 e3c3b1d2
d3a3 c4 a3d4c5d2a3 b4e3d2d1 c5a4d2b3d2 c1e5a3 a1e5 c4e5d2 d2d4e2c4d2c2a3d1 c4e3 e1c4e5d1 c2b1e3d4d3a3 d3a4e5c4a3e5b1
c1e5a3 d1e3e5e2 c4e3 e1a3b1a1a3 d3a3 b3a3d1e3b1 d2c4 e1a4e5c5e3d2a1 b1a3d1d1a3d4a1d2b1 e3e1b1a3d1 e3c5a4d2b1
c3d2a3d4 d1a4d4d3a3 a1a4e5a1a3d1 c4a3d1 e1e3b1a1d2a3d1 d3a3 d1a4d4 e3b4a3 a1e5 e3d1 b3a4b4e1b1d2d1 c1e5 e5d4a3
d1a3e5c4a3 a3a1e3d2a1 a4e5c5a3b1a1a3 e3 a1a3d1 b3a4e5e1d1

b3e3b1 c1e5a3c4 e3e5a1b1a3 b4e3c4 e1a4e5c5e3d2d1 a1e5
c4e5d2 e2e3d2b1a3 c4e5d2 a3d4c4a3c5a3b1 d1a4d4 a4b1 a2e3b4e3d2d1 d2c4 d4 a3d4 e2e5a1 c4 a3d1b3c4e3c5a3 e3e5a2a4e5b1d3 b2e5d2
b4a3b4a3 c4a3 e1c4e5d1 c1e5 d2c4 e1a3e5a1 d2c4 c4 a3c4a4d2c2d4a3 d3a3 d1a4d4 b3a4a3e5b1 a3a1
d3e3d4d1 e5d4a3 d1d2 c2b1e3d4d3a3 e2e3b3d2c4d2a1a3 d3 a3d4 e3b3c1e5a3b1d2b1 d2c4 d4 d5 b3b2a3b1b3b2a3 e1e3d1 d3a3
e1c4e5d1 e1b1a3b3d2a3e5b5 e3c5e3d4a1e3c2a3 c1e5a3 d3a3 c4a3 b4a3e1b1d2d1a3b1

c4 e3e5b1e3d2d1a1e5 e1b1d2c5a3 d3a3 d1a3d1 e3b4d2d1 a1e5 c4a3 d1e3c5e3d2d1 d1d2 d3d2c2d4a3 d3 a3a1b1a3 e3d2b4a3 c1e5 d2c4 a3e5a1
e3d2d1a3b4a3d4a1 b1a3b4e1c4e3b3a3 b3a3e5b5 c1e5 d2c4 e3e5b1e3d2a1 e1a3b1d3e5d1 b3e3b1 d3a3 a1a4e5d1 c4a3d1 e1a3b1d1a4d4d4e3c2a3d1
e1e5d2d1d1e3d4a1d1 d3e3d4d1 c4e3 b4e3d2d1a4d4 d3e5 e1b1d2d4b3a3 a2a3 d4 e3d2 b3a4d4d4e5 c1e5a3
c4e5d2 d3a4d4a1 c4 e3b4d2a1d2a3 c2a3d4a3b1e3c4a3b4a3d4a1 d1d2 e5a1d2c4a3 a3a1e3d2a1 e1c4e5d1 b1a3b3b2a3b1b3b2a3a3
a3d4b3a4b1a3 e1a4e5b1 d1e3 d3a4e5b3a3e5b1

c4e5d2 e3e5b1e3d2d1a1e5 b1e3c5d2 c4 a3d1a1d2b4a3 e1e5c3c4d2c1e5a3
d2c4 d5 e1a4d1d1a3d3a3 d3a3d1 d3b1a4d2a1d1 a1b1a4e1 d1a4c4d2d3a3d1 e1a4e5b1 a3a1b1a3 a3c3b1e3d4c4a3d1 b4a3b4a3
e1e3b1 a1a4d2 e3e5b1e3d2d1a1e5 d3a3a1b1e5d2a1 d1e3 d1e3d4a1a3 b4e3d2d1 a1e5 b3a4d4d4e3d2d1d1e3d2d1 d1a4d4
e3b4a3 d4a4e5b1b1d2a3 a3a1 e1a4e5b1 d3d2b1a3 e1c4e5d1 d4a3a3 e3e5 d1a3d2d4 d3a3d1 a3a1e5d3a3d1 c4d2c3a3b1e3c4a3d1
b3a3a1a1a3 e3b4a3 c1e5 a3c4c4a3d1 a4d4a1 e3e2e2a3b1b4d2a3 a2e5d1c1e5 e3 c4e3 b1a3d4d3b1a3 d2d4e3b3b3a3d1d1d2c3c4a3
e3e5b5 d1a4e5e2e2b1e3d4b3a3d1 d3e5 b3a4b1e1d1

c4e5d2 e3e5b1e3d2d1a1e5 a4a1a3 c4e3 c5d2a3
b3a4b4c3d2a3d4 e1a3e5 e1e3b1 c4e3 e1a4e5b1b1e3d2d1a1e5 d4e5d2b1a3 e3 e5d4 c2a3d4d2a3 e3e5c1e5a3c4 d1e3
b1a3d4a4b4b4a3a3 e1b1a4b4a3a1 c4 d2b4b4a4b1a1e3c4d2a1a3  d2c4 e3 a1b1e3c5e3d2c4c4a3 e3 d1a3 d1e5b1c5d2c5b1a3
d3e3d4d1 c4e3 e1c4e5d1 d4a4c3c4a3 e1e3b1a1d2a3 d3a3 d1a4d4 a3a1b1a3  a3a1 d1a3d1 d2c4c4e5d1a1b1a3d1 d1a3d1 a3c4a4c1e5a3d4a1a3d1
b3a4b4e1a4d1d2a1d2a4d4d1 c4a3 b1e3b3b2a3a1a3b1a4d4a1 d3e5 a1a4b4c3a3e3e5 a1e3d4a1 c1e5a3 c4a3d1
c4a3a1a1b1a3d1 a2a4e5d2b1a4d4a1 d3a3 c1e5a3c4c1e5a3 b2a4d4d4a3e5b1 a1e3d4a1 c1e5a3 d1e5c3d1d2d1a1a3b1a4d4a1 c4e3
e1e5d2d1d1e3d4b3a3 d3a3 c4e3 c4e3d4c2e5a3 b1a4b4e3d2d4a3 a3a1 c4a3d1 b3b2e3b1b4a3d1 d3a3 c4e3 c4e3d4c2e5a3
c2b1a3b3c1e5a3 e1a4c4d5c3a3 d3a4d2a1 c3b1d2c4c4a3b1 a3d4a1b1a3 b3a3d1 c2b1e3d4d3d1 d4a4b4d1 c1e5d2 c5a3b1b1a4d4a1
a3d4 c4e5d2 c4a3 b1d2c5e3c4 a4e5 d1d2 d1e3 b4a4d3a3d1a1d2a3 b1a3e2e5d1a3 b3a3a1 a3c4a4c2a3 c4 e3d1d1a4b3d2a3 d3a3 c4a3e5b1 c2c4a4d2b1a3

a1a4d4 e5d4d2c1e5a3 e1a3d4d1a3a3 e2e5a1 d3a4d4b3 d3a3 a1b1a4e5c5a3b1 b3b2a3a5 c4e5d2 c4 a3d4d3b1a4d2a1
c4a3 e1c4e5d1 c5e5c4d4a3b1e3c3c4a3 b3 a3d1a1 a3d4 a3e2e2a3a1 e3 c4 a3c4d2a1a3 d3a3d1 b2e5b4e3d2d4d1
c1e5a3 a1e5 b1a3d1a3b1c5a3d1 a1a3d1 b3a4e5e1d1 c4a3d1 e1c4e5d1 b2e3c3d2a1e5a3c4d1 a1a3d1 e2e5b1a3e5b1d1 c1e5d2
d1a3c5d2d1d1a3d4a1 d2d4d3d2d1a1d2d4b3a1a3b4a3d4a1 a3a1 c1e5 d2c4 e2e3e5a1 b3b1e3d2d4d3b1a3 e3e5 b4d2c4d2a3e5
b4a3b4a3 d3a3 a1a3d1 c3d2a3d4e2e3d2a1d1 d2c4 a1 a3d4 a3e5a1 d1d2 e1a3e5 b3a4e5a1a3 d3 a3e1e3b1c2d4a3b1
b3a3a1a1a3 b1d2c2e5a3e5b1 e3 e5d4 b2a4b4b4a3 d1e5b1 c4a3c1e5a3c4 a1a3d1 e2e3c5a3e5b1d1 d1a3b4c3c4e3d2a3d4a1
d3a3e1e3b1a1d2a3d1 e3c5a3b3 b3b2a4d2b5 a3a1 b1a3e2c4a3b5d2a4d4 a3a1 d4a4d4 d1e5d2c5e3d4a1 a1a4d4 e5d1e3c2a3
a2a3a1a3a3d1 d1e3d4d1 d3d2d1b3a3b1d4a3b4a3d4a1

e3a2a4e5a1a4d4d1 d1d2 c5a4e5d1 c5a4e5c4a3a5 e3 b3a3d1 e1c4e3d2d4a1a3d1 c4a3d1 b1a3c2b1a3a1d1 c1e5a3 c5a4e5d1
c4e3d2d1d1a3 e5d4 e2b1a3b1a3 d3 e5d4 d1d2 c3a3e3e5 d4e3a1e5b1a3c4 a3d4c4a3c5a3 d3a3d1 d1a3d1 e1b1a3b4d2a3b1d1
e1b1a4c2b1a3d1 d3e3d4d1 c4e3 b3e3b1b1d2a3b1a3 d1 d2c4 a3a1e3d2a1 d3d2c2d4a3 d3a3 c5a4e5d1 e3e1e1e3b1a1a3d4d2b1
c5a4e5d1 a3a1d2a3a5 c3d2a3d4 e1c4e5d1 d3d2c2d4a3 a3d4b3a4b1a3 d3a3 d4 e3c5a4d2b1 e3 c5a3b1d1a3b1 e3e5b3e5d4a3
c4e3b1b4a3 d1e5b1 c4a3 e2b1a3b1a3 b4a3b4a3 c4a3 b4a4d2d4d1 b4a3b1d2a1e3d4a1 a1a4e5d1 b1a3d4d3a3d4a1 d3a3
c4e5d2 e5d4 b4a3b4a3 a1a3b4a4d2c2d4e3c2a3  d2c4 b4e3d4c1e5a3 e3 c5a4a1b1a3 c2c4a4d2b1a3 b1d2a3d4 d4a3
b4e3d4c1e5a3 e3 c4e3 d1d2a3d4d4a3

d2c4 d4 d5 e3c5e3d2a1 b1d2a3d4 a3d4 c4e5d2 c1e5a3 c5a4e5d1 d4a3 e2e5d1d1d2a3a5
e2d2a3b1 d3 e3c5a4e5a3b1 e5d4 e2b1a3b1a3 b4a4d2d4d1 a3b5b3a3c4c4a3d4a1 d4a3 c5a4e5d1 a3e5a1 e1e3d1 a1b1a4e5c5a3
b4a4d2d4d1 a1a3d4d3b1a3 b4e3d2d1 c5a4a1b1a3 e3e2e2a3b3a1d2a4d4 b1a3d4b3a4d4a1b1e3d4a1 d3e3d4d1 b3a3c4e5d2b3d2
e5d4a3 e1c4e5d1 b1d2b3b2a3 b4e3a1d2a3b1a3 d1 d5 a3d1a1 d3a3e1c4a4d5a3a3 e3c5a3b3 c3d2a3d4 e1c4e5d1 d3a3 b3a4b4e1c4e3d2d1e3d4b3a3
d2c4 d4 e3 e5d1a3 d3a3 d1a4d4 b3b1a3d3d2a1 e1a4e5b1 d4e5d2b1a3 e3 e1a3b1d1a4d4d4a3 d2c4
d4 e3 b4a3d4e3b3a3 e1a3b1d1a4d4d4a3 d3a3 d1a4d4 e2b1a3b1a3 d2c4 e3c5e3d2a1 e1b1d2d1 a3b5a3b4e1c4a3 d3a3 c5a4a1b1a3
b4a4d3a3b1e3a1d2a4d4 d2c4 e3c5e3d2a1 d1a3d4a1d2 d3a3 c1e5a3c4 b2a4d4d4a3e5b1 b4e3d2d1 e3e5d1d1d2 d3a3 c1e5a3c4
e2e3b1d3a3e3e5 c5a4e5d1 b3b2e3b1c2d2a3a5 c4a3d1 c5a4a1b1a3d1 a3a1 d2c4 e3 d1e5e2e2d2 e3 b3a3a1a1a3 a1e3b3b2a3

d2b4e1d2a1a4d5e3c3d2a3 d3a3d1a1d2d4a3a3 c1e5a3 d4a3 d3a3d1e3b1b4a3 e3e5b3e5d4a3 c5a3b1a1e5 a3c4c4a3 e3 b4a4d2d1d1a4d4d4a3
c5a4a1b1a3 e2b1a3b1a3 e3c5e3d4a1 c1e5 d2c4 b3a4d4d4e5a1 a1a4e5a1a3 d1e3 e2a3c4d2b3d2a1a3 b4a4d4 d2d4d3d2c2d4e3a1d2a4d4
a2a3 c4a3 d1e3d2d1 a3d1a1 a1b1a4e1 e2e3d2c3c4a3  d2c4 a3d1a1 d1d2 d3d2e2e2d2b3d2c4a3 d3a3 a1b1a4e5c5a3b1
d3a3d1 e1e3b1a4c4a3d1 c1e5d2 a3b5e1b1d2b4a3d4a1 d3d2c2d4a3b4a3d4a1 c4a3d1 c2b1e3d4d3a3d1 d3a4e5c4a3e5b1d1
e1a4e5b1d1e5d2c5a4d4d1 a1a4e5a1a3e2a4d2d1 d4a4d1 e1c4e3d2d4a1a3d1 d1d2 d4a4d1 e1c4e3d2d4a1a3d1 d1a3b1c5a3d4a1 d3a3
c1e5a3c4c1e5a3 b3b2a4d1a3

d3a3b4e3d4d3a4d4d1 e3 c4e3 e2a4b1a1e5d4a3  e1a4e5b1c1e5a4d2 a1e3d4a1 d3a3 c5d2a4c4a3d4b3a3
a3a1 a1e3d4a1 d3 d2d4a2e5d1a1d2b3a3 e1a4e5b1c1e5a4d2 d1 a3d1a1a3c4c4a3 b1a3e1a3d4a1d2a3 d1d2 c5d2a1a3 d3a3
d1a4d4 d2d4d3e5c4c2a3d4b3a3 d3 a4e5 c5d2a3d4a1 b3a3a1a1a3 b3b1e5e3e5a1a3 c1e5d2 d1a3 b1e5a3 d1d2 c3b1e5a1e3c4a3b4a3d4a1
a3d4a1b1a3 d3a3e5b5 e2b1a3b1a3d1 c1e5d2 d3a3 d1e3 e2e3e5b5 d1e3d4c2c4e3d4a1a3 a1b1e3d4b3b2a3 c4a3d1
d4a4a3e5d3d1 d3 e5d4a3 d1d2 d3a4e5b3a3 a3a1 d1d2 d1a4c4d2d3a3 b3a4d4b3a4b1d3a3 c1e5d2 c3a4e5c4a3c5a3b1d1a3 b3a3a1a1a3
c5a3b1a1e5a3e5d1a3 e2e3b4d2c4c4a3 d3a3 a2a3e5d4a3d1 b2a4b4b4a3d1 a1a4e5d1 d3d2c2d4a3d1 c4 e5d4 d3a3 c4 e3e5a1b1a3
c1e5d2 d1e3d4d1 b4a4a1d2e2 a3d4 e3c3e3a1 c4e3 e2c4a3e5b1 a3b2 c1e5a3 d1a3b1a1 d3a4d4b3 e5d4a3 e1e5b1a3a1a3
d3a3 b3a4a3e5b1 e2d2d3a3c4a3 e3 a1a4e5a1a3d1 c4a3d1 c4a4d2d1 d3a3 c4e3 b4a4b1e3c4a3 e5d4a3 e2b1e5c2e3c4d2a1a3
e3d4a1d2c1e5a3 e5d4 a3b4e1d2b1a3 b3a4d4d1a1e3d4a1 d1e5b1 d1a4d2b4a3b4a3 e3e5 d1a3d2d4 d3 e5d4a3 e1e5d2d1d1e3d4b3a3
a3a1 d3 e5d4a3 e1b1a4d1e1a3b1d2a1a3 d1e3d4d1 c3a4b1d4a3d1 c4a3 d1d2d4b3a3b1a3 a3a1 d2d4c5e3b1d2e3c3c4a3
e3b4a4e5b1 d3a3d1 c4a3a1a1b1a3d1 e5d4a3 e3b4a3 e1e5b1a3 d3a3 a1a4e5a1a3 d1a4e5d2c4c4e5b1a3

e1a4c4d5c3a3 a3d1a1 d3e3d4d1 c4a3d1 e1c4a3e5b1d1 a3a1 e3c5a3b1a1d2 e1e3b1 c4e3 e1a3b1a1a3 d3 e5d4 e2b1a3b1a3 d3a3 b3a3 c1e5a3
c4a3 d1a4b1a1 e1a3e5a1 d1e5b1 c4a3d1 e3e5a1b1a3d1 d2c4 a1b1a3b4c3c4a3 b4a3b4a3 e1a4e5b1 c4a3d1 b3a4d4d1a4c4e3a1a3e5b1d1
c1e5d2 c4e5d2 b1a3d1a1a3d4a1 a4 b3e3a1e3d1a1b1a4e1b2a3 d4a4d4 b4a3b1d2a1a3a3 e1a4c4d5c3a3 a3d1a1
d3e3d4d1 c4a3d1 e1c4a3e5b1d1 d2c4 e3 e1a4e5b1 c4e5d2 c4e3 e2e3c5a3e5b1 d3a3 b3a3d1e3b1 a3a1 d2c4 c2a3b4d2a1 a3d4b3a4b1a3
d1e3d4d1 d3a4e5a1a3 e2a4b1a1e5d4a3 d2d4d1e3a1d2e3c3c4a3 a1e5 e3d1 c5a4e5c4e5 b4a4d4a1b1a3b1 c1e5a3
b1d2a3d4 e1e3d1 b4a3b4a3 b3a3d1e3b1 d4a3 e1a3e5a1 c2e3b1e3d4a1d2b1 d3a3 a1a3d1 e3a1a1a3d4a1e3a1d1


d4a4e5d1 e1a4e5c5a4d4d1 e3b3b3e5d1a3b1 d1e3d4d1 e2d2d4 c4e3 d3a3d1a1d2d4a3a3 b4e3d2d1 c4e3
b3b2e3d4c2a3b1 a3d1a1 d2b4e1a4d1d1d2c3c4a3 e2d2b5a3 a3a1 d2d4a3b5a4b1e3c3c4a3 d3e3d4d1 d1a3d1 b1d2c2e5a3e5b1d1
d4d2 d2d4c5a3b3a1d2c5a3d1 d4d2 e1c4a3e5b1d1 d4d2 b1e3d2d1a4d4 d4a3 c4 a3b4a3e5c5a3d4a1  a3c4c4a3 d4 a3e1e3b1c2d4a3
a2e3b4e3d2d1 e1a3b1d1a4d4d4a3 a3c4c4a3 d4a3 e2e3d2a1 c2b1e3b3a3 d3a3 b1d2a3d4 a3a1a4e5e2e2a4d4d1 d3a4d4b3
d3a3d1 c4e3b4a3d4a1e3a1d2a4d4d1 d2d4e2b1e5b3a1e5a3e5d1a3d1 c1e5d2 d4a4e5d1 b1a3e5d4d2b1e3d2a3d4a1 e1c4e5a1a4a1 e3
c4 a4c3a2a3a1 d3a3 d4a4d1 d3a4e5c4a3e5b1d1 c1e5 a3c4c4a3d1 d4a3 c4a3 a1d2b1a3b1e3d2a3d4a1 d3a3 c4e3 a1a4b4c3a3
b3a3d1 a1a4b1a1e5b1a3d1c4e3 d4a3 d1a4d4a1 e1e3d1 e5d4 b1a3b4a3d3a3 d2c4 e2e3e5a1 d3a4d4b3 d3a3d1 c4a3 e1b1d2d4b3d2e1a3
d5 b1a3d4a4d4b3a3b1 c4a4d2d4 d3a3 d4a4e5d1 d3a3 e1e5a3b1d2c4d1 d1a4e5c4e3c2a3b4a3d4a1d1 a3a1 a2a3 d4a3
d1e3d2d1 c1e5a3c4 e3b4a3b1 e1c4e3d2d1d2b1 d3a3 a1b1d2d1a1a3d1d1a3  c4 e3b4a3 d1 d5 d3a4d2a1 d1 e3b1b1e3b3b2a3b1

d1d2 c4e3 b1e3d2d1a4d4 d4a3 b4a3a1 e5d4 a1a3b1b4a3 e3 d4a4d1 c4e3b1b4a3d1 c4e3 e2a4b1a1e5d4a3 d4a3 c4 d5
b4a3a1a1b1e3 e1a4d2d4a1 a2a3a1a3a5 c4a3d1 d5a3e5b5 d1e5b1 c4 b2e5b4e3d4d2a1a3 c1e5d2 c5a4e5d1 a3d4c5d2b1a4d4d4a3
e1e3b1a1a4e5a1 d3 e3c3a4d4d3e3d4a1a3d1 a3a1 d2d4a3e1e5d2d1e3c3c4a3d1 b3e3e5d1a3d1 d3 e3e2e2c4d2b3a1d2a4d4
c4 e5d4 a3d1a1 b3b2e3c1e5a3 a2a4e5b1 e1a4e5d1d1a3 c5a3b1d1 c4a3 a1b1e3c5e3d2c4 e1e3b1 c4e3 d3a3a1b1a3d1d1a3
a3a1 c4a3 c3a3d1a4d2d4  c4 e3b4c3d2a1d2a4d4 c1e5d2 d4a3 b3a4d4d4e3a1 e1e3d1 c4a3 b1a3e1a4d1 e3d2c2e5d2c4c4a4d4d4a3
b3a3a1 e3e5a1b1a3 e1c4e5d1 c4a4d2d4 a4d4 b4e3e5d3d2a1 c4a3d1 b1d2b3b2a3d1d1a3d1 c1e5 a4d4 e3
d1a4e5b2e3d2a1a3a3d1 a3a1 c4 a4d4 a1b1a4e5c5a3 d1a4d4 d1e5e1e1c4d2b3a3 d3e3d4d1 c4a3 d1e5b3b3a3d1 d3a3 d1a3d1
c5a4a3e5b5 e3d2c4c4a3e5b1d1 c4a3d1 d1a4e5b3d2d1 a4e5 c4a3d1 e3e2e2e3d2b1a3d1 a1a4e5b1b4a3d4a1a3d4a1 a4e5 c4a3d1
e2c4a4a1d1 d3a3 b3c4d2a3d4a1d1 c1e5d2 e3d1d1d2a3c2a3d4a1 d1e3d4d1 b3a3d1d1a3 d4a4d1 c5a3d1a1d2c3e5c4a3d1 b3a3c4e5d2b3d2
d3a3e1c4a4b1a3 c4e3 d4e3d2d1d1e3d4b3a3 d3a3 d1a3d1 a3d4e2e3d4a1d1 b3a3c4e5d2c4e3 c2a3b4d2a1 d3a3 c4a3e5b1
e1a3b1a1a3 c4a3d1 c4e3b1b4a3d1 d4a4e5d1 b4e3d4c1e5a3b1a4d4a1 e1c4e5d1 a1a4a1 c1e5a3 c4a3d1 b4a4a1d2e2d1
d3 a3d4 c5a3b1d1a3b1

d4a3 c5a4d5a3a5c5a4e5d1 e1e3d1 c1e5a3c4c4a3 a3b5d2d1a1a3d4b3a3 d4a4e5d1 e3 e1b1a4b4d2d1a3
c4e3 d4e3a1e5b1a3 a3d4 c5a4e5c4e3d4a1 c1e5a3 c4a3d1 e1c4a3e5b1d1 e2e5d1d1a3d4a1 c4a3 e1b1a3b4d2a3b1 e3e5c2e5b1a3
d3a3 d4a4a1b1a3 d4e3d2d1d1e3d4b3a3 a1a3c4 a3d1a1 c4a3 d3a3c3e5a1 d3a3 c4e3 c5d2a3 a3a1 c4e3 d1e5d2a1a3 d3a3
d4a4d1 e3d4d1 d5 b1a3e1a4d4d3 b3 a3d1a1 d3e3d4d1 c4a3d1 e1c4a3e5b1d1 c1e5 d2c4d1 d1a3 e1e3d1d1a3d4a1 c1e5a3
b3a3b3d2 d4a4e5d1 e3e1e1b1a3d4d4a3 e3 d4a4e5d1 b4a4d3a3b1a3b1 a3d4 b3a3 c1e5d2 d3a4d2a1 d1a3 b1a3d4a4e5c5a3c4a3b1
d1d2 d1a4e5c5a3d4a1 a3a1 a3d4 c5a4d5e3d4a1 d1a3 e1b1a3d1d1a3b1 d1e5b1 d4a4d1 e1e3d1 b3a3a1a1a3
b4e3d1d1a3 d3 e3e2e2c4d2b3a1d2a4d4d1 d2b4b4d2d4a3d4a1a3d1 d1e3b3b2a4d4d1 a1e3b1d2b1 a4e5 d3e5 b4a4d2d4d1 b1a3d1a3b1c5a3b1
d4a4d1 c4e3b1b4a3d1 d1 d2c4 a3d1a1 e5d4a3 b3b2a4d1a3 d3a4d4a1 d2c4 e2e3d2c4c4a3 a3a1b1a3 e3c5e3b1a3
b3 a3d1a1 d3a3 b3a3c4c4a3 d1e5b1a1a4e5a1 d3a4d4a1 c4 e5d1e3c2a3 d4 a3d1a1 c1e5a3 a1b1a4e1 e2b1a3c1e5a3d4a1

e1a3d4d1a3a5 e3e5d1d1d2 e1a4e5b1 c5a4e5d1 b1e3e2e2a3b1b4d2b1 d3e3c5e3d4a1e3c2a3 c1e5a3 c4a3 b4a4d2d4d1
e2c4e3a1a1a3 d3a3 c5a4a1b1a3 d3a4e5c4a3e5b1 a3d1a1 b3a3c4e5d2 e3 c1e5d2 a3c4c4a3 d1a3b4c3c4a3 d1 e3d3b1a3d1d1a3b1
a4e5 d2c4 c5a4e5d1 c4e3 d3a3e2a3d4d3 a4e5 d2c4 c4 d2c2d4a4b1a3 b1d2a3d4 d4 a3d1a1 d3a4d4b3 b4a4d2d4d1 b1e3d2d1a4d4d4e3c3c4a3
c1e5 e5d4 b2a4b4b4e3c2a3 c1e5d2 a4e2e2a3b1a1 e3 e5d4 a3a1b1a3 d2d4d1a3d4d1d2c3c4a3 a3d1a1
d1a1a3b1d2c4a3 a3a1 c1e5d2 d1 d2c4 a3d1a1 d1a3d4a1d2 d3a3e1c4e3a1

a3d1a1d2c4 e5d4 b2a4b4b4a3 d3e3d4d1 a1a4e5a1 c4 e5d4d2c5a3b1d1 e1a4e5b1 c1e5d2 c5a4a1b1a3
d3a3e5d2c4 d1a4d2a1 e5d4 d1e5a2a3a1 d3a3 a2a4d2a3  a2a3 d3d2b1e3d2d1 b2e3b1d3d2b4a3d4a1 c1e5a3 d4a4d4 a3b2
c3d2a3d4 b3a3d1 b4a3b4a3d1 d3d2d1e1a4d1d2a1d2a4d4d1 c1e5a3 d4e5c4 d4a3 d4a4e5b1b1d2a1 b3a4d4a1b1a3 c5a4e5d1
c5a4e5d1 c4a3d1 e1b1a3a1a3a5 e3 c5a4a1b1a3 e2b1a3b1a3 a3d4 b3b1a4d5e3d4a1 c1e5 d2c4 c5a4e5d3b1e3d2a1 c5a4e5d1 d3a3b3b2d2b1a3b1
c4a3 b3a4a3e5b1 c5a4e5d1 e3b1b1e3b3b2a3b1 e3 c5a4d1 a1b1e3c5e3e5b5 e3 c5a4d1 d4a4c3c4a3d1 a3a1e5d3a3d1
e3 b3a3d1e3b1 c4e3 b3b2a4d1a3 a3d1a1a3c4c4a3 c5b1e3d2d1a3b4c3c4e3c3c4a3 b3a3c4e5d2 d3a4d4a1 c5a4e5d1
a4c3a1a3d4d2a3a5 e5d4a3 e3e2e2a3b3a1d2a4d4 e2b1e3a1a3b1d4a3c4c4a3 e5d4a3 c5a3d4a3b1e3a1d2a4d4 e1b1a3d1c1e5a3 e2d2c4d2e3c4a3
e5d4 b3e5c4a1a3 d3e5 e3 c5a4d1 c4e5b4d2a3b1a3d1 d1e5e1a3b1d2a3e5b1a3d1 b3a3c4e5d2c4e3 c5a4e5d1 d3a3b4e3d4d3a3
d3a3d1 b1a3c2b1a3a1d1 b4e3d2d1 d4a4d4 d3e5 d3a3d1a3d1e1a4d2b1 c1e5a3c4 b3b2e3b1b4a3 a1b1a4e5c5a3a5c5a4e5d1
e3e5 b3b2e3c2b1d2d4 c1e5d2 c5a4e5d1 b3a4d4d1a1d2a1e5a3 c1e5e3d4d3 c5a4a1b1a3 e2b1a3b1a3 d1 d2c4
d5 e3 b3b2a3a5 c4a3d1 b4a4b1a1d1 c1e5a3c4c1e5a3 d1a3d4a1d2b4a3d4a1 d3a3d1d2b1a3b1e3d2a1 d5 b4a3a1a1b1a3 e5d4
a1a3b1b4a3

d1 d2c4 d1 e3c2d2d1d1e3d2a1 d3 e5d4 e2b1a3b1a3 b4a4d2d4d1 a1a3d4d3b1a3 d3a4d4a1 c4a3 b3a4a3e5b1 e2e5a1
b4a4d2d4d1 d1e5b1 a2 a3b4e1c4a4d2a3b1e3d2d1 c4a3 c4e3d4c2e3c2a3 d3e5 d3a4e5a1a3 a3a1 a2a3 d3d2b1e3d2d1  a4e5
c5a4a1b1a3 e2b1a3b1a3 a3b5d2c2a3 d3a3 c5a4e5d1 d3a3d1 d1a4e5e2e2b1e3d4b3a3d1 a3a1 d3a3d1 e1c4a3e5b1d1 d1e3d4d1 e2d2d4
a3a1 d3a3d1 c4a4b1d1 d2c4 a3d1a1 d2d4d3d2c2d4a3 d3a3 a1e3d4a1 d3 e3e2e2a3b3a1d2a4d4  a4e5 d2c4 a3d1a1 c4a4d2d4 d3a3
c4a3d1 c5a4e5c4a4d2b1 a3a1 d2c4 e2e3e5a1 b1a3d4a4d4b3a3b1 e3 e5d4a3 d3a4e5c4a3e5b1 d2d4a3e2e2d2b3e3b3a3 e1a4e5b1
a1a4e5d1 d3a3e5b5 e3 e5d4 b3a4a3e5b1 d3a3d4e3a1e5b1a3 d3a3 a1a3c4d1 b1a3c2b1a3a1d1 d4a3 d1a4d4a1 e1e3d1
d3e5d1  e5d4 b3a4a3e5b1 e3d2b4e3d4a1 c4a3d1 b1a3e2e5d1a3b1e3d2a1 b4e3d2d1 a2a3 e1e3b1c4a3 d3 e5d4 e2b1a3b1a3
d3a4d4a1 c4e3 a1a3d4d3b1a3d1d1a3 c5a4e5d1 e2e5a1 a1b1a4e1 c3d2a3d4 e1b1a4e5c5a3a3  a1a4e5a1 c5a4e5d1 e3d1d1e5b1a3
c1e5a3 c4e3 e1c4e5d1 c5d2c5a3 e1a3d2d4a3 c1e5 d2c4 e1e5a1 b1a3d1d1a3d4a1d2b1 d1a3b1e3d2a1 c1e5a3 c5a4e5d1 e2e5d1d1d2a3a5
e1a4e5b1 c4e5d2 d3a3c5a4b1a3 d3 e3b4a3b1a1e5b4a3d1 d3a3 a1a4e5b1b4a3d4a1d1 d4a4d4 b4a4d2d4d1
a3b5b3a3d1d1d2e2d1 c1e5 d2b4b4a3b1d2a1a3d1 a3a1 d3a3 c5a4d2b1 d2d4b3a3d1d1e3b4b4a3d4a1 c5a4d1 d5a3e5b5 d1a3
b1a3b4e1c4d2b1 a1a4e5b1 e3 a1a4e5b1 a3a1 d1 a3e1e5d2d1a3b1 a3d4 c4e3b1b4a3d1

b4e3d2d1 c5a4d2b3d2 d1e5b1a1a4e5a1 b3a3 c1e5d2 d3a4d2a1 a3e1e3b1c2d4a3b1 e3 c5a4a1b1a3 a1a3d4d3b1a3d1d1a3 d3a3d1
c2a3b4d2d1d1a3b4a3d4a1d1 d1e5e1a3b1e2c4e5d1  d1a4d4c2a3a5 e3e5b5 e2b1a3b1a3d1 c1e5d2 c5a4e5d1 b1a3d1a1a3d4a1
d4a3 d3a3c5a3a5c5a4e5d1 e1e3d1 c4a3d1 d2d4d1a1b1e5d2b1a3 d3 a3b5a3b4e1c4a3 e3 d1a3 b1e3d2d3d2b1 d1a4e5d1 c4 d2d4a2e5d1a1a3
b4e3d2d4 c1e5d2 c4a3d1 e2b1e3e1e1a3  e5d4 c2b1e3d4d3 b3e3e1d2a1e3d2d4a3 e3e1b1a3d1 e5d4 a3b3b2a3b3
e3e2e2a3b3a1a3 e3 d3a3d1d1a3d2d4 d3a3 c4e3 c2e3a1a3 a3a1 d3a3c2e5d2d1a3 d1e3 e1a4d1d2a1d2a4d4 b3b1d2a1d2c1e5a3
d1a4e5d1 e5d4a3 a2a4d2a3 e2e3b3a1d2b3a3 d3a3 e1a3e5b1 c1e5 a3d4 c5a4d5e3d4a1 c4a3e5b1 b3b2a3e2 b3a4d4d1a1a3b1d4a3
c4a3 b3a4e5b1e3c2a3 d3a3d1 d1a4c4d3e3a1d1 d4a3 d1 e3c3e3a1a1a3 a1a3c4 a3d1a1 b4e3d2d4a1a3d4e3d4a1
c5a4a1b1a3 d3a3c5a4d2b1

e1b1a3d4a3a5 e5d4 c5d2d1e3c2a3 c1e5d2 d3a3b4a3d4a1a3 c4 a3a1e3a1 d3a3 c5a4a1b1a3
e3b4a3 a3a1 d1 d2c4 d1a3 e1a3e5a1 c3e3d4d4d2d1d1a3a5 a3d4a1d2a3b1a3b4a3d4a1 c5a4d1 d3a4e5c4a3e5b1d1  d1d2d4a4d4
b3a4d4b3a3d4a1b1a3a5c4a3d1 b3a4d4a1a3d4a3a5a3d4 a2e5d1c1e5 e3e5b5 d1d5b4e1a1a4b4a3d1 e2e3d2a1a3d1
c1e5a3 c5a4d1 e2b1a3b1a3d1 d1a3 b1a3c2c4a3d4a1 d3 e3e1b1a3d1 c5a4e5d1 a1a4e5a1 c4a3e5b1 d1a3b4c3c4a3b1e3 b2a4d4a4b1e3c3c4a3
d3a3d1 c1e5 d2c4d1 c5a4e5d1 c4a3 c5a3b1b1a4d4a1 e2e3d2b1a3 a3a1 c4a3e5b1d1 d1a3d4a1d2b4a3d4a1d1 d1a3
b4a4d3d2e2d2a3b1a4d4a1 d1e5b1 c4 a3b5e1b1a3d1d1d2a4d4 d3a3 c5a4d1 a1b1e3d2a1d1 c5a4e5d1 d3a3c5a3a5 a3a1b1a3 a3a1
c4a3e5b1 b3a4d4d1a4c4e3a1d2a4d4 a3a1 c4a3e5b1 b3a4d4d1a4c4e3a1a3e5b1  a4b1 e1a4e5b1b1a3a5c5a4e5d1 e3b1b1a3a1a3b1
c4a3e5b1d1 e1c4e3d2d4a1a3d1 d1d2 c5a4e5d1 c4e3d2d1d1a3a5 e5d4 c4d2c3b1a3 b3a4e5b1d1 e3e5b5 c5a4a1b1a3d1


e5d4 e3e5a1b1a3 b4a4d5a3d4 d3a3 c5a4e5d1 e1b1a3d1a3b1c5a3b1 d3a3d1 a3b5b3a3d1 d3a3 c4 e3e2e2c4d2b3a1d2a4d4
b3 a3d1a1 d3a3 b1a3e2c4a3b3b2d2b1 c1e5a3 b1d2a3d4 d3a3 b3a3 c1e5a3 c5a4e5d1 e2e3d2a1a3d1 d4a3 e1a3e5a1
b1a3d1a1a3b1 d1a3b3b1a3a1 c4a3 d1e5e2e2b1e3c2a3 d3a3 c4 e5d4d2c5a3b1d1 c5a4e5d1 e3 d2b4e1a4d1a3 e5d4a3 c2b1e3d4d3a3
a1e3b3b2a3  a4d1a3a5 c4e3 b1a3b4e1c4d2b1 b3a3a1 a3d1d1e3d2b4 d3a3 b3a4d4d1a4c4e3a1a3e5b1d1 c1e5d2 c5a4e5d1 e3d1d1d2a3c2a3
a3e1d2a3 c4 d2d4a1a3b1d2a3e5b1 d3a3 c5a4a1b1a3 e3b4a3 a3a1 a1e3b3b2a3 d3a3 d1e5b1e1b1a3d4d3b1a3 a2e5d1c1e5 a4e5
c5e3 d1e3 e2a4b1b3a3 b3a4d4a1b1a3 c4e3 d3a4e5c4a3e5b1 d1d2 c5a4e5d1 d4 a3a1a3d1 b2e3c3d2c4a3 c1e5 e3
e5d1a3b1 d3a3 c4e3 c3a4d4d4a3 e2a4b1a1e5d4a3 d1d2 c5a4e5d1 d1e3e5b1d2a3a5 d1a4e5e2e2b1d2b1 a3d4 b2a4b4b4a3
c4 e3d3c5a3b1d1d2a1a3 d2c4 d4 a3d1a1 e1a4d2d4a1 d3 d5a3e5b5 c1e5d2 d4 a4c3d1a3b1c5a3d4a1 c4a3d1 c5a4a1b1a3d1

a1a4e5a1 a3d1a1 e1a3b1b4d2d1 e3 b3a3e5b5 d3a4d4a1 c4a3d1 e3e2e2a3b3a1d2a4d4d1 e1a3e5c5a3d4a1 d1a3 b3e3b3b2a3b1 e1a4e5b1
c5a4e5d1 c4a3 b4a4d2d4d3b1a3 b4d5d1a1a3b1a3 a3d1a1 d2b4e1a4d1d1d2c3c4a3  c4e3 e2a4b1a1e5d4a3 c5a4e5d1 a3b5e1a4d1a3
e3e5 c2b1e3d4d3 a2a4e5b1 c4a3 b4a4d4d3a3 a3d4a1d2a3b1 d1e3e5b1e3 d3a3 c1e5a3c4 e3d2b1 c5a4e5d1 e3c5a3a5
b1a3e5 b3a3a1a1a3 c3c4a3d1d1e5b1a3 d1d2 e3e5 e1b1a3b4d2a3b1 b3b2a4b3 c5a4e5d1 e3c5a3a5 c3e3d2d1d1a3 c5a4a1b1a3
a3e1a3a3 a4e5 d1d2 c5a4e5d1 a3a1a3d1 d3a3b4a3e5b1a3 e2a3b1b4a3 c4 e3b4d2a1d2a3 d3a3 b3a3d1e3b1 a3a1 c5a4a1b1a3
c2c4a4d2b1a3 c4d2a1a1a3b1e3d2b1a3 c5a4e5d1 a4d4a1 d3a3d1a4b1b4e3d2d1 e1c4e3b3a3 a1b1a4e1 b2e3e5a1 a1a4e5a1 e3b3a1a3
c5e5c4c2e3d2b1a3 a1a4e5a1a3 e2e3d2c3c4a3d1d1a3 d3a3 b3a4a3e5b1 c5a4e5d1 b3a4b4e1b1a4b4a3a1a1b1e3d2a1 a4b1 c1e5a4d2
d3a3 e1c4e5d1 e2e3d2c3c4a3 a3a1 d3a3 e1c4e5d1 a3e2e2a3b4d2d4a3 c1e5a3 d3a3 d1a3 c4e3d2d1d1a3b1 b4d2d4a3b1 e1e3b1
c4a3 b3b2e3c2b1d2d4  

d1d2 c5a4a1b1a3 d3a3e5d2c4 a3d1a1 c4a3 b4a3b4a3 c1e5a3 b3a3c4e5d2 d3a3 c5a4d1 e2b1a3b1a3d1
d2c4 a3d1a1 b4a4d2d4d1 c4d2c3b1a3 d3e3d4d1 d1a4d4 a3b5e1b1a3d1d1d2a4d4 c4 a4e1d2d4d2a4d4 c1e5 a4d4 e3 b3a4d4e5a3
d3a3 c5a4d1 a1e3c4a3d4a1d1 a3a1 d3a3 c5a4a1b1a3 b3e3b1e3b3a1a3b1a3 c5a4e5d1 d2d4a1a3b1d3d2a1 c3d2a3d4 d3a3d1
b3b2a4d1a3d1  a4d4 a3b5d2c2a3 d3a3 c5a4e5d1 d3a3 c2b1e3d4d3d1 d1e3b3b1d2e2d2b3a3d1 a4d4 a3d4 e3a1a1a3d4d3 d3a3
e1c4e5d1 c2b1e3d4d3d1 a3d4b3a4b1a3 d1d2 c5a4e5d1 a3e5d1d1d2a3a5 e2e3d2a1 c5a4a3e5 d3 a3d4a1d2a3b1a3 d2d4d3a3e1a3d4d3e3d4b3a3
c5a4e5d1 d4 e3e5b1d2a3a5 e1e3d1 e3a1a1d2b1a3 d1e5b1 c5a4e5d1 c4a3d1 b1a3c2e3b1d3d1 d3a3 a1a4e5d1

d2c4 c5a4e5d1 e2e3e5a1 b4e3d2d4a1a3d4e3d4a1 b1a3b4e1c4d2b1 c4a3d1 c3a3c4c4a3d1 e1b1a4b4a3d1d1a3d1 c1e5a3 c5a4e5d1
e3c5a3a5 d3a4d4d4a3a3d1 e3e5b5 e3d3b4d2b1e3a1a3e5b1d1 d3a3 c5a4a1b1a3 c2a3d4d2a3 e3 b3a3e5b5 c1e5d2 a3d4
e1e5c3c4d2a3d4a1 c4a3d1 e1b1a4d3e5b3a1d2a4d4d1 e3 b3a3e5b5 a3d4e2d2d4 c1e5d2 d1 d2c4d1 d4 a4d4a1 e1e3d1 c3a3d1a4d2d4
d3a3 c5a4d1 e1e5d2d1d1e3d4a1a3d1 e2e3c5a3e5b1d1 b1a3b3c4e3b4a3d4a1 d3e5 b4a4d2d4d1 c4a3d1 e2b1e5d2a1d1
d3a3 c5a4a1b1a3 e1c4e5b4a3  d2c4d1 a3d4 d1a4d4a1 d3a3e1a4d1d2a1e3d2b1a3d1 c5a4e5d1 d4a3 e1a4e5c5a3a5
e1c4e5d1 b1d2a3d4 e2e3d2b1a3 d3 d2d4d3d2c2d4a3 d3a3 c5a4d1 c4e5b4d2a3b1a3d1 a3a1 d3a3 c5a4d1 c5a3b1a1e5d1
d1e3d4d1 c1e5 e5d4a3 e2a4e5c4a3 d3 b2a4b4b4a3d1 d1a3 b1a3e1a3d4a1a3d4a1 d3a3 c4a3e5b1 e3d3b4d2b1e3a1d2a4d4
e1a4e5b1 c5a4e5d1

c5a4e5d1 d4 e3c5a3a5 e1e3d1 c4a3 d3b1a4d2a1 d3a3 c5a4e5d1 e3e2e2c4d2c2a3b1 d1e3d4d1 b4a3d1e5b1a3
a3a1 b3a3 d4 a3d1a1 e1e3d1 c4a3 d1a3e5c4 c1e5d2 c5a4e5d1 d1a4d2a1 b1e3c5d2  c5a4e5d1 d4 e3e5b1d2a3a5
e1e3d1 d3b1a4d2a1 d3a3 e1b1a4c4a4d4c2a3b1 c5a4a1b1a3 d1a4b4b4a3d2c4 e5d4a3 e1e3b1a1d2a3 d3e5 a2a4e5b1 d3a3
e2e5d2b1 c4a3 a1a4e5b1c3d2c4c4a4d4 d3a3d1 e3e2e2e3d2b1a3d1 e1a4e5b1 c4a3 c4a4d2d1d2b1 a3a1 c4e3 e1e3d2b5 d3a3d1
b3b2e3b4e1d1 d3a3 c5a4e5d1 d3a3c4e3d1d1a3b1 e1e3b1 e5d4 c5a4d5e3c2a3 d3 e3c2b1a3b4a3d4a1 d3a3d1 e3d1d1d2d3e5d1
a1b1e3c5e3e5b5 d3 e5d4 e1a4d1a1a3 c4e3c3a4b1d2a3e5b5 d3a3 c5a4e5d1 b1a3b3b1a3a3b1 c4 a3d1e1b1d2a1
e1e3b1 d3a3d1 d1e1a3b3a1e3b3c4a3d1 c5e3b1d2a3d1 d3a3 b1a3c2c4a3b1 e3 c5a4d1 e2e3d4a1e3d2d1d2a3d1 c4 a3b4e1c4a4d2 d3 e5d4a3 a2a4e5b1d4a3a3
b4d2c4c4a3 b3b2a4d1a3d1 c5a4e5d1 d1a4d4a1 d2d4a1a3b1d3d2a1a3d1 c1e5d2 d1a4d4a1 e1a3b1b4d2d1a3d1 e3 c4 b2e5b4c3c4a3 b4a4b1a1a3c4
c2d2d1e3d4a1 d3e3d4d1 e5d4 b3a4d2d4 a4c3d1b3e5b1 e5d4a3 c2b1e3d4d3a3 e2a4b1a1e5d4a3 a3d1a1 e5d4a3 c2b1e3d4d3a3 d1a3b1c5d2a1e5d3a3

e3e5b3e5d4a3 d3a3 c5a4d1 e3b3a1d2a4d4d1 d4a3 c5a4e5d1 e3e1e1e3b1a1d2a3d4a1 a1e3d4a1 d3a3 b4d2c4c4d2a3b1d1 d3 e3e5d3d2a3d4b3a3d1
e3 d3a4d4d4a3b1 a1e3d4a1 d3a3 b1a3c1e5a3a1a3d1 e3 b4a3a1a1b1a3 a3d4 a4b1d3b1a3 b3a3d1 a1a4b1b1a3d4a1d1 d3 e3e2e2e3d2b1a3d1 c1e5d2 e3e2e2c4e5a3d4a1
c5a3b1d1 c5a4e5d1 d3a3 a1a4e5d1 c4a3d1 e1a4d2d4a1d1 d3e5 c2c4a4c3a3 a3a1 c1e5a3 c5a4e5d1 d3a3c5a3a5 e1c4e3b3a3b1
e3 c4a3e5b1 b1e3d4c2 d1a4e5d1 c4a3d1 a2a3e5b5 d3e5 b4e3a1b1a3 d3e5 b4a4d4d3a3 c5a3e5c4a3d4a1 e5d4a3
d2b4b4a3d4d1a3 b3a4d4a1a3d4a1d2a4d4 d3 a3d1e1b1d2a1 a4e5d2 a2a3 c4a3 b1a3e1a3a1a3 d2c4 c5a4e5d1 a3d1a1 d2d4a1a3b1d3d2a1
d3a3 e1c4a3e5b1a3b1 e3e2d2d4 d3a3 e1a4e5c5a4d2b1 a3b3a4e5a1a3b1 b3a3e5b5 c1e5d2 e1c4a3e5b1a3d4a1
e1a4e5b1 a3d1d1e5d5a3b1 c4a3d1 c4e3b1b4a3d1 d3a3 b3a3e5b5 d3a4d4a1 c4e3 d3a3a1b1a3d1d1a3 b3b2a3b1b3b2a3 e3
e3c3a4b1d3a3b1 c4e3 e1d2a1d2a3 d3e5 e1c4e5d1 d3a4e5b5 d3a3d1 a3b4e1a3b1a3e5b1d1 d2c4 e2e3e5a1 d3 e3c3a4b1d3 d1a3b3b2a3b1 c4a3d1 c5a4a1b1a3d1

c5a4e5c4a3a5c5a4e5d1 a3d4e2d2d4 e1e3b1c5a3d4d2b1 e3 c4 e3c4c4a3c2a3b4a3d4a1 c4a3
e1c4e5d1 a3e2e2d2b3e3b3a3 e3 c4 a3d4a1d2a3b1 a4e5c3c4d2 d3a3 c5a4d1 e1a3d2d4a3d1 c1e5a3 b3a3d1e3b1 a4b3b3e5e1a3
c5a4d1 e1a3d4d1a3a3d1  b3a4d4d1d2d3a3b1a3a5 d3a3 c1e5a3c4 d3a3c5a4e5a3b4a3d4a1 d3a3 c1e5a3c4 d2d4e2e3a1d2c2e3c3c4a3
a5a3c4a3 c5a4e5d1 d3a3c5a3a5 e1e3d5a3b1 d1e3 b2e3e5a1a3 c3d2a3d4c5a3d2c4c4e3d4b3a3 c5a4e5d1 d1a3d4a1d2b1a3a5
c1e5 d2c4 d4a3 c5a4e5d1 a3d1a1 e1e3d1 e1c4e5d1 e3b3b3a4b1d3a3 d3a3 e1c4a4d5a3b1 d1a4e5d1 c4a3 e2e3d2b5
c1e5 e3 c4 e3a1c4e3d1 d3a4d4a1 c4a3d1 a3e1e3e5c4a3d1 d1 d2c4 e2e3e5a1 b3b1a4d2b1a3 c4e3 e2e3c3c4a3 d1e5e1e1a4b1a1a3d4a1
c4a3 b4a4d4d3a3

a3a1 b3a3d1e3b1 c4e5d2b4a3b4a3 e3 c1e5d2 a1a4e5a1 a3d1a1 e1a3b1b4d2d1 a3d1a1 e1e3b1
b3a3c4e3 d1a3e5c4 c4a4d2d4 d3a3 e1a4e5c5a4d2b1 a1a4e5a1 d1a3 e1a3b1b4a3a1a1b1a3 a1a4e5a1a3d1 c4a3d1 e2e3b4d2c4c4a3d1
d1a4d4a1 e1b1a4a1a3c2a3a3d1 e1e3b1 d1e3 c5d2c2d2c4e3d4b3a3 c4e3 e1e3d2b5 e1e5c3c4d2c1e5a3 e1e3b1 d1a3d1
a1b1e3c5e3e5b5 c4a3d1 a2a4e5d2d1d1e3d4b3a3d1 a3a1 c4a3d1 c4a4d2d1d2b1d1 d3a3 a1a4e5d1 e1e3b1 d1a4d4 d2d4c2a3d4d2a3e5d1a3
e3b3a1d2c5d2a1a3 d3e5 a2a4e5b1 a4e5 b3a3d1e3b1 d1 a3d1a1 c5a4e5a3 e3e5 c3a4d4b2a3e5b1 d3e5 c2a3d4b1a3 b2e5b4e3d2d4
d2c4 d1 a3d1a1 b1e3c5d2 e3 c4e5d2b4a3b4a3 e1e3b1a3d2c4 e3e5b5 e3d1a1b1a3d1 c1e5d2 e1a4e5b1d1e5d2c5a3d4a1
c4a3e5b1 b3a4e5b1d1 d1e3d4d1 e2d2d4 b3a4b4b4a3 d1e3d4d1 b1a3c4e3b3b2a3 d2c4 c4e5d2 a3d1a1 d3a3e2a3d4d3e5
d3a3 d1 e3b1b1a3a1a3b1 a2e3b4e3d2d1 d3a3 d3d2d1e1a4d1a3b1 d3 e5d4 d1a3e5c4 d2d4d1a1e3d4a1

e3 c3d2a3d4 d3a3d1 a3c2e3b1d3d1 c4e3 b4a3b4a3 d4a3b3a3d1d1d2a1a3 c5a4e5d1 b3a4b4b4e3d4d3a3 c5a4e5d1 e3b1b1e3b3b2a3
e3 c5a4d1 c2a4e5a1d1 a3a1 e3e5 d1a4d2d4 d3a3 c5a4d1 d2d4a1a3b1a3a1d1
a1e3d4a1 c1e5a3 b3a3d1e3b1 c2a4e5c5a3b1d4a3 c4e3 a1a3b1b1a3 c5a4e5d1 d4a3 e1a4e5c5a3a5 c4a3 b4a4d2d4d1
d3e5 b4a4d4d3a3 c5a4e5d1 c4d2c5b1a3b1 d4d2 e3e5b5 e1c4e3d2d1d2b1d1 d4d2 e3 c4e3 d3a4e5c4a3e5b1 d4d2 e3 b1d2a3d4
c1e5d2 c5a4e5d1 d1a4d2a1 e1a3b1d1a4d4d4a3c4  c5a4e5d1 c5a4e5d1 d3a3c5a3a5 a1a4e5a1 e3 b3a3d1e3b1

a3a1 c1e5a3 d3d2d1a2a3  e1e5d2d1c1e5a3 b3a3d1e3b1 c5a4e5d1 c4 e3c5a4e5a3a5 b2e3e5a1a3b4a3d4a1 c5a4e5d1 a3d1a1 e1c4e5d1
b3b2a3b1 c1e5a3 c5a4a1b1a3 c5d2a3 a1e3d4a1 c1e5 d2c4 b1a3d1e1d2b1a3 c5a4e5d1 d4a3 d1e3e5b1d2a3a5 d1e3d4d1 d2d4a2e5d1a1d2b3a3
c5a4e5d1 e1c4e3d2d4d3b1a3 d3a3 c4e3 e2a4b1a1e5d4a3 a1a4e5d1 c4a3d1 c5a4a1b1a3d1 b1a3c5d2c5a3d4a1
a3d4 c4e5d2  c5a4e5d1 d4 e3c5a3a5 b1d2a3d4 e1a3b1d3e5 c5a4d1 d5a3e5b5 d3a4d2c5a3d4a1 a3a1b1a3 d1a3b3d1 d1a3b1a3d2d4d1
b4a3b4a3  c5a4e5d1 a1b1a4e5c5a3a5 a1a4e5a1 a3d4 c4e5d2 d2c4 c5a4e5d1 a1d2a3d4a1 c4d2a3e5 d3a3 a1a4e5a1
d2c4 b1a3e1e5c2d4a3b1e3d2a1 a1b1a4e1 e3 c5a4a1b1a3 d1e3c2a3d1d1a3 e3 c5a4a1b1a3 e3b4a3 d1a3d4d1d2c3c4a3 a3a1 b1a3b3a4d4d4e3d2d1d1e3d4a1a3
d3a3 b4a3b3a4d4d4e3a1b1a3 c5a4a1b1a3 e2a3c4d2b3d2a1a3 a2e5d1c1e5 e3 a4d1a3b1 d3a3e1c4a4b1a3b1 c5a4a1b1a3 d1a4b1a1 d3e5 c5d2c5e3d4a1 d3a3 b3a3d1e3b1


a2a3 c5a4e5d1 d2d4d3d2c1e5a3b1e3d2 a3d4b3a4b1a3 e5d4 e3e5a1b1a3 b1a3b4a3d3a3 d4a4d4 d1e3d4d1 d3a4e5a1a3
e1c4e5d1 e1e5d2d1d1e3d4a1 b4e3d2d1 d3 e5d4 e5d1e3c2a3 e1c4e5d1 e2e3b4d2c4d2a3b1 b3 a3d1a1 d1a4e5d1 c5a4a1b1a3
a1a4d2a1 c1e5a3 c5a4d1 b3b2e3c2b1d2d4d1 b4a3d4e3b3a3d4a1 d3a3 c5a4e5d1 d1e3d2d1d2b1 e3e5 b1a3a1a4e5b1  b3e3b1
a3d4 e1b1a3d1a3d4b3a3 d3a3 c5a4a1b1a3 d3d2c5d2d4d2a1a3 d2c4d1 d4a3 d1e3e5b1e3d2a3d4a1 a1b1a4e5c5a3b1 e3b3b3a3d1
b3a3d1e3b1 c4a3d1 b3a4b4e1b1d2b4a3 a1a4e5d1 a3d4 c5a4e5d1 b4e3d2d1 e5d4a3 e2a4d2d1 c4a4d2d4 d3a3 c4e5d2 c4e3
d3a4e5c4a3e5b1 b3a4b4b4a3 a1b1a4e5c5e3d4a1 c4 a4b3b3e3d1d2a4d4 a1a3d4d3b1e3 d3a3d1 e1d2a3c2a3d1 e3 c5a4a1b1a3
d2d1a4c4a3b4a3d4a1 a3a1 e1a3e5 e3 e1a3e5 a3c4c4a3 d1a3 c2c4d2d1d1a3b1e3 d3e3d4d1 c5a4a1b1a3 e3b4a3 c4d2c5b1a3a3
e3e5 b1a3e1a4d1

d4a3 c4e3d2d1d1a3a5 d3a4d4b3 e3e5b3e5d4a3 e1e3b1a1d2a3 d3a3 c5a4a1b1a3 a1a3b4e1d1 d2d4a4b3b3e5e1a3a3
e1e3b1 c4 a3a1e5d3a3  b3 a3d1a1 b4e3d2d4a1a3d4e3d4a1 c1e5a3 c5a4d1 b4e5d1a3d1 b3b2a3b1d2a3d1 d1d2
c4a4d4c2a1a3b4e1d1 a3a1 d1d2 e2d2d3a3c4a3b4a3d4a1 e3d2b4a3a3d1 c5a4e5d1 e1e3d2a3b1a4d4a1 d3a3 b1a3a1a4e5b1
b4e3d2d4a1a3d4e3d4a1 c1e5 a3c4c4a3d1 b1a3b3c4e3b4a3d4a1 c4a3e5b1 a5a3c4e3a1a3e5b1 a3a1 c4a3e5b1 e1a4d4a1d2e2a3
b4e3d2d4a1a3d4e3d4a1 c1e5a3 c5a4e5d1 d4a3 d3a3c5a3a5 e1c4e5d1 c1e5d2a1a1a3b1 b2a4b4a3b1a3 a3a1 c5d2b1c2d2c4a3
c1e5d2 a4d4a1 c3d2a3d4 b4a3b1d2a1a3 d3e5 c2a3d4b1a3 b2e5b4e3d2d4 b3a4b4b4a3 c5a4e5d1 d3a3 a1a4e5a1a3d1
c4a3d1 d4e3a1d2a4d4d1 a3a1 d3 a3e5b5b4a3b4a3d1 b3e3b1 c5a4e5d1 c4a3d1 e3c5a3a5 e2e3d2a1 b3a4d4d4e3a1b1a3 e3
d3a3d1 e1a3e5e1c4a3d1 e1a4e5b1 c4a3d1c1e5a3c4d1 d2c4d1 d4 e3c5e3d2a3d4a1 e1a4d2d4a1 a3b3b1d2a1 d4a3 b1a3d3a4e5a1a3a5
b1d2a3d4 e1a4e5b1 a1a4e5d1 c4a3d1 b4a4b4a3d4a1d1 c1e5a3 c5a4e5d1 b4a3a1a1b1a3a5 d1a4e5d1 c4a3e5b1 d1e3e5c5a3c2e3b1d3a3
b3 a3d1a1 b4e3d2d4a1a3d4e3d4a1 c1e5a3 c4a3d1 e2e3d2a1d1 d3a3 b3a3d1e3b1 b1a3b3c4e3b4a3d4a1 a1a4e5d1
c5a4d1 a3e2e2a4b1a1d1 d2c4 e2e3e5a1 c1e5a3 a1a4e5d1 c4a3d1 d1d2a3b3c4a3d1 a3d4 d1a4d2a3d4a1 d2d4e2a4b1b4a3d1 e1e3b1
e5d4 a1a3b4a4d2c2d4e3c2a3 d3a4b4a3d1a1d2c1e5a3  b3a3c4a3c3b1a3a5c4a3d1 c4e5d2b4a3b4a3 e1a4e5b1 c4e3
e2a4b1b4a3 a3a1 c4a3 e1c4e3d4 d3a3 b3a3d1 e3d4d4e3c4a3d1 c5a4e5d1 d3a4d4d4a3b1e3 a3a1 c4e3 b4e3a1d2a3b1a3 a3a1 c4 a3b5a3b4e1c4a3

a2a3 d4 d2b1e3d2 e1e3d1 a2e5d1c1e5 e3 c5a4e5d1 b3a4d4d1a3d2c4c4a3b1 d3 e3e1e1c4d2c1e5a3b1 e3 c4e3
b3a4b4e1a4d1d2a1d2a4d4 d3a3 e2e3c3c4a3d1 d3 e3e1a4c4a4c2e5a3d1 d3e3d4d1 c4a3 c2a4e5a1 d3 a3d1a4e1a3 c2a3d4b1a3
c1e5a3 d4 a4d4a1 e1e3d1 a3d1d1e3d5a3 c4a3d1 b1a4b4e3d2d4d1 b3a3a1a1a3 c2b1e3b3a3 d3a3 d1a1d5c4a3 c1e5d2
c5a4e5d1 a3d1a1 e1b1a4e1b1a3 d2c4 a3d1a1 d3d2e2e2d2b3d2c4a3 d1e3d4d1 d3a4e5a1a3 e3 e5d4a3 e3b4a3 d1d2 b1e5d3a3b4a3d4a1
e2b1e3e1e1a3a3 d3 e3c3a4b1d3a3b1 a1a4e5a1 e3 b3a4e5e1 d3a3d1 a3b5a3b1b3d2b3a3d1 d3a3 e1e5b1 e3c2b1a3b4a3d4a1
a1a4e5a1a3e2a4d2d1 a1a3d4a3a5c5a4e5d1 d1e5b1 c1e5 a3c4c4a3 a3d1a1 d3a3a2e3 b1e3e2e2a3b1b4d2a3 a3a1
b1a3d4d3e5a3 e3 a3c4c4a3b4a3b4a3 d1d2 d3a3 b3a4b4e1a4d1d2a1d2a4d4d1 e1c4e5d1 e3e5d1a1a3b1a3d1 a3c4c4a3 e1a3e5a1
d3a3d1b3a3d4d3b1a3 e3 d3a3 b4a4d2d4d1 c2b1e3c5a3d1 d1e5a2a3a1d1

c5a4a1b1a3 d2b4e3c2d2d4e3a1d2a4d4 c1e5a4d2c1e5a3 b4e3c4e3d3a3 a3d4b3a4b1a3 a3a1 a3d4 c4e5a1a1a3 b3a4d4a1b1a3 a3c4c4a3b4a3b4a3
d1a3 d1a3d4a1d2b1e3 d3d2d1a1b1e3d2a1a3 e1e3b1 c4a3 d1a3b1d2a3e5b5 d3a3 d1a3d1 a1b1e3c5e3e5b5 b4e3d2d1 c4a3d1 b3b2a4d1a3d1 c1e5d2
c5a3e5c4a3d4a1 a3a1b1a3 a1b1e3d2a1a3a3d1 d3 e5d4 a3d1e1b1d2a1 d1a3b1a3d2d4 c4e5d2 b1a3e1e5c2d4a3b1a4d4a1 a1e3d4a1
c1e5 a3c4c4a3 d4a3 d1a3b1e3 e1e3d1 a3d4a1d2a3b1a3b4a3d4a1 b1a3d4a1b1a3a3 d3e3d4d1 d1a4d4 e3d1d1d2a3a1a1a3
c1e5 a3c4c4a3 b3a4b4b4a3d4b3a3 d3a4d4b3 e1e3b1 d3a3d1 d1e5a2a3a1d1 d1a3c5a3b1a3d1 e1a4e5b1 d1a3 d3a3a1a3d4d3b1a3
e3e1b1a3d1 d1e5b1 d3a3 e1c4e5d1 b1d2e3d4a1a3d1 e1b1a4d3e5b3a1d2a4d4d1


b3a3 d1a3b1e3 a3d4 a4e5a1b1a3 e5d4 c2b1e3d4d3 b4a4a1d2e2 d3a3 d1a4e5c4e3c2a3b4a3d4a1 d3a3 c5a4e5d1 d3a3b4e3d4d3a3b1
d1a4e5c5a3d4a1 e3 c5a4e5d1b4a3b4a3  a3d1a1b3a3 e1a4e5b1 b4a4d2 c1e5a3 a2a3 b4 e3e2e2c4d2c2a3
a4e5 e1a4e5b1 b3a3c4e5d2 c1e5d2 e3 b3a3d1d1a3 d3 a3a1b1a3 d1d2 b3 a3d1a1 e1a4e5b1 b4a4d2 e3e5e1b1a3d1
d3a3 c1e5d2 a3d1a1 c4a3 b4a3b1d2a1a3 d3a3 c4e3 e2e3d2c3c4a3d1d1a3 d3a4d4a1 a2a3 b4a3 e1e3b1a3 a3c4c4a3
d3a3c5b1e3d2a1 e1a4e5b1 a3a1b1a3 a3b5b3e5d1e3c3c4a3 e1e3b1a1d2b1 d3 e5d4 e1c4e5d1 d4a4c3c4a3 e2a4d4d3
c1e5e3d4d3 d3a3d1 e1a3d4d1a3a3d1 d3 d2d4a1a3b1a3a1 d1 d5 b4a3c4a3d4a1 c4a3 b3a4a3e5b1 d5 d3a3c5d2a3d4a1
a3a1b1e3d4c2a3b1 a4b1 b1d2a3d4 d4a3 d1d2a3d3 b4a4d2d4d1 e3 c4 b2a4d4d4a3a1a3 b2a4b4b4a3 c1e5a3 d3a3
e2e3d2b1a3 d3a3 c4e3 b4a4b1a1 d3 e5d4 e2b1a3b1a3 c4 a4c3a2a3a1 d3 e5d4 b3e3c4b3e5c4

d1d2 b3 a3d1a1 e1a4e5b1 c4e5d2 c1e5a3 a2a3 b4a3 c4e3b4a3d4a1a3 a2a3 d3a4d2d1 e3d3b4a3a1a1b1a3 d3e3d4d1 c4 e3e1e1b1a3b3d2e3a1d2a4d4
d3a3 b4e3 b3a4d4d3e5d2a1a3 c4 e5d4 d3a3 b3a3d1 d3a3e5b5 e1a4d2d4a1d1 a4e5 c4a3d1 b4a4b1a1d1 d1a4d4a1 e1b1d2c5a3d1 d3a3
a1a4e5a1 d1a3d4a1d2b4a3d4a1 a3a1 b4a4d4 e2b1a3b1a3 a3b3b2e3e1e1a3 e3 a1a4e5a1a3d1 c4a3d1 d3d2d1c2b1e3b3a3d1
d3a3 c4e3 c5d2a3 d1a3 b1a3a1b1a4e5c5a3 e3e5b5 b4a3b4a3d1 c4d2a3e5b5 a4e5 d2c4 a3a1e3d2a1 e3c5e3d4a1 d3a3
d4e3a1b1a3 c4d2c3b1a3 d3a3 a1a4e5a1 b4e3c4 d1e3d4d1 b3b1e3d2d4a1a3 d1e3d4d1 d3a3d1d2b1 d1e3d4d1 d1a4e5e2e2b1e3d4b3a3
e3e5b3e5d4a3 c1e5a3c4c4a3 a3d1a1 e3c4a4b1d1 b4e3 d3a3b4a3d4b3a3 d3a3 d4a4e5b1b1d2b1 e5d4a3
d3a4e5c4a3e5b1 d1e3d4d1 e2d2d4 e1a4e5b1 c1e5d2 d4 a3d4 a3e1b1a4e5c5a3b1e3 a2e3b4e3d2d1

 a4e5 c4a3 a1b1a3e1e3d1 d4a4e5d1 c4e3d2d1d1a3 a3d4b3a4b1a3 c1e5a3c4c1e5a3 d1a3d4a1d2b4a3d4a1 a3a1 e3d2d4d1d2 c4 e3b4a3 d3a3 b4a4d4
e2b1a3b1a3 b1a3d4c5a4d5a3a3 b3a4b4b4a3 d3 e5d4a3 c4a4d4c2e5a3 e1b1d2d1a4d4 a2a4e5d2a1 a3d4e2d2d4 d3 a3c4c4a3b4a3b4a3
d3a3 d1a4d4 d2d4d3a3e1a3d4d3e3d4b3a3 d3e5 d1e1a3b3a1e3b3c4a3 d3a3 c4e3 d4e3a1e5b1a3 a3a1 a1e3d4d3d2d1
c1e5 d2c4 b1a3c2e3b1d3a3 d3 a3d4 b2e3e5a1 c4a3d1 b3b2a4d1a3d1 d3a3 c4e3 a1a3b1b1a3 d2c4 b3a4d4a1a3b4e1c4a3
e3e5d1d1d2 d3a3 e1c4e5d1 e1b1a3d1 c4a3d1 b3a3c4a3d1a1a3d1 b4d5d1a1a3b1a3d1 d3a4d4a1 d2c4 e3 d1d2 c4a4d4c2a1a3b4e1d1
a3a1 d1d2 c5e3d2d4a3b4a3d4a1 b3b2a3b1b3b2a3 c4e3 b3c4a3e2 e1a4e5b1c1e5a4d2 d3a4d4b3 b4a3 b3a4d4d1e5b4a3a2a3
e3 b1a3c2b1a3a1a1a3b1 e5d4 e2b1a3b1a3 c1e5d2 a3d1a1 b2a3e5b1a3e5b5 a4e5 c1e5d2 d4 a3d1a1 e1c4e5d1 b1d2a3d4
c4 a3d4c5d2a3 d1a3e5c4a3 e1c4a3e5b1a3b1e3d2a1 d1a4d4 c3a4d4b2a3e5b1 e1c4a3e5b1a3b1 c4a3 d4a3e3d4a1 a3d1a1 e2a4c4d2a3

 c5a4a1b1a3 b3b2e3c2b1d2d4 c5d2a3d4a1d2c4 d3a3 b3a3 c1e5a3 c5a4e5d1 c5a4e5d1 e2d2c2e5b1a3a5
c5a4a1b1a3 e2b1a3b1a3 d3a3e1a4e5d2c4c4a3 d3a3d1 c3b1d2c4c4e3d4a1d1 e3c5e3d4a1e3c2a3d1 c1e5d2 c4 a3d4a1a4e5b1e3d2a3d4a1
d3a3 a1a4e5a1 c4a3e5b1 a3b3c4e3a1 b4e3d2d1 d1a4d4c2a3a5 c1e5a3 d1 d2c4 e3 e1a3b1d3e5 c3d2a3d4 d3a3d1
b3b2a4d1a3d1 d2c4 a3d4 a3d1a1 d3e3c5e3d4a1e3c2a3 c1e5 d2c4 d4a3 b3b1e3d2d4a1 e1c4e5d1 e1a4d2d4a1 d3a3 b1a3d1d1a3d4a1d2b4a3d4a1
c1e5d2 c4a3 a1a4e5b1b4a3d4a1a3 d3a3 b4e3c4e3d3d2a3 c1e5d2 c4 e3c3e3a1a1a3 d3a3 d1a4e5e1a4d4
c1e5d2 c4a3 b2e3b1b3a3c4a3 c4 a3d4c5d2a3 e3e5 e2d2a3c4 b1a4d4c2a3e5b1 b3a4d4d1a1e3d4a1a3 a3d4d4a3b4d2a3 d3a3
a1a4e5a1 b3a3 c1e5d2 d1 a3c4a3c5a3 d4a3 d1 e3b3b2e3b1d4a3b1e3 e1c4e5d1 d1e5b1 c4e5d2  c4e3 b3b1e3d2d4a1a3 d4a3
c4 e3d2c2e5d2c4c4a4d4d4a3b1e3 e1c4e5d1  c4e3 c4a3c2a3b1a3a1a3 d3a3 c4e3 e2a4b1a1e5d4a3 d1d2 e1b1a4b4e1a1a3 e3
b3b2e3d4c2a3b1 d3a3 e2e3c5a4b1d2d1 d4a3 a1b1a4e5c3c4a3b1e3 e1c4e5d1 d1a4d4 b1a3e1a4d1 b3e3c4b3e5c4a3a5 c3d2a3d4
a4d4 c4e5d2 e3 e2e3d2a1 c2b1e3b3a3 e1c4e5a1a4a1 c1e5a3 d3a4b4b4e3c2a3

 d2c4 d4a3 a2a4e5d2b1e3 d4d2 d3a3 d1a4d4 a4e1e5c4a3d4b3a3 d4d2 d3a3 d1a4d4 b3b1a3d3d2a1 d4d2 d3e5 c5a4a1b1a3 d2c4 d4a3 b1a3d4d3b1e3
d2c4 d4a3 b1a3b3a3c5b1e3 e1c4e5d1 d3a3 c3d2a3d4e2e3d2a1d1 a3d1a1d2c4 e3 e1c4e3d2d4d3b1a3 d3 e3c5a4d2b1 e1a3b1d3e5 a1a4e5a1
b3a3c4e3 a4e5 b2a3e5b1a3e5b5 d3a3 d4a3 e1e3d1 c4a3 b1a3c2b1a3a1a1a3b1  b3b1a4d5a3a5b4a4d2 e1c4e5d1 b2a3e5b1a3e5b5
a3d1a1 c4 b2a4b4b4a3 e3 c1e5d2 c4e3 e2a4b1a1e5d4a3 a3d1a1 d2d4e5a1d2c4a3 c1e5a3 b3a3c4e5d2 c1e5d2
c4 e3 d1a4e5d1 c4e3 b4e3d2d4 a1a4e5d1 b3a3d1 e2e3e5b5 c3d2a3d4d1 d1d2 d1e1a3b3d2a3e5b5 c1e5d2 d4a4e5d1
e3b4e5d1a3d4a1 d3a3 c4a3e5b1d1 a1b1a4b4e1a3e5d1a3d1 d3a4e5b3a3e5b1d1 a1b1a3d1a4b1d1 d3d2c2d4d2a1a3d1 e1e5d2d1d1e3d4b3a3
a3a1 a1e3d4a1 d3 e3e5a1b1a3d1 d1a3d3e5b3a1d2a4d4d1 d3a3c5e3d4a1 c4a3d1c1e5a3c4c4a3d1 c4 e3c5a3e5c2c4a3
b3e5e1d2d3d2a1a3 b2e5b4e3d2d4a3 d1 a3c3e3b2d2a1 d4a3 d1a3 b3a4d4d1a3b1c5a3d4a1 c1e5 e3 c2b1e3d4d3 e1a3d2d4a3
d1a4d4a1 c5e5d1 e3c5a3b3 a3d4c5d2a3 b3a3e5b5 b4a3b4a3 c1e5 d2c4d1 d3a3b3a4b1a3d4a1 a3d4 d1a4d4a1 e3b3b3e3c3c4a3d1
d2c4d1 b4a3d4e3b3a3d4a1 e1c4e5d1 c1e5 d2c4d1 d4a3 d1a3b1c5a3d4a1  c2c4d2d1d1e3d4a1d1 a3a1 e2e5c2d2a1d2e2d1
c1e5d2 a2e3b4e3d2d1 e1a3e5a1 c4a3d1 c3d2a3d4 d1e3d2d1d2b1  b3e3b1 d4 a3e5a1a4d4 d3e3d4d1 c4 e3c5a3d4d2b1
b1d2a3d4 e3 b3b1e3d2d4d3b1a3 e5d4a3 c2b1e3d4d3a3 e2a4b1a1e5d4a3 e3 b4e3d2d4a1a3d4d2b1 b3a4e5a1a3 c3d2a3d4 d3a3d1 d1a4e5b3d2d1

 c5a3e5d2c4c4a3a5 a3d4 b3b1a4d2b1a3 b3a3e5b5 c1e5d2 e3e1e1b1a4e2a4d4d3d2d1d1a3d4a1 c4a3
b4d2a3e5b5 c4e3 c5a3b1d2a1a3 a1a4e5a1a3 c5d2a3 a3d1a1 e5d4 d1e5e1e1c4d2b3a3 c4e3d4b3a3d1 d1e5b1 b3a3a1a1a3
b4a3b1 e1b1a4e2a4d4d3a3 a3a1 d1e3d4d1 b1a3e1a4d1 d3e3d4d1 c4a3d1 a4d1b3d2c4c4e3a1d2a4d4d1 d3e5 e2c4e5b5 a3a1 d3e5
b1a3e2c4e5b5 a1e3d4a1a4a1 e1a4b1a1a3d1 e1e3b1 e5d4a3 d1e5c3d2a1a3 a3c4a3c5e3a1d2a4d4 a1e3d4a1a4a1 e1b1a3b3d2e1d2a1a3d1
e1c4e5d1 c3e3d1 c1e5 e3e5e1e3b1e3c5e3d4a1 e1a4e5d1d1a3d1 b1a3e1a4e5d1d1a3d1 d1e3d4d1 b3a3d1d1a3
d4e5c4c4a3 e1e3b1a1 d4a4e5d1 d4a3 e1a4e5c5a4d4d1 a2a3a1a3b1 c4 e3d4b3b1a3  d4a4e5d1 e2c4a4a1a1a4d4d1 d1e5d1e1a3d4d3e5d1
e3e5b5 c5e3c2e5a3d1 d4a4e5d1 d4a4e5d1 b2a3e5b1a1a4d4d1 c4a3d1 e5d4d1 b3a4d4a1b1a3 c4a3d1 e3e5a1b1a3d1
e2e3d2d1e3d4a1 a1b1a4e1 d1a4e5c5a3d4a1 d4e3e5e2b1e3c2a3 c4a3 b1a3d3a4e5a1e3d4a1 a1a4e5a2a4e5b1d1 e3e5
b4d2c4d2a3e5 d3a3 b3a3d1 e2c4a4a1d1 d1d2 a4b1e3c2a3e5b5 a3a1 a3b5e1a4d1a3d1 e3 a1a4e5a1a3d1 c4a3d1 a1a3b4e1a3a1a3d1
c4a3 d4e3c5d2c2e3a1a3e5b1 d4 e3 d3a3 e1a4b1a1 c1e5a3 c4a3 a1b1a3e1e3d1

 d4a3 e1c4a3e5b1a3a5 d3a4d4b3 e1e3d1 b3a4b4b4a3 e2a3b1e3d2a1 c4 a3d4c5d2a3 c4a3 c3a4d4b2a3e5b1 d3 e5d4
e2b1a3b1a3  d2c4 b1a3e1a4d1a3  d2c4 a3d1a1 a3d4e2d2d4 c4d2c3b1a3 b2a4b1d1 d3a3 e1a3b1d2c4 d2b4b4a4b1a1a3c4  d2c4
c5a4d2a1 c1e5a3 b3a3d1e3b1 a3a1 a1a4e5d1 c4a3d1 b1a3a2a3a1a4d4d1 d3a3 b3a3d1e3b1 c4e5d2 d1e5b1c5d2c5a3d4a1 d2c4
c5a4d2a1 c4e5d2 d1e5b1c5d2c5b1a3 e1a4c4d5c3a3 a3a1 a1a4e5d1 d1a3d1 e2b1a3b1a3d1 e3c5e3d4a1 c1e5 a3c4c4a3 b3b2e3d4c2a3e3a1
b1d2a3d4 d3a3 d1a3d1 e2e3c5a3e5b1d1 d2c4 e3 c1e5d2a1a1a3 c4e3 e2a4b1a1e5d4a3 d2b4b4a4c3d2c4a3 a3d4b3a4b1a3
a3a1 c1e5d2 c4e5d2 c5a3b1d1e3d2a1 d1a3d1 d3a4d4d1 e3 e1c4a3d2d4a3d1 b4e3d2d4d1

 d2c4 a2a4e5d2a1 b4e3d2d4a1a3d4e3d4a1 d3 e5d4 b3d2a3c4 e1e5b1 a3a1 d1e3d4d1 d4e5e3c2a3 d2c4 e3 d3a3 b3a3a1a1a3 b2e5b4c3c4a3 a3a1
c3e3d1d1a3 b1a3c2d2a4d4 e1b1d2d1 d1a4d4 c5a4c4 c5a3b1d1 c4a3 d1a3a2a4e5b1 b4d5d1a1a3b1d2a3e5b5 c1e5d2 a4e5c5b1a3
e3e5b5 e3b4a3d1 d3a3c2e3c2a3a3d1 d3a3 c4a3e5b1d1 e2a3b1d1 d1a3d1 d3a3b4a3e5b1a3d1 c3d2a3d4b2a3e5b1a3e5d1a3d1
d3e3d4d1 d1a4d4 c5e3c2e5a3 a3a1 c4d2c3b1a3 a3d1d1a4b1 d2c4 d3a3b3a4e5c5b1a3 a1a4e5d1 c4a3d1 a1b1a3d1a4b1d1 d3a3
c4e3 d4e3a1e5b1a3 e3c5a3b3 e5d4 d1e5e1b1a3b4a3 b1e3c5d2d1d1a3b4a3d4a1 d3a3a1b1a4b4e1a3a5c5a4e5d1 d2c4
d4 e3 e1a4d2d4a1 e1a3b1d3e5 c4e3 c4e5b4d2a3b1a3 d2c4 a3d4 b1a3d1e1d2b1a3 e5d4a3 e1c4e5d1 e1e3d2d1d2c3c4a3


 c5a3b1d1 c4e3c1e5a3c4c4a3 d4a4e5d1 d4a4e5d1 e3b3b2a3b4d2d4a4d4d1 a1a4e5d1 c1e5a3 e1c4e3d2c2d4a4d4d1d4a4e5d1
d1a4d4 d1a4b1a1 d2c4 d4a3 d4a4e5d1 e3 e1e3d1 c1e5d2a1a1a3d1 d2c4 e3 e1b1d2d1 c4a3d1 d3a3c5e3d4a1d1
b3 a3d1a1 b3b1a4d5a3a5b4a4d2 e5d4 c2b1e3d4d3 c3a4d4b2a3e5b1 c1e5a3 d3a3 b4a4e5b1d2b1
e3e5 a1a3b4e1d1 d3a3 c4e3 e2a3c4d2b3d2a1a3 b1d2a3d4 d4 a3d1a1 d1e5b1 d2b3d2c3e3d1 e2e5a1b3a3 e1a4e5b1 e5d4
d1a3e5c4 a2a4e5b1 d3e3d4d1 c4 d2b4e1a3d4a3a1b1e3c3c4a3 a4c3d1b3e5b1d2a1a3 d3a3 b3a3 c1e5d2 d3a4d2a1 a3a1b1a3
c1e5d2 d3a3c5d2d4a3b1e3 d1d2 e1a4e5b1 c5a4a1b1a3 e2b1a3b1a3 c4e3 b4a4b1a1 e3 a3a1a3 a2e3c4a4e5d1a3 a4e5 c3d2a3d4c5a3d2c4c4e3d4a1a3

 a3a1 e5d4a3 b3a4d4d1a4c4e3a1d2a4d4 d2d4e2e3d2c4c4d2c3c4a3 e1a4e5b1 c5a4e5d1 c1e5d2 a3a1a3d1
a2e5d1a1a3 a3d4 a1a4e5a1a3d1 b3b2a4d1a3d1 d1a3b1e3 d3a3 e1a3d4d1a3b1 d4a4d4 c1e5 e5d4 a1a4b1a1 c5a4e5d1 e3
a3a1a3 e2e3d2a1 e1e3b1 c4e3 e1a3b1a1a3 d3 e5d4 a1a3c4 e2b1a3b1a3 b4e3d2d1 c1e5a3 c5a4e5d1 a3a1a3d1 b1a3d3a3c5e3c3c4a3
e3e5 b3d2a3c4 d3 e3c5a4d2b1 a2a4e5d2 c4a4d4c2a1a3b4e1d1 a3a1 e1c4a3d2d4a3b4a3d4a1 d3a3 d1e3 a1a3d4d3b1a3d1d1a3

a2 e3e1e1a3c4c4a3 d2d4a2e5d1a1d2b3a3 d3d2d1e1e5a1a3b1 e3e5 c3d2a3d4e2e3d2a1a3e5b1 a1a4e5a1 d3b1a4d2a1 e5c4a1a3b1d2a3e5b1
d1e5b1 d1a3d1 d3a4d4d1  e3c5d2d3d2a1a3 d4a3 e1e3d1 a1a3d4d2b1 e1a4e5b1 c2e3d2d4 d3 e3c5a4d2b1 b1a3e5 b4e3d2d1
e1a4e5b1 d3a4b4b4e3c2a3 d3 e3c5a4d2b1 b1a3d1a1d2a1e5a3  d2d4c2b1e3a1d2a1e5d3a3 d4a4b4b4a3b1 d3d2d1c2b1e3b3a3
c4a3 a1a3b1b4a3 d3a3 c4e3 a2a4e5d2d1d1e3d4b3a3  a2 e3e1e1a3c4c4a3 d3a3b1e3d2d1a4d4 d1 d2b4e3c2d2d4a3b1
c1e5 a4d4 d4a3 e1a3e5a1 c2a4e5a1a3b1 c1e5a3 d3a3d1 c3d2a3d4d1 e3b3a1e5a3c4d1 e3e5 c4d2a3e5 d3a3 d1a3 b1a3e1a4d1a3b1
e3e5d1d1d2 d1e5b1 c4a3d1 e2b1e5d2a1d1 d3e5 e1e3d1d1a3 a3a1 d3 e3e1e1b1a3b3d2a3b1 c4e3 e2d2b5d2a1a3 d3a3
b3a3 c1e5d2 e2e5a1 a2e3d3d2d1  b3e3b1 c4e3 d3e5 b4a4d2d4d1 e1c4e5d1 d3a3 b1a3c5a4c4e5a1d2a4d4 e3 b3b1e3d2d4d3b1a3

 a4d4 b1a3d1d1a3b1b1a3 a1b1a4e1 d1a3d1 a2a4e5d2d1d1e3d4b3a3d1 d1d2 a4d4 d4 a3d4 b3b1a4d2a1 a1b1a4e5c5a3b1
c1e5 e3e5b5 b3b2a4d1a3d1 c1e5a3 c4 a4d4 a1d2a3d4a1 a3a1 c1e5 a4d4 c5a4d2a1 d1d2 c4a3d1 e3c5a4d2b1 e1a4d1d1a3d3a3a3d1
a3d1a1 b3a4b4e1a1a3 e1a4e5b1 b1d2a3d4 b3e3b1 a1a4e5a1 e1c4e3d2d1d2b1 a3d1a1 e1b1a4b4e1a1 e3 d4a4e5d1
c1e5d2a1a1a3b1 d2c4 e2e5d2a1 d2c4 d1 a3d4c5a4d2a3 a3a1 e1b1a3d1c1e5a3 e3c5e3d4a1 d3 e3b1b1d2c5a3b1 d2c4 d4 a3d1a1
e1c4e5d1 c1e5a3 c4 d2b4e3c2d2d4e3a1d2a4d4 d1a3 b1a3e1a4b1a1a3 d3a4d4b3 d1e5b1 c4a3 e1e3d1d1a3  a1a4e5a1 b3a3
c1e5d2 a2e3b4e3d2d1 e3 e1e5 d4a4e5d1 b3b2e3b1b4a3b1 b1e3e1e1a3c4a4d4d1c4a3 a3a1 c1e5a3 d3a3 e2b1a3c1e5a3d4a1a3d1
b4a3d3d2a1e3a1d2a4d4d1 d4a4e5d1 c4a3 e2e3d1d1a3d4a1 b4d2a3e5b5 d1e3c5a4e5b1a3b1 c4a3d1 e1c4e3d2d1d2b1d1
d4 a4d4a1 d3a3 b3a4d4d1a1e3d4a1 a3a1 d3a3 e2d2d3a3c4a3 c1e5a3 c4a3e5b1 d1a4e5c5a3d4d2b1 c4a3e5b1
e1b1a3d1a3d4b3a3 d3e5b1a3 a1b1a4e1 e1a3e5

c5a4e5d1 e3c5a3a5 e1a4d1d1a3d3a3 e5d4 a3b5b3a3c4c4a3d4a1 e2b1a3b1a3
b3a4b4e1a1a3a5 b3a3c4e3 e1a4e5b1 e5d4a3 e2a3c4d2b3d2a1a3 d3a3d1 e1c4e5d1 c2b1e3d4d3a3d1 a3a1 e3e5 c4d2a3e5 d3a3
d3d2b1a3  a2a3 e1a4e5c5e3d2d1 c4 e3c5a4d2b1 e1c4e5d1 c4a4d4c2a1a3b4e1d1  d1a4d4c2a3a5 b3a4b4c3d2a3d4
d3a3 a1a3b4e1d1 c5a4e5d1 c4 e3c5a3a5 a3e5 c4e3 d4e3a1e5b1a3 c5a4e5d1 c4 e3c5e3d2a1 b3a4b4b4a3 e3 a1a4e5d1
c4a3d1 e2b1a3b1a3d1 d4a4d4 d3a4d4d4a3 e1a4e5b1 a1a4e5a2a4e5b1d1 b4e3d2d1 e1b1a3a1a3 d2c4 c4e5d2 e3 e1c4e5
d3a3 c4a3 b1a3d3a3b4e3d4d3a3b1 d1e3d4d1 e3a1a1a3d4d3b1a3 c1e5a3 c5a4e5d1 c5a4e5d1 a3d4 e2e5d1d1d2a3a5 b1e3d1d1e3d1d2a3
a3c4c4a3 e3 d1e5d2c5d2 d1e3 c4a4d2

c1e5 e5d4 d3a3c3d2a1a3e5b1 d1 d2d4d3d2c2d4a3 d3a3 b1a3b4c3a4e5b1d1a3b1
e5d4 e1b1a3a1 c1e5d2 d1e5b1a1a4e5a1 c4e5d2 e2e5a1 e2e3d2a1 c2b1e3a1e5d2a1a3b4a3d4a1 d4a3 e1e3d1d1a3b1e3a1d2c4
e1e3d1 e1a4e5b1 d2d4a2e5d1a1a3 b3 a3d1a1 e3 b3a3 a1d2a1b1a3 c1e5a3 c5a4e5d1 b1a3e5a1a3d1 c4e3
c5d2a3 c5a4a1b1a3 e2b1a3b1a3 a3a1 c5a4e5d1  c4e3 d4e3a1e5b1a3 e3 e5d1a3 d3a3 d1a4d4 d3b1a4d2a1 a3d4 a3b5d2c2a3e3d4a1
e1c4e5d1 a1a4a1 d1a3d1 e3c5e3d4b3a3d1 d3a3 b3a3c4e5d2 c1e5 a3c4c4a3 e3 c5a4e5c4e5  d4a3 c4 e3b3b3e5d1a3a5
e1e3d1 d1a3d1 b3a4d4d3d2a1d2a4d4d1 a3a1e3d2a3d4a1 b3a4d4d4e5a3d1  e3b3b3e5d1a3a5 c4 a3d1e1b1d2a1 b2e5b4e3d2d4
d1d2 e3c5d2d3a3 d3e3d4d1 d1a3d1 e1b1a3a1a3d4a1d2a4d4d1 d1d2 c5d2a1a3 a4e5c3c4d2a3e5b5 d3a3 b3a3 c1e5a3 d1a4d4a1
c4a3d1 b3b2a4d1a3d1 d3a3 b3a3 c1e5 a3d1a1 c4 b2a4b4b4a3 c4e5d2b4a3b4a3 c1e5e3d4d3 c4e3 d4e3a1e5b1a3 d4a3
c4 a3d4 e3c5a3b1a1d2a1 e1e3d1

b1a3a2a4e5d2d1d1a3a5c5a4e5d1 d3 e3c5a4d2b1 a3e5 e5d4 d1d2 c3a4d4 e2b1a3b1a3
a3a1 c4e3 a2a4e5d2d1d1e3d4b3a3 d3 e5d4 a1a3c4 c3d2a3d4 a1b1a4e1 b3a4e5b1a1a3 e3e5 c2b1a3 d3a3 c5a4d1 c5a4a3e5b5
d1e3b3b2a3a5 e3e5 b4a4d2d4d1 c4 e3e1e1b1a3b3d2a3b1 b1a3b3a4d4d4e3d2d1d1a3a5 c1e5a3 d1d2 c4e3 e1a4d1d1a3d1d1d2a4d4
e2e5a1 d3a3d1 e1c4e5d1 d3a4e5b3a3d1 c4e3 e1a3b1a1a3 e3e5d1d1d2 a3a1e3d2a1 d3e3d4d1 c4 a4b1d3b1a3 d3a3d1
b3b2a4d1a3d1 b2e5b4e3d2d4a3d1 d2c4 d5 e3 e5d4a3 d2d4b3a4d4d1a3c1e5a3d4b3a3 d3a3d1 e1c4e5d1 c2b1e3d4d3a3d1
e3 c5a4e5d1 e3e2e2a3b3a1a3b1 d3a3 b3a3 c1e5a3 c4a3 d1a4b1a1 c5a4e5d1 e3d2a1 e1a4e5b1 e1a3e5 d3 d2d4d1a1e3d4a1d1
c2b1e3a1d2e2d2a3 d3 e5d4 a1a3c4 e2b1a3b1a3 a3a1 e3 d4a3 e1e3d1 c5a4e5d1 e3e1e1c4e3e5d3d2b1 c1e5 d2c4 c5a4e5d1 a3d4
e3d2a1 c2b1e3a1d2e2d2a3

 b4e3d2d1 e5d4a3 e1a3b1a1a3 d1d2 d2b4e1b1a3c5e5a3   b2a3c4e3d1 a2a4e5a3a1
d3a3 d1a4d4 d2c4c4e5d1d2a4d4 d3e3d4d1 a1a4e5a1 b3a3 c1e5 d2c4 b3b2a3b1d2a1 c4 b2a4b4b4a3 a4e5c3c4d2a3 c5a4c4a4d4a1d2a3b1d1
d1e3 b3a4d4d3d2a1d2a4d4 b4a4b1a1a3c4c4a3 c4e3 d4e3a1e5b1a3 d4 e3 a3d4b3a4b1a3 e2e3d2a1 d1e3c5a4d2b1
e3 e1a3b1d1a4d4d4a3 c1e5 d2c4 d3a4d2c5a3 a3a1b1a3 a3b5a3b4e1a1 d3a3 d1a3d1 d2d4e2c4a3b5d2c3c4a3d1
d3a3b3b1a3a1d1 a2a4e5b1d4a3c4c4a3b4a3d4a1 e1e3d1d1a3d4a1 d3a3c5e3d4a1 d4a4d1 d5a3e5b5 c4a3d1 e2e5d4a3b1e3d2c4c4a3d1
d3 b2a4b4b4a3d1 b3a4d4d4e5d1 a4e5 d2d4b3a4d4d4e5d1 d3a3 d4a4e5d1 a3a1 d4a4e5d1 e1a3d4d1a4d4d1
e3 e3e5a1b1a3 b3b2a4d1a3 a3a1 d4a4e5d1 e3e1e1a3c4a4d4d1 d1e5c3d2a1a3 e5d4a3 b3e3a1e3d1a1b1a4e1b2a3
c1e5a3 b3b2e3c1e5a3 b2a3e5b1a3 d3a3 c4e3 c5d2a3 d4a4e5d1 b4a4d4a1b1a3 d2d4a3c5d2a1e3c3c4a3 d2c4 d4 d5 e3
d3a4d4b3 e1e3d1 c4e3 d2d4a2e5d1a1d2b3a3 d3e5 d1a4b1a1  d2c4 d5 e3 d3a3e1b1e3c5e3a1d2a4d4 d3 a3d1e1b1d2a1 b3b2a3a5
c4 b2a4b4b4a3 d2d4d1e3a1d2e3c3c4a3 a3d4 a1a4e5a1 a3a1 c1e5d2 d1 d2d4d3d2c2d4a3 d3a3 d1a4b1a1d2b1 d3 e5d4
c4d2a3e5 a4e5 d2c4 e2e5a1 e3d3b4d2d1 e3 a1d2a1b1a3 e1b1a3b3e3d2b1a3

 b3a4b4c3d2a3d4 a3a1e3d2a1 e1c4e5d1 a2e5d1a1a3 b3a3 d1e3c2a3 c1e5d2 e3e1e1b1a3d4e3d4a1 c4e3 b4a4b1a1
d3a3 d1a4d4 e2d2c4d1 e2d2a1 b3a3a1a1a3 b1a3e1a4d4d1a3 d3d2c2d4a3 d3 e5d4a3 e3b4a3 b2a3b1a4c1e5a3  a3d4
c4e5d2 d3a4d4d4e3d4a1 c4e3 c5d2a3 a2a3 d1e3c5e3d2d1 c1e5 d2c4 b4a4e5b1b1e3d2a1 e5d4 a2a4e5b1 e2e3e5a1d2c4
d1 a3a1a4d4d4a3b1 c1e5a3 d3 e5d4 a1a3c4 b2a4b4b4a3 d1a4d2a1 d1a4b1a1d2 e5d4 b3d2a1a4d5a3d4 c1e5d2 d1e5a1
b3a4e5b1e3c2a3e5d1a3b4a3d4a1 b4a4e5b1d2b1  c4e3 b4a4b1a1 d3 e5d4 e2d2c4d1 d4a3 e1e3b1e5a1 e1e3d1 e3e5
e1b2d2c4a4d1a4e1b2a3 c1e5a3c4c1e5a3 b3b2a4d1a3 d3a3 d4a4e5c5a3e3e5  b3e3b1 c1e5 d5 e3a1d2c4 d3a3 d4a4e5c5a3e3e5
c1e5 e5d4 b2a4b4b4a3 b4a3e5b1a3 c4e5d2 d3a4d4a1 a1a4e5a1a3 c4 a3b5d2d1a1a3d4b3a3 d4 a3d1a1
c1e5 e5d4 e3b3b2a3b4d2d4a3b4a3d4a1 c5a3b1d1 c4e3 b4a4b1a1  

 a3d4 c4e5d2 d3a4d4d4e3d4a1 c4e3 c5d2a3 a2a3 d1e3c5e3d2d1 c1e5 d2c4 b4a4e5b1b1e3d2a1 e5d4 a2a4e5b1 a3a1 d2c4 e3a2a4e5a1a3 e3c5a3b3
e1c4e5d1 d3a3 d1e3c2a3d1d1a3 a3d4b3a4b1a3 a3a1 d3a3 e2a3b1b4a3a1a3  a2a3 c4 e3d2 a3c4a3c5a3 e1a4e5b1 b3a3c4e3
a4e5d2 b3 a3d1a1 e1a4e5b1 b3a3c4e3 c1e5 a4d4 d4a4e5d1 a3c4a3c5a3 a1a4e5d1 c1e5d2b3a4d4c1e5a3 e3b1b1d2c5a3
e3 c4e3 c4e5b4d2a3b1a3 a3d1a1 e1b1a4b4d2d1 e3e5 a1b1a3e1e3d1 b2a3e5b1a3e5b5 d3e5 e1b1a3a1 c1e5d2 d4a4e5d1
a3d1a1 e2e3d2a1 b1a3d4d3a4d4d1c4a3 d3a3d1 c1e5 a4d4 c4a3 b1a3b3c4e3b4a3b1e3 c4a3 d1a4b1a1 d1e3d2d1d2b1e3
c4 e5d4 e1c4e5d1 a1a4a1 c4 e3e5a1b1a3 e1c4e5d1 a1e3b1d3 d2c4 d4 a4e5c3c4d2a3b1e3 e1a3b1d1a4d4d4a3 d1a4d5a4d4d1
d3a4d4b3 e1b1a3a1d1 e3 a1a4e5a1 d2d4d1a1e3d4a1 d4a3 b3b1e3d2c2d4a4d4d1 a2e3b4e3d2d1 c4 d2d4a3c5d2a1e3c3c4a3 a3a1
e3a1a1a3d4d3a4d4d1 a1a4e5a2a4e5b1d1 c4a3 e1a4d1d1d2c3c4a3

 b3d2a1a3b1e3d2a2a3 b3a3d1 c2a3d4a3b1e3e5b5 a3a1 c4a3d1 a3d4e2e3d4a1d1 d3a3 b3a3d1 c2a3d4a3b1e3e5b5 a3a1 a1e3d4a1 d3 b2a4b4b4a3d1
b3b2e3b1c2a3d1 d3a3 b3a4d4d1e5c4e3a1d1 a4e5 d3a3 a1b1d2a4b4e1b2a3d1 e1e3d5e3d4a1 a1b1d2c3e5a1 e3 c4 d2d4a3b5a4b1e3c3c4a3 d3a3d1a1d2d4
d3a3d1 b1a4d5e3e5b4a3d1 a3d4a1d2a3b1d1 e3c5a3b3 c4a3e5b1d1 b1a4d2d1 d3a3d1 e1a3e5e1c4a3d1 e3c5a3b3 c4a3d1 b1e3b3a3d1
c1e5d2 c4a3d1 b3a4b4e1a4d1a3d4a1 d1e5c3d2d1d1e3d4a1 c4e3 b4a3b4a3 e2e3a1e3c4d2a1a3  a1a4e5a1 b2a4b4b4a3
c1e5a3 d3d2d1a2a3  a1a4e5a1a3 b3b2a4d1a3 b4e3b1b3b2a3 e3 d1e3 d3a3b1d4d2a3b1a3 b2a3e5b1a3 b4e3d2d1 a1a4e5d1
d4 a4d4a1 e1e3d1 b4a3b4a3 e2d2d4 b3 a3d1a1 e3e5 b4d2c4d2a3e5 d3a3 d1e3 b3a4e5b1d1a3 c1e5a3 c4e3 c5d2a3 e3c3e3d4d3a4d4d4a3
c4 e5d4 a3c4c4a3 a3b3b2e3e1e1a3 e3 c4 e3e5a1b1a3 d3a3d1 c4a3 e1b1a3b4d2a3b1 e1e3d1 a1e3d4d3d2d1
c1e5 e5d4a3 a3b5a1b1a3b4a3 c5d2a3d2c4c4a3d1d1a3 d3a3a2e3 c4e3d1d1a3 d3a3 a2a4e5b1d1 a4c3a1d2a3d4a1 e3 e1a3d2d4a3
c4a3 b3a4d4c2a3 c1e5 a3c4c4a3 d3a3b4e3d4d3a3  b3a3c4e5d2b3d2 a1a4b4c3a3 e3e5 b4e3a1d2d4 b3a3c4e5d2c4e3
c4a3 d1a4d2b1 b4e3d2d1 a1a4e5d1 d1 e3c5e3d4b3a3d4a1 c5a3b1d1 e5d4 b4a3b4a3 a1a3b1b4a3 a2a3 d4a3 d1e3d2d1
d1 d2c4 d5 e3 e1c4e5d1 d3a3 e2a4c4d2a3 e3 b4a3b3a4d4d4e3a1b1a3 c4e3 c4a4d2 c1e5d2 d4a4e5d1 b3a4d4d3e3b4d4a3 e3
b4a4e5b1d2b1 c1e5a3 d3 d2b4e1e5d3a3d4b3a3 e3 d5 b1a3d1d2d1a1a3b1

 e1b1a3d4a3a5 a3d4 b4e3d2d4 e1b1a3d4a3a5 b3a3d1 a4a3e5c5b1a3d1 d3a4d4a1 c5a4d1 a1b1e3c5e3e5b5 d2d4c2a3d4d2a3e5b5
a4d4a1 e3b3b3b1e5 c4e3 b3a3c4a3c3b1d2a1a3 c4a3d1 b3b2e3d4a1d1 d3a3 b3a3d1 d3a3e5b5 e1a4a1a3d1
d3a4d4a1 c5a4e5d1 e3c5a3a5 b1a4b4e1e5 c4a3d1 c5a3b1d1 e3c5a3b3 a1e3d4a1 d3a3 c3a4d4b2a3e5b1 c1e5a3 c4a3
b4a3a1b1a3 d1a3e5c4 e3 d3d2d1e1e3b1e5 d1e3d4d1 c1e5 d2c4d1 e3d2a3d4a1 b1d2a3d4 e1a3b1d3e5 d3a3 c4a3e5b1
c2b1e3b3a3 b3e3b1 a3d4 c4a3d1 e2e3d2d1e3d4a1 e1e3d1d1a3b1 d3e3d4d1 e5d4 e3e5a1b1a3 d2d3d2a4b4a3 c5a4e5d1
c4a3e5b1 e3c5a3a5 b3b2a4d1a3 d1d2 d3d2e2e2d2b3d2c4a3 b3a4d4d1a3b1c5a3 d1a4e5d1 e5d4 b3a4d1a1e5b4a3 a3a1b1e3d4c2a3b1
a1a4e5d1 c4a3e5b1d1 b4a3b1d2a1a3d1 d2c4 d4 a3d1a1 e1e3d1 e5d4 d3a3d1 b3b2e3d4a1d1 d3a3 c4a3e5b1d1 e1a4b4a3d1
c1e5d2 d4a3 c5a4e5d1 a4e2e2b1a3 e5d4a3 e2a4e5c4a3 d3 a3b5a3b4e1c4a3d1 d3a3d1 c5d2b3d2d1d1d2a1e5d3a3d1 b2e5b4e3d2d4a3d1
d3a3d1 b3a4e5e1d1 d2b4e1b1a3c5e5d1 d3e5 b2e3d1e3b1d3 a3a1 d3a3 c4e3b1b4a3d1 e3b4a3b1a3d1
e1b1a4c5a4c1e5a3a3d1 e1e3b1 b4d2c4c4a3 a3a1 b4d2c4c4a3 b3e3e5d1a3d1

c4d2d1a3a5 b3a3d1 e2a4e5d3b1a4d5e3d4a1a3d1 c4a3a4d4d1 d1d2 e1e3a1b2a3a1d2c1e5a3b4a3d4a1 b1a3e1b1a4d3e5d2a1a3d1 e1e3b1 c5a4e5d1
c5a4e5d1 b1a4e5c2d2b1a3a5 d3a3 e2e3d2c3c4d2b1 d1d2 e1b1a4b4e1a1a3b4a3d4a1 a3a1 d3a3 d3a3b3b2a4d2b1 d3a3 c4e3 b2e3e5a1a3e5b1 d3a3 c5a4d1
d3d2d1b3a4e5b1d1 c2e3b1d3a3a5 c1e5a3 b3a3e5b5 c1e5d2 d4e3c2e5a3b1a3 e3d3b4d2b1e3d2a3d4a1 c1e5d2 e3d3b4d2b1a3d4a1
a3d4b3a4b1a3 c5a4d1 a3b3b1d2a1d1 d1a3 d3a3b4e3d4d3a3d4a1 b3a4b4b4a3d4a1 d3a3 d1d2 d1e5c3c4d2b4a3d1
a3a1 d1d2 e2a4b1a1a3d1 e1e3b1a4c4a3d1 a4d4a1 e1e5 d1a4b1a1d2b1 d3 e5d4a3 e3b4a3 d1d2 e2e3b3d2c4a3 e3 c3b1d2d1a3b1

e3e5 c4d2a3e5 d3a3 c5a4e5d1 d4e3c5b1a3b1 c4a3 b3a4a3e5b1 b1a3e1a4b1a1a3a5c4a3 d1e5b1 c4a3d1 b1d2b3b2a3d1 a3a1
d4a4b4c3b1a3e5d1a3d1 b3a4d4d1a4c4e3a1d2a4d4d1 c1e5d2 c5a4e5d1 e3a1a1a3d4d3a3d4a1  a1a4e5b1d4a3a5 c5a4d1 d5a3e5b5
d1e5b1 d3a3d1 e2b1a3b1a3d1 b3b2a3b1d2d1 d1e5b1 e5d4a3 a3e1a4e5d1a3 d1e5b1 e5d4 e2d2c4d1 c4e3 e2a4b1a1e5d4a3
c5a4e5d1 e3 e2e3d2a1 e1e3d5a3b1 c4a3 d1e3c4e5a1 d3 a3e5b5 a1a4e5d1 e3e5 e1b1d2b5 d3 e5d4 d1a3e5c4 d1e3b3b1d2e2d2b3a3
c5a4e5d1 e3c5a3a5 e1c4e5d1 d3 e5d4 e3d1d2c4a3 a4e5 b1a3e1a4d1a3b1 c5a4a1b1a3 d3a4e5c4a3e5b1
e1b1a3c5a3d4a3a5 d2b3d2 c4a3 c3c4e3b4a3 e1e5c3c4d2b3  c1e5 a4d4 d4a3 b3b1a4d2a3 e1e3d1
c1e5 a3d4 c5a4e5d1 e5d4a3 d1a3e5c4a3 d3a4e5c4a3e5b1 c4 a3b4e1a4b1a1a3 d1e5b1 a1e3d4a1 d3a3 b3a4d4d1a4c4e3a1d2a4d4d1

c5a4e5d1 c5a4d5a3a5 a1a4e5d1 c4a3d1 c5a4a1b1a3d1 e2b1e3e1e1a3d1 d3e5 b4a3b4a3 b3a4e5e1 c1e5a3
c5a4e5d1b4a3b4a3  c5a4e5d1 d1a3d4a1a3a5 c1e5a3 c4a4d2d4 d3a3 e1a4e5c5a4d2b1 c5a3d4d2b1 e3 c5a4a1b1a3
e3d2d3a3 d2c4d1 d4 e3a1a1a3d4d3a3d4a1 c1e5a3 d3a3 c5a4e5d1 c1e5a3c4c1e5a3 d1a4e5c4e3c2a3b4a3d4a1 b4a4d2d4d1
d3a4d4b3 c4a3e5b1d1 c4e5b4d2a3b1a3d1 a3a1 c4a3e5b1 c2a3d4d2a3 e3e1e1b1a4b3b2a3d4a1 d3a3d1 c5a4a1b1a3d1 e1c4e5d1
b3 a3d1a1 c5a4a1b1a3 d3a3c5a4d2b1 d3a3 b1a3d1d2d1a1a3b1 e3e5 b4e3c4 b3a4b4b4e5d4 a3a1 b3 a3d1a1 d3a3a2e3
e5d4a3 d1a4b1a1a3 d3 e3c4c4a3c2a3b4a3d4a1 c1e5a3 d3a3 e1e3b1a1e3c2a3b1 d1e3 e1a3d2d4a3 a3d4a1b1a3 e1c4e5d1d2a3e5b1d1  
e5d4 e2e3b1d3a3e3e5 e3d2d4d1d2 d3d2c5d2d1a3 d3a4d2a1 b1a3d3e5d2b1a3 c3a3e3e5b3a4e5e1 c4e3 e1e3b1a1
c1e5d2 c5a4e5d1 b1a3d1a1a3

a2a3 d4a3 b3a3d1d1a3b1e3d2 d4a4d4 e1c4e5d1 d3a3 c5a4e5d1 a4e2e2b1d2b1 c4 d2b4e3c2a3
d3a3 b3a3d1e3b1 a1e3d4a1 c1e5 d2c4 c2a4e5c5a3b1d4a3 c4a3 b4a4d4d3a3 a3a1 c1e5 d2c4 e1b1a4e5c5a3 b3a4b4c3d2a3d4
c4 e3e5a1a4b1d2a1a3 d1a3 b3a4d4d1a3b1c5a3 b4d2a3e5b5 e1e3b1 c4a3d1 c3d2a3d4e2e3d2a1d1 c1e5a3 e1e3b1 c4a3d1
e3b1b4a3d1 a1e3d4a1 c1e5 d2c4 e1b1a3d1d2d3a3 e3e5b5 b3b2a4d1a3d1 b2e5b4e3d2d4a3d1 c5a4e5d1 d4a3 b3a4e5b1a3a5
e1e3d1 b1d2d1c1e5a3 d3a3 c5a4e5d1 e3e1a3b1b3a3c5a4d2b1 d3 e3e5b3e5d4a3 e1a3b1a1a3  a3d4 c4e5d2 d1a3e5c4
c5a4e5d1 a1b1a4e5c5a3a5 e5d4 d1e5e1e1a4b1a1 e5d4 b3a4d4d1a4c4e3a1a3e5b1 d1e5e2e2d2d1e3d4a1 b1a3c4a3c5a3a5
c5a4a1b1a3 b3a4e5b1e3c2a3 a3a1 b3b2e3c1e5a3 e2a4d2d1 c1e5a3 c4a3d1 c4e3b1b4a3d1 c5d2a3d4d3b1a4d4a1 b1a3b4e1c4d2b1
c5a4d1 d5a3e5b5 e3b1b1a3a1a3a5c4a3d1 d1e5b1 b3a3d1e3b1 a3c4c4a3d1 d1a3 d1a3b3b2a3b1a4d4a1 e3e5 b1e3d3d2a3e5b5
e3d1e1a3b3a1 d3a3 b3a3a1a1a3 e1e5d2d1d1e3d4a1a3 d3d2c5d2d4d2a1a3 a3c3c4a4e5d2d1 d3a3 d1a4d4 a3b3c4e3a1 c5a4d1
b1a3c2e3b1d3d1 d4a3 e1a4e5b1b1a4d4a1 d1a3 e1a4b1a1a3b1 d1e5b1 d4e5c4 e3e5a1b1a3 a4c3a2a3a1 d2c4 c4a3d1 a1d2a3d4d3b1e3
e2d2b5a3d1 d1e5b1 c4e5d2 d1a3e5c4

c1e5 d2c4 b3a4d4a1d2d4e5a3 d3 a3a1b1a3 d4e5d2a1 a3a1 a2a4e5b1 c4a3 c3e5a1 d3a3 c5a4d1
b3a4d4a1a3b4e1c4e3a1d2a4d4d1 c1e5a3 c5a4a1b1a3 e3b4a3 a3a1 c5a4d1 e1a3d4d1a3a3d1 d4a3 d1 a3d4 a3b3e3b1a1a3d4a1
a2e3b4e3d2d1  c1e5 d2c4 d1a4d2a1 c5a4a1b1a3 b1a3b3a4e5b1d1 b3a4d4a1b1a3 c4e3 e2a4b1a1e5d4a3  a3a1 d1e3d4d1 d3a4e5a1a3
b3a3 e1b1d2d4b3a3 d1d2 d3a3c3a4d4d4e3d2b1a3 d1d2 e3e2e2a3b3a1e5a3e5b5 e1a4e5b1 a1a4e5d1 b3a3e5b5 c1e5d2 c4e5d2
e3e1e1e3b1a1d2a3d4d4a3d4a1 e3e5b1e3 d3a3a2e3 b4d2d1 e1c4e5d1 d3 e5d4 e3e1e1e3b1a3d2c4 d1e5b1 c5a4a1b1a3 c3c4a3d1d1e5b1a3
a3a1 e1b1a4d3d2c2e5a3 c4a3 c3e3e5b4a3 c1e5d2 d3a4d2a1 b3b2e3b1b4a3b1 c5a4d1 d3a4e5c4a3e5b1d1
b4e3d2d1 a3d4b3a4b1a3 d4 a3d4 a3e5a1d2c4 b1d2a3d4 e2e3d2a1 c5a4d2b1 d1a3e5c4a3b4a3d4a1 b3a3d1e3b1 a4e5 e1a3d4d1a3b1
e3 c4e5d2 d4 a3d1a1b3a3 e1e3d1 e5d4 e3d3a4e5b3d2d1d1a3b4a3d4a1 c3d2a3d4 b1a3a3c4 e3 c5a4a3 b4e3e5b5

e1e5d2d1d1e3d4b3a3d1 d3e5 b3d2a3c4 e1b1a3a1a3a5c4a3 c4a4d4c2a1a3b4e1d1 e3 c4e3 a1a3b1b1a3 c1e5 d2c4 a3c2e3c4a3
c4a3d1 b2e3e5a1d1 e2e3d2a1d1 d3 e3e5c2e5d1a1a3 a3a1 d3a3e1e3d1d1a3 d1a3d1 e3d4d4a3a3d1  c1e5a3 a1e3d4a1 c1e5 d2c4
d1a3b1e3 e1e3b1b4d2 c4a3d1 b2a4b4b4a3d1 d2c4 d4a3 d1 e3e1a3b1a4d2c5a3 e1e3d1 c1e5a3 b1d2a3d4 d3e3d4d1
d1e3 b4e3d2d1a4d4 d1a4d2a1 b4a4b1a1a3c4  c1e5a3 c4a3 b4e3a1b1a3 e2e5a1e5b1 d3a3 c4 a3b4e1d2b1a3 c1e5a3
d1a4d4 e2d2c4d1 d3a4d4a1 d2c4 e3e5b1e3 e3e1e1b1a3b3d2a3 c4a3 c4a4d4c2 d3a3c5a4e5b4a3d4a1 d1a4d2a1 c4a3 b3a4c4c4a3c2e5a3
d3a3 d1a4d4 e1a3b1a3 e3c5e3d4a1 d3 a3d4 a3a1b1a3 c4a3 d1e5b3b3a3d1d1a3e5b1  c1e5a3 c3d2a3d4 a1e3b1d3
a3a1 e1a4e5b1 d4a4d1 d4a3c5a3e5b5 d1a3e5c4a3b4a3d4a1 c4e5d2d1a3 c4a3 a2a4e5b1 a4e5 d1e3 e2e3b4d2c4c4a3 c4a3
e1c4e3b3a3b1e3 d3e3d4d1 c4a3d1 b3d2a3e5b5


 c1e5a3 c4a3d1 b4e3d2d4d1 a4 e2a4b1a1e5d4a3 c4a3 b1a3d1e1a3b3a1a3d4a1 c1e5 d2c4 d4 a3e1b1a4e5c5a3
a1e3 e1e5d2d1d1e3d4b3a3 c1e5a3 e1e3b1 a1a3d1 e2e3c5a3e5b1d1 e1a3b1b4a3a1d1 c1e5 d2c4 c2e5a3b1d2d1d1a3 c4a3d1
e1c4e3d2a3d1 d3e5 c2a3d4b1a3 b2e5b4e3d2d4 d3a3e1e5d2d1 c4a4d4c2a1a3b4e1d1 d1a4e5e2e2b1e3d4a1 a3a1 a3e1e5d2d1a3
a1a4e5a1 b3a3 c1e5a3 c4a3d1 e2e5b1a3e5b1d1 d3a3 d1a4d4 e1b1a3d3a3b3a3d1d1a3e5b1 a4d4a1 a3c3b1e3d4c4a3 e1a3b1b4a3a1d1
c1e5 d2c4 c4a3 b1a3e1c4e3b3a3 d1e5b1 d3a3 e2a3b1b4a3d1 c3e3d1a3d1 e1e5d2d1d1a3 b3a3a1 e3d1a1b1a3 c1e5d2
c5d2d4a1 c3b1d2c4c4a3b1 d1e5b1 e5d4 b4a4d4d3a3 a1a4b4c3a3 d3e3d4d1 c4a3 b3b2e3a4d1 a3a1 a3d4c2c4a4e5a1d2
d3e3d4d1 c4a3d1 a1a3d4a3c3b1a3d1 d4a3 d1 a3b3c4d2e1d1a3b1 a2e3b4e3d2d1  

c1e5 d2c4 e1e3b3d2e2d2a3 c4e3 c2a3b1b4e3d4d2a3 c1e5 d2c4 d4a4e5d1 a4e5c5b1a3 c4e3 c3b1a3a1e3c2d4a3 c1e5 d2c4 b3a4d4a1d2d4e5a3
a3a1 b1a3d4a4e5c5a3c4c4a3 c4a3d1 a1b1d2a4b4e1b2a3d1 d3a3 d1a4d4 e1a3b1a3 c2c4a4d2b1a3 d3a4d4a1 b4a4d2b4a3b4a3 a2a3 d1a3b1e3d2
d1e1a3b3a1e3a1a3e5b1  b3 a3d1a1 c4e3 e1b1a3b4d2a3b1a3 d3a3 d1a3d1 c5a3b1a1e5d1 d1e3 b3c4a3b4a3d4b3a3
c1e5d2 b4a3 c4a3 e1b1a4b4a3a1 b3e3b1 a3d4 b4a3 e1b1a3b3d2e1d2a1e3d4a1 d3e3d4d1 c4 e3c3b4a3 d2c4 d4 e3
e1e3d1 a2e5b1a3 d3a3 d4a3 b4 a3d4 e1a4d2d4a1 a1d2b1a3b1  c1e5a3 d3d2d1a2a3  d2c4 d4a3 b4 d5 e3 e1e3d1
b4a3b4a3 e1b1a3b3d2e1d2a1a3  c4a3 d1a4b1a1 b4a3 e1a4e5d1d1e3d2a1 e3 b4e3 b3b2e5a1a3 a3a1 d1e3 b4e3d2d4
d3d2c5d2d4a3 b4 e3 d1a4e5a1a3d4e5 a3a1 d1a4d4 d2d4d3e5c4c2a3d4b3a3 e3 d3e3d2c2d4a3 e3d3a4e5b3d2b1 e1a4e5b1
b4a4d2 c4e3 b1e5d3a3d1d1a3 d3e5 b3a4e5e1 d2c4 e3 d2d4a1a3b1b3a3d3a3 a3d4 b4e3 e2e3c5a3e5b1 e3e5e1b1a3d1 d3e5
d1a3d4e3a1  d2c4 e3 e2e3d2a1 e1c4e5d1 c1e5a3 d3a3 b4a3 d3a4d4d4a3b1 c4e3 c5d2a3 d2c4 c4 e3 d3a3b4e3d4d3a3a3
e1a4e5b1 b4a4d2

b3 a3d1a1 e3 c4e5d2 e3 c5a4d2b1 b3a4b4b4a3d4a1 d2c4 c4e5d2 e1c4e3d2b1e3 d3 e3e1e1b1a3b3d2a3b1
b4e3 b3e3e5d1a3 d1e3 a2e5d1a1d2b3a3 c4e3 b1a3b3a4d4d4e3a1b1e3 c3a4d4d4a3 a4e5 d1e3 b3c4a3b4a3d4b3a3 c4e3
b1a3d4d3b1e3 a1a3c4c4a3 b4e3d2d1 c4a3 c3d2a3d4e2e3d2a1 d1a3b1e3 a3c2e3c4 e1a4e5b1 b4a4d2 d1a4d2a1 c1e5 d2c4 b4a3
c5a4d2a3 d1a4d2a1 c1e5 d2c4 c5a3e5d2c4c4a3 b4a3 c5a4d2b1 d2d4d4a4b3a3d4a1 b2a3e5b1a3e5b5 a1a4e5a1a3e2a4d2d1 a2e5d1c1e5a3
d3e3d4d1 b4a3d1 b4e3c4b2a3e5b1d1 a2 e3d2b4a3 e3 b3a4d4d1d2d3a3b1a3b1 d1a4d4 e3b3a1d2c5a3 b3a4b4e1e3d1d1d2a4d4
e1e3b1b3a4e5b1e3d4a1 a1a4e5a1 c4a3 c2c4a4c3a3 d3a3 b3a3 b4a3b4a3 b3a4d2d4 d3a3 a1a3b1b1a3 a4e5
a2a3 d1e5d2d1 a3d4d1a3c5a3c4d2 a1e3d4a1 d3 d2d4e2a4b1a1e5d4a3d1 e1c4a4d4c2a3d1 d3e3d4d1 c4 a4e5c3c4d2 d3 e5d4a3
d3d2d1c2b1e3b3a3 d3a3 e1c4e5d1d2a3e5b1d1 e3d4d4a3a3d1 a3d4 a4d4a1 a3a1a3 e3b1b1e3b3b2a3d1 e1e3b1 c4e5d2 a3a1 b1e3b4a3d4a3d1
e3 c4e3 c4e5b4d2a3b1a3  a2a3 d4a3 b3b1e3d2d4d1 e1e3d1 d3 a3a1b1a3 c4a3 d1a3e5c4 c1e5d2 a3b3b2e3e1e1a3
e3 d1e3 e1d2a1d2a3 b4e3d2d1 c1e5d2 d1e3d2a1 b4d2a3e5b5 c1e5a3 c4e5d2 c4 d2d4d1a1e3d4a1 a4e5 d2c4 d3a4d2a1 c5a3d4d2b1
e3e5 d1a3b3a4e5b1d1 d3a3 b3b2e3b3e5d4  a2a3 e2a3b1e3d2 a1a4e5a1 e1a4e5b1 c1e5a3 d1e3 b3c4a3b4a3d4b3a3 d4a3
b1a4e5c2d2d1d1a3 e1e3d1 d3a3 d3a3d1b3a3d4d3b1a3 e3 b4a4d2

c3a3d4d2a3 d1a4d2a1a3c4c4a3 a4 b3a3d1e3b1  e1e3b1 a3c4c4a3 a3d4 a3e2e2a3a1 d3a3d1 c3e3d4d4d2d1 c5d2c5a3d4a1 d1a4e5d1 a1a4d4
b1a3c2d4a3 e3c5a3b3 b4a4d2d4d1 d3 e3c4e3b1b4a3 c1e5a3 d4e3c2e5a3b1a3 c4a3d1 e1b1a3b4d2a3b1d1 d3a3 c4 a3b4e1d2b1a3 d1a4e5d1 b3e3c4d2c2e5c4e3
e1c4e5d1 d3 e3d4c2a4d2d1d1a3d1 e1c4e5d1 d3a3 c2c4e3d2c5a3 d3 b2a3e5b1a3 a3d4 b2a3e5b1a3 e3a1a1a3d4d3e5
b3b2e3c1e5a3 c5a4d2c4a3 c1e5d2 d1a3 b4a4d4a1b1a3 e3 c4 b2a4b1d2a5a4d4 d4a3 d4a4e5d1 e2e3d2a1 e1c4e5d1
e1e3c4d2b1 c2b1e3b3a3 e3 a1a4d2 c4a3d1 b1d2c2e5a3e5b1d1 d3e5 d1a4b1a1 a4d4a1 c4a3e5b1d1 c3a4b1d4a3d1 c4 e3c5a3d4d2b1
d4a4e5d1 c4a3 e2e3d2a1 a3d1e1a3b1a3b1 b4a3d2c4c4a3e5b1 a3a1 c4a3 e1b1a3d1a3d4a1 a3d1a1 e3d1d1e5b1a3 e3b2
d1e3d4d1 d3a4e5a1a3 c4e3 e2a4e5d3b1a3 a3d1a1 a2e5d1a1a3 d3e3d4d1 d1a3d1 b3a4e5e1d1 c1e5e3d4d3 b3a3e5b5
b4a3b4a3 c1e5 a3c4c4a3 e2b1e3e1e1a3 c4e3 b1a3c5a3b1a3d4a1


e3d2d4d1d2 d3a4d4b3 e1a4c4d5c3a3 c4a3 e1b1d2d4b3a3 c1e5d2 a3d1a1 c4a3 b3a4d4d1a4c4e3a1a3e5b1
d3a3 a1a4e5d1 c4a3d1 b2e5b4e3d2d4d1 e3 d3a3a2e3 d1d2 a2a3 d4a3 b4a3 a1b1a4b4e1a3 d1a4e5c4e3c2a3 c5a4a1b1a3
e3b4a3 a3a1 e3e1e1c4d2c1e5a3 d1e5b1 e5d4a3 d1d2 c2b1e3c5a3 c3c4a3d1d1e5b1a3 d3a3d1 b1a3b4a3d3a3d1 a3d4b3a4b1a3
e1c4e5d1 e1e5d2d1d1e3d4a1d1 d2c4 d4 e3 b1d2a3d4 a4b4d2d1 e1a4e5b1 c5a4e5d1 b1e3e2e2a3b1b4d2b1 a1a4e5d1
c4a3d1 a3b5a3b4e1c4a3d1 e1b1a4e1b1a3d1 e3 c5a4e5d1 d2d4d1e1d2b1a3b1 c4e3 b1a3d1d2c2d4e3a1d2a4d4 d1e3 b4a3b4a4d2b1a3
d1d2 e2d2d3a3c4a3 c5a4e5d1 c4a3d1 e3 b1e3e1e1a4b1a1a3d1  d2c4 c5a4e5d1 e3 d3a3c5a3c4a4e1e1a3 c4a3d1
e1b1a3b3a3e1a1a3d1 d3a3 a1a4e5d1 c4a3d1 d1e3c2a3d1 e3c5a3b3 d1a4d4 a3c4a4c1e5a3d4b3a3 a4b1d3d2d4e3d2b1a3

d4e5c4 d4 e3e5b1e3d2a1 b4d2a3e5b5 b1a3b4e1c4d2 c1e5a3 c4e5d2 b3a3a1a1a3 a1e3b3b2a3 d3a3 b3a4d4d1a4c4e3a1d2a4d4 d3a3
a1a3c4d1 d3d2d1b3a4e5b1d1 e3e5b1a4d4a1 e5d4 a1a4e5a1 e3e5a1b1a3 e1a4d2d3d1 a1a4b4c3e3d4a1 d3a3 d1a3d1 c4a3c5b1a3d1
b3a4b4b4a3 e3e5a1e3d4a1 d3 a4b1e3b3c4a3d1  d1a4d4 e3e5a1a4b1d2a1a3 e1c4e5d1 b2e5b4e3d2d4a3 c3b1d2d1a3b1e3
c4e3 e2a4b1b3a3 d3a3 c5a4a1b1a3 d3a4e5c4a3e5b1 e2d2c2e5b1a3a5c5a4e5d1 c4 a3d4a1a3d4d3b1a3 c5a4e5d1 d3d2b1a3
a1e5 d4 a3d1 e1e3d1 c4e3 d1a3e5c4a3 c5d2b3a1d2b4a3 c1e5a3 c4e3 e2a4b1a1e5d4a3 d1a3 d1a4d2a1 b3b2a4d2d1d2a3 a3a1
c1e5 a3c4c4a3 e3d2a1 d1d2 d2d4d3d2c2d4a3b4a3d4a1 a1b1e3d2a1a3a3 a3b5d2d1a1a3a1d2c4 a3b5d2d1a1e3a1d2c4 a2e3b4e3d2d1
d1e5b1 a1a4e5a1a3 c4e3 e2e3b3a3 d3e5 c2c4a4c3a3 e5d4a3 d1a3e5c4a3 b4e3d2d1a4d4 c1e5d2 d4 e3d2a1 e1c4a3e5b1a3
c1e5a3c4c1e5a3 b3e3a1e3d1a1b1a4e1b2a3  d1e3d4d1 b4 e3b1b1a3a1a3b1 e3 d3a3d1 e2e3d2a1d1 c5e5c4c2e3d2b1a3d1 c1e5d2
e1c4e5d1 a4c3d1b3e5b1d1 d4 a3d4 d1a4d4a1 e1e3d1 b4a4d2d4d1 e2b1e3e1e1e3d4a1d1 b3 a3d1a1 e3 d4a4d1 e2e3d1a1a3d1
e3e5b5 e3d4d4e3c4a3d1 d3a3 b3a3a1a1a3 b1a3e1e5c3c4d2c1e5a3 c1e5a3 a2a3 a1a3 b1e3b4a3d4a3

a1e5 c5a4d2d1 a1a4e5a1a3d1 b3a3d1 d2b4e3c2a3d1 c1e5d2 b1a3b4e1c4d2d1d1a3d4a1 c4a3 c5a3d1a1d2c3e5c4a3 d3a3d1 b3a3d1e3b1d1
a3d4 a3d1a1d2c4 e5d4a3 c1e5a3 d4 e3d2a1 b1a3d4d3e5a3 e2e3b4a3e5d1a3 c1e5a3c4c1e5a3 c2b1e3d4d3a3 e1a3d2d4a3 d3a4b4a3d1a1d2c1e5a3
a3d1a1d2c4 e5d4 d3a3 b3a3d1 b2a4b4b4a3d1 a4b1d4a3b4a3d4a1d1 d3a3d1 d1d2a3b3c4a3d1 a4e5 d2c4d1 a4d4a1
c3b1d2c4c4a3 c1e5d2 d4 e3d2a1 a3e5 c4a3 b3a4a3e5b1 d3a3b3b2d2b1a3 d3e5 a1b1a3e1e3d1 d3a3d1 d1d2a3d4d1 a4e5 c1e5d2
d4a3 c4a3e5b1 e3d2a1 c4e5d2b4a3b4a3 c4e3d2d1d1a3 c4a3d1 e1c4e5d1 b3e5d2d1e3d4a1d1 b1a3c2b1a3a1d1  

a1a3 b1e3e1e1a3c4c4a3b1e3d2a2a3 d1b3d2e1d2a4d4 c4 e3e2b1d2b3e3d2d4 e3e1e1b1a3d4e3d4a1 d3e3d4d1 c4 a3b5d2c4 c4e3 b4a4b1a1 d3a3
d1a4d4 e2b1a3b1a3  d2c4 c4 e3c5e3d2a1 e3b1b1e3b3b2a3 e3 c4e3 e1b1d2d1a4d4 b4e3d2d1 e3 c4e3 b4a4b1a1 d2c4 d4a3
e1e5a1 c4a3 d1a4e5d1a1b1e3d2b1a3 a3a1 a1a4e5d1 e3c5e3d2a3d4a1 c5e5 b3a4b4c3d2a3d4 d1e3 a1a3d4d3b1a3d1d1a3 e1a4e5b1
c4e5d2 d1a3 b1a3c5a4c4a1e3d2a1 b4a3b4a3 b3a4d4a1b1a3 c4a3d1 d3b1a4d2a1d1 c4a3d1 e1c4e5d1 a2e5d1a1a3d1 b3e3b1 c4a3
a2a4e5b1 b4a3b4a3 a4e5 d2c4 a3d4c4a3c5e3 b3a3 e2b1a3b1a3 d3a3d1 b4e3d2d4d1 d3a3 c4 a4e2e2d2b3d2a3b1 d3e5 a1b1d2c3e5d4
d2c4 a4d1e3 b2a4b4b4a3 e1b1d2c5a3 d1 a4e1e1a4d1a3b1 e3 b3a3 a1b1d2c3e5d4 d3e5 e1a3e5e1c4a3
a3b2 c3d2a3d4 b3a3a1 b2a4b4b4a3 d1e5e1e1a4b1a1e3 c4e3 b4a4b1a1 d3a3 d1a4d4 e2b1a3b1a3 e3c5a3b3 e3e5a1e3d4a1
d3a3 b3a4e5b1e3c2a3 c1e5 d2c4 c4 e3c5e3d2a1 d3a3e2a3d4d3e5

a1a3 b3d2a1a3b1e3d2a2a3 d1b3d2e1d2a4d4 a3b4d2c4d2a3d4 a1a3b4a4d2d4 e1b1a3d1c1e5a3 a3d4 e5d4 d1a3e5c4 a3a1 b4a3b4a3 b4a4b4a3d4a1
d3e5 a1b1d2a4b4e1b2a3 d3 e5d4 e1a3b1a3 a3a1 d3a3d1 e2e5d4a3b1e3d2c4c4a3d1 d3a3 d3a3e5b5 e2b1a3b1a3d1 a3a1 d4a3e3d4b4a4d2d4d1
c1e5a4d2c1e5a3 e3d3a4c4a3d1b3a3d4a1 e3 e1a3d2d4a3 a3a1 a1a4e5b3b2e3d4a1 a3d4b3a4b1a3 e3 c4 a3d4e2e3d4b3a3 d2c4
c5d2a1 d1e3 e2e3b4d2c4c4a3 a3d4d1a3c5a3c4d2a3 d1a4e5d1 c4a3d1 a1b1a4e1b2a3a3d1 d3a3 d1a4d4 b3b2a3e2 d2c4 b3a4d4a1a3b4e1c4e3
b3a3 c3b1e5d1c1e5a3 c5d2d3a3 e3c5a3b3 c4e3 e2a3b1b4a3a1a3 d3 e5d4 b2a3b1a4d1 d4a3 e1a4e5b1
e2e3d2b1a3 b1a3c5d2c5b1a3 d3e3d4d1 b1a4b4a3 c4a3d1 d1b3d2e1d2a4d4d1 a3a1 e1a4e5b1 d3a3a1b1e5d2b1a3 b3e3b1a1b2e3c2a3


c1e5a3 d3d2b1a3 d3a3d1 d3a3e5b5 c4e5b3e5c4c4e5d1 d3a4d4a1 c4 b2a3e5b1a3e5d1a3 e5d4d2a4d4
e2e5a1 b1a4b4e1e5a3 e1e3b1 c4e3 b4a4b1a1  d3a3d1 a1b1a4d2d1 e1a4b4e1a3a3d1 e3 c1e5d2 c4a3 b3b1e5a3c4 d3a3d1a1d2d4
d4 e3 e1e3d1 c4e3d2d1d1a3 c4a3 c3a4d4b2a3e5b1 d3a3 a1a4b4c3a3b1 d1a4e5d1 c4a3 b4a3b4a3 b3a4e5e1
d1a3b5a1e5d1 e1a4b4e1a3a3 a3e5a1 d3 e3c3a4b1d3 c4a3 b3b2e3c2b1d2d4 d3a3 d1e5b1c5d2c5b1a3 e3 d1e3 d1a4a3e5b1
d3a4d4a1 c4e3 b4a4b1a1 c3b1d2d1e3 c4a3d1 c4d2a3d4d1 d1d2 d1a4c4d2d3a3b4a3d4a1 e2a4b1b4a3d1 d3a3 c4e3 e1e3d2b5 e1e5c3c4d2c1e5a3
d2c4 d1e5b1c5a3b3e5a1 a3d4b3a4b1a3 e3 b3a3 d3d2c2d4a3 e2b1a3b1a3 c1e5a3 c4e3 e2a4b1a1e5d4a3 d4 e3c5e3d2a1
a1e3d4a1 a3c4a3c5a3 c1e5a3 e1a4e5b1 c4a3 e1b1a3b3d2e1d2a1a3b1 d3 e3e5d1d1d2 b2e3e5a1 c1e5a3 d1a4d4 e1a3b1a3  a3a1
e3e1b1a3d1 b3a3a1a1a3 d4a4e5c5a3c4c4a3 a3e1b1a3e5c5a3 d2c4 e1e5a1 d1e5e2e2d2b1a3 d4a4d4 d1a3e5c4a3b4a3d4a1 e3
d1e3 d3a4e5c4a3e5b1 b4e3d2d1 e3e5b5 d1a4d2d4d1 d3a3 c4e3 c2e5a3b1b1a3

e1e3b1a1a4e5a1 d1 a4e2e2b1a3d4a1 d3 d2d4d4a4b4c3b1e3c3c4a3d1 a3b5a3b4e1c4a3d1 d3a3 e2b1a3b1a3d1 d1a3e1e3b1a3d1
e1e3b1 c4e3 b4a4b1a1 a4e5 e1c4e5a1a4a1 e3 e1a3d2d4a3 e5d4 d1a3e5c4 b3a4e5e1c4a3 e2b1e3a1a3b1d4a3c4
e3a1d2c4 a3a1a3 c5e5 c5d2a3d2c4c4d2d1d1e3d4a1 a3d4d1a3b4c3c4a3 b4e3d2d1 d4a3 d1a4b1a1a4d4d1 e1e3d1 d3a3 c4e3
b4e3d2d1a4d4 d2b4e1a3b1d2e3c4a3 a4e5 a3d1a1 c4 b2a4b4b4a3 e3d1d1a3a5 d3a3e1a4e5b1c5e5 d3a3 d1a3d4d1
a3a1 d3a3 b1e3d2d1a4d4 e1a4e5b1 d1a3 e1c4e3d2d4d3b1a3 c1e5a3 c4e3 e2a4b1a1e5d4a3 c4e5d2 d2d4e2c4d2c2a3 c1e5a3c4c1e5a3
d3a3e5d2c4 c1e5e3d4d3 d2c4 d1e3e5b1e3 c1e5 a3c4c4a3 e3 a3e5 d1a4d2e2 d3a3d1 c4e3b1b4a3d1 b4a3b4a3 d3a3d1
b3a3d1e3b1d1  

e3e5c2e5d1a1a3 e3 e1c4a3e5b1a3 a4b3a1e3c5d2a3 d1e3 d1a4a3e5b1 d1d2 b3b2a3b1a3b4a3d4a1
e3d2b4a3a3 a3a1 c4e3 d4e3a1e5b1a3 d4 e3 e1e3d1 e2e3d2a1 b1a3b4d2d1a3 d3a3 b3a3 a1b1d2c3e5a1 d3a3 c4e3b1b4a3d1 e3
c4 b2a4b4b4a3 e3e5c1e5a3c4 a3c4c4a3 d3a3d1a1d2d4e3d2a1 c4a3 b3d2a3c4 a3a1 c1e5a3 d3d2d1a2a3  e3b3b3e3c3c4a3
d3a3 a1a4e5d1 c4a3d1 c2a3d4b1a3d1 d3a3 d3a3e5d2c4 d2c4 e3 c5e5 e1a3b1d2b1 c4a3 e2d2c4d1 d3a3 d1e3 d1a4a3e5b1 e1b1a3e1e3b1a3
e1e3b1 c4e5d2 e3 c4e5d2 d1e5b3b3a3d3a3b1 d2c4 e3 e1a4e5b1 a1a4e5a1 b3a4b4e1b1a3d4d3b1a3 a3d4 d3a3e5b5
b4a4a1d1 c5e5 e1a3b1d2b1 d1a3d1 c2a3d4d3b1a3d1 d1a3d1 e2d2c4d1 e3d3a4e1a1d2e2d1 d1a3d1 d4a3c5a3e5b5 a3a1
d4e5c4 d3a3 a1a4e5d1 c4a3d1 b4a4b1a1a3c4d1 d4a3 d1a3d4a1d2a1 e1c4e5d1 c1e5a3 c4e5d2 c1e5 d2c4 a3a1e3d2a1 b2a4b4b4a3
a1e3d4a1 c1e5 d2c4 d3a3b4a3e5b1e3 b3b2a3a5 c4a3d1 b2a4b4b4a3d1 b3a3e1a3d4d3e3d4a1 a1e3d4a1 d3a3 b3a4e5e1d1
a1a3b1b1d2c3c4a3d1 d4 a3b5b3a3d3a3b1a3d4a1 e1e3d1 c4a3d1 e2a4b1b3a3d1 d3a3 b3a3a1a1a3 e3b4a3 c1e5d2 d1e5e2e2d2d1e3d2a1
e3 a1a4e5a1 a3a1 c5e3d2d4c1e5a3e5b1 d3a3d1 d4e3a1d2a4d4d1 a3a1b1e3d4c2a3b1a3d1 c4a3 d3d2c5d2d4 e3e5c2e5d1a1a3
d1e5a1 a3d4b3a4b1a3 c5e3d2d4b3b1a3 d1a3d1 d3a4e5c4a3e5b1d1

b3 b3a3d1e3b1 e2d2c4d1 e3d3a4e1a1d2e2 a3a1 e1a3a1d2a1e2d2c4d1 d3 e3e5c2e5d1a1a3 b4a4d4 a4d4b3c4a3 e3e5
d1a4b1a1d2b1 d3a3 c4 e3d3a4c4a3d1b3a3d4b3a3 e1a3b1d3d2a1 d1a4d4 e2b1a3b1a3 b3b2a3b1d2 c4e5b3d2e5d1 e1b1d2d4b3a3 d3a3
c4e3 a2a3e5d4a3d1d1a3 b3a4b4b4a3 c4e5d2 b3 a3d1a1 d3e3d4d1 c4a3d1 e3e1e1b1a3a1d1 d3a3 c4e3 c2e5a3b1b1a3 d3a3d1
e1e3b1a1b2a3d1 a4e5 d2c4 e3c4c4e3d2a1 a3a1b1a3 c3c4a3d1d1a3 c1e5 d2c4 b1a3e5a1 b3a3a1a1a3 e1c4e3d2a3 b4d2c4c4a3
e2a4d2d1 e1c4e5d1 e1b1a4e2a4d4d3a3 a3a1 d2c4 a3d4d3e5b1e3 c4 e5d4a3 a3a1 c4 e3e5a1b1a3 e3c5a3b3 c4a3 b4a3b4a3
b2a3b1a4d1b4a3 e3c5a3b3 c4e3 b4a3b4a3 b1a3d1d2c2d4e3a1d2a4d4

a1d2c3a3b1a3 b4a4d4 a4d4b3c4a3 c5d2a1 b4a4e5b1d2b1 d3e3d4d1 d1a3d1 c3b1e3d1 a3a1 b3a4e5c5a3b1a1 d3a3 d1a3d1 c3e3d2d1a3b1d1
b4a4d4 e1a3b1a3 d3b1e5d1e5d1 c2a3b1b4e3d4d2b3e5d1 d1a4d4 e2b1a3b1a3 e1e5d4a3 c1e5d2 d4a4e5d1 e3c5e3d2a1 a4e5c5a3b1a1 c4a3
b3a3d4a1b1a3 d3a3 c4e3 c2a3b1b4e3d4d2a3 a3a1 d1a4e5b4d2d1 c4a3d1 b1e3b3a3d1 c4a3d1 e1c4e5d1 d2d4d3a4b4e1a1e3c3c4a3d1
c1e5a3 e2d2a1 e1a4e5b1a1e3d4a1 a1d2c3a3b1a3  d2c4 b4d2a1 e5d4 e2b1a3d2d4 d4a4d4 d1a3e5c4a3b4a3d4a1
e3 d1a4d4 d3a3d1a3d1e1a4d2b1 b4e3d2d1 e3 b3a3c4e5d2 d3a3d1 e3e5a1b1a3d1 c4 e3b1b4a3a3 a3d4a1d2a3b1a3 e3b3b3e3c3c4a3a3
e1e3b1 c4e3 e2a4e5d3b1a4d5e3d4a1a3 d4a4e5c5a3c4c4a3 b1a3b3c4e3b4e3d2a1 c4a3d1 b1a3d1a1a3d1 d3a3 d1a4d4
b3b2a3b1 d3b1e5d1e5d1 d2c4 c4e3 b3a4d4a1d2d4a1 d3e3d4d1 c4a3d1 c3a4b1d4a3d1 d3 e5d4a3 e3e2e2c4d2b3a1d2a4d4 a1a4e5a1a3
b1a4b4e3d2d4a3 d2c4 a2e5c2a3e3 c1e5a3 d1d2 c4e3 d3d2d1b3d2e1c4d2d4a3 b4d2c4d2a1e3d2b1a3 e3 d1a3d1 b1a3c2c4a3d1 c4e3
d3a4e5c4a3e5b1 e3e5d1d1d2 e3 c4a3d1 d1d2a3d4d4a3d1 d1 d2c4 d4 a3e5a1 d3 e3c3a4b1d3 d1a3b3b2a3 d1a3d1 c4e3b1b4a3d1
b3a4b4b4a3d4a1 a3e5a1d2c4 a3d1d1e5d5a3 c4a3d1 d4a4a1b1a3d1


b4e3b1b3e3d4a1a4d2d4a3 b4a4d4 e3a3e5c4 c4a3 e1b1a3b4d2a3b1 d3a3d1 b2a4b4b4a3d1
e3e1b1a3d1 d1a4d4 c5e3d2d4c1e5a3e5b1 b1a3b3a4d4d1a1d2a1e5e3d2a1 c4e3 b1a3e1e5c3c4d2c1e5a3 d1a4e5d1 c4a3 e1a4e5c5a4d2b1
a1b1d2e5b4c5d2b1e3c4 d3a4d4a1 d2c4 a3a1e3d2a1 c4a3 b3b2a3e2 d2c4 d4a3 b3a4d4d4e3d2d1d1e3d2a1 e1a4d2d4a1 d3a3
d1e5e1a3b1d2a3e5b1 a3a1 d1e3e5e2 d1a3d1 d3a3e5b5 b3a4c4c4a3c2e5a3d1 c5a4d5e3d2a1 a1a4e5a1 e3e5d3a3d1d1a4e5d1
d3a3 c4e5d2 c4a4b1d1c1e5 d2c4 e3e1e1b1d2a1 c4e3 e2d2d4 a1b1e3c2d2c1e5a3 d3a3 d1a4d4 e2b1a3b1a3

a4 a1d5b1e3d4d4d2c1e5a3 e2a4b1a1e5d4a3 c1e5a3c4 a2a3e5 b3b1e5a3c4 a1e5 a1a3 e2e3d2d1 d3e5 b4e3c4b2a3e5b1 d3a3d1 b2e5b4e3d2d4d1
d3e3d4d1 c4a3 b4a3b4a3 a1a3b4e1d1 c1e5a3 b4e3b1b3e3d4a1a4d2d4a3 d1d2a3c2a3e3d2a1 e3b1c3d2a1b1a3 d3e5 d3b1a4d2a1
d3a3 c5d2a3 a3a1 d3a3 b4a4b1a1 d1e5b1 d1a3d1 b3a4d4b3d2a1a4d5a3d4d1 c4a3 e2b1a3b1a3 d3a3 b3a3 b4e3b1b3e3d4a1a4d2d4a3
a3a1e3d2a1 b3a4d4d3e3b4d4a3 b3a4d4d3e5d2a1 e3e5 d1e5e1e1c4d2b3a3 c4a3 a1b1d2e5b4c5d2b1 d1e5e1a4b1a1e3
b3a3e1a3d4d3e3d4a1 b3a3a1a1a3 e3e2e2b1a3e5d1a3 c3c4a3d1d1e5b1a3 e3c5a3b3 e3e5a1e3d4a1 d3a3 b4e3c2d4e3d4d2b4d2a1a3
c1e5a3 a1a4e5a1a3d1 c4a3d1 d3d2d1c2b1e3b3a3d1 e1b1a3b3a3d3a3d4a1a3d1  d1a3d1 e1c4a3e5b1d1 e3 c4e5d2 b3a3
e2e5a1 c4a3 d1e3d4c2 d3a3 c5d2d4c2a1 c4a3c2d2a4d4d1 d2b4b4a4c4a3a3d1 e3e5b5 b4e3d4a3d1 e2b1e3a1a3b1d4a3c4d1

b4e3d2d1 e1a4e5b1 d4a3 e1e3d1 b1e3e1e1a3c4a3b1 b4d2c4c4a3 e3e5a1b1a3d1 d1a4e5c5a3d4d2b1d1 d3a4d4a1 e1c4e5d1d2a3e5b1d1
b4a3 d1a4d4a1 e1a3b1d1a4d4d4a3c4d1 c4a3 d1a4b1a1 b4 e3 e2b1e3e1e1a3 d3a3e5b5 e2a4d2d1 a3a1 d3e3d4d1
e5d4 e2b1a3b1a3 a3a1 d3e3d4d1 e5d4a3 d1a4a3e5b1 a3a1 d3a3e5b5 e2a4d2d1 d2c4 e3 c5e5 c1e5 d2c4 e1a4e5c5e3d2a1
b4a3 c3c4a3d1d1a3b1 b4e3d2d1 d4a4d4 b4a3 c5e3d2d4b3b1a3 a2 e3d2 e1a3b1d3e5 c2a3b1b4e3d4d2b3e5d1 b4a4d4
e2b1a3b1a3 a3a1 e1a4e5b1 a2e5c2a3b1 b3a4b4c3d2a3d4 a2a3 c4 e3d2b4e3d2d1 d2c4 e2e3e5a1 b3a4b4e1b1a3d4d3b1a3
a2e5d1c1e5 a4e5 c5a4d4a1 b3b2a3a5 e5d4 e2b1a3b1a3 d3a3c5a4e5a3 b3a3d1 e3e2e2a3b3a1d2a4d4d1 d3e5 d1e3d4c2
a3d4 e3d2a2a3 b4a4d2d4d1 d1e5 b1a3c2c4a3b1 b4e3 d3a4e5c4a3e5b1 d3a3 b4e3d4d2a3b1a3 e3 d4a3 b1d2a3d4 a4b4a3a1a1b1a3
d3a3 b3a3 c1e5 a3b5d2c2a3e3d2a1 c4a3 d3a3c5a4d2b1 d3 e5d4 c3a4d4 e2b1a3b1a3 b3a4b4b4a3 e3 d4a3
b1d2a3d4 e2e3d2b1a3 c1e5a3 c4 a4d4 e1e5a1 c3c4e3b4a3b1 d3e3d4d1 e5d4 e1b1d2d4b3a3

d1e5e1e1a4d1a3a5 d3a4d4b3 e1a4c4d5c3a3 c1e5a3 b3 a3d1a1 c4a3 e1a3b1a3 d3a3 c4e3 e1e3a1b1d2a3 c1e5d2 c5a4e5d1
b1e3e1e1a4b1a1a3 b3a3d1 d3d2e2e2a3b1a3d4a1d1 a1b1e3d2a1d1 c4e5d2 c1e5d2 c5a4e5d1 b4a4d4a1b1a3 c1e5 e3e5b3e5d4a3
b3b2a4d1a3 d4 a3d1a1 d1e3b3b1a3a3 d4d2 d2d4c5d2a4c4e3c3c4a3 e1a4e5b1 c4e3 e2a4b1a1e5d4a3 c1e5d2 e3 a4d1a3 e2e3d2b1a3
d1a4b1a1d2b1 d3a3d1 e1a4b4e1a3d1 e2e5d4a3b1e3d2b1a3d1 d3a3 b3a3d1 b4a3b4a3d1 e1e3c4e3d2d1 a4e5 a3c4c4a3 c5d2a3d4a1
b3b2a3b1b3b2a3b1 d4a4d1 d3a3b4d2d3d2a3e5b5 c1e5 a4d4 d4a3 d1 a3a1a4d4d4a3 e1c4e5d1 d3a3 c4e3 a1b1a4e5c5a3b1
a3d4 c1e5a3c4c1e5a3 b1a3d4b3a4d4a1b1a3 a4e5 c3e3b1c3e3b1a3 a4e5 d2d4a2e5d1a1a3 e3e5b1e3d2a1a3c4c4a3
e1a4e5b1 d3a3d1 a1a3a1a3d1 e1b1d2c5a3a3d1 c4e3 b4a4d2d4d3b1a3 a3c1e5d2a1a3 c4a3d1 b4a4d2d4d3b1a3d1 b4a3d4e3c2a3b4a3d4a1d1
a3c4c4a3 d3a4d4a1 c4 d2b4e1c4e3b3e3c3c4a3 e2e5b1a3e5b1 e3 a1e3d4a1 d3a3 e2a4d2d1 d1a4e5d2c4c4a3
e1e3b1 c4e3 b4a4b1a1 c4 a4b1a3d2c4c4a3b1 d1e3b3b1a3 d3a3d1 b3a3d1e3b1d1

a3d4 c5e3d2d4 c4a3d1 e1c4e5d1 e3b4a3b1d1 b1a3e1b1a4b3b2a3d1 d1a4b1a1d2b1a4d4a1 a3a1 d3a3 d4a4a1b1a3 c3a4e5b3b2a3 a3a1
d3a3 c4e3 c3a4e5b3b2a3 d3a3 a1a4e5a1 e5d4 e1a3e5e1c4a3 a3c4c4a3 d4 a3d4 b1e3c3e3a1a1b1e3 b1d2a3d4 d3a3 d1a3d1 b1d2c2e5a3e5b1d1 d1a4e5b1d3a3 e3
a1a4e5a1a3 e1c4e3d2d4a1a3 e3 a1a4e5a1a3 a3b5e1d2e3a1d2a4d4 b3a3 c1e5 a3c4c4a3 e3 e2e3d2a1 d3a3d1 b3b2a4d1a3d1 d3a3
b3a3 b4a4d4d3a3 a3c4c4a3 c4a3 e2a3b1e3 a1a4e5a2a4e5b1d1  d2c4 d4 a3d1a1 b1d2a3d4 c1e5a3 c4e3d2d1d1a3 a3d4 e1e3d2b5
d1a4d4 e3e5d3e3b3a3 b1d2a3d4 c1e5a3 d4a3 a1a4e5b3b2a3d4a1 d1a3d1 b4e3d2d4d1 e1b1a4e2e3d4a3d1 a3c4c4a3
e2a4b1b3a3b1e3 b3a4b4b4a3 a3c4c4a3 c4a3 e2d2a1 d3a3 a1a4e5a1 a1a3b4e1d1 c4a3d1 e1c4e5d1 d1e3d2d4a1a3d1 c3e3b1b1d2a3b1a3d1
a3c4c4a3 d1a3 e2a3b1e3 a2a4e5b1 e1a4e5b1 d5 e1a4b1a1a3b1 c4a3 d3a3e5d2c4 a2e5d1c1e5 a3d4 b3a3d1
d3a3b4a3e5b1a3d1 c1e5d2 a4d4a1 d3a3d1 a1a3b4e1c4a3d1 e1a4e5b1 e3c5a3d4e5a3d1 a3a1 d1e5b1 c4a3d1 e1a4b1a1d2c1e5a3d1
d3a3 c4e3 a1a4e5a1a3e1e5d2d1d1e3d4b3a3 a3c4c4a3 a3d4c4e3b3a3b1e3 d3a3 b3b1a3e1a3d1 c4a3d1 c4e3e5b1d2a3b1d1

e1e5d2d1d1a3d4a1 d1a3e5c4a3b4a3d4a1 d1d2 a3c4c4a3 d4 e3 e1e3d1 a3d4b3a4b1a3 b1a3d1a4c4e5 d3 e3d4a3e3d4a1d2b1
c4a3 b4a4d4d3a3 d1d2 c4a3 d4a4b4 b1a4b4e3d2d4 c4e5d2 d1a1 a3d4b3a4b1a3 b3b2a3b1 d4a4d1
c5a4a3e5b5 a3a1 c4a3d1 e1e5c3c4d2c1e5a3d1 e1b1d2a3b1a3d1 a4c3a1a3d4d2b1 d3 a3c4c4a3 c1e5 e5d4 e1b1d2d4b3a3
d3a4d4d4a3 e3e5 c2a3d4b1a3 b2e5b4e3d2d4 d3a3a2e3 d1e5b1 c4a3 e1a3d4b3b2e3d4a1 d3a3 c4 e3c3b4a3 d1a4d2a1
e3e5d1d1d2 d1e3b3b1a3 e1a4e5b1 a3c4c4a3 c1e5 d2c4 c4 a3d1a1 e1a4e5b1 c4 e5d4d2c5a3b1d1 c1e5 a3c4c4a3 e3e1e1b1a3d4d4a3
d3a3 c4e5d2 c4e3 b3c4a3b4a3d4b3a3 c1e5 a3c4c4a3 d1a4d2a1 d3a4e5b3a3 a3d4c5a3b1d1 c4a3 e1c4e5d1 d3a4e5b5 d3a3d1 e1b1d2d4b3a3d1


e1a4e5b1 c5a4e5d1 c4a3d1 d5a3e5b5 e2d2b5a3d1 d1e5b1 b3a3d1 c2b1e3d4d3d1 b2a4b4b4a3d1 b3d2a1a3d1 a1a4e5a1
e3 c4 b2a3e5b1a3 a3a1 d3a3a2e3 b1a3e5d1 d3e3d4d1 c4a3 b3d2a3c4 a4e5 d3e3d4d1 e5d4a3 d1e1b2a3b1a3 c5a4d2d1d2d4a3
d3e5 b3d2a3c4 d1a4e5e2e2b1a3a5 d1e3d4d1 b4e5b1b4e5b1a3 c1e5a3 c4a3 d1a4b1a1 a3a1a3d4d3a3 a2e5d1c1e5 e3
c5a4e5d1 b3a3a1a1a3 b4e3d2d4 c1e5d2 e2b1e3e1e1a3 b3a3e5b5 b4a3b4a3 e1e3b1 c1e5d2 c4 b2e5b4e3d4d2a1a3 b1a3d1e1d2b1a3
a3d4b3a4b1a3 d2b4d2a1a3a5 c4a3e5b1 b3a4e5b1e3c2a3 e3 d1a4e5a1a3d4d2b1 e3 c5e3d2d4b3b1a3 c4e3 d3a4e5c4a3e5b1
a3a1 e3e5a1e3d4a1 c1e5 d2c4 a3d1a1 d3a4d4d4a3 e3 c4 b2a4b4b4a3 b4e3b1b3b2a3a5 d1e5b1 c4a3e5b1d1
a1b1e3b3a3d1 d3d2c5d2d4a3d1

e1e3b1a1a4e5a1 e3d2c4c4a3e5b1d1 d3e3d4d1 c4a3d1 d3d2c2d4d2a1a3d1 a3a1 c4e3 d4a4c3c4a3d1d1a3
d2c4 d5 e3 c4 a4c3d1a1e3b3c4a3 d3a3d1 d3d2d1a1e3d4b3a3d1 b4e3d2d1 c4e3 c5a3b1a1e5 a3d1a1 e3b3b3a3d1d1d2c3c4a3 e3
a1a4e5d1  a3c4c4a3 d4a3 d3a3d3e3d2c2d4a3 a2e3b4e3d2d1 c1e5d2b3a4d4c1e5a3 e2e3d2a1 a1e3d4a1 c1e5a3 d3a3 d1a3
a2e5c2a3b1 d3d2c2d4a3 d3 a3c4c4a3 c1e5a3c4d1 e1c4e5d1 c3a3e3e5b5 b4a4d3a3c4a3d1 e1a4e5b1 c5a4e5d1 c1e5a3 d3a3d1
b2a4b4b4a3d1 c1e5d2 e1a4e5c5e3d4a1 d1 d2d4d3d2c2d4a3b1 d3a3 d4 a3a1b1a3 e1a4d2d4a1 a3b5a3b4e1a1d1 d3a3 b3a3d1
b3e3c4e3b4d2a1a3d1 d4 a4d4a1 e1a4e5b1a1e3d4a1 e1e3d1 a1a3d4e5 e3 d2d4a2e5d1a1d2b3a3 d3 a3a1b1a3 a3d4 b3a3 d1a3e5c4
e1a4d2d4a1 e3d1d1d2b4d2c4a3d1 e3e5b5 e3e5a1b1a3d1 a3a1 d4 d5 a4d4a1 c5e5 c1e5a3 c4a3 d3b1a4d2a1 b3a4b4b4e5d4
d3a3 c4e3 b4a4b1a1 c1e5 d2c4d1 a4d4a1 d1e5c3d2a3 d1e3d4d1 b1a3d1d2d1a1e3d4b3a3 e2e3b1a4e5b3b2a3 b3a4b4b4a3 d1e3d4d1
b4a4c4c4a3d1d1a3 a3e2e2a3b4d2d4a3a3 b3e3b1 d4a3 e1a4d2d4a1 d1a3d4a1d2b1 d1a3d1 b4e3e5b5 b3 a3d1a1 d4 a3a1b1a3
e1e3d1 b2a4b4b4a3  d4a3 e1e3d1 c4a3d1 d1e5e1e1a4b1a1a3b1 b3 a3d1a1 b4e3d4c1e5a3b1 d3a3 b3a4e5b1e3c2a3

e3e1b1a3d1 e3c5a4d2b1 e1e3b1b3a4e5b1e5 c4e3 c4d2d1a1a3 d3a3 a1a4e5d1 c4a3d1 b3a3d1e3b1d1 c1e5a3 c4a3 d1a4b1a1 e3
e1b1d2c5a3d1 d3a3 d1a4a3e5b1d1 a4e5 d3a3 e2b1a3b1a3d1 a2a3 d4a3 e1e5d2d1 a3d4 a4e5c3c4d2a3b1 e5d4 c1e5d2 b4a3b1d2a1a3
e5d4a3 b4a3d4a1d2a4d4 d1e1a3b3d2e3c4a3 a3d4e2e3d4a1a3 e1e3b1 c4e3 d4e3a1e5b1a3 e1a4e5b1 c4e3 b1e5d2d4a3
a3a1 c4 a4e1e1b1a4c3b1a3 d3a3 c4 b2e5b4e3d4d2a1a3 e1a4e5b1 b1a3d4c5a3b1d1a3b1 d3a3 e2a4d4d3 a3d4 b3a4b4c3c4a3
e5d4 a3b4e1d2b1a3 c1e5a3 b1a3c4a3c5a3 c4e3 b3c4a3b4a3d4b3a3 d3e5 b4a3d2c4c4a3e5b1 d3a3d1 d1a4e5c5a3b1e3d2d4d1

b3e3c4d2c2e5c4e3 b3a3a1 b2a4b4b4a3 e3e5d1d1d2 d2d4b3e3e1e3c3c4a3 d3a3 d1a3 b1a3a2a4e5d2b1 c1e5a3 d3a3 d1 e3e2e2c4d2c2a3b1
a3d4 e1b1d2d4b3a3 a3c5d2a1e3 e3e1b1a3d1 c4e3 e1a3b1a1a3 d3a3 d1e3 d1a4a3e5b1 d3b1e5d1d2c4c4e3 c4e3 c5e5a3
a3a1 c4a3 b3a4b4b4a3b1b3a3 d3a3 d1a3d1 b3a4d4b3d2a1a4d5a3d4d1 d4 e3d1d1d2d1a1e3 e1e3d1 e3e5b5 a4c3d1a3c1e5a3d1
d3a3 b3a3a1a1a3 d1a4a3e5b1 d4a3 c4e5d2 b1a3d4d3d2a1 e1e3d1 c4a3d1 d3a3b1d4d2a3b1d1 d3a3c5a4d2b1d1 b4e3d2d1 b1a3a1d2b1a3
e3 d1e3 b4e3d2d1a4d4 d3 e3c4c3a3 b3b2a3b1b3b2e3 d3e3d4d1 c4a3d1 d3a3d1 d3e3d4d1 c4a3d1 b3e3d1a3d1 d3 e5d4a3
a1e3c3c4a3 d3a3 a2a3e5 a3a1 e3e5a1b1a3d1 d3d2d1a1b1e3b3a1d2a4d4d1 e1e3b1a3d2c4c4a3d1 c4a3 d1a4e5c4e3c2a3b4a3d4a1 d3e5
e1c4e5d1 b3b1e5a3c4 b3b2e3c2b1d2d4 a4 b2a4d4a1a3 d3e5 b1e3d4c2 d1e5e1b1a3b4a3 e5d4 a3b4e1a3b1a3e5b1
b1a4b4e3d2d4 e1c4a3e5b1a3 e5d4a3 d1a4a3e5b1 a3a1 b3a3 d1a4d4a1 c4a3d1 d3a3d1 c1e5d2 c4a3 b3a4d4d1a4c4a3d4a1

b3a3 b4a3b4a3 b3e3e5d1 d3e3d4d1 a1a4e5d1 c4a3d1 b3e3e1b1d2b3a3d1 d3e5 d3a3c4d2b1a3 a1e3d4a1a4a1 c4e3d2d1d1a3
b3b1a4a1b1a3 d1e3 c3e3b1c3a3 a3a1 d1a3d1 b3b2a3c5a3e5b5 a1e3d4a1a4a1 e1e3b1b3a4e5b1a1 a3d4 a3c2e3b1a3 c4a3d1
b1d2c5e3c2a3d1 d3 d2a1e3c4d2a3 a3a1 d3a3 d1d2b3d2c4a3 d4 a3a1e3d4a1 a2e3b4e3d2d1 c3d2a3d4 d1e5b1 d1 d2c4 c5a3e5a1
e1a4e5b1 d3b1e5d1d2c4c4e3 d3a3d1 e1c4a3e5b1d1 a4e5 d3a3d1 e3e5a1a3c4d1  b3e3b1 a3d4 b4a3b4a3 a1a3b4e1d1
c1e5 d2c4 c4e5d2 c5a4e5a3 d3a3d1 a1a3b4e1c4a3d1 a3a1 c4a3d1 b2a4d4d4a3e5b1d1 d3d2c5d2d4d1 d2c4 e2b1e3e1e1a3
d3a3d1 e1c4e5d1 b3b1e5a3c4d1 b3b2e3a1d2b4a3d4a1d1 c1e5d2b3a4d4c1e5a3 d4a3 b4a4d4a1b1a3 e1e3d1 e3d1d1a3a5
d3 e3e2e2c4d2b3a1d2a4d4 a4d4 c4a3 c5a4d2a1 e3e5d1d1d2 d2b4e1e3a1d2a3d4a1 d1a4e5d1 c4a3d1 b3a4e5e1d1 d3a3 c4e3
b4e3e5c5e3d2d1a3 e2a4b1a1e5d4a3 c1e5 d2c4 a3a1e3d2a1 d3e3d4d1 c4e3 e1b1a4d1e1a3b1d2a1a3 c2a4d4e2c4a3 d3 e5d4
a4b1c2e5a3d2c4 e1c4e5d1 c1e5 b2e5b4e3d2d4

a1a4e5a1a3 e3b4a3 b1a4b4e3d2d4a3 b1a3e1e5d3d2a3b1e3 c4 a3b5a3b4e1c4a3 d3 e5d4 d2d4d1a3d4d1a3 c1e5d2 a4e5c3c4d2a3 d1a4d4 d3a3e5d2c4
d3e3d4d1 d3a3d1 a2a3e5b5 b2a4b1d1 d3a3 d1e3d2d1a4d4 a4e5 c1e5d2 c4 e3d2c2b1d2a1 a3d4b3a4b1a3 e1e3b1 e5d4a3 d4a3c2c4d2c2a3d4b3a3 a3a1 e1e3b1 e5d4a3
b4e3c4e1b1a4e1b1a3a1a3 b1a3e1a4e5d1d1e3d4a1a3d1 a4e5 c1e5d2 d1a3 b3a4d4d1a4c4a3 a3d4 c3e3b1c3e3b1a3 e1e3b1 c4a3
b4e3c4 d3 e3e5a1b1e5d2

c1e5e3d4a1 e3 e1a4c4d5c3a3 d2c4 d4 e3 b1d2a3d4 d3e3d4d1 d1e3 b3a4d4d3e5d2a1a3 c1e5 d2c4
c4e5d2 e2e3d2c4c4a3 b3b2e3d4c2a3b1 d2c4 d1 a3d1a1 d3a3 c3a4d4d4a3 b2a3e5b1a3 e1e3d1d1d2a4d4d4a3 e1a4e5b1 b3a3d1
a3a1e5d3a3d1 c1e5d2 b1a3c4a3c5a3d4a1 d1d2 c3d2a3d4 c4a3 e1b1d2b5 d3a3 c4e3 e1b1a4d1e1a3b1d2a1a3 c1e5d2 e3c4c4a3c2a3d4a1
d1d2 e3d2d1a3b4a3d4a1 c4 d2d4e2a4b1a1e5d4a3 c1e5d2 e2a4d4a1 c4a3 e1c4e5d1 c3a3c4 a4b1d4a3b4a3d4a1
b3a4b4b4a3 c4e3 e1c4e5d1 d3a4e5b3a3 b3a4d4d1a4c4e3a1d2a4d4 d3a3 c4 b2a4b4b4a3
e1c4a4d4c2a3a5c5a4e5d1 d3a4d4b3 d3e3c5e3d4a1e3c2a3 a3d4b3a4b1a3 d3e3d4d1 c5a4d1 a3a1e5d3a3d1
b3b2a3b1d2a3d1 b3 a3d1a1 b4e3d2d4a1a3d4e3d4a1 c1e5 d2c4 e2e3e5a1 c5a4e5d1 a3d4 e2e3d2b1a3 b3a4b4b4a3 e5d4
b1a3b4e1e3b1a1 a4e5 c4e3 d3a4e5c4a3e5b1 d4a3 a1b1a4e5c5a3 e3e5b3e5d4a3 c3b1a3b3b2a3 e1a4e5b1 d1 d2d4a1b1a4d3e5d2b1a3
a2e5d1c1e5 e3 c5a4a1b1a3 e3b4a3

 c4e3 b4a3b4a4d2b1a3 d3a3 c5a4a1b1a3 e2b1a3b1a3 d3a3b4e3d4d3a3 e3e5d1d1d2 c1e5a3 c5a4a1b1a3 e1c4e5b4a3 c4e5d2 a3c4a3c5a3 e5d4
b4a4d4e5b4a3d4a1 d3e5b1e3c3c4a3 b3e3b1 c5a4d2c4e3 c4a3d1 d1a3e5c4a3d1 a4a3e5c5b1a3d1 d3a3 c4 b2a4b4b4a3 c1e5a3 d4 a4e5a1b1e3c2a3 d4e5c4c4a3
a1a3b4e1a3a1a3 c1e5a3 c4a3 a1a3b4e1d1 d4a3 b3a4d4d1e5b4a3 a2e3b4e3d2d1 a1a4e5a1 c4a3 b1a3d1a1a3 a3d4a1e3d1d1a3b4a3d4a1d1
d3a3 e1d2a3b1b1a3d1 b4e3e5d1a4c4a3a3d1 d3a3 b4e3b1c3b1a3 a1a4b4c3a3e3e5b5 d3a3 a1a3b1b1a3
a3c4a3c5a3d1 e3 d3 d2b4b4a3d4d1a3d1 b2e3e5a1a3e5b1d1 d4a3 e1b1a4c4a4d4c2a3d4a1 e1e3d1 d3a3 c3a3e3e5b3a4e5e1
d4a4a1b1a3 d4a4b4 d3a3d1a1d2d4a3d1 c1e5 d2c4d1 d1a4d4a1 e3 e1a3b1d2b1 b3a4b4b4a3 d4a4e5d1 d2c4 d4 a3d1a1
d3 d2d4d3a3d1a1b1e5b3a1d2c3c4a3 c1e5a3 c4a3d1 d1a4e5c5a3d4d2b1d1 a1b1e3d4d1b4d2d1 e1e3b1 c4a3 c2a3d4d2a3  a1a3c4 a3d1a1
c4a3 c2a3d4a3b1a3e5b5 b2a4b4b4e3c2a3 c4a3 a1a3b4e1c4a3 c1e5a3 c5a4e5d1 d3a3c5a3a5 e3 c5a4a1b1a3 e2b1a3b1a3
b3a4d4d1e3b3b1a3b1 d1a4d4 d4a4b4 d3e3d4d1 c5a4d1 e1b1a4d3e5b3a1d2a4d4d1 d2b4b4a4b1a1a3c4c4a3d1 c4e5d2 c5e3e5d3b1e3
b4d2a3e5b5 c1e5a3 d3a3d1 e1c4a3e5b1d1 a3a1 d3a3 d1a1a3b1d2c4a3d1 b1a3c2b1a3a1d1

 c1e5e3d4a1 e3 c4e3 e2a4b1a1e5d4a3 d1e3 b3e3e5d1a3 d2c4 a3d1a1 c5b1e3d2 d4a3 d1e3e5b1e3d2a1 d1a3 e1c4e3d2d3a3b1
b4e3d2d4a1a3d4e3d4a1 e3e5e1b1a3d1 d3a3 c5a4e5d1  b3e3b1 a1a4e5d1 d1a3d1 d3a4d4d1 d3a3d1 c1e5 a3c4c4a3
a3d4 e3 b1a3e1b1d2d1 e5d4 d1a3e5c4 d4a4e5d1 d3a3c5d2a3d4d4a3d4a1 e1e3b1 c4e3 b4a3b4a3 d1e5d1e1a3b3a1d1 a2a3
a1a3d4a1a3b1e3d2 d4a3e3d4b4a4d2d4d1 d3a3 c4e3 a2e5d1a1d2e2d2a3b1 d1d2a1a4a1 c1e5a3 c4a3 a1a3b4e1d1 e3e5b1e3
e2e3d2a1 d3a3 c5a4e5d1 e5d4 a2e5c2a3 e1c4e5d1 a3c1e5d2a1e3c3c4a3  e3c4a4b1d1 c5a4e5d1 e1a4e5b1b1a3a5 c5a4e5d1
b1a3b3a4d4b3d2c4d2a3b1 e3c5a3b3 a3c4c4a3 a3d4 a3e2e2a3a1 e1e3b1 b3a4b4c3d2a3d4 d3a3 c2b1e3b3a3d1 d4 e3a1a3c4c4a3
e1e3d1 d3 e3c5e3d4b3a3 b3a4b4e1a3d4d1a3 b3a3a1a1a3 e1b1a3b4d2a3b1a3 d2d4a2e5b1a3 e1e3b1 b3a4b4c3d2a3d4
d3a3 e2e3c5a3e5b1d1 d4a3 c5e3a1a3c4c4a3 e1e3d1 c4e3 b1e3b3b2a3a1a3b1 a3d4b3a4b1a3 a3a1 e3e1b1a3d1 a1a4e5a1
b3a3 c1e5 a3c4c4a3 c5a4e5d1 e3 b1e3c5d2 a3c4c4a3 c5a4e5d1 c4 e3c5e3d2a1 e3e5d1d1d2 d3a4d4d4a3

 d4 e3b1b4a3a5 d3a4d4b3 e1e3d1 b3a4d4a1b1a3 c5a4e5d1b4a3b4a3 c5a4a1b1a3 d2b4e3c2d2d4e3a1d2a4d4 d4 e3a1a1d2d1a3a5 e1e3d1
c5a4d1 d3a4e5c4a3e5b1d1 d1d2 c5a4a1b1a3 a3c4a4c1e5a3d4b3a3 e3 c4a3 e1a4e5c5a4d2b1 d3 e3c2b1e3d4d3d2b1 c4a3d1
e1a3a1d2a1a3d1 b3b2a4d1a3d1 a1a4e5a1 b3a4b4b4a3 d3a3 b1e3c3e3d2d1d1a3b1 a3a1 d3a3 b1a3d3e5d2b1a3 c4a3d1 c2b1e3d4d3a3d1
e3e5b5 e1c4e5d1 b4d2d4b3a3d1 e1b1a4e1a4b1a1d2a4d4d1 c1e5 a3c4c4a3 b1a3d1a3b1c5a3 b4e3d2d4a1a3d4e3d4a1 d1e3
c5d2c2e5a3e5b1 e1a4e5b1 e5d4 e3e5a1b1a3 e5d1e3c2a3 c1e5 a3c4c4a3 d1 a3b4e1c4a4d2a3 a1a4e5a1a3 e3 c5a4e5d1 b3a4d4d1a4c4a3b1
a3a1 e1a4e5b1a1e3d4a1 e1b1a3d4a3a5 c2e3b1d3a3  e1a3e5a1a3a1b1a3 d1a3d1 a3e2e2a4b1a1d1 d1a3b1e3d2a3d4a1d2c4d1
b4a3b4a3 d1e5e1a3b1e2c4e5d1  b3e3b1 a4d4 d4a3 d1 a3d4 a1d2a3d4a1 e1e3d1 e3 b3a3 c1e5 a3b5d2c2a3 d3a3
d4a4e5d1 c4e3 d4e3a1e5b1a3  c4e3 d3a4e5c4a3e5b1 e3 d1a4d4 e3e2e2a3b3a1e3a1d2a4d4

  a2e3b4e3d2d1 e3e5 b1a3d1a1a3 a2a3 d4a3 e1b1a3a1a3d4d3b1e3d2 c5a4e5d1 d2d4a1a3b1d3d2b1a3 a1a4e5a1a3 a1b1d2d1a1a3d1d1a3 a2a3 d1e3d2d1 c3d2a3d4
c1e5 d2c4 d1a3 a1b1a4e5c5a3 d3a3d1 c2a3d4d1 d3 e5d4a3 e1b2d2c4a4d1a4e1b2d2a3 d3e5b1a3 e1c4e5a1a4a1 c1e5a3 b3a4e5b1e3c2a3e5d1a3
c1e5d2 d4d2a3d4a1 c1e5a3 c4a3 d1e3c2a3 e1e5d2d1d1a3 b3a4d4d4e3a1b1a3 c4e3 d3a4e5c4a3e5b1 b4e3d2d1
d2c4 e1e3b1e3a1 c1e5a3 b3a3d1 b2a4b4b4a3d1 d4a3 d1a4d4a1 a2e3b4e3d2d1 a1a4b4c3a3d1 d3e3d4d1 c4a3d1 d1a4e5e2e2b1e3d4b3a3d1
e3e5a1b1a3b4a3d4a1 c4e3 e2a4b1a1e5d4a3 a3e5a1 d3a3b3a4d4b3a3b1a1a3 c4a3e5b1 e2d2a3b1a3 d1e3c2a3d1d1a3
a3a1 c4a3d1 a3e5a1 b3a4d4a1b1e3d2d4a1d1 a3d4 d3a3e1d2a1 d3 a3e5b5b4a3b4a3d1 e3 b3a4d4e2a3d1d1a3b1
c4e3 c5a3b1d2a1a3

 c4e3 b1e3d2d1a4d4 e3e5b1e3 e2e3d2a1 e3d1d1a3a5 d1d2 a3c4c4a3 b1a3a1b1e3d4b3b2a3 c4a3 d1e5e1a3b1e2c4e5
c4 a3b5b3a3d1 d3a3 c4e3 d3a4e5c4a3e5b1  c1e5e3d4a1 e3 c4e3 d1e5e1e1b1d2b4a3b1 a1a4e5a1a3 d4a3 c4 a3d1e1a3b1a4d4d1
d4a3 c4a3 d3a3d1d2b1a4d4d1 e1e3d1
c1e5 a3c4c4a3 c2e3b1d3a3 e1c4e5a1a4a1 e5d4a3 b4a3d1e5b1a3 c1e5d2 d1e3d4d1 b1a3d1d1a3b4c3c4a3b1 e3 c4 d2d4d1a3d4d1d2c3d2c4d2a1a3
d4d2 e3e5 d3a3c4d2b1a3 d4a4e5d1 b4e3d2d4a1d2a3d4d4a3 d3e3d4d1 c4 a3a1e3a1 d3 e5d4a3
e3b4a3 e3e2e2a3b3a1a3a3 b4e3d2d1 d4a4d4 a2a3a1a3a3 b2a4b1d1 d3a3 d1a4d4 d1d2a3c2a3 c1e5a3 c5a4d1 e1c4a3e5b1d1
b3a4e5c4a3d4a1 b4e3d2d1 c1e5 d2c4d1 b3a4e5c4a3d4a1 e1a4e5b1 b3a3d1d1a3b1 c3d2a3d4a1a4a1  c1e5a3 d3a3d1 c2a3b4d2d1d1a3b4a3d4a1d1
d1 a3b3b2e3e1e1a3d4a1 d3a3 b3a3 b3a4a3e5b1 c3b1d2d1a3  b4e3d2d1 c1e5 d2c4d1 e3d2a3d4a1
c4a3e5b1 a1a3b1b4a3 b1a3c2c4a3a5 c5a4a1b1a3 e3e2e2c4d2b3a1d2a4d4 d3a3 b4e3d4d2a3b1a3 e3 c4e3 a2e5d1a1d2e2d2a3b1
e3e5b5 d5a3e5b5 d3a3d1 d1e3c2a3d1 b3a4b4b4a3 e3 b3a3e5b5 d3a3 c5a4d1 e2b1a3b1a3d1

 e2e3d2a1a3d1 c1e5a3 c4e3 b4a3b4a4d2b1a3 d3a3 b3a3c4e5d2 c1e5d2 d4 a3d1a1 e1c4e5d1 e1e5d2d1d1a3 d1 a4e2e2b1d2b1 e3 c5a4e5d1
d1a4e5c5a3d4a1 a3a1 e3c5a3b3 b3b2e3b1b4a3  d3e3d4d1 c5a4d1 d3d2d1b3a4e5b1d1 e1e3b1c4a3a5 b4e3d2d4a1a3d1 e2a4d2d1 d3a3 c4e5d2
a3a1 c1e5a3 c5a4d1 d1a4e5c5a3d4d2b1d1 c5a4e5d1 c4a3 b1a3e1b1a3d1a3d4a1a3d4a1 d1e3d4d1 b3a3d1d1a3 a4b1 d2c4 e2e3e5a1
e1a4e5b1 b3a3c4e3 d1e3c5a4d2b1 a1b1a4e5c5a3b1 d3e3d4d1 b3a3d1 d1a4e5c5a3d4d2b1d1 e1c4e5d1 d3a3 d3a4e5b3a3e5b1
c1e5a3 d3 e3b4a3b1a1e5b4a3 b3e3b1 d2c4 a3d1a1 d4e3a1e5b1a3c4 c1e5a3 c4 a3d1e1b1d2a1 e2d2d4d2d1d1a3 e1e3b1 d1 a3c4a4d2c2d4a3b1
d3a3d1 e1a3d4d1a3a3d1 e3e5b5c1e5a3c4c4a3d1 d2c4 d4a3 b1a3c5d2a3d4a1 c1e5 e3c5a3b3 a1b1d2d1a1a3d1d1a3

 b1e3e1e1a3c4a3a5 c5a4e5d1 a1e3d4a1 d3a3 b4a4d3a3d1a1d2a3 a1e3d4a1 d3 e3e1a1d2a1e5d3a3 e3 a3d4a1b1a3e1b1a3d4d3b1a3
d3 b2e3c3d2c4a3a1a3 d3e3d4d1 c4 a3b5a3b3e5a1d2a4d4 d3a3 e2d2d3a3c4d2a1a3 d3e3d4d1 c4a3d1 a3d4c2e3c2a3b4a3d4a1d1
b1e3b3a4d4a1a3a5 e3e5b5 e3e5a1b1a3d1 a1a4e5a1a3d1 d1a3d1 e3b3a1d2a4d4d1 a1a4e5a1a3d1 d1a3d1 e1e3b1a4c4a3d1 a3a1
b1a3d3d2a1a3d1c5a4e5d1c4a3d1 e3 c5a4e5d1b4a3b4a3 e1a3d4d1a3a5 e3 b3a3 c1e5 d2c4 e2e5a1 a3a1 e3 a1a4e5a1
b3a3 c1e5 d2c4 e1b1a4b4a3a1a1e3d2a1 d3 a3a1b1a3 b3e3b1 c1e5a3 d4a3 e1a4e5c5e3d2a1a4d4 e1e3d1 b2e3b1d3d2b4a3d4a1 a3d1e1a3b1a3b1 d3 e5d4 a1a3c4
e2b1a3b1a3

 c5a4d2c4e3 a1a3c4c4a3d1 c1e5a3 a2a3 c4a3d1 e3d2 e1e5 b1a3d3d2c2a3b1 c4a3d1 b1a3e2c4a3b5d2a4d4d1 d3 e5d4
a3d1e1b1d2a1 d3a3d1 c4a4d4c2a1a3b4e1d1 e3e2e2e3d2d1d1a3 a3a1 e3e1e1a3d1e3d4a1d2 e1e3b1 c4e3 d3d2d1c2b1e3b3a3 d1d2
a3c4c4a3d1 c5a4e5d1 d1a3b4c3c4a3d4a1 e3e5d3a3d1d1a4e5d1 d3a3 c5a4a1b1a3 c2a3d4d2a3 a4e5 e1a3e5 e1b1a4e1b1a3d1
e3 c2e5a3b1d2b1 c5a4d1 d3a4e5c4a3e5b1d1 d1a4d4c2a3a5 b3a4b4c3d2a3d4 c4 b2a4b4b4a3 c1e5 a3d4c4e3b3a3d4a1
a3a1 e3c3d1a4b1c3a3d4a1 d1a3d1 e1b1a4e1b1a3d1 b4e3e5b5 b4e3d4c1e5a3 d3a3 c4a4d2d1d2b1 e1a4e5b1
b3a4d4d1a4c4a3b1 e3e5a1b1e5d2 a3a1 c1e5a3 c4a3d1 a1a3b1b4a3d1 d3a3 d4a4a1b1a3 d2d3d2a4b4a3 c5d2a3d4d4a3d4a1
d3d2e2e2d2b3d2c4a3b4a3d4a1 e3e5 c3e3d4d4d2 a3d4a1a4e5b1a3 d3a3 c3e3b1c3e3b1a3d1 d3a4d4a1 c4a3 c4e3d4c2e3c2a3
d3d2d1b3a4b1d3e3d4a1 b3b2a4c1e5e3d4a1 b4a3b4a3 e1a4e5b1 d3a3d1 c3e3b1c3e3b1a3d1 e5d4 e1a3e5 b3d2c5d2c4d2d1a3d1
e2b1a3b4d2a1 d2d4b3a3d1d1e3b4b4a3d4a1 e3 d1a4d4 a4b1a3d2c4c4a3

e1e3d1d1 / b4a4a1 d3a3 e1e3d1d1a3 : b3e1e3e3a4e5b1c3b5e1a2e1c2e2a4
~~~

We can use an [online monoalphabetic substitution solver](https://www.dcode.fr/monoalphabetic-substitution) to find the key, but first we must simplify the substitution:

~~~py
filename = "ch12.txt"
file = open(filename,"rt")
text = file.read()
file.close()
text = text.replace(" ","")
text = text.replace("\n","")
text = text.replace("/","")
text = text.replace(":","")

charlist = []

for i in range(0,len(text),2):
    charlist.append(text[i]+text[i+1])

charset = set(charlist)

file = open(filename,"rt")
text = file.read()
file.close()
letter = "A"
for x in list(charset):
    text = text.replace(x,letter)
    num = ord(letter)+1
    letter = chr(num)

file = open("newfile","wt")
file.write(text)
file.close()
~~~

This replaces the two-letter codes with single alphabetic characters. The key is:

~~~
xuvjgcoslzqbtinfehdymrapkw
~~~

The text can be solved:

~~~
filename = "ch12.txt"
file = open(filename,"rt")
text = file.read()
file.close()

dic = "ABCDEFGHIJKLMNOPQRSTUVWXYZ"
key = "xuvjgcoslzqbtinfehdymrapkw"

for i in range(len(dic)):
    text = text.replace(dic[i],key[i])
~~~

</details>

### Answer

<details>

<summary markdown="span">Answer</summary>

~~~
cpaaourbxpjpgfo
~~~

</details>

---

### [Cryptanalysis](#contents) | [Root-Me](./rootme.md) | [Home](./index.md)

---
 
Last updated Jan 2022.

## [djm89uk.github.io](https://djm89uk.github.io)
