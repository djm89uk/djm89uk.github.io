# [PicoGym](./picogym.md) Reverse Engineering

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
- [revese_cipher](#reverse-cipher)
- [Need For Speed](#need-for-speed)
- [B1ll_Gat35](#b1ll-gat35)
- [Forky](#forky)

---

### [Reverse Engineering](#contents) | [PicoGym](./picogym.md) | [PicoCTF](./picoctf.md) | [Home](./index.md)

---

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

### Solutions

<details>

<summary markdown="span">Solution 1</summary>

The flag can be read directly from the VaultDoorTraining.java source file.

Reviewing the source code we can see a class "VaultDoorTraining" is defined and a new "VaultDoorTraining" class object "VaultDoor" is created:

~~~java
class VaultDoorTraining {
    public static void main(String args[]) {
        VaultDoorTraining vaultDoor = new VaultDoorTraining();
~~~

Next, the code creates a new object, "scanner" of the ["Scanner" class](https://www.w3schools.com/java/java_user_input.asp), part of the java.util package.  The code then prints a string to the terminal: "Enter vault password: ".  The user input string is stored in a new String object "userInput":

~~~java
Scanner scanner = new Scanner(System.in); 
System.out.print("Enter vault password: ");
String userInput = scanner.next();
~~~

The next part of the code, creates a new String object, "input" and assigns the value to a substring of the user input "userInput" String object.  The first component of the string, "picoCTF{" is removed, and the final character is removed.  The substring "input" is subseuqently passed to the "checkPassword" Method.  This returns a boolean that determines the print string indicating if the password is successful:

~~~java
String input = userInput.substring("picoCTF{".length(),userInput.length()-1);
if (vaultDoor.checkPassword(input)) {
    System.out.println("Access granted.");
} else {
    System.out.println("Access denied!");
}
~~~

The "checkPassword" Method is a simple equivalence comparator that returns 1 (True) if all characters in the object "input" match a predefined string, or 0 (False) if any character if the strings are not equivalent:

~~~java
public boolean checkPassword(String password) {
    return password.equals("w4rm1ng_Up_w1tH_jAv4_3808d338b46");
}
~~~

We can thus infer the correct flag is:

~~~
picoCTF{w4rm1ng_Up_w1tH_jAv4_3808d338b46}
~~~

This password can be tested using the java class file.  First the .java needs to be compiled into a class:

~~~
$ javac -d ./build VaultDoorTraining.java
~~~

This creates a build directory with "VaultDoorTraining.class".  We can call this class directly from java:

~~~
$ cd build
$ java VaultDoorTraining
Picked up _JAVA_OPTIONS: -Dawt.useSystemAAFontSettings=on -Dswing.aatext=true
Enter vault password: 
~~~

We can enter the flag and receive an Authentication message:

~~~
Enter vault password: picoCTF{w4rm1ng_Up_w1tH_jAv4_3808d338b46}
Access granted.
~~~

Due to the string handling, the password must contain the string w4rm1ng_Up_w1tH_jAv4_3808d338b46 in positions [8..39] and must be exactly 41 characters in length.  However, the picoCTF{ and } characters can be replaced with any ascii input and access is granted:

~~~
Enter vault password: !"£$%^&*w4rm1ng_Up_w1tH_jAv4_3808d338b46@
Access granted.
~~~

However, if we shorten the string by removing the last character:

~~~
Enter vault password: !"£$%^&*w4rm1ng_Up_w1tH_jAv4_3808d338b46
Access denied!
~~~

Or if we add an erroneous character to the end of the string:

~~~
Enter vault password: !"£$%^&*w4rm1ng_Up_w1tH_jAv4_3808d338b46@@
Access denied!
~~~

</details>

### Answer

<details>
<summary markdown="span">Flag</summary>

~~~
picoCTF{w4rm1ng_Up_w1tH_jAv4_3808d338b46}
~~~

</details>

---

### [Reverse Engineering](#contents) | [PicoGym](./picogym.md) | [PicoCTF](./picoctf.md) | [Home](./index.md)

---

## vault-door-1

- Author: Mark E. Haase
- 100 points

### Description

This vault uses some complicated arrays! I hope you can make sense of it, special agent. The source code for this vault is here: VaultDoor1.java

### Hints

1. Look up the [charAt() method online](https://www.w3schools.com/jsref/jsref_charat.asp).

### Attachments

<details>

<summary markdown="span">VaultDoor1.java</summary>

~~~java
// VaultDoor1.java
import java.util.*;

class VaultDoor1 {
    public static void main(String args[]) {
        VaultDoor1 vaultDoor = new VaultDoor1();
        Scanner scanner = new Scanner(System.in);
        System.out.print("Enter vault password: ");
	String userInput = scanner.next();
	String input = userInput.substring("
	{".length(),userInput.length()-1);
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

</details>

### Solutions

<details>

<summary markdown="span">Solution 1</summary>

This problem has the password in plaintext within the source code, with the string index values checked non-linearly.  The password could be read manually by recording each index value, however, we can edit this java file to print the password with some simple substitutions of the source.  A useful function for generating the password string literal is [StringBuilder](https://docs.oracle.com/javase/tutorial/java/data/buffers.html).  This has been completed under a new class name, "VaultDoor1_modified":

~~~java
import java.util.*;

class VaultDoor1_modified {
    public static void main(String args[]) {
        VaultDoor1_modified vaultDoor = new VaultDoor1_modified();
        vaultDoor.showPassword();
//        Scanner scanner = new Scanner(System.in);
//        System.out.print("Enter vault password: ");
//	String userInput = scanner.next();
//	String input = userInput.substring("picoCTF{".length(),userInput.length()-1);
//	if (vaultDoor.checkPassword(input)) {
//	    System.out.println("Access granted.");
//	} else {
//	    System.out.println("Access denied!");
//	}
    }

    // I came up with a more secure way to check the password without putting
    // the password itself in the source code. I think this is going to be
    // UNHACKABLE!! I hope Dr. Evil agrees...
    //
    // -Minion #8728
    public boolean showPassword() {
        StringBuilder password = new StringBuilder("abcdefghijklmnopqrstuvwxyzABCDEF");
        password.setCharAt(0,'d');
        password.setCharAt(29, 'a');
        password.setCharAt(4, 'r');
        password.setCharAt(2, '5');
        password.setCharAt(23, 'r');
        password.setCharAt(3, 'c');
        password.setCharAt(17, '4');
        password.setCharAt(1, '3');
        password.setCharAt(7, 'b');
        password.setCharAt(10, '_');
        password.setCharAt(5, '4');
        password.setCharAt(9, '3');
        password.setCharAt(11, 't');
        password.setCharAt(15, 'c');
        password.setCharAt(8, 'l');
        password.setCharAt(12, 'H');
        password.setCharAt(20, 'c');
        password.setCharAt(14, '_');
        password.setCharAt(6, 'm');
        password.setCharAt(24, '5');
        password.setCharAt(18, 'r');
        password.setCharAt(13, '3');
        password.setCharAt(19, '4');
        password.setCharAt(21, 'T');
        password.setCharAt(16, 'H');
        password.setCharAt(27, '6');
        password.setCharAt(30, 'f');
        password.setCharAt(25, '_');
        password.setCharAt(22, '3');
        password.setCharAt(28, 'd');
        password.setCharAt(26, 'f');
        password.setCharAt(31, '4');
        System.out.println(password);
        
        return true;
    }
}
~~~

This can be compiled:

~~~
$ javac -d ./build VaultDoor1_modified.java  
~~~

And run:

~~~
$ java ./build/VaultDoor1_modified
~~~

This returns:

~~~
d35cr4mbl3_tH3_cH4r4cT3r5_f6daf4
~~~

which is our flag.


</details>

### Answer

<details>

<summary markdown="span">Flag</summary>

~~~
picoCTF{d35cr4mbl3_tH3_cH4r4cT3r5_f6daf4}
~~~

</details>

---

### [Reverse Engineering](#contents) | [PicoGym](./picogym.md) | [PicoCTF](./picoctf.md) | [Home](./index.md)

---

## vault-door-3

- Author: Mark E. Haase
- 200 points

### Description

This vault uses [for-loops](https://www.w3schools.com/java/java_for_loop.asp) and [byte arrays](https://www.w3schools.com/java/java_ref_string.asp). The source code for this vault is here: VaultDoor3.java

### Hints

1. Make a table that contains each value of the loop variables and the corresponding buffer index that it writes to.

### Attachments

<details>
	
<summary markdown="span">VaultDoor3.java</summary>

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

</details>

### Solutions

<details>

<summary markdown="span">Solution 1</summary>

This challenge again scrambles the password before comparison.  A simple method givePassword() can be added to a new file, VaultDoor3_modified to reverse the assignments in checkPassword as shown below.

~~~java
import java.util.*;

class VaultDoor3_modified {
    public static void main(String args[]) {
        VaultDoor3_modified vaultDoor = new VaultDoor3_modified();
        Scanner scanner = new Scanner(System.in);
        System.out.print("Enter vault password: ");
        String userInput = scanner.next();
	String input = userInput.substring("picoCTF{".length(),userInput.length()-1);
	if (vaultDoor.checkPassword(input)) {
	    System.out.println("Access granted.");
	} else {
	    System.out.println("Access denied!");
	    System.out.println("The Password is:");
            vaultDoor.givePassword();
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
    public boolean givePassword(){
    	String scrambled = new String("jU5t_a_sna_3lpm12g94c_u_4_m7ra41");
        char[] buffer = new char[32];
        int i;
        for (i=0; i<8; i++) {
            buffer[i] = scrambled.charAt(i);
        }
        for (; i<16; i++) {
            buffer[23-i] = scrambled.charAt(i);
        }
        for (; i<32; i+=2) {
            buffer[46-i] = scrambled.charAt(i);
        }
        for (i=31; i>=17; i-=2) {
            buffer[i] = scrambled.charAt(i);
        }
        String password = new String(buffer);
        System.out.println(password);
        return true;
    }
}
~~~

This can be compiled:

~~~
$ javac VaultDoor3_modified.java
~~~

The original method is called.  When running the class, we must make a trivial guess at the password.  This rejects the password after checkPassword method is called and prints the correct password from the showPassword method:

~~~
$ java VaultDoor3_modified                                             1 ⚙
Picked up _JAVA_OPTIONS: -Dawt.useSystemAAFontSettings=on -Dswing.aatext=true
Enter vault password: picoCTF{guess}
Access denied!
The Password is:
jU5t_a_s1mpl3_an4gr4m_4_u_c79a21
~~~

We can check the password locally by entering this back in:

~~~
$ java VaultDoor3_modified                                             1 ⚙
Picked up _JAVA_OPTIONS: -Dawt.useSystemAAFontSettings=on -Dswing.aatext=true
Enter vault password: picoCTF{jU5t_a_s1mpl3_an4gr4m_4_u_c79a21}
Access granted.
~~~

</details>

### Answer

<details>

<summary markdown="span">Flag</summary>

~~~
picoCTF{jU5t_a_s1mpl3_an4gr4m_4_u_c79a21}
~~~

</details>

---

### [Reverse Engineering](#contents) | [PicoGym](./picogym.md) | [PicoCTF](./picoctf.md) | [Home](./index.md)

---

## vault-door-4

- Author: Mark E. Haase
- 250 points

### Description

This vault uses [ASCII encoding](https://en.wikipedia.org/wiki/ASCII) for the password. The source code for this vault is here: VaultDoor4.java

### Hints

1. Use a search engine to find an ["ASCII table"](http://www.asciitable.com/).
2. You will also need to know the difference between [octal](https://en.wikipedia.org/wiki/Octal), [decimal](https://en.wikipedia.org/wiki/Decimal), and [hexadecimal](https://en.wikipedia.org/wiki/Hexadecimal) numbers.

### Attachments

<details>

<summary markdown="span">VaultDoor4.java</summary>

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

</details>

### Solutions

<details>

<summary markdown="span">Solution 1</summary>

This challenge compares an input password in a byte array.  The input string is converted using the [getBytes()](https://www.w3resource.com/java-tutorial/string/string_getbytes.php) method.

Again, we can create a modified program, adding a showPassword method with an inverse of the comparison within checkPassword():

~~~java
import java.util.*;

class VaultDoor4_modified {
    public static void main(String args[]) {
        VaultDoor4_modified vaultDoor = new VaultDoor4_modified();
        Scanner scanner = new Scanner(System.in);
        System.out.print("Enter vault password: ");
        String userInput = scanner.next();
	String input = userInput.substring("picoCTF{".length(),userInput.length()-1);
	if (vaultDoor.checkPassword(input)) {
	    System.out.println("Access granted.");
	} else {
	    System.out.println("Access denied!");
	    System.out.println("Password Is:");
	    vaultDoor.showPassword();
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
    public boolean showPassword(){
        byte[] passBytes = {
            106 , 85  , 53  , 116 , 95  , 52  , 95  , 98  ,
            0x55, 0x6e, 0x43, 0x68, 0x5f, 0x30, 0x66, 0x5f,
            0142, 0131, 0164, 063 , 0163, 0137, 0146, 064 ,
            'a' , '8' , 'c' , 'd' , '8' , 'f' , '7' , 'e' ,
        };
	String password = new String(passBytes);
	System.out.println(password);
    	return true;
    }
}
~~~

This can be compiled:

~~~
$ javac VaultDoor4_modified.java 
~~~

When run, we have to enter a password guess.  The program returns the correct password:

~~~
$ java VaultDoor4_modified                                             1 ⚙
Picked up _JAVA_OPTIONS: -Dawt.useSystemAAFontSettings=on -Dswing.aatext=true
Enter vault password: picoCTF{guess}
Access denied!
Password Is:
jU5t_4_bUnCh_0f_bYt3s_f4a8cd8f7e
~~~

This can be checked locally to ensure it is correct using the unmodified checkPassword() method:

~~~
$ java VaultDoor4_modified                                             1 ⚙
Picked up _JAVA_OPTIONS: -Dawt.useSystemAAFontSettings=on -Dswing.aatext=true
Enter vault password: picoCTF{jU5t_4_bUnCh_0f_bYt3s_f4a8cd8f7e}
Access granted.
~~~

The flag is therefore picoCTF{jU5t_4_bUnCh_0f_bYt3s_f4a8cd8f7e}.

</details>

### Answer

<details>

<summary markdown="span">Flag</summary>

~~~
picoCTF{jU5t_4_bUnCh_0f_bYt3s_f4a8cd8f7e}
~~~

</details>

---

### [Reverse Engineering](#contents) | [PicoGym](./picogym.md) | [PicoCTF](./picoctf.md) | [Home](./index.md)

---

## vault-door-5

- Author: Mark E. Haase
- 300 points

### Description

In the last challenge, you mastered octal (base 8), decimal (base 10), and hexadecimal (base 16) numbers, but this vault door uses a different change of base as well as URL encoding! The source code for this vault is here: VaultDoor5.java

### Hints

1. You may find an encoder/decoder tool helpful, such as [https://encoding.tools/](https://encoding.tools/).
2. Read the wikipedia articles on [URL encoding](https://en.wikipedia.org/wiki/Percent-encoding) and [base 64 encoding](https://en.wikipedia.org/wiki/Base64) to understand how they work and what the results look like.

### Attachments

<details>

<summary markdown="span">VaultDoor5.java</summary>

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

</details>

### Solutions

<details>

<summary markdown="span">Solution 1</summary>

This challenge encodes the user input string into URL and Base64 bytes before comparing to an encoded passphrase.  We can create a modified version of the java class "VaultDoor5_modified" and create inversion methods using the [Base64 decoder](https://www.baeldung.com/java-base64-encode-and-decode) and the URL decoder that is hinted in the source code as an imported external library, [URLDeocder](https://www.baeldung.com/java-url-encoding-decoding):

~~~java
import java.net.URLDecoder;
import java.util.*;

class VaultDoor5_modified {
    public static void main(String args[]) {
        VaultDoor5_modified vaultDoor = new VaultDoor5_modified();
        Scanner scanner = new Scanner(System.in);
        System.out.print("Enter vault password: ");
        String userInput = scanner.next();
	String input = userInput.substring("picoCTF{".length(),userInput.length()-1);
	if (vaultDoor.checkPassword(input)) {
	    System.out.println("Access granted.");
	} else {
	    System.out.println("Access denied!");
	    System.out.println("Password is:");
	    vaultDoor.showPassword();
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
    public String base64Decode(String encodedString) {
    	byte[] decodedBytes = Base64.getDecoder().decode(encodedString);
    	String decodedString = new String(decodedBytes);
        return decodedString;
    }
    public String urlDecode(String value) {
        return URLDecoder.decode(value);
    }
    public boolean showPassword(){
    	String b64password = new String("JTYzJTMwJTZlJTc2JTMzJTcyJTc0JTMxJTZlJTY3JTVm"
                        + "JTY2JTcyJTMwJTZkJTVmJTYyJTYxJTM1JTY1JTVmJTM2"
                        + "JTM0JTVmJTM4JTM0JTY2JTY0JTM1JTMwJTM5JTM1");
	String urlpassword = base64Decode(b64password);
	String password = urlDecode(urlpassword);
	System.out.println(password);
        return true;
    }
}
~~~

THis can be compiled:

~~~
$ javac VaultDoor5_modified.java
~~~

And we can run the code with an initial password guess.  The method showPassword will give us the correct passphrase:

~~~
$ java VaultDoor5_modified                                             1 ⚙
Picked up _JAVA_OPTIONS: -Dawt.useSystemAAFontSettings=on -Dswing.aatext=true
Enter vault password: picoCTF{guess}
Access denied!
Password is:
c0nv3rt1ng_fr0m_ba5e_64_84fd5095
~~~

This can be checked locally by entering in the correct passphrase:

~~~
$ java VaultDoor5_modified                                             1 ⚙
Picked up _JAVA_OPTIONS: -Dawt.useSystemAAFontSettings=on -Dswing.aatext=true
Enter vault password: picoCTF{c0nv3rt1ng_fr0m_ba5e_64_84fd5095}
Access granted.
~~~

This shows us the correct flag is picoCTF{c0nv3rt1ng_fr0m_ba5e_64_84fd5095}.

</details>

### Answer

<details>

<summary markdown="span">Flag</summary>

~~~
picoCTF{c0nv3rt1ng_fr0m_ba5e_64_84fd5095}
~~~

</details>

---

### [Reverse Engineering](#contents) | [PicoGym](./picogym.md) | [PicoCTF](./picoctf.md) | [Home](./index.md)

---

## vault-door-6

- Author: Mark E. Haase
- 350 points

### Description

This vault uses an XOR encryption scheme. The source code for this vault is here: VaultDoor6.java

### Hints

1. If X ^ Y = Z, then Z ^ Y = X. Write a program that decrypts the flag based on this fact.

### Attachments

<details>

<summary markdown="span">VaultDoor6.java</summary>

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

</details>

### Solutions

<details>

<summary markdown="span">Solution 1</summary>

This challenge uses XOR binary operation on the use input passphrase to compare to a binary array holding the correct password.  This can be inverted as described in the challenge hint, where A^B=C then C^B=A.

We can invert the checkPassword method with a new showPassword method.  We need a correctly sized byte array, passBytes, in which the correct password (after XOR operation) will be stored and myBytes, which will hold the compared byte array:

~~~java
import java.util.*;

class VaultDoor6_modified {
    public static void main(String args[]) {
        VaultDoor6_modified vaultDoor = new VaultDoor6_modified();
        Scanner scanner = new Scanner(System.in);
        System.out.print("Enter vault password: ");
        String userInput = scanner.next();
	String input = userInput.substring("picoCTF{".length(),userInput.length()-1);
	if (vaultDoor.checkPassword(input)) {
	    System.out.println("Access granted.");
	} else {
	    System.out.println("Access denied!");
	    System.out.println("Password is:");
	    vaultDoor.showPassword();
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
    public boolean showPassword() {
    	byte[] passBytes = {
            0x00, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00,
            0x00, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00,
            0x00, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00,
            0x00, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00,
        };
        byte[] myBytes = {
            0x3b, 0x65, 0x21, 0xa , 0x38, 0x0 , 0x36, 0x1d,
            0xa , 0x3d, 0x61, 0x27, 0x11, 0x66, 0x27, 0xa ,
            0x21, 0x1d, 0x61, 0x3b, 0xa , 0x2d, 0x65, 0x27,
            0xa , 0x66, 0x36, 0x30, 0x67, 0x6c, 0x64, 0x6c,
        };
        for (int i=0; i<32; i++) {
            passBytes[i] = (byte) (myBytes[i] ^ 0x55);
        }
        String password = new String(passBytes);
	System.out.println(password);
        
        return true;
    }
}
~~~

This can be compiled:

~~~
$ javac VaultDoor6_modified.java 
~~~

When run, we enter a password guess, and the correct password is returned:

~~~
$ java VaultDoor6_modified                                             1 ⚙
Picked up _JAVA_OPTIONS: -Dawt.useSystemAAFontSettings=on -Dswing.aatext=true
Enter vault password: picoCTF{guess}
Access denied!
Password is:
n0t_mUcH_h4rD3r_tH4n_x0r_3ce2919
~~~

We can verify this is the correct password locally:

~~~
$ java VaultDoor6_modified                                             1 ⚙
Picked up _JAVA_OPTIONS: -Dawt.useSystemAAFontSettings=on -Dswing.aatext=true
Enter vault password: picoCTF{n0t_mUcH_h4rD3r_tH4n_x0r_3ce2919}
Access granted.
~~~

The flag is therefore picoCTF{n0t_mUcH_h4rD3r_tH4n_x0r_3ce2919}.

</details>

### Answer

<details>

<summary markdown="span">Flag</summary>

~~~
picoCTF{n0t_mUcH_h4rD3r_tH4n_x0r_3ce2919}
~~~

</details>

---

### [Reverse Engineering](#contents) | [PicoGym](./picogym.md) | [PicoCTF](./picoctf.md) | [Home](./index.md)

---

## vault-door-7

- Author: Mark E. Haase
- 400 points

### Description

This vault uses bit shifts to convert a password string into an array of integers. Hurry, agent, we are running out of time to stop Dr. Evil's nefarious plans! The source code for this vault is here: VaultDoor7.java

### Hints

1. Use a decimal/hexadecimal converter such as [this one](https://www.mathsisfun.com/binary-decimal-hexadecimal-converter.html).
2. You will also need to consult an ASCII table such as [this one](https://www.asciitable.com/).

### Attachments

<details>

<summary markdown="span">VaultDoor7.java</summary>

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

</details>

### Solutions

<details>

<summary markdown="span">Solution 1</summary>

THis challenge uses bit shifting to split the user-submitted passphrase into 8, 4-letter byte arrays that are encoding into a large integer.  Each substring is appended into a byte array using bit shifting operations.

Similar to before, we can simply generate a new method, showPassword, and invert the checkPassword method:

~~~java
import java.util.*;
import javax.crypto.Cipher;
import javax.crypto.spec.SecretKeySpec;
import java.security.*;

class VaultDoor7_modified {
    public static void main(String args[]) {
        VaultDoor7_modified vaultDoor = new VaultDoor7_modified();
        Scanner scanner = new Scanner(System.in);
        System.out.print("Enter vault password: ");
        String userInput = scanner.next();
	String input = userInput.substring("picoCTF{".length(),userInput.length()-1);
	if (vaultDoor.checkPassword(input)) {
	    System.out.println("Access granted.");
	} else {
	    System.out.println("Access denied!");
	    System.out.println("Password is:");
	    vaultDoor.showPassword();
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
    public String IntArrayToPassword(int[] array){
    	byte[] passBytes = new byte[32];
    	for (int i=0; i<8; i++){
    	    byte[] buffer = new byte[]{
    	        (byte)(array[i] >> 24),
    	        (byte)(array[i] >> 16),
    	        (byte)(array[i] >> 8),
    	        (byte)array[i],
    	    };
    	    for (int j=0; j<4; j++){
    	        passBytes[i*4+j] = (byte) buffer[j];
    	    }
	}
	return new String(passBytes);
    }
    public boolean showPassword() {
    	int[] array = {
    	    1096770097, 1952395366, 1600270708, 1601398833, 
    	    1716808014, 1734293296,  842413104, 1684157793
    	};
        String password = IntArrayToPassword(array);
        System.out.println(password);
        return true;
    }
}
~~~

This can be compiled:

~~~
$ javac VaultDoor7_modified.java 
~~~

When run, we are prompted for a password and when the checkPassword method returns a false boolean, the correct password is printed when showPassword method is called:

~~~
$ java VaultDoor7_modified                                             1 ⚙
Picked up _JAVA_OPTIONS: -Dawt.useSystemAAFontSettings=on -Dswing.aatext=true
Enter vault password: picoCTF{guess}
Access denied!
Password is:
A_b1t_0f_b1t_sh1fTiNg_702640db5a
~~~

We can check the passphrase locally within the checkPassword Method:

~~~
$ java VaultDoor7_modified                                             1 ⚙
Picked up _JAVA_OPTIONS: -Dawt.useSystemAAFontSettings=on -Dswing.aatext=true
Enter vault password: picoCTF{A_b1t_0f_b1t_sh1fTiNg_702640db5a}
Access granted.
~~~

Therefore the flag is picoCTF{A_b1t_0f_b1t_sh1fTiNg_702640db5a}.

</details>

### Answer

<details>

<summary markdown="span">Flag</summary>

~~~
picoCTF{A_b1t_0f_b1t_sh1fTiNg_702640db5a}
~~~

</details>

---

### [Reverse Engineering](#contents) | [PicoGym](./picogym.md) | [PicoCTF](./picoctf.md) | [Home](./index.md)

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

<details>

<summary markdown="span">VaultDoor8.java</summary>

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

</details>

### Solutions

<details>

<summary markdown="span">Solution 1</summary>

First, we need to sort out the formatting of the java file.  A useful online resource for formatting code is [codebeautify.org](https://codebeautify.org).  There is a specific interface for java: [javaviewer](https://codebeautify.org/javaviewer).  This gives us a legible java file:

~~~java
// These pesky special agents keep reverse engineering our source code and then
// breaking into our secret vaults. THIS will teach those sneaky sneaks a
// lesson.
//
// -Minion #0891
import java.util.*;
import javax.crypto.Cipher;
import javax.crypto.spec.SecretKeySpec;
import java.security.*;
class VaultDoor8 {
  public static void main(String args[]) {
    Scanner b = new Scanner(System.in);
    System.out.print("Enter vault password: ");
    String c = b.next();
    String f = c.substring(8, c.length() - 1);
    VaultDoor8 a = new VaultDoor8();
    if (a.checkPassword(f)) {
      System.out.println("Access granted.");
    } else {
      System.out.println("Access denied!");
    }
  }
  public char[] scramble(String password) {
    /* Scramble a password by transposing pairs of bits. */
    char[] a = password.toCharArray();
    for (int b = 0; b < a.length; b++) {
      char c = a[b];
      c = switchBits(c, 1, 2);
      c = switchBits(c, 0, 3); /* c = switchBits(c,14,3); c = switchBits(c, 2, 0); */
      c = switchBits(c, 5, 6);
      c = switchBits(c, 4, 7);
      c = switchBits(c, 0, 1); /* d = switchBits(d, 4, 5); e = switchBits(e, 5, 6); */
      c = switchBits(c, 3, 4);
      c = switchBits(c, 2, 5);
      c = switchBits(c, 6, 7);
      a[b] = c;
    }
    return a;
  }
  public char switchBits(char c, int p1, int p2) {
    /* Move the bit in position p1 to position p2, and move the bit
    that was in position p2 to position p1. Precondition: p1 < p2 */
    char mask1 = (char)(1 << p1);
    char mask2 = (char)(1 << p2); /* char mask3 = (char)(1<<p1<<p2); mask1++; mask1--; */
    char bit1 = (char)(c & mask1);
    char bit2 = (char)(c & mask2);
    /* System.out.println("bit1 " + Integer.toBinaryString(bit1));
System.out.println("bit2 " + Integer.toBinaryString(bit2)); */
    char rest = (char)(c & ~(mask1 | mask2));
    char shift = (char)(p2 - p1);
    char result = (char)((bit1 << shift) | (bit2 >> shift) | rest);
    return result;
  }
  public boolean checkPassword(String password) {
    char[] scrambled = scramble(password);
    char[] expected = {
      0xF4, 0xC0, 0x97, 0xF0, 0x77, 0x97, 0xC0, 0xE4, 
      0xF0, 0x77, 0xA4, 0xD0, 0xC5, 0x77, 0xF4, 0x86,
      0xD0, 0xA5, 0x45, 0x96, 0x27, 0xB5, 0x77, 0xD2, 
      0xD0, 0xB4, 0xE1, 0xC1, 0xE0, 0xD0, 0xD0, 0xE0
    };
    return Arrays.equals(scrambled, expected);
  }
}
~~~

As before, we will work on a modified class, VaultDoor8_modified.java.  We can invert the Method scramble, using a new Method unscamble by reversing the scamble order and passing a char array to the Method.  A new Method showPassword will take the scrambled passphrase and return an unscrambled string:

~~~java
// These pesky special agents keep reverse engineering our source code and then
// breaking into our secret vaults. THIS will teach those sneaky sneaks a
// lesson.
//
// -Minion #0891
import java.util.*;
import javax.crypto.Cipher;
import javax.crypto.spec.SecretKeySpec;
import java.security.*;
class VaultDoor8_modified {
  public static void main(String args[]) {
    Scanner b = new Scanner(System.in);
    System.out.print("Enter vault password: ");
    String c = b.next();
    String f = c.substring(8, c.length() - 1);
    VaultDoor8_modified a = new VaultDoor8_modified();
    if (a.checkPassword(f)) {
      System.out.println("Access granted.");
    } else {
      System.out.println("Access denied!");
      System.out.println("Password is:");
      a.showPassword();
    }
  }
  public char[] scramble(String password) {
    /* Scramble a password by transposing pairs of bits. */
    char[] a = password.toCharArray();
    for (int b = 0; b < a.length; b++) {
      char c = a[b];
      c = switchBits(c, 1, 2);
      c = switchBits(c, 0, 3); /* c = switchBits(c,14,3); c = switchBits(c, 2, 0); */
      c = switchBits(c, 5, 6);
      c = switchBits(c, 4, 7);
      c = switchBits(c, 0, 1); /* d = switchBits(d, 4, 5); e = switchBits(e, 5, 6); */
      c = switchBits(c, 3, 4);
      c = switchBits(c, 2, 5);
      c = switchBits(c, 6, 7);
      a[b] = c;
    }
    return a;
  }
  public char switchBits(char c, int p1, int p2) {
    /* Move the bit in position p1 to position p2, and move the bit
    that was in position p2 to position p1. Precondition: p1 < p2 */
    char mask1 = (char)(1 << p1);
    char mask2 = (char)(1 << p2); /* char mask3 = (char)(1<<p1<<p2); mask1++; mask1--; */
    char bit1 = (char)(c & mask1);
    char bit2 = (char)(c & mask2);
    /* System.out.println("bit1 " + Integer.toBinaryString(bit1));
System.out.println("bit2 " + Integer.toBinaryString(bit2)); */
    char rest = (char)(c & ~(mask1 | mask2));
    char shift = (char)(p2 - p1);
    char result = (char)((bit1 << shift) | (bit2 >> shift) | rest);
    return result;
  }
  public boolean checkPassword(String password) {
    char[] scrambled = scramble(password);
    char[] expected = {
      0xF4, 0xC0, 0x97, 0xF0, 0x77, 0x97, 0xC0, 0xE4, 
      0xF0, 0x77, 0xA4, 0xD0, 0xC5, 0x77, 0xF4, 0x86,
      0xD0, 0xA5, 0x45, 0x96, 0x27, 0xB5, 0x77, 0xD2, 
      0xD0, 0xB4, 0xE1, 0xC1, 0xE0, 0xD0, 0xD0, 0xE0
    };
    return Arrays.equals(scrambled, expected);
  }
  public String unscramble(char[] passChar) {
    /* uncramble a password by transposing pairs of bits. */
    for (int b = 0; b < passChar.length; b++) {
      char c = passChar[b];
      c = switchBits(c, 6, 7);
      c = switchBits(c, 2, 5);
      c = switchBits(c, 3, 4);
      c = switchBits(c, 0, 1); /* d = switchBits(d, 4, 5); e = switchBits(e, 5, 6); */
      c = switchBits(c, 4, 7);
      c = switchBits(c, 5, 6);
      c = switchBits(c, 0, 3); /* c = switchBits(c,14,3); c = switchBits(c, 2, 0); */
      c = switchBits(c, 1, 2);
      passChar[b] = c;
    }
    return new String(passChar);
  }
  public boolean showPassword() {
    char[] passChar = {
      0xF4, 0xC0, 0x97, 0xF0, 0x77, 0x97, 0xC0, 0xE4, 
      0xF0, 0x77, 0xA4, 0xD0, 0xC5, 0x77, 0xF4, 0x86,
      0xD0, 0xA5, 0x45, 0x96, 0x27, 0xB5, 0x77, 0xD2, 
      0xD0, 0xB4, 0xE1, 0xC1, 0xE0, 0xD0, 0xD0, 0xE0
    };
    String password = unscramble(passChar);
    System.out.println(password);
    return true;
  }
}
~~~

This can be compiled:

~~~
$ javac VaultDoor8_modified.java 
~~~

When run, we enter a trivial guess of the passphrase and the correct passphrase is returned:

~~~
$ java VaultDoor8_modified                                             1 ⚙
Picked up _JAVA_OPTIONS: -Dawt.useSystemAAFontSettings=on -Dswing.aatext=true
Enter vault password: picoCTF{guess}
Access denied!
Password is:
s0m3_m0r3_b1t_sh1fTiNg_91c642112
~~~

This can be checked using the checkPassword Method to validate the returned string:

~~~
$ java VaultDoor8_modified                                             1 ⚙
Picked up _JAVA_OPTIONS: -Dawt.useSystemAAFontSettings=on -Dswing.aatext=true
Enter vault password: picoCTF{s0m3_m0r3_b1t_sh1fTiNg_91c642112}
Access granted.
~~~

The flag is therefore picoCTF{s0m3_m0r3_b1t_sh1fTiNg_91c642112}.

</details>

### Answer

<details>

<summary markdown="span">Flag</summary>

~~~
picoCTF{s0m3_m0r3_b1t_sh1fTiNg_91c642112}
~~~

</details>

---

### [Reverse Engineering](#contents) | [PicoGym](./picogym.md) | [PicoCTF](./picoctf.md) | [Home](./index.md)

---

## asm1

- Author: Sanjay C
- 200 points

### Description

What does asm1(0x8be) return? Submit the flag as a hexadecimal value (starting with '0x'). NOTE: Your submission for this question will NOT be in the normal flag format. Source

### Hints

1. [assembly conditions](https://www.tutorialspoint.com/assembly_programming/assembly_conditions.htm).

### Attachments

<details>

<summary markdown="span">test.S</summary>

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

</details>

### Solutions

<details>

<summary markdown="span">Solution 1</summary>

Reviewing the ASM1 assembly code in test.S we can better understand this challenge.

First, we can see this assembly code is for 32-bit architecture.  The use of EAX and EBP indicate this architecture.  A description of resgisters can be seen in the tables below.

| GP Register       | 8 bit   | 16 bit | 32 bit | 64 bit |
|-------------------|---------|--------|--------|--------|
| Acummulator       | AH / AL | AX     | EAX    | RAX    |
| Base              | BH / BL | BX     | EBX    | RBX    |
| Counter           | CH / CL | CX     | ECX    | RCX    |
| Data              | DH / DL | DX     | EDX    | RDX    |
| Source Index      | SIL     | SI     | ESI    | RSI    |
| Destination Index | DIL     | DI     | EDI    | RDI    |
| Stack Pointer     | SPL     | SP     | ESP    | RSP    |
| Base Pointer      | BPL     | BP     | EBP    | RBP    |
| General Purpose 1 | R8B     | R8W    | R8D    | R8     |
| General Purpose 2 | R9B     | R9W    | R9D    | R9     |
| General Purpose 3 | R10B    | R10W   | R10D   | R10    |
| General Purpose 4 | R11B    | R11W   | R11D   | R11    |
| General Purpose 5 | R12B    | R12W   | R12D   | R12    |
| General Purpose 6 | R13B    | R13W   | R13D   | R13    |
| General Purpose 7 | R14B    | R14W   | R14D   | R14    |
| General Purpose 8 | R15B    | R15W   | R15D   | R15    |

| Pointer Register    | 8 bit   | 16 bit | 32 bit | 64 bit |
|---------------------|---------|--------|--------|--------|
| Instruction Pointer | N/A     | IP     | EIP    | RIP    |

We can see in the asm1 assembly code, references to the 32-bit registers: base pointer (EBP), stack pointer (ESP), Accumulator (EAX).

Now we have a reference for the registers, we should understand the instructions in the assembly code.

| Instruction | Description                                                                             |
|-------------|-----------------------------------------------------------------------------------------|
| push        | push a value to the stack                                                               |
| mov         | mov data into registers (read and write to memory)                                      |
| cmp         | comparison operator. Compares two values and amends ZF and CF                           |
| jg          | conditional jump, performs jump if cmp(a,b) returns a>b                                 |
| jne         | conditional jump, performs jump if cmp(a,b) returns a!=b                                |
| add         | performs addition of two registers. add(a,b) sets a = a+b                               |
| sub         | performs subtraction of two registers. sub(a,b) sets a = a-b                            |
| pop         | restores the top of the stack into a reg. pop x sets x to value at the top of the stack |
| ret         | pops the return address off the stack and returns control to that location              |

We now have enough information to analyse the asm1 assembly code:

The first two lines of the asm1 assembly are:

~~~nasm
<+0>:	push   ebp
<+1>:	mov    ebp,esp
~~~

This is establishing a new stack frame. push ebp preserves the current frame pointer (for stack walking) and mov ebp,esp creates a new frame pointer at the top of the current stack.

EBP is now the reference address for the stack.  The stack can be visualised as shown below.

| Address    | Value   |
|------------|---------|
| EBP + 0x08 | input   |
| EBP + 0x04 | ret     |
| EBP        | Old EBP |

EBP+0x8 refers to the user input byte, for this challenge, EBP+0x8 is 0x8BE.  The next line is a comparator:

~~~nasm
<+3>:	cmp    DWORD PTR [ebp+0x8],0x71c
<+10>:	jg     0x512 <asm1+37>
~~~

This compares the value in memory address EBP+0x8 using the dword pointer and the value 0x71C.  We know the contents of the memory address EBP+0x8 is 0x8BE.  The comparator is thus comparing 0x8BE and 0x71C.  This instruction will affect the Zero Flag (ZF) and Carry Flag (CF) as described below.

| CMP(A,B)  | ZF | CF |
|-----------|----|----|
| A == B    | 1  | 0  |
| A < B     | 0  | 1  |
| A > B     | 0  | 0  |

These flags are used to inform sequential jump operations.  The next line, JG, is a conditional jump that is completed if ZF=CF=0, (e.g. A>B).

We can now see, CMP(0x8BE,0x71C) will return ZF = 0, CF = 0.  We thus perform the jump to memory location 0x512, described at line 37 of the asm1 assembly code.

If we were to enter a value, less than 0x71C, we would continue to the next line:

~~~nasm
<+12>:	cmp    DWORD PTR [ebp+0x8],0x6cf
<+19>:	jne    0x50a <asm1+29>
~~~

Here, we have another comparator, we compare the input with 0x6CF.  The subsequent line is a "jump if not equal".  If we do not input 0x6Cf to the program, we will jump to address 0x50A.  If, however we were to enter 0x6CF to the program, we would not jump at <+10> and we would not jump at <+19> we would therefore continue to the next line:

~~~nasm
<+21>:	mov    eax,DWORD PTR [ebp+0x8]
<+24>:	add    eax,0x3
<+27>:	jmp    0x529 <asm1+60>
~~~

This moves the value of the memory at EBP+0x8 (user input) to the accumulator, adds 0x3 to this and jumps to memory address 0x529 (in this case, this is the pop call).

If we were to enter a value that is not equal to 0x6CF and is less than 0x71C, we would jump to the next lines in ASM1:

~~~nasm
<+29>:	mov    eax,DWORD PTR [ebp+0x8]
<+32>:	sub    eax,0x3
<+35>:	jmp    0x529 <asm1+60>
~~~

This copies the input into the accumulator and subtracts 3 before jumpting to the pop call.

If we were to enter a value that is greater than 0x71C, we would jump from <+10> to <+37>:

~~~nasm
<+37>:	cmp    DWORD PTR [ebp+0x8],0x8be
<+44>:	jne    0x523 <asm1+54>
~~~

As before, this compares the user input to 0x8BE and if not equal, will jump to address 0x523.  If it is equal, it will continue to the next line:

~~~nasm
<+46>:	mov    eax,DWORD PTR [ebp+0x8]
<+49>:	sub    eax,0x3
<+52>:	jmp    0x529 <asm1+60>
~~~

If we arrive at <+46> the input is copied into the accumulator and 3 is subtracted from it before we jump to the pop call.

If our input is greater than 0x71C, and is not equal to 0x8be, we will jump to <+54>:

~~~nasm
<+54>:	mov    eax,DWORD PTR [ebp+0x8]
<+57>:	add    eax,0x3
~~~

This copies the input to the accumulator and adds 3 before we continue to <+60>.

The end of the asm1 assembly code:

~~~nasm
<+60>:	pop    ebp
<+61>:	ret
~~~

The first line restores the top of the stack into the register (return to the previous EBP address).  The second line returns the value of EAX.

We can rewrite this ASM1 assembly code in pseudo code:

~~~
ASM1(input):
  if input == 1743:
    return input+3
  else if input < 1820:
    return input -3
  else if input == 2238:
    return input -3
  else
    return input + 3
~~~

The input for this challenge, 2238 will return 2235, or in hexadecimal: 0x8bb.

As described in the hints, this is the flag without picoCTF{}.

</details>

<details>

<summary markdown="span">Solution 2</summary>

This challenge can be solved without reviewing, or understanding, the assembly code.  We can write a c program to pass the relevant variables to the assembly code program and print the output.

Using a 32-bit virtual machine, we can build and run executables in a native 32-bit architecture environment.  All that is required to compile in a 32-bit environment is the gcc compiler and dependent libraries.  These can be installed using:

~~~
$ apt-get install build-essential
~~~

This installs the 32-bit gcc compiler.

We can now transcribe the asm into c using inline assembly code following the [extended asm](https://gcc.gnu.org/onlinedocs/gcc/Extended-Asm.html) format.

~~~c
#include <stdio.h>
#include <stdlib.h>

int asm1(int in ) {
  int val;

  asm(
    	// "push   ebp;"
    	// "mov    ebp,esp;"
    	"cmp    DWORD PTR [ebp+0x8],0x71c;"
    	"jg    _asm1_37;"
    	"cmp    DWORD PTR [ebp+0x8],0x6cf;"
    	"jne  _asm1_29;"
    	"mov    eax,DWORD PTR [ebp+0x8];"
    	"add    eax,0x3;"
    	"jmp  _asm1_60;"
    "_asm1_29:"
    	"mov    eax,DWORD PTR [ebp+0x8];"
    	"sub    eax,0x3;"
    	"jmp  _asm1_60;"
    "_asm1_37:"
    	"cmp    DWORD PTR [ebp+0x8],0x8be;"
    	"jne    _asm1_54;"
    	"mov    eax,DWORD PTR [ebp+0x8];"
    	"sub    eax,0x3;"
    	"jmp  _asm1_60;"
    "_asm1_54:"
    	"mov    eax,DWORD PTR [ebp+0x8];"
    	"add    eax,0x3;"
    "_asm1_60:"
    	// "pop    ebp;"
    	// "ret;"
    	: "=r"(val)
    	: "b"( in )
  );

  return val;
}

int main(void) {
  int input;
  printf("asm1 executable.\n");
  printf("Enter an input value for asm1 in hexadecimal format without 0x :");
  scanf("%x", & input);
  printf("\nYou entered: 0x%x\n", input);
  printf("----------\n");
  printf("running asm1(0x%x).\n", input);
  int output = asm1(input);
  printf("complete.\n");
  printf("Flag = 0x%x\n", output);
  printf("Goodbye\n");
  printf("----------\n");
  return 0;
}
~~~

This can be compiled using extended flags described below.

| Flag                 | Description                                                                        |
|----------------------|------------------------------------------------------------------------------------|
| -masm=intel          | Sets assembly dialect to intel.                                                    |
| -m32                 | flag for compiling 32 bit executable in 64 bit environment (not required for x86). |
| -Wall                | enables all warnings about constructions from the compiler.                        |
| -Wextra              | enables extra warning flags from compiler.                                         |
| -fno-stack-protector | disables stack protection.                                                         |
| -no-pie              | disables address space layout randomisation.                                       |

The complete compiling command:

~~~
$ gcc -masm=intel -m32 asm1.c -o asm1 -Wall -Wextra -fno-stack-protector -no-pie
~~~

We can now run the executable and enter the input given in the challenge:

~~~
$ ./asm1
asm1 executable.
Enter an input value for asm1 in hexadecimal format without 0x :8be

You entered: 0x8be
----------
running asm1(0x8be).
complete.
Flag = 0x8bb
Goodbye
----------
~~~

This returns the flag 0x8bb.

</details>

### Answer

<details>

<summary markdown="span">Flag</summary>

~~~
0x8bb
~~~

</details>

---

### [Reverse Engineering](#contents) | [PicoGym](./picogym.md) | [PicoCTF](./picoctf.md) | [Home](./index.md)

---

## asm2

- Author: Sanjay C
- 250 points

### Description

What does asm2(0xb,0x2e) return? Submit the flag as a hexadecimal value (starting with '0x'). NOTE: Your submission for this question will NOT be in the normal flag format. Source

### Hints

1. [assembly conditions](https://www.tutorialspoint.com/assembly_programming/assembly_conditions.htm).

### Attachments

<details>

<summary markdown="span">test.S</summary>

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

</details>

### Solutions

<details>

<summary markdown="span">Solution 1</summary>

ASM2 is similar to ASM1.  The initial stack can be seen below.

| Address    | Value   |
|------------|---------|
| EBP + 0x0C | input 2 |
| EBP + 0x08 | input 1 |
| EBP + 0x04 | ret     |
| EBP        | Old EBP |

The ASM2 assembly code first 3 lines allocate additional memory for the program:

~~~nasm
<+0>:	push   ebp
<+1>:	mov    ebp,esp
<+3>:	sub    esp,0x10
~~~

Line <+3> allocates an additional 4 memory location (4x4-Byte = 0x10), our stack now looks:

| Address    | Value   |
|------------|---------|
| EBP + 0x0C | input 2 |
| EBP + 0x08 | input 1 |
| EBP + 0x04 | ret     |
| EBP        | Old EBP |
| EBP - 0x04 | 0x00    |
| EBP - 0x08 | 0x00    |
| EBP - 0x0c | 0x00    |
| EBP - 0x10 | 0x00    |

The next line assigns the accumulator register the value held in address ebp+0xc (input 2).  This is subsequently copied into the memory address EBP-0x4:

~~~nasm
<+6>:	mov    eax,DWORD PTR [ebp+0xc]
<+9>:	mov    DWORD PTR [ebp-0x4],eax
~~~

Our stack now looks like:

| Address    | Value   |
|------------|---------|
| EBP + 0x0C | input 2 |
| EBP + 0x08 | input 1 |
| EBP + 0x04 | ret     |
| EBP        | Old EBP |
| EBP - 0x04 | input 2 |
| EBP - 0x08 | 0x00    |
| EBP - 0x0c | 0x00    |
| EBP - 0x10 | 0x00    |

The next two lines copy input 1 from EBP + 0x08 to EBP - 0x08:

~~~nasm
<+12>:	mov    eax,DWORD PTR [ebp+0x8]
<+15>:	mov    DWORD PTR [ebp-0x8],eax
~~~

The stack now appears:

| Address    | Value   |
|------------|---------|
| EBP + 0x0C | input 2 |
| EBP + 0x08 | input 1 |
| EBP + 0x04 | ret     |
| EBP        | Old EBP |
| EBP - 0x04 | input 2 |
| EBP - 0x08 | input 1 |
| EBP - 0x0c | 0x00    |
| EBP - 0x10 | 0x00    |

The next 6 lines operate on the stored data.  Line <+18> jumps to the comparator operator at <+28>.  This compares the value at EBP - 0x08 with 0x63f3.  If dword ptr(0x08) is less than 0x63f3, line <+35> jumps to <+20>, otherwise the next line copies the value of the memory at EBP - 0x4 to the accumulator register for return.

~~~nasm
<+18>:	jmp    0x509 <asm2+28>
<+20>:	add    DWORD PTR [ebp-0x4],0x1
<+24>:	sub    DWORD PTR [ebp-0x8],0xffffff80
<+28>:	cmp    DWORD PTR [ebp-0x8],0x63f3
<+35>:	jle    0x501 <asm2+20>
<+37>:	mov    eax,DWORD PTR [ebp-0x4]
~~~

We can now look at the pseudocode for the ASM2 program:

~~~
ASM(input1, input2):
  var0 = input2
  var1 = input1
  while var1 <= 0x63f3:
    var0 = var0 + 1
    var1 = var1 - 0xffffff80
  return var0
~~~



</details>

### Answer

<details>

<summary markdown="span">Flag</summary>

~~~
picoCTF{}
~~~

</details>

---

### [Reverse Engineering](#contents) | [PicoGym](./picogym.md) | [PicoCTF](./picoctf.md) | [Home](./index.md)

---

## asm3

- Author: Sanjay C
- 300 points

### Description

What does asm3(0xba6c5a02,0xd101e3dd,0xbb86a173) return? Submit the flag as a hexadecimal value (starting with '0x'). NOTE: Your submission for this question will NOT be in the normal flag format. Source

### Hints

1. [more(?) registers](https://wiki.skullsecurity.org/index.php?title=Registers).

### Attachments

<details>
<summary markdown="span">test.S</summary>

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

</details>

### Solutions

<details>

<summary markdown="span">Solution 1</summary>

As in previous asm challenges, we can compile the assembly code within c as shown below.

~~~c
#include <stdio.h>
#include <stdlib.h>

int asm3(int in1, int in2, int in3) {
  int val;
  asm(
    // "push   ebp;"
    // "mov    ebp,esp;"
    "xor    eax,eax;"
    "mov    ah,BYTE PTR [ebp+0xb];"
    "shl    ax,0x10;"
    "sub    al,BYTE PTR [ebp+0xd];"
    "add    ah,BYTE PTR [ebp+0xc];"
    "xor    ax,WORD PTR [ebp+0x12];"
    "nop;"
    //"pop    ebp;"
    : "=r"(val)
    : "b"(in1), "c"(in2), "d"(in3)
  );
  return val;
}

int main(void) {
  int input1, input2, input3;
  printf("asm3 executable.\n");
  printf("Enter an input1 value for asm3 in hexadecimal format without 0x :");
  scanf("%x", & input1);
  printf("\nYou entered: 0x%x\n", input1);
  printf("Enter an input2 value for asm3 in hexadecimal format without 0x :");
  scanf("%x", & input2);
  printf("\nYou entered: 0x%x\n", input2);
  printf("Enter an input3 value for asm3 in hexadecimal format without 0x :");
  scanf("%x", & input3);
  printf("\nYou entered: 0x%x\n", input3);
  printf("----------\n");
  printf("running asm3(0x%x,0x%x,0x%x).\n", input1, input2, input3);
  int output = asm3(input1, input2, input3);
  printf("complete.\n");
  printf("Flag = 0x%x\n", output);
  printf("Goodbye\n");
  printf("----------\n");
  return 0;
}
~~~

This can be compiled as shown below:

~~~
$ gcc -masm=intel -m32 asm3.c -o asm3 -Wall -Wextra -fno-stack-protector -no-pie
~~~

When executed, we can enter the three inputs separately to generate the flag:

~~~
$ ./asm3
asm3 executable.
Enter an input1 value for asm3 in hexadecimal format without 0x :ba6c5a02

You entered: 0xba6c5a02
Enter an input2 value for asm3 in hexadecimal format without 0x :d101e3dd

You entered: 0xd101e3dd
Enter an input3 value for asm3 in hexadecimal format without 0x :bb86a173

You entered: 0xbb86a173
----------
running asm3(0xba6c5a02,0xd101e3dd,0xbb86a173).
complete.
Flag = 0x669b
Goodbye
----------
~~~

This returns the flag 0x669b.

</details>

### Answer

<details>

<summary markdown="span">Flag</summary>

~~~
0x669b
~~~

</details>

---

### [Reverse Engineering](#contents) | [PicoGym](./picogym.md) | [PicoCTF](./picoctf.md) | [Home](./index.md)

---

## asm4

- Author: Sanjay C
- 400 points

### Description

What will asm4("picoCTF_f97bb") return? Submit the flag as a hexadecimal value (starting with '0x'). NOTE: Your submission for this question will NOT be in the normal flag format. Source

### Hints

1. Treat the Array argument as a pointer

### Attachments

<details>

<summary markdown="span">test.S</summary>

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

### [Reverse Engineering](#contents) | [PicoGym](./picogym.md) | [PicoCTF](./picoctf.md) | [Home](./index.md)

---

## OTP Implementation

- Author: madStacks
- 300 points

### Description

Yay reversing! Relevant files: otp flag.txt

### Hints

1. [https://sourceware.org/gdb/onlinedocs/gdb/Python-API.html](https://sourceware.org/gdb/onlinedocs/gdb/Python-API.html).
2. I think [GDB Python](https://wiki.python.org/moin/DebuggingWithGdb) is very useful, you can solve this problem without it, but can you solve future problems (hint hint)?
3. Also test your skills by solving this with [ANGR](https://github.com/angr/angr)!

### Attachments

[otp (binary file)](./resources/picoctf/picogym/attachments/reverse-engineering/otp-implementation)

<details>

<summary markdown="span">flag.txt</summary>

~~~
18a07fbdbcd1af759895328ec4d82d2b411dc7876c34a0ab61eda8f2efa5bb0f198a3aa0ac47ff9a0cf3d913d3138678ce4b
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

### [Reverse Engineering](#contents) | [PicoGym](./picogym.md) | [PicoCTF](./picoctf.md) | [Home](./index.md)

---

## droids0

- Author: Jason
- 300 points

### Description

Where do droid logs go. Check out this file.

### Hints

1. Try using an emulator or device
2. [https://developer.android.com/studio](https://developer.android.com/studio).

### Attachments

[zero.apk](./resources/picoctf/picogym/attachments/reverse-engineering/droids0/zero.apk)

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

### [Reverse Engineering](#contents) | [PicoGym](./picogym.md) | [PicoCTF](./picoctf.md) | [Home](./index.md)

---

## droids1

- Author: Jason
- 350 points

### Description

Find the pass, get the flag. Check out this file.

### Hints

1. Try using [apktool](https://ibotpeaches.github.io/Apktool/) and an [emulator](https://developer.android.com/studio).
2. [https://ibotpeaches.github.io/Apktool/](https://ibotpeaches.github.io/Apktool/).
3. [https://developer.android.com/studio](https://developer.android.com/studio).

### Attachments

[one.apk](./resources/picoctf/picogym/attachments/reverse-engineering/droids1/one.apk)

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

### [Reverse Engineering](#contents) | [PicoGym](./picogym.md) | [PicoCTF](./picoctf.md) | [Home](./index.md)

---

## droids2

- Author: Jason
- 400 points

### Description

Find the pass, get the flag. Check out this file.

### Hints

1. Try using [apktool](https://ibotpeaches.github.io/Apktool/) and an [emulator](https://developer.android.com/studio).
2. [https://ibotpeaches.github.io/Apktool/](https://ibotpeaches.github.io/Apktool/).
3. [https://developer.android.com/studio](https://developer.android.com/studio).

### Attachments

[two.apk](./resources/picoctf/picogym/attachments/reverse-engineering/droids2/two.apk)

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

### [Reverse Engineering](#contents) | [PicoGym](./picogym.md) | [PicoCTF](./picoctf.md) | [Home](./index.md)

---

## droids3

- Author: Jason
- 450 points

### Description

Find the pass, get the flag. Check out this file.

### Hints

1. Try using [apktool](https://ibotpeaches.github.io/Apktool/) and an [emulator](https://developer.android.com/studio).
2. [https://ibotpeaches.github.io/Apktool/](https://ibotpeaches.github.io/Apktool/).
3. [https://developer.android.com/studio](https://developer.android.com/studio).

### Attachments

[three.apk](./resources/picoctf/picogym/attachments/reverse-engineering/droids3/three.apk)

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

### [Reverse Engineering](#contents) | [PicoGym](./picogym.md) | [PicoCTF](./picoctf.md) | [Home](./index.md)

---

## droids4

- Author: Jason
- 500 points

### Description

Reverse the pass, patch the file, get the flag. Check out this file.

### Hints

None

### Attachments

[four.apk](./resources/picoctf/picogym/attachments/reverse-engineering/droids4/four.apk)

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

### [Reverse Engineering](#contents) | [PicoGym](./picogym.md) | [PicoCTF](./picoctf.md) | [Home](./index.md)

---

## reverse-cipher

- Author: Danny Tunitis
- 300 points

### Description

We have recovered a binary and a text file. Can you reverse the flag.
### Hints

1. [objdump](https://en.wikipedia.org/wiki/Objdump) and [Gihdra](https://ghidra-sre.org/) are some tools that could assist with this.

### Attachments

[rev](./resources/picoctf/picogym/attachments/reverse-engineering/reverse_cipher/rev)

<details>

<summary markdown="span">"rev_this" text file:</summary>

~~~
picoCTF{w1{1wq8/7376j.:}
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

### [Reverse Engineering](#contents) | [PicoGym](./picogym.md) | [PicoCTF](./picoctf.md) | [Home](./index.md)

---

## Need For Speed

- Author: Alexander Bushkin
- 400 points

### Description

The name of the game is speed. Are you quick enough to solve this problem and keep it above 50 mph? need-for-speed.

### Hints

1. What is the final key?

### Links

1. [https://www.youtube.com/watch?v=8piqd2BWeGI](https://www.youtube.com/watch?v=8piqd2BWeGI).

### Attachments

[need-for-speed](./resources/picoctf/picogym/attachments/reverse-engineering/need-for-speed/need-for-speed)

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

### [Reverse Engineering](#contents) | [PicoGym](./picogym.md) | [PicoCTF](./picoctf.md) | [Home](./index.md)

---

## B1ll-Gat35

- Author: Alex Bushkin
- 400 points

### Description

Can you reverse this Windows Binary?

### Hints

1. Microsoft provides [windows virtual machines](https://developer.microsoft.com/en-us/windows/downloads/virtual-machines).
2. [Ollydbg](http://www.ollydbg.de/) may be helpful.
3. Flag format: PICOCTF{XXXX}.

### Attachments

[win-exec-1.exe](./resources/picoctf/picogym/attachments/reverse-engineering/b1ll_gat35/win-exec-1.exe)

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

### [Reverse Engineering](#contents) | [PicoGym](./picogym.md) | [PicoCTF](./picoctf.md) | [Home](./index.md)

---

## Forky

- Author: Samuel
- 500 points

### Description

In this program, identify the last integer value that is passed as parameter to the function doNothing().

### Hints

1. What happens when you fork? The flag is picoCTF{IntegerYouFound}. For example, if you found that the last integer passed was 1234, the flag would be picoCTF{1234}

### Attachments

[vuln](./resources/picoctf/picogym/attachments/reverse-engineering/forky/vuln)

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

### [Reverse Engineering](#contents) | [PicoGym](./picogym.md) | [PicoCTF](./picoctf.md) | [Home](./index.md)

---

## [djm89uk.github.io](https://djm89uk.github.io)
