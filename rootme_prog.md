# [Root-Me](./rootme.md) Root-Me Programming [4/18]

Automate tasks and build shellcodes.

There are two types of challenges here:
1. automation challenges, which require you to write code in order to solve a task in constrained time
2. shellcoding challenges, which require you to build assembly payloads, also known as shellcodes

## Contents

1. [IRC - Go back to college](#irc-go-back-to-college) 🗸
2. [IRC - Encoded string](#irc-encoded-string) 🗸
3. [IRC - The Roman’s wheel](#irc-the-romans-wheel) 🗸
4. [IRC - Uncompress me](#irc-uncompress-me) 🗸
5. [CAPTCHA me if you can](#captcha-me-if-you-can)
6. [Ethereum - Tutoreum](#ethereum-tutoreum)
7. [Arithmetic progression](#arithmetic-progression)
8. [ELF x64 - Shellcoding - Sheep warmup](#elf-x64-shellcoding-sheep-warmup)
9. [Ethereum - Takeover](#ethereum-takeover)
10. [Various encodings](#various-encodings)
11. [ARM - Shellcoding - Egg hunter](#arm-shellcoding-egg-hunter)
12. [Ethereum - NotSoPriv8](#ethereum-notsopriv8)
13. [ELF x64 - Shellcoding - Polymorphism](#elf-x64-shellcoding-polymorphism)
14. [Quick Response Code](#quick-response-code)
15. [WinKern x64 - shellcoding : token stealing](#winkern-x64-shellcoding-token-stealing)
16. [Ethereum - BadStack](#ethereum-badstack)
17. [ELF x64 - Sandbox shellcoding](#elf-x64-sandbox-shellcoding)
18. [ELF x86 - Shellcoding - Alphanumeric](#elf-x86-shellcoding-alphanumeric)

---

### [Programming](#contents) | [Root-Me](./rootme.md) | [Home](./index.md)

---

## IRC Go back to college

- Author: Baco
- Date: 30 April 2011
- Points: 5
- Level: 1

### Statement

To start the challenge using IRC, you must send a private message to bot Candy : !ep1. The bot replies with a message in private with a string like this:

~~~
<number1>/<number2>
~~~

You must calculate the square root of the number n°1 and multiply the result by the number n°2.
Then you need to round to two decimals.
You have 2 seconds to send the correct answer from the time the bot gets the message !ep1
If the bot does not respond, then you have been banned. Just wait a few minutes.
The answer must be sent as :
 
~~~
!ep1 -rep <answer>.
~~~

Example :

~~~
25/2

You must send "!ep1 -rep <reponse>" as private message to the bot.
~~~

### Connection Details

1. Host: irc.root-me.org
2. Protocol: IRC
3. Port: 6667
4. IRC Channel: #root-me_challenge
5. Bot: candy

### Links

1. [root-me_challenge](irc://irc.root-me.org:6667/root-me_challenge)


### Resources

1. [Perl](https://repository.root-me.org/Programmation/Perl/)
2. [Python](https://repository.root-me.org/Programmation/Python/)
3. [PHP](https://repository.root-me.org/Programmation/PHP/)

### Solutions

<details>

<summary markdown="span">Solution 1</summary>

We can write a python code to run the IRC bot:

~~~py
import numpy as np
import socket
import time

def solution(number1, number2):
    num1 = np.sqrt(np.double(number1))
    num2 = np.double(number2)
    answer = str(np.round(num1*num2,2))
    return answer

def response(text):
    text = "PRIVMSG candy :!ep1 -rep "+text+"\r\n"
    return text
        
host="irc.root-me.org"
port=6667
channel = "#root-me_challenge"
botnick = "unique123"

irc = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
irc.connect((host,port))
time.sleep(2)
irc.send(("NICK "+botnick+"\r\n").encode())
irc.send(("USER "+botnick+" 0 * :UNI\r\n").encode())
time.sleep(5)
irc.send(("PRIVMSG candy :!ep1\r\n").encode())
time.sleep(0.5)

while 1:
    text = ""
    text = irc.recv(7000).decode()
    print(text)
    if text.find("/")>-1:
        text = text.split("PRIVMSG "+botnick+" :")[1]
        num1 = text.split("/")[0]
        num2 = text.split("/")[1]
        answer = solution(num1,num2)
        print("{}**0.5*{} = {}".format(num1,num2,answer))
        resp = response(answer)
        print("{}".format(resp))
        irc.send(resp.encode())
        print(irc.recv(7000))
        break
irc.close()
~~~

</details>

### Answer

<details>

<summary markdown="span">Answer</summary>

~~~
jaimlefr0m4g
~~~

</details>

---

### [Programming](#contents) | [Root-Me](./rootme.md) | [Home](./index.md)

---

## IRC Encoded string

- Author: Baco
- Date: 30 April 2011
- Points: 10
- Level: 1

### Statement

To start this challenge, you must send a private message to bot Candy: !ep2

- The bot answer you by a private message.
- This is a series of encoded characters.
- You must send him the decoded message.
- You have 2 seconds.
- If the bot does not respond, then you have been banned. Just wait a few minutes.
- The answer must be sent as :

~~~
!ep2 -rep <answer>.
~~~

Example :

~~~
Um9vdE1l

You must send "!ep2 -rep RootMe" as private message to bot.
~~~

### Connection Details

1. Host: irc.root-me.org
2. Protocol: IRC
3. Port: 6667
4. IRC Channel: #root-me_challenge
5. Bot: candy

### Links

1. [root-me_challenge](irc://irc.root-me.org:6667/root-me_challenge)


### Resources

1. [Perl](https://repository.root-me.org/Programmation/Perl/)
2. [Python](https://repository.root-me.org/Programmation/Python/)
3. [PHP](https://repository.root-me.org/Programmation/PHP/)

### Solutions

<details>

<summary markdown="span">Solution 1</summary>

We can write a python code to run the IRC bot:

~~~py
import socket
import time
import base64 as b64

def solution(question):
    answer = b64.b64decode(question.encode()).decode()
    return answer

def response(text):
    text = "PRIVMSG candy :!ep2 -rep "+text+"\r\n"
    return text
        
host="irc.root-me.org"
port=6667
channel = "#root-me_challenge"
botnick = "unique123"

irc = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
irc.connect((host,port))
time.sleep(2)
irc.send(("NICK "+botnick+"\r\n").encode())
irc.send(("USER "+botnick+" 0 * :UNI\r\n").encode())
time.sleep(5)
irc.send(("PRIVMSG candy :!ep2\r\n").encode())
time.sleep(0.5)

while 1:
    text = ""
    text = irc.recv(7000).decode()
    print(text)
    if text.find("PRIVMSG "+botnick)>-1:
        text = text.split("PRIVMSG "+botnick+" :")[1]
        question = text[:-2]
        answer = solution(question)
        print("{} = {}".format(question, answer))
        resp = response(answer)
        print("{}".format(resp))
        irc.send(resp.encode())
        print(irc.recv(7000))
        break
irc.close()
~~~

</details>

### Answer

<details>

<summary markdown="span">Answer</summary>

~~~
Viv3l"64
~~~

</details>

---

### [Programming](#contents) | [Root-Me](./rootme.md) | [Home](./index.md)

---

## IRC The Romans Wheel

- Author: lokhi
- Date: 04 May 2011
- Points: 10
- Level: 1

### Statement

To start this challenge, you must send a private message to bot Candy: !ep3

- The bot answer you by a private message.
- This is an encoded string with ROT13.
- You must send him the message decoded.
- You have 2 second.
- If the bot does not respond, then you have been banned. Just wait a few minutes.
- The answer must be sent as :

~~~
!ep3 -rep <reponse>
~~~

Example :

~~~
WnvzrEbbgZR

You must send "!ep3 -rep JaimeRootME" as private message to the bot.
~~~

### Connection Details

1. Host: irc.root-me.org
2. Protocol: IRC
3. Port: 6667
4. IRC Channel: #root-me_challenge
5. Bot: candy

### Links

1. [root-me_challenge](irc://irc.root-me.org:6667/root-me_challenge)


### Resources

1. [Perl](https://repository.root-me.org/Programmation/Perl/)
2. [Python](https://repository.root-me.org/Programmation/Python/)
3. [PHP](https://repository.root-me.org/Programmation/PHP/)

### Solutions

<details>

<summary markdown="span">Solution 1</summary>

We can write a python code to run the IRC bot:

~~~py
import socket
import time
import codecs

def solution(question):
    answer = codecs.decode(question,'rot_13')
    return answer

def response(text):
    text = "PRIVMSG candy :!ep3 -rep "+text+"\r\n"
    return text
        
host="irc.root-me.org"
port=6667
channel = "#root-me_challenge"
botnick = "unique123"

irc = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
irc.connect((host,port))
time.sleep(2)
irc.send(("NICK "+botnick+"\r\n").encode())
irc.send(("USER "+botnick+" 0 * :UNI\r\n").encode())
time.sleep(5)
irc.send(("PRIVMSG candy :!ep3\r\n").encode())
time.sleep(0.5)

while 1:
    text = ""
    text = irc.recv(7000).decode()
    print(text)
    if text.find("PRIVMSG "+botnick)>-1:
        text = text.split("PRIVMSG "+botnick+" :")[1]
        question = text[:-2]
        answer = solution(question)
        print("{} = {}".format(question, answer))
        resp = response(answer)
        print("{}".format(resp))
        irc.send(resp.encode())
        print(irc.recv(7000))
        break
irc.close()
~~~

</details>

### Answer

<details>

<summary markdown="span">Answer</summary>

~~~
3bienBr4v0Continuepe7i7PONEY
~~~

</details>

---

### [Programming](#contents) | [Root-Me](./rootme.md) | [Home](./index.md)

---

## IRC Uncompress Me

- Author: HacKSpider
- Date: 4 May 2011
- Points: 10
- Level: 1

### Statement

To start this challenge, you must send a private message to bot Candy: !ep4

- The bot answer you by a private message.
- This is a string compressed with zlib and encoded with base64.
- You must send him the original message.
- You have 2 seconds.
- If the bot does not respond, then you have been banned. Just wait a few minutes.
- The answer must be sent as :

~~~
!ep4 -rep <reponse>
~~~

Example :

~~~
eJxzrHItCqn0zC8AABBiA2g=

You must send "!ep4 -rep AzErTyIop" as private message to the bot.
~~~

### Connection Details

1. Host: irc.root-me.org
2. Protocol: IRC
3. Port: 6667
4. IRC Channel: #root-me_challenge
5. Bot: candy

### Links

1. [root-me_challenge](irc://irc.root-me.org:6667/root-me_challenge)


### Resources

1. [Perl](https://repository.root-me.org/Programmation/Perl/)
2. [Python](https://repository.root-me.org/Programmation/Python/)
3. [PHP](https://repository.root-me.org/Programmation/PHP/)

### Solutions

<details>

<summary markdown="span">Solution 1</summary>

We can write a python code to run the IRC bot:

~~~py
import socket
import time
import base64 as b64
from zlib import decompress

def solution(question):
    step1 = b64.b64decode(question.encode())
    step2 = decompress(step1).decode()
    answer = step2
    return answer

def response(text):
    text = "PRIVMSG candy :!ep4 -rep "+text+"\r\n"
    return text
        
host="irc.root-me.org"
port=6667
channel = "#root-me_challenge"
botnick = "unique123"

irc = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
irc.connect((host,port))
time.sleep(2)
irc.send(("NICK "+botnick+"\r\n").encode())
irc.send(("USER "+botnick+" 0 * :UNI\r\n").encode())
time.sleep(5)
irc.send(("PRIVMSG candy :!ep4\r\n").encode())
time.sleep(0.5)

while 1:
    text = ""
    text = irc.recv(7000).decode()
    print(text)
    if text.find("PRIVMSG "+botnick)>-1:
        text = text.split("PRIVMSG "+botnick+" :")[1]
        question = text[:-2]
        answer = solution(question)
        print("{} = {}".format(question, answer))
        resp = response(answer)
        print("{}".format(resp))
        irc.send(resp.encode())
        print(irc.recv(7000))
        break
irc.close()
~~~

</details>

### Answer

<details>

<summary markdown="span">Answer</summary>

~~~
tumasp0wned
~~~

</details>

---

### [Programming](#contents) | [Root-Me](./rootme.md) | [Home](./index.md)

---

Last updated Jan 2022.

## [djm89uk.github.io](https://djm89uk.github.io)
