# [Root-Me](./rootme.md) Root-Me Steganography [9/23]

The art of hiding information in a document. 

## Contents

1. [Gunnm](#gunnm) 🗸
2. [Squared](#squared) 🗸
3. [Dot and next line](#dot-and-next-line) 🗸
4. [Steganomobile](#steganomobile) 🗸
5. [Twitter Secret Messages](#twitter-secret-messages) 🗸
6. [Some noise](#some-noise) 🗸
7. [George and Alfred](#george-and-alfred) 🗸
8. [Poem from Space](#poem-from-space) 🗸
9. [Yellow dots](#yellow-dots) 🗸
10. [Audio stegano](#audio-stegano)
11. [Mimic - Dummy sight](#mimic-dummy-sight)
12. [We need to go deeper](#we-need-to-go-deeper)
13. [APNG - Just A PNG](#apng-just-a-png)
14. [Base Jumper](#base-jumper)
15. [ELF x64 - Duality](#elf-x64-duality)
16. [Hide and seek](#hide-and-seek)
17. [PDF Object](#pdf-object)
18. [Angecryption](#angecryption)
19. [Kitty spy](#kitty-spy)
20. [LSB - Uncle Scrooge](#lsb-uncle-scrooge)
21. [Pixel Indicator Technique](#pixel-indicator-technique)
22. [Pixel Value Differencing](#pixel-value-differencing)
23. [Crypt-art](#crypt-art)

---

### [Steganography](#contents) | [Root-Me](./rootme.md) | [Home](./index.md)

---

## Gunnm

- Author: g0uZ
- Date: 07 October 2006
- Points: 5
- Level: 1

### Statement

For the beginning : an image

### Attachments

1. [ch1.png](http://challenge01.root-me.org/steganographie/ch1/ch1.png)

### Solutions

<details>

<summary markdown="span">Solution 1</summary>

This challenge is a struggle, none of the file contents appear to yield the password.  There is nothing extractable using steganography tools. However, if you zoom in to the top right corner, you can make out a partially-visible password.

</details>

### Answer

<details>

<summary markdown="span">Answer</summary>

~~~
TOTORO
~~~

</details>

---

### [Steganography](#contents) | [Root-Me](./rootme.md) | [Home](./index.md)

---

## Squared

- Author: g0uZ
- Date: 07 October 2006
- Points: 5
- Level: 1

### Statement

None.

### Attachments

1. [ch2.jpg](http://challenge01.root-me.org/steganographie/ch2/ch2.jpg).

### Solutions

<details>

<summary markdown="span">Solution 1</summary>

Using strings we can retrieve the password from the image binary:
 
~~~shell
$ strings ch2.jpg | grep PASS
PASS=HAHAHA
~~~

</details>

### Answer

<details>

<summary markdown="span">Answer</summary>

~~~
HAHAHA
~~~

</details>

---

### [Steganography](#contents) | [Root-Me](./rootme.md) | [Home](./index.md)

---

## Dot and next line

- Author: SQalp
- Date: 16 June 2013
- Points: 10
- Level: 1

### Statement

“Rien de trop est un point dont on parle sans cesse et qu’on n’observe point.”

Jean de La Fontaine

### Attachments

1. [ch5.zip](http://challenge01.root-me.org/steganographie/ch5/ch5.zip).

### Solutions

<details>

<summary markdown="span">Solution 1</summary>

Translating the statement, we have a quote from 17th century French poet, [Jean de La Fontaine](https://en.wikipedia.org/wiki/Jean_de_La_Fontaine): Nothing too much is a point that we talk about all the time and do not observe.
  
We can retrieve the file using wget:

~~~shell
$ wget http://challenge01.root-me.org/steganographie/ch5/ch5.zip
--2022-01-07 14:25:38--  http://challenge01.root-me.org/steganographie/ch5/ch5.zip
Resolving challenge01.root-me.org (challenge01.root-me.org)... 212.129.38.224, 2001:bc8:35b0:c166::151
Connecting to challenge01.root-me.org (challenge01.root-me.org)|212.129.38.224|:80... connected.
HTTP request sent, awaiting response... 200 OK
Length: 52241 (51K) [application/zip]
Saving to: ‘ch5.zip’

ch5.zip                                                     100%[=========================================================================================================================================>]  51.02K  --.-KB/s    in 0.06s   

2022-01-07 14:25:38 (841 KB/s) - ‘ch5.zip’ saved [52241/52241]
~~~

Decompressing the archive, we find a jpg, journal.jpg:
  
~~~shell
$ unzip ch5.zip 
Archive:  ch5.zip
  inflating: journal.jpg       
~~~

Again, no luck with steganography tools or the binary itself.  Inspecting the image we see several sentences.  After a few attempts the flag can be retrieved by the letter corresponding to the line location above each period.

</details>

### Answer

<details>

<summary markdown="span">Answer</summary>

~~~
chatelet15h
~~~

</details>

---

### [Steganography](#contents) | [Root-Me](./rootme.md) | [Home](./index.md)

---

## Steganomobile

- Author: Ryscrow
- Date: 29 April 2011
- Points: 10
- Level: 1

### Statement

After extraction of mobile data, the searcher, investigator have get this sequence of numbers. Maybe a phone number?

### Attachments

1. [ch6.txt](http://challenge01.root-me.org/steganographie/ch6/ch6.txt).

### Solutions

<details>

<summary markdown="span">Solution 1</summary>

We are given a text file:

~~~
222-33-555-555-7-44-666-66-33
~~~

Each group has identical integers, perhaps a simple code?  We can try subsitution ciphers and get nonsense out.  This is due to the lack of data we have.  We can try a much simpler scheme.  Using two dictionaries, we can shift through the alphabet to identify possible solutions:

~~~py
ans_int = [222,33,555,555,7,44,666,66,33]

dic1 = [1,2,3,4,5,6,7,8,9,11,22,33,44,55,66,77,88,99,111,222,333,444,555,666,777,888,999]
dic2 = [1,11,111,2,22,222,3,33,333,4,44,444,5,55,555,6,66,666,7,77,777,8,88,888,9,99,999]
alphabet = "abcdefghijklmnopqrstuvwxyz"

for i in range(26):
    pass1 = ""
    pass2 = ""
    for letter in ans_int:
        pos1 = dic1.index(letter)
        pos2 = dic2.index(letter)
        pass1 += alphabet[pos1]
        pass2 += alphabet[pos2]
    print("Password {}.1 attempt: {}".format(i,pass1))
    print("password {}.2 attempt: {}".format(i,pass2))
    alphabet = alphabet[-1]+alphabet[:-1]
~~~

This returns 50 possible answers:

~~~
Password 0.1 attempt: tlwwgmxol
password 0.2 attempt: fhooskrqh
Password 1.1 attempt: skvvflwnk
password 1.2 attempt: egnnrjqpg
Password 2.1 attempt: rjuuekvmj
password 2.2 attempt: dfmmqipof
Password 3.1 attempt: qittdjuli
password 3.2 attempt: cellphone
Password 4.1 attempt: phsscitkh
password 4.2 attempt: bdkkognmd
Password 5.1 attempt: ogrrbhsjg
password 5.2 attempt: acjjnfmlc
Password 6.1 attempt: nfqqagrif
password 6.2 attempt: zbiimelkb
Password 7.1 attempt: meppzfqhe
password 7.2 attempt: yahhldkja
Password 8.1 attempt: ldooyepgd
password 8.2 attempt: xzggkcjiz
Password 9.1 attempt: kcnnxdofc
password 9.2 attempt: wyffjbihy
Password 10.1 attempt: jbmmwcneb
password 10.2 attempt: vxeeiahgx
Password 11.1 attempt: iallvbmda
password 11.2 attempt: uwddhzgfw
Password 12.1 attempt: hzkkualcz
password 12.2 attempt: tvccgyfev
Password 13.1 attempt: gyjjtzkby
password 13.2 attempt: subbfxedu
Password 14.1 attempt: fxiisyjax
password 14.2 attempt: rtaaewdct
Password 15.1 attempt: ewhhrxizw
password 15.2 attempt: qszzdvcbs
Password 16.1 attempt: dvggqwhyv
password 16.2 attempt: pryycubar
Password 17.1 attempt: cuffpvgxu
password 17.2 attempt: oqxxbtazq
Password 18.1 attempt: bteeoufwt
password 18.2 attempt: npwwaszyp
Password 19.1 attempt: asddntevs
password 19.2 attempt: movvzryxo
Password 20.1 attempt: zrccmsdur
password 20.2 attempt: lnuuyqxwn
Password 21.1 attempt: yqbblrctq
password 21.2 attempt: kmttxpwvm
Password 22.1 attempt: xpaakqbsp
password 22.2 attempt: jlsswovul
Password 23.1 attempt: wozzjparo
password 23.2 attempt: ikrrvnutk
Password 24.1 attempt: vnyyiozqn
password 24.2 attempt: hjqqumtsj
Password 25.1 attempt: umxxhnypm
password 25.2 attempt: gipptlsri
~~~ 

We can see there is 1 answer that produces an english word, cellphone.

</details>

### Answer

<details>

<summary markdown="span">Answer</summary>

~~~
cellphone
~~~

</details>

---

### [Steganography](#contents) | [Root-Me](./rootme.md) | [Home](./index.md)

---

## Twitter Secret Messages

- Author: xblade,
- Date: 21 December 2016
- Points: 10
- Level: 1

### Statement

We suspect that this tweet hides a rendezvous point. Help us to find it.

~~~
Ｃhｏose  a  jοｂ  yоu lονｅ,  and  you  ｗіｌl  ｎeｖｅｒ  have tο ｗｏrk  a  day  in  yοur lіfｅ．      
~~~                 

The validation password is the meeting place (in lower case).


### Attachments

1. [ch6.txt](http://challenge01.root-me.org/steganographie/ch6/ch6.txt).

### Solutions

<details>

<summary markdown="span">Solution 1</summary>

We can use a twitter steganography tool, [holloway.nz](https://holloway.nz/steg/) which provides the hidden message: "rendezvous at grand central terminal on friday.   b/j.  "

</details>

### Answer

<details>

<summary markdown="span">Answer</summary>

~~~
grand central terminal
~~~

</details>

---

### [Steganography](#contents) | [Root-Me](./rootme.md) | [Home](./index.md)

---

## Some noise

- Author: Hackira
- Date: 7 October 2006
- Points: 15
- Level: 2

### Statement

The password has to be given in lowercase.

### Resources

1. [watch?v=J0nUaCyj1G8](https://www.youtube.com/watch?v=J0nUaCyj1G8)

### Attachments

1. [ch3.wav](http://challenge01.root-me.org/steganographie/ch3/ch3.wav).

### Solutions

<details>

<summary markdown="span">Solution 1</summary>

We can retrieve the wav file using wget:

~~~shell
$ wget http://challenge01.root-me.org/steganographie/ch3/ch3.wav
~~~

Playing the file, we get a condensed audio which is not understandable.  We can play the audio with a lower sample rate using ffmpeg:

~~~shell
$ ffplay -af "asetrate=12000" ch3.wav
~~~

Listening to this, we can hear the audio is reversed.  We can reverse the wav file using ffmpeg:

~~~shell
$ ffmpeg -i ch3.wav -af areverse ch3_reversed.wav
~~~

Now we can listen to the reversed file at the lower sample rate:

~~~shell
$ ffplay -af "asetrate=12000,aformat=channel_layouts=2" ch3_reversed.wav
~~~

This gives us the password.

</details>

### Answer

<details>

<summary markdown="span">Answer</summary>

~~~
3b27641fc5h0
~~~

</details>

---

### [Steganography](#contents) | [Root-Me](./rootme.md) | [Home](./index.md)

---

## George and Alfred

- Author: g0uZ
- Date: 20 December 2014
- Points: 15
- Level: 2

### Statement

This challenge is only available in french language due to it specificity.

### Attachments

1. [ch4.txt](http://challenge01.root-me.org/steganographie/ch4/ch4.txt).

### Solutions

<details>

<summary markdown="span">Solution 1</summary>

We are given the text file with contents:

~~~
Je suis très émue de vous dire que j'ai
bien compris, l'autre jour, que vous avez
toujours une envie folle de me faire
danser. Je garde un souvenir de votre
baiser et je voudrais que ce soit
là une preuve que je puisse être aimée
par vous. Je suis prête à vous montrer mon
Affection toute désintéressée et sans cal-
cul. Si vous voulez me voir ainsi
dévoiler, sans aucun artifice mon âme
toute nue, daignez donc me faire une visite
Et nous causerons en amis et en chemin.
Je vous prouverai que je suis la femme
sincère capable de vous offrir l'affection
la plus profonde et la plus étroite
Amitié, en un mot, la meilleure amie
que vous puissiez rêver. Puisque votre
âme est libre, alors que l'abandon où je
vis est bien long, bien dur et bien souvent
pénible, ami très cher, j'ai le coeur
gros, accourez vite et venez me le
fait oublier. À l'amour, je veux me sou-
mettre. 

Alfred de Musset a répondu ceci :

Quand je vous jure, hélàs, un éternel hommage
Voulez-vous qu'un instant je change de language
Que ne puis-je, avec vous, goûter le vrai bonheur
Je vous aime, ô ma belle, et ma plume en délire
Couche sur le papier ce que je n'ose dire
Avec soin, de mes vers, lisez le premier mot
Vous saurez quel remède apporter à mes maux.


De la même manière George Sand a répondu ceci :

Cette grande faveur que votre ardeur réclame
Nuit peut-être à l'honneur mais répond à ma flamme.

Utilisez la dernière "phrase cachée", pour valider cette épreuve.
~~~

This can be translated:

~~~
I am very moved to tell you that I have well understood, the other day, that you have always a crazy desire to make me dance. I keep a memory of your fuck and I wish it was there is a proof that I can be loved by you. I am ready to show you my Affection all disinterested and without calculation. If you want to see me like this to reveal, without any artifice, my soul naked, so deign to visit me And we will talk as friends and on the way. I will prove to you that I am the woman sincere able to offer you affection the deepest and narrowest Friendship, in a word, the best friend that you can dream. Since your soul is free, while abandonment where I screw is very long, very hard and very often painful, dear friend, I have the heart big, run fast and come to me makes us forget. To love, I want to submit.

Alfred de Musset replied: 

When I swear to you, alas, an eternal tribute Do you want me to change my language for a moment What can I, with you, taste true happiness I love you, O my beautiful, and my pen in delirium Put on paper what I dare not say Carefully, from my verses, read the first word You will know what remedy to bring to my ailments. 

In the same way George Sand replied this: 

This great favor that your ardor demands Night maybe in the spotlight but responds to my flame. 

Use the last "hidden sentence" to validate this test.
~~~

We can read every other line of the first paragraph, and the first word of each line in the second paragraph:

~~~
Je suis très émue de vous dire que j'ai
toujours une envie folle de me faire
baiser et je voudrais que ce soit
par vous. Je suis prête à vous montrer mon
cul. Si vous voulez me voir ainsi
toute nue, daignez donc me faire une visite
Je vous prouverai que je suis la femme
la plus profonde et la plus étroite
que vous puissiez rêver. Puisque votre
vis est bien long, bien dur et bien souvent
gros, accourez vite et venez me le
mettre. 

Alfred de Musset a répondu ceci :

Quand 
Voulez-vous 
Que 
Je 
Couche 
Avec 
Vous 


De la même manière George Sand a répondu ceci :

Cette 
Nuit 
~~~

This can be translated to a rathe leud conversation:

~~~
I am very moved to tell you that I have always a crazy desire to make me fuck and I wish it was by you. I am ready to show you my arse. If you want to see me like this naked, so deign to visit me I will prove to you that I am the woman the deepest and narrowest that you can dream. Since your screw is very long, very hard and very often big, run fast and come to me put. 

Alfred de Musset replied: When Do you want That I Layer With You In the same way 

George Sand replied this: This Night
~~~

The answer is This Night, in french: Cette Nuit

</details>

### Answer

<details>

<summary markdown="span">Answer</summary>

~~~
Cette Nuit
~~~

</details>

---

### [Steganography](#contents) | [Root-Me](./rootme.md) | [Home](./index.md)

---

## Poem From Space

- Author: Cryptanalyse
- Date: 15 July 2020
- Points: 15
- Level: 2

### Statement

Deeply understand the meaning of this famous poem to validate this challenge.

### Attachments

1. [ch19.txt](http://challenge01.oot-me.org/steganographie/ch19/ch19.txt).

### Solutions

<details>

<summary markdown="span">Solution 1</summary>

We are given a poem:

~~~
The Charge of the Light Brigade    	 	  	 
Lord Alfred Tennyson 
1854 	
      			 	
Half a league, half a league,	    
Half a league onward, 	
All in the valley of Death       
Rode the six hundred.	    
"Forward, the Light Brigade! 	
Charge for the guns!" he said:      	 	
Into the valley of Death	    
Rode the six hundred. 	
"Forward, the Light Brigade!"      	  			
Was there a man dismayed?	  	 
Not though the soldier knew 	
Some one had blundered:      		   
Their's not to make reply,	    
Their's not to reason why, 	
Their's but to do and die:      	 		 
Into the valley of Death	    
Rode the six hundred. 	
      	  	  
Cannon to right of them,	  	 
Cannon to left of them, 	
Cannon in front of them      	   	
Volleyed and thundered;	    
Stormed at with shot and shell, 	
Boldly they rode and well,      		 			
Into the jaws of Death,	  	 
Into the mouth of Hell 	
Rode the six hundred.      	    		
	    
Flashed all their sabres bare, 	
Flashed as they turned in air      	     	
Sabring the gunners there,	  	 
Charging an army, while 	
All the world wondered:      	 		  
Plunged in the battery-smoke	    
Right through the line they broke; 	
Cossack and Russian      		  
Reeled from the sabre-stroke	  	 
Shattered and sundered. 	
Then they rode back, but not,      			 	
Not the six hundred.	    
 	
Cannon to right of them,      				  
Cannon to left of them,	  	 
Cannon behind them 	
Volleyed and thundered;      	 				
Stormed at with shot and shell,	    
While horse and hero fell, 	
They that had fought so well      		    
Came through the jaws of Death	  	 
Back from the mouth of Hell, 	
All that was left of them,      	  	 	 
Left of six hundred.	    
 	
When can their glory fade?      			  		
O the wild charge they made!	  	 
All the world wondered. 	
Honour the charge they made!  
Honour the Light Brigade,
Noble six hundred!
~~~

Using the whitespace online compiler at [Try it online](https://tio.run/#whitespace) we can take the trailing whitespace characters and get the password.

</details>

### Answer

<details>

<summary markdown="span">Answer</summary>

~~~
RootMe{Wh1t3_Sp4c3}
~~~

</details>

---

### [Steganography](#contents) | [Root-Me](./rootme.md) | [Home](./index.md)

---

## Yellow Dots

- Author: LetMeR00t
- Date: 29 September 2019
- Points: 15
- Level: 2

### Statement

You attend an interview for a forensic investigator job and they give you a challenge to solve as quickly as possible (having the Internet).
They ask you to find the date of printing as well as the serial number of the printer in this document.
You remain dubitative and accept the challenge.

The answer is in the form:
hh:mm dd/mm/yyyy SSSSSSSS
with
 hh: the hour of the event
 mm: the minutes of the event
 dd: the day of the event
 MM: the month of the event
 yyyy: the year of the event
 SSSSSSSS: the serial number

### Resources

1. [Yellow Dots of Mystery](https://repository.root-me.org/St%C3%A9ganographie/EN%20-%20Yellow%20Dots%20of%20Mystery%20-%20Is%20Your%20Printer%20Spying%20on%20You%20-%20Instructables.pdf).

### Attachments

1. [ch18.png](http://challenge01.root-me.org/steganographie/ch18/ch18.png).

### Solutions

<details>

<summary markdown="span">Solution 1</summary>

Following the guide, we can find the dots on the page on the right.  Using this [decoding guide from EFF.org](https://www.eff.org/files/filenode/printers/ccc.pdf) we can identify it is a Xerox style encoding which can be read:

~~~
    RP |  time   | date  | UNK | SEP | Serial  | UNK 
     1 | 1 2 3 4 | 1 2 3 |  1  |  1  | 1 2 3 4 |  1 
    ------------------------------------------------
CP | 1   0 1 1 1   0 1 1    1     0    1 0 1 0    1
64 | 1   0 0 0 0   0 0 0    0     0    0 0 1 0    0
32 | 1   0 0 0 0   0 0 0    0     0    0 0 0 0    0
16 | 1   0 0 0 0   1 0 0    0     0    1 1 1 0    0
 8 | 0   0 0 0 1   1 0 1    0     0    1 1 1 0    0
 4 | 0   1 0 0 0   0 1 1    0     0    1 1 1 1    0
 2 | 0   0 0 0 1   1 1 1    0     0    1 0 0 1    0
 1 | 1   1 0 0 1   1 1 0    0     0    0 1 0 0    0

time:
    1 = 5
    2 = 0
    3 = 0
    4 = 11
date:
    1 = 27
    2 = 7
    3 = 14
UNK:
    1 = 0
SEP:
    1 = 0
Serial:
    1 = 30
    2 = 29
    3 = 92
    4 = 6

Date = 27/7/2014
Serial = 6922930
Time = 11:05

password = 11:05 27/07/2014 06922930
~~~

</details>

### Answer

<details>

<summary markdown="span">Answer</summary>

~~~
11:05 27/07/2014 06922930
~~~

</details>

---

### [Steganography](#contents) | [Root-Me](./rootme.md) | [Home](./index.md)

---

Last updated Jan 2022.

## [djm89uk.github.io](https://djm89uk.github.io)
