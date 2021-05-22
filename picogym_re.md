# [PicoCTF](./picoctf.md) PicoGym Reverse Engineering

Reverse engineering entails taking a software system and analyzing it to trace it back to the original design and implementation information. It is used to fix certain bugs in software as well as to enhance product features in both hardware and software.

## Contents

- [vault-door-training (2019)](#vault-door-training)
- [vault-door-1 (2019)](#vault-door-1)
- [vault-door-3 (2019)](#vault-door-3)
- [vault-door-4 (2019)](#vault-door-4)
- [vault-door-5 (2019)](#vault-door-5)
- [vault-door-6 (2019)](#vault-door-6)
- [vault-door-7 (2019)](#vault-door-7)
- [vault-door-8 (2019)](#vault-door-8)
- [asm1 (2019)](#asm1)
- [asm2 (2019)](#asm2)
- [asm3 (2019)](#asm3)
- [asm4 (2019)](#asm4)
- [droids0 (2019)](#droids0)
- [droids1 (2019)](#droids1)
- [droids2 (2019)](#droids2)
- [droids3 (2019)](#droids3)
- [droids4 (2019)](#droids4)
- [revese_cipher (2019)](#reverse-cipher)
- [Need For Speed (2019)](#need-for-speed)
- [B1ll_Gat35 (2019)](#b1ll-gat35)
- [Forky (2019)](#forky)
- [OTP Implementation (2020)](#otp-implementation)
- [Transformation (2021)](#transformation)
- [Keygenme-py (2021)](#keygneme-py)
- [crackme-py (2021)](#crackme-py)
- [ARMssembly 0 (2021)](#armssembly-0)
- [speeds and feeds (2021)](#speeds-and-feeds)
- [Shop (2021)](#shop)
- [ARMssembly 1 (2021)](#armssembly-1)
- [ARMssembly 2 (2021)](#armssembly-2)
- [Hurry up! Wait! (2021)](#hurry-up-wait)
- [gogo (2021)](#gogo)
- [ARMssembly 3 (2021)](#armssembly-3)
- [Let's get dynamic (2021)](#lets-get-dynamic)
- [Easy as GDB (2021)](#easy-as-gdb)
- [ARMssembly 4 (2021)](#armssembly-4)
- [Powershelly (2021)](#powershelly)
- [Rolling My Own (2021)](#rolling-my-own)
- [Checkpass (2021)](#checkpass)
- [not crypto (2021)](#not-crypto)
- [breadth (2021)](#breadth)
- [riscy business (2021)](#riscy-business)
- [MATRIX (2021)](#matrix)

---

### [Reverse Engineering](#contents) | [PicoCTF](./picoctf.md) | [Home](./index.md)

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

### [Reverse Engineering](#contents) | [PicoCTF](./picoctf.md) | [Home](./index.md)

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

### [Reverse Engineering](#contents) | [PicoCTF](./picoctf.md) | [Home](./index.md)

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

### [Reverse Engineering](#contents) | [PicoCTF](./picoctf.md) | [Home](./index.md)

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

### [Reverse Engineering](#contents) | [PicoCTF](./picoctf.md) | [Home](./index.md)

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

This can be compiled:

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

### [Reverse Engineering](#contents) | [PicoCTF](./picoctf.md) | [Home](./index.md)

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

### [Reverse Engineering](#contents) | [PicoCTF](./picoctf.md) | [Home](./index.md)

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

### [Reverse Engineering](#contents) | [PicoCTF](./picoctf.md) | [Home](./index.md)

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

### [Reverse Engineering](#contents) | [PicoCTF](./picoctf.md) | [Home](./index.md)

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

int asm1(int input ) {
  int output;
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
    		: "=r"( output )
    		: "b"( input )
  );

  return output;
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

### [Reverse Engineering](#contents) | [PicoCTF](./picoctf.md) | [Home](./index.md)

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

### [Reverse Engineering](#contents) | [PicoCTF](./picoctf.md) | [Home](./index.md)

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

int asm3(int input1, int input2, int input3) {
  int output;
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
    : "=r"( output )
    : "b"( input1 ), "c"( input2 ), "d"( input3 )
  );
  return output;
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

### [Reverse Engineering](#contents) | [PicoCTF](./picoctf.md) | [Home](./index.md)

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

As with the previous ASM challenges, we can compile a C program to execute the assembly code:

~~~c
#include <stdio.h>
#include <stdlib.h>

int asm4(char * input ) {
  int output;
  asm(
    	// "push   ebp;"
    	// "mov    ebp,esp;"
    	"push   ebx;"
    	"sub    esp,0x10;"
    	"mov    DWORD PTR [ebp-0x10],0x27a;"
    	"mov    DWORD PTR [ebp-0xc],0x0;"
    	"jmp    _asm4_27;"
    "_asm4_23:"
    	"add    DWORD PTR [ebp-0xc],0x1;"
    "_asm4_27:"
    	"mov    edx,DWORD PTR [ebp-0xc];"
    	"mov    eax,DWORD PTR [ebp+0x8];"
    	"add    eax,edx;"
    	"movzx  eax,BYTE PTR [eax];"
    	"test   al,al;"
    	"jne   _asm4_23;"
    	"mov    DWORD PTR [ebp-0x8],0x1;"
    	"jmp   _asm4_138;"
    "_asm4_51:"
    	"mov    edx,DWORD PTR [ebp-0x8];"
    	"mov    eax,DWORD PTR [ebp+0x8];"
    	"add    eax,edx;"
    	"movzx  eax,BYTE PTR [eax];"
    	"movsx  edx,al;"
    	"mov    eax,DWORD PTR [ebp-0x8];"
    	"lea    ecx,[eax-0x1];"
    	"mov    eax,DWORD PTR [ebp+0x8];"
    	"add    eax,ecx;"
    	"movzx  eax,BYTE PTR [eax];"
    	"movsx  eax,al;"
    	"sub    edx,eax;"
    	"mov    eax,edx;"
    	"mov    edx,eax;"
    	"mov    eax,DWORD PTR [ebp-0x10];"
    	"lea    ebx,[edx+eax*1];"
    	"mov    eax,DWORD PTR [ebp-0x8];"
    	"lea    edx,[eax+0x1];"
    	"mov    eax,DWORD PTR [ebp+0x8];"
    	"add    eax,edx;"
    	"movzx  eax,BYTE PTR [eax];"
    	"movsx  edx,al;"
    	"mov    ecx,DWORD PTR [ebp-0x8];"
    	"mov    eax,DWORD PTR [ebp+0x8];"
    	"add    eax,ecx;"
    	"movzx  eax,BYTE PTR [eax];"
    	"movsx  eax,al;"
    	"sub    edx,eax;"
    	"mov    eax,edx;"
    	"add    eax,ebx;"
    	"mov    DWORD PTR [ebp-0x10],eax;"
    	"add    DWORD PTR [ebp-0x8],0x1;"
    "_asm4_138:"
    	"mov    eax,DWORD PTR [ebp-0xc];"
    	"sub    eax,0x1;"
    	"cmp    DWORD PTR [ebp-0x8],eax;"
    	"jl    _asm4_51;"
    	"mov    eax,DWORD PTR [ebp-0x10];"
    	"add    esp,0x10;"
    	"pop    ebx;"
    	// "pop    ebp;"
    	// "ret;"
    		: "=r"( output )
		: "b"( input )
  );
  return output;
}

int main(void) {
  char input[20];
  printf("asm4 executable.\n");
  printf("Enter an input value for asm4 as a string :");
  scanf("%s", & input);
  printf("\nYou entered: %s", input);
  printf("----------\n");
  printf("running asm4(\"%s\").\n", input);
  int output = asm4(input);
  printf("complete.\n");
  printf("Flag = 0x%x\n", output);
  printf("Goodbye\n");
  printf("----------\n");
  return 0;
}
~~~

This can be compiled as before:

~~~
$ gcc -masm=intel -m32 asm4.c -o asm4 -Wall -Wextra -fno-stack-protector -no-pie
~~~

When run, we enter the challenge input and the flag is returned:

~~~
$ ./asm4
asm4 executable.
Enter an input value for asm4 as a string :picoCTF_f97bb

You entered: picoCTF_f97bb----------
running asm4("picoCTF_f97bb").
complete.
Flag = 0x265
Goodbye
----------
~~~

The flag is therefore 0x265

</details>

### Answer

<details>

<summary markdown="span">Flag</summary>

~~~
0x265
~~~

</details>

---

### [Reverse Engineering](#contents) | [PicoCTF](./picoctf.md) | [Home](./index.md)

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

We are given an Android Package Kite (APK) titled "zero.apk".  We can extract the files to a directory in Linux:

~~~shell
$ unzip zero.apk -d zero
~~~

In the lib subdirectory, we find folders:

~~~
arm64-v8a
armeabi-v7a
x86
x86_64
~~~

These directories all have the file "libhellojni.so".  We can thus determine that this apk was likely built for arm7, arm8, x86 (intel Atom x86) and x86-64bit architectures.

This can be confirmed by inspecting the lib files:

~~~shell
$ file libhellojni.so      
libhellojni.so: ELF 32-bit LSB shared object, Intel 80386, version 1 (SYSV), dynamically linked, BuildID[sha1]=d0c69f98297e5b6953f09c22bfa382c4a12c60e8, stripped
~~~

Or by reviewing the ELF header:

~~~shell
$ readelf -h libhellojni.so
ELF Header:
  Magic:   7f 45 4c 46 01 01 01 00 00 00 00 00 00 00 00 00 
  Class:                             ELF32
  Data:                              2's complement, little endian
  Version:                           1 (current)
  OS/ABI:                            UNIX - System V
  ABI Version:                       0
  Type:                              DYN (Shared object file)
  Machine:                           Intel 80386
  Version:                           0x1
  Entry point address:               0x0
  Start of program headers:          52 (bytes into file)
  Start of section headers:          12840 (bytes into file)
  Flags:                             0x0
  Size of this header:               52 (bytes)
  Size of program headers:           32 (bytes)
  Number of program headers:         8
  Size of section headers:           40 (bytes)
  Number of section headers:         25
  Section header string table index: 24
~~~

We now know what hardware this apk will run on, we need to find what Software Development Kit (SDK) version of Android the apk is compiled for.

We can use aapt to identify the compatible SDK version:

~~~shell
$ aapt dump badging zero.apk | grep "Version"                                                             1 ⨯
package: name='com.hellocmu.picoctf' versionCode='1' versionName='1.0' compileSdkVersion='29' compileSdkVersionCodename='10'
sdkVersion:'15'
targetSdkVersion:'29'
~~~

We can see the APK is compiled for v29 of the Android SDK (Android 10).

</details>

### Answer

<details>

<summary markdown="span">Flag</summary>

~~~
picoCTF{}
~~~

</details>

---

### [Reverse Engineering](#contents) | [PicoCTF](./picoctf.md) | [Home](./index.md)

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

### [Reverse Engineering](#contents) | [PicoCTF](./picoctf.md) | [Home](./index.md)

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

### [Reverse Engineering](#contents) | [PicoCTF](./picoctf.md) | [Home](./index.md)

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

### [Reverse Engineering](#contents) | [PicoCTF](./picoctf.md) | [Home](./index.md)

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

### [Reverse Engineering](#contents) | [PicoCTF](./picoctf.md) | [Home](./index.md)

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

This challenge provides a binary file, rev, and the output rev_this, generated from an unknown flag.txt input file.

We can import the binary into Ghidra and review the main function:

~~~c
void main(void)
{
  size_t sVar1;
  char local_58 [23];
  char local_41;
  int local_2c;
  FILE *local_28;
  FILE *local_20;
  uint local_14;
  int local_10;
  char local_9;
  
  local_20 = fopen("flag.txt","r");
  local_28 = fopen("rev_this","a");
  if (local_20 == (FILE *)0x0) {
    puts("No flag found, please make sure this is run on the server");
  }
  if (local_28 == (FILE *)0x0) {
    puts("please run this on the server");
  }
  sVar1 = fread(local_58,0x18,1,local_20);
  local_2c = (int)sVar1;
  if ((int)sVar1 < 1) {
                    /* WARNING: Subroutine does not return */
    exit(0);
  }
  local_10 = 0;
  while (local_10 < 8) {
    local_9 = local_58[local_10];
    fputc((int)local_9,local_28);
    local_10 = local_10 + 1;
  }
  local_14 = 8;
  while ((int)local_14 < 0x17) {
    if ((local_14 & 1) == 0) {
      local_9 = local_58[(int)local_14] + '\x05';
    }
    else {
      local_9 = local_58[(int)local_14] + -2;
    }
    fputc((int)local_9,local_28);
    local_14 = local_14 + 1;
  }
  local_9 = local_41;
  fputc((int)local_41,local_28);
  fclose(local_28);
  fclose(local_20);
  return;
}
~~~

Skipping the variable initialisations, we can see two files are opened at the beginning of this program:

~~~c
local_20 = fopen("flag.txt","r");
local_28 = fopen("rev_this","a");
~~~

The first file, flag.txt, is opened in a read-only mode.  This is the file that we do not have access to.  A second file, rev_this is opened in "append" mode, that is to add characters to the file without altering the existing information.

We can rename these variables, in_file and out_file to make the source easier to read and rewrite in pseudo code:

~~~c
in_file   = OpenFile(flag.txt,readonly)
out_file  = OpenFile(rev_this,append);

  if (in_file == (FILE *)0x0) {
    puts("No flag found, please make sure this is run on the server");
  }
  if (out_file == (FILE *)0x0) {
    puts("please run this on the server");
  }
  sVar1 = fread(local_58,0x18,1,in_file);
  local_2c = (int)sVar1;
  if ((int)sVar1 < 1) {
                    /* WARNING: Subroutine does not return */
    exit(0);
  }
  local_10 = 0;
  while (local_10 < 8) {
    local_9 = local_58[local_10];
    fputc((int)local_9,out_file);
    local_10 = local_10 + 1;
  }
  local_14 = 8;
  while ((int)local_14 < 0x17) {
    if ((local_14 & 1) == 0) {
      local_9 = local_58[(int)local_14] + '\x05';
    }
    else {
      local_9 = local_58[(int)local_14] + -2;
    }
    fputc((int)local_9,out_file);
    local_14 = local_14 + 1;
  }
  local_9 = local_41;
  fputc((int)local_41,out_file);
  fclose(out_file);
  fclose(in_file);
  return;
}
~~~

The next functions are print statements for if the required files are not found.  We can remove these to simplify our code.

The contents of flag.txt are then read to a variable, local_58 we can rename flag.  We can ignore the boolean error handling:

~~~c
in_file   = OpenFile(flag.txt,readonly)
out_file  = OpenFile(rev_this,append);

flag 	  = ReadFile(flag.txt, length=24)

  local_10 = 0;
  while (local_10 < 8) {
    local_9 = flag[local_10];
    fputc((int)local_9,out_file);
    local_10 = local_10 + 1;
  }
  local_14 = 8;
  while ((int)local_14 < 0x17) {
    if ((local_14 & 1) == 0) {
      local_9 = flag[(int)local_14] + '\x05';
    }
    else {
      local_9 = flag[(int)local_14] + -2;
    }
    fputc((int)local_9,out_file);
    local_14 = local_14 + 1;
  }
  local_9 = local_41;
  fputc((int)local_41,out_file);
  fclose(out_file);
  fclose(in_file);
  return;
}
~~~

The program now iterates through the first 8 Bytes and appends these to the output file:

~~~c
in_file   = OpenFile(flag.txt,readonly)
out_file  = OpenFile(rev_this,append)

flag 	  = ReadFile(flag.txt, length=24)

i = 0
while (i < 8) {
  buff = flag[i];
  WriteFile(rev_this,buff)
  i += 1


  local_14 = 8;
  while ((int)local_14 < 0x17) {
    if ((local_14 & 1) == 0) {
      local_9 = flag[(int)local_14] + '\x05';
    }
    else {
      local_9 = flag[(int)local_14] + -2;
    }
    fputc((int)local_9,out_file);
    local_14 = local_14 + 1;
  }
  local_9 = local_41;
  fputc((int)local_41,out_file);
  fclose(out_file);
  fclose(in_file);
  return;
}
~~~

The program now iterates through the next 15 Bytes and either adds 5 or subtracts 2 if the index is even or odd respectively:

~~~c
in_file   = OpenFile(flag.txt,readonly)
out_file  = OpenFile(rev_this,append)

flag 	  = ReadFile(flag.txt, length=24)

i = 0
while (i < 8):
  buff = flag[i]
  WriteFile(rev_this,buff)
  i += 1

i = 8
while (i < 23):
  if (i is even):
    buff = flag[i]+5
  else:
    buff = flag[i]-2
  WriteFile(rev_this, buff)
  i += 1

  local_9 = local_41;
  fputc((int)local_41,out_file);
  fclose(out_file);
  fclose(in_file);
  return;
}
~~~

Finally, the program appends variable "local_41" to the rev_this file and closes the files.  We do not have a declaration for local_41, however we can assume this is the "}" character expected at the end of the flag:


~~~c
in_file   = OpenFile(flag.txt,readonly)
out_file  = OpenFile(rev_this,append)

flag 	  = ReadFile(flag.txt, length=24)

i = 0
while (i < 8):
  buff = flag[i]
  AppendFile(rev_this,buff)
  i += 1

i = 8
while (i < 23):
  if (i is even):
    buff = flag[i]+5
  else:
    buff = flag[i]-2
  AppendFile(rev_this, buff)
  i += 1

AppendFile(rev_this,"}")

close(flag.txt)
close(rev_this)
~~~

We can now reverse this program; We have the following rev_this output:

~~~
picoCTF{w1{1wq8/7376j.:}
~~~

The first 8 characters and the last character are unchanged. Then from index 8 to index 22 the ASCII characters can be substituted for ASCII(int - 5) for even indexes and ASCII(int + 2) for odd indexes:

| Index | Character | Decimal | Reversing | Out Dec | Out ASCII |
|-------|-----------|---------|-----------|---------|-----------|
|  8    | w         | 119     | -5        | 114     | r         |
|  9    | 1         |  49     | +2        |  51     | 3         |
| 10    | {         | 123     | -5        | 118     | v         |
| 11    | 1         |  49     | +2        |  51     | 3         |
| 12    | w         | 119     | -5        | 114     | r         |
| 13    | q         | 113     | +2        | 115     | s         |
| 14    | 8         |  56     | -5        |  51     | 3         |
| 15    | /         |  47     | +2        |  49     | 1         |
| 16    | 7         |  55     | -5        |  50     | 2         |
| 17    | 3         |  51     | +2        |  53     | 5         |
| 18    | 7         |  55     | -5        |  50     | 2         |
| 19    | 6         |  54     | +2        |  56     | 8         |
| 20    | j         | 106     | -5        | 101     | e         |
| 21    | .         |  46     | +2        |  48     | 0         |
| 22    | :         |  58     | -5        |  53     | 5         |

~~~
picoCTF{r3v3rs312528e05}
~~~

</details>

### Answer

<details>

<summary markdown="span">Flag</summary>

~~~
picoCTF{r3v3rs312528e05}
~~~

</details>

---

### [Reverse Engineering](#contents) | [PicoCTF](./picoctf.md) | [Home](./index.md)

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

If we run the executable, we can see the program begins generating a key and exits before the key is given:

~~~shell
$ ./need-for-speed 
Keep this thing over 50 mph!
============================

Creating key...
Not fast enough. BOOM!
~~~

We can load the executable into Ghidra and see the main function:

~~~c
undefined8 main(void)

{
  header();
  set_timer();
  get_key();
  print_flag();
  return 0;
}
~~~

This calls 4 subfunctions: header(), set_timer(), get_key() and print_flag().

If we look at header:

~~~c
void header(void)

{
  uint local_c;
  
  puts("Keep this thing over 50 mph!");
  local_c = 0;
  while (local_c < 0x1c) {
    putchar(0x3d);
    local_c = local_c + 1;
  }
  puts("\n");
  return;
}
~~~

We can see this provides the initial print function for the program. The second function, set_timer():

~~~c
void set_timer(void)

{
  __sighandler_t p_Var1;
  
  p_Var1 = __sysv_signal(0xe,alarm_handler);
  if (p_Var1 == (__sighandler_t)0xffffffffffffffff) {
    puts("\n\nSomething bad happened here. ");
                    /* WARNING: Subroutine does not return */
    exit(0);
  }
  alarm(1);
  return;
}
~~~

This calls the function, alarm_handler:

~~~c
void alarm_handler(void)

{
  puts("Not fast enough. BOOM!");
                    /* WARNING: Subroutine does not return */
  exit(0);
}
~~~

Which exits the program.

We need to find a way to avoid this function.  We can load the executable into the [GNU debugger](https://www.gnu.org/software/gdb/):

~~~shell
$ gdb -f need-for-speed
~~~

In the debugger, we can run the program as before:

~~~shell
(gdb) run
Starting program: /home/djm89uk/Downloads/need-for-speed 
Keep this thing over 50 mph!
============================

Creating key...
Not fast enough. BOOM!
[Inferior 1 (process 158598) exited normally]
~~~

We can put a break into the main function and rerun the program:

~~~shell
(gdb) br main
Breakpoint 1 at 0x55555540091e
(gdb) run
Starting program: /home/djm89uk/Downloads/need-for-speed 

Breakpoint 1, 0x000055555540091e in main ()
~~~

Lets call the subfunction and skip the timer function.  Calling the header first, we get the expected output:

~~~shell
(gdb) call (void) header()
Keep this thing over 50 mph!
============================
~~~

We can now run the get_key() function, skipping the timer:

~~~shell
(gdb) call (void) get_key()
Creating key...
Finished
~~~

We should now be able to retrieve the flag by calling the print_flag() function:

~~~shell
(gdb) call (void) print_flag()
Printing flag:
PICOCTF{Good job keeping bus #190ca38b speeding along!}
~~~

This gives us the flag PICOCTF{Good job keeping bus #190ca38b speeding along!}

</details>

### Answer

<details>

<summary markdown="span">Flag</summary>

~~~
PICOCTF{Good job keeping bus #190ca38b speeding along!}
~~~

</details>

---

### [Reverse Engineering](#contents) | [PicoCTF](./picoctf.md) | [Home](./index.md)

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

### [Reverse Engineering](#contents) | [PicoCTF](./picoctf.md) | [Home](./index.md)

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

This challenge implements multiprocessing using the [fork](https://man7.org/linux/man-pages/man2/fork.2.html) system call.

We can import the binary vuln file into Ghidra to decompile the source.  This gives us a main function:

~~~c
undefined4 main(undefined1 param_1)

{
  int *piVar1;
  
  piVar1 = (int *)mmap((void *)0x0,4,3,0x21,-1,0);
  *piVar1 = 1000000000;
  fork();
  fork();
  fork();
  fork();
  *piVar1 = *piVar1 + 0x499602d2;
  doNothing(*piVar1);
  return 0;
}
~~~

With a custom subfunction, "doNothing":

~~~c
void doNothing(undefined4 param_1)

{
  return;
}
~~~

This program can be rewritten for compiling using the c libraries [stdio.h](https://man7.org/linux/man-pages/man3/stdio.3.html), [sys/mman.h](https://man7.org/linux/man-pages/man0/sys_mman.h.0p.html), [sys/types.h](http://manpages.ubuntu.com/manpages/precise/en/man7/sys_types.h.7posix.html) and [unistd.h](https://man7.org/linux/man-pages/man0/unistd.h.0p.html).  Another useful library is [sys/wait.h](https://manpages.ubuntu.com/manpages/precise/man7/wait.h.7posix.html) that provides the wait and waitpid functions:

~~~c
#include <stdio.h>
#include <sys/mman.h>
#include <sys/types.h> 
#include <unistd.h> 
#include <sys/wait.h>

void doNothing(int32_t param_1);

int32_t main(void)
{
  int32_t *piVar1;
  piVar1 = (int32_t *)mmap((void *)0x0,4,3,0x21,-1,0);
  *piVar1 = 1000000000;
  fork();
  fork();
  fork();
  fork();
  *piVar1 = *piVar1 + 0x499602d2;
  doNothing(*piVar1);
  return 0;
}

void doNothing(int32_t param_1)
{
    return;
}
~~~

This can be compiled and executed with gcc.  We can ass a printf statement at the end of the main function block to see what is returned:

~~~c
#include <stdio.h>
#include <sys/mman.h>
#include <sys/types.h> 
#include <unistd.h> 
#include <sys/wait.h>

void doNothing(int32_t param_1);

int32_t main(void)
{
  int32_t *piVar1;
  piVar1 = (int32_t *)mmap((void *)0x0,4,3,0x21,-1,0);
  *piVar1 = 1000000000;
  fork();
  fork();
  fork();
  fork();
  *piVar1 = *piVar1 + 0x499602d2;
  doNothing(*piVar1);
  
  printf("piVar1 = %d \n",*piVar1);
  
  return 0;
}

void doNothing(int32_t param_1)
{
    return;
}
~~~

Compiling and running this executable results in various returns that are not repeatable.  This is most likely caused by the alive subprocesses returning values from their threads.  We can run this code multiple times and eventually can identify 16 unique outputs that are printed in repeatable sequences.

~~~
piVar1 = -2060399406                                                                
piVar1 = -825831516                                                                 
piVar1 = 408736374                                                                  
piVar1 = 1643304264                                                                 
piVar1 = -1417095142                                                                
piVar1 = -182527252                                                                 
piVar1 = 1052040638                                                                 
piVar1 = -2008358768                                                                
piVar1 = -773790878 
piVar1 = 460777012                                                                  
piVar1 = 1695344902                                                                 
piVar1 = -1365054504                                                                
piVar1 = -130486614                                                                 
piVar1 = 1104081276                                                                 
piVar1 = -1956318130
piVar1 = -721750240
~~~

One of these is the correct (and final) value.  To understand this better, we can review the fork() command.  Each fork() call creates 2 child processes.  The first fork will generate two further forks etc.  When no child process dies, we should see 2x2x2x2 (4xfork() calls) = 16 child processes.  The executable does not always maintain these child processes and we do not always get all 16 responses.  We can try to close and wait for the child processes to end using waitpid and sleep functions:

~~~c
#include <stdio.h>
#include <sys/mman.h>
#include <sys/types.h> 
#include <unistd.h> 
#include <sys/wait.h>

int32_t main(void)
{
  int32_t *piVar1;
  pid_t parent = getpid();
  piVar1 = (int32_t *)mmap((void *)0x0,4,3,0x21,-1,0);
  *piVar1 = 1000000000;
  fork();
  fork();
  fork();
  fork();
  *piVar1 = *piVar1 + 0x499602d2;
  pid_t current = getpid();
  if(current != parent){
    int status;
    waitpid(current,&status,0);
    sleep(1);
  }
  sleep(1);
  printf("piVar1 = %d\n",*piVar1);
  return 0;
}
~~~

This provides a repeatable and exact return:

~~~
piVar1 = -721750240 
~~~

Giving our flag picoCTF{-721750240}.

</details>

### Answer

<details>

<summary markdown="span">Flag</summary>

~~~
picoCTF{-721750240}
~~~

</details>

---

### [Reverse Engineering](#contents) | [PicoCTF](./picoctf.md) | [Home](./index.md)

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

We can decompile the OTP binary in Ghidra.  The main function provides:

~~~c
undefined8 main(int param_1,undefined8 *param_2)

{
  char cVar1;
  byte bVar2;
  int iVar3;
  undefined8 uVar4;
  long in_FS_OFFSET;
  int local_f0;
  int local_ec;
  char local_e8 [100];
  undefined local_84;
  char local_78 [104];


long local_10;
  
  local_10 = *(long *)(in_FS_OFFSET + 0x28);
  if (param_1 < 2) {
    printf("USAGE: %s [KEY]\n",*param_2);
    uVar4 = 1;
  }
  else {
    strncpy(local_e8,(char *)param_2[1],100);
    local_84 = 0;
    local_f0 = 0;
    while( true ) {
      uVar4 = valid_char(local_e8[local_f0]);
      if ((int)uVar4 == 0) break;
      if (local_f0 == 0) {
        cVar1 = jumble(local_e8[0]);
        bVar2 = (byte)(cVar1 >> 7) >> 4;
        local_78[0] = (cVar1 + bVar2 & 0xf) - bVar2;
      }
      else {
        cVar1 = jumble(local_e8[local_f0]);
        bVar2 = (byte)((int)cVar1 + (int)local_78[local_f0 + -1] >> 0x37);
        local_78[local_f0] =
             ((char)((int)cVar1 + (int)local_78[local_f0 + -1]) + (bVar2 >> 4) & 0xf) - (bVar2 >> 4)
        ;
      }
      local_f0 = local_f0 + 1;
    }
    local_ec = 0;
    while (local_ec < local_f0) {
      local_78[local_ec] = local_78[local_ec] + 'a';
      local_ec = local_ec + 1;
    }
    if (local_f0 == 100) {
      iVar3 = strncmp(local_78,
                      "mngjlepdcbcmjmmjipmmegfkjbicaemoemkkpjgnhgomlknmoepmfbcoffikhplmadmganmlojndmfahbhaancamdhfdkiancdjf"
                      ,100);
      if (iVar3 == 0) {
        puts("You got the key, congrats! Now xor it with the flag!");
        uVar4 = 0;
        goto LAB_001009ea;
      }
    }
    puts("Invalid key!");
    uVar4 = 1;
  }
LAB_001009ea:
  if (local_10 != *(long *)(in_FS_OFFSET + 0x28)) {
                    /* WARNING: Subroutine does not return */
    __stack_chk_fail();
  }
  return uVar4;
}
~~~

The main function takes two inputs: "param_1" and "param_2" these are decompiled names for argc (argument count) and argv (argument vector) the [command-line arguments](https://ece.uwaterloo.ca/~dwharder/icsrts/C/05/) for c programs.

| argc | Argument Count  | Integer for number of parameters + executable call passed to the program |
| argv | Argument Vector | Character array vector pointer (string pointer) for parameters and executable passed to program. |

argc is always greater than 0 and provides a count of the number of inputs. For example, in this program we will run it using a command similar to:

~~~shell
$ ./otp input_string
~~~

The argc in this call will be 2 and the argument vector will be argv[0] = otp, argv[1] = input_string.

In the main program, an IF statement is used to check the minimum number of inputs is included in the program call:

~~~c
  if (param_1 < 2) {
    printf("USAGE: %s [KEY]\n",*param_2);
    ret_val = 1;
  }
~~~

This will pass value 1 to the return statement if argc is less than 2 (no additional input is given to the program call).  In effect, we require an input string in order to successfully execute this program.

The first code block within the main function, after the main function signature are initialisations of local variables.

~~~c
  char cVar1;
  byte bVar2;
  int iVar3;
  undefined8 uVar4;
  long in_FS_OFFSET;
  int local_f0;
  int local_ec;
  char local_e8 [100];
  undefined local_84;
  char local_78 [104];
  long local_10;
~~~

We can rename these later to reflect the purpose of these variables.

The first line after initialisations, is generating a local long integer value read from the FileSystem value at FS:0x28, known as the stack_cookie:

~~~c
local_10 = *(long *)(in_FS_OFFSET + 0x28);
~~~

This is used to verify the integrity of the stack prior to the completion of the program execution.  It is a code-hardening technique to protect againt buffer overflows.  The validation code can be found towards the end of the main function:

~~~c
if (local_10 != *(long *)(in_FS_OFFSET + 0x28)) {
    /* WARNING: Subroutine does not return */
  __stack_chk_fail();
}
~~~

[stack_chk_fail()](http://refspecs.linux-foundation.org/LSB_4.1.0/LSB-Core-generic/LSB-Core-generic/libc---stack-chk-fail-1.html) is a function that aborts execution of the program.

After checking the input to the program, the program first copies the input string to a new local variable, local_e8, using the function [strncpy](https://www.cplusplus.com/reference/cstring/strncpy/) up to 100 characters in length.  This is the input key and we can rename to key_str:

~~~c
strncpy(key_str,(char *)argv[1],100);
~~~

An unknown variable, "local_84" is set to zero in the next line.  This is not used elsewhere in the code so can be removed from the program.

A new integer, "local_f0", is set to 0 and used to increment through an iterative while loop.  We can rename this variable i:

~~~c
int i;
...

i = 0;
while (true){
  ...
  i = i + 1;
}
~~~

This is a [for loop](https://www.tutorialspoint.com/cprogramming/c_for_loop.htm) iterating through the length of the key_str string and can be re-written using the [strlen()](https://www.programiz.com/c-programming/library-function/string.h/strlen) function for clarity:

~~~c
for (int i=0; i<strlen(key_str); i++){
  ...
}
~~~

The first line of this loop checks the corresponding key_str index to see if it is a valid character using the string function [valid_char](https://valadoc.org/glib-2.0/string.valid_char.html).  If the valid_char returns FALSE, this sets the ret_val to 1 and breaks from the loop:

~~~c
ret_val = valid_char(key_str[i]);
if ((int)ret_val == 0) break;
~~~

The next code block affects the first character of the key_str.  This assigns two local variables from the key_str using local function, jumble, and using binary shift operations.  The first local variable, "cVar1" is a char variable that is set from the jumble function.  The second local variable, "bVar2" is a byte variable set using bit shifting operations on cVar1. These are appended to the local character array, "local_78" we can rename these as x, y and new_str:

~~~c
x = jumble(key_str[0]);
y = (byte)(x >> 7) >> 4;
new_str[0] = (x + y & 0xf) - y;
~~~

The new_str[0] character is assigned the value of the summation of y subtracted from x and the bitwise AND calculation (y & 0xf).

for all other indexes (above 0) the local variable x is calculated using the jumble function from the key_str character.  The byte variable, y, is set from the summation of x and the previous character, bit shifted.  New_str[i] is a function of the previous character and x and y:

~~~c
x = jumble(key_str[i]);
y = (byte)((int)x + (int)new_str[i - 1] >> 0x37);
new_str[i] = ((char)((int)x + (int)new_str[i - 1]) + (y >> 4) & 0xf) - (y >> 4);
~~~

We can re-write this entire for loop to make it more condensed and easier to reverse engineer:

~~~c
for(int i=0; i<strlen(key_str); i++){
  ret_val = valid_char(key_str[i]);
  if ((int)ret_val == 0) break;
  x = jumble(key_str[i]);
  if (i == 0) {
    y = (byte)(x >> 7) >> 4;
    new_str[0] = (x + y & 0xf) - y;
  } else {
    y = (byte)((int)x + (int)new_str[i - 1] >> 0x37);
    new_str[i] = ((char)((int)x + (int)new_str[i - 1]) + (y >> 4) & 0xf) - (y >> 4);
  }
}
~~~

The next code block is another for loop adding 48 ('a') to each string value:

~~~c
local_ec = 0;
while (local_ec < i) {
  new_str[local_ec] = new_str[local_ec] + 'a';
  local_ec = local_ec + 1;
}
~~~

We can rewrite this to condense it again:

~~~c
for(int j=0; j<100; j++){
  new_str[j] = new_str[j] + 'a';
}
~~~

The final operation compares the new_str to a known correct string to identify if the original key input is correct and jumps to the nex code block if it is correct, or returns an error if incorrect:

~~~c
if (i == 100) {
  iVar3 = strncmp(new_str,"mngjlepdcbcmjmmjipmmegfkjbicaemoemkkpjgnhgomlknmoepmfbcoffikhplmadmganmlojndmfahbhaancamdhfdkiancdjf",100);
  if (iVar3 == 0) {
    puts("You got the key, congrats! Now xor it with the flag!");
    ret_val = 0;
    goto LAB_001009ea;
  }
}
puts("Invalid key!");
ret_val = 1;
~~~

We can remove error checking and condense the main program block as shown below:

~~~c
undefined8 main(int argc,char *argv[])
{
  char x;
  byte y;
  char key_str [100];
  char new_str [104];
  
  // copy input string to local variable, up to 100 characters in length.
  strncpy(key_str,(char *)argv[1],100);
  
  // For loop to iterate through key string:
  for(int i=0; i<strlen(key_str); i++){
      
    // Calculate jumbled value from key_str character
    x = jumble(key_str[i])
      
    // Assign  new_str values:
    if (i == 0) {
      y = (byte)(x >> 7) >> 4;
      new_str[0] = (x + y & 0xf) - y;
    } else {
      y = (byte)((int)x + (int)new_str[i - 1] >> 0x37);
      new_str[i] = ((char)((int)x + (int)new_str[i - 1]) + (y >> 4) & 0xf) - (y >> 4);
    }
    new_str[j] = new_str[j] + 'a';
  }
  if(strncmp(new_str,"mngjlepdcbcmjmmjipmmegfkjbicaemoemkkpjgnhgomlknmoepmfbcoffikhplmadmganmlojndmfahbhaancamdhfdkiancdjf",100)){
    printf("Incorrect Key\n");
  } else {
    printf("Correct Key! Now xor it with the flag!");
  }
  return 0;
}
~~~

We need to review the jumble function to understand the return value:

~~~c
char jumble(char param_1)
{
  byte bVar1;
  char local_c;
  
  local_c = param_1;
  if ('`' < param_1) {
    local_c = param_1 + '\t';
  }
  bVar1 = (byte)(local_c >> 7) >> 4;
  local_c = ((local_c + bVar1 & 0xf) - bVar1) * '\x02';
  if ('\x0f' < local_c) {
    local_c = local_c + '\x01';
  }
  return local_c;
}
~~~

This is a series of binary operations that change the input character and return an adapted output character.  We can simplify this:

~~~c
char jumble(char input)
{
  byte x;
  
  if ('`' < input) {
    input = input + '\t';
  }
  x = (byte)(input >> 7) >> 4;
  input = ((input + x & 0xf) - x) * '\x02';
  if ('\x0f' < input) {
    input = input + '\x01';
  }
  return input;
}
~~~

We can rewrite these manipulation subroutines as function in Python:

~~~py
def jumble(c):
    c = ord(c)
    if (c > 96):
        c += 9
    a = (c>>7)>>4
    c = ((c + a & 0xf) - a) * 2
    if c > 15:
        c += 1
    return chr(c)

def newstr(keystr):
    outstr = ''
    for i in range(0,len(keystr),1):
        x = jumble(keystr[i])
        if i==0:
            y = (ord(x)>>7)>>4
            outstr += chr((ord(x)+y&0xf)-y)
        else:
            y = ord(x)+ord(outstr[i-1])>>0x37
            outstr += chr(((ord(x)+ord(outstr[i-1]))+(y>>4)&0xf)-(y>>4))
    return outstr
~~~

The test string can be adapted for direct comparison:

~~~py
test_str1 = "mngjlepdcbcmjmmjipmmegfkjbicaemoemkkpjgnhgomlknmoepmfbcoffikhplmadmganmlojndmfahbhaancamdhfdkiancdjf"
test_str2 = ''

for i in range(0,len(test_str1),1):
    test_int = ord(test_str1[i])
    test_str2 += chr(test_int-97)
~~~

The enciphered flag and key are both hex strings, we can iterate through a key string using hex alphanumeric characters:

~~~py
key_str = ''
charset = "0123456789abcdef"

for i in range(0,len(test_str2),1):
    string = test_str2[:i+1]
    for a in charset:
        b = key_str + a
        c = newstr(b)
        if(c==string):
            key_str += a
            break
~~~

We should now have the key in hex string form, we need to convert this into a byte array to be XOR's with the enciphered flag:

~~~py
key_int = int(key_str,16)
    
ct_str = "18a07fbdbcd1af759895328ec4d82d2b411dc7876c34a0ab61eda8f2efa5bb0f198a3aa0ac47ff9a0cf3d913d3138678ce4b"
ct_int = int(ct_str,16)

flag_int = key_int^ct_int
flag = bytearray.fromhex(hex(flag_int)[2:]).decode()
print(flag)
~~~

Running this, we get the response:

~~~shell
In [1]: runfile('otp.py')
picoCTF{cust0m_jumbl3s_4r3nt_4_g0Od_1d3A_33ead16f}
~~~

</details>

### Answer

<details>

<summary markdown="span">Flag</summary>

~~~
picoCTF{cust0m_jumbl3s_4r3nt_4_g0Od_1d3A_33ead16f}
~~~

</details>

---

### [Reverse Engineering](#contents) | [PicoCTF](./picoctf.md) | [Home](./index.md)

---
	
## Transformation

- Author: madStacks
- 20 points

### Description

I wonder what this really is... enc 

~~~
''.join([chr((ord(flag[i]) << 8) + ord(flag[i + 1])) for i in range(0, len(flag), 2)])
~~~

### Hints

1. You may find some decoders online
	
### Attachments

<details>

<summary markdown="span">enc</summary>

~~~
灩捯䍔䙻ㄶ形楴獟楮獴㌴摟潦弸彥ㄴㅡて㝽
~~~

</details>

### Solutions

<details>

<summary markdown="span">Solution 1</summary>

Solution 1

</details>

### Answer

<details>

<summary markdown="span">Flag</summary>

~~~
picoCTF{}
~~~

</details>

---

### [Reverse Engineering](#contents) | [PicoCTF](./picoctf.md) | [Home](./index.md)

---
	
## keygenme-py

- Author: Syreal
- 30 points

### Description

keygenme-trial.py

### Hints

None
	
### Attachments

<details>

<summary markdown="span">keygenme-trial.py</summary>

~~~py
#============================================================================#
#============================ARCANE CALCULATOR===============================#
#============================================================================#

import hashlib
from cryptography.fernet import Fernet
import base64



# GLOBALS --v
arcane_loop_trial = True
jump_into_full = False
full_version_code = ""

username_trial = "FREEMAN"
bUsername_trial = b"FREEMAN"

key_part_static1_trial = "picoCTF{1n_7h3_|<3y_of_"
key_part_dynamic1_trial = "xxxxxxxx"
key_part_static2_trial = "}"
key_full_template_trial = key_part_static1_trial + key_part_dynamic1_trial + key_part_static2_trial

star_db_trial = {
  "Alpha Centauri": 4.38,
  "Barnard's Star": 5.95,
  "Luhman 16": 6.57,
  "WISE 0855-0714": 7.17,
  "Wolf 359": 7.78,
  "Lalande 21185": 8.29,
  "UV Ceti": 8.58,
  "Sirius": 8.59,
  "Ross 154": 9.69,
  "Yin Sector CL-Y d127": 9.86,
  "Duamta": 9.88,
  "Ross 248": 10.37,
  "WISE 1506+7027": 10.52,
  "Epsilon Eridani": 10.52,
  "Lacaille 9352": 10.69,
  "Ross 128": 10.94,
  "EZ Aquarii": 11.10,
  "61 Cygni": 11.37,
  "Procyon": 11.41,
  "Struve 2398": 11.64,
  "Groombridge 34": 11.73,
  "Epsilon Indi": 11.80,
  "SPF-LF 1": 11.82,
  "Tau Ceti": 11.94,
  "YZ Ceti": 12.07,
  "WISE 0350-5658": 12.09,
  "Luyten's Star": 12.39,
  "Teegarden's Star": 12.43,
  "Kapteyn's Star": 12.76,
  "Talta": 12.83,
  "Lacaille 8760": 12.88
}


def intro_trial():
    print("\n===============================================\n\
Welcome to the Arcane Calculator, " + username_trial + "!\n")    
    print("This is the trial version of Arcane Calculator.")
    print("The full version may be purchased in person near\n\
the galactic center of the Milky Way galaxy. \n\
Available while supplies last!\n\
=====================================================\n\n")


def menu_trial():
    print("___Arcane Calculator___\n\n\
Menu:\n\
(a) Estimate Astral Projection Mana Burn\n\
(b) [LOCKED] Estimate Astral Slingshot Approach Vector\n\
(c) Enter License Key\n\
(d) Exit Arcane Calculator")

    choice = input("What would you like to do, "+ username_trial +" (a/b/c/d)? ")
    
    if not validate_choice(choice):
        print("\n\nInvalid choice!\n\n")
        return
    
    if choice == "a":
        estimate_burn()
    elif choice == "b":
        locked_estimate_vector()
    elif choice == "c":
        enter_license()
    elif choice == "d":
        global arcane_loop_trial
        arcane_loop_trial = False
        print("Bye!")
    else:
        print("That choice is not valid. Please enter a single, valid \
lowercase letter choice (a/b/c/d).")


def validate_choice(menu_choice):
    if menu_choice == "a" or \
       menu_choice == "b" or \
       menu_choice == "c" or \
       menu_choice == "d":
        return True
    else:
        return False


def estimate_burn():
  print("\n\nSOL is detected as your nearest star.")
  target_system = input("To which system do you want to travel? ")

  if target_system in star_db_trial:
      ly = star_db_trial[target_system]
      mana_cost_low = ly**2
      mana_cost_high = ly**3
      print("\n"+ target_system +" will cost between "+ str(mana_cost_low) \
+" and "+ str(mana_cost_high) +" stone(s) to project to\n\n")
  else:
      # TODO : could add option to list known stars
      print("\nStar not found.\n\n")


def locked_estimate_vector():
    print("\n\nYou must buy the full version of this software to use this \
feature!\n\n")


def enter_license():
    user_key = input("\nEnter your license key: ")
    user_key = user_key.strip()

    global bUsername_trial
    
    if check_key(user_key, bUsername_trial):
        decrypt_full_version(user_key)
    else:
        print("\nKey is NOT VALID. Check your data entry.\n\n")


def check_key(key, username_trial):

    global key_full_template_trial

    if len(key) != len(key_full_template_trial):
        return False
    else:
        # Check static base key part --v
        i = 0
        for c in key_part_static1_trial:
            if key[i] != c:
                return False

            i += 1

        # TODO : test performance on toolbox container
        # Check dynamic part --v
        if key[i] != hashlib.sha256(username_trial).hexdigest()[4]:
            return False
        else:
            i += 1

        if key[i] != hashlib.sha256(username_trial).hexdigest()[5]:
            return False
        else:
            i += 1

        if key[i] != hashlib.sha256(username_trial).hexdigest()[3]:
            return False
        else:
            i += 1

        if key[i] != hashlib.sha256(username_trial).hexdigest()[6]:
            return False
        else:
            i += 1

        if key[i] != hashlib.sha256(username_trial).hexdigest()[2]:
            return False
        else:
            i += 1

        if key[i] != hashlib.sha256(username_trial).hexdigest()[7]:
            return False
        else:
            i += 1

        if key[i] != hashlib.sha256(username_trial).hexdigest()[1]:
            return False
        else:
            i += 1

        if key[i] != hashlib.sha256(username_trial).hexdigest()[8]:
            return False



        return True


def decrypt_full_version(key_str):

    key_base64 = base64.b64encode(key_str.encode())
    f = Fernet(key_base64)

    try:
        with open("keygenme.py", "w") as fout:
          global full_version
          global full_version_code
          full_version_code = f.decrypt(full_version)
          fout.write(full_version_code.decode())
          global arcane_loop_trial
          arcane_loop_trial = False
          global jump_into_full
          jump_into_full = True
          print("\nFull version written to 'keygenme.py'.\n\n"+ \
                 "Exiting trial version...")
    except FileExistsError:
    	sys.stderr.write("Full version of keygenme NOT written to disk, "+ \
	                  "ERROR: 'keygenme.py' file already exists.\n\n"+ \
			  "ADVICE: If this existing file is not valid, "+ \
			  "you may try deleting it and entering the "+ \
			  "license key again. Good luck")

def ui_flow():
    intro_trial()
    while arcane_loop_trial:
        menu_trial()



# Encrypted blob of full version
full_version = \
b"""
gAAAAABgT_nvdPbQsvAhvsNvjCeuMqNP4gGInWyNCirwqXlGMM4EDHMeVEIci77G1dQTtGCgsVSeUfJKzwcBldLozZ24_kcrd9fd-a81-z2KBOrI8Qv_IOhY1LqsooySaeEQMvjMqBhhLhoIDfsXBSWnEb8RPDXVzZhc_5WaNDorzw8lUMqf1vLI8bWCP97UnQZclfIa_hH-ib5hy6hXuimvny4X9-eOzEIAROHD5l-FB8r82ZfUiPKED2woAgROd1_PF9HrCN_Poi_b5D42E_-R4fTX5G6ASWexix3vtO9jXW9YqSI4mN-RMoTLcYHe6wAt89e-SnhmmVxdqXzsbx37Z0UNaEEToIaUqEWuI5hHWRx9ytb9GQLimBzBVd3ZS1vuOp4gYaxRzCy8tAR63G3QrEx3mo-XLPRm8ajHVMxlsbc5U9D11znoZKEYZd2zTjTPGxaHwXaQA7hw4ZWHEEQIAUaBtAJtB_Ua0ERrop1xG1P6U-zlAWKzzymqYIV88_yHqChyWta8291J-QTy5sYYsbWygg65G5Ea4G30Eu5I6izqanJMhMFTLcBSKx_b0HBokRvim65ywa8tCh4iYZFHDsOqr2kDgyq2pZuvSRRTEHaPJVct68QScVLmWlBXSIM36ng4izANXH1qWTMxakfHQ52MRKmKhRV3sVUHGgHqdtQWJPnIeKlnWw6bHUtGxAvCQLTgwO6HR3D5EAiHMB6qu5yiAxRJMWophLMIZNN0alYV2VX0Amvd54WqAW9MnO0q1sunAyao7l1JJe6bGYIeKSYwyRiQVKtQ2nOkWXuJCRPY3PsfcT9OAkfKRCowlGF_hPmgCpB3izpUNOAD8HuNrkqKIUhROAOU-WCa04rQ2ig7bETXfJJldPRQGCvHC9zzczQC-ppq1G5PWs_tjT8VwtrrOc_Nb14dGqbLkDuKdPMa09TJKhBto0kD8O0f-JO--TOl51bPSitqTT11E1ZLiRufSojQDDbpFBMTFJNzf5puj4r3JJnDERw0quqGU8IxBPR91ZfKKEjW1U44p5G5GBbHVN1JTb0j4hpQAyKbWQKs7kGIyuToTL0VKR0WBovSeOwR_O4KmDit6ncHHEBXt7FBD6BCWkmUPuiF2QfIIFW83AizJfilZ4YhIOjiBW2J3b7-CJj0Vayq8eZY_ZeDiehwErGeiuxgeH96TZVA3C9-vAnNjdSJLPGLU935tuv74HOsPln5zQCiNyhJ3JZR4BaWLyex3haa1X-XJJZLgeGAVNqtU0ByUR5nLG37tKF9POPEkTH7Z7ujMVtcH9GfK231Fm9giBurP2CQmInoyp_oyuErlBFDPH0p5F8qWx1zcgOUZBTscZPtCzrT4otRh0HCNSV0blYPwxPjvpW2Nqs-ojXjjRgMOS6prdbtTm0eiCMC0DLY9b4YY7Gt5CKYX4HM8eyaY8Z04WPCpVvqEOLTl4NSqUlWRaVEUcbCBQNdyHIFeUbDUrs9PjXa4_WMwbqMnBPzQmBzmx4KqJJZz9RCy7I0BeqP_wy0kcTV5q8SPfZPyz_WoHx65e3z0GCuxZrzN1D7rj_WLsTPp96oCkF3B9yBx81UKXgZodZrUGooEJLxglMTCwX35X_GTh2aIggPah_k8emL1_rX_psDqGlDUPMYj8Af_O1KinL9lylCtHgGYLyGInBzHMgv4ixHPqqHk56YFmsKgqWUwR8g9an8eevQwm9_KAcg6VzreQEYsCjnsGLKvEMHt7ll3QfwhHiW-GHnPWxvhk169hKVaidBXuJuHmOpsQad5eJyvywwg0Hx0cfd6cKi3RS4PQcaYBlQXw7nsQ3xDLk0s6Bv97G3MAyQ_FIi5ieHdWO1FMYW1kbZy3Zrx5muiRmoNEBaTyDVeko8rJ9aaZWEXV1gQdDVAr92bFT_tb2ZImbPc2yJxmynaRV40ZCnVuxmwLVwCq36BSLss6yz_vnUVpswWQ4qKDbFbdPAof9mkNt0fe4Vqe_MC4ZhVvWSlsJhTlMvLedsrTbp3mL2JGvBOfvxwiOGkO-XgW1F7TGMXzh8j-KbTVKHdt6xp3DRs1Uhae5hncMCaIGqq5ocTO9Id-esyaJEumEL7oR-uzYXss3z6rSOjnGDF0k0aWCCFEKMWe1zzYhZis74IsFZ7cCfV0daXkrdD7VFIgor0ifd4-DoLYxIr-eC-yLc7eVouoHHirk0PcrMC2w7SuXReCuYvMt-jcUlZBEphb9D_0IEZDsua_Rl62FwT-1wPzyZg_uGcUviq1h8Bkgh0rs4DBdheLwRg3k6ekdTzPA78bqk5qnSbSyJMD5fK4daKbplPcNFLHTMJzKSAhQeGx0Uw3NS70q_k2uLXvbaagMB5NHzM7ZzH8P5chxcT07hkNNt7dfu9_ux35z6sEIeCmQ-MqvVn4GRBK3zEF2t_PYsQw_da6lbzEiPVWIlqQUkFcmyhsL9hSFDeBkK18abEknjs3cdukrD-e9JRKdxRJxJW97gJM-btsh_5Nbf1pIz-uxQbQhBZQkHOqC4BWyLjg3xT92B-3yDmZnykvk7d8pXNHOwtXSHtBD0jCAdCzUyE9_U51p7icO8toV0sbZ9tj22tPe1DKMM5M2uMHQXCySv4oTGpTGp4xA4tD5Wo_o59zgzwlpXtKukU7cT8DS2NCBRlDW_2L6HojArs2NPeKtBm_-DIDCiSrHSYdiITZq7GaoeyAywiOiqlVNDdLy0p3lcNW_Yo4vXyzfSm8qXTfEpoAb9gPps0LbJhci1sWqNL9JJPI4yIca4r0rr9Y1wIEYuwXeyLoQD_Yn6xPRiVmuGSnco3HsIBOuDoyU3AGQOczn_QZ_TvyIJYdS8op8UJFRMD7W7lJWFe-ivoFdUlAjMqyDCUO_PbAeJYaE0ekh7xh3yudd7dMmD9LcTOi_LQoEfYjPXIEQPaC7D_SDYw8AbBJ51FyKSif7n_fW6_PU0U6vfYZwbPWU5tp0nNjTuaPxI_88tyuZC_2gW3YgAIWs4vo0zWBk9AvdgfxNwFiIdp4dugGGg0-dJp_SW_XzgGv1ALkaMbxiOYSK0sE8ZXb3_5zA3vUn2OsKpCq6ROt4poLIFce_Cot1RSU3FUYie2V4GT7ChUrq-vJfTPVlixee1gSPE7TnlyAm_kANyQ3_VFgIyEiEfGBLb_mlIWbVCO9e9QC6_SDKbc8UvuXodJ9HcDe-yWTjV7V-7s7-Qhp_WSIBVwex8tmyCo5W69An5eOrPRwK5NfCFp0uJClvim9qfLnVDXc5QQmajx61VuwnCVZg82iWxMh_Jms-2EiaCEz1oyB87F_awJ413I_kT8Wa6OW1ZhadZkDS5IVEZTNYwIxeIaVUoZLSBESHwwwzD7zsR02pGlJFJcWcvdI96wtCcx1os6g_Lq7tpTwd33zCA-RgYZWTHKPnFSi1z0h-RsyCIqbBmGx2eswpfJbKRKi_QFQMw60w7O41FWQL8ZluxBOSd3kSP5xyVJC7bnDfE3g_OnBdU5MFQGl6uFaIxr1lUt98GeD6Gt2X1A-Hi1zOF4iaxCbb9h9FECqUrwGlwGo_TY_W0ekFM1UXFVVcUwsCwm5hL_wC7hCcN5Ad4dWx9EAL4NX3_N8n9qC3hW_l34Cq5V4Xzm1O7T7py7XF_CZ_Xd_GDdU89f2hrV1IngHqey_fc9lTroIhoLeZ3v2nj7_9osKs7qLHa_QwnwQ5jH0LxhAOGS9FHLBGdn3tXnRyzglLLOTP3XR1qeoSOEqz4Uk13qfI3GRiHacUnyyyT2OHdi4IsrxlxzGNEjBMDws9FPjXH4Xv_R0iSeD77JBIKqgd0n0hxaZRu8lOUhmnJFHpe6OrnmK8nB4A-yHuI5z37zC3KJDgKxnBBs8zfAOP0-g==
"""



# Enter main loop
ui_flow()

if jump_into_full:
    exec(full_version_code)
~~~

</details>

### Solutions

<details>

<summary markdown="span">Solution 1</summary>

Solution 1

</details>

### Answer

<details>

<summary markdown="span">Flag</summary>

~~~
picoCTF{}
~~~

</details>

---

### [Reverse Engineering](#contents) | [PicoCTF](./picoctf.md) | [Home](./index.md)

---
	
## crackme-py

- Author: Syreal
- 30 points

### Description

crackme.py

### Hints

None
	
### Attachments

<details>

<summary markdown="span">crackme.py</summary>

~~~py
# Hiding this really important number in an obscure piece of code is brilliant!
# AND it's encrypted!
# We want our biggest client to know his information is safe with us.
bezos_cc_secret = "A:4@r%uL`M-^M0c0AbcM-MFE067d3eh2bN"

# Reference alphabet
alphabet = "!\"#$%&'()*+,-./0123456789:;<=>?@ABCDEFGHIJKLMNOPQRSTUVWXYZ"+ \
            "[\\]^_`abcdefghijklmnopqrstuvwxyz{|}~"



def decode_secret(secret):
    """ROT47 decode

    NOTE: encode and decode are the same operation in the ROT cipher family.
    """

    # Encryption key
    rotate_const = 47

    # Storage for decoded secret
    decoded = ""

    # decode loop
    for c in secret:
        index = alphabet.find(c)
        original_index = (index + rotate_const) % len(alphabet)
        decoded = decoded + alphabet[original_index]

    print(decoded)



def choose_greatest():
    """Echo the largest of the two numbers given by the user to the program

    Warning: this function was written quickly and needs proper error handling
    """

    user_value_1 = input("What's your first number? ")
    user_value_2 = input("What's your second number? ")
    greatest_value = user_value_1 # need a value to return if 1 & 2 are equal

    if user_value_1 > user_value_2:
        greatest_value = user_value_1
    elif user_value_1 < user_value_2:
        greatest_value = user_value_2

    print( "The number with largest positive magnitude is "
        + str(greatest_value) )



choose_greatest()
~~~

</details>

### Solutions

<details>

<summary markdown="span">Solution 1</summary>

Solution 1

</details>

### Answer

<details>

<summary markdown="span">Flag</summary>

~~~
picoCTF{}
~~~

</details>

---

### [Reverse Engineering](#contents) | [PicoCTF](./picoctf.md) | [Home](./index.md)

---
	
## ARMssembly 0

- Author: Dylan McGuire
- 40 points

### Description

What integer does this program print with arguments 4134207980 and 950176538? File: chall.S Flag format: picoCTF{XXXXXXXX} -> (hex, lowercase, no 0x, and 32 bits. ex. 5614267 would be picoCTF{0055aabb})

### Hints

1. Simple Compare
	
### Attachments

<details>

<summary markdown="span">chall.S</summary>

~~~
	.arch armv8-a
	.file	"chall.c"
	.text
	.align	2
	.global	func1
	.type	func1, %function
func1:
	sub	sp, sp, #16
	str	w0, [sp, 12]
	str	w1, [sp, 8]
	ldr	w1, [sp, 12]
	ldr	w0, [sp, 8]
	cmp	w1, w0
	bls	.L2
	ldr	w0, [sp, 12]
	b	.L3
.L2:
	ldr	w0, [sp, 8]
.L3:
	add	sp, sp, 16
	ret
	.size	func1, .-func1
	.section	.rodata
	.align	3
.LC0:
	.string	"Result: %ld\n"
	.text
	.align	2
	.global	main
	.type	main, %function
main:
	stp	x29, x30, [sp, -48]!
	add	x29, sp, 0
	str	x19, [sp, 16]
	str	w0, [x29, 44]
	str	x1, [x29, 32]
	ldr	x0, [x29, 32]
	add	x0, x0, 8
	ldr	x0, [x0]
	bl	atoi
	mov	w19, w0
	ldr	x0, [x29, 32]
	add	x0, x0, 16
	ldr	x0, [x0]
	bl	atoi
	mov	w1, w0
	mov	w0, w19
	bl	func1
	mov	w1, w0
	adrp	x0, .LC0
	add	x0, x0, :lo12:.LC0
	bl	printf
	mov	w0, 0
	ldr	x19, [sp, 16]
	ldp	x29, x30, [sp], 48
	ret
	.size	main, .-main
	.ident	"GCC: (Ubuntu/Linaro 7.5.0-3ubuntu1~18.04) 7.5.0"
	.section	.note.GNU-stack,"",@progbits
~~~

</details>

### Solutions

<details>

<summary markdown="span">Solution 1</summary>

Solution 1

</details>

### Answer

<details>

<summary markdown="span">Flag</summary>

~~~
picoCTF{}
~~~

</details>

---

### [Reverse Engineering](#contents) | [PicoCTF](./picoctf.md) | [Home](./index.md)

---
	
## speeds and feeds

- Author: Ryan Ramseyer
- 50 points

### Description

There is something on my shop network running at nc mercury.picoctf.net 16524, but I can't tell what it is. Can you?

### Hints

1. What language does a CNC machine use?

### Solutions

<details>

<summary markdown="span">Solution 1</summary>

Solution 1

</details>

### Answer

<details>

<summary markdown="span">Flag</summary>

~~~
picoCTF{}
~~~

</details>

---

### [Reverse Engineering](#contents) | [PicoCTF](./picoctf.md) | [Home](./index.md)

---
	
## Shop

- Author: THELSHELL
- 50 points

### Description

Best Stuff - Cheap Stuff, Buy Buy Buy... Store Instance: source. The shop is open for business at nc mercury.picoctf.net 11371.

### Hints

1. Always check edge cases when programming
	
### Attachments

- source

</details>

### Solutions

<details>

<summary markdown="span">Solution 1</summary>

Solution 1

</details>

### Answer

<details>

<summary markdown="span">Flag</summary>

~~~
picoCTF{}
~~~

</details>

---

### [Reverse Engineering](#contents) | [PicoCTF](./picoctf.md) | [Home](./index.md)

---
	
## ARMssembly 1

- Author: Pranay Garg
- 70 points

### Description

For what argument does this program print `win` with variables 68, 2 and 3? File: chall_1.S Flag format: picoCTF{XXXXXXXX} -> (hex, lowercase, no 0x, and 32 bits. ex. 5614267 would be picoCTF{0055aabb})

### Hints

1. Shifts
	
### Attachments

<details>

<summary markdown="span">chall_1.S</summary>

~~~
	.arch armv8-a
	.file	"chall_1.c"
	.text
	.align	2
	.global	func
	.type	func, %function
func:
	sub	sp, sp, #32
	str	w0, [sp, 12]
	mov	w0, 68
	str	w0, [sp, 16]
	mov	w0, 2
	str	w0, [sp, 20]
	mov	w0, 3
	str	w0, [sp, 24]
	ldr	w0, [sp, 20]
	ldr	w1, [sp, 16]
	lsl	w0, w1, w0
	str	w0, [sp, 28]
	ldr	w1, [sp, 28]
	ldr	w0, [sp, 24]
	sdiv	w0, w1, w0
	str	w0, [sp, 28]
	ldr	w1, [sp, 28]
	ldr	w0, [sp, 12]
	sub	w0, w1, w0
	str	w0, [sp, 28]
	ldr	w0, [sp, 28]
	add	sp, sp, 32
	ret
	.size	func, .-func
	.section	.rodata
	.align	3
.LC0:
	.string	"You win!"
	.align	3
.LC1:
	.string	"You Lose :("
	.text
	.align	2
	.global	main
	.type	main, %function
main:
	stp	x29, x30, [sp, -48]!
	add	x29, sp, 0
	str	w0, [x29, 28]
	str	x1, [x29, 16]
	ldr	x0, [x29, 16]
	add	x0, x0, 8
	ldr	x0, [x0]
	bl	atoi
	str	w0, [x29, 44]
	ldr	w0, [x29, 44]
	bl	func
	cmp	w0, 0
	bne	.L4
	adrp	x0, .LC0
	add	x0, x0, :lo12:.LC0
	bl	puts
	b	.L6
.L4:
	adrp	x0, .LC1
	add	x0, x0, :lo12:.LC1
	bl	puts
.L6:
	nop
	ldp	x29, x30, [sp], 48
	ret
	.size	main, .-main
	.ident	"GCC: (Ubuntu/Linaro 7.5.0-3ubuntu1~18.04) 7.5.0"
	.section	.note.GNU-stack,"",@progbits
~~~

</details>

### Solutions

<details>

<summary markdown="span">Solution 1</summary>

Solution 1

</details>

### Answer

<details>

<summary markdown="span">Flag</summary>

~~~
picoCTF{}
~~~

</details>

---

### [Reverse Engineering](#contents) | [PicoCTF](./picoctf.md) | [Home](./index.md)

---
		
## ARMssembly 2

- Author: Dylan McGuire
- 90 points

### Description

What integer does this program print with argument 2403814618? File: chall_2.S Flag format: picoCTF{XXXXXXXX} -> (hex, lowercase, no 0x, and 32 bits. ex. 5614267 would be picoCTF{0055aabb})

### Hints

1. Loops
	
### Attachments

<details>

<summary markdown="span">chall_2.S</summary>

~~~
	.arch armv8-a
	.file	"chall_2.c"
	.text
	.align	2
	.global	func1
	.type	func1, %function
func1:
	sub	sp, sp, #32
	str	w0, [sp, 12]
	str	wzr, [sp, 24]
	str	wzr, [sp, 28]
	b	.L2
.L3:
	ldr	w0, [sp, 24]
	add	w0, w0, 3
	str	w0, [sp, 24]
	ldr	w0, [sp, 28]
	add	w0, w0, 1
	str	w0, [sp, 28]
.L2:
	ldr	w1, [sp, 28]
	ldr	w0, [sp, 12]
	cmp	w1, w0
	bcc	.L3
	ldr	w0, [sp, 24]
	add	sp, sp, 32
	ret
	.size	func1, .-func1
	.section	.rodata
	.align	3
.LC0:
	.string	"Result: %ld\n"
	.text
	.align	2
	.global	main
	.type	main, %function
main:
	stp	x29, x30, [sp, -48]!
	add	x29, sp, 0
	str	w0, [x29, 28]
	str	x1, [x29, 16]
	ldr	x0, [x29, 16]
	add	x0, x0, 8
	ldr	x0, [x0]
	bl	atoi
	bl	func1
	str	w0, [x29, 44]
	adrp	x0, .LC0
	add	x0, x0, :lo12:.LC0
	ldr	w1, [x29, 44]
	bl	printf
	nop
	ldp	x29, x30, [sp], 48
	ret
	.size	main, .-main
	.ident	"GCC: (Ubuntu/Linaro 7.5.0-3ubuntu1~18.04) 7.5.0"
	.section	.note.GNU-stack,"",@progbits
~~~

</details>

### Solutions

<details>

<summary markdown="span">Solution 1</summary>

Solution 1

</details>

### Answer

<details>

<summary markdown="span">Flag</summary>

~~~
picoCTF{}
~~~

</details>

---

### [Reverse Engineering](#contents) | [PicoCTF](./picoctf.md) | [Home](./index.md)

---
		
## Hurry up Wait

- Author: Syreal
- 100 points

### Description

svchost.exe

### Hints

None
	
### Attachments

- svchost.exe

### Solutions

<details>

<summary markdown="span">Solution 1</summary>

Solution 1

</details>

### Answer

<details>

<summary markdown="span">Flag</summary>

~~~
picoCTF{}
~~~

</details>

---

### [Reverse Engineering](#contents) | [PicoCTF](./picoctf.md) | [Home](./index.md)

---
		
## gogo
	
- Author: THELSHELL
- 110 points

### Description

Hmmm this is a weird file... enter_password. There is a instance of the service running at mercury.picoctf.net:20140.

### Hints

1. use go tool objdump or ghidra
	
### Attachments

- enter_password

### Solutions

<details>

<summary markdown="span">Solution 1</summary>

Solution 1

</details>

### Answer

<details>

<summary markdown="span">Flag</summary>

~~~
picoCTF{}
~~~

</details>

---

### [Reverse Engineering](#contents) | [PicoCTF](./picoctf.md) | [Home](./index.md)

---
		
## ARMssembly 3

- Author: Dylan McGuire
- 130 points

### Description

What integer does this program print with argument 3634247936? File: chall_3.S Flag format: picoCTF{XXXXXXXX} -> (hex, lowercase, no 0x, and 32 bits. ex. 5614267 would be picoCTF{0055aabb})

### Hints

1. beep boop beep boop...
	
### Attachments

<details>

<summary markdown="span">chall_2.S</summary>

~~~
	.arch armv8-a
	.file	"chall_3.c"
	.text
	.align	2
	.global	func1
	.type	func1, %function
func1:
	stp	x29, x30, [sp, -48]!
	add	x29, sp, 0
	str	w0, [x29, 28]
	str	wzr, [x29, 44]
	b	.L2
.L4:
	ldr	w0, [x29, 28]
	and	w0, w0, 1
	cmp	w0, 0
	beq	.L3
	ldr	w0, [x29, 44]
	bl	func2
	str	w0, [x29, 44]
.L3:
	ldr	w0, [x29, 28]
	lsr	w0, w0, 1
	str	w0, [x29, 28]
.L2:
	ldr	w0, [x29, 28]
	cmp	w0, 0
	bne	.L4
	ldr	w0, [x29, 44]
	ldp	x29, x30, [sp], 48
	ret
	.size	func1, .-func1
	.align	2
	.global	func2
	.type	func2, %function
func2:
	sub	sp, sp, #16
	str	w0, [sp, 12]
	ldr	w0, [sp, 12]
	add	w0, w0, 3
	add	sp, sp, 16
	ret
	.size	func2, .-func2
	.section	.rodata
	.align	3
.LC0:
	.string	"Result: %ld\n"
	.text
	.align	2
	.global	main
	.type	main, %function
main:
	stp	x29, x30, [sp, -48]!
	add	x29, sp, 0
	str	w0, [x29, 28]
	str	x1, [x29, 16]
	ldr	x0, [x29, 16]
	add	x0, x0, 8
	ldr	x0, [x0]
	bl	atoi
	bl	func1
	str	w0, [x29, 44]
	adrp	x0, .LC0
	add	x0, x0, :lo12:.LC0
	ldr	w1, [x29, 44]
	bl	printf
	nop
	ldp	x29, x30, [sp], 48
	ret
	.size	main, .-main
	.ident	"GCC: (Ubuntu/Linaro 7.5.0-3ubuntu1~18.04) 7.5.0"
	.section	.note.GNU-stack,"",@progbits
~~~

</details>

### Solutions

<details>

<summary markdown="span">Solution 1</summary>

Solution 1

</details>

### Answer

<details>

<summary markdown="span">Flag</summary>

~~~
picoCTF{}
~~~

</details>

---

### [Reverse Engineering](#contents) | [PicoCTF](./picoctf.md) | [Home](./index.md)

---
		
## Lets get dynamic

- Author: Ryan Ramseyer
- 150 points

### Description

Can you tell what this file is reading? chall.S

### Hints

1. Running this in a debugger would be helpful
	
### Attachments

<details>

<summary markdown="span">chall.S</summary>

~~~
	.file	"chall.c"
	.text
	.section	.rodata
	.align 8
.LC1:
	.string	"Correct! You entered the flag."
.LC2:
	.string	"No, that's not right."
	.align 8
.LC0:
	.string	"\207\312\304\371\307m\2753&V\035A"
	.string	"\231]\314~\025\345\225\343\177\013M\214\034SJG\246i\372\026\0323@\033jW\204\370\311}\221\350T\236pr"
	.text
	.globl	main
	.type	main, @function
main:
.LFB5:
	.cfi_startproc
	pushq	%rbp
	.cfi_def_cfa_offset 16
	.cfi_offset 6, -16
	movq	%rsp, %rbp
	.cfi_def_cfa_register 6
	pushq	%rbx
	subq	$296, %rsp
	.cfi_offset 3, -24
	movl	%edi, -292(%rbp)
	movq	%rsi, -304(%rbp)
	movq	%fs:40, %rax
	movq	%rax, -24(%rbp)
	xorl	%eax, %eax
	movq	.LC0(%rip), %rax
	movq	8+.LC0(%rip), %rdx
	movq	%rax, -144(%rbp)
	movq	%rdx, -136(%rbp)
	movq	16+.LC0(%rip), %rax
	movq	24+.LC0(%rip), %rdx
	movq	%rax, -128(%rbp)
	movq	%rdx, -120(%rbp)
	movq	32+.LC0(%rip), %rax
	movq	40+.LC0(%rip), %rdx
	movq	%rax, -112(%rbp)
	movq	%rdx, -104(%rbp)
	movzwl	48+.LC0(%rip), %eax
	movw	%ax, -96(%rbp)
	movabsq	$6696342006613324260, %rax
	movabsq	$-8132455899522779815, %rdx
	movq	%rax, -80(%rbp)
	movq	%rdx, -72(%rbp)
	movabsq	$1620531284261501257, %rax
	movabsq	$-8910415579227789898, %rdx
	movq	%rax, -64(%rbp)
	movq	%rdx, -56(%rbp)
	movabsq	$-1220993050035004038, %rax
	movabsq	$9122898327681286650, %rdx
	movq	%rax, -48(%rbp)
	movq	%rdx, -40(%rbp)
	movw	$44, -32(%rbp)
	movq	stdin(%rip), %rdx
	leaq	-208(%rbp), %rax
	movl	$49, %esi
	movq	%rax, %rdi
	call	fgets@PLT
	movl	$0, -276(%rbp)
	jmp	.L2
.L3:
	movl	-276(%rbp), %eax
	cltq
	movzbl	-144(%rbp,%rax), %edx
	movl	-276(%rbp), %eax
	cltq
	movzbl	-80(%rbp,%rax), %eax
	xorl	%eax, %edx
	movl	-276(%rbp), %eax
	xorl	%edx, %eax
	xorl	$19, %eax
	movl	%eax, %edx
	movl	-276(%rbp), %eax
	cltq
	movb	%dl, -272(%rbp,%rax)
	addl	$1, -276(%rbp)
.L2:
	movl	-276(%rbp), %eax
	movslq	%eax, %rbx
	leaq	-144(%rbp), %rax
	movq	%rax, %rdi
	call	strlen@PLT
	cmpq	%rax, %rbx
	jb	.L3
	leaq	-272(%rbp), %rcx
	leaq	-208(%rbp), %rax
	movl	$49, %edx
	movq	%rcx, %rsi
	movq	%rax, %rdi
	call	memcmp@PLT
	testl	%eax, %eax
	je	.L4
	leaq	.LC1(%rip), %rdi
	call	puts@PLT
	movl	$0, %eax
	jmp	.L6
.L4:
	leaq	.LC2(%rip), %rdi
	call	puts@PLT
	movl	$1, %eax
.L6:
	movq	-24(%rbp), %rcx
	xorq	%fs:40, %rcx
	je	.L7
	call	__stack_chk_fail@PLT
.L7:
	addq	$296, %rsp
	popq	%rbx
	popq	%rbp
	.cfi_def_cfa 7, 8
	ret
	.cfi_endproc
.LFE5:
	.size	main, .-main
	.ident	"GCC: (Ubuntu 7.5.0-3ubuntu1~18.04) 7.5.0"
	.section	.note.GNU-stack,"",@progbits
~~~

</details>

### Solutions

<details>

<summary markdown="span">Solution 1</summary>

Solution 1

</details>

### Answer

<details>

<summary markdown="span">Flag</summary>

~~~
picoCTF{}
~~~

</details>

---

### [Reverse Engineering](#contents) | [PicoCTF](./picoctf.md) | [Home](./index.md)

---
		
## Easy as GDB

- Author: MCKADE
- 160 points

### Description

The flag has got to be checked somewhere... File: brute

### Hints

1. [https://sourceware.org/gdb/onlinedocs/gdb/Basic-Python.html#Basic-Python](#https://sourceware.org/gdb/onlinedocs/gdb/Basic-Python.html#Basic-Python)
2. With GDB Python, I can guess wrong flags faster than ever before!
	
### Attachments

- brute

### Solutions

<details>

<summary markdown="span">Solution 1</summary>

Solution 1

</details>

### Answer

<details>

<summary markdown="span">Flag</summary>

~~~
picoCTF{}
~~~

</details>

---

### [Reverse Engineering](#contents) | [PicoCTF](./picoctf.md) | [Home](./index.md)

---
		
## ARMssembly 4

- Author: Dylan McGuire
- 170 points

### Description

What integer does this program print with argument 1215610622? File: chall_4.S Flag format: picoCTF{XXXXXXXX} -> (hex, lowercase, no 0x, and 32 bits. ex. 5614267 would be picoCTF{0055aabb})

### Hints

1. Switching things up
	
### Attachments

<details>

<summary markdown="span">chall_4.S</summary>

~~~
	.arch armv8-a
	.file	"chall_4.c"
	.text
	.align	2
	.global	func1
	.type	func1, %function
func1:
	stp	x29, x30, [sp, -32]!
	add	x29, sp, 0
	str	w0, [x29, 28]
	ldr	w0, [x29, 28]
	cmp	w0, 100
	bls	.L2
	ldr	w0, [x29, 28]
	add	w0, w0, 100
	bl	func2
	b	.L3
.L2:
	ldr	w0, [x29, 28]
	bl	func3
.L3:
	ldp	x29, x30, [sp], 32
	ret
	.size	func1, .-func1
	.align	2
	.global	func2
	.type	func2, %function
func2:
	stp	x29, x30, [sp, -32]!
	add	x29, sp, 0
	str	w0, [x29, 28]
	ldr	w0, [x29, 28]
	cmp	w0, 499
	bhi	.L5
	ldr	w0, [x29, 28]
	sub	w0, w0, #86
	bl	func4
	b	.L6
.L5:
	ldr	w0, [x29, 28]
	add	w0, w0, 13
	bl	func5
.L6:
	ldp	x29, x30, [sp], 32
	ret
	.size	func2, .-func2
	.align	2
	.global	func3
	.type	func3, %function
func3:
	stp	x29, x30, [sp, -32]!
	add	x29, sp, 0
	str	w0, [x29, 28]
	ldr	w0, [x29, 28]
	bl	func7
	ldp	x29, x30, [sp], 32
	ret
	.size	func3, .-func3
	.align	2
	.global	func4
	.type	func4, %function
func4:
	stp	x29, x30, [sp, -48]!
	add	x29, sp, 0
	str	w0, [x29, 28]
	mov	w0, 17
	str	w0, [x29, 44]
	ldr	w0, [x29, 44]
	bl	func1
	str	w0, [x29, 44]
	ldr	w0, [x29, 28]
	ldp	x29, x30, [sp], 48
	ret
	.size	func4, .-func4
	.align	2
	.global	func5
	.type	func5, %function
func5:
	stp	x29, x30, [sp, -32]!
	add	x29, sp, 0
	str	w0, [x29, 28]
	ldr	w0, [x29, 28]
	bl	func8
	str	w0, [x29, 28]
	ldr	w0, [x29, 28]
	ldp	x29, x30, [sp], 32
	ret
	.size	func5, .-func5
	.align	2
	.global	func6
	.type	func6, %function
func6:
	sub	sp, sp, #32
	str	w0, [sp, 12]
	mov	w0, 314
	str	w0, [sp, 24]
	mov	w0, 1932
	str	w0, [sp, 28]
	str	wzr, [sp, 20]
	str	wzr, [sp, 20]
	b	.L14
.L15:
	ldr	w1, [sp, 28]
	mov	w0, 800
	mul	w0, w1, w0
	ldr	w1, [sp, 24]
	udiv	w2, w0, w1
	ldr	w1, [sp, 24]
	mul	w1, w2, w1
	sub	w0, w0, w1
	str	w0, [sp, 12]
	ldr	w0, [sp, 20]
	add	w0, w0, 1
	str	w0, [sp, 20]
.L14:
	ldr	w0, [sp, 20]
	cmp	w0, 899
	bls	.L15
	ldr	w0, [sp, 12]
	add	sp, sp, 32
	ret
	.size	func6, .-func6
	.align	2
	.global	func7
	.type	func7, %function
func7:
	sub	sp, sp, #16
	str	w0, [sp, 12]
	ldr	w0, [sp, 12]
	cmp	w0, 100
	bls	.L18
	ldr	w0, [sp, 12]
	b	.L19
.L18:
	mov	w0, 7
.L19:
	add	sp, sp, 16
	ret
	.size	func7, .-func7
	.align	2
	.global	func8
	.type	func8, %function
func8:
	sub	sp, sp, #16
	str	w0, [sp, 12]
	ldr	w0, [sp, 12]
	add	w0, w0, 2
	add	sp, sp, 16
	ret
	.size	func8, .-func8
	.section	.rodata
	.align	3
.LC0:
	.string	"Result: %ld\n"
	.text
	.align	2
	.global	main
	.type	main, %function
main:
	stp	x29, x30, [sp, -48]!
	add	x29, sp, 0
	str	w0, [x29, 28]
	str	x1, [x29, 16]
	ldr	x0, [x29, 16]
	add	x0, x0, 8
	ldr	x0, [x0]
	bl	atoi
	str	w0, [x29, 44]
	ldr	w0, [x29, 44]
	bl	func1
	mov	w1, w0
	adrp	x0, .LC0
	add	x0, x0, :lo12:.LC0
	bl	printf
	nop
	ldp	x29, x30, [sp], 48
	ret
	.size	main, .-main
	.ident	"GCC: (Ubuntu/Linaro 7.5.0-3ubuntu1~18.04) 7.5.0"
	.section	.note.GNU-stack,"",@progbits
~~~

</details>

### Solutions

<details>

<summary markdown="span">Solution 1</summary>

Solution 1

</details>

### Answer

<details>

<summary markdown="span">Flag</summary>

~~~
picoCTF{}
~~~

</details>

---

### [Reverse Engineering](#contents) | [PicoCTF](./picoctf.md) | [Home](./index.md)

---
		
## Powershelly

- Author: Sara
- 180 points

### Description

It's not a bad idea to learn to read Powershell. We give you the output, but do you think you can find the input? rev_PS.ps1 output.txt

### Hints

1. We tend to move only forward, but it may be a good idea to begin solving it backwards.
2. The flag is in standard format, I promise.
	
### Attachments

<details>

<summary markdown="span">rev_PS.ps1</summary>

~~~
$input = ".\input.txt"

$out = Get-Content -Path $input
$enc = [System.IO.File]::ReadAllBytes("$input")
$encoding = [system.Text.Encoding]::UTF8
$total = 264
$t = ($total + 1) * 5
$numLength = ($total * 30 ) + $t
if ($out.Length -gt 5 -or $enc.count -ne $numLength)
{
  Write-Output "Wrong format 5"
  Exit
}

else
{
  for($i=0; $i -lt $enc.count ; $i++)
  {
    if (($enc[$i] -ne 49) -and ($enc[$i] -ne 48) -and ($enc[$i] -ne 10) -and ($enc[$i] -ne 13) -and ($enc[$i] -ne 32))
    {
      Write-Output "Wrong format 1/0/"
      Exit
    }
  }
}

$blocks = @{}
for ($i=0; $i -lt $out.Length ; $i++)
{
  $r = $out[$i].Split(" ")
  if ($i -gt 0)
  {
    for ($j=0; $j -lt $r.Length ; $j++)
    {
    if ($r[$j].Length -ne 6)
    {
      Write-Output "Wrong Format 6" $r[$j].Length
      Exit
    }
      $blocks[$j] += $r[$j]
    }
  }
  else
  {
    for ($j=0; $j -lt $r.Length ; $j++)
    {
    if ($r[$j].Length -ne 6)
    {
      Write-Output "Wrong Format 6" $r[$j].Length
      Exit
    }
      $blocks[$j] = @()
      $blocks[$j] += $r[$j]
    }
  }

}


function Exit  {
  exit
}


function Random-Gen {
  $list1 = @()
  for ($i=1; $i -lt ($blocks.count + 1); $i++)
  {
    $y = ((($i * 327) % 681 ) + 344) % 313
    $list1 += $y
  }
  return $list1
}


function Scramble {
    param (
        $block,
        $seed
    )
    $raw = [system.String]::Join("", $block)
    $bm = "10 " * $raw.Length
    $bm = $bm.Split(" ")
    for ($i=0; $i -lt $raw.Length ; $i++)
    {

      $y = ($i * $seed) % $raw.Length
      $n = $bm[$y]
      while ($n -ne "10")
      {
        $y = ($y + 1) % $raw.Length
        $n = $bm[$y]
      }
      if ($raw[$i] -eq "1" )
      {
        $n = "11"
      }
      else
      {
      $n = "00"
      }
      $bm[$y] = $n
    }
    $raw2 = [system.String]::Join("", $bm)
    $b = [convert]::ToInt64($raw2,2)
    return $b
}


$result = 0
$seeds = @()
for ($i=1; $i -lt ($blocks.count +1); $i++)
{
  $seeds += ($i * 127) % 500
}

$randoms = Random-Gen
$output_file = @()
for ($i=0; $i -lt $blocks.count ; $i++)
{

  $fun = Scramble -block $blocks[$i] -seed $seeds[$i]
  if($i -eq 263)
  {
  Write-Output $seeds[$i]
  Write-Output $randoms[$i]
  Write-Output $fun
  }
  $result = $fun -bxor $result -bxor $randoms[$i]
  $output_file += $result
}
  Add-Content -Path output.txt -Value $output_file
~~~

</details>

<details>

<summary markdown="span">output.txt</summary>

~~~
879059547225600221
71793452475485205
1148698281253257227
217070812329394967
1085086090799284516
4238685779263969
1085311228075820020
4486897510174167
879257471590075933
233062363111948053
879310247956329413
220620237942043428
864704387274818528
219564707018453810
1080930139169943704
284575531841633519
1095289279840717921
219827558966836273
922164813414728577
71789326353092547
922970468266331303
284624197914774733
935887582569446640
233341656386976839
1095496211378261093
270431259404009621
922112088142040996
271114274360574141
936480455350027154
14580558453485969
1149315982842597017
273649820165456770
1134960775807159720
69285389258153
868979240123514018
230541216188255296
1148645726972267632
72057336087430075
1135966209599275106
220398260916600638
1152010064483073927
271272397879702293
1139343700758887558
271077784355540943
1139146754428701768
4222399461461231
922326496319573062
283942073776672713
1081923578845401015
274442431825195106
1097967845536444498
16944574752682771
935675805365747915
67832102939014098
1081920473329287448
1073068336005587
1081721748899955656
55155024869773009
918738451380057054
274652781735887568
918791227752582714
270430592862047689
922960640253902083
17112864268238567
878479842607955275
229951587760733494
881632416504951469
1112495565767363
882638470697435530
17112815333330190
1151848652045611600
54057266045841968
919582927853977200
274441624099950113
881860882925030709
58476429884768707
869190591810957703
220606270746394268
1138496186912600710
288226252967132741
1139407393294925175
68609593282673765
1095272117148061322
68468771777351541
935689876626275940
287170512185785987
1098877480162557621
220452029779136139
1138341911719821923
287966424658087442
933159088420617518
57487952572330426
1084466749241033436
13735927918412192
881805026941256233
216450958350103112
1135821692603413223
284838396737815122
1148422235162410505
271130552259837474
922972957682372071
220675298603830864
1139406530802367886
18010259016859042
879323443101908642
284839262375919183
1149490972761796781
58493138394427981
922182117624696644
71780503401582160
922129603001122379
13464974967361
918750881951576401
57636189074621104
882438342200737477
233910087384579782
882635416186125660
288018432198980036
882691507922931320
229740485016616693
1081778432842190433
274504086948213472
919012484050846377
273870767986373374
1098653128292552208
17789823524785699
936484823391600233
288006061884174664
1135755039810466391
220610149264392545
923026816572866165
220673079782928545
1084509890119794064
57698195299630181
1098597714352143950
273662949817528928
1084245170751013532
233289910418682556
1152868676445159022
273861906596622869
1152062995421196783
16892006533755522
878202962169560357
219551526581911207
1081712678517132855
54901075530993324
1138351810784785110
287368617589457513
918959449055625535
68663387948777742
864744991438602546
17789270218755452
879100224243548756
18010272116257113
879323430003683923
284839275073057464
935837243715555216
233127265157825173
1098822166335471510
284585233327522172
1081089049280840078
66190813938289
1085311369869266603
217017417431055728
1085086103734386376
4238672944955073
868969548061077922
230585125518176963
1134964279694586486
58532504927404773
935903202292740735
13788713532460788
1098610032472277687
273808907837424086
1098611059250691362
287170705462591839
935904280600953359
54953797377651428
1081972437337034002
3431352717032734
882490899915869684
217017478683823314
1080880677300142569
3395020505739494
864760452650840824
68399248252862156
1152854450759479489
72056508471328536
1135967031275879667
220398260878299005
923237031130165425
220461087109169122
1081778639814733919
54940658191577131
1094599850818548609
271327652553490220
1080916961136738199
229961702408703798
868279998848633946
54044282154139485
879258544116612891
284625063628717240
879258296069853009
284798865657302933
1152867835705298073
55168202888248452
1138513488130130342
287107984222384471
1085089592271237237
271274871827451557
923224455449361838
67817894327611560
878469330928386996
270483416669012830
879274208876507235
220675540129136812
868980306940527370
230594235130183793
1094599899900607733
217282137553960044
1094652833283493100
283796252737158241
878482303020224500
270496420967206807
1138513245732277422
220675350747672793
1085300646950993669
14570660180524263
1149279867130331935
283727823485587214
1135765772921798622
55164714502340078
919001518395568616
14422035514995649
919002553226628642
270494089596571160
1081075896199954192
233909007654326019
1081765291043638494
3645104131685402
881847842601189364
287158284404650157
933353496081530906
288213815831556244
868082087813444404
71833031890124679
882441640700022534
233962879194169438
1151852763148127243
274455678322262261
869181263355903934
274442229753314412
1135751534516958032
71776131962646638
932248434541314171
229697655603511460
1149491014637175127
271063908134941100
936537392976704440
14636695302442350
1098824639182863983
216398129639732071
1084469432518917257
216177127761104710
~~~

</details>

### Solutions

<details>

<summary markdown="span">Solution 1</summary>

Solution 1

</details>

### Answer

<details>

<summary markdown="span">Flag</summary>

~~~
picoCTF{}
~~~

</details>

---

### [Reverse Engineering](#contents) | [PicoCTF](./picoctf.md) | [Home](./index.md)

---
		
## Rolling My Own

- Author: Luke Rindells
- 300 points

### Description

I don't trust password checkers made by other people, so I wrote my own. It doesn't even need to store the password! If you can crack it I'll give you a flag. remote nc mercury.picoctf.net 57112

### Hints

1. It's based on [this paper](#https://link.springer.com/article/10.1007/s11416-006-0011-3)
2. Here's the start of the password: D1v1
	
### Attachments

- remote

### Solutions

<details>

<summary markdown="span">Solution 1</summary>

Solution 1

</details>

### Answer

<details>

<summary markdown="span">Flag</summary>

~~~
picoCTF{}
~~~

</details>

---

### [Reverse Engineering](#contents) | [PicoCTF](./picoctf.md) | [Home](./index.md)

---
		
## Checkpass

- Author: Jay Bosamiya
- 375 points

### Description

What is the password? File: checkpass Flag format: picoCTF{...}

### Hints

1. How is the password being checked?
	
### Attachments

- checkpass

### Solutions

<details>

<summary markdown="span">Solution 1</summary>

Solution 1

</details>

### Answer

<details>

<summary markdown="span">Flag</summary>

~~~
picoCTF{}
~~~

</details>

---

### [Reverse Engineering](#contents) | [PicoCTF](./picoctf.md) | [Home](./index.md)

---
		
## not crypto

- Author: Asphyxia
- 150 points

### Description

there's crypto in here but the challenge is not crypto... 🤔

### Hints

None

### Attachments

- not-crypto

### Solutions

<details>

<summary markdown="span">Solution 1</summary>

Solution 1

</details>

### Answer

<details>

<summary markdown="span">Flag</summary>

~~~
picoCTF{}
~~~

</details>

---

### [Reverse Engineering](#contents) | [PicoCTF](./picoctf.md) | [Home](./index.md)

---
		
## breadth

- Author: Asphyxia
- 200 points

### Description

Surely this is what people mean when they say "horizontal scaling," right?

TOP SECRET INFO:

Our operatives managed to exfiltrate an in-development version of this challenge, where the function with the real flag had a mistake in it. Can you help us get the flag?

### Hints

None
	
### Attachments

- breadth.v1
- breadth.v2

### Solutions

<details>

<summary markdown="span">Solution 1</summary>

Solution 1

</details>

### Answer

<details>

<summary markdown="span">Flag</summary>

~~~
picoCTF{}
~~~

</details>

---

### [Reverse Engineering](#contents) | [PicoCTF](./picoctf.md) | [Home](./index.md)

---
		
## riscy business

- Author: Asphyxia
- 350 points

### Description

Try not to take too many riscs when finding the flag.

### Hints

None
	
### Attachments

- riscy

### Solutions

<details>

<summary markdown="span">Solution 1</summary>

Solution 1

</details>

### Answer

<details>

<summary markdown="span">Flag</summary>

~~~
picoCTF{}
~~~

</details>

---

### [Reverse Engineering](#contents) | [PicoCTF](./picoctf.md) | [Home](./index.md)

---
		
## MATRIX

- Author: Asphyxia
- 500 points

### Description

Enter the M A T R I X

nc mars.picoctf.net 31259

### Hints

None
	
### Attachments

- matrix

### Solutions

<details>

<summary markdown="span">Solution 1</summary>

Solution 1

</details>

### Answer

<details>

<summary markdown="span">Flag</summary>

~~~
picoCTF{}
~~~

</details>

---

### [Reverse Engineering](#contents) | [PicoCTF](./picoctf.md) | [Home](./index.md)

---

## [djm89uk.github.io](https://djm89uk.github.io)
