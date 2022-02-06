# [Root-Me](./rootme.md) Root-Me Steganography [13/23]

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
10. [Audio stegano](#audio-stegano) 🗸
11. [Mimic - Dummy sight](#mimic-dummy-sight)
12. [We need to go deeper](#we-need-to-go-deeper) 🗸
13. [APNG - Just A PNG](#apng-just-a-png) 🗸
14. [Base Jumper](#base-jumper) 🗸
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
Choose a job you love, and you will never have to work a day in your life.
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

## Some Noise

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

## Audio Stegano

- Author: stickmen
- Date: 2 October 2011
- Points: 20
- Level: 2

### Statement

Interesting mix.

### Attachments

1. [ch7.wav](http://challenge01.root-me.org/steganographie/ch7/ch7.wav).

### Solutions

<details>

<summary markdown="span">Solution 1</summary>

We can download and play this wav file with ffmpeg.  This displays a waterfall frequency plot of the audio file as it is played.  We can see the password in this plot:

~~~shell
$ ffplay ch7.wav
ffplay version 4.2.4-1ubuntu0.1 Copyright (c) 2003-2020 the FFmpeg developers
  built with gcc 9 (Ubuntu 9.3.0-10ubuntu2)
  configuration: --prefix=/usr --extra-version=1ubuntu0.1 --toolchain=hardened --libdir=/usr/lib/x86_64-linux-gnu --incdir=/usr/include/x86_64-linux-gnu --arch=amd64 --enable-gpl --disable-stripping --enable-avresample --disable-filter=resample --enable-avisynth --enable-gnutls --enable-ladspa --enable-libaom --enable-libass --enable-libbluray --enable-libbs2b --enable-libcaca --enable-libcdio --enable-libcodec2 --enable-libflite --enable-libfontconfig --enable-libfreetype --enable-libfribidi --enable-libgme --enable-libgsm --enable-libjack --enable-libmp3lame --enable-libmysofa --enable-libopenjpeg --enable-libopenmpt --enable-libopus --enable-libpulse --enable-librsvg --enable-librubberband --enable-libshine --enable-libsnappy --enable-libsoxr --enable-libspeex --enable-libssh --enable-libtheora --enable-libtwolame --enable-libvidstab --enable-libvorbis --enable-libvpx --enable-libwavpack --enable-libwebp --enable-libx265 --enable-libxml2 --enable-libxvid --enable-libzmq --enable-libzvbi --enable-lv2 --enable-omx --enable-openal --enable-opencl --enable-opengl --enable-sdl2 --enable-libdc1394 --enable-libdrm --enable-libiec61883 --enable-nvenc --enable-chromaprint --enable-frei0r --enable-libx264 --enable-shared
  libavutil      56. 31.100 / 56. 31.100
  libavcodec     58. 54.100 / 58. 54.100
  libavformat    58. 29.100 / 58. 29.100
  libavdevice    58.  8.100 / 58.  8.100
  libavfilter     7. 57.100 /  7. 57.100
  libavresample   4.  0.  0 /  4.  0.  0
  libswscale      5.  5.100 /  5.  5.100
  libswresample   3.  5.100 /  3.  5.100
  libpostproc    55.  5.100 / 55.  5.100
Input #0, wav, from 'ch7.wav':=    0KB vq=    0KB sq=    0B f=0/0   
  Duration: 00:00:04.99, bitrate: 705 kb/s
    Stream #0:0: Audio: pcm_s16le ([1][0][0][0] / 0x0001), 22050 Hz, 2 channels, s16, 705 kb/s
^Z32.08 M-A:  0.000 fd=   0 aq=    0KB vq=    0KB sq=    0B f=0/0   
[3]+  Stopped                 ffplay ch7.wav
~~~

</details>

### Answer

<details>

<summary markdown="span">Answer</summary>

~~~
secret-password
~~~

</details>

---

### [Steganography](#contents) | [Root-Me](./rootme.md) | [Home](./index.md)

---

## We need to go deeper

- Author: whoami
- Date: 12 August 2015
- Points: 20
- Level: 2

### Statement

Thumbnails 😉

### Attachments

1. [ch10.jpg](http://challenge01.root-me.org/steganographie/ch10/ch10.jpg).

### Solutions

<details>

<summary markdown="span">Solution 1</summary>

The challenge jpg can be downloaded.  Using strings we do not find anything other than "We need to go deeper":

~~~shell
$ strings ch10.jpg | uniq | sort
...
We need to go deeper
...
yoyoyoyoyoyioyoyoyoyoyoyl
~~~

Looking at the file we can see the file is a jpeg and it is 126KB in size:

~~~shell
$ file ch10.jpg 
ch10.jpg: JPEG image data, JFIF standard 1.01, resolution (DPI), density 96x96, segment length 16, Exif Standard: [TIFF image data, big-endian, direntries=4, xresolution=62, yresolution=70, resolutionunit=2], progressive, precision 8, 1360x716, components 3
$ ls -lh ch10.jpg 
-rw-rw-r-- 1 user user 126K Jan 31 20:59 ch10.jpg

~~~

Inspecting the image with exiftool we see a large image size (0.974 Megapixels):

~~~shell
$ exiftool ch10.jpg 
ExifTool Version Number         : 11.88
File Name                       : ch10.jpg
Directory                       : .
File Size                       : 126 kB
File Modification Date/Time     : 2022:01:31 20:59:01+00:00
File Access Date/Time           : 2022:01:31 20:59:01+00:00
File Inode Change Date/Time     : 2022:01:31 20:59:01+00:00
File Permissions                : rw-rw-r--
File Type                       : JPEG
File Type Extension             : jpg
MIME Type                       : image/jpeg
JFIF Version                    : 1.01
Exif Byte Order                 : Big-endian (Motorola, MM)
X Resolution                    : 96
Y Resolution                    : 96
Resolution Unit                 : inches
Y Cb Cr Positioning             : Centered
Compression                     : JPEG (old-style)
Thumbnail Offset                : 202
Thumbnail Length                : 41506
Image Width                     : 1360
Image Height                    : 716
Encoding Process                : Progressive DCT, Huffman coding
Bits Per Sample                 : 8
Color Components                : 3
Y Cb Cr Sub Sampling            : YCbCr4:4:4 (1 1)
Image Size                      : 1360x716
Megapixels                      : 0.974
Thumbnail Image                 : (Binary data 41506 bytes, use -b option to extract)
~~~

This does not reflect the file size.  We can investigate with binwalk:

~~~shell
$ binwalk ch10.jpg 

DECIMAL       HEXADECIMAL     DESCRIPTION
--------------------------------------------------------------------------------
0             0x0             JPEG image data, JFIF standard 1.01
30            0x1E            TIFF image data, big-endian, offset of first image directory: 8
202           0xCA            JPEG image data, JFIF standard 1.01
232           0xE8            TIFF image data, big-endian, offset of first image directory: 8
404           0x194           JPEG image data, JFIF standard 1.01
~~~

We appear to have multiple images within the file!  We can extract these with binwalk:

~~~shell
$ binwalk --dd='.*' ch10.jpg 

DECIMAL       HEXADECIMAL     DESCRIPTION
--------------------------------------------------------------------------------
0             0x0             JPEG image data, JFIF standard 1.01
30            0x1E            TIFF image data, big-endian, offset of first image directory: 8
202           0xCA            JPEG image data, JFIF standard 1.01
232           0xE8            TIFF image data, big-endian, offset of first image directory: 8
404           0x194           JPEG image data, JFIF standard 1.01
~~~

Opening the last jpg (194) we find the flag.

</details>

### Answer

<details>

<summary markdown="span">Answer</summary>

~~~
B33r1sG00d!
~~~

</details>

---

### [Steganography](#contents) | [Root-Me](./rootme.md) | [Home](./index.md)

---


## APNG Just A PNG

- Author: exti0p, AnthoLaMalice
- Date: 22 November 2021
- Points: 25
- Level: 3

### Statement

Your joking colleague challenges you to find the message hidden in this animation.

### Attachments

1. [ch21.apng](http://challenge01.root-me.org/steganographie/ch21/ch21.apng).

### Related Resources

1. [APNG_Specification](https://wiki.mozilla.org/APNG_Specification).
2. [Animated_Portable_Network_Graphics](https://fr.wikipedia.org/wiki/Animated_Portable_Network_Graphics).

### Solutions

<details>

<summary markdown="span">Solution 1</summary>

Using apngdis, the animated png can be disassembled:

~~~shell
$ apngdis ch21.apng 

APNG Disassembler 2.9

Reading 'ch21.apng'...
extracting frame 1 of 13
extracting frame 2 of 13
extracting frame 3 of 13
extracting frame 4 of 13
extracting frame 5 of 13
extracting frame 6 of 13
extracting frame 7 of 13
extracting frame 8 of 13
extracting frame 9 of 13
extracting frame 10 of 13
extracting frame 11 of 13
extracting frame 12 of 13
extracting frame 13 of 13
all done
~~~

This returns 13 png files and 13 text files.  Each text file has a different delay value:

~~~shell
$ strings *.txt
delay=70/10
delay=76/10
delay=65/10
delay=71/10
delay=58/10
delay=80/10
delay=51/10
delay=80/10
delay=111/10
delay=70/10
delay=82/10
delay=111/10
delay=71/10
~~~

These values can be appended to an array in python:

~~~py
import os

txtarr = []
indx = []

for filename in os.listdir("./"):
    if ".txt" in filename:
        indx.append(filename.split("frame")[1].split(".t")[0])
        f = open(filename)
        txtarr.append(f.read())

chrarr = []
for val in txtarr:
    chrarr.append(val.split("=")[1].split("/10")[0])

indx, chrarr = (list(t) for t in zip(*sorted(zip(indx, chrarr))))
~~~

These sorted values can be decoded into ascii:

~~~py
solution = ""
for val in chrarr:
    solution += chr(int(val))
    
print(solution)
~~~


</details>

### Answer

<details>

<summary markdown="span">Answer</summary>

~~~
P3PoFRoG
~~~

</details>

---

### [Steganography](#contents) | [Root-Me](./rootme.md) | [Home](./index.md)

---


## Base Jumper

- Author: pickle
- Date: 03 March 2018
- Points: 25
- Level: 3

### Statement

It seems steganography is all the rage with attackers exfiltrating data these days.
Look at this example I found, I think it has a flag inside.

### Attachments

1. [ch15.jpg](http://challenge01.root-me.org/steganographie/ch15/ch15.jpg).

### Solutions

<details>

<summary markdown="span">Solution 1</summary>

The challenge file can be collected and inspected:

~~~shell
$ wget http://challenge01.root-me.org/steganographie/ch15/ch15.jpg
--2022-02-06 08:49:03--  http://challenge01.root-me.org/steganographie/ch15/ch15.jpg
Resolving challenge01.root-me.org (challenge01.root-me.org)... 212.129.38.224, 2001:bc8:35b0:c166::151
Connecting to challenge01.root-me.org (challenge01.root-me.org)|212.129.38.224|:80... connected.
HTTP request sent, awaiting response... 200 OK
Length: 682367 (666K) [image/jpeg]
Saving to: ‘ch15.jpg’

ch15.jpg                                                    100%[=========================================================================================================================================>] 666.37K  --.-KB/s    in 0.1s    

2022-02-06 08:49:03 (4.53 MB/s) - ‘ch15.jpg’ saved [682367/682367]

$ file ch15.jpg 
ch15.jpg: JPEG image data, JFIF standard 1.01, resolution (DPI), density 300x300, segment length 16, Exif Standard: [TIFF image data, big-endian, direntries=11, manufacturer=NIKON CORPORATION, model=NIKON D5000, orientation=upper-left, xresolution=176, yresolution=184, resolutionunit=2, software=GIMP 2.8.16, datetime=2017:08:02 12:34:15, GPS-Data], comment: "CgoK", progressive, precision 8, 1024x680, components 3
~~~

Reviewing the metadata using exiftool we see excessive comments:

~~~shell
$ exiftool ch15.jpg 
ExifTool Version Number         : 11.88
File Name                       : ch15.jpg
Directory                       : .
File Size                       : 666 kB
File Modification Date/Time     : 2021:12:10 16:37:08+00:00
File Access Date/Time           : 2022:02:06 08:49:04+00:00
File Inode Change Date/Time     : 2022:02:06 08:49:03+00:00
File Permissions                : rw-rw-r--
File Type                       : JPEG
File Type Extension             : jpg
MIME Type                       : image/jpeg
JFIF Version                    : 1.01
Exif Byte Order                 : Big-endian (Motorola, MM)
Make                            : NIKON CORPORATION
Camera Model Name               : NIKON D5000
Orientation                     : Horizontal (normal)
X Resolution                    : 300
Y Resolution                    : 300
Resolution Unit                 : inches
Software                        : GIMP 2.8.16
Modify Date                     : 2017:08:02 12:34:15
Y Cb Cr Positioning             : Co-sited
Exposure Time                   : 1/2000
F Number                        : 8.0
Exposure Program                : Not Defined
ISO                             : 400
Exif Version                    : 0221
Date/Time Original              : 2012:05:18 10:03:28
Create Date                     : 2012:05:18 10:03:28
Components Configuration        : Y, Cb, Cr, -
Compressed Bits Per Pixel       : 4
Exposure Compensation           : 0
Max Aperture Value              : 3.5
Metering Mode                   : Multi-segment
Light Source                    : Unknown
Focal Length                    : 18.0 mm
User Comment                    : 
Sub Sec Time                    : 00
Sub Sec Time Original           : 00
Sub Sec Time Digitized          : 00
Flashpix Version                : 0100
Color Space                     : sRGB
Exif Image Width                : 1024
Exif Image Height               : 680
Interoperability Index          : R98 - DCF basic file (sRGB)
Interoperability Version        : 0100
Sensing Method                  : One-chip color area
File Source                     : Digital Camera
Scene Type                      : Directly photographed
CFA Pattern                     : [Green,Blue][Red,Green]
Custom Rendered                 : Normal
Exposure Mode                   : Auto
White Balance                   : Auto
Digital Zoom Ratio              : 1
Focal Length In 35mm Format     : 27 mm
Scene Capture Type              : Standard
Gain Control                    : Low gain up
Contrast                        : Normal
Saturation                      : Normal
Sharpness                       : Normal
Subject Distance Range          : Unknown
GPS Version ID                  : 2.2.0.0
Compression                     : JPEG (old-style)
Thumbnail Offset                : 1018
Thumbnail Length                : 8498
Comment                         : CgoK.CgoKTmV=.dHdv.cmsg.V29yax==.aW5n.IEdy.b3VwIJ==.ICAgIC==.ICC=.ICAg.ICAgIE==.ICAgIC==.ICAgIE==.ICAgIF==.ICAgICB=.ICAgUw==.LiBKb3P=.ZWZ=.c3Nvbl==.LCB=.RWQuClI=.ZXF1Zc==.c3QgZp==.b3Ig.Q29t.bWVudHM=.OiAz.NTQ4IG==.ICAgICB=.ICA=.ICAgICB=.ICAgICC=.ICAgIE==.ICC=.ICAg.ICB=.ICAgIF==.ICA=.ICBKdV==.bHkgMjA=.MDMKQ0==.YXRl.Z29y.eTo=.IEluZm/=.cm1h.dGlvbt==.YWwKCgo=.ICAg.ICD=.ICD=.ICAg.ICAgVGh=.ZSBCYXM=.ZTE2LP==.IEJ=.YXNlMz==.MiwgYW7=.ZCBCYXN=.ZTY0IA==.RGG=.dGEgRZ==.bmNv.ZGluZ3M=.CgpTdGF=.dHVzIG+=.ZiB0aGl=.cyBNZS==.bW+=.CgogIF==.IFRo.aXMgbW==.ZW1vIHB=.cm92aWQ=.ZXMgaY==.bmZvcm1=.YXQ=.aW9u.IGZvcr==.IHRoZT==.IElu.dGVybmU=.dCBjb23=.bXVu.aXR5Lk==.ICBJdM==.IGRvZV==.cwo=.ICAg.bm90.IHNwZV==.Y2lmeR==.IGG=.biB=.SW50.ZXI=.bmV0IHO=.dGFu.ZGFyZCC=.b2YgYW5=.eSBraW5=.ZC5=.ICBEaV==.c3RyaV==.YnX=.dGk=.b24g.b2Yg.dGhp.cwr=.ICAgbWV=.bW8gaXM=.IHVubGl=.bWl0ZWR=.LgoK.Q29w.eXJp.Z2h0IE6=.b3RpY5==.ZQoKICB=.IEO=.b3B5.cmln.aHQg.KEMp.IFRoZZ==.IElu.dGVy.bmU=.dCBT.b2Np.ZXR5ICj=.MjAw.MykuICB=.QWxsIA==.UmlnaK==.dHN=.IFJlc2U=.cnZlZC5=.CgpBYl==.c3Q=.cmFjdAo=.CiAg.IFRoaXO=.IGRvY1==.dW1lbh==.dCBk.ZXN=.Y3JpYl==.ZXMgdGj=.ZSBjb21=.bW9ubHl=.IHW=.c2V=.ZCA=.YmFz.ZSA2NCz=.IGJhc0==.ZSAzMj==.LCBhbmQ=.IGJhc2X=.CiAgIDF=.NiBlbmN=.b2Rp.bmcgc2M=.aGVt.ZXM=.LiAgSXR=.IGE=.bHNvIGR=.aXNj.dXNz.ZXMgdGh=.ZSB1c2V=.IG8=.ZiBsaS==.bmUtZl==.ZWVkc6==.IGluCl==.ICB=.IGVu.Y29kZc==.ZCBkYXT=.YSwgdW==.c2Ugbz==.ZiA=.cGFkZGn=.bmcgaU==.biBlbs==.Y29kZU==.ZCBkYW==.dGEsIE==.dXNlIP==.b2Yg.bm9=.bi1hbE==.cGhhYp==.ZXR=.CiAg.IGNoYXJ=.YWN=.dGVyc1==.IGl=.biBlbmP=.b2Rl.ZCBk.YXRhLD==.IGFuZCA=.dXNlIG+=.ZiB=.ZGl=.ZmZl.cmVudK==.IGVuY29=.ZGluZyA=.YWxw.aGG=.YmV0cy6=.Cgo=.VGFibGX=.IG9mIN==.Q29udA==.ZW50.cwq=.CiAgIDG=.LiAg.SW50ck==.b2R1Y/==.dGlvbk==.IC7=.IC4g.LiAuIF==.LiAuIE==.LiAuIF==.LiAuIC==.LiA=.LiB=.LiA=.LiD=.LiD=.LiAu.IC4=.IC4g.LiD=.LiB=.LiA=.LiAu.IC5=.ICB=.Mgog.ICAyLiB=.IEltcB==.bGU=.bWVu.dGF0aW+=.biBkaXO=.Y3JlcGF=.bmNpZT==.cyAuIN==.LiAu.IC4gLk==.IC6=.IC4=.IC4g.LiAuIM==.LiAuIJ==.LiAuIB==.LiAuIC7=.ICAyCk==.ICAgIL==.ICAgMi4=.MS4gIEz=.aW5lIGY=.ZWX=.ZHN=.IGl=.biBl.bmNv.ZGVk.IGRh.dGEgLiA=.LiC=.LiB=.LiAuIC4=.IC4gLh==.IC4gLiB=.LiAuIC4=.IC4g.LiAg.MgogIN==.ICAgICB=.Mi4=.Mi4gIG==.UGFkZGl=.bmcg.b2Yg.ZW5j.b2R=.ZWS=.IGS=.YXRhICB=.LiB=.LiA=.LiAuIC7=.IC5=.IC4=.IC4gLiA=.LiAuII==.LiAuIP==.LiB=.LiAuICA=.Mwog.ICAg.ICAgMi7=.My4g.IEludGX=.cnByZXR=.YXRp.b24=.IG/=.ZiD=.bm9=.bi1h.bHBoYQ==.YmV0IGO=.aGFyYWO=.dGVycyB=.aW4=.IGVuY29=.ZGW=.ZAog.ICAgIE==.ICC=.ICAg.ICAg.ZGF0.YSAu.IC4g.LiAuIC6=.IC4gLiB=.LiAu.IC4gLiA=.LiAu.IC4gLiA=.LiAuIC6=.IC4gLiB=.LiAuIA==.LiAuIM==.LiAu.ICAzCiD=.ICAgICB=.IDIu.NC4gIEM=.aG9=.b3N=.aW5nIHQ=.aGV=.IGF=.bHBoYWI=.ZXQgIC6=.IC4g.LiAu.IC4gLp==.IC4g.LiAuID==.LiD=.LiAuIC5=.IC4=.IC4gLr==.IC4gIE==.Mwr=.ICB=.IDMu.ICBCYV==.c2UgNjS=.IEVu.Y29k.aW5n.IC4gLiA=.LiAuIC5=.IC4g.LiAuIB==.LiAu.IC5=.IC4gLiB=.LiAu.IC4gLiA=.LiAuIC6=.IC4gLt==.IC4gIDQ=.CiAgIDT=.LiAgQmE=.c2V=.IDY0IF==.RW4=.Y29kaW4=.ZyB3aXT=.aCD=.VVJMIGF=.bmQg.RmlsZQ==.bmG=.bWUg.U2G=.ZmUgQU==.bHB=.aGFi.ZXS=.IC4gLk==.IC4g.LiAuICC=.NgogICB=.NS5=.ICBC.YXNlIDN=.MiA=.RW5jb2R=.aW5nIC5=.IC4=.IC4g.LiAuIC4=.IC4gLiD=.LiB=.LiB=.LiAuIF==.LiAu.IC4=.IC4g.LiAu.IC4gLiD=.LiAuIC==.LiB=.IDZ=.CiB=.ICA=.Ni4gIF==.QmF=.c2UgMZ==.NiBFbj==.Y29kaZ==.bmcgLiB=.LiAuIG==.LiAu.IC5=.IC4gLiB=.LiAu.IC6=.IC4gLl==.IC4g.LiA=.LiA=.LiAu.IC7=.IC5=.IC4g.LiAuIF==.IDgK.ICAg.Ny4gIEl=.bGx1c3Q=.cmF0.aW9uc8==.IGFuZCC=.ZXhh.bXBsZU==.cyD=.LiAuIC6=.IC4gLj==.IC4gLt==.IC4gLg==.IC4g.LiAuIK==.LiB=.LiAuIC4=.IC4gLu==.ICB=.OQog.ICA4LiB=.IFNlY3W=.cml0eZ==.IENvbnN=.aWRlcmF=.dGlvbnM=.ICB=.LiAuIC5=.IC4g.LiAuID==.LiAu.IC4gLl==.IC4gLp==.IC4g.LiAuIC5=.IC4=.IC6=.IC4g.MTAKIF==.ICA=.OS4g.IFJl.ZmVyZW5=.Y2VzIC4=.IC4gLiB=.LiAuIC==.LiC=.LiAuIE==.LiAu.IC7=.IC4gLiD=.LiB=.LiAuIC4=.IC4gLt==.IC5=.IC4gLk==.IC4g.LiB=.LiAuIE==.MTEKII==.ICAgICB=.IDkuMS4=.ICBO.b3Jt.YXQ=.aXZl.IFJl.ZmVy.ZW5jZV==.cyB=.LiAuIJ==.LiAuIC5=.IC4gLj==.IC4g.LiAuIC5=.IC4g.LiA=.LiAuIC7=.IC4gLiD=.MTEK.ICAgICB=.ICA5Lg==.Mi4gIK==.SW5mb0==.cm3=.YXRpdt==.ZSBS.ZWZlci==.ZW5jZXO=.IC4gLiB=.LiAu.IC4gLk==.IC4gLiB=.LiAuIC5=.IC5=.IC5=.IC7=.IC4g.LiAu.IDExCiB=.ICAxMB==.LiBBY2v=.bm93bD==.ZWQ=.Z2Vt.ZW50c5==.IC4g.LiAu.IC4g.LiA=.LiAuIC5=.IC4g.LiAuIC4=.IC4g.LiB=.LiB=.LiAuIC5=.IC4g.LiAuIC6=.IC4gMTF=.CiA=.ICAx.MS4g.RWRpdG/=.cif=.cyBBZF==.ZHJlc3M=.IC6=.IC4gLiB=.LiAu.IC4gLiB=.LiAuIF==.LiAu.IC4gLl==.IC4gLn==.IC4gLj==.IC4g.LiB=.LiA=.LiAuIF==.LiAx.MgogICC=.MTIuIEa=.dWx=.bCB=.Q29weXK=.aWdo.dCC=.U3Rh.dGV=.bWVudCA=.LiAu.IC4gLh==.IC4g.LiAu.IC4gLk==.IC4gLiD=.LiAu.IC4gLiC=.LiAuIC4=.IC4gMTP=.CgoKCgp=.CgpK.b3N=.ZWZzc1==.b26=.ICAgICC=.ICAgICB=.ICA=.ICAgICA=.ICAg.SW5m.b3JtYXT=.aW9u.YWwgIE==.ICA=.ICAg.ICB=.ICA=.ICAgIP==.ICAg.ICB=.ICA=.W1BhZ2X=.IDFd.CgwKUt==.RkMg.MzU0.OCAgICA=.IFT=.aGX=.IEJhc2V=.MTYsIEI=.YXNlMy==.MiwgYW6=.ZCBC.YXNlNjR=.IERhdD==.YSBF.bmNvZGn=.bmdzID==.ICAgIF==.SnVs.eSAy.MDB=.Mwp=.Cgox.LiAg.SW5=.dHJvZF==.dWN0aW9=.bgoK.ICAgQn==.YXM=.ZSD=.ZW5=.Y29kaR==.bmcgb2==.ZiBk.YXRhII==.aXMgdXP=.ZWQgaT==.biBt.YW55IF==.c2l0.dWF=.dGk=.b25=.cyB0byA=.c3Rv.cmX=.IG9y.IHT=.cmFuc1==.ZmVyCiB=.ICBk.YXRhIJ==.aW4g.ZW52aV==.cm9ubWV=.bnRzIHR=.aGF0LG==.IHA=.ZXJoYU==.cHMgZp==.b3Ig.bGVnYWN=.eSBy.ZWFzb24=.cywg.YXJlIHK=.ZXN0cl==.aWN0ZWQ=.CiAg.IHRv.IG9u.bHkgVU==.Uy1BU0==.Q0lJIH==.Wzld.IGR=.YXRhLiA=.IEJhc2X=.IGW=.bmNv.ZGluZyB=.Y2FuIE==.YWy=.c28=.IGL=.ZSB1c2V=.ZCA=.aW4gbmU=.dwr=.ICAgYXB=.cGxpYw==.YXRp.b25zIP==.dGhhdCB=.ZG8=.IG5vdCD=.aGF2ZSD=.bGVnYWN=.eSByZXM=.dHL=.aWP=.dGl=.b25zLD==.IHNpbd==.cGx5IGI=.ZWM=.YXVzZa==.IGl0Ck==.ICAgbWH=.a2VzIGm=.dCB=.cG9zcx==.aWJs.ZSC=.dG8gbWF=.bmlwdW==.bGE=.dGV=.IG9i.amU=.Y3R=.cyB3aXT=.aCB0ZU==.eHQgZf==.ZGl0b3J=.cy4KCi==.ICAgSV==.biB0aB==.ZSBw.YXN0.LCBkaWY=.ZmVyZU==.bnQgYX==.cHBs.aWN=.YXRp.b25z.IGhhdj==.ZSD=.aGFk.IGRpZk==.ZmW=.cmW=.bnQgcmV=.cXV=.aXK=.ZW1lbh==.dHMK.ICB=.IGFuZCB=.dGh1.cyBz.b21ldGn=.bWVzIGk=.bXBsZW3=.ZW50ZWQ=.IGJhc5==.ZSBlbi==.Y29kaV==.bmc=.cyBpbiB=.c2xp.Z2h0bB==.eSBkaQ==.ZmZlcmW=.bnQKIE==.ICB=.d2F5.cy4g.IFR=.b2RheSx=.IHA=.cm8=.dG9jb2y=.IHN=.cGVj.aWZ=.aWNhdE==.aW9uc0==.IHN=.b21l.dGn=.bWVzIF==.dXNl.IGI=.YXNl.IGX=.bmNvZD==.aW5ncyB=.aW4KICC=.IGdlbk==.ZXJhbCx=.IGH=.bmQ=.ICJiYf==.c2V=.NjQiIGk=.biBwYS==.cnRpY5==.dWxh.ciwgd2k=.dGhv.dXQg.YSD=.cHJl.Y2lz.ZSBk.ZXNj.cmlwdGl=.b25=.IG9yCl==.ICAg.cmVm.ZXK=.ZW5jZV==.LiAg.TUlN.RSBbM10=.IGlzIG/=.ZnRl.biB1c0==.ZWQgYT==.cyBh.IHJlZmV=.cmVuY2U=.IGY=.b3J=.IGJhc2U=.NjQgd9==.aXRobw==.dXT=.CiAgID==.Y29uc2l=.ZGVy.aW5nIF==.dGh=.ZSBjb0==.bnP=.ZXF1.ZW5jZd==.cyBm.b3IgbGk=.bmUtd3K=.YXBwaY==.bmcgb3L=.IG5vbi==.LWFscGh=.YWJl.dAogIF==.IGNoYXL=.YWN0ZXJ=.cy4g.IFRo.ZSBw.dXJw.b3Nl.IG9m.IHRo.aXM=.IHN=.cGVjaWb=.aWM=.YXRpb9==.biBpcyB=.dG8g.ZXN0.YWJsaXN=.aCA=.Y29t.bW9u.CiAgIGF=.bHBoYWI=.ZXQg.YW5kIF==.ZW5j.b2Rp.bmcg.Y29u.c2lkZXJ=.YXRpb26=.cy5=.ICBUaD==.aXP=.IHdpbE==.bCC=.aG9wZZ==.ZnVsbHl=.IHJl.ZHVjZQo=.ICAgYW3=.YmlndT==.aXR5IG==.aW4=.IG90.aGVy.IGRvY/==.dW1lbk==.dHMs.IGxlYf==.ZGl=.bmcgdD==.byBi.ZXR0ZXL=.IGl=.bnQ=.ZXJv.cGVy.YWJp.bGl0ef==.Lgp=.CiAg.IFRoZQ==.IGtleSC=.d29yZJ==.cyAi.TVVTVCI=.LCB=.Ik1=.VVNU.IE5PVCJ=.LCA=.IlI=.RVFVSZ==.UkV=.RCIs.ICK=.U0hBTB==.TCIsICJ=.U0hB.TEwg.Tk+=.VCI=.LAogICB=.IlNIT1U=.TER=.Iix=.ICJT.SE9VTE==.RCBOT5==.VCIsICJ=.UkVDTx==.TU1FTkQ=.RUQiLE==.ICJN.QVkiLE==.IGFuZCB=.Ik9Q.VElPTj==.QUy=.IiBpbiB=.dGhpc0==.CiC=.ICBkb2N=.dW1l.bnQg.YXJ=.ZSB0.byB=.YmV=.IGludGV=.cnBy.ZXR=.ZWR=.IGFz.IGT=.ZXNj.cmli.ZWQg.aW4gUkZ=.QyAyMTE=.OSBb.MV0uCt==.CjIuICB=.SW1wbGV=.bWW=.bnRh.dGlvbiC=.ZGlz.Y3J=.ZXBhbmN=.aWVz.CgogICA=.SGVyZSC=.d2V=.IGQ=.aXNj.dXP=.cyB0aN==.ZSBk.aXNj.cmVw.YW5jaWU=.cyBi.ZXR3ZV==.ZW5=.IGJhcw==.ZSBlbmO=.b2Rpbj==.ZwogICD=.aW1wbGV=.bWVudD==.YXRp.b25z.IGluIN==.dGg=.ZSBw.YXN0LCD=.YW5kIHf=.aGVyZSB=.YXA=.cHJvcHL=.aWH=.dGUsIG1=.YW5kYXQ=.ZSD=.YQr=.ICB=.IHNw.ZWNpZj==.aWMg.cmVjb23=.bWV=.bmRl.ZCA=.YmVoYS==.dmlv.ciBmb3K=.IHRoZU==.IGZ=.dXR1cl==.ZS4K.CjIuMS==.LiC=.IExpbk==.ZSA=.ZmW=.ZWR=.cyA=.aW5=.IGVuY29=.ZGVk.IGR=.YXQ=.YQo=.CiAgIE3=.SU1F.IFt=.M11=.IGlzIG9=.ZnRlbiB=.dXNl.ZCBhcz==.IGEgcmU=.ZmVyZW6=.Y2UgZm9=.ciBiYR==.c2W=.IDY0IE==.ZW5=.Y29k.aW5n.LiAg.SG9=.d2V2.ZXJ=.LAog.ICBNSS==.TUV=.IGRv.ZXMgbm9=.dCB=.ZGVmaR==.bmUgImJ=.YXM=.ZSA2NCJ=.IHBlcg==.IHNlLP==.IGJ=.dXQgcj==.YXRo.ZXL=.IGF=.ICJiYXM=.ZSA2NAr=.ICAgQ2/=.bnRlbnR=.LVRy.YW4=.c2Zl.ci1F.bmNvZP==.aW5nIiB=.Zm9yIHU=.c2Ugdy==.aXRo.aW4gTUm=.TUUuICB=.QXMgc3U=.Y2gsIE3=.SU1F.CiAgIJ==.ZW4=.Zm9=.cmNl.cyBh.IGxpbWm=.dCB=.b24gbGl=.bmW=.IGxlbme=.dGh=.IG9=.ZiA=.YmH=.c2V=.IDY=.NCA=.ZW5jb1==.ZGV=.ZCBkYZ==.dGF=.IHRvIDc=.Ngog.ICBjaGH=.cmFj.dGVycx==.LiAgTT==.SU3=.RSBpbk==.aGVyaV==.dHMgdE==.aGUg.ZW5jb2Q=.aW5nIJ==.ZnJvbSB=.UEU=.TSBbMl==.XSBzdGF=.dGluZyB=.aXQgaXP=.CiAgICJ=.dmk=.cnR1YWy=.bHkgaWQ=.ZW4=.dGn=.Y2FsIiz=.IGhv.d2V2ZXJ=.IFA=.RU0gdXP=.ZXMgYSD=.bGluZSB=.bGVu.Z3RoID==.b2b=.IDY0CiB=.ICBj.aGFy.YWN0ZQ==.cnO=.LiAgVGi=.ZSBNSU1=.RSBhbmQ=.IFBF.TSBsaf==.bWl0cyB=.YXJlIGI=.b3RoIK==.ZHVlIF==.dG8gbGm=.bWl0.cyB3aXQ=.aGluCl==.ICB=.IFP=.TVRQLgo=.CiD=.ICBJ.bXBsZU==.bWU=.bnT=.YXRp.b25zIE1=.VVNU.IE6=.T1R=.IG5v.dCBhZD==.ZCBs.aW4=.ZSBmZU==.ZWRz.IHRvIGL=.YXNl.IGVuY5==.b2Rl.ZCA=.ZGF0YV==.CiAgIHV=.bmxlc3M=.IHRo.ZSBz.cGVjaS==.Zmk=.Y2F0.aW9uIM==.cmW=.ZmVy.cml=.bmcgdG8=.IHRoaX==.cyB=.ZG9=.Y3Vt.ZW50IB==.ZXhw.bGlj.aXR=.bHkKICB=.IGRpcmW=.Y3R=.cyBi.YXN=.ZSBlbmM=.b2RlcnP=.IHRvIGE=.ZGQg.bGl=.bmUgZl==.ZWVk.cyB=.YWZ=.dGVyIB==.YSBzcF==.ZWNp.Zmk=.YyBu.dW1i.ZXIgby==.Zgog.ICB=.Y2h=.YXJhY6==.dGVy.cy4KCl==.Cgq=.CgoKCo==.Ckr=.b3P=.ZWZzc0==.b24gICD=.ICD=.ICB=.ICA=.ICD=.ICAgICD=.ICAgIEl=.bmZv.cm1hdGk=.b25h.bCAgIP==.ICAgICB=.ICAgIA==.ICAg.ICAgIK==.ICAgW1B=.YWdl.IDI=.XQr=.DAr=.UkZDIF==.MzU0.OCAg.ICA=.IFRoZZ==.IEJhc2V=.MTYs.IEJh.c2UzMiw=.IGFu.ZCB=.QmFzZV==.NjQgRH==.YXQ=.YSBFbt==.Y29kaR==.bmd=.cyAgIK==.ICB=.SnU=.bHl=.IDIwMDM=.Cgp=.CjIuMl==.LiA=.IFBhZE==.ZGlu.ZyBvZl==.IGVuY29=.ZGVkIA==.ZGF0YZ==.Cgog.ICBJbiB=.c29tZSB=.Y2ly.Y3Vtcx==.dGFuY2U=.cywgdH==.aGU=.IHVzZd==.IG+=.ZiA=.cGFk.ZGluZyD=.KCI9.Iil=.IGluIB==.YmFz.ZSBlbk==.Y29kZZ==.ZCBk.YXRhCiA=.ICBp.cyBu.b3Qg.cmVxdR==.aXJ=.ZWQgbj==.b3J=.IHVzZWR=.LiAg.SW4gdGh=.ZSBn.ZW6=.ZXJhbCB=.Y2FzZSw=.IHdoZf==.biBhc0==.c3VtcP==.dGlvbnN=.IG8=.bgogIP==.IHNpemV=.IG9mID==.dHJhbt==.c3A=.b3J0Zf==.ZCB=.ZGF0YT==.IGNh.bm5vdN==.IGI=.ZSA=.bWG=.ZGUs.IHBhZJ==.ZGluZz==.IGlzII==.cmVx.dWlyZd==.ZCB0b0==.IHlpZc==.bGQK.ICAgY2+=.cnJlY3R=.IGRl.Y29kZW==.ZCBkYR==.dGEuCgo=.ICAg.SW1w.bGV=.bWVudGF=.dGlv.bnMgTU==.VVNUIJ==.aW5jbE==.dWRl.IGFwcE==.cm9=.cHJpYXQ=.ZSB=.cGE=.ZCB=.Y2g=.YXJhY9==.dGVyc0==.IGF0IHR=.aGW=.IGVuZCA=.b2YK.ICAgZW7=.Y29kZS==.ZCBkYXR=.YSB1bh==.bGVz.cyD=.dGhl.IHNwZWN=.aWZpY2E=.dGlvbr==.IHJl.ZmV=.cnJpbm==.ZyB0b4==.IHRoac==.cyD=.ZG9=.Y3V=.bWVudAo=.ICA=.IGV4cGx=.aWNpdGw=.eSBz.dGF0ZXP=.IG/=.dGhlcnd=.aXNl.LgoKMi4=.My6=.ICBJ.bnRl.cnByZXS=.YXR=.aW9=.biBvZl==.IG5vbl==.LWFs.cGh=.YWJldN==.IGNo.YXJhY3Q=.ZXJzIGm=.biBl.bmNv.ZGVk.IGT=.YXRhCj==.CiAgIE==.QmE=.c2UgZd==.bmNvZGm=.bmdzIHU=.c2Ug.YSD=.c3BlY2n=.ZmljLE==.IHI=.ZWR1.Y2VkLK==.IGF=.bHBoYWI=.ZXR=.IHR=.byBlbmN=.b2Rl.IGJpbg==.YXJ5.CiAgIJ==.ZGF0YW==.LiAgTm8=.biB=.YWxw.aGFiZXR=.IGNo.YXJhY3R=.ZXJz.IGNv.dWxkIN==.ZXhpc3Q=.IHdpdN==.aGl=.biBiYS==.c2UgZV==.bmNvZB==.ZWQgZGE=.dGEs.CiAg.IGNhdXN=.ZWQgYnk=.IGRhdGF=.IGP=.b3JydU==.cHRpb27=.IG+=.ciBieU==.IGR=.ZXNpZ4==.bi4gIE7=.b24gYWx=.cGg=.YWJldCB=.Y2hhcmE=.Y3Rlcn==.cyBtYU==.eQog.ICBi.ZSBleHC=.bG9pdGX=.ZCBhcyB=.YSAiY29=.dmVy.dCC=.Y2hhbp==.bmVsIiw=.IHdoZR==.cmUg.bm9u.LXByb3Q=.b2Nv.bCD=.ZGF0Yd==.IGNh.biBiZQo=.ICAgcy==.ZW50.IGZv.ciBuZWa=.YXJ=.aW91.cyBwdXI=.cG9z.ZXN=.LiAgTl==.b24gYWw=.cGhhYmU=.dCBjaGG=.cmFj.dGVycyB=.bWlnaG==.dCBh.bHNvIGI=.ZQp=.ICAg.c2Vu.dCB=.aW4gb3J=.ZGVyIN==.dG8g.ZXhwbB==.b2l0IGl=.bXBsZT==.bWVu.dGF0.aW9uIC==.ZXJ=.cm9ycyB=.bGVhZGl=.bmc=.IHRvLCB=.ZS4=.Zy4sCiB=.ICBi.dWZm.ZXIg.b3a=.ZXJm.bG93.IGF0dE==.YWNr.cy4KCiD=.ICBJbXB=.bGV=.bWU=.bnT=.YXRp.b26=.cyA=.TVX=.U1Qgci==.ZWplY3R=.IHQ=.aGUg.ZW5j.b2Rp.bmcgaWa=.IGl0.IGM=.b250YU==.aW5z.IGN=.aGFyYWP=.dGU=.cnMK.ICAg.b3V0c/==.aWRlIE==.dGhlIGL=.YXNlIGH=.bHB=.aGFi.ZXQgd2g=.ZW7=.IGlu.dGVycHL=.ZXRp.bmcgYmF=.c2UgZW4=.Y29k.ZWQ=.IGRh.dGEs.IHW=.bmxlc5==.cwogIB==.IHRoZV==.IHNw.ZWNpZmk=.Y2F0aS==.b25=.IHJl.ZmVycml=.bmd=.IHRv.IHQ=.aGlzIE==.ZG9jdW2=.ZW50IB==.ZXhw.bGljaR==.dGx5IHN=.dGF0ZT==.cwog.ICA=.b3T=.aGU=.cndp.c2X=.LiA=.IFN1Y2j=.IHN=.cGVj.aWY=.aWNh.dGn=.b25zIJ==.bWF5LCA=.YXMgTV==.SU1FIE==.ZG9lcy==.LCBpbj==.c3RlYWQ=.IHN0.YXRlIHT=.aGF0.CiAgIF==.Y2hh.cmF=.Y3Rl.cnMgb3X=.dHNpZGV=.IHR=.aGUgYh==.YXNl.IGVu.Y29kaT==.bmcgYS==.bHBoYU==.YmV0IHP=.aG91bB==.ZCBz.aW0=.cGx=.eSBiZR==.CiAg.IGln.bm9y.ZWQg.d2hlbiA=.aW50ZXL=.cHK=.ZXRpbk==.ZyBkYXQ=.YSAo.ImJl.IGx=.aWJ=.ZXJhbCB=.aW4g.d2hh.dCB5bx==.dSB=.YWNjZR==.cHT=.IikuCj==.ICAgTm9=.dGUgdGj=.YXQ=.IHRoaf==.cyBtZWF=.bnMgdGg=.YXQgYW7=.eSBDUkz=.RiB=.Y29ucz==.dGl0.dXRl.ICJub27=.IGFscE==.aGE=.YmV0Cq==.ICAgY2h=.YXJhY3Q=.ZXJzIu==.IGFu.ZCBh.cmUgaV==.Z25v.cmW=.ZC4gIEa=.dXJ0aGV=.cm1vcmV=.LCBzdWM=.aCBz.cGX=.Y2lmaV==.Y2F0.aW8=.bnMgbd==.YXkKICA=.IGNvbnM=.aWRlcl==.IHRoZSB=.cGFkIJ==.Y2hhcj==.YWN0.ZXI=.LCAiPSL=.LCB=.YXMgbm8=.dCA=.cGFydCC=.b2YgdE==.aGUgYmH=.c2Ug.YWxwaGG=.YmV=.dAp=.ICC=.IHVu.dGlsIHR=.aGUgZW5=.ZCB=.b2YgdGg=.ZSBz.dHJp.bmcu.ICBJZl==.IG1v.cmU=.IHRoYX==.biB=.dGhlIF==.YWxs.b3dlZCB=.bnU=.bWJlct==.IG9mIHB=.YWR=.CiAgIGM=.aGFyYc==.Y3R=.ZXJzIGE=.cmX=.IGa=.b3Vu.ZCBhdCB=.dGhl.IGVu.ZCA=.b2YgdGj=.ZSD=.c3R=.cmk=.bmcsIGU=.Lmcu.LCBh.IGJh.c2V=.IDY0ID==.c3Ry.aW5nCl==.ICAgdGV=.cm1pbmE=.dGVkIHc=.aXRoIN==.Ij09PSI=.LCB0aC==.ZSBl.eGM=.ZXNzIP==.cGFkIGN=.aGE=.cmFjdP==.ZXJ=.cyBj.b3VsZCA=.YmUgaWf=.bm9yZWT=.Lgp=.CjI=.LjQuIC==.IENo.b2+=.c2luZ0==.IHRo.ZSBh.bHD=.aGFiZV==.dAoK.ICAgRC==.aWZmZXK=.ZW50IGE=.cHBsac==.Y2F0aW+=.bnMgaGF=.dmV=.IGRpZmZ=.ZXJlbt==.dCBy.ZXF1aXJ=.ZW1l.bnRz.IG8=.biB0aGX=.IGNo.YXJh.Y3Rlcj==.cwog.ICBp.biB0aGU=.IGFs.cGhhYmX=.dC5=.ICBI.ZXJlIB==.YXJlIB==.YSBmZXc=.IHJlcV==.dWl=.cmU=.bWVu.dHP=.IHS=.aGF0IGR=.ZXRlcm0=.aW5=.ZSB3aGm=.Y2gKIF==.ICBhbHC=.aGFi.ZXQg.c2g=.b3VsZCB=.YmUgdR==.c2VkOgr=.CiAg.IG9=.ICAg.SGFuZD==.bGVk.IGJ5.IGj=.dW1=.YW5zLj==.ICBDaB==.YXJhY3Q=.ZXI=.cyAi.MCIs.ICK=.TyIgYU==.cmUgZWE=.c2ls.eSBpbnR=.ZXJjaE==.YW7=.Z2V=.ZCwKIE==.ICAgICB=.IGFzIHe=.ZWx=.bCAi.MSIsICJ=.bCIgYW6=.ZCAiSSI=.LiAgSU==.biC=.dGhlIGI=.YXM=.ZTMyIGH=.bHD=.aGFi.ZXR=.IGJl.bG93LCA=.d2hlcv==.ZSAw.CiAgICB=.ICA=.ICh6ZXL=.byn=.IGFuZCB=.MSAobz==.bmUpIN==.aXMgbg==.b3Qg.cHJlc6==.ZW50LE==.IGEgZGX=.Y29kZd==.ciBt.YXl=.IGludGU=.cnBy.ZXQgMCC=.YXMKICB=.ICAgICB=.Tyw=.IGFuZCD=.MSBhcyB=.SSB=.b3IgTCB=.ZGVw.ZW7=.ZGlu.ZyBv.biBjYXM=.ZS4gIN==.KEhv.d2U=.dmVyLD==.IGJ5.IGRlZmE=.dWz=.dCBpdAp=.ICAgIF==.ICAg.c2hvdR==.bGQ=.IG5v.dCwg.c2VlIC==.cHJl.dmlv.dXMgc2V=.Y3Rp.b24=.LikKCgp=.CgoKCp==.Sm9zZWZ=.c3NvbiA=.ICAgIF==.ICAgICB=.ICAg.ICAgICA=.ICBJ.bmZvcl==.bWF0aW8=.bmG=.bCAgICA=.ICAgICB=.ICAgIB==.ICAg.ICAgICD=.IFtQYT==.Z2Ug.M10K.DAp=.UkZDIDM=.NTQ4IE==.ICAgIE==.VGhl.IEJh.c2V=.MTYsIA==.QmFz.ZTMy.LCBhbmS=.IEI=.YXM=.ZTY0IK==.RGF=.dGEgRW4=.Y29kae==.bmdz.ICAgIF==.IEq=.dWx5IDJ=.MDAzCl==.Cgp=.ICAgbyD=.ICBFbk==.Y29kZT==.ZCB=.aW50.byBz.dHJ1.Y3R1cmU=.cyB0aB==.YXQg.cGxh.Y2V=.IG90aG==.ZXIgcl==.ZXF1.aXJl.bWU=.bnRzLiD=.IEY=.b3Ig.YmFzZQp=.ICAgID==.ICAg.MTYgYd==.bmQg.YmFzZSA=.MzIs.IHRo.aXMgZN==.ZXRlcm1=.aW5l.cyB0aE==.ZSB1c1==.ZSB=.b2YgdR==.cHB=.ZXItIB==.b3IgbG9=.d2VyY2F=.c2UK.ICAg.ICAg.IGFscC==.aGH=.YmV=.dHMuICB=.Rm9y.IGK=.YXNlIF==.NjQs.IHRo.ZSBu.b24=.LWFscGj=.YW4=.dW1l.cmljIF==.Y2hh.cmFjdGU=.cnMg.KGlu.CiAg.ICAgICD=.cGFydGl=.Y3Vs.YXIg.Ii8=.Iin=.IG1h.eSBiZSD=.cHJv.YmxlbWF=.dGl=.YyBpbiA=.ZmlsZSC=.bmFt.ZXMgYV==.bmR=.IFVS.THMu.Cgog.ICBvICB=.IFVzZU==.ZCBh.cyBpZE==.ZW50aWY=.aWVyc/==.LiB=.IEM=.ZXJ0.YWluIP==.Y2hh.cmFjdE==.ZXJz.LCBu.b3T=.YWJsed==.ICIr.IiBh.bmQ=.ICIv.IiBpbv==.CiAgICB=.ICAgdA==.aGUgYq==.YXNlIE==.NjQgYWx=.cGhh.YmV0LF==.IGFy.ZSB0cg==.ZWF=.dGVk.IGFz.IHdv.cmQtYnJ=.ZWF=.a3N=.IGJ=.eSBs.ZWdhY0==.eSB0ZX==.eHQKICB=.ICAg.ICA=.c2Vh.cmNoL3==.aW5kZXg=.IHRvb2z=.cy4KCiA=.ICBUaGX=.cmV=.IGlzIB==.bm8gdW4=.aXZlcnN=.YWxs.eSBhYy==.Y2VwdGW=.ZCBhbE==.cGhh.YmX=.dCB0.aGF0.IGZ1bF==.ZmlsbHN=.IGFsbCC=.dGhl.CiC=.ICByZXF=.dWlyZV==.bWVudB==.cy4gIA==.SW4g.dGhp.cyBkb2P=.dW1l.bnQsIF==.d2Ug.ZG8=.Y3Vt.ZW50.IGH=.bmQgbj==.YW3=.ZSB=.c29tZT==.IGN1.cnJlbt==.dGx5.CiA=.ICB1c2X=.ZCBhbN==.cGhhYg==.ZXRz.Lgq=.CjMuIJ==.IEI=.YXNlIG==.NjQgRW5=.Y29=.ZGlu.ZwoK.ICAgVJ==.aGUgZl==.b2xsbx==.d2lu.ZyB=.ZGVz.Y3JpcHQ=.aW9=.biBvZiB=.YmFz.ZSA2.NCBpc0==.IGR1.ZSB0.byC=.WzJdLE==.IFszXSz=.IFs0XV==.IGFuZCB=.WzVdLgo=.CiD=.ICBU.aGU=.IEJh.c2UgNjR=.IGVu.Y29kaW4=.ZyBpc2==.IGRl.c2l=.Z24=.ZWQgdG9=.IHJlcHJ=.ZXNlbnR=.IGFy.Yml0cmE=.cnk=.IHO=.ZXE=.dWX=.bmNlcy==.IG9mCk==.ICAgb3==.Y3RldHM=.IGluIGH=.IGZvcm1=.IHRoYZ==.dCByZXE=.dWly.ZXMg.Y2FzZZ==.IHNlbk==.c2l0aXZ=.aXR5IGI=.dXQgbmV=.ZWQgbm9=.dCB=.YmUKICB=.IGh1.bWFu.bHl=.IHJlYT==.ZGFi.bGUuCgq=.ICAg.QSA2NU==.LWNoYXI=.YWN0ZY==.ciBzdWL=.c2X=.dCBvZk==.IFVT.LUFTQ/==.SUkg.aXMg.dXNlZE==.LCD=.ZW5hYmz=.aW5n.IDYgYk==.aXRz.IHT=.byD=.YmV=.CiA=.ICD=.cmVwcmX=.c2Vu.dGVkIHB=.ZXIg.cHJpbj==.dGFibGX=.IGN=.aGFyYWM=.dGVyLiA=.IChU.aGUgZa==.eHRyYSB=.NjV0aCA=.Y2hh.cmH=.Y3Rl.ciwgIl==.PSIsCl==.ICAgaXN=.IHVzZWR=.IHRv.IHN=.aWduaWY=.eSBhIHN=.cGVjaU==.YWx=.IHD=.cm9jZXN=.c2lu.ZyB=.ZnVuY3S=.aW9u.LikK.CiAgIFR=.aGUgZW4=.Y2/=.ZGluZyA=.cHJvY2X=.c3M=.IHJlcHL=.ZXM=.ZW50c9==.IDI0LW==.Ymk=.dCBncm9=.dXBzIG8=.ZiBpbt==.cHV0IF==.Yml0.cyBh.cyBvdW==.dHB1dAp=.ICAg.c3Ry.aW5nc2==.IG+=.ZiA0IE==.ZW5jbz==.ZGVkIGN=.aGE=.cmFjdGU=.cnMuICB=.UHJv.Y2Vl.ZGluZ1==.IGa=.cm9tIF==.bGVmdC==.IHT=.byByaT==.Z2h0.LCBh.CiAg.IDL=.NC1i.aXQg.aW5wdXR=.IGdyb3U=.cCA=.aXMg.Zm9y.bWVkIK==.Ynl=.IGNvbmM=.YXT=.ZW5hdGm=.bmcgMyB=.OC1iaU==.dCBpbo==.cHV0IGf=.cm91cC==.cy4KIE==.ICBUaGV=.c2X=.IDI0IGJ=.aXRzIE==.YXJl.IHRo.ZW7=.IHRy.ZWE=.dGVkIN==.YXMgNF==.IGNvbh==.Y2F0ZR==.bmF=.dGVkIDZ=.LWJp.dCC=.Z3JvdXB=.cywgZT==.YWNo.CiAgIF==.b2Ygd2h=.aWNo.IGlzIC==.dHJhbnN=.bGF=.dGU=.ZCBp.bnT=.byBhIHN=.aW5nbGV=.IGS=.aWdpdCA=.aW4gdGh=.ZSBiYR==.c2X=.IDY0.IGFscGh=.YWJldC==.LgoK.ICAg.RWF=.Y2ggNi1=.Yml0IGc=.cm91.cCBpcyB=.dXNl.ZCBh.cyBhbiA=.aW5=.ZGV4IGl=.bnRv.IGE=.biA=.YXJyYXl=.IG9mIDY=.NCBw.cmn=.bnR=.YWJsZV==.CiAgIGO=.aGFyYWN=.dGVyc1==.LiAgVGg=.ZSBjaGF=.cmFj.dGV=.ciA=.cmW=.ZmVyZR==.bmNl.ZCBieS==.IHRoZU==.IGlu.ZGV4.IGn=.cyBw.bGFjZWQ=.IGlu.IHS=.aGUKICB=.IG91.dHB1dB==.IHN0cmm=.bmcu.CgoKCj==.CgoKCt==.CgoKCgo=.CgoKCi==.Ckpvc2W=.ZnNz.b24gIE==.ICAgICD=.ICAgICB=.ICAgIF==.ICAgIF==.SW5=.Zm9ybU==.YXRpb1==.bmFs.ICA=.ICB=.ICAgICD=.ICAgICB=.ICAgIF==.ICAg.IFtQYWd=.ZSA0XQo=.DAr=.UkZD.IDN=.NTR=.OCAgIE==.ICBUaM==.ZSB=.QmFzZTE=.Niz=.IEJhc2W=.MzIsIE==.YW5kIEL=.YXNlNt==.NCA=.RGF0YS==.IEVuY1==.b2Rpbme=.cyC=.ICB=.ICB=.SnVseT==.IDIwMF==.MwoKCp==.ICAgIE==.ICAgIJ==.ICAg.ICAg.ICB=.ICAgVGE=.Ymxl.IDE=.OiC=.VGhlIE==.QmG=.c2Ug.NjT=.IEFscGg=.YWJl.dAo=.CiC=.ICAg.ICBWYWy=.dWV=.IEU=.bmNvZGm=.bmcgIF==.VmFsdS==.ZSBFbmO=.b2Rpbk==.ZyAgVh==.YWx=.dWUg.RW5j.b2Rpbl==.ZyAgVmG=.bHV=.ZSA=.RW5j.b2Rp.bmcKICB=.ICAgICD=.ICAgMF==.IEE=.ICAg.ICAgICC=.ICAg.IDE3.IFIgIE==.ICAgICC=.ICAgIJ==.IDM0IGk=.ICC=.ICAg.ICAgICD=.ICB=.NTEg.egog.ICAgICA=.ICB=.ICB=.MSBCIE==.ICAg.ICAg.ICA=.ICAgMTh=.IFMg.ICB=.ICAgICB=.ICAgIDN=.NSBqIJ==.ICAgICB=.ICAgIA==.ICA=.NTIgMAr=.ICAgICD=.ICAgICB=.MiA=.QyAg.ICAgIP==.ICB=.ICAgIDE=.OSBU.ICD=.ICAg.ICD=.ICAg.ICAzNk==.IGsg.ICAg.ICAgICD=.ICAg.NTMgMQr=.ICB=.ICAgICA=.ICAgMyA=.RCC=.ICC=.ICB=.ICA=.ICAgICD=.MjAgVSC=.ICB=.ICAg.ICA=.ICAgIDO=.NyC=.bCAgICA=.ICD=.ICAgIC==.ICA1NF==.IDJ=.CiAg.ICAgICD=.ICAg.NCBFID==.ICA=.ICAgICC=.ICAg.IDIx.IFY=.ICAg.ICAgICD=.ICB=.ICAz.OCBtICA=.ICB=.ICAgIA==.ICAgIDW=.NSAz.CiAgIE==.ICAgICC=.ICD=.NSBGIE==.ICD=.ICC=.ICAgIE==.ICAg.MjJ=.IFcgICC=.ICAgICB=.ICAgIG==.Mzk=.IG4g.ICAgIE==.ICAgIH==.ICB=.IDU2ID==.NAog.ICAg.ICD=.ICAg.IDYgR0==.ICC=.ICAgIF==.ICA=.ICAgIDJ=.MyBYIB==.ICAgICA=.ICAgICC=.IDQwIG+=.ICAgIE==.ICAgIP==.ICB=.ICA=.NTcgNd==.CiB=.ICAgICB=.ICA=.ICA3.IEggICB=.ICAgICB=.ICA=.ICAyNCC=.WSA=.ICAgIE==.ICAg.ICB=.ICA0.MSBwICD=.ICAgID==.ICAg.ICAg.NTgg.Ngog.ICAgICA=.ICAgIJ==.OCBJ.ICAg.ICAg.ICA=.ICAg.IDI1IFr=.ICAgIA==.ICAg.ICD=.ICAg.NDIg.cSD=.ICAg.ICAgICB=.ICAgNTk=.IDcK.ICAgICA=.ICAgIK==.IDkgSk==.ICAgIN==.ICA=.ICAgICD=.IDI2IGF=.ICAgICB=.ICAg.ICB=.ICB=.NDMgco==.ICAgIE==.ICB=.ICAg.ICD=.IDYw.IDgKIF==.ICA=.ICAgIN==.ICAxMG==.IEsgICC=.ICAgICB=.ICAgIF==.Mjcg.YiAg.ICAgIB==.ICAgIC==.ICC=.NDQgc0==.ICD=.ICB=.ICB=.ICAgID==.ICA2MZ==.IDkK.ICAg.ICAg.ICAg.MTEgTCB=.ICAgIB==.ICAgIF==.ICAgMn==.OCA=.YyAgIN==.ICAgICA=.ICA=.ICD=.NDUg.dCAg.ICAgIF==.ICB=.ICA=.ICA2Mk==.ICsKIE==.ICAgIN==.ICA=.ICAx.MiA=.TSAg.ICAgICC=.ICAg.ICAy.OSC=.ZCAgICB=.ICAgICB=.ICAgNA==.NiB1.ICB=.ICA=.ICB=.ICAgIF==.ICA2M0==.IC8KIF==.ICAgICA=.ICAg.MTMg.TiB=.ICAg.ICAgICD=.ICAg.MzA=.IGUgICD=.ICAgIC==.ICAgID==.IDQ3ID==.dgo=.ICAgICD=.ICA=.ICAx.NCD=.TyB=.ICAgIE==.ICAg.ICAg.IDMxIN==.ZiA=.ICD=.ICB=.ICAg.ICB=.ICB=.NDh=.IHcgIF==.ICAgICB=.ICAocGE=.ZCkgPQp=.ICAg.ICB=.ICA=.ICB=.MTUg.UCAg.ICD=.ICB=.ICA=.ICAgIDO=.MiB=.ZyAgICB=.ICB=.ICAgIJ==.ICA0OSB=.eAog.ICAg.ICA=.ICAgMc==.NiBRICB=.ICAg.ICAgID==.ICD=.IDMzIGh=.ICAgICA=.ICD=.ICAgICB=.NTAg.eQo=.CiAgIFP=.cGVj.aWFs.IHByb2N=.ZXNzaU==.bmcgaf==.cyBw.ZXJmb3J=.bWVkIGk=.ZiBm.ZXdlciD=.dGhhbiD=.MjQgYk==.aXRzIP==.YXJlIGF=.dmE=.aWxhYv==.bGUK.ICAg.YXQgdE==.aGUgZW7=.ZCBv.ZiD=.dGhlIE==.ZGF0.YSBiZWn=.bmcg.ZW5jb9==.ZGVkLiA=.IEEgZnU=.bGwgZa==.bmNvZE==.aW5n.IHF1YW7=.dHVtIF==.aXMKICB=.IGFs.d2F5cyB=.Y29tcGy=.ZXRl.ZCB=.YXQgdG==.aGW=.IGVuZCB=.b2Yg.YSA=.cXVhbnR=.aXT=.eS4g.IFdo.ZW4gZmU=.d2Vy.IHRoYd==.biAyNCC=.aW4=.cHX=.dAogIF==.IGJpdE==.cyBhcs==.ZSBhdl==.YWls.YWJ=.bGU=.IGluIE==.YW5=.IGlucHV=.dCBnck==.b3VwLC==.IHplcj==.byBi.aXRzIGE=.cmUgYWS=.ZGV=.ZCAob24=.IHRoZX==.CiAg.IHJpZ2h=.dCkgdE==.byBm.b3J=.bSBhbiB=.aW5=.dGVn.cmFsIJ==.bnV=.bWJl.ciBvZj==.IDYtYmk=.dCBncm9=.dXA=.cy4g.IFBh.ZGT=.aW5nIN==.YXQ=.IHR=.aGUK.ICAgZV==.bmQgb2Y=.IHQ=.aGW=.IGRhdF==.YSBpcyC=.cGW=.cmZvcl==.bWVkIH==.dXNpbl==.ZyB0.aGV=.ICf=.PScgYz==.aGF=.cmFj.dGW=.ci4gIE==.U2lu.Y2UgYZ==.bGw=.IGL=.YXNlCt==.ICA=.IDY0IC==.aW5wdXS=.IGlz.IGF=.biA=.aW50.ZWdyYd==.bCBudW1=.YmVy.IG9mIE==.b2N0ZXS=.cywgb25=.bHkg.dGhlIGZ=.b2xs.b3d=.aW5n.IGNhc2V=.cwp=.ICAg.Y2FuIG==.YXJp.c2U6Ch==.CiAgID==.KDEpIHR=.aGUgZmk=.bmFs.IHF1YW7=.dHU=.bSBvZiC=.ZW5jb2R=.aW5nIGk=.bnB1dCD=.aXM=.IGF=.biBpbnQ=.ZWdyYf==.bCBtdU==.bHRpcN==.bGUgb2Y=.IDL=.NAog.ICBiaXR=.czsgaB==.ZXJl.LCB=.dGhlIGY=.aW5hbF==.IHU=.bml=.dCBvZiD=.ZW5jb0==.ZGVk.IG91dN==.cHV0.IHc=.aWxsIN==.YmUgYR==.biBpbnR=.ZWdyYWw=.CiAgII==.bXVsdP==.aXBsZU==.IG9m.IDQgY2g=.YXJhY6==.dGVy.cyB3.aXRo.IG5=.byAi.PSIgcD==.YWRkaY==.bmf=.LAoK.ICAgKDJ=.KSB0.aGV=.IGZp.bmFsIF==.cXV=.YW50.dW3=.IG9m.IGVuY29=.ZGluZ0==.IGlucN==.dXQg.aXMg.ZXhh.Y3Q=.bHkgOCA=.Yml=.dHM7IGh=.ZXJl.LCB0aGV=.CiAg.IGZpbmG=.bCB1.bml0IG9=.ZiBlbmN=.b2RlZC==.IG91.dHB1.dCB3aWy=.bCBiZU==.IHR3.byA=.Y2hhcl==.YWN0ZT==.cnMgZt==.b2xsb3c=.ZWQ=.IGJ5IHS=.d28K.ICAgIj1=.IiBwYV==.ZGRpbmf=.IGNo.YXJhY3R=.ZXI=.cywg.b3IKCiB=.ICAo.Mykg.dGj=.ZSBm.aW5hbCB=.cXVhbnQ=.dW0gb2Y=.IGVuY8==.b2Rpbmf=.IGlucD==.dXQgaXN=.IGV4.YWN0.bHkgMV==.NiBiaR==.dHM7IB==.aGVy.ZSwg.dGhl.CiC=.ICBm.aW5h.bCB1.bml0.IG9mIGV=.bmNv.ZGVkIB==.b3V0cHW=.dCB3.aWx=.bCBiZW==.IHRocmV=.ZSBj.aGFyYWN=.dGV=.cnM=.IGZvbGx=.b3dlZCB=.Ynkgbx==.bmUKICB=.ICI9.IiBwYV==.ZGR=.aW5nIGM=.aGE=.cmFjdGX=.ci4K.CgoK.Cgr=.CgoKCgp=.Sm9zZT==.ZnNzb9==.biA=.ICD=.ICAgICD=.ICAgICB=.ICAg.ICAg.IEluZm8=.cm1hdC==.aW9u.YWwg.ICAgIJ==.ICAgID==.ICAg.ICAgICC=.ICAgIF==.IFu=.UGFnZV==.IDVd.CgwKUkZ=.QyA=.MzU0OCB=.ICB=.ICA=.VGhlIEK=.YXNlMTY=.LCBC.YXNl.MzIsIGF=.bmQ=.IEK=.YXNlNk==.NCBE.YXT=.YSBF.bmNv.ZGlu.Z3MgIC==.ICB=.IEo=.dWx=.eSAy.MDAzCh==.Cgo0LiA=.IEJhc2==.ZSA2.NCBF.bmNvZGl=.bmc=.IHdpdGh=.IFVSTF==.IGFu.ZCBGaQ==.bGVuYW2=.ZSBT.YWZlIE==.QWxwaL==.YWJldAp=.CiB=.ICBUaD==.ZSA=.QmH=.c2V=.IDY0.IGU=.bmNv.ZGluZz==.IHdp.dGj=.IGFuIE==.VVJM.IGFu.ZCD=.ZmlsZW7=.YW1=.ZSBzYWY=.ZSBh.bHBoYf==.YmV0IE==.aGFz.IGJl.ZW4K.ICAgdS==.c2W=.ZCB=.aW4=.IFs4Xb==.LgoKICB=.IEFuIGE=.bHRlcm7=.YXRp.dmUgYWx=.cGhhYmV=.dCBo.YXMg.YmVlbiB=.c3VnZ2W=.c3RlZCA=.dGhh.dCB=.dXNlZA==.ICJ+IiD=.YXMgdF==.aGUgNp==.M3JkCk==.ICAgY5==.aGFy.YWN=.dGVy.LiA=.IFNpbi==.Y2UgdE==.aGUg.In4i.IGNoYXK=.YWN0Zd==.ciBo.YXMgcy==.cGVj.aWF=.bCBt.ZWFuaU==.bme=.IGlu.IHO=.b21l.IGZp.bGV=.CiAg.IHN5cw==.dGVt.IGVudml=.cm9u.bWVudHN=.LCB0aF==.ZSC=.ZW5j.b2Rpbmd=.IGQ=.ZXNjcml=.YmX=.ZCBpbl==.IHRo.aXMg.c2U=.Y3Rp.b24gaXO=.CiAg.IHJlY29=.bW0=.ZW5kZa==.ZCB=.aW5zdGU=.YWQuCgq=.ICAg.VGhpcyD=.ZW5j.b2Rpbk==.ZyBzaG9=.dWxkIF==.bm90.IGJl.IHJlZw==.YXJkZV==.ZCB=.YXN=.IHRoZSC=.c2FtZU==.IGG=.cyB=.dGhl.ICI=.YmFzZTb=.NCIKICD=.IGVuY0==.b2Rpbmf=.LCD=.YW5kIE==.c2j=.b3VsZCD=.bm90IE==.YmUgcmX=.ZmX=.cnJl.ZCB0b0==.IGFzIC==.b25s.eSAiYmG=.c2U2.NCIu.ICBVbk==.bGVzcwr=.ICAgbZ==.YWQ=.ZSBjbK==.ZWFyLD==.ICJi.YXNl.NjQ=.IiByZZ==.ZmVy.IHRvIF==.dGhlIGL=.YXM=.ZSA2.NCBpbs==.IHS=.aGUgcD==.cmV=.dmlv.dXMg.c2VjdB==.aW8=.bi4KCi==.ICB=.IFRoaS==.cyBl.bmNvZN==.aW5nID==.aXMgdGW=.Y2huaWN=.YWxs.eSBpZB==.ZW50.aWNh.bCC=.dG9=.IHRoZSB=.cHJl.dmlv.dXMgb4==.bmUsIGV=.eGNlcHQ=.CiAgIH==.Zm9=.ciB0.aGU=.IDb=.MjpuZCD=.YW5=.ZCA2.Mzpy.ZCBhbHA=.aGFiZZ==.dCBjaGF=.cmFjdGU=.ciwg.YXMg.aW5k.aWNhdGV=.ZCA=.aW4g.dGF=.YmxlIC==.Mi4KCiC=.ICAgIE==.ICAgIFT=.YWJsZSD=.MjogVF==.aGU=.ICI=.VVJM.IGE=.bmT=.IEZpbGX=.bmFt.ZSBz.YWZlIiB=.QmFzZT==.IDb=.NCBBbHB=.aGFiZXQ=.Cgog.ICAgVv==.YWx1ZU==.IEVu.Y29kaf==.bmcgIFZ=.YWx1ZT==.IEX=.bmNvZGl=.bmcgIFY=.YWx1Zf==.IEV=.bmNv.ZGlu.ZyAgVmE=.bHU=.ZSC=.RW5jb5==.ZGlu.Zwog.ICAgICA=.IDAgQV==.ICAgIE==.ICAgIC==.ICAgIDF=.NyBSICB=.ICAgIC==.ICAg.ICB=.IDM0.IGkg.ICAgIG==.ICA=.ICAgICB=.NTEgego=.ICAgICC=.ICAxIEL=.ICAgID==.ICB=.ICAgIB==.ICAx.OCBTIF==.ICAgICA=.ICAgICB=.IDM1IGp=.ICAgID==.ICB=.ICA=.ICD=.ICA1.MiAw.CiAgICB=.ICB=.IDJ=.IEMgIG==.ICAgICB=.ICB=.ICC=.IDE5.IFQ=.ICAgIE==.ICAgICC=.ICAgMzY=.IGsgICB=.ICAgICA=.ICAgIDW=.MyAxCk==.ICAgIM==.ICAg.MyBEIN==.ICAg.ICAgICA=.ICAg.MjB=.IFUgICA=.ICB=.ICAgICB=.ICAzNyC=.bCC=.ICAgICB=.ICAg.ICAgNR==.NCAyCiB=.ICAg.ICAgNE==.IEUgIC==.ICAg.ICAgIF==.ICAgMq==.MSBWICB=.ICAgICA=.ICB=.ICAgM9==.OCBtIC==.ICAgICD=.ICAgIF==.ICA1.NSAzCq==.ICA=.ICAgICD=.NSBG.ICAgIE==.ICAgICA=.ICAgMv==.MiBXIE==.ICAgIC==.ICAgIJ==.ICAgMz==.OSBuIF==.ICAgIB==.ICAgIJ==.ICAgNTZ=.IDQK.ICAg.ICAg.IDYgRyC=.ICAgICC=.ICAgICB=.IDIzIB==.WCAgIN==.ICAgIC==.ICAg.ICA0MCB=.byAg.ICB=.ICAgIG==.ICAgIDW=.NyA1.CiAg.ICB=.ICAg.NyBIID==.ICAgIB==.ICA=.ICB=.ICAg.MjQgWSB=.ICAgIE==.ICB=.ICAg.ICA0.MSBwIF==.ICA=.ICAgIC==.ICB=.ICAgNU==.OCA2Cp==.ICA=.ICAg.ICC=.OCBJIB==.ICB=.ICAgID==.ICAg.ICAy.NSBaIE==.ICC=.ICAg.ICB=.ICAg.IDQyIE==.cSAg.ICAgICB=.ICA=.ICAgNU==.OSD=.NwogIJ==.ICAg.ICA5ID==.SiAgIF==.ICAgIC==.ICA=.ICA=.IDI2IGH=.ICAgICD=.ICB=.ICAg.ICA0.MyA=.ciAgICD=.ICAgIN==.ICAgIDY=.MCA4CiD=.ICAg.ICAx.MCBL.ICAgICD=.ICAg.ICAgIE==.Mjf=.IGIgICD=.ICB=.ICAg.ICAgID==.NDQg.cyAgICD=.ICAgIE==.ICD=.ICA2.MSA5.CiAgIN==.ICA=.IDEx.IEwgICA=.ICC=.ICAg.ICC=.ICAy.OCBjICB=.ICAg.ICAg.ICAgID==.NDW=.IHR=.ICAgICB=.ICAg.ICAgIK==.NjIgLSA=.KG1pbnX=.cyl=.CiAgICA=.ICAxMl==.IE0g.ICA=.ICAg.ICAgICD=.IDJ=.OSBkICA=.ICAgICA=.ICAgIF==.IDQ2.IHUgIG==.ICAgIF==.ICAgICA=.IDYz.IF8gKM==.dW5=.ZGVyc1==.dHI=.aWtlKQp=.ICAgICA=.IDEz.IE4gIF==.ICB=.ICAgIA==.ICAg.IDMw.IGW=.ICB=.ICAg.ICAg.ICAgIDR=.NyB2CiA=.ICAgICB=.MTR=.IE9=.ICAgID==.ICAg.ICB=.ICAgMw==.MSBmICB=.ICAg.ICAg.ICAgIF==.NDi=.IHcgICC=.ICB=.ICAg.IChw.YWQp.ID0K.ICB=.ICAgIDE=.NSBQICD=.ICAg.ICAg.ICAg.IDMyIGc=.ICAgIP==.ICAg.ICB=.ICAgNDk=.IHgK.ICAgICA=.IDE2IFG=.ICAg.ICAgICC=.ICAgIE==.MzMgaP==.ICB=.ICA=.ICAgIK==.ICAg.IDUwIF==.eQp=.CjUuIF==.IEJh.c2Ug.MzJ=.IEVuY3==.b2Rpbj==.ZwoKIE==.ICBUaGV=.IGZv.bGxv.d2l=.bmcgZGW=.c2NyaY==.cHRpb27=.IG9m.IGI=.YXP=.ZSAz.MiBp.cyBkdWV=.IHQ=.byBbN11=.ICh3aXS=.aAogIE==.IGNvcl==.cmVjdGl=.b25zKS4=.Cgo=.ICAg.VGhl.IEJh.c2W=.IDMyIF==.ZW5jbz==.ZGl=.bmcg.aXN=.IGRlc4==.aWd=.bmVkIE==.dG9=.IHJl.cHJl.c2VudCA=.YXJi.aXRyYd==.cnkgc2V=.cXVl.bmNlcyB=.b2YK.ICAg.b2M=.dGV0.cyBp.biBhIGZ=.b3JtIHQ=.aGF=.dCBuZU==.ZWT=.cyB0b0==.IGL=.ZSBj.YXNlIF==.aW5zZW5=.c2l0aXa=.ZSBidQ==.dCBu.ZWX=.ZCBu.b3Qg.YmUKIN==.ICBo.dW1hbmw=.eSByZWH=.ZGH=.Ymxl.LgoKCk==.Cgr=.Ckpvc9==.ZWZzcz==.b24gIN==.ICA=.ICAgICD=.ICD=.ICAg.ICAgIE==.ICD=.SW5mb9==.cm1h.dGk=.b24=.YWwgIK==.ICAgIE==.ICAgIO==.ICAg.ICAg.ICAg.ICAgW1==.UGFnZW==.IDZdCl==.DAo=.UkZD.IDP=.NTR=.OCB=.ICAg.IFRo.ZSBCYXM=.ZTE2LN==.IEI=.YXNlMx==.Miwg.YW4=.ZCBC.YXNl.NjQg.RGH=.dGEg.RW5jb2R=.aW5n.cyAgIA==.ICD=.SnVseSA=.MjD=.MDMKCgp=.ICAg.QSAzM0==.LWN=.aGF=.cmE=.Y3RlciD=.c3Vi.c2V0.IG+=.ZiBVUz==.LUFTQ1==.SUkg.aXMgdXN=.ZWQsIG==.ZW6=.YWJ=.bGk=.bmcg.NSC=.Yml0cx==.IHRvIGI=.ZQogIJ==.IHJlcE==.cmW=.c2VudF==.ZWQ=.IHBlck==.IHByaV==.bnQ=.YWJsZR==.IGNo.YXJh.Y3Q=.ZXIuIP==.IChUaE==.ZSBl.eHRyYZ==.IDN=.M3JkIGN=.aGFyYR==.Y3Rlck==.LCAi.PSL=.LAogIM==.IGlzIHX=.c2Vk.IHRvIN==.c2k=.Z25pZv==.eSBhIHN=.cGVjaT==.YWwgcN==.cm9jZT==.c3Np.bmcgZt==.dW4=.Y3Rp.b24u.KQoKICA=.IFRo.ZSC=.ZW5j.b2Rpbme=.IHBy.b2Nlc3N=.IHJlcD==.cmVzZd==.bnRzID==.NDAtYo==.aXQg.Z3L=.b3Vw.cyBvZiA=.aW5w.dXQgYmm=.dHMgYU==.cyBvdY==.dHB1dE==.CiAgIHO=.dHJp.bmdzIM==.b2YgOM==.IGVuY2/=.ZGV=.ZCBjaGF=.cmFjdE==.ZXJ=.cy5=.ICBQcm9=.Y2VlZGl=.bmcgZk==.cm9tIGx=.ZWa=.dCB0.byB=.cml=.Z2h0LCC=.YQogICB=.NDAtYl==.aXQgaR==.bnB=.dXQgZ3I=.b3VwIGl=.cyBmb3J=.bWV=.ZCBieSB=.Y29uYz==.YXRlbmE=.dGlu.ZyA1IM==.OGL=.aXQgaW5=.cHV=.dCA=.Z3K=.b3Vwcy5=.CiAgIA==.VGh=.ZXM=.ZSA0.MCA=.Yml0c6==.IGFy.ZSB0.aGV=.biB0cj==.ZWF0.ZWQgYXP=.IDgg.Y29=.bmNhdD==.ZW5hdJ==.ZWQgNS1=.Yml0II==.Z3JvdV==.cHN=.LCBl.YWNo.CiAgIG/=.ZiB3aGk=.Y2ggaXP=.IHQ=.cmFuc2y=.YXRlZCB=.aW5=.dG8gYSC=.c2luZ2y=.ZSBkaWd=.aXQ=.IGluIHS=.aGUg.YmG=.c2UgM0==.MiBhbB==.cGhh.YmV0Lk==.CiAg.IFdoZW7=.IGVuY5==.b2Rpbmc=.IGEgYmm=.dCC=.c3Ry.ZWFtIHY=.aWEgdM==.aGW=.IGJhc2V=.IDN=.MiBl.bmNvZGm=.bmcsIHQ=.aGV=.IGI=.aXQgc3R=.cmV=.YW0K.ICAgbT==.dXN0IGI=.ZSC=.cHJlc1==.dW1lZCA=.dG8g.YmUgbw==.cmRl.cmX=.ZCD=.d2l0aCB=.dGhlIA==.bW9zdC2=.c2ln.bmlm.aWNhbnS=.LWJpdE==.IGZpcv==.c3QuCk==.ICD=.IFRoYXS=.IGlzLF==.IHQ=.aGX=.IGZpck==.c3R=.IGJp.dCBpbt==.IHRoZSB=.c3Ry.ZWFtIHc=.aWxsIN==.YmUg.dGh=.ZSC=.aGl=.Z2gtbz==.cmRlciA=.Yml0.IGluCt==.ICAgdGh=.ZSBm.aXJz.dCA4Yml=.dCBieV==.dGUsID==.YW5kIJ==.dGg=.ZSBl.aWdo.dGgg.Yml=.dCC=.d2lsbF==.IGK=.ZSB0aB==.ZSBsb3d=.LW9yZH==.ZXIg.Yml0ID==.aW4KICB=.IHRo.ZSA=.Zmk=.cnN0.IDhi.aXQg.Ynl0ZSz=.IGH=.bmQgc0==.byBvbv==.Lgp=.CiAgIEU=.YWNoIDX=.LWJpdCD=.Z3JvdU==.cCBpcy==.IHVzZZ==.ZCBhcyA=.YW4gaW7=.ZGV4IGn=.bnRv.IGFuIGF=.cnJheSA=.b2YgMzL=.IHB=.cmludF==.YWJsZR==.CiAgIE==.Y2hhcmF=.Y3Rl.cnMuIM==.IFT=.aGUgY2==.aGFyYWM=.dGVyIN==.cmVmZXI=.ZW5=.Y2VkIE==.Ynm=.IHRoZSB=.aW5k.ZXg=.IGlzIHA=.bGF=.Y2V=.ZCBp.biB0aD==.ZQogICC=.b3V0.cHV0IF==.c3RyaS==.bmcuIF==.IFRo.ZXNlII==.Y2hh.cmFjdF==.ZXJz.LCB=.aWT=.ZW5=.dGlmaR==.ZWQgad==.biBU.YWJ=.bGUg.Miy=.IGJlbG9=.dywg.YXJlCk==.ICD=.IHNl.bGVjdGU=.ZCA=.ZnL=.b23=.IFVT.LUFTQ0==.SUkgZGk=.Z2m=.dHMgYW6=.ZCB1.cHBlcmN=.YXNlID==.bGV0dGX=.cnMuCl==.CiA=.ICAg.ICAgICC=.ICB=.ICAg.ICB=.ICAgVF==.YWJ=.bGUg.MzogVGh=.ZSBC.YXNlIH==.MzIgQWw=.cGhhYmX=.dAp=.CiAgICC=.ICAg.IFY=.YWx1ZSD=.RW5j.b2Q=.aW5n.ICD=.VmFsdWV=.IEVu.Y29=.ZGlu.ZyAg.VmFsdU==.ZSB=.RW5jb2R=.aW5nIE==.IFZhbE==.dWUgRW==.bmNvZGl=.bmd=.CiAgIB==.ICAgIF==.ICA=.ICB=.IDAg.QSAgIE==.ICAgID==.ICAg.ICAg.OSBKICB=.ICB=.ICAgICB=.ICAgMTh=.IFN=.ICAg.ICAgICB=.ICAg.IDI3.IDMKICA=.ICAgICB=.ICAgIF==.IDEg.QiA=.ICD=.ICAgIE==.ICAgICA=.MTAgSyC=.ICB=.ICAg.ICAgICA=.IDG=.OSD=.VCAgIE==.ICD=.ICAg.ICB=.ICAyOD==.IDQKICD=.ICAg.ICB=.ICAgICA=.MiBD.ICD=.ICAgIN==.ICAg.ICAg.MTEgTD==.ICAgICD=.ICAgIE==.ICAgMv==.MCBVIE==.ICAg.ICAgICD=.ICAgMt==.OSA1.CiAg.ICAg.ICAg.ICAgID==.MyBEICD=.ICAg.ICAgICB=.ICA=.MTI=.IE0gICC=.ICAg.ICC=.ICAgIE==.MjEg.ViAgIJ==.ICAgICB=.ICB=.ICAzMCB=.NgogICB=.ICAgIF==.ICAg.ICA0.IEUg.ICB=.ICAgICC=.ICAgIDF=.MyBOIA==.ICD=.ICAgIE==.ICA=.ICAgMl==.MiA=.VyAgIL==.ICB=.ICAgICB=.ICAz.MSA3Ck==.ICAgIE==.ICAg.ICAgIL==.IDUgRk==.ICAgICD=.ICAgIN==.ICAg.MTR=.IE9=.ICAg.ICC=.ICB=.ICAg.ICAyMyB=.WAog.ICAgIH==.ICB=.ICAgIG==.IDYgRx==.ICAgICA=.ICA=.ICAgICB=.MTUgUE==.ICAg.ICAg.ICAgICC=.IDI0IFn=.ICAgIF==.ICAgICB=.KHBh.ZCk=.ID0K.ICAgICB=.ICAgICA=.ICC=.NyBIII==.ICAgIC==.ICAg.ICAgIDG=.NiBRIE==.ICAgIO==.ICB=.ICAgICB=.MjUgWgq=.ICAgICC=.ICAg.ICAg.IDh=.IEkgICB=.ICAgICB=.ICA=.ICB=.MTcgUk==.ICAgICD=.ICAg.ICB=.ICAyNiA=.MgoK.CiAgIFM=.cGVjaU==.YWwgcM==.cm+=.Y2Vzc2l=.bmcg.aXMgcGU=.cmZvcm3=.ZWQ=.IGlm.IGZl.d2VyIHR=.aGF=.biA0MCB=.Yml0cyA=.YXJ=.ZSBhdmE=.aWxhYmx=.ZQog.ICB=.YXQgdGh=.ZSA=.ZW4=.ZCC=.b2Z=.IHRoZSB=.ZGF0YSC=.YmVpbl==.ZyBlbmM=.b2RlZI==.LiAgQSB=.ZnVsbCA=.ZW5=.Y29k.aW5nIHG=.dWE=.bnR1bSD=.aXMKICD=.IGF=.bHdheXM=.IGNv.bXBsZf==.dGVkIGF=.dCB0.aGUg.ZW5kID==.b2Yg.YSBi.b2R5Lt==.ICBXaGU=.biBm.ZXdl.ciB0aGE=.biA0MK==.IGlucE==.dXT=.IGJp.dHMK.ICAgYY==.cmUg.YXb=.YWls.YWJ=.bGUg.aW4gYW5=.IGl=.bnB1dF==.IGdyb1==.dXA=.LCB6ZX==.cm8gYl==.aXRz.IGE=.cmUg.YWRkZWT=.IChvbl==.IHS=.aGUg.cmlnaHR=.KQogIF==.IHR=.byBm.b3I=.bSB=.YW4gaW4=.dGVncq==.YWwg.bnVt.YmVyIG9=.ZiA1LWI=.aXQgZ/==.cm9=.dXBz.LiAgUGF=.ZGRp.bmcg.YXQ=.IHRoZSC=.ZW5kIG9=.Zgp=.ICAgdD==.aGUgZF==.YXRhIH==.aXMgcGV=.cmZvcm0=.ZWQg.dXNp.bmcgdGi=.ZSAiPSJ=.IGNo.YXJh.Y3Rlci5=.ICBTaS==.bmNl.IGF=.bGwgYk==.YXN=.ZSAz.MgogICA=.aW5wdXR=.IGlz.IGFuIE==.aW4=.dGVncg==.YWwg.bnVt.YmVyIG+=.ZiBv.Y3Rl.dHMsIG+=.bmx5IE==.dGhlIGb=.b2xs.b3f=.aW5nIE==.Y2G=.c2Vz.IGN=.YW5=.CiB=.ICBh.cmlzZR==.Ogp=.CiA=.ICB=.KDH=.KSB0aGV=.IGZ=.aW5hbD==.IHF1YW4=.dHVtIG/=.ZiBlbmM=.b2Rp.bmf=.IGlucE==.dXQgaU==.cyBh.biBpbk==.dGX=.Z3JhbF==.IG11.bHRpcD==.bGUg.b2YgNDB=.CiAgIF==.Yml=.dHO=.OyB=.aGV=.cmV=.LCB0.aGUg.ZmluYR==.bCB1.bml0IG==.b2YgZW6=.Y29kZT==.ZCBv.dXRwdXT=.IHd=.aWw=.bCBiZSD=.YW4gaW7=.dGVnck==.YWwKICD=.IG11.bHRp.cGz=.ZSBvZiB=.OCBj.aGFyYWM=.dGVy.cyD=.d2l0.aCD=.bm8gIj1=.IiBw.YWQ=.ZGluZyw=.CgoKCq==.CgpK.b3N=.ZWY=.c3P=.b24gIF==.ICAgIB==.ICAgICC=.ICB=.ICB=.ICAgIH==.IElu.Zm9y.bWF0.aW9u.YWwgICB=.ICAg.ICAgICA=.ICB=.ICAgIB==.ICAgICB=.W1BhZ3==.ZSA3.XQp=.DApSRkM=.IDM1NDi=.ICAg.ICBUaF==.ZSBC.YXNlMR==.Niwg.QmFzZTM=.MiwgYW5=.ZCBCYS==.c2U2NCC=.RGF=.dGEg.RW5jbz==.ZGluZ3O=.ICAg.ICBKdV==.bHkgMp==.MDAzCgp=.CiAgICh=.Mik=.IHR=.aGUgZml=.bmFs.IHF1YW4=.dHVtIG+=.ZiBlbmM=.b2Rpbk==.ZyBpbn==.cHU=.dCBpc8==.IGV4.YWP=.dGw=.eSA4IGL=.aXRz.OyBoZT==.cmUs.IHR=.aGUKID==.ICC=.Zml=.bmFsID==.dW5p.dCBvZl==.IGVu.Y29kZWR=.IG9=.dXT=.cHV0IHc=.aWz=.bCD=.YmUgdHd=.byBjaGE=.cmFj.dGVyc/==.IGZvbGx=.b3c=.ZWQg.Ynkgc/==.aXgK.ICB=.ICI9IiA=.cGFk.ZGn=.bmcgY2j=.YXJhY3R=.ZXJzLD==.Cgog.ICAoMyn=.IHR=.aGUgZj==.aW5hbCD=.cXVhbnR=.dW0gb2Y=.IGVuYy==.b2S=.aW5nIGl=.bnB1dB==.IGlz.IGV4YV==.Y3RseSA=.MTYg.Yml0cy==.OyBoZV==.cmUsIJ==.dGh=.ZQogIB==.IGZpbmH=.bCB1.bml=.dCB=.b2Yg.ZW6=.Y29kZV==.ZCBvdW==.dHB=.dXQg.d2l=.bGwg.YmUg.Zm91.ciBjaGE=.cmH=.Y3Q=.ZXJzIGZ=.b2xsb3c=.ZWQg.YnkgZm9=.dXIK.ICAgIh==.PSIg.cGE=.ZGRpbmf=.IGNoYXJ=.YWN0ZXJ=.cywKCl==.ICC=.ICg0KV==.IHRo.ZSBmaa==.bmFsIHE=.dWFudN==.dW0=.IG9mIGU=.bmP=.b2Rpbt==.ZyBpbnA=.dXQgaf==.cyBleGF=.Y3Rs.eSAyNCA=.Ymn=.dHM7.IGj=.ZXJl.LCB=.dGhlCiA=.ICBmaW7=.YWz=.IHVu.aXQg.b2Yg.ZW5j.b2Rl.ZCBv.dXRw.dXR=.IHdpbA==.bCBiZSC=.Zml2ZZ==.IGM=.aGFyYWN=.dGW=.cnN=.IGZvbE==.bG93.ZWQgYnl=.CiAgIF==.dGhyZWU=.ICI9Il==.IHA=.YWRkaW5=.ZyBjaN==.YXJh.Y3RlcnN=.LCA=.b3IKCk==.ICAgKDX=.KSB0aGU=.IGZpbs==.YWz=.IHF1.YW4=.dHVtIN==.b2YgZW==.bmNvZB==.aW4=.ZyBpbnD=.dXR=.IGlzIGV=.eGFj.dGx5.IDMyIGJ=.aXRz.OyBoZW==.cmUs.IHRoZQo=.ICAg.Zmn=.bmFsIHU=.bml0IG/=.ZiB=.ZW5jbx==.ZGVkIN==.b3V0cC==.dXQgd8==.aWxsIP==.YmV=.IHNl.dmVu.IGNoYXI=.YWN0.ZXJzIGb=.b2xsb3f=.ZWQgYnl=.IG9uZT==.CiAg.ICI9IiD=.cGFk.ZGluZ0==.IGNoYXI=.YWN0Za==.ci4KCjZ=.LiAgQj==.YXP=.ZSAx.NiB=.RW5jb2Q=.aW5nCgq=.ICAg.VGhlIGZ=.b2xsb1==.d2luZ3==.IGRl.c2N=.cmk=.cHRpb24=.IGlzIG/=.cmln.aW5=.YWwg.YnU=.dCBhbh==.YWw=.b2dvdXP=.IHRvIC==.cHJldk==.aW/=.dXMK.ICA=.IGRlc2N=.cmlw.dGlvbnN=.LiAgRV==.c3N=.ZW50aWE=.bGx=.eSwg.QmFzZSB=.MTYgZW5=.Y29kaQ==.bmcgaZ==.cyB0aF==.ZSB=.c3R=.YW5kYXJ=.ZCBz.dGFuZGG=.cmQKIB==.ICBjYS==.c2U=.IGluc2U=.bnNpdP==.aXZlIE==.aGX=.eCBl.bmP=.b2Rpbmd=.LCBhbj==.ZCBtYd==.eSBiZSA=.cmVm.ZXI=.cmVkIK==.dG9=.IGFz.ICJiYR==.c2V=.MTYiIE==.b3IK.ICA=.ICJo.ZXi=.Ii4KCiB=.ICBB.IDF=.Ni1jaJ==.YXJhY0==.dGVyIHN=.dWJz.ZXQg.b2b=.IFV=.Uy1BU0M=.SUkgab==.cyB1.c2U=.ZCwgZW7=.YWJ=.bGluZyA=.NCBi.aXRzIHR=.byB=.YmUKIE==.ICBy.ZXBy.ZXNlbnR=.ZWQ=.IHBlcu==.IHBy.aW50.YWJsZU==.IGNoYe==.cmFjdE==.ZXIuCm==.CiA=.ICBUaM==.ZSC=.ZW5jb2R=.aW5nIC==.cHJv.Y2U=.c3Mgck==.ZXByZZ==.c2VudHN=.IDgt.Yml0IGd=.cm+=.dXC=.cyAob2N=.dGV0cyk=.IG9mIM==.aW5wdXR=.IGI=.aXR=.cwog.ICBhc0==.IG8=.dXRw.dXS=.IHN0.cmluZ3O=.IG9mIDJ=.IGU=.bmNv.ZGVk.IGNo.YXJhY3R=.ZXJz.LiC=.IFByb1==.Y2VlZGk=.bmcg.ZnJ=.b20g.bGV=.ZnQgdE==.bwp=.ICAg.cmlnaE==.dCx=.IGH=.IDgt.Yml=.dCBp.bnB1dG==.IGlz.IHRha2V=.biBmcj==.b20gdGg=.ZSC=.aW5=.cHV0ID==.ZGF0YS4=.ICB=.VGhlc2U=.IDj=.IGJp.dHMgYXI=.ZQogIE==.IHRoZd==.biB0.cmVh.dGVkIGF=.cyAyIF==.Y29uY1==.YXR=.ZW4=.YXRlZCB=.NC1i.aXQgZ0==.cm9=.dXBzLJ==.IGU=.YWM=.aCC=.b2Ygdz==.aGljaN==.IGk=.cwog.ICB0.cmH=.bnNs.YXRlZCD=.aW50byB=.YSBzaT==.bmdsZSD=.ZGl=.Z2l0IGk=.biB0aC==.ZSBiYZ==.c2UgMT==.NiBhbHB=.aGFiZXR=.LgoK.ICAg.RWFjaF==.IDQtYp==.aXQg.Z3Jv.dXAgaXN=.IHW=.c2VkIJ==.YXMg.YW4g.aW5kZS==.eCBp.bnRvIGE=.biB=.YXJyYR==.eSB=.b2YgMT==.NiBwci==.aW50YU==.Ymxl.CiAgIM==.Y2h=.YXJh.Y3Rlcj==.cy7=.ICBUaGV=.IGM=.aGFyYd==.Y3RlciB=.cmV=.ZmV=.cmV=.bmNlZF==.IGJ5IB==.dGhlIE==.aW5=.ZGV4IF==.aXMgcGw=.YWNlZF==.IGluIHQ=.aGX=.CiB=.ICBv.dXQ=.cHV0.IHN0cml=.bmcu.CgogICB=.ICAgIE==.ICAgICB=.ICAg.ICA=.ICBUYWK=.bGUgNZ==.OiBUaD==.ZSBCYXN=.ZSAxNl==.IEFscGg=.YWJldI==.Cgog.ICAgICD=.VmFsdWX=.IEVuY0==.b2Rpbv==.ZyAg.VmF=.bHVlID==.RW5jb2T=.aW5=.ZyA=.IFZhbHX=.ZSD=.RW5=.Y29k.aW4=.ZyAgVv==.YWx1.ZSBFbk==.Y29kaf==.bmd=.CiAg.ICA=.ICA=.ICAg.IDAgMCC=.ICAgICC=.ICAg.ICAg.IDQgNE==.ICAgICD=.ICAgICB=.ICAgOD==.IDggIF==.ICAg.ICB=.ICB=.ICAgMT==.MiBDCl==.ICA=.ICAgIN==.ICAgIDF=.IDG=.ICAgICB=.ICB=.ICAgIC==.ICB=.NSA1IE==.ICAgICB=.ICAgIB==.ICA=.IDm=.IDm=.ICAg.ICB=.ICAg.ICA=.ICD=.MTMgRAq=.ICAgIF==.ICAgICC=.IDIgMl==.ICAg.ICAg.ICAg.ICAgIDZ=.IDYgIB==.ICAgIE==.ICAg.ICAg.MTAgQW==.ICB=.ICA=.ICAgIJ==.ICAgIDE=.NCD=.RQp=.ICAgICB=.ICAgICA=.MyD=.MyAgID==.ICB=.ICA=.ICAgIK==.ICA3.IDcg.ICB=.ICAg.ICAg.ICAgMTE=.IEL=.ICC=.ICAgID==.ICAg.ICAgMT==.NSA=.Rgr=.CiAg.IFVubN==.aWtl.IGJhcz==.ZSD=.MzIgYU==.bmQgYmH=.c2UgNjT=.LCBu.byB=.c3A=.ZWNp.YWwgcGH=.ZGT=.aW5nIGl=.cyA=.bmVj.ZXNzYf==.cnkg.c2luY0==.ZSBhCv==.ICAgZnV=.bGwgY28=.ZGUgdy==.b3JkIGm=.cyB=.YWw=.d2F=.eXMgYV==.dmE=.aWxh.Ymw=.ZS4KCp==.CgoKCko=.b3NlZk==.c3NvbiB=.ICAg.ICAgIB==.ICAgIN==.ICAgICA=.ICAgST==.bmZvcj==.bWE=.dGlvbt==.YWwgICA=.ICB=.ICAgIB==.ICA=.ICAgIN==.ICAgICB=.ICBbUD==.YWf=.ZSA4XQp=.DApSRj==.QyAzNTR=.OCAgIF==.ICBUaH==.ZSBCYXN=.ZTE2LCA=.QmFz.ZTM=.Miwg.YW5k.IEJhc9==.ZTY=.NCA=.RGF0YU==.IEVu.Y29kaf==.bmd=.cyA=.ICAg.IEp1bHn=.IDIw.MDMKCgr=.Ny4gIE==.SWxs.dXN0.cmF0af==.b25zIGF=.bmQg.ZXhh.bXA=.bGU=.cwoKICC=.IFRvIHS=.cmFuc2x=.YXRlIC==.YmV0d2W=.ZW4gYml=.bmE=.cnkgYW5=.ZCC=.YSBi.YXNlIF==.ZW4=.Y29kad==.bmc=.LCB0aH==.ZSBp.bnB1.dCBpcyB=.c3Rvcg==.ZWT=.CiA=.ICBp.biBhIHP=.dHJ1Yy==.dHVyZSB=.YW5k.IHRo.ZSA=.b3V0cHV=.dCBpcx==.IGV4.dHJhY0==.dGVk.LiA=.IFRo.ZSB=.Y2E=.c2Ug.Zm9=.ciC=.YmFzZV==.IDY0IB==.aXMK.ICAg.ZGlzcGx=.YXl=.ZWQgaR==.biB=.dGhlIGY=.b2x=.bG93.aW5=.ZyBmaT==.Z3X=.cmUsIE==.Ym9ycv==.b3dlZE==.IGb=.cm9tIN==.WzRd.LgoKID==.ICAgICD=.ICB=.ICs=.LS0=.Zmly.c3Qg.b2O=.dGV0LZ==.LSst.c2Vj.b25k.IG8=.Y3RldL==.LS0rLV==.LXRoaXJ=.ZCBvY3S=.ZXQt.LSt=.CiAgIG==.ICAgIB==.ICB8.NyA2IDU=.IDR=.IDMgMt==.IDEgME==.fDcgNs==.IDX=.IDQgM1==.IDIg.MSAw.fDcg.NiA1.IDQgM0==.IDIg.MSAw.fAogICB=.ICAgIB==.ICArLR==.LS0t.LS2=.LS1=.LS0tKy0=.LS3=.Ky0tLS1=.LS0t.Ky1=.LS0tLU==.LS0rLS1=.LSt=.LS0t.LS0t.LS0tLU==.LSt=.CiAg.ICB=.ICAgIB==.IHz=.NSA0.IDMg.MiAx.IDB8NSA=.NCAzIDL=.IDEgMHz=.NSA0.IDN=.IDIg.MSA=.MHw1IDT=.IDMgMiD=.MSAwfE==.CiD=.ICAgICD=.ICAg.Ky1=.LTEuaT==.bmRleC3=.LSst.LTIu.aW5kZU==.eC0tKy==.LS0zLp==.aW5kZXg=.LS2=.Ky0tNN==.Lmlu.ZGV4.LS0r.Cgog.ICBUaD==.ZSBjYXO=.ZSBmb3I=.IGJhc8==.ZSAzMp==.IGlzIB==.c2hvd27=.IGluIHR=.aGUgZm8=.bGw=.b3dpbs==.ZyBmaWf=.dXJlLF==.IGJvcnJ=.b3dlZCA=.ZnJ=.b20=.CiAgIE==.WzZdLiB=.IEVh.Y2ggc3W=.Y2Nlc0==.c2l2ZSD=.Y2hh.cmFj.dGX=.ciBpbiB=.YSBiYT==.c2UtM1==.MiB2.YWx=.dWW=.IHI=.ZXB=.cmVzZW4=.dHMgNQp=.ICAgc8==.dWNjZf==.c3Npdk==.ZSBiaf==.dHMgb0==.ZiB0.aGUg.dW5k.ZXL=.bHlp.bmcg.b2P=.dGV0IHN=.ZXE=.dWVuY/==.ZS4gIE==.VGh1cy==.LCBl.YWO=.aCB=.Z3JvdR==.cAp=.ICAgb2Z=.IDg=.IGNo.YXI=.YWN0.ZXJzIF==.cmV=.cHJ=.ZXNl.bnRzIGG=.IHNlcXV=.ZW4=.Y2Ug.b2Yg.NSBv.Y3RldHN=.ICg0MCB=.Yml0c0==.KS4K.CiB=.ICAgICB=.ICB=.ICAg.ICAg.ICAgICB=.ICA=.ICAgMSB=.ICAgICB=.ICAg.IDIg.ICAgICA=.ICC=.ICAzCt==.ICAg.ICAg.ICAgIDB=.MTIzNDV=.Njcg.ODk=.MDEy.MzR=.NSA2Nzg=.OTAx.MjMgNJ==.NTY3.ODkwMSB=.MjM0NV==.Njd=.ODkKIF==.ICB=.ICAg.ICAg.Ky2=.LS0tLS1=.LS0rLQ==.LS3=.LS1=.LS0t.Ky0=.LS0t.LS0tLSs=.LS0tLS1=.LS0tK0==.LS0t.LS0t.LS0rCiC=.ICAg.ICAg.ICD=.fDwg.MSA+PCB=.Mnwg.Pjwg.MyA+.PHx=.LjQgPk==.PCB=.NS58Pjw=.IDYgPjy=.Lnw3IM==.PjwgOCA=.PnwK.ICAgICC=.ICC=.ICB=.Ky0tLT==.LS3=.LS1=.LSt=.LS0t.LS0tLW==.LSstLS1=.LS0t.LS1=.Ky0t.LS0tLX==.LS0rLS1=.LS0tLW==.LS0rCiA=.ICB=.ICA=.ICAgICA=.ICAgIF==.ICAg.ICA=.ICAgIL==.ICB=.ICB=.ICAgIE==.ICB=.ICAgICA=.ICAg.ICAg.ICAgICC=.PD09PZ==.PiA4dD==.aCBjaJ==.YXJhY3R=.ZXIKIK==.ICAgIF==.ICB=.ICAg.ICAg.ICAg.ICAg.ICAgIB==.ICAgICB=.ICAg.ICAg.ICAgICA=.ICAgIN==.PD09PQ==.PT4gN1==.dGh=.IGNoYXK=.YWN0ZV==.cgogICB=.ICB=.ICAgICA=.ICAg.ICB=.ICAgICA=.ICAgICB=.ICAgIJ==.ICAgICA=.ICAg.IDz=.PT09.PiA2.dGggY2h=.YXJhY3R=.ZXIK.ICA=.ICAg.ICAgIO==.ICAgIF==.ICA=.ICAgIF==.ICAgICB=.ICAgIH==.ICAg.IDw9PT==.PT0=.PiD=.NXRoID==.Y2hhcmH=.Y3Rlcgp=.ICAg.ICA=.ICAgIP==.ICAgICB=.ICAg.ICAgID==.ICAgICD=.PD09PT1=.PiA0dA==.aCC=.Y2hhcmG=.Y3Rlcgp=.ICAg.ICAgID==.ICAgICB=.ICAgICB=.ICAgIDx=.PT09.PiAz.cmQgY1==.aGFy.YWN0ZXJ=.CiAgIE==.ICAgICB=.ICAg.ICB=.ICA8PT0=.PT0+.IDJuZH==.IGNoYXJ=.YWN=.dGV=.cgr=.ICAgICA=.ICD=.ICAg.PD09PT==.PiAxc3R=.IGN=.aGF=.cmE=.Y3R=.ZXJ=.CgoKCg==.CgoKCgp=.CgoKCgo=.CgoK.CgoKCv==.Ckpv.c2Vmcz==.c29=.biAgIF==.ICAgIG==.ICAgIB==.ICAgIA==.ICAgICD=.SW5mb0==.cm1hdB==.aW9u.YWwg.ICAgID==.ICAgIF==.ICAgIE==.ICAgIH==.ICAgID==.IFtQYd==.Z2UgOV0=.Cgw=.ClJG.QyC=.MzU0.OCAg.ICC=.IFRo.ZSBCYXN=.ZTE2LCA=.QmFz.ZTMy.LCBh.bmQgQu==.YXM=.ZTY0IN==.RGE=.dGEgRV==.bmNv.ZGluZ3M=.ICAgIF==.IEo=.dWx5II==.MjB=.MDMKCi==.CiB=.ICBUaD==.ZSA=.Zm9sbG+=.d2lu.ZyBleE==.YW1wbGV=.IG9m.IEI=.YXNlNjR=.IGRhdB==.YSBpc5==.IGZyb20=.IFs0XS5=.CgogIF==.ICAgICA=.SW4=.cHV0IGS=.YXRh.OiAgMHg=.MTRmYjn=.YzAzZDk=.N2UKICD=.ICAgIF==.IEhl.eDogICC=.ICB=.MSAg.IDQg.ICA=.IGYgICD=.YiAgIN==.IDkgICA=.YyAgICD=.IHwg.MCD=.ICAzIE==.ICD=.IGQgIN==.IDkgICA=.IDf=.ICAg.ZQogIN==.ICA=.ICAg.OC0=.Yml0OiC=.ICAwMJ==.MDE=.MDH=.MDAg.MTExMTG=.MDF=.MSA=.MTAwMW==.MTEw.MCB=.IHwgME==.MDAwMN==.MDExIB==.MTEwMTH=.MDAxCk==.ICC=.ICAgICD=.MTExMT==.MTExME==.CiB=.ICAg.ICAgNi1=.Yml0Oi==.ICB=.IDAwMDE=.MDEgMDA=.MTExMV==.IDEwMTE=.MTAg.MDExMTD=.MCB8IN==.MDAwMDA=.MCAxMTE=.MTAxIDG=.MDA=.MTExCiD=.ICAgICA=.IDEx.MTEx.MAq=.ICAg.ICB=.ICBEZWN=.aW1hbDp=.IDX=.ICAgIE==.ICB=.MTV=.ICA=.ICAgNM==.NiD=.ICAg.IDI4.ICAgICB=.ICAwIB==.ICAg.ICA2MSA=.ICAg.IDN=.NyA=.ICC=.ICA2Mgq=.ICAgICA=.ICBPdXQ=.cHV0OiC=.IEYgICC=.ICAgUCB=.ICAgID==.IHUg.ICAg.ICBjICB=.ICAgIE==.ICBBIN==.ICAgICB=.OSAgIE==.ICAgbF==.ICAg.ICAgKx==.CgogICD=.ICAgIE==.SW5w.dXR=.IGRhdGF=.OiAgMHg=.MTRmYjn=.YzAz.ZDl=.CiAgICC=.ICAgSE==.ZXg6.ICC=.ICAgMSC=.ICA0.ICB=.ICBmICA=.IGI=.ICB=.ICA5IE==.ICBjICD=.ICAg.fCB=.MCAgIF==.MyAgICA=.ZCAgIJ==.OQogIE==.ICAgIN==.IDgt.Yml0OiB=.ICC=.MDA=.MDEw.MTAwIE==.MTE=.MTEx.MDEx.IDF=.MDAxMTE=.MDAgIM==.fCC=.MDAwMF==.MDAxMSA=.MTE=.MDEx.MDA=.MQr=.ICD=.ICAg.ICB=.ICAgICA=.ICA=.ICAg.ICC=.ICAgICC=.ICAg.ICAgIE==.ICAg.ICAgICD=.ICAgICB=.ICAg.ICB=.ICA=.ICAgIO==.cGFkIHc=.aXT=.aCA=.MDC=.CiAg.ICAgICB=.Ni1iaR==.dDog.ICAwMN==.MDEwMU==.IDAw.MTExMSD=.MTAxMTE=.MCAwMc==.MTH=.MDA=.IHwgMDD=.MDA=.MDD=.IDEx.MTF=.MDEgMTA=.MDEwMP==.CiAgICB=.ICAg.RGVjaT==.bWFsOt==.IDUgID==.ICAgIDF=.NSAgIF==.ICA0.NiAgIB==.ICAyOCB=.ICAg.ICAgMCA=.ICB=.ICAg.NjEg.ICAgIM==.MzYKICD=.ICB=.ICC=.ICAgICB=.ICAgICB=.ICAgICC=.ICC=.ICAgICB=.ICAgIE==.ICAg.ICAgICC=.ICAgICB=.ICAg.ICAgICA=.ICAgIB==.IHB=.YWQ=.IHdp.dGggPQp=.ICAgICC=.ICBP.dXRwdU==.dDq=.ICBGICC=.ICAg.IFAgIE==.ICAgIC==.dSAgIE==.ICAgYyB=.ICA=.ICAg.ICBBICA=.ICD=.ICA5.ICAgIN==.ICBrICA=.ICD=.ICA9Cgr=.ICAgIE==.ICAgSW7=.cHX=.dCBkYU==.dGE6ICD=.MHgxNN==.ZmI5Yw==.MDMKIK==.ICAgICB=.IEhleDo=.ICAgICC=.MSAgIF==.NCAgIB==.IGYg.ICBi.ICAgIDm=.ICB=.IGMgICA=.ICB8.IDAgICC=.MwogIJ==.ICB=.ICAgOC1=.Yml0OiB=.ICB=.MDAwMTA=.MTAw.IDExMTG=.MTAxMSD=.MTAwMU==.MTEwML==.ICB8.IDAw.MDAwMDF=.MQp=.ICAg.ICAg.ICAgIC==.ICAgICB=.ICA=.ICAg.ICAgICA=.ICAgICB=.ICB=.ICA=.ICB=.ICAgICC=.ICAg.ICBwYWR=.IHc=.aXS=.aCAw.MDAw.CiAgICC=.ICAg.Ni1i.aXQ6ICB=.IDAwMF==.MTC=.MSAwME==.MTG=.MTEgMTA=.MTF=.MTAgMC==.MTExMM==.MCD=.fCA=.MDD=.MDAwMCB=.MTEwMDA=.MAr=.ICAg.ICAgIEQ=.ZWN=.aW1h.bDp=.IDUg.ICAg.ICAx.NSA=.ICAgIF==.NDYg.ICAgIB==.MjggICC=.ICAg.IDB=.ICAg.ICA=.IDQ4Cq==.ICAgIF==.ICAgICB=.ICAgICB=.ICAgIF==.ICAgICA=.ICAgIM==.ICD=.ICAgICD=.ICAgIE==.ICAg.ICAgICD=.ICAgIN==.IHBh.ZCA=.d2l0aP==.ID0gIE==.ICAgIP==.PQogIE==.ICAgICA=.T3V0cHW=.dDogIEa=.ICB=.ICAgID==.UCAg.ICAgIHW=.ICAg.ICAgY1==.ICAgICC=.ICAgQSC=.ICAgIF==.IHcgIE==.ICAgIF==.PSAg.ICAgID==.PQp=.Cjg=.LiA=.IFNl.Y3V=.cml0eSA=.Q29uc8==.aWS=.ZXJhdE==.aW/=.bnM=.Cgp=.ICAgVz==.aGVuIN==.aW1wbB==.ZW1lbl==.dGluZw==.IEJhc5==.ZSBlbk==.Y29=.ZGluZyB=.YW5k.IGRlY0==.b2Rp.bmf=.LCBjYU==.cmU=.IHNob3V=.bGQ=.IGJl.IHRh.a2Vu.CiAgIM==.bm90.IHRvIN==.aW50cm9=.ZHVj.ZSB2.dWxuZXJ=.YWJpbGk=.dGll.cyB=.dG8gYnV=.ZmZ=.ZXIgb3a=.ZXJmbE==.b3cgYe==.dHRh.Y2t=.cyx=.IG9yIG==.b3RoZXJ=.CiAgIE==.YXS=.dGFj.a3Mgb25=.IHRoZR==.IGlt.cGxlbd==.ZW50YXQ=.aW9uLr==.ICBBIGQ=.ZWP=.b2Rl.ciBz.aG91bGT=.IG5v.dCBick==.ZWH=.ayD=.b24gaU==.bnZhbP==.aWR=.CiAgIA==.aW5wda==.dCBpbmN=.bHU=.ZGlu.Zywg.ZS5n.Liwg.ZW1iZWT=.ZGX=.ZCB=.TlU=.TCBj.aGFyYWO=.dGVycyB=.KEFTQ0l=.SSAw.KS4KCiB=.ICBJ.ZiA=.bm9uLWF=.bHBoYWJ=.ZXQg.Y2hhcmE=.Y3R=.ZXL=.cyA=.YXJl.IGlnbt==.b3JlZCy=.IGluc1==.dGVh.ZCBv.ZiBjYa==.dXNp.bmcgcmV=.amVjdGl=.b24KIC==.ICBv.ZiB0aGV=.IGVudGk=.cmUg.ZW4=.Y29k.aW5=.ZyAoYXN=.IHI=.ZWNv.bW1lbt==.ZGVkKU==.LCBhIG==.Y292ZV==.cnQgYy==.aGF=.bm5lbG==.IHRoYR==.dCA=.Y2FuIGK=.ZQp=.ICAgdXM=.ZWQgdM==.byAibJ==.ZWE=.ayL=.IGlu.Zm9ybR==.YXRpb25=.IGlz.IG1h.ZGU=.IHA=.b3Nz.aWJs.ZS4=.ICBUaC==.ZSBp.bXC=.bGljYXR=.aW9ucyA=.b2YKICD=.IHRo.aXMg.c2hvdZ==.bGQgYmV=.IHVu.ZGVy.c3Rvb5==.ZCBpbl==.IGE=.cHBsaWN=.YXRpb0==.bnMgdH==.aGF0.IGRvIG4=.b3QgZs==.b2xsb3e=.IHRoZT==.CiAg.IHI=.ZWNvbW3=.ZW5k.ZWQ=.IHD=.cmFjdGk=.Y2Uu.ICBTaW3=.aWx=.YXJseV==.LCB3aN==.ZW4gdGg=.ZSBiYe==.c2V=.IDE2.IGE=.bmR=.IGJhc5==.ZSAz.MgogICB=.YWxw.aGFi.ZXRzID==.YXJlIGh=.YW5=.ZGw=.ZWQgY2H=.c2UgaT==.bnNlbnP=.aXRp.dmV=.bHksIGE=.bHT=.ZXJh.dGn=.b24g.b2Yg.Y2FzZU==.IGP=.YW4g.YmX=.CiAgIE==.dXNl.ZCB0byD=.bGVha9==.IGluZm8=.cm1hdGk=.b24uCgq=.ICAgQp==.YXNl.IGVuYz==.b2Rpbmf=.IHZpc3V=.YWw=.bHkgaGn=.ZGVzIG9=.dGhl.cndpc1==.ZSBlYR==.c2l=.bHkgcmU=.Y29nbn==.aXp=.ZWQgaW4=.Zm8=.cm3=.YXQ=.aW9u.LAogICD=.c3U=.Y2ggYXP=.IHBhc3N=.d29yZHN=.LCBi.dXQgZE==.b2VzIE==.bm9=.dCBwcl==.b3Zp.ZGUgYR==.bnl=.IGN=.b21wdQ==.dGG=.dGk=.b25h.bAogICD=.Y29u.ZmlkZW4=.dGlhbN==.aXR5Lk==.ICBUaI==.aXP=.IGhhc9==.IGJlZT==.biD=.a25vd25=.IHRvIGM=.YXVzZf==.IHNlY0==.dXL=.aXR5.IGluY9==.aWRlbnQ=.cwogIC==.IHdo.ZW4sIJ==.ZS5nLiw=.IGEgdXP=.ZXJ=.IHJlcE==.b3J=.dHO=.IGR=.ZXR=.YWm=.bHMgb5==.ZiB=.YSBuZT==.dHdv.cmsgcE==.cm8=.dG9=.Y29sIGV=.eGNoYW5=.Z2UKCgq=.Ckq=.b3NlZl==.c3Nvbk==.ICAgIE==.ICB=.ICAgIJ==.ICA=.ICAgIN==.ICAgIE==.SW5mb3J=.bWF0aW+=.bmE=.bCAgIM==.ICAgICC=.ICB=.ICAg.ICA=.ICAg.ICAg.W1C=.YWdl.IDE=.MF0K.DAp=.UkZD.IDM=.NTS=.OCAgIM==.ICD=.VGh=.ZSBC.YXM=.ZTE2LF==.IEJhc2V=.MzIsIGE=.bmQgQmF=.c2U2NB==.IERhdGG=.IEVuY0==.b2Rp.bmdzICD=.ICAg.SnVseV==.IDIwME==.MwoK.CiAgICi=.cGVyaGE=.cHMgdP==.byB=.aWxs.dXN0cmE=.dGUg.c29t.ZSD=.b3RoZd==.ciBwcm8=.Ymxl.bSkgYW7=.ZCBh.Y2Np.ZGVudGH=.bGx5IE==.cmV2.ZWFs.cwogIP==.IHR=.aGUg.cGFz.c3c=.b3JkIGL=.ZWNhdd==.c2Ugc2g=.ZSBp.cyD=.dW5h.d2FyZSD=.dGhhdCB=.dGg=.ZSBi.YXNlIGU=.bmNvZK==.aW5=.ZyBk.b2VzIG4=.b3R=.CiAgIHB=.cm90ZU==.Y3QgdC==.aGUgcF==.YXNzd29=.cmQuCgp=.OS4gIF==.UmVmZX==.cmU=.bmP=.ZXMK.Cjku.MS4g.IE5vck==.bWF0.aXZ=.ZSBS.ZWZl.cmVuYy==.ZXMK.CiAgIF==.WzFd.IEJy.YWRuZXI=.LCBTLk==.LCAi.S2V5.IHdvcl==.ZHMgZm9=.ciB=.dXNlIGl=.biBSRj==.Q3MgdG+=.IEluZE==.aWNh.dGUgUmU=.cXVp.cmVtZW6=.dAogIF==.ICAg.ICBMZXY=.ZWxzIiz=.IEJDUCB=.MTQs.IFJGQ0==.IDL=.MTE5.LCBNYXJ=.Y2gg.MTk=.OTcu.Cgo=.OS4y.LiAgSV==.bmZvcm0=.YXT=.aXZ=.ZSBS.ZWZlcmV=.bmNlcwp=.CiAgIC==.WzJdIF==.TGlu.biwg.Si4=.LCAiUHJ=.aXZh.Y3kgRQ==.bmhhbmO=.ZW1lbnS=.IGZvciB=.SW50ZR==.cm5ldN==.IEVsZR==.Y3R=.cm8=.bmljIE3=.YWlsOi==.CiAgICB=.ICAg.UGFydA==.IEn=.OiBN.ZXNzYWd=.ZSBFbmM=.cnlw.dGlvbiA=.YW5kIEF=.dXRoZV==.bnRpY6==.YXRpb0==.biB=.UHJv.Y2U=.ZHVyZV==.cyIsIA==.UkZDCiB=.ICAgICA=.IDH=.NDIxLCB=.RmVick==.dWH=.cnkgMY==.OTn=.My4KCiA=.ICBbM5==.XSBG.cmVlZF==.LCD=.Ti4g.YW5kIE4=.LiBCb8==.cmVuc5==.dGVp.biwgIm==.TXVs.dGlwdZ==.cnBv.c2Ug.SW50.ZXI=.bmV0IE3=.YWls.CiAgIB==.ICA=.ICD=.RXj=.dGV=.bnNpb24=.cyAo.TUlNRSn=.IFBh.cnQg.T25l.OiBGb9==.cm1=.YXQgb2Y=.IEl=.bnRlcm4=.ZXQgTWX=.c3Nh.Z2UgQm/=.ZGllc0==.IiwKICD=.ICD=.ICB=.IFJG.QyAyMDQ=.NSwgTv==.b3ZlbU==.YmVy.IDE5Of==.Ni4K.CiAgIFt=.NF0=.IENhbP==.bGFzLCB=.Si4s.IERvbj==.bmVyaGH=.Y2tlLE==.IEwu.LCA=.Rmm=.bm5leZ==.LCBILiA=.YW7=.ZCBS.LiB=.VGh=.YXll.ciwg.Ik9wZW4=.UEdQCiB=.ICAg.ICC=.IE1=.ZXNzYW==.Z2W=.IEZvck==.bWG=.dCIs.IFI=.RkMgMl==.NDQ=.MCwg.Tm/=.dmV=.bWJlci==.IDE5OV==.OC4KCiA=.ICBb.NV0gRWE=.c3T=.bGFr.ZSwg.RC4sICJ=.RG9tYV==.aW4gTmE=.bWV=.IFN5cz==.dGVt.IFNl.Y3Vyad==.dHl=.IEV4dG==.ZW5zaV==.b25z.Iiy=.IFJGQyA=.MjUzNSx=.CiAg.ICA=.ICA=.IE1hcmN=.aCAx.OTk5.LgoKICA=.IFs2.XSD=.S2x5bt==.ZSw=.IEcuIP==.YW5k.IEwu.IE1hc2l=.bnRlciw=.ICL=.SWRl.bnRpZnn=.aW5=.ZyA=.Q2/=.bXBvc9==.aXRlIA==.TWVk.aWEK.ICAg.ICAgIK==.RmVh.dHV=.cmVzIj==.LCBSRkP=.IDI5.MzgsIE==.U2VwdO==.ZW1iZXJ=.IDJ=.MDAwLl==.Cgog.ICBb.N11=.IE15.ZXJzLCA=.Si4sIH==.IlNBU0x=.IEdTU0==.QVBJIM==.bWVjaGH=.bmk=.c21zIt==.LCB=.V29=.cmsgaR==.biBQcm8=.Z3Jlc2==.cy5=.Cgo=.ICB=.IFs4XSB=.V2lsY0==.b3g=.LU8n.SGVh.cm4sIJ==.Qi4=.LCC=.IlBv.c3S=.IHRvIF==.UDJQLWi=.YWNr.ZXJzIG0=.YWls.aW5n.IGxpc0==.dCK=.LCBXb3L=.bGQ=.CiAgICD=.ICAgV2l=.ZGUgV2U=.YiB=.aHQ=.dHA6L0==.L3p=.Z3Aubx==.cmcvcJ==.aXA=.ZXJtYWn=.bC9wMt==.cC1oYWM=.a2Vycy+=.MjAwMS1=.CiA=.ICAgIP==.ICBTZXB=.dGU=.bWL=.ZXL=.LzAwMDN=.MTUuaHQ=.bWws.IFNlcP==.dGV=.bWJlcj==.IDL=.MDB=.MS4KCj==.ICAg.Wzn=.XSBDZU==.cmb=.LCBW.LiwgIt==.QVNDSQ==.SSBm.b3Jt.YXQg.Zm9yIK==.TmV=.dHdvcms=.IElu.dGX=.cmNoYW6=.Z2UiLF==.IFJGQyB=.MjAsIJ==.T2N0b2J=.ZXIKICA=.ICAgIF==.IDE5Nl==.OS4KCjH=.MC4=.ICBB.Y2tub3f=.bGVkZ2V=.bWVudB==.cwo=.CiAg.IFNldmX=.cmE=.bCB=.cGV=.b3BsZR==.IG9mZk==.ZXJlZCC=.Y2/=.bW1=.ZW50.cyBhbg==.ZCBz.dWe=.Z2V=.c3Rp.b25zLCA=.aW5jbK==.dWR=.aW5nIF==.VG9u.eQp=.ICB=.IEg=.YW5zZW6=.LCA=.R29y.ZG9uIE1=.b2g=.ciwgSm+=.aG4gTXl=.ZXJzLD==.IENocml=.cyB=.TmV3bU==.YW5=.LCBhbmQ=.IEFu.ZHJldyB=.U2llYmV=.ci4K.ICA=.IFRleF==.dCB1cz==.ZWQg.aW4gdN==.aGk=.cyD=.ZG9=.Y3U=.bWVudN==.IGlzIF==.YmFz.ZWQgb24=.IGVhcj==.bGll.ciA=.Ukb=.Q3N=.IGS=.ZXNjcml=.Ymk=.bmcKIM==.ICBzcGV=.Y2lm.aWMg.dXNlcyB=.b2a=.IHZhck==.aW91cyD=.YmH=.c2UgZW5=.Y29kaW4=.Z3MuIC==.IFRoZZ==.IGF1.dGg=.b3IgYd==.Y2tub1==.d2xl.ZGdlcyB=.dGi=.ZQp=.ICB=.IFK=.U0EgTB==.YWJvcg==.YXT=.b3JpZT==.cyBmb0==.ciBz.dXBwbz==.cnRpbmd=.IHR=.aGUg.d29y.ayB0.aGE=.dCBsZc==.ZCB0byD=.dGhpcyB=.ZG9jdS==.bWVudC6=.CgoKCgp=.Cko=.b3Nl.ZnP=.c29u.ICC=.ICAgIE==.ICAgIO==.ICAgICB=.ICAgICB=.SW5mb1==.cm1=.YXR=.aW9u.YWwgII==.ICAg.ICB=.ICAg.ICAgIA==.ICAgIE==.ICAg.W1BhZ2X=.IDH=.MV0KDE==.ClL=.RkMg.MzX=.NDh=.ICA=.ICAgVP==.aGUgQmF=.c2U=.MTYsIEI=.YXNl.MzIs.IGG=.bmQg.QmFzZTa=.NCBEYXR=.YSA=.RW5jb2T=.aW5n.cyAg.ICAgSnV=.bHkgMjB=.MDMKCgp=.MTF=.LiAgRWS=.aXR=.b3IncyB=.QWRkcj==.ZXNzCk==.CiAgIFN=.aW1vbiD=.Sm9=.c2Vmc3N=.b24=.CiD=.ICB=.RU1=.YWlsOiC=.c2l=.bW9u.QGpvc0==.ZWZz.c29uLq==.b3JnCgp=.CgoKCj==.CgoKCt==.CgoKCj==.CgoKCgq=.CgoK.CgoKCgo=.Cgr=.CgoK.CgoKCgp=.Cgp=.CgoKCl==.CgoKCgq=.Sm9z.ZWZzc5==.b24gIA==.ICAgICB=.ICAg.ICAg.ICAgICA=.ICBJ.bmZv.cm3=.YXRp.b25hbN==.ICA=.ICAg.ICAgICD=.ICAgIN==.ICAgICA=.ICBb.UGFnZf==.IDEyXU==.CgwKUkb=.QyD=.MzU0.OCAg.ICB=.IFRoZQ==.IEJhc6==.ZTE2LCB=.QmFzZT==.MzIs.IGFuZE==.IEL=.YXNlNjR=.IEQ=.YXRhIEV=.bmNv.ZGluZ2==.cyAgICA=.IEp1bF==.eSAyMDC=.Mwo=.CgoxMi5=.ICBG.dWw=.bCBD.b3B5.cmlnaHT=.IFP=.dGF0ZT==.bWVu.dAoKIC==.ICBDb0==.cHly.aWf=.aHQ=.IChDKU==.IFRoZc==.IEludE==.ZXJu.ZXQg.U2/=.Y2m=.ZXR5IE==.KDJ=.MDAz.KS4g.IEFs.bCBSaWd=.aHRz.IFJlc2V=.cnZlZG==.LgoK.ICAgVGg=.aXN=.IGRvY0==.dW1l.bnQg.YW5k.IHRy.YW5=.c2xhdGk=.b27=.cyBvZiD=.aXQg.bWF=.eSBiZSA=.Y29waWX=.ZCBhbmT=.IGZ1ck==.bmlz.aGVk.IHRvCv==.ICAg.b3RoZXJ=.cywgYT==.bmQgZGX=.cml2.YXR=.aXZlIA==.d29ya3O=.IHRoYXS=.IGNv.bW1=.ZW50IG8=.biBvcp==.IG90aGV=.cnc=.aXNlIGW=.eHBs.YWluIJ==.aXQ=.CiA=.ICBvcl==.IGFzc2l=.c3QgaW==.biBpdHN=.IGltcB==.bGVt.ZW50YXT=.aW9=.biBtYXl=.IGI=.ZSBwcmW=.cGFy.ZWR=.LCBjby==.cGn=.ZWQs.IHB1Yj==.bGlzaH==.ZWR=.CiAgID==.YW6=.ZCBk.aXN0.cmlidU==.dGW=.ZCwgaY==.biB3.aG9sZc==.IG+=.ciBpbl==.IHBhcn==.dCwgd2k=.dGhv.dXQg.cmVzdHL=.aWM=.dGlvbiC=.b2YgYT==.bnkK.ICAga0==.aW5kLE==.IHB=.cm92aWQ=.ZWQgdE==.aGF0IK==.dGhlIGE=.Ym8=.dmW=.IGNvcJ==.eXI=.aWdodO==.IG5vdF==.aWNlIK==.YW5=.ZCB=.dGhpcyB=.cGFyYR==.Z3JhcE==.aCBh.cmUKICB=.IGl=.bmN=.bHVkZWR=.IG9uIE==.YWxs.IHN1Y/==.aCBjb0==.cGn=.ZXP=.IGFuZCB=.ZGVyaT==.dmF0aXb=.ZSB3b3J=.a3MuIA==.IEhvd6==.ZXZlcg==.LCB0.aGlzCg==.ICAgZG8=.Y3U=.bWVudCA=.aXRz.ZWxmIA==.bWF5IA==.bm90IA==.YmUgbQ==.b2Rp.Zmk=.ZWQ=.IGluIA==.YW4=.eSB3.YXksIA==.c3VjaCA=.YXMgYnk=.IHI=.ZW1v.dmluZw==.CiA=.ICB0aA==.ZSBj.b3B5cmk=.Z2h0.IG5v.dGljZQ==.IG8=.ciByZWY=.ZXI=.ZW5jZXM=.IHRvIHQ=.aGU=.IEludGU=.cm4=.ZXQgUw==.b2Np.ZXR5IG8=.ciBv.dGhlcg==.CiAgIEk=.bnRlcg==.bmV0.IG8=.cmdhbmk=.emE=.dGlvbnM=.LCBleGM=.ZXA=.dCBh.cyBu.ZWVk.ZWQgZm8=.ciB0aGU=.IHB1.cnBv.c2U=.IG9mCiA=.ICBkZQ==.dmU=.bG9waW4=.ZyBJ.bnRlcm4=.ZXQgc3Q=.YW4=.ZGE=.cmRzIA==.aW4g.d2hpY2g=.IGNhc2U=.IHQ=.aGUgcHI=.b2NlZA==.dXJlcw==.IGZvcgo=.ICAgYw==.b3B5cmk=.Z2h0cyA=.ZGVm.aW4=.ZWQg.aW4gdGg=.ZSBJ.bnRl.cm5ldA==.IFN0YQ==.bmRhcg==.ZHMgcHI=.b2Nlcw==.cyA=.bXVzdCA=.YmUK.ICAgZg==.b2xsb3c=.ZWQs.IG9yIA==.YXM=.IHJlcXU=.aXI=.ZWQ=.IHRvIHQ=.cmFu.c2xhdGU=.IGl0IA==.aW4=.dG8gbGE=.bmc=.dWFnZXM=.IG90aGU=.ciB0aA==.YW4KICA=.IEU=.bmds.aXNo.LgoK.ICA=.IFQ=.aGU=.IGxpbWk=.dGVkIA==.cGU=.cm1pc3M=.aW9ucyA=.Z3JhbnQ=.ZWQgYQ==.Ym92.ZSBh.cmUgcGU=.cnBl.dHVhbA==.IGFuZCA=.d2ls.bCBub3Q=.IGJlCg==.ICAgcmU=.dm8=.a2VkIA==.Ynk=.IHRoZSA=.SW50.ZXJuZQ==.dCBTb2M=.aWV0.eSA=.b3I=.IGl0cyA=.c3U=.Y2M=.ZXNzb3I=.cyBvciA=.YXNzaQ==.Z25lZXM=.LgoKIA==.ICBUaA==.aXMgZA==.b2N1.bWVudCA=.YW4=.ZCB0.aGUg.aW5mbw==.cm0=.YXRpbw==.biBjbw==.bnRhaW4=.ZWQg.aGVyZQ==.aW4g.aXMgcA==.cm92aQ==.ZGVkIG8=.biA=.YW4K.ICAg.IkFT.IElT.IiA=.YmFz.aXMg.YW5kIFQ=.SEU=.IEk=.TlRFUk4=.RVQgU08=.Q0lFVA==.WSBBTg==.RCBU.SEUgSQ==.TlRFUg==.TkVUIA==.RU5HSU4=.RUVS.SU5HCiA=.ICBU.QVM=.SyBGTw==.UkNFIEQ=.SVNDTA==.QUk=.TVMg.QUxM.IFc=.QVJSQQ==.TlRJRQ==.Uywg.RVhQUkU=.U1MgT1I=.IElN.UExJ.RUQs.IElO.Q0xVRA==.SU5HCg==.ICA=.IEJV.VCA=.Tk9UIA==.TElNSVQ=.RUQgVE8=.IEFO.WSBXQQ==.UlJBTg==.VFkgVA==.SEFU.IFQ=.SEUgVVM=.RSA=.T0Y=.IFRIRQ==.IEk=.TkZPUg==.TUFUSU8=.Tgog.ICA=.SEVS.RUlOIA==.V0k=.TEwg.Tk8=.VCBJ.TkZSSU4=.R0Ug.QU5ZIFI=.SUdI.VFMg.T1Ig.QU5ZIA==.SU0=.UExJ.RUQg.V0FS.UkFOVEk=.RVM=.IE8=.Rgog.ICA=.TUVSQ0g=.QU5U.QUI=.SUxJ.VFkgTw==.UiBGSVQ=.TkU=.U1MgRk8=.UiA=.QSBQQQ==.UlRJ.Q1U=.TEFSIFA=.VVJQTw==.U0UuCg==.CkFja24=.b3dsZWQ=.Z2VtZQ==.bnQ=.Cgog.ICA=.RnVuZA==.aW5n.IGZv.ciA=.dGhlIA==.UkZD.IEU=.ZGl0bw==.ciBmdQ==.bmN0.aW9u.IGk=.cyBj.dXJyZQ==.bnRseQ==.IHBy.b3ZpZGU=.ZCBieQ==.IHRo.ZQog.ICA=.SW50ZQ==.cm5l.dCBTbw==.Y2ll.dHk=.LgoKCg==.CgoKCgo=.Cgo=.CgoKCgo=.Cgo=.CgoKSm8=.c2U=.ZnNzbw==.biA=.ICAgICA=.ICAgICA=.ICA=.ICAg.ICAgIA==.SW5m.b3JtYXQ=.aW9uYWw=.ICAgICA=.ICAgIA==.ICAg.ICA=.ICAg.ICA=.ICBbUA==.YWdlIA==.MTM=.XQo=.DAo=
Native Digest                   : 256,257,258,259,262,274,277,284,530,531,282,283,296,301,318,319,529,532,306,270,271,272,305,315,33432;B368EA75AC056F096408B89BC3910BAB
Creator Tool                    : Adobe Photoshop CS3 Windows
Metadata Date                   : 2012:04:26 20:23:24+03:00
Date Time                       : 2012:04:26 20:23:24
Date/Time Digitized             : 2012:05:18 10:03:28
Subsec Time                     : 00
Flash Pix Version               : FlashPix Version 1.0
Interoperability Index          : R98
Interoperability Version        : 0100
Format                          : image/jpeg
Color Mode                      : RGB
ICC Profile Name                : sRGB IEC61966-2.1
History                         : 
Instance ID                     : uuid:4F23BC69C48FE11187D7ED1DDF4DBD3B
Document ID                     : uuid:4E23BC69C48FE11187D7ED1DDF4DBD3B
Profile CMM Type                : Linotronic
Profile Version                 : 2.1.0
Profile Class                   : Display Device Profile
Color Space Data                : RGB
Profile Connection Space        : XYZ
Profile Date Time               : 1998:02:09 06:49:00
Profile File Signature          : acsp
Primary Platform                : Microsoft Corporation
CMM Flags                       : Not Embedded, Independent
Device Manufacturer             : Hewlett-Packard
Device Model                    : sRGB
Device Attributes               : Reflective, Glossy, Positive, Color
Rendering Intent                : Perceptual
Connection Space Illuminant     : 0.9642 1 0.82491
Profile Creator                 : Hewlett-Packard
Profile ID                      : 0
Profile Copyright               : Copyright (c) 1998 Hewlett-Packard Company
Profile Description             : sRGB IEC61966-2.1
Media White Point               : 0.95045 1 1.08905
Media Black Point               : 0 0 0
Red Matrix Column               : 0.43607 0.22249 0.01392
Green Matrix Column             : 0.38515 0.71687 0.09708
Blue Matrix Column              : 0.14307 0.06061 0.7141
Device Mfg Desc                 : IEC http://www.iec.ch
Device Model Desc               : IEC 61966-2.1 Default RGB colour space - sRGB
Viewing Cond Desc               : Reference Viewing Condition in IEC61966-2.1
Viewing Cond Illuminant         : 19.6445 20.3718 16.8089
Viewing Cond Surround           : 3.92889 4.07439 3.36179
Viewing Cond Illuminant Type    : D50
Luminance                       : 76.03647 80 87.12462
Measurement Observer            : CIE 1931
Measurement Backing             : 0 0 0
Measurement Geometry            : Unknown
Measurement Flare               : 0.999%
Measurement Illuminant          : D65
Technology                      : Cathode Ray Tube Display
Red Tone Reproduction Curve     : (Binary data 2060 bytes, use -b option to extract)
Green Tone Reproduction Curve   : (Binary data 2060 bytes, use -b option to extract)
Blue Tone Reproduction Curve    : (Binary data 2060 bytes, use -b option to extract)
Image Width                     : 1024
Image Height                    : 680
Encoding Process                : Progressive DCT, Huffman coding
Bits Per Sample                 : 8
Color Components                : 3
Y Cb Cr Sub Sampling            : YCbCr4:4:4 (1 1)
Aperture                        : 8.0
Image Size                      : 1024x680
Megapixels                      : 0.696
Scale Factor To 35 mm Equivalent: 1.5
Shutter Speed                   : 1/2000
Create Date                     : 2012:05:18 10:03:28.00
Date/Time Original              : 2012:05:18 10:03:28.00
Modify Date                     : 2017:08:02 12:34:15.00
Thumbnail Image                 : (Binary data 8498 bytes, use -b option to extract)
Flash                           : No Flash
Circle Of Confusion             : 0.020 mm
Field Of View                   : 67.4 deg
Focal Length                    : 18.0 mm (35 mm equivalent: 27.0 mm)
Hyperfocal Distance             : 2.02 m
Light Value                     : 15.0

~~~

This can be exported to a text file:

~~~shell
$ exiftool ch15.jpg > data.txt
~~~

This file can be opened and the comments can be extracted and decoded in Python:

~~~py
import base64 as b64

filename = "ch15.txt"
f = open(filename,"r")
txtstr = f.read()
f.close()
txtstr = txtstr.split("Native")[0].split("Comment")[-1].split("\n")[0].split(":")[1]

b64arr = txtstr.split(".")
asciiarr = []

for val in b64arr:
    asciiarr.append(b64.b64decode(val).decode())
    
asciistr = "".join(asciiarr)

f = open("ch15decoded.txt","w")
f.write(asciistr)
f.close()
~~~

This shows the comments are base64 encoded copy of RFC 3548.  The bits can be extracted to base32 using unhide_bits function.  When decoded, this provides a wikipedia page on base jumping.  Extracting again, the ascii flag can be found.  Full Python code:

~~~py
#!/usr/bin/env python3
# -*- coding: utf-8 -*-

import base64 as b64
import math
from tinyscript import *

DEF_BASE64 = "ABCDEFGHIJKLMNOPQRSTUVWXYZabcdefghijklmnopqrstuvwxyz0123456789+/"
DEF_BASE32 = "ABCDEFGHIJKLMNOPQRSTUVWXYZ234567"

def unhide_bits(encoded, charset, pad="=", n_pad=8):
    def __gcd(a,b):
        while b > 0:
            a, b = b, a % b
        return a
    padding = encoded.count(b(pad))
    n_repr = int(math.ceil(math.log(len(charset), 2)))
    w_len  = n_repr * n_pad / __gcd(n_repr, n_pad)
    n_char = int(math.ceil(float(w_len) / n_repr))
    if encoded == "" or len(encoded) % n_char != 0 or padding == 0:
        return
    unused = {n: int(w_len - n * n_repr) % n_pad for n in range(n_char)}
    b_val  = bin(b(charset).index(encoded.rstrip(b(pad))[-1]))[2:].zfill(n_repr)
    return b(b_val[-unused[padding]:])

filename = "ch15.txt"
f = open(filename,"r")
txtstr = f.read()
f.close()
txtstr = txtstr.split("Native")[0].split("Comment")[-1].split("\n")[0].split(":")[1]

b64arr = txtstr.split(".")
asciiarr1 = []
asciiarr2 = []

for val in b64arr:
    asciiarr1.append(b64.b64decode(val).decode())
    
asciistr = "".join(asciiarr1)

f = open("ch15decoded.txt","w")
f.write(asciistr)
f.close()

bitstr = b""

for val in b64arr:
    bitstr += unhide_bits(val.encode(),charset=DEF_BASE64) or b("")

b32str = b("").join(ts.bin2str(bitstr[i:i+8]) for i in range(0, len(bitstr), 8))
b32arr = b32str.strip(b"\x00").decode().split("\n")

bitstr = b""
for val in b32arr:
    bitstr += unhide_bits(val.encode(),charset=DEF_BASE32) or b("")

asciistr = b("").join(ts.bin2str(bitstr[i:i+8]) for i in range(0, len(bitstr), 8))
asciistr = asciistr.strip(b"\x00").decode()

print(asciistr)
~~~


</details>

### Answer

<details>

<summary markdown="span">Answer</summary>

~~~
3v3ry0ne_h4s_s3cr3ts!
~~~

</details>

---

### [Steganography](#contents) | [Root-Me](./rootme.md) | [Home](./index.md)

---

Last updated Jan 2022.

## [djm89uk.github.io](https://djm89uk.github.io)
