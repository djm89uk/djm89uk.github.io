# [Root-Me](./rootme.md) Root-Me Steganography [15/23]

The art of hiding information in a document. 

## Contents

1. [EXIF Metadata](#exif-metadata) 🗸
2. [Gunnm](#gunnm) 🗸
3. [Squared](#squared) 🗸
4. [Dot and next line](#dot-and-next-line) 🗸
5. [Steganomobile](#steganomobile) 🗸
6. [Twitter Secret Messages](#twitter-secret-messages) 🗸
7. [Some noise](#some-noise) 🗸
8. [George and Alfred](#george-and-alfred) 🗸
9. [Poem from Space](#poem-from-space) 🗸
10. [Yellow dots](#yellow-dots) 🗸
11. [Audio stegano](#audio-stegano) 🗸
12. [Mimic - Dummy sight](#mimic-dummy-sight)
13. [We need to go deeper](#we-need-to-go-deeper) 🗸
14. [APNG - Just A PNG](#apng-just-a-png) 🗸
15. [Base Jumper](#base-jumper) 🗸
16. [ELF x64 - Duality](#elf-x64-duality)
17. [Hide and seek](#hide-and-seek)
18. [PDF Object](#pdf-object) 🗸
19. [Angecryption](#angecryption)
20. [Kitty spy](#kitty-spy)
21. [LSB - Uncle Scrooge](#lsb-uncle-scrooge)
22. [Pixel Indicator Technique](#pixel-indicator-technique)
23. [Pixel Value Differencing](#pixel-value-differencing)
24. [Crypt-art](#crypt-art) 🗸

---

### [Steganography](#contents) | [Root-Me](./rootme.md) | [Home](./index.md)

---

## EXIF Metadata

- Author: ISISTM
- Date: 28 March 2022
- Points: 5
- Level: 1

### Statement

Our sad friend pepo got lost! Can you find where he is ?

The password is the city where pepo is located.

### Attachments

1. [ch1.png](http://challenge01.root-me.org/steganographie/ch1/ch1.png)

### Solutions

<details>

<summary markdown="span">Solution 1</summary>

Using exiftool, we can find the gps coordinates of where the photo was taken:

~~~shell
$ exiftool ch1.png 
ExifTool Version Number         : 11.88
File Name                       : ch1.png
Directory                       : .
File Size                       : 13 kB
File Modification Date/Time     : 2022:03:28 09:29:00+01:00
File Access Date/Time           : 2022:04:17 22:45:32+01:00
File Inode Change Date/Time     : 2022:04:17 22:45:32+01:00
File Permissions                : rw-rw-r--
File Type                       : PNG
File Type Extension             : png
MIME Type                       : image/png
Image Width                     : 96
Image Height                    : 96
Bit Depth                       : 8
Color Type                      : RGB with Alpha
Compression                     : Deflate/Inflate
Filter                          : Adaptive
Interlace                       : Noninterlaced
SRGB Rendering                  : Perceptual
Gamma                           : 2.2
Pixels Per Unit X               : 3779
Pixels Per Unit Y               : 3779
Pixel Units                     : meters
Exif Byte Order                 : Big-endian (Motorola, MM)
Image Description               : S0rry_N0_Gu3ss1ng_Gh1zm0!
Resolution Unit                 : inches
Y Cb Cr Positioning             : Centered
Exif Version                    : 0232
Components Configuration        : Y, Cb, Cr, -
Flashpix Version                : 0100
Owner Name                      : ISISTM
GPS Latitude Ref                : North
GPS Longitude Ref               : East
Image Size                      : 96x96
Megapixels                      : 0.009
GPS Latitude                    : 43 deg 17' 56.27" N
GPS Longitude                   : 5 deg 22' 49.38" E
GPS Position                    : 43 deg 17' 56.27" N, 5 deg 22' 49.38" E
~~~

A quick look on [gps-coordinates.net](https://www.gps-coordinates.net/) shows us the city.

</details>

### Answer

<details>

<summary markdown="span">Answer</summary>

~~~
Marseille
~~~

</details>

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
Comment                         : CgoK.CgoKTmV=.dHdv....
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

## PDF Object

- Author: eilco
- Date: 23 July 2017
- Points: 25
- Level: 3

### Statement

Find the hidden information in this PDF file.
Understanding the French language is not needed.

### Attachments

1. [ch11.zip](http://challenge01.root-me.org/steganographie/ch11/ch11.zip).

### Resources

1. [Malicious Origami in PDF](https://repository.root-me.org/St%C3%A9ganographie/EN%20-%20Malicious%20Origami%20in%20PDF%20-%20Raynal%20-%20Delugr%C3%A9.pdf).

### Solutions

<details>

<summary markdown="span">Solution 1</summary>

We can download and uncompress the zip file:
	
~~~shell
$ wget http://challenge01.root-me.org/steganographie/ch11/ch11.zip
--2022-04-28 17:25:34--  http://challenge01.root-me.org/steganographie/ch11/ch11.zip
Resolving challenge01.root-me.org (challenge01.root-me.org)... 212.129.38.224, 2001:bc8:35b0:c166::151
Connecting to challenge01.root-me.org (challenge01.root-me.org)|212.129.38.224|:80... connected.
HTTP request sent, awaiting response... 200 OK
Length: 2164768 (2.1M) [application/zip]
Saving to: ‘ch11.zip.1’

ch11.zip.1                                                  100%[=========================================================================================================================================>]   2.06M  8.09MB/s    in 0.3s    

2022-04-28 17:25:34 (8.09 MB/s) - ‘ch11.zip.1’ saved [2164768/2164768]
$ unzip ch11.zip 
Archive:  ch11.zip
  inflating: epreuve_BAC_2004.pdf 
$ file epreuve_BAC_2004.pdf 
epreuve_BAC_2004.pdf: PDF document, version 1.3
~~~

We can use the PeePDF python tool to inspect the file:

~~~shell
$ peepdf -i epreuve_BAC_2004.pdf 
Warning: PyV8 is not installed!!

File: epreuve_BAC_2004.pdf
MD5: 89d00a355489034dd39ddea2b426fb46
SHA1: be1edb8e45be559388dad27128595daac3d1fae9
SHA256: 579d71aa13b0bf20289bb6beabdbeccff5ccc2776d38a11808e8bed6650d1650
Size: 2388166 bytes
Version: 1.3
Binary: True
Linearized: False
Encrypted: False
Updates: 0
Objects: 78
Streams: 25
URIs: 0
Comments: 0
Errors: 0

Version 0:
	Catalog: 1
	Info: 2
	Objects (78): [1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13, 14, 15, 16, 17, 18, 19, 20, 21, 22, 23, 24, 25, 26, 27, 28, 29, 30, 31, 32, 33, 34, 35, 36, 37, 38, 39, 40, 41, 42, 43, 44, 45, 46, 47, 48, 49, 50, 51, 52, 53, 54, 55, 56, 57, 58, 59, 60, 61, 62, 63, 64, 65, 66, 67, 68, 69, 70, 71, 72, 73, 74, 75, 76, 77, 78]
	Streams (25): [8, 14, 20, 26, 32, 38, 44, 50, 56, 62, 68, 74, 77, 5, 12, 18, 24, 30, 36, 42, 48, 54, 60, 66, 72]
		Encoded (25): [8, 14, 20, 26, 32, 38, 44, 50, 56, 62, 68, 74, 77, 5, 12, 18, 24, 30, 36, 42, 48, 54, 60, 66, 72]
		Decoding errors (25): [8, 14, 20, 26, 32, 38, 44, 50, 56, 62, 68, 74, 77, 5, 12, 18, 24, 30, 36, 42, 48, 54, 60, 66, 72]
	Suspicious elements:
		/Names (1): [1]

~~~

We can see 78 objects and 25 streams.  The first set of streams (8-74) are standard PDF objects with the same structure:

~~~
PPDF> object 8

<< /Filter /FlateDecode
/Length 255189
/ColorSpace /DeviceRGB
/DecodeParms << /Colors 3
/Columns 3488
/Predictor 15 >>
/BitsPerComponent 8
/Height 2480
/Width 3488
/Subtype /Image >>
stream

endstream
~~~

The last set of streams (5-72) are flatencoded integers:

~~~
PPDF> object 72

<< /Length 73 0 R
/Filter /FlateDecode >>
stream

endstream
~~~

Only 1 object seems suspicious, object 77 contains an unknown stream:

~~~
PPDF> object 77

<< /Length 79749
/Type /Embeddedfile
/Filter /FlateDecode
/Params << /Size 108542
/Checksum VY
            ½]¿átâ± >>
/Subtype /text/plain >>
stream

endstream
~~~

We can find the byte offsets for these objects:

~~~
PPDF> offsets

       0 Header
...
 2306406
        Object  77 (79905)
 2386310
 ...
~~~

We can import this data in python and decompress into a new file using zlib:

~~~py
import base64 as b64
import zlib

filename = "epreuve_BAC_2004.pdf"
file = open(filename,"rb")
data = file.read()
file.close()

data = data[2306400:2386400]
data = data[178:-73]
data = zlib.decompress(data)
data = b64.b64decode(data)

filename = "output"
file = open(filename,"wb")
file.write(data)
file.close()
~~~

Inspecting the output, we can see it is a jpg:

~~~shell
$ file output
output: JPEG image data, JFIF standard 1.01, resolution (DPI), density 96x96, segment length 16, comment: "CREATOR: gd-jpeg v1.0 (using IJG JPEG v62), quality = 95", baseline, precision 8, 500x417, components 3
~~~

The jpg can be opened to retrieve the solution.

</details>

### Answer

<details>

<summary markdown="span">Answer</summary>

~~~
Hidden_embedded_Fil3
~~~

</details>

---

### [Steganography](#contents) | [Root-Me](./rootme.md) | [Home](./index.md)

---

## Kitty Spy

- Author: LetMeR00t
- Date: 9 July 2018
- Points: 30
- Level: 3

### Statement

Find the flag of the challenge through this heavy picture.

### Attachments

1. [ch16.jpg](http://challenge01.root-me.org/steganographie/ch16/ch16.jpg).

### Solutions

<details>

<summary markdown="span">Solution 1</summary>

We can download and inspect the jpg:
	
~~~shell
$ wget http://challenge01.root-me.org/steganographie/ch16/ch16.jpg
--2022-04-25 15:06:53--  http://challenge01.root-me.org/steganographie/ch16/ch16.jpg
Resolving challenge01.root-me.org (challenge01.root-me.org)... 212.129.38.224, 2001:bc8:35b0:c166::151
Connecting to challenge01.root-me.org (challenge01.root-me.org)|212.129.38.224|:80... connected.
HTTP request sent, awaiting response... 200 OK
Length: 4354048 (4.2M) [image/jpeg]
Saving to: ‘ch16.jpg’

ch16.jpg                                                    100%[=========================================================================================================================================>]   4.15M  5.51MB/s    in 0.8s    

2022-04-25 15:06:54 (5.51 MB/s) - ‘ch16.jpg’ saved [4354048/4354048]

$ file ch16.jpg 
ch16.jpg: JPEG image data, JFIF standard 1.01, resolution (DPI), density 72x72, segment length 16, progressive, precision 8, 100x67, components 3
~~~

Inspecting the file with strings, we see multiple zip files are contained:

~~~shell
$ strings ch16.jpg 
...
step4/UT
step4/README#4.txtUT
y;"6
step4/kitty.pngUT
K)_c
step1.zipUT
step2.zipUT
step3.zipUT
step4.zipUT
~~~

We can unzip the jpg:

~~~shell
$ unzip ch16.jpg
Archive:  ch16.jpg
warning [ch16.jpg]:  7265 extra bytes at beginning or within zipfile
  (attempting to process anyway)
 extracting: step1.zip               
 extracting: step2.zip               
 extracting: step3.zip               
 extracting: step4.zip 
~~~
	
There are 4 "steps" to solve this.  Step 1:

~~~shell
$ unzip step1.zip 
Archive:  step1.zip
   creating: step1/
  inflating: step1/route.png         
  inflating: step1/README#1.txt
$ cat step1/README#1.txt 
Something is hidden in this picture, I'm pretty sure of this... But what ?
$ exiftool step1/route.png 
ExifTool Version Number         : 11.88
File Name                       : route.png
Directory                       : step1
File Size                       : 659 kB
File Modification Date/Time     : 2017:08:08 06:32:40+01:00
File Access Date/Time           : 2022:04:25 15:09:16+01:00
File Inode Change Date/Time     : 2022:04:25 15:08:51+01:00
File Permissions                : rwxrwx---
File Type                       : PNG
File Type Extension             : png
MIME Type                       : image/png
Image Width                     : 1195
Image Height                    : 688
Bit Depth                       : 8
Color Type                      : RGB
Compression                     : Deflate/Inflate
Filter                          : Adaptive
Interlace                       : Noninterlaced
Pixels Per Unit X               : 2835
Pixels Per Unit Y               : 2835
Pixel Units                     : meters
Comment                         : Hello you :) Just stay on the picture !!
Modify Date                     : 2017:08:07 11:36:27
Image Size                      : 1195x688
Megapixels                      : 0.822
~~~

The picture shows a route from Russie to the USA, to Algeria, to China, to Argentina and to France.  We can try some ISO codes for the password following this route:

~~~
RUACAF - FAIL
RUUSDZCNARFR - FAIL
RUSUSADZACHNARGFRA - FAIL
643840012156032250 - FAIL
~~~

Uploading the image to [stegonline](https://stegonline.georgeom.net/image) we can see text encoded in the LSB of the image. After careful inspection, it can be seen this spells out:

~~~	
f1rstStepi5DoN3
~~~

This unencrypts the second zip file including a wav file:

~~~shell
$ cat README#2.txt 
Well ... Now that we know that, we must find the next step, we success to record a sound from his micro !
Maybe a trap to escape us ? I hope not ! We need to find how to use this sound, EVERYTHING can be a clue ...


Copyright © - 2017 - 18574115dbcd47d71e7eb9da74e45bf2
$ file monster.wav 
monster.wav: RIFF (little-endian) data, WAVE audio, Microsoft PCM, 8 bit, mono 11025 Hz
$ exiftool monster.wav 
ExifTool Version Number         : 11.88
File Name                       : monster.wav
Directory                       : .
File Size                       : 8.8 kB
File Modification Date/Time     : 2017:08:08 06:32:40+01:00
File Access Date/Time           : 2022:04:25 15:40:59+01:00
File Inode Change Date/Time     : 2022:04:25 15:38:38+01:00
File Permissions                : rwxrwx---
File Type                       : WAV
File Type Extension             : wav
MIME Type                       : audio/x-wav
Encoding                        : Microsoft PCM
Num Channels                    : 1
Sample Rate                     : 11025
Avg Bytes Per Sec               : 11025
Bits Per Sample                 : 8
Duration                        : 0.81 s
$ binwalk -Me monster.wav 

Scan Time:     2022-04-25 15:42:15
Target File:   /home/derek/Downloads/step2/monster.wav
MD5 Checksum:  d18a1ab91444fa08a66cd569e02737b1
Signatures:    391

DECIMAL       HEXADECIMAL     DESCRIPTION
--------------------------------------------------------------------------------
~~~
	
The hex string at the end of the README file can be unhashed using the tool at [md5hashing.net](https://md5hashing.net/) to reveal it is an Md5 hash of "meowmeowmeowmeow"  this is not the password for step3.zip.  Using steghide the password can be retrieved:

~~~shell
$ steghide extract -sf step2/monster.wav 
Enter passphrase: meowmeowmeowmeow
wrote extracted data to "step2.txt".
$ cat step2.txt 
passw0rd=s3c0nDSt3pIsAls0D0n3
~~~

The 3rd zip file can now be inflated.  We can inspect the README file:

~~~shell
$ cat README#3 
Wow ... Now we need to find what's hidden in this suspected website, we know that the guy get information from this site ...
BUt WhERe AnD HoW ?
~~~

Interesting letter cases at the end:

~~~
BUt WhERe AnD HoW
BUWERADHW
theno
~~~

Inside the suspected website directory we find teh LICENSE.md file with an interesting code at the end:

~~~
++++++++++[>+>+++>+++++++>++++++++++<<<<-]>>>-----.>++++++++..<<++.>>+++++++++++++.----------.++++++.<<.>>-------.---------..-.<<.>>++++++++++++++++.-----.<<.>>----.+++.+.++++++++.<<.>>--------------.++++++++++.<<.>>+.------------.-------.+++++++++++++++++++.<<.>>+++++.----------.++++++.<<.>>++.--------------.+++..<<.>>----.-------.+++++++++++++++++++++.-----------------.<<.>>+++++++++++++++.-----.<<.>>---------.+++.+++++.----------.<<.>>---.<<.>++++++++++++++++.+.---------------.>++++++++++++++.-----------.+.<<.>>+++++++++++++++.-----.<<.>>-------.-------.+++++++++++++++++++++.-----------------.<<.>>+++++++++++++++.------------.---.<<.>>+.++++++.-----------.++++++.<<.+.
~~~

This is brainfk and can be compiled and executed using an online tool at [tutorialspoint](https://www.tutorialspoint.com/execute_brainfk_online.php) resulting in:

~~~
$bfi main.bf
All you need to know is that you will have to find a QRCode to have the flag !
~~~

On the index.html webpage, an interesting comment:

~~~
You just have to know that the hidden message is not using numbers ! You have to skip them :) 
~~~

In the webpage source code:

~~~
"Do you know the difference between a "C" and a "c" ? ... It could help you !"
~~~

And in the README file:

~~~
QRCode - It's very funny to hide a QRCode in a picture ... you just have to apply 1-LSB on a pixel color to hide it ...
~~~

So perhaps we are looking for a QR Code?
	
</details>

### Answer

<details>

<summary markdown="span">Answer</summary>

~~~
ARTLOVERSWILLNEVERDIE
~~~

</details>

---

### [Steganography](#contents) | [Root-Me](./rootme.md) | [Home](./index.md)

---

## LSB Uncle Scrooge

- Author: koma
- Date: 21 March 2012
- Points: 30
- Level: 3

### Statement

Uncle Scrooge does not only love gold, seems he also likes secrets. Find what is hidden in the image.

### Attachments

1. [ch9.png](http://challenge01.root-me.org/steganographie/ch9/ch9.png).

### Resources

1. [Pixel Indicator Technique for RGB Image Steganography](https://repository.root-me.org/St%C3%A9ganographie/EN%20-%20Pixel%20Indicator%20Technique%20for%20RGB%20Image%20Steganography%20-%20Adnan%20Abdul%20-%20Aziz%20Gutub.pdf).
2. [Image Steganography Overview](https://repository.root-me.org/St%C3%A9ganographie/EN%20-%20Image%20Steganography%20Overview.pdf).
3. [LSB Steganography](https://repository.root-me.org/St%C3%A9ganographie/EN%20-%20LSB%20Steganography.pdf).

### Solutions

<details>

<summary markdown="span">Solution 1</summary>

We can download and inspect the file:

~~~shell
$ wget http://challenge01.root-me.org/steganographie/ch9/ch9.png
--2022-04-28 18:27:25--  http://challenge01.root-me.org/steganographie/ch9/ch9.png
Resolving challenge01.root-me.org (challenge01.root-me.org)... 212.129.38.224, 2001:bc8:35b0:c166::151
Connecting to challenge01.root-me.org (challenge01.root-me.org)|212.129.38.224|:80... connected.
HTTP request sent, awaiting response... 200 OK
Length: 64218 (63K) [image/png]
Saving to: ‘ch9.png’

ch9.png                                                     100%[=========================================================================================================================================>]  62.71K  --.-KB/s    in 0.04s   

2022-04-28 18:27:25 (1.40 MB/s) - ‘ch9.png’ saved [64218/64218]
$ file ch9.png 
ch9.png: PNG image data, 225 x 225, 8-bit/color RGB, non-interlaced
~~~

We can see the image is a 255x255 pixel 8-bit color RGB PNG image file.  We can look for hints in the file using strings:

~~~shell
$ strings -n 7 -t x ch9.png 
    ad2 apXFoo/
   213c %)EeRhP
   23eb *!k% VQ
   2422 b -cb &
   320b !;ldw)h
   3733 '~<wn2%5
   3d30 m=] 454r
   3f5a b"IJSDq@*
   4598 \QgggSSS
   47a5 w>c7LMa
   497e mooomm}
   5026 tWWWcccooo
   5e69 fZ'\pF_
   6245 jYK"M!+
   6665 R}FB2ox
   67bf (B(u,PR
   70cc oPPR}CDR
   774e qtDB!$1
   8471 Zs&7CnF
   8e49 .T#;)5o
   91e6 ?A<1k3h
   9e91 NG['@0yl
   9ed7 d=6/RQT
   a3f4 3v,HDi`
   a476 BN4\nr(P
   a831 ?[=sw\z
   aad8 O;8@:;k
   aba8 n5l_Dm-
   b019 }cF4zb>9X*g
   b171 S,3888~
   b6a7 V^HEd|+j
   bfbe MRtut5'I
   c0d3 HM#P5,`CHC3
   c257 Kg2Il*Ime
   c493 qLe&)K)
   ccb3 -'"LZfD
   cdc5 ` LP*(U
   d074 S&M&fHu
   d6d5 ROZv>gW
   dd38 v #p3ig
   e4db J@JeXTjE	
   eadb MP	*v"d
   ed1f l|{7c>a
   eeae ,t\(aa -
   ef4f MhC)J4Q
   efbf LHd3Kha
~~~

Nothing of interest here.  Using exiftool, we can look at the specifications for the image for anything suspicious.

~~~shell
$ exiftool ch9.png 
ExifTool Version Number         : 11.88
File Name                       : ch9.png
Directory                       : .
File Size                       : 63 kB
File Modification Date/Time     : 2021:12:10 17:05:19+00:00
File Access Date/Time           : 2022:04:28 18:27:25+01:00
File Inode Change Date/Time     : 2022:04:28 18:27:25+01:00
File Permissions                : rw-rw-r--
File Type                       : PNG
File Type Extension             : png
MIME Type                       : image/png
Image Width                     : 225
Image Height                    : 225
Bit Depth                       : 8
Color Type                      : RGB
Compression                     : Deflate/Inflate
Filter                          : Adaptive
Interlace                       : Noninterlaced
Image Size                      : 225x225
Megapixels                      : 0.051
~~~

Using binwalk, we can see the image uses zlib compression:

~~~shell
$ binwalk ch9.png

DECIMAL       HEXADECIMAL     DESCRIPTION
--------------------------------------------------------------------------------
0             0x0             PNG image, 225 x 225, 8-bit/color RGB, non-interlaced
41            0x29            Zlib compressed data, default compression
~~~

We can use pngcheck to identify the location of the pixel data in the file:

~~~shell
$ pngcheck -vtp7f ch9.png 
File: ch9.png (64218 bytes)
  chunk IHDR at offset 0x0000c, length 13
    225 x 225 image, 24-bit RGB, non-interlaced
  chunk IDAT at offset 0x00025, length 64161
    zlib: deflated, 32K window, default compression
  chunk IEND at offset 0x0fad2, length 0
No errors detected in ch9.png (3 chunks, 57.7% compression).
~~~
	
Using stegolsb, stegdetect, we can extract RGB bit planes from the png to identify possible locations of hidden data.  All 3 bit-0 planes have interesting coding in the top row of pixels and several large squares appear across the lowest 4 bits.
	
</details>

### Answer

<details>

<summary markdown="span">Answer</summary>

~~~

~~~

</details>

---

### [Steganography](#contents) | [Root-Me](./rootme.md) | [Home](./index.md)

---

## Crypt Art

- Author: m31z0nyx
- Date: 11 December 2011
- Points: 35
- Level: 3

### Statement

A police unit intercepted a message from a terrorist group. This message may contain a secret key used to encrypt other communications. They need you to decrypt it !

### Attachments

1. [ch8.ppm](http://challenge01.root-me.org/steganographie/ch8/ch8.ppm).

### Solutions

<details>

<summary markdown="span">Solution 1</summary>

We can download and inspect the ppm file:
	
~~~shell
$ wget http://challenge01.root-me.org/steganographie/ch8/ch8.ppm
--2022-04-25 14:56:53--  http://challenge01.root-me.org/steganographie/ch8/ch8.ppm
Resolving challenge01.root-me.org (challenge01.root-me.org)... 212.129.38.224, 2001:bc8:35b0:c166::151
Connecting to challenge01.root-me.org (challenge01.root-me.org)|212.129.38.224|:80... connected.
HTTP request sent, awaiting response... 200 OK
Length: 10513 (10K) [application/octet-stream]
Saving to: ‘ch8.ppm’

ch8.ppm                                                     100%[=========================================================================================================================================>]  10.27K  --.-KB/s    in 0s      

2022-04-25 14:56:54 (167 MB/s) - ‘ch8.ppm’ saved [10513/10513]

$ file ch8.ppm 
ch8.ppm: Netpbm image data, size = 70 x 50, rawbits, pixmap
~~~

The encrypted password can be retrieved from the image using strings:

~~~shell
$ strings ch8.ppm 
70 50
  Hi! Welcome to  
esoteric programming!
The encrypted pass is:  
EPCQFBXKWURQCTXOIPMNV
 Bienvenue a la program
mation esoterique!
Le pass encrypte est
EPCQFBXKWURQCTXOIPMNV
~~~

We need a key to decipher the password.  The key can be retrieved using [npiet online](https://www.bertnase.de/npiet/npiet-execute.php) providing: EYJFRGTT
	
We can decipher using an [online deciphering tool](https://www.dcode.fr/vigenere-cipher) to provide the password ARTLOVERSWILLNEVERDIE
	
</details>

### Answer

<details>

<summary markdown="span">Answer</summary>

~~~
ARTLOVERSWILLNEVERDIE
~~~

</details>

---

### [Steganography](#contents) | [Root-Me](./rootme.md) | [Home](./index.md)

---

Last updated Jan 2022.

## [djm89uk.github.io](https://djm89uk.github.io)
