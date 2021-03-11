# [PicoGym](./picogym.md) Web Exploitation

Web Exploitation entails the manipulation of websites and web hosted services using vulnerabilities in the interactive elements of a website.

## Contents

- [Insp3ct0r](#insp3ct0r)
- [logon](#logon)
- [where are the robots](#where-are-the-robots)
- [dont-use-client-side](#dont-use-client-side)
- [Web Gauntlet](#web-gauntlet)
- [picobrowser](#picobrowser)
- [Client-side-again](#client-side-again)
- [Irish-Name-Repo 1](#irish-name-repo-1)
- [Irish-Name-Repo 2](#irish-name-repo-2)
- [Irish-Name-Repo 3](#irish-name-repo-3)
- [JaWT Scratchpad](#jawt-scratchpad)
- [Java Script Kiddie](#java-script-kiddie)
- [Java Script Kiddie 2](#java-script-kiddie-2)

---

### [Web Exploitation](#contents) | [PicoGym](./picogym.md) | [PicoCTF](./picoctf.md) | [Home](./index.md)

---

## Insp3ct0r

- Author: zaratec/danny
- 50 Points

### Description

Kishor Balan tipped us off that the following code may need inspection: https://jupiter.challenges.picoctf.org/problem/9670/ ([link](https://jupiter.challenges.picoctf.org/problem/9670/)) or http://jupiter.challenges.picoctf.org:9670

### Hints

1. How do you inspect web code on a browser?
2. There's 3 parts

### Solutions

<details>

<summary markdown="span">Solution 1</summary>

We can visit the website and inspect the source code:

~~~html
<!doctype html>
<html>
  <head>
    <title>My First Website :)</title>
    <link href="https://fonts.googleapis.com/css?family=Open+Sans|Roboto" rel="stylesheet">
    <link rel="stylesheet" type="text/css" href="mycss.css">
    <script type="application/javascript" src="myjs.js"></script>
  </head>

  <body>
    <div class="container">
      <header>
	<h1>Inspect Me</h1>
      </header>

      <button class="tablink" onclick="openTab('tabintro', this, '#222')" id="defaultOpen">What</button>
      <button class="tablink" onclick="openTab('tababout', this, '#222')">How</button>
      
      <div id="tabintro" class="tabcontent">
	<h3>What</h3>
	<p>I made a website</p>
      </div>

      <div id="tababout" class="tabcontent">
	<h3>How</h3>
	<p>I used these to make this site: <br/>
	  HTML <br/>
	  CSS <br/>
	  JS (JavaScript)
	</p>
	<!-- Html is neat. Anyways have 1/3 of the flag: picoCTF{tru3_d3 -->
      </div>
      
    </div>
    
  </body>
</html>
~~~

This gives us the first part of the flag, "picoCTF{tru3_d3".  Inspecting the stylesheet, mycss.css, we can find the second part of the flag:

~~~css
div.container {
    width: 100%;
}

header {
    background-color: black;
    padding: 1em;
    color: white;
    clear: left;
    text-align: center;
}

body {
    font-family: Roboto;
}

h1 {
    color: white;
}

p {
    font-family: "Open Sans";
}

.tablink {
    background-color: #555;
    color: white;
    float: left;
    border: none;
    outline: none;
    cursor: pointer;
    padding: 14px 16px;
    font-size: 17px;
    width: 50%;
}

.tablink:hover {
    background-color: #777;
}

.tabcontent {
    color: #111;
    display: none;
    padding: 50px;
    text-align: center;
}

#tabintro { background-color: #ccc; }
#tababout { background-color: #ccc; }

/* You need CSS to make pretty pages. Here's part 2/3 of the flag: t3ct1ve_0r_ju5t */
~~~

Our flag is now "picoCTF{tru3_d3t3ct1ve_0r_ju5t".  We can also view the javascript source, myjs.js:

~~~js
function openTab(tabName,elmnt,color) {
    var i, tabcontent, tablinks;
    tabcontent = document.getElementsByClassName("tabcontent");
    for (i = 0; i < tabcontent.length; i++) {
	tabcontent[i].style.display = "none";
    }
    tablinks = document.getElementsByClassName("tablink");
    for (i = 0; i < tablinks.length; i++) {
	tablinks[i].style.backgroundColor = "";
    }
    document.getElementById(tabName).style.display = "block";
    if(elmnt.style != null) {
	elmnt.style.backgroundColor = color;
    }
}

window.onload = function() {
    openTab('tabintro', this, '#222');
}

/* Javascript sure is neat. Anyways part 3/3 of the flag: _lucky?2e7b23e3} */
~~~

This gives us the final part of the flag.  Our flag is complete: picoCTF{tru3_d3t3ct1ve_0r_ju5t_lucky?2e7b23e3}



</details>

### Answer

<details>

<summary markdown="span">Flag</summary>

~~~
picoCTF{tru3_d3t3ct1ve_0r_ju5t_lucky?2e7b23e3}
~~~

</details>

---

### [Web Exploitation](#contents) | [PicoGym](./picogym.md) | [PicoCTF](./picoctf.md) | [Home](./index.md)

---

## logon

- Author: bobson
- 100 points

### Description

The factory is hiding things from all of its users. Can you login as Joe and find what they've been looking at? https://jupiter.challenges.picoctf.org/problem/44573/ ([link](https://jupiter.challenges.picoctf.org/problem/44573/)) or http://jupiter.challenges.picoctf.org:44573

### Hints

1. Hmm it doesn't seem to check anyone's password, except for Joe's?

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

### [Web Exploitation](#contents) | [PicoGym](./picogym.md) | [PicoCTF](./picoctf.md) | [Home](./index.md)

---

## where are the robots

- Author: zaratec/Danny
- 100 points

### Description

Can you find the robots? https://jupiter.challenges.picoctf.org/problem/56830/ ([link](https://jupiter.challenges.picoctf.org/problem/56830/)) or http://jupiter.challenges.picoctf.org:56830

### Hints

1. What part of the website could tell you where the creator doesn't want you to look?

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

### [Web Exploitation](#contents) | [PicoGym](./picogym.md) | [PicoCTF](./picoctf.md) | [Home](./index.md)

---

## dont-use-client-side

- Author: Alex Fulton/Danny
- 100 points

### Description

Can you break into this super secure portal? https://jupiter.challenges.picoctf.org/problem/17682/ ([link](https://jupiter.challenges.picoctf.org/problem/17682/)) or http://jupiter.challenges.picoctf.org:17682

### Hints

1. Never trust the client

### Solutions

<details>

<summary markdown="span">Solution 1</summary>

We can inspect the html source for this website:

~~~html
<html>
<head>
<title>Secure Login Portal</title>
</head>
<body bgcolor=blue>
<!-- standard MD5 implementation -->
<script type="text/javascript" src="md5.js"></script>

<script type="text/javascript">
  function verify() {
    checkpass = document.getElementById("pass").value;
    split = 4;
    if (checkpass.substring(0, split) == 'pico') {
      if (checkpass.substring(split*6, split*7) == '706c') {
        if (checkpass.substring(split, split*2) == 'CTF{') {
         if (checkpass.substring(split*4, split*5) == 'ts_p') {
          if (checkpass.substring(split*3, split*4) == 'lien') {
            if (checkpass.substring(split*5, split*6) == 'lz_b') {
              if (checkpass.substring(split*2, split*3) == 'no_c') {
                if (checkpass.substring(split*7, split*8) == '5}') {
                  alert("Password Verified")
                  }
                }
              }
      
            }
          }
        }
      }
    }
    else {
      alert("Incorrect password");
    }
    
  }
</script>
<div style="position:relative; padding:5px;top:50px; left:38%; width:350px; height:140px; background-color:yellow">
<div style="text-align:center">
<p>This is the secure login portal</p>
<p>Enter valid credentials to proceed</p>
<form action="index.html" method="post">
<input type="password" id="pass" size="8" />
<br/>
<input type="submit" value="verify" onclick="verify(); return false;" />
</form>
</div>
</div>
</body>
</html>
~~~

We can see the password is authenticated in an inline javascript in the page.  We can reconstruct the password and retrieve the flag picoCTF{no_clients_plz_b706c5}.

</details>

### Answer

<details>

<summary markdown="span">Flag</summary>

~~~
picoCTF{no_clients_plz_b706c5}
~~~

</details>

---

### [Web Exploitation](#contents) | [PicoGym](./picogym.md) | [PicoCTF](./picoctf.md) | [Home](./index.md)

---

## Web Gauntlet

- Author: madStacks
- 200 points

### Description

Can you beat the filters? Log in as admin http://jupiter.challenges.picoctf.org:54319/ http://jupiter.challenges.picoctf.org:54319/filter.php

### Hints

1. You are not allowed to login with valid credentials.
2. Write down the injections you use in case you lose your progress.
3. For some filters it may be hard to see the characters, always (always) look at the raw hex in the response.
4. sqlite.
5. If your cookie keeps getting reset, try using a private browser window.

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

### [Web Exploitation](#contents) | [PicoGym](./picogym.md) | [PicoCTF](./picoctf.md) | [Home](./index.md)

---

## picobrowser

- Author: Archit
- 200 points

### Description

This website can be rendered only by picobrowser, go and catch the flag! https://jupiter.challenges.picoctf.org/problem/28921/ ([link](https://jupiter.challenges.picoctf.org/problem/28921/)) or http://jupiter.challenges.picoctf.org:28921

### Hints

1. You don't need to download a new web browser.

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

### [Web Exploitation](#contents) | [PicoGym](./picogym.md) | [PicoCTF](./picoctf.md) | [Home](./index.md)

---

## Client-side-again

- Author: Danny
- 200 points

### Description

Can you break into this super secure portal? https://jupiter.challenges.picoctf.org/problem/60786/ ([link](https://jupiter.challenges.picoctf.org/problem/60786/)) or http://jupiter.challenges.picoctf.org:60786

### Hints

1. What is obfuscation?

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

### [Web Exploitation](#contents) | [PicoGym](./picogym.md) | [PicoCTF](./picoctf.md) | [Home](./index.md)

---

## Irish-Name-Repo 1

- Author: Chris Hensler
- 300 points

### Description

There is a website running at https://jupiter.challenges.picoctf.org/problem/39720/ ([link](https://jupiter.challenges.picoctf.org/problem/39720/)) or http://jupiter.challenges.picoctf.org:39720. Do you think you can log us in? Try to see if you can login!

### Hints

1. There doesn't seem to be many ways to interact with this. I wonder if the users are kept in a database?
2. Try to think about how the website verifies your login.

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

### [Web Exploitation](#contents) | [PicoGym](./picogym.md) | [PicoCTF](./picoctf.md) | [Home](./index.md)

---

## Irish-Name-Repo 2

- Author: Xingyang Pan
- 350 points

### Description

There is a website running at https://jupiter.challenges.picoctf.org/problem/52849/ ([link](https://jupiter.challenges.picoctf.org/problem/52849/)). Someone has bypassed the login before, and now it's being strengthened. Try to see if you can still login! or http://jupiter.challenges.picoctf.org:52849

### Hints

1. The password is being filtered.

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

### [Web Exploitation](#contents) | [PicoGym](./picogym.md) | [PicoCTF](./picoctf.md) | [Home](./index.md)

---

## Irish-Name-Repo 3

- Author: Xingyang Pan
- 400 points

### Description

There is a secure website running at https://jupiter.challenges.picoctf.org/problem/29132/ ([link](https://jupiter.challenges.picoctf.org/problem/29132/)) or http://jupiter.challenges.picoctf.org:29132. Try to see if you can login as admin!

### Hints

1. Seems like the password is encrypted.

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

### [Web Exploitation](#contents) | [PicoGym](./picogym.md) | [PicoCTF](./picoctf.md) | [Home](./index.md)

---

## JaWT Scratchpad

- Author: John Hammond
- 400 points

### Description

Check the admin scratchpad! https://jupiter.challenges.picoctf.org/problem/61864/ or http://jupiter.challenges.picoctf.org:61864.

### Hints

1. What is that cookie?
2. Have you heard of JWT?

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

### [Web Exploitation](#contents) | [PicoGym](./picogym.md) | [PicoCTF](./picoctf.md) | [Home](./index.md)

---

## Java Script Kiddie

- Author: John Johnson
- 400 points

### Description

The image link appears broken... https://jupiter.challenges.picoctf.org/problem/17205 or http://jupiter.challenges.picoctf.org:17205

### Hints

1. This is only a JavaScript problem.

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

### [Web Exploitation](#contents) | [PicoGym](./picogym.md) | [PicoCTF](./picoctf.md) | [Home](./index.md)

---

## Java Script Kiddie 2

- Author: John Johnson
- 450 points

### Description

The image link appears broken... twice as badly... https://jupiter.challenges.picoctf.org/problem/51400 or http://jupiter.challenges.picoctf.org:51400

### Hints

1. This is only a JavaScript problem.

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

### [Web Exploitation](#contents) | [PicoGym](./picogym.md) | [PicoCTF](./picoctf.md) | [Home](./index.md)

---

## [djm89uk.github.io](https://djm89uk.github.io)
