# [Root-Me](./rootme.md) Root-Me Cryptanalysis [11/56]

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
12. [ELF64 - PID encryption](#elf64-pid-encryption)
13. [File - PKZIP](#file-pkzip)
14. [Monoalphabetic substitution - Caesar](#monoalphabetic-substitution-caesar)
15. [Known plaintext - XOR](#known-plaintext-xOr)
16. [Code - Pseudo Random Number Generator](#code-pseudo-random-number-generator)
17. [File - Insecure storage 1](#file-insecure-storage-1)
18. [Polyalphabetic substitution - Vigenère](#polyalphabetic-substitution-vigenère)
19. [System - Android lock pattern](#system-android-lock-pattern)
20. [Transposition - Rail Fence](#transposition-rail-fence)
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

## Hash MD5

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

Last updated Jan 2022.

## [djm89uk.github.io](https://djm89uk.github.io)
