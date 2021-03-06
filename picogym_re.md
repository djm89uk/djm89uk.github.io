
## [Home](https://djm89uk.github.io)

# [PicoGym](./picogym.m)
[picoCTF](https://picoCTF.org) provides a practice CTF environment called picoGym to allow individuals to work on their CTF skills outside of a formal CTF event.

# Reverse Engineering
Reverse engineering entails taking a software system and analyzing it to trace it back to the original design and implementation information. It is used to fix certain bugs in software as well as to enhance product features in both hardware and software.

## Contents
- [vault-door-training](#vault-door-training)
- [vault-door-1](#vault-door-1)
- [vault-door-3](#vault-door-3)
- [vault-door-4](#vault-door-4)
- [vault-door-5](#vault-door-5)
- [vault-door-6](#vault-door-6)
- [vault-door-7](#vault-door-7)
- [vault-door-8](#vault-door-8)
- [asm1](#asm1)
- [asm2](#asm2)
- [asm3](#asm3)
- [asm4](#asm4)
- [OTP Implementation](#otp-implementation)
- [droids0](#droids0)
- [droids1](#droids1)
- [droids2](#droids2)
- [droids3](#droids3)
- [droids4](#droids4)
- [revese_cipher](#reverse_cipher)
- [Need For Speed](#need-for-speed)
- [B1ll_Gat35](#b1ll_gat35)
- [Forky](#forky)

## vault-door-training

- Author: Mark E. Haase
- 50 Points

### Description

Your mission is to enter Dr. Evil's laboratory and retrieve the blueprints for his Doomsday Project. The laboratory is protected by a series of locked vault doors. Each door is controlled by a computer and requires a password to open. Unfortunately, our undercover agents have not been able to obtain the secret passwords for the vault doors, but one of our junior agents obtained the source code for each vault's computer! You will need to read the source code for each level to figure out what the password is for that vault door. As a warmup, we have created a replica vault in our training facility. The source code for the training vault is here: VaultDoorTraining.java

### Hints

1. The password is revealed in the program's source code.

### Attachments

<details>
<summary markdown="span">VaultDoorTraining.java</summary>

~~~java
// VaultDoorTraining.java
import java.util.*;

class VaultDoorTraining {
    public static void main(String args[]) {
        VaultDoorTraining vaultDoor = new VaultDoorTraining();
        Scanner scanner = new Scanner(System.in); 
        System.out.print("Enter vault password: ");
        String userInput = scanner.next();
	String input = userInput.substring("picoCTF{".length(),userInput.length()-1);
	if (vaultDoor.checkPassword(input)) {
	    System.out.println("Access granted.");
	} else {
	    System.out.println("Access denied!");
	}
   }

    // The password is below. Is it safe to put the password in the source code?
    // What if somebody stole our source code? Then they would know what our
    // password is. Hmm... I will think of some ways to improve the security
    // on the other doors.
    //
    // -Minion #9567
    public boolean checkPassword(String password) {
        return password.equals("w4rm1ng_Up_w1tH_jAv4_3808d338b46");
    }
}
~~~

</details>

### [Top](#contents)

---

## vault-door-1

- Author: Mark E. Haase
- 100 points

### Description

This vault uses some complicated arrays! I hope you can make sense of it, special agent. The source code for this vault is here: VaultDoor1.java

### Hints

1. Look up the [charAt() method online](https://www.w3schools.com/jsref/jsref_charat.asp){:target="_blank"}.

### Attachments

1. VaultDoor1.java

~~~java
// VaultDoor1.java
import java.util.*;

class VaultDoor1 {
    public static void main(String args[]) {
        VaultDoor1 vaultDoor = new VaultDoor1();
        Scanner scanner = new Scanner(System.in);
        System.out.print("Enter vault password: ");
	String userInput = scanner.next();
	String input = userInput.substring("picoCTF{".length(),userInput.length()-1);
	if (vaultDoor.checkPassword(input)) {
	    System.out.println("Access granted.");
	} else {
	    System.out.println("Access denied!");
	}
    }

    // I came up with a more secure way to check the password without putting
    // the password itself in the source code. I think this is going to be
    // UNHACKABLE!! I hope Dr. Evil agrees...
    //
    // -Minion #8728
    public boolean checkPassword(String password) {
        return password.length() == 32 &&
               password.charAt(0)  == 'd' &&
               password.charAt(29) == 'a' &&
               password.charAt(4)  == 'r' &&
               password.charAt(2)  == '5' &&
               password.charAt(23) == 'r' &&
               password.charAt(3)  == 'c' &&
               password.charAt(17) == '4' &&
               password.charAt(1)  == '3' &&
               password.charAt(7)  == 'b' &&
               password.charAt(10) == '_' &&
               password.charAt(5)  == '4' &&
               password.charAt(9)  == '3' &&
               password.charAt(11) == 't' &&
               password.charAt(15) == 'c' &&
               password.charAt(8)  == 'l' &&
               password.charAt(12) == 'H' &&
               password.charAt(20) == 'c' &&
               password.charAt(14) == '_' &&
               password.charAt(6)  == 'm' &&
               password.charAt(24) == '5' &&
               password.charAt(18) == 'r' &&
               password.charAt(13) == '3' &&
               password.charAt(19) == '4' &&
               password.charAt(21) == 'T' &&
               password.charAt(16) == 'H' &&
               password.charAt(27) == '6' &&
               password.charAt(30) == 'f' &&
               password.charAt(25) == '_' &&
               password.charAt(22) == '3' &&
               password.charAt(28) == 'd' &&
               password.charAt(26) == 'f' &&
               password.charAt(31) == '4';
    }
}
~~~

### [Top](#contents)

---

## vault-door-3

- Author: Mark E. Haase
- 200 points

### Description

This vault uses [for-loops](https://www.w3schools.com/java/java_for_loop.asp){:target="_blank"} and [byte arrays](https://www.w3schools.com/java/java_ref_string.asp){:target="_blank"}. The source code for this vault is here: VaultDoor3.java

### Hints

1. Make a table that contains each value of the loop variables and the corresponding buffer index that it writes to.

### Attachments

1. VaultDoor3.java

~~~java
// VaultDoor3.java
import java.util.*;

class VaultDoor3 {
    public static void main(String args[]) {
        VaultDoor3 vaultDoor = new VaultDoor3();
        Scanner scanner = new Scanner(System.in);
        System.out.print("Enter vault password: ");
        String userInput = scanner.next();
	String input = userInput.substring("picoCTF{".length(),userInput.length()-1);
	if (vaultDoor.checkPassword(input)) {
	    System.out.println("Access granted.");
	} else {
	    System.out.println("Access denied!");
        }
    }

    // Our security monitoring team has noticed some intrusions on some of the
    // less secure doors. Dr. Evil has asked me specifically to build a stronger
    // vault door to protect his Doomsday plans. I just *know* this door will
    // keep all of those nosy agents out of our business. Mwa ha!
    //
    // -Minion #2671
    public boolean checkPassword(String password) {
        if (password.length() != 32) {
            return false;
        }
        char[] buffer = new char[32];
        int i;
        for (i=0; i<8; i++) {
            buffer[i] = password.charAt(i);
        }
        for (; i<16; i++) {
            buffer[i] = password.charAt(23-i);
        }
        for (; i<32; i+=2) {
            buffer[i] = password.charAt(46-i);
        }
        for (i=31; i>=17; i-=2) {
            buffer[i] = password.charAt(i);
        }
        String s = new String(buffer);
        return s.equals("jU5t_a_sna_3lpm12g94c_u_4_m7ra41");
    }
}
~~~

### [Top](#contents)

---

## vault-door-4

- Author: Mark E. Haase
- 250 points

### Description

This vault uses [ASCII encoding](https://en.wikipedia.org/wiki/ASCII){:target="_blank"} for the password. The source code for this vault is here: VaultDoor4.java

### Hints

1. Use a search engine to find an ["ASCII table"](http://www.asciitable.com/){:target="_blank"}.
2. You will also need to know the difference between [octal](https://en.wikipedia.org/wiki/Octal){:target="_blank"}, [decimal](https://en.wikipedia.org/wiki/Decimal){:target="_blank"}, and [hexadecimal](https://en.wikipedia.org/wiki/Hexadecimal){:target="_blank"} numbers.

### Attachments

1. VaultDoor4.java

~~~java
// VaultDoor4.java
import java.util.*;

class VaultDoor4 {
    public static void main(String args[]) {
        VaultDoor4 vaultDoor = new VaultDoor4();
        Scanner scanner = new Scanner(System.in);
        System.out.print("Enter vault password: ");
        String userInput = scanner.next();
	String input = userInput.substring("picoCTF{".length(),userInput.length()-1);
	if (vaultDoor.checkPassword(input)) {
	    System.out.println("Access granted.");
	} else {
	    System.out.println("Access denied!");
        }
    }

    // I made myself dizzy converting all of these numbers into different bases,
    // so I just *know* that this vault will be impenetrable. This will make Dr.
    // Evil like me better than all of the other minions--especially Minion
    // #5620--I just know it!
    //
    //  .:::.   .:::.
    // :::::::.:::::::
    // :::::::::::::::
    // ':::::::::::::'
    //   ':::::::::'
    //     ':::::'
    //       ':'
    // -Minion #7781
    public boolean checkPassword(String password) {
        byte[] passBytes = password.getBytes();
        byte[] myBytes = {
            106 , 85  , 53  , 116 , 95  , 52  , 95  , 98  ,
            0x55, 0x6e, 0x43, 0x68, 0x5f, 0x30, 0x66, 0x5f,
            0142, 0131, 0164, 063 , 0163, 0137, 0146, 064 ,
            'a' , '8' , 'c' , 'd' , '8' , 'f' , '7' , 'e' ,
        };
        for (int i=0; i<32; i++) {
            if (passBytes[i] != myBytes[i]) {
                return false;
            }
        }
        return true;
    }
}
~~~

### [Top](#contents)

---

## vault-door-5

- Author: Mark E. Haase
- 300 points

### Description

In the last challenge, you mastered octal (base 8), decimal (base 10), and hexadecimal (base 16) numbers, but this vault door uses a different change of base as well as URL encoding! The source code for this vault is here: VaultDoor5.java

### Hints

1. You may find an encoder/decoder tool helpful, such as [https://encoding.tools/](https://encoding.tools/){:target="_blank"}.
2. Read the wikipedia articles on [URL encoding](https://en.wikipedia.org/wiki/Percent-encoding){:target="_blank"} and [base 64 encoding](https://en.wikipedia.org/wiki/Base64){:target="_blank"} to understand how they work and what the results look like.

### Attachments

1. VaultDoor5.java

~~~java
// VaultDoor5.java
import java.net.URLDecoder;
import java.util.*;

class VaultDoor5 {
    public static void main(String args[]) {
        VaultDoor5 vaultDoor = new VaultDoor5();
        Scanner scanner = new Scanner(System.in);
        System.out.print("Enter vault password: ");
        String userInput = scanner.next();
	String input = userInput.substring("picoCTF{".length(),userInput.length()-1);
	if (vaultDoor.checkPassword(input)) {
	    System.out.println("Access granted.");
	} else {
	    System.out.println("Access denied!");
        }
    }

    // Minion #7781 used base 8 and base 16, but this is base 64, which is
    // like... eight times stronger, right? Riiigghtt? Well that's what my twin
    // brother Minion #2415 says, anyway.
    //
    // -Minion #2414
    public String base64Encode(byte[] input) {
        return Base64.getEncoder().encodeToString(input);
    }

    // URL encoding is meant for web pages, so any double agent spies who steal
    // our source code will think this is a web site or something, defintely not
    // vault door! Oh wait, should I have not said that in a source code
    // comment?
    //
    // -Minion #2415
    public String urlEncode(byte[] input) {
        StringBuffer buf = new StringBuffer();
        for (int i=0; i<input.length; i++) {
            buf.append(String.format("%%%2x", input[i]));
        }
        return buf.toString();
    }

    public boolean checkPassword(String password) {
        String urlEncoded = urlEncode(password.getBytes());
        String base64Encoded = base64Encode(urlEncoded.getBytes());
        String expected = "JTYzJTMwJTZlJTc2JTMzJTcyJTc0JTMxJTZlJTY3JTVm"
                        + "JTY2JTcyJTMwJTZkJTVmJTYyJTYxJTM1JTY1JTVmJTM2"
                        + "JTM0JTVmJTM4JTM0JTY2JTY0JTM1JTMwJTM5JTM1";
        return base64Encoded.equals(expected);
    }
}
~~~

### [Top](#contents)

---

## vault-door-6

- Author: Mark E. Haase
- 350 points

### Description

This vault uses an XOR encryption scheme. The source code for this vault is here: VaultDoor6.java

### Hints

1. If X ^ Y = Z, then Z ^ Y = X. Write a program that decrypts the flag based on this fact.

### Attachments

1. VaultDoor6.java

~~~java
// VaultDoor6.java
import java.util.*;

class VaultDoor6 {
    public static void main(String args[]) {
        VaultDoor6 vaultDoor = new VaultDoor6();
        Scanner scanner = new Scanner(System.in);
        System.out.print("Enter vault password: ");
        String userInput = scanner.next();
	String input = userInput.substring("picoCTF{".length(),userInput.length()-1);
	if (vaultDoor.checkPassword(input)) {
	    System.out.println("Access granted.");
	} else {
	    System.out.println("Access denied!");
        }
    }

    // Dr. Evil gave me a book called Applied Cryptography by Bruce Schneier,
    // and I learned this really cool encryption system. This will be the
    // strongest vault door in Dr. Evil's entire evil volcano compound for sure!
    // Well, I didn't exactly read the *whole* book, but I'm sure there's
    // nothing important in the last 750 pages.
    //
    // -Minion #3091
    public boolean checkPassword(String password) {
        if (password.length() != 32) {
            return false;
        }
        byte[] passBytes = password.getBytes();
        byte[] myBytes = {
            0x3b, 0x65, 0x21, 0xa , 0x38, 0x0 , 0x36, 0x1d,
            0xa , 0x3d, 0x61, 0x27, 0x11, 0x66, 0x27, 0xa ,
            0x21, 0x1d, 0x61, 0x3b, 0xa , 0x2d, 0x65, 0x27,
            0xa , 0x66, 0x36, 0x30, 0x67, 0x6c, 0x64, 0x6c,
        };
        for (int i=0; i<32; i++) {
            if (((passBytes[i] ^ 0x55) - myBytes[i]) != 0) {
                return false;
            }
        }
        return true;
    }
}
~~~

### [Top](#contents)

---

## vault-door-7

- Author: Mark E. Haase
- 400 points

### Description

This vault uses bit shifts to convert a password string into an array of integers. Hurry, agent, we are running out of time to stop Dr. Evil's nefarious plans! The source code for this vault is here: VaultDoor7.java

### Hints

1. Use a decimal/hexadecimal converter such as [this one](https://www.mathsisfun.com/binary-decimal-hexadecimal-converter.html){:target="_blank"}.
2. You will also need to consult an ASCII table such as [this one](https://www.asciitable.com/){:target="_blank"}.

### Attachments

1. VaultDoor7.java

~~~java
// VaultDoor7.java
import java.util.*;
import javax.crypto.Cipher;
import javax.crypto.spec.SecretKeySpec;
import java.security.*;

class VaultDoor7 {
    public static void main(String args[]) {
        VaultDoor7 vaultDoor = new VaultDoor7();
        Scanner scanner = new Scanner(System.in);
        System.out.print("Enter vault password: ");
        String userInput = scanner.next();
	String input = userInput.substring("picoCTF{".length(),userInput.length()-1);
	if (vaultDoor.checkPassword(input)) {
	    System.out.println("Access granted.");
	} else {
	    System.out.println("Access denied!");
        }
    }

    // Each character can be represented as a byte value using its
    // ASCII encoding. Each byte contains 8 bits, and an int contains
    // 32 bits, so we can "pack" 4 bytes into a single int. Here's an
    // example: if the hex string is "01ab", then those can be
    // represented as the bytes {0x30, 0x31, 0x61, 0x62}. When those
    // bytes are represented as binary, they are:
    //
    // 0x30: 00110000
    // 0x31: 00110001
    // 0x61: 01100001
    // 0x62: 01100010
    //
    // If we put those 4 binary numbers end to end, we end up with 32
    // bits that can be interpreted as an int.
    //
    // 00110000001100010110000101100010 -> 808542562
    //
    // Since 4 chars can be represented as 1 int, the 32 character password can
    // be represented as an array of 8 ints.
    //
    // - Minion #7816
    public int[] passwordToIntArray(String hex) {
        int[] x = new int[8];
        byte[] hexBytes = hex.getBytes();
        for (int i=0; i<8; i++) {
            x[i] = hexBytes[i*4]   << 24
                 | hexBytes[i*4+1] << 16
                 | hexBytes[i*4+2] << 8
                 | hexBytes[i*4+3];
        }
        return x;
    }

    public boolean checkPassword(String password) {
        if (password.length() != 32) {
            return false;
        }
        int[] x = passwordToIntArray(password);
        return x[0] == 1096770097
            && x[1] == 1952395366
            && x[2] == 1600270708
            && x[3] == 1601398833
            && x[4] == 1716808014
            && x[5] == 1734293296
            && x[6] == 842413104
            && x[7] == 1684157793;
    }
}
~~~

### [Top](#contents)

---

## vault-door-8

- Author: Mark E. Haase
- 450 points

### Description

Apparently Dr. Evil's minions knew that our agency was making copies of their source code, because they intentionally sabotaged this source code in order to make it harder for our agents to analyze and crack into! The result is a quite mess, but I trust that my best special agent will find a way to solve it. The source code for this vault is here: VaultDoor8.java

### Hints

1. Clean up the source code so that you can read it and understand what is going on.
2. Draw a diagram to illustrate which bits are being switched in the scramble() method, then figure out a sequence of bit switches to undo it. You should be able to reuse the switchBits() method as is.

### Attachments

1. VaultDoor8.java

~~~java
// VaultDoor8.java
// These pesky special agents keep reverse engineering our source code and then
// breaking into our secret vaults. THIS will teach those sneaky sneaks a
// lesson.
//
// -Minion #0891
import java.util.*; import javax.crypto.Cipher; import javax.crypto.spec.SecretKeySpec;
import java.security.*; class VaultDoor8 {public static void main(String args[]) {
Scanner b = new Scanner(System.in); System.out.print("Enter vault password: ");
String c = b.next(); String f = c.substring(8,c.length()-1); VaultDoor8 a = new VaultDoor8(); if (a.checkPassword(f)) {System.out.println("Access granted."); }
else {System.out.println("Access denied!"); } } public char[] scramble(String password) {/* Scramble a password by transposing pairs of bits. */
char[] a = password.toCharArray(); for (int b=0; b<a.length; b++) {char c = a[b]; c = switchBits(c,1,2); c = switchBits(c,0,3); /* c = switchBits(c,14,3); c = switchBits(c, 2, 0); */ c = switchBits(c,5,6); c = switchBits(c,4,7);
c = switchBits(c,0,1); /* d = switchBits(d, 4, 5); e = switchBits(e, 5, 6); */ c = switchBits(c,3,4); c = switchBits(c,2,5); c = switchBits(c,6,7); a[b] = c; } return a;
} public char switchBits(char c, int p1, int p2) {/* Move the bit in position p1 to position p2, and move the bit
that was in position p2 to position p1. Precondition: p1 < p2 */ char mask1 = (char)(1 << p1);
char mask2 = (char)(1 << p2); /* char mask3 = (char)(1<<p1<<p2); mask1++; mask1--; */ char bit1 = (char)(c & mask1); char bit2 = (char)(c & mask2); /* System.out.println("bit1 " + Integer.toBinaryString(bit1));
System.out.println("bit2 " + Integer.toBinaryString(bit2)); */ char rest = (char)(c & ~(mask1 | mask2)); char shift = (char)(p2 - p1); char result = (char)((bit1<<shift) | (bit2>>shift) | rest); return result;
} public boolean checkPassword(String password) {char[] scrambled = scramble(password); char[] expected = {
0xF4, 0xC0, 0x97, 0xF0, 0x77, 0x97, 0xC0, 0xE4, 0xF0, 0x77, 0xA4, 0xD0, 0xC5, 0x77, 0xF4, 0x86, 0xD0, 0xA5, 0x45, 0x96, 0x27, 0xB5, 0x77, 0xD2, 0xD0, 0xB4, 0xE1, 0xC1, 0xE0, 0xD0, 0xD0, 0xE0 }; return Arrays.equals(scrambled, expected); } }
~~~

### [Top](#contents)

---

## asm1

- Author: Sanjay C
- 200 points

### Description

What does asm1(0x8be) return? Submit the flag as a hexadecimal value (starting with '0x'). NOTE: Your submission for this question will NOT be in the normal flag format. Source

### Hints

1. [assembly conditions](https://www.tutorialspoint.com/assembly_programming/assembly_conditions.htm){:target="_blank"}.

### Attachments

1. test.S

~~~nasm
asm1:
	<+0>:	push   ebp
	<+1>:	mov    ebp,esp
	<+3>:	cmp    DWORD PTR [ebp+0x8],0x71c
	<+10>:	jg     0x512 <asm1+37>
	<+12>:	cmp    DWORD PTR [ebp+0x8],0x6cf
	<+19>:	jne    0x50a <asm1+29>
	<+21>:	mov    eax,DWORD PTR [ebp+0x8]
	<+24>:	add    eax,0x3
	<+27>:	jmp    0x529 <asm1+60>
	<+29>:	mov    eax,DWORD PTR [ebp+0x8]
	<+32>:	sub    eax,0x3
	<+35>:	jmp    0x529 <asm1+60>
	<+37>:	cmp    DWORD PTR [ebp+0x8],0x8be
	<+44>:	jne    0x523 <asm1+54>
	<+46>:	mov    eax,DWORD PTR [ebp+0x8]
	<+49>:	sub    eax,0x3
	<+52>:	jmp    0x529 <asm1+60>
	<+54>:	mov    eax,DWORD PTR [ebp+0x8]
	<+57>:	add    eax,0x3
	<+60>:	pop    ebp
	<+61>:	ret    
~~~

### [Top](#contents)

---

## asm2

- Author: Sanjay C
- 250 points

### Description

What does asm2(0xb,0x2e) return? Submit the flag as a hexadecimal value (starting with '0x'). NOTE: Your submission for this question will NOT be in the normal flag format. Source

### Hints

1. [assembly conditions](https://www.tutorialspoint.com/assembly_programming/assembly_conditions.htm){:target="_blank"}.

### Attachments

1. test.S

~~~nasm
asm2:
	<+0>:	push   ebp
	<+1>:	mov    ebp,esp
	<+3>:	sub    esp,0x10
	<+6>:	mov    eax,DWORD PTR [ebp+0xc]
	<+9>:	mov    DWORD PTR [ebp-0x4],eax
	<+12>:	mov    eax,DWORD PTR [ebp+0x8]
	<+15>:	mov    DWORD PTR [ebp-0x8],eax
	<+18>:	jmp    0x509 <asm2+28>
	<+20>:	add    DWORD PTR [ebp-0x4],0x1
	<+24>:	sub    DWORD PTR [ebp-0x8],0xffffff80
	<+28>:	cmp    DWORD PTR [ebp-0x8],0x63f3
	<+35>:	jle    0x501 <asm2+20>
	<+37>:	mov    eax,DWORD PTR [ebp-0x4]
	<+40>:	leave  
	<+41>:	ret    
~~~

### [Top](#contents)

---

## asm3

- Author: Sanjay C
- 300 points

### Description

What does asm3(0xba6c5a02,0xd101e3dd,0xbb86a173) return? Submit the flag as a hexadecimal value (starting with '0x'). NOTE: Your submission for this question will NOT be in the normal flag format. Source

### Hints

1. [more(?) registers](https://wiki.skullsecurity.org/index.php?title=Registers){:target="_blank"}.

### Attachments

1. test.S

~~~nasm
asm3:
	<+0>:	push   ebp
	<+1>:	mov    ebp,esp
	<+3>:	xor    eax,eax
	<+5>:	mov    ah,BYTE PTR [ebp+0xb]
	<+8>:	shl    ax,0x10
	<+12>:	sub    al,BYTE PTR [ebp+0xd]
	<+15>:	add    ah,BYTE PTR [ebp+0xc]
	<+18>:	xor    ax,WORD PTR [ebp+0x12]
	<+22>:	nop
	<+23>:	pop    ebp
	<+24>:	ret    
~~~

### [Top](#contents)

---

## asm4

- Author: Sanjay C
- 400 points

### Description

What will asm4("picoCTF_f97bb") return? Submit the flag as a hexadecimal value (starting with '0x'). NOTE: Your submission for this question will NOT be in the normal flag format. Source

### Hints

1. Treat the Array argument as a pointer

### Attachments

1. test.S

~~~nasm
asm4:
	<+0>:	push   ebp
	<+1>:	mov    ebp,esp
	<+3>:	push   ebx
	<+4>:	sub    esp,0x10
	<+7>:	mov    DWORD PTR [ebp-0x10],0x27a
	<+14>:	mov    DWORD PTR [ebp-0xc],0x0
	<+21>:	jmp    0x518 <asm4+27>
	<+23>:	add    DWORD PTR [ebp-0xc],0x1
	<+27>:	mov    edx,DWORD PTR [ebp-0xc]
	<+30>:	mov    eax,DWORD PTR [ebp+0x8]
	<+33>:	add    eax,edx
	<+35>:	movzx  eax,BYTE PTR [eax]
	<+38>:	test   al,al
	<+40>:	jne    0x514 <asm4+23>
	<+42>:	mov    DWORD PTR [ebp-0x8],0x1
	<+49>:	jmp    0x587 <asm4+138>
	<+51>:	mov    edx,DWORD PTR [ebp-0x8]
	<+54>:	mov    eax,DWORD PTR [ebp+0x8]
	<+57>:	add    eax,edx
	<+59>:	movzx  eax,BYTE PTR [eax]
	<+62>:	movsx  edx,al
	<+65>:	mov    eax,DWORD PTR [ebp-0x8]
	<+68>:	lea    ecx,[eax-0x1]
	<+71>:	mov    eax,DWORD PTR [ebp+0x8]
	<+74>:	add    eax,ecx
	<+76>:	movzx  eax,BYTE PTR [eax]
	<+79>:	movsx  eax,al
	<+82>:	sub    edx,eax
	<+84>:	mov    eax,edx
	<+86>:	mov    edx,eax
	<+88>:	mov    eax,DWORD PTR [ebp-0x10]
	<+91>:	lea    ebx,[edx+eax*1]
	<+94>:	mov    eax,DWORD PTR [ebp-0x8]
	<+97>:	lea    edx,[eax+0x1]
	<+100>:	mov    eax,DWORD PTR [ebp+0x8]
	<+103>:	add    eax,edx
	<+105>:	movzx  eax,BYTE PTR [eax]
	<+108>:	movsx  edx,al
	<+111>:	mov    ecx,DWORD PTR [ebp-0x8]
	<+114>:	mov    eax,DWORD PTR [ebp+0x8]
	<+117>:	add    eax,ecx
	<+119>:	movzx  eax,BYTE PTR [eax]
	<+122>:	movsx  eax,al
	<+125>:	sub    edx,eax
	<+127>:	mov    eax,edx
	<+129>:	add    eax,ebx
	<+131>:	mov    DWORD PTR [ebp-0x10],eax
	<+134>:	add    DWORD PTR [ebp-0x8],0x1
	<+138>:	mov    eax,DWORD PTR [ebp-0xc]
	<+141>:	sub    eax,0x1
	<+144>:	cmp    DWORD PTR [ebp-0x8],eax
	<+147>:	jl     0x530 <asm4+51>
	<+149>:	mov    eax,DWORD PTR [ebp-0x10]
	<+152>:	add    esp,0x10
	<+155>:	pop    ebx
	<+156>:	pop    ebp
	<+157>:	ret    
~~~

### [Top](#contents)

---

## OTP Implementation

- Author: madStacks
- 300 points

### Description

Yay reversing! Relevant files: otp flag.txt

### Hints

1. [https://sourceware.org/gdb/onlinedocs/gdb/Python-API.html](https://sourceware.org/gdb/onlinedocs/gdb/Python-API.html){:target="_blank"}.
2. I think [GDB Python](https://wiki.python.org/moin/DebuggingWithGdb){:target="_blank"} is very useful, you can solve this problem without it, but can you solve future problems (hint hint)?
3. Also test your skills by solving this with [ANGR](https://github.com/angr/angr){:target="_blank"}!

### Attachments

1. otp (binary file)
2. flag.txt:

~~~
18a07fbdbcd1af759895328ec4d82d2b411dc7876c34a0ab61eda8f2efa5bb0f198a3aa0ac47ff9a0cf3d913d3138678ce4b
~~~

### [Top](#contents)

---

## droids0

- Author: Jason
- 300 points

### Description

Where do droid logs go. Check out this file.

### Hints

1. Try using an emulator or device
2. [https://developer.android.com/studio](https://developer.android.com/studio){:target="_blank"}.

### Attachments

1. zero.apk

### [Top](#contents)

---

## droids1

- Author: Jason
- 350 points

### Description

Find the pass, get the flag. Check out this file.

### Hints

1. Try using [apktool](https://ibotpeaches.github.io/Apktool/){:target="_blank"} and an [emulator](https://developer.android.com/studio){:target="_blank"}.
2. [https://ibotpeaches.github.io/Apktool/](https://ibotpeaches.github.io/Apktool/){:target="_blank"}.
3. [https://developer.android.com/studio](https://developer.android.com/studio){:target="_blank"}.

### Attachments

1. one.apk

### [Top](#contents)

---

## droids2

- Author: Jason
- 400 points

### Description

Find the pass, get the flag. Check out this file.

### Hints

1. Try using [apktool](https://ibotpeaches.github.io/Apktool/){:target="_blank"} and an [emulator](https://developer.android.com/studio){:target="_blank"}.
2. [https://ibotpeaches.github.io/Apktool/](https://ibotpeaches.github.io/Apktool/){:target="_blank"}.
3. [https://developer.android.com/studio](https://developer.android.com/studio){:target="_blank"}.

### Attachments

1. two.apk

### [Top](#contents)

---

## droids3

- Author: Jason
- 450 points

### Description

Find the pass, get the flag. Check out this file.

### Hints

1. Try using [apktool](https://ibotpeaches.github.io/Apktool/){:target="_blank"} and an [emulator](https://developer.android.com/studio){:target="_blank"}.
2. [https://ibotpeaches.github.io/Apktool/](https://ibotpeaches.github.io/Apktool/){:target="_blank"}.
3. [https://developer.android.com/studio](https://developer.android.com/studio){:target="_blank"}.

### Attachments

1. three.apk

### [Top](#contents)

---

## droids4

- Author: Jason
- 500 points

### Description

Reverse the pass, patch the file, get the flag. Check out this file.

### Hints

None

### Attachments

1. four.apk

### [Top](#contents)

---

## reverse_cipher

- Author: Danny Tunitis
- 300 points

### Description

We have recovered a binary and a text file. Can you reverse the flag.
### Hints

1. [objdump](https://en.wikipedia.org/wiki/Objdump){:target="_blank"} and [Gihdra](https://ghidra-sre.org/){:target="_blank"} are some tools that could assist with this.

### Attachments

1. "rev" binary
2. "rev_this" text file:

~~~
picoCTF{w1{1wq8/7376j.:}
~~~

### [Top](#contents)

---

## Need For Speed

- Author: Alexander Bushkin
- 400 points

### Description

The name of the game is speed. Are you quick enough to solve this problem and keep it above 50 mph? need-for-speed.

### Hints

1. What is the final key?

### Links

1. [https://www.youtube.com/watch?v=8piqd2BWeGI](https://www.youtube.com/watch?v=8piqd2BWeGI){:target="_blank"}

### Attachments

1. "need-for-speed" binary file.

### [Top](#contents)

---

## B1ll_Gat35

- Author: Alex Bushkin
- 400 points

### Description

Can you reverse this Windows Binary?

### Hints

1. Microsoft provides [windows virtual machines](https://developer.microsoft.com/en-us/windows/downloads/virtual-machines){:target="_blank"}.
2. [Ollydbg](http://www.ollydbg.de/){:target="_blank"} may be helpful.
3. Flag format: PICOCTF{XXXX}.

### Attachments

1. win-exec-1.exe

### [Top](#contents)

---

## Forky

- Author: Samuel
- 500 points

### Description

In this program, identify the last integer value that is passed as parameter to the function doNothing().

### Hints

1. What happens when you fork? The flag is picoCTF{IntegerYouFound}. For example, if you found that the last integer passed was 1234, the flag would be picoCTF{1234}

### Attachments

1. "vuln" binary file.

### [Top](#contents)

---

# [djm89uk homepage](https://djm89uk.github.io)
