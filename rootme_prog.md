# [Root-Me](./rootme.md) Root-Me Programming [6/18]

Automate tasks and build shellcodes.

There are two types of challenges here:
1. automation challenges, which require you to write code in order to solve a task in constrained time
2. shellcoding challenges, which require you to build assembly payloads, also known as shellcodes

## Contents

1. [IRC - Go back to college](#irc-go-back-to-college) 🗸
2. [IRC - Encoded string](#irc-encoded-string) 🗸
3. [IRC - The Roman’s wheel](#irc-the-romans-wheel) 🗸
4. [IRC - Uncompress me](#irc-uncompress-me) 🗸
5. [CAPTCHA me if you can](#captcha-me-if-you-can) 🗸
6. [Ethereum - Tutoreum](#ethereum-tutoreum)
7. [Arithmetic progression](#arithmetic-progression) 🗸
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

## CAPTCHA me if you can

- Author: koma
- Date: 23 March 2012
- Points: 20
- Level: 1

### Statement

Break the CAPTCHA in less than 3 seconds.

### Links

1. [challenge site](http://challenge01.root-me.org/programmation/ch8/)


### Resources

1. [Perl](https://repository.root-me.org/Programmation/Perl/)
2. [Python](https://repository.root-me.org/Programmation/Python/)
3. [PHP](https://repository.root-me.org/Programmation/PHP/)

### Solutions

<details>

<summary markdown="span">Solution 1</summary>

Visiting the website we can see a CAPTCH and a form to submit the CAPTCHA.  This is generated in base64:

~~~html
<html>

<head></head>

<body>
    <link rel='stylesheet' property='stylesheet' id='s' type='text/css' href='/template/s.css' media='all' /><iframe id='iframe' src='https://www.root-me.org/?page=externe_header'></iframe>
    <p>Trop tard...<br>Rat&eacute;, retente ta chance.<br></p><br/><img src="data:image/png;base64,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" /><br><br>
    <form action="" method="POST"><input type="text" name="cametu" /><input type="submit" value="Try" /></form>
</body>

</html>
~~~

We can use the Python [requests](https://docs.python-requests.org/en/latest/) library to GET and POST data to and from the webserver, and the Python [pytesseract](https://pypi.org/project/pytesseract/) library to solve th captcha.  Playing around with pytesseract, it has relatively low accuracy, so we must put this in a loop.  Our Python code:

~~~py
import base64 as b64
import requests
import pytesseract
from PIL import Image

URL = "http://challenge01.root-me.org/programmation/ch8/"
fail_text1 = "Rat&eacute;, retente ta chance."
fail_text2 = "Failed, Try again."
splitstr1 = "png;base64,"
splitstr2 = "\" /><br><br>"
solstr1 = "le flag est "
solstr2 = "\n</p></p><br/></body></html>"
imagefile = "image.png"
alphabet = "abcdefghijklmnopqrstuvwxyzABCDEFGHIJKLMNOPQRSTUVWXYZ0123456789"

session = requests.Session()

while True:
    x = session.get(URL)
    imageb64 = x.text.split(splitstr1)[1].split(splitstr2)[0]
    imagebin = b64.b64decode(imageb64)
    image_bytes = bytearray(imagebin)
    
    f = open(imagefile,"w+b")
    f.write(image_bytes)
    f.close()
    
    img = Image.open(imagefile)
    captcha = pytesseract.image_to_string(img)
    
    captcha_text = ""
    for i in range(len(captcha)):
        if captcha[i]in alphabet:
            captcha_text += captcha[i]
    
    payload = {"cametu": captcha_text,}
    x = session.post(URL,data=payload)
    
    if fail_text1 in x.text or fail_text2 in x.text:
        print("pytesseract has failed to solve CAPTCHA: {}".format(captcha_text))         
    else:
        print("Solved!! pytesseract has solved CAPTCHA: {}".format(captcha_text))
        soln = x.text.split(solstr1)[1].split(solstr2)[0]
        print("Flag = {}".format(soln))
        break
~~~

Returns the flag.

</details>

### Answer

<details>

<summary markdown="span">Answer</summary>

~~~
dtePZJgVAfaU
~~~

</details>

---

### [Programming](#contents) | [Root-Me](./rootme.md) | [Home](./index.md)

---


## Arithmetic Progression

- Author: Baco
- Date: 04 February 2011
- Points: 20
- Level: 2

### Statement

You have 2 seconds to send the result of an arithmetic progression back.  Who said impossible?

### Links

1. [challenge site](http://challenge01.root-me.org/programmation/ch1/)

### Solutions

<details>

<summary markdown="span">Solution 1</summary>

Visiting the website we can see a html formatted arithmetic equation we have to solve:

~~~html
<html>

<body>
    <link rel='stylesheet' property='stylesheet' id='s' type='text/css' href='/template/s.css' media='all' /><iframe id='iframe' src='https://www.root-me.org/?page=externe_header'></iframe>U<sub>n+1</sub> = [ 45 + U<sub>n</sub> ] + [ n * 45 ]<br /> U
    <sub>0</sub> = -569
    <br />You must find U<sub>746358</sub><br /><br />You have only 2 seconds to send the result with the HTTP GET method (at http://challenge01.root-me.org/programmation/ch1/ep1_v.php?result=...)</body>

</html>
~~~

We can isolate the arithmetic equation from a requests response and submit the answer with the associated cookie using Python:

~~~py
import requests as req

Q_URL = "http://challenge01.root-me.org/programmation/ch1/"
A_URL = "http://challenge01.root-me.org/programmation/ch1/ep1_v.php?result="

response = req.get(Q_URL)
cookie = response.cookies
response = response.text
response = response.split("iframe>")[1].split("<br /><br />")[0]

N0 = int(response.split("<sub>0</sub> = ")[1].split("<br />")[0])
X = int(response.split("<sub>")[-1].split("</sub>")[0])
A = int(response.split(" = [ ")[1].split(" ")[0])
B = int(response.split("n * ")[1].split(" ")[0])

U = N0
for i in range(X):
    U = (A+U)+(i*B)

print(U)

response = req.get(A_URL+str(U), cookies=cookie).text
print(response)
~~~

Returns the flag.

</details>

### Answer

<details>

<summary markdown="span">Answer</summary>

~~~
lFablYE9P1
~~~

</details>

---

### [Programming](#contents) | [Root-Me](./rootme.md) | [Home](./index.md)

---


## Various Encodings

- Author: BlackRaven, Ruulian
- Date: 12 August 2021
- Points: 30
- Level: 3

### Statement

This service sends you encoded messages. Decode them all to get the flag!

### Connection Information

- Host: challenge01.root-me.org
- Protocol: TCP
- Port: 52017

### Solutions

<details>

<summary markdown="span">Solution 1</summary>

This is a simple decoding exercise that can be solved with a few helpful python libraries:

~~~py
#!/usr/bin/env python3
# -*- coding: utf-8 -*-
"""
Created on Sun Jan 30 13:21:06 2022

@author: derek
"""
import socket
import base64 as b64
import binascii

URL = "challenge01.root-me.org"
PORT = 52017
MORSE={"A" : ".-","B" : "-...","C" : "-.-.","D" : "-..","E" : ".","F" : "..-.","G" : "--.","H" : "....","I" : "..","J" : ".---","K" : "-.-","L" : ".-..","M" : "--","N" : "-.","O" : "---","P" : ".--.","Q" : "--.-","R" : ".-.","S" : "...","T" : "-","U" : "..-","V" : "...-","W" : ".--","X" : "-..-","Y" : "-.--","Z" : "--.."}
invMORSE = dict((v,k) for (k,v) in MORSE.items())

def dataString(data):
    ds = data.decode()
    ds = ds.split("please: '")[1]
    ds = ds.split("'\n")[0]
    return ds

def morsetoascii(datastring):
    morsearr = datastring.split("/")
    asciitext = ""
    for unit in morsearr:
        asciitext += invMORSE.get(unit)
    return asciitext.lower()

def decodeData(datastring):
    print("decoding {}".format(datastring))
    try:
        asciistr = b64.b64decode(datastring).decode()
        print("base64 encoding found!")
        print("ASCII = {}".format(asciistr))
        return asciistr.lower()
    except:
        print("not base64")
        pass
    try:
        asciistr = binascii.unhexlify(datastring.encode()).decode()
        print("hexadecimal encoding found!")
        print("ASCII = {}".format(asciistr))
        return asciistr
    except:
        print("not hexadecimal")
        pass
    try:
        asciistr = morsetoascii(datastring)
        print("Morse Code found!")
        print("ASCII = {}".format(asciistr))
        return asciistr
    except:
        print("not Morse")
        pass
    try:
        asciistr = b64.b32decode(datastring).decode()
        print("base32 encoding found!")
        print("ASCII = {}".format(asciistr))
        return asciistr
    except:
        print("not base32")
        pass
    try:
        asciistr = b64.b16decode(datastring).decode()
        print("base16 encoding found!")
        print("ASCII = {}".format(asciistr))
        return asciistr
    except:
        print("not base16")
        pass
    try:
        asciistr = b64.a85decode(datastring).decode()
        print("ASCII85 encoding found!")
        print("ASCII = {}".format(asciistr))
        return asciistr
    except:
        print("not ASCII85")
        pass
    try:
        asciistr = b64.b32hexdecode(datastring).decode()
        print("Base32 Hexadecimal encoding found!")
        print("ASCII = {}".format(asciistr))
        return asciistr
    except:
        print("not Base 32 Hexadecimal")
        pass
    try:
        asciistr = b64.b85decode(datastring).decode()
        print("Base85 encoding found!")
        print("ASCII = {}".format(asciistr))
        return asciistr
    except:
        print("not Base 85")
        pass
    return 0

s = socket.socket(socket.AF_INET,socket.SOCK_STREAM)
s.connect((URL,PORT))

while True:
    data = s.recv(1024)
    print(data.decode())
    if "flag" in data.decode():
        break
    ds = dataString(data)
    asciistr = decodeData(ds)
    if asciistr==0:
        print("No solution found")
        break
    s.send(asciistr.encode()+b"\n")
s.close()
~~~

</details>

### Answer

<details>

<summary markdown="span">Answer</summary>

~~~
D3c0d1ng_1s_R34LLY_h4rd_f0r_hum4ns!!!
~~~

</details>

---

### [Programming](#contents) | [Root-Me](./rootme.md) | [Home](./index.md)

---

Last updated Jan 2022.

## [djm89uk.github.io](https://djm89uk.github.io)
