# [Root-Me](./rootme.md) Root-Me Cryptanalysis [18/56]

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
18. [Polyalphabetic substitution - Vigenère](#polyalphabetic-substitution-vigenère) 🗸
19. [System - Android lock pattern](#system-android-lock-pattern)
20. [Transposition - Rail Fence](#transposition-rail-fence) 🗸
21. [AES - CBC - Bit-Flipping Attack](#aes-cbc-bit-flipping-attack)
22. [AES - ECB](#aes-ecb)
23. [LFSR - Known plaintext](#lfsr-known-plaintext)
24. [RSA - Factorisation](#rsa-factorisation)
25. [RSA - Decipher Oracle](#rsa-decipher-pracle)
26. [Service - Timing attack](#service-timing-attack)
27. [Monoalphabetic substitution - Polybe](#monoalphabetic-substitution-polybe)
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
 
Last updated Jan 2022.

## [djm89uk.github.io](https://djm89uk.github.io)
