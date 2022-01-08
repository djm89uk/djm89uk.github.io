# [Root-Me](./rootme.md) Root-Me Web Client [6/29]

Client-side technologies implemented in the web browser.

## Contents

1. [HTML - disabled buttons](#html-disabled-buttons) 🗸
2. [Javascript - Authentication](#javascript-authentication) 🗸
3. [Javascript - Source](#javascript-source) 🗸
4. [Javascript - Authentication 2](#javascript-authentication-2) 🗸
5. [Javascript - Obfuscation 1](#javascript-obfuscation-1) 🗸
6. [Javascript - Obfuscation 2](#javascript-obfuscation-2) 🗸
7. [Javascript - Native code](#javascript-native-code)
8. [Javascript - Webpack](#javascript-webpack)
9. [Javascript - Obfuscation 3](#javascript-obfuscation-3)
10. [Web Socket - 0 protection](#web-socket-0-protection)
11. [XSS - Stored 1](#xss-stored-1)
12. [CSP Bypass - Inline code](#csp-bypass-inline-code)
13. [CSRF - 0 protection](#csrf-0-protection)
14. [XSS DOM Based - Introduction](#xss-dom-based-introduction)
15. [Flash - Authentication](#flash-authentication)
16. [XSS DOM Based - AngularJS](#xss-dom-based-angularjs)
17. [XSS DOM Based - Eval](#xss-dom-based-eval)
18. [CSP Bypass - Dangling markup](#csp-bypass-dangling-markup)
19. [CSP Bypass - JSONP](#csp-bypass-jsonp)
20. [CSRF - token bypass](#csrf-token-bypass)
21. [XSS - Reflected](#xss-reflected)
22. [CSP Bypass - Dangling markup 2](#csp-bypass-dangling-markup-2)
23. [Javascript - Obfuscation 4](#javascript-obfuscation-4)
24. [XSS - Stored 2](#xss-stored-2)
25. [XSS DOM Based - Filters Bypass](#xss-dom-based-filters-bypass)
26. [HTTP Response Splitting](#http-response-splitting)
27. [Javascript - Obfuscation 5](#javascript-obfuscation-5)
28. [XSS - Stored - filter bypass](#xss-stored-filter-bypass)
29. [XSS - DOM Based](#xss-dom-based)

---

### [Web - Client](#contents) | [Root-Me](./rootme.md) | [Home](./index.md)

---

## HTML disabled buttons

- Author: Final
- Date: 16 July 2017
- Points: 5
- Level: 1

### Statement

This form is disabled and can not be used. It’s up to you to find a way to use it.

### Links

1. [challenge site](http://challenge01.root-me.org/web-client/ch25/)

### Solutions

<details>

<summary markdown="span">Solution 1</summary>

Visiting the website we can see an under-construction banner.  The webpage has a form with disabled inputs:

~~~html
<html>
    <head>
        <title>Under construction</title>
        <link rel='stylesheet' property='stylesheet' type='text/css' href='style.css' media='all' />
    </head>
   <body><link rel='stylesheet' property='stylesheet' id='s' type='text/css' href='/template/s.css' media='all' /><iframe id='iframe' src='https://www.root-me.org/?page=externe_header'></iframe>
        <h1>Website temporarily closed.</h1>
        <hr>

        <form action="" method="post" name="authform">
            <div>
                <input disabled type="text" name="auth-login" value="" />
                <input disabled type="submit" value="Member access" name="authbutton" />
            </div>
        </form>
            </body>
</html>
~~~

Using the Firefox WebDeveloper toolset, we can remove the disabled attribute and submit a form to retrieve response:

~~~html
<html>
    <head>
        <title>Under construction</title>
        <link rel='stylesheet' property='stylesheet' type='text/css' href='style.css' media='all' />
    </head>
   <body><link rel='stylesheet' property='stylesheet' id='s' type='text/css' href='/template/s.css' media='all' /><iframe id='iframe' src='https://www.root-me.org/?page=externe_header'></iframe>
        <h1>Website temporarily closed.</h1>
        <hr>
<div class='success'>Member access granted! The validation password is HTMLCantStopYou</div>    </body>
</html>
~~~

This gives the password

</details>

### Answer

<details>

<summary markdown="span">Answer</summary>

~~~
HTMLCantStopYou
~~~

</details>

---

### [Web - Client](#contents) | [Root-Me](./rootme.md) | [Home](./index.md)

---

## Javascript Authentication

- Author: g0uZ
- Date: 08 October 2006
- Points: 5
- Level: 1

### Statement

None.

### Links

1. [challenge site](http://challenge01.root-me.org/web-client/ch9/)

### Solutions

<details>

<summary markdown="span">Solution 1</summary>

Visiting the website we can see a login form:

~~~html
<html>
<head>
<script type="text/javascript" src="login.js"></script>
</head>
<body><link rel='stylesheet' property='stylesheet' id='s' type='text/css' href='/template/s.css' media='all' /><iframe id='iframe' src='https://www.root-me.org/?page=externe_header'></iframe>
    <fieldset style="margin-top: 10px; padding: 10px;" width="60%">
	<legend><b>Login</b></legend><br/>
	<form name="login" method="POST" action="">
	    Username : <input name="pseudo" /><br/>
	    Password : <input type="password" name="password" /></br></br>
	    <input onclick="Login()" type="button" value="login" name="button" />
	</form>
    </fieldset>
</body>
</html>
~~~

The form operates with javascript. Using Firefox WebDeveloper toolset, we can see the page uses /login.js as its javascript source:

~~~js
/* <![CDATA[ */

function Login(){
	var pseudo=document.login.pseudo.value;
	var username=pseudo.toLowerCase();
	var password=document.login.password.value;
	password=password.toLowerCase();
	if (pseudo=="4dm1n" && password=="sh.org") {
	    alert("Password accepté, vous pouvez valider le challenge avec ce mot de passe.\nYou an validate the challenge using this password.");
	} else { 
	    alert("Mauvais mot de passe / wrong password"); 
	}
}
/* ]]> */ 
~~~

We can login with the username and password (4dm1n, sh.org) and get the login banner from the javascript. The challenge solution is the password.

</details>

### Answer

<details>

<summary markdown="span">Answer</summary>

~~~
sh.org
~~~

</details>

---

### [Web - Client](#contents) | [Root-Me](./rootme.md) | [Home](./index.md)

---

## Javascript Source

- Author: g0uZ
- Date: 07 October 2006
- Points: 5
- Level: 1

### Statement

None.

### Links

1. [challenge site](http://challenge01.root-me.org/web-client/ch1/).

### Resources

1. [RFC 1945](https://repository.root-me.org/RFC/EN%20-%20rfc1945.txt).

### Solutions

<details>

<summary markdown="span">Solution 1</summary>

Visiting the website, we find a html page with javascript:

~~~html
<html>
    <head>
	<script type="text/javascript">
	/* <![CDATA[ */
	    function login(){
		pass=prompt("Entrez le mot de passe / Enter password");
		if ( pass == "123456azerty" ) {
		    alert("Mot de passe accepté, vous pouvez valider le challenge avec ce mot de passe.\nYou can validate the challenge using this password.");  }
		else {
		    alert("Mauvais mot de passe / wrong password !");
		}
	    }
	/* ]]> */
	</script>
    </head>
   <body onload="login();"><link rel='stylesheet' property='stylesheet' id='s' type='text/css' href='/template/s.css' media='all' /><iframe id='iframe' src='https://www.root-me.org/?page=externe_header'></iframe>

    </body>
</html>
~~~

The login password is 123456azerty which we can use to get the message:

~~~
Mot de passe accepté, vous pouvez valider le challenge avec ce mot de passe.
You can validate the challenge using this password.
~~~

Thus the challenge solution is the password.

</details>

### Answer

<details>

<summary markdown="span">Answer</summary>

~~~
123456azerty
~~~

</details>

---

### [Web - Client](#contents) | [Root-Me](./rootme.md) | [Home](./index.md)

---

## Javascript Authentication 2

- Author: na5sim
- Date: 3 February 2011
- Points: 10
- Level: 1

### Statement

None.

### Links

1. [challenge site](http://challenge01.root-me.org/web-client/ch11/).

### Solutions

<details>

<summary markdown="span">Solution 1</summary>

Visiting the website, we find a html page with external javascript:

~~~html
<html>
    <head>
	<title>JS Authentication</title>
	<script language="JavaScript" src="login.js"></script>
    </head>
   <body><link rel='stylesheet' property='stylesheet' id='s' type='text/css' href='/template/s.css' media='all' /><iframe id='iframe' src='https://www.root-me.org/?page=externe_header'></iframe>
	<div id=EchoTopic>
	<p>Authentication</p>
	<p><input type="button" value="login" onclick="connexion();"></p>
	<br/><br/>
	<a href="javascript:window.close();">Close Window</a>
	</div>
    </body>
</html>
~~~

The login.js code:

~~~js
function connexion(){
    var username = prompt("Username :", "");
    var password = prompt("Password :", "");
    var TheLists = ["GOD:HIDDEN"];
    for (i = 0; i < TheLists.length; i++)
    {
        if (TheLists[i].indexOf(username) == 0)
        {
            var TheSplit = TheLists[i].split(":");
            var TheUsername = TheSplit[0];
            var ThePassword = TheSplit[1];
            if (username == TheUsername && password == ThePassword)
            {
                alert("Vous pouvez utiliser ce mot de passe pour valider ce challenge (en majuscules) / You can use this password to validate this challenge (uppercase)");
            }
        }
        else
        {
            alert("Nope, you're a naughty hacker.")
        }
    }
}
~~~

We can write a short javascript code to solve this:

~~~js
var TheLists = ["GOD:HIDDEN"];
for (i = 0; i < TheLists.length; i++)
{
  var TheSplit = TheLists[i].split(":");
  var TheUsername = TheSplit[0];
  var ThePassword = TheSplit[1];
}
console.log("TheUsername = "+TheUsername+" ThePassword = " + ThePassword)
~~~

Running in an [online compiler](https://onecompiler.com/javascript/) we find the username is "GOD" and the password is "HIDDEN" which we can input to the website to test.  We get the response:

~~~
Vous pouvez utiliser ce mot de passe pour valider ce challenge (en majuscules) / You can use this password to validate this challenge (uppercase)
~~~

So the challenge solution is HIDDEN

</details>

### Answer

<details>

<summary markdown="span">Answer</summary>

~~~
HIDDEN
~~~

</details>

---

### [Web - Client](#contents) | [Root-Me](./rootme.md) | [Home](./index.md)

---

## Javascript Obfuscation 1

- Author: hel0ck
- Date: 7 October 2006
- Points: 10
- Level: 1

### Statement

None.

### Links

1. [challenge site](http://challenge01.root-me.org/web-client/ch4/ch4.html).

### Resources

1. [Automatic simplification of obfuscated Javascript code](https://repository.root-me.org/Virologie/EN%20-%20Automatic%20simplification%20of%20obfuscated%20JavaScript%20code.pdf).
2. [Spiffy: Automated JavaScript deobfuscation](https://repository.root-me.org/Virologie/EN%20-%20Spiffy:%20Automated%20JavaScript%20deobfuscation.pdf). 
3. [Automatic detection for JavaScript obfuscation attacks](https://repository.root-me.org/Virologie/EN%20-%20Automatic%20detection%20for%20javaScript%20obfuscation%20attacks.pdf).
4. [DEFCON a different approach to JavaScript obfuscation](https://repository.root-me.org/Virologie/EN%20-%20DEFCON%20a%20different%20approach%20to%20JavaScript%20obfuscation.pdf).

### Solutions

<details>

<summary markdown="span">Solution 1</summary>

Visiting the website, we find a html page with embedded javascript:

~~~html
<html>
    <head>
        <title>Obfuscation JS</title>

          <script type="text/javascript">
              /* <![CDATA[ */

              pass = '%63%70%61%73%62%69%65%6e%64%75%72%70%61%73%73%77%6f%72%64';
              h = window.prompt('Entrez le mot de passe / Enter password');
              if(h == unescape(pass)) {
                  alert('Password accepté, vous pouvez valider le challenge avec ce mot de passe.\nYou an validate the challenge using this pass.');
              } else {
                  alert('Mauvais mot de passe / wrong password');
              }

              /* ]]> */
          </script>
    </head>
   <body><link rel='stylesheet' property='stylesheet' id='s' type='text/css' href='/template/s.css' media='all' /><iframe id='iframe' src='https://www.root-me.org/?page=externe_header'></iframe>
    </body>
</html>

~~~

We can see the password is included in the JavaScript:

~~~js
pass = '%63%70%61%73%62%69%65%6e%64%75%72%70%61%73%73%77%6f%72%64';
h = window.prompt('Entrez le mot de passe / Enter password');
if(h == unescape(pass)) {
  alert('Password accepté, vous pouvez valider le challenge avec ce mot de passe.\nYou an validate the challenge using this pass.');
} else {
  alert('Mauvais mot de passe / wrong password');
}
~~~

This appears to be URL encoded, we can decode [online](https://www.urldecoder.io/) to get the password: cpasbiendurpassword. Entering this into the form we get the message:

~~~
Password accepté, vous pouvez valider le challenge avec ce mot de passe.
You an validate the challenge using this pass.
~~~

</details>

### Answer

<details>

<summary markdown="span">Answer</summary>

~~~
cpasbiendurpassword
~~~

</details>

---

### [Web - Client](#contents) | [Root-Me](./rootme.md) | [Home](./index.md)

---

## Javascript Obfuscation 2

- Author: hel0ck
- Date: 3 February 2011
- Points: 10
- Level: 1

### Statement

None.

### Links

1. [challenge site](http://challenge01.root-me.org/web-client/ch12/ch12.html).

### Solutions

<details>

<summary markdown="span">Solution 1</summary>

Visiting the website, we find a html page with embedded javascript:

~~~html
<html>

<head>
	<title>Obfuscation JS</title>
<!-- 
Obfuscation 
.Niveau : Facile 
.By Hel0ck
.The mission : 
	Retrouver le password contenu dans la var pass.
	You need my help ? IRC : irc.root-me.org #root-me
-->
<script type="text/javascript">
	var pass = unescape("unescape%28%22String.fromCharCode%2528104%252C68%252C117%252C102%252C106%252C100%252C107%252C105%252C49%252C53%252C54%2529%22%29");
</script>
</head>

</html>
~~~

We can see the password is included in the JavaScript:

~~~js
var pass = unescape("unescape%28%22String.fromCharCode%2528104%252C68%252C117%252C102%252C106%252C100%252C107%252C105%252C49%252C53%252C54%2529%22%29");
~~~

The [unescape()](https://www.w3schools.com/jsref/jsref_unescape.asp) function is a deprecated function replaced by [decodeURI()](https://www.w3schools.com/jsref/jsref_decodeuri.asp).  The [String.fromChar](https://www.w3schools.com/jsref/jsref_fromcharcode.asp) converts JavaScript Char codes into ASCII and the codes themselves appear to be URL encoded, we can solve this with a simple javascript program:

~~~js
var pass1 = decodeURI("unescape%28%22String.fromCharCode%2528104%252C68%252C117%252C102%252C106%252C100%252C107%252C105%252C49%252C53%252C54%2529%22%29");
var pass2 = decodeURI("String.fromCharCode%28104%2C68%2C117%2C102%2C106%2C100%2C107%2C105%2C49%2C53%2C54%29")
var pass3 = String.fromCharCode(104,68,117,102,106,100,107,105,49,53,54)
console.log("Password decode 1 = "+pass1)
console.log("Password decode 2 = "+pass2)
console.log("Password decode 3 = "+pass3)
~~~

This returns the challenge solution.

</details>

### Answer

<details>

<summary markdown="span">Answer</summary>

~~~
hDufjdki156
~~~

</details>

---

### [Web - Client](#contents) | [Root-Me](./rootme.md) | [Home](./index.md)

---

Last updated Jan 2022.

## [djm89uk.github.io](https://djm89uk.github.io)
