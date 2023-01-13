# [Root-Me](./rootme.md) Root-Me Realist [1/44]

You will end up in environments full of diverse and varied themes. These challenges will help you understand the operation, including authentication methods, and target vulnerabilities to exploit target in realistic scenarios.

The challenges are complete web sites with multiple security vulnerabilities, with a completely fictional content. You play the role of a hacker contacted by organizations or individuals in order to provide justice through a hack. Once received your goals, it’s up to you to browse the site by trying to discover and exploit vulnerabilities. This series of challenges can be directly applied to the real world.

## Contents

1. [It happens, sometimes ](#it-happens-sometimes) 🗸
2. [P0wn3d ](#p0wn3d)
3. [The h@ckers l4b ](#the-h@ckers-l4b)
4. [Neonazi inside ](#neonazi-inside)
5. [Well-known ](#well-known)
6. [Bash/Awk - netstat parsing ](#bash/awk-netstat-parsing)
7. [Breaking Root-Me like it’s 2020 ](#breaking-root-me-like-its-2020)
8. [PyRat Auction ](#pyrat-auction)
9. [Root them ](#root-them)
10. [IPBX - call me maybe ](#ipbx-call-me-maybe)
11. [Marabout ](#marabout)
12. [Root-We ](#root-we)
13. [Starbug Bounty ](#starbug-bounty)
14. [Ultra Upload ](#ultra-upload)
15. [A bittersweet shellfony ](#a-bittersweet-shellfony)
16. [Bash - System Disaster ](#bash-system-disaster)
17. [Imagick ](#imagick)
18. [MALab ](#malab)
19. [SSHocker ](#sshocker)
20. [Web TV ](#web-tv)
21. [SamBox v2 ](#sambox-v2)
22. [SamCMS ](#samcms)
23. [BBQ Factory - First Flirt ](#bbq-factory-first-flirt)
24. [Django unchained ](#django-unchained)
25. [Getting root Over it! ](#getting-root-over-it)
26. [Texode ](#texode)
27. [BBQ Factory - Back To The Grill ](#bbq-factory-back-to-the-grill)
28. [In Your Kubernetass ](#in-your-kubernetass)
29. [DjangocatZ ](#djangocatz)
30. [SamBox v1 ](#sambox-v1)
31. [SAP Pentest 007 ](#sap-pentest-007)
32. [Crypto Secure ](#crypto-secure)
33. [Bozobe Hospital ](#bozobe-hospital)
34. [Red Pills ](#red-pills)
35. [SamBox v3 ](#sambox-v3)
36. [ARM FTP Box ](#arm-ftp-box)
37. [SAP Pentest 000 ](#sap-pentest-000)
38. [Texode Back ](#texode-back)
39. [Bluebox 2 - Pentest ](#bluebox-2-pentest)
40. [Nodeful ](#nodeful)
41. [Bluebox - Pentest ](#bluebox-pentest)
42. [Highway to shell ](#highway-to-shell)
43. [SamBox v4 ](#sambox-v4)


---

### [Realist](#contents) | [Root-Me](./rootme.md) | [Home](./index.md)

---

## It happens sometimes

- Author: na5sim
- Date: 3 March 2017
- Points: 10
- Level: 1

### Statement

Find a vulnerabilty in this service and exploit it.

The flag is on the index.php file.

### Links

1. [challenge site](http://challenge01.root-me.org/realiste/ch3/).

### Resources

1. [OWASP testing guide v2](https://repository.root-me.org/Exploitation%20-%20Web/EN%20-%20OWASP%20testing%20guide%20v2.pdf).
2. [OWASP testing guide v3](https://repository.root-me.org/Exploitation%20-%20Web/EN%20-%20OWASP%20testing%20guide%20v3.pdf).
3. [OWASP testing guide v4](https://repository.root-me.org/Exploitation%20-%20Web/EN%20-%20OWASP%20testing%20guide%20v4.pdf).

### Solutions

<details>

<summary markdown="span">Solution 1</summary>

Visiting the site, we can see the following html:

~~~html
<!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Strict//EN" 
"http://www.w3.org/TR/xhtml1/DTD/xhtml1-strict.dtd">
<html xmlns="http://www.w3.org/1999/xhtml" xml:lang="fr" lang="fr">
  <head>
    <title>WebGallery 1.0
    </title>
    <link href="format.css" rel="stylesheet" type="text/css" />
    <meta http-equiv="Content-Type" content="text/html; charset=iso-8859-1">
    <style type="text/css">
      <!--
      .Style9 {
        font-size: medium;
        font-family: "Comic Sans MS";
      }
      .Style10 {
        font-family: "Comic Sans MS"}
      .Style11 {
        font-size: medium}
      .Style12 {
        font-size: small}
      .Style13 {
        color: #FFFFFF
      }
      -->
    </style>
  </head>
  <body>
    <div id="site">
      <div id="header">
      </div>
      <div id="contenu">
        <div id="left">
          <div id="bloc">
            <h3>Welcome on WebGallery 1.0
            </h3>
            <p class="Style12">On 11/11/1960 we decided to start coding a revolutionary program, a program that would meet everyone's needs. WebGallery 1.0 is a program that classifies your photos by date. So cool, isn't it? It is on sale for 50 easy payments of $500. The purchase page will soon be open.
            </p>
            <p class="Style12">Last November, we suffered a hack, so we had to close all our systems, the hacker had deleted all our files. So we always work on our site, there is nothing special about it.
            </p>
          </div>
        </div>
        <div id="right">
          <div id="menu">
            <ul>
              <li>
                <a href="#">Home
                </a>
              </li>
            </ul>
          </div>
        </div>
      </div>
      <div id="footer">
        <p>&copy;2010 root-me.org, All rights reserved
        </p>
      </div>
    </div>
  </body>
</html>
~~~

Nothing very fancy, however after a short while we can find /admin as a password protected subsite.  This does not let us access the page without first logging on.  We can use BURP to intercept and change from GET to PUT which gives us the admin page.

~~~html
<!DOCTYPE HTML PUBLIC "-//W3C//DTD HTML 4.0 Transitional//EN">
<html>
<head>
    <title>Admin section</title>
</head>
<body>
    <h1>Mot de passe / password : 0010110111101001</h1>
</body>
</html>
~~~

This has the challenge solution.

</details>

### Answer

<details>

<summary markdown="span">Answer</summary>

~~~
0010110111101001
~~~

</details>

---

### [Realist](#contents) | [Root-Me](./rootme.md) | [Home](./index.md)

---

Last updated Jan 2022.

## [djm89uk.github.io](https://djm89uk.github.io)
