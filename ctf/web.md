# Web

Well I think this is the most important field in CTF challenges\(RE/PWN people gonna hate :smile:\). But it make sense to have lot of web challenges since everything in today's time is on WEB.

Web challenges can sometime really screw up things with you.

## Source

Always look into the source code. When you visit the challenge website and see nothing unsual then just dive into the source and try to find something. Like if it's a form then see if there's anything with `hidden` keyword in the tag or any script that might give you somthing or most probably a comment left by creator.

Just don't forget to look at the source

## Tools

There are tones of tool you can use like [nikto](https://github.com/sullo/nikto) or [Burp](https://portswigger.net/burp) or [sqlmap](https://github.com/sqlmapproject/sqlmap) and many more. But Web challenges are not about tools atleast not until you know what the hell is supposed to be done.

As the great @Corb3nik of [OTA](https://opentoallctf.github.io/) said `If there is one thing that I've learned from doing CTFs, it's that vulnerability scanners and automated tools such as (SQLMap, Nmap, ...) are rarely the solution.`

Like if a form is provided then randomly running sqlmap won't give you anything\(it may, sometimes but not the ideal way to do stuff\). But still you need tools, for the time when you know what is to be done like sometime you need to enumerate at that point you can use burp repeater or write few lines of python code.

Some good and most used tools are:

1\) Burp

* [Cheatsheet](https://repo.zenk-security.com/Techniques%20d.attaques%20%20.%20%20Failles/Pentesting%20With%20Burp%20Suite.pdf)
* [Guide](https://support.portswigger.net/customer/portal/articles/1969845-using-burp-to-test-for-the-owasp-top-ten)

2\) nmap

* [Cheatsheet](https://blogs.sans.org/pen-testing/files/2013/10/NmapCheatSheetv1.1.pdf)
* [Cheatsheet](https://www.stationx.net/nmap-cheat-sheet/)

3\) Developer tools

They can be really useful. I have solved lot of challenges just using the firefox dev tool.

4\) Python

Or any other scripting language you are comfortable with. I mean sometime for enumeration you might need simple script like in [evlzctf/enumerate](https://ctftime.org/task/7567) all you need was to send the request to a given link with some weird char so it's just best to write some line of code\(unless you are fan of burp :smirk:\)

5\) [dirb](https://tools.kali.org/web-applications/dirb)

You can also use [dirsearch](https://github.com/maurosoria/dirsearch) or any other similar tool. They can be helpful sometime.

6\) wget/curl/httpie

I use [httpie](https://github.com/jakubroztocil/httpie) mostly but most people use curl maybe because it's default or maybe they are not aware of httpie but it totally depends on you, use the one that comforts you.

[httpie-cheatsheet](https://devhints.io/httpie) [curl-cheatsheet](https://devhints.io/curl)

## Robots

If the name or the description of the challenge have the word `robots` or `robot` or something like `Even google can't find up` or `prevents google scraping it`, well just run for the `robots.txt` file.

What is robots.txt? - [https://moz.com/learn/seo/robotstxt](https://moz.com/learn/seo/robotstxt)

This file might have some link, so you can visit those links and get the flag or maybe the next part of the challenge.

## Cookies

Well if something hints you about the cookie then obviously you should look into cookie. Most of the time you have to change the values or add some values. Like if the challenge says that only admin can see something then see if there is any value something like `admin=False` or `admin=1` if yes then make them `admin=True` or `admin=0` if no then try adding the latter values in headers.

Cookies can also have something like md5 hash so you might have to crack it to see what exactly is there, is it some bogus stuff or string that make sense.

If it's base64 then also try to make sense out of it.

## PHP code

Sometime it happens that you are given a PHP code and you have to give some specific input in parameter to get the flag so you must look out for [loose comparision](http://php.net/manual/en/types.comparisons.php), also see what all kind of `param` it is accepting and is it possible to exploit them. Look out of something like `strcmp` and you can try to exploit it like [this](https://www.doyler.net/security-not-included/bypassing-php-strcmp-abctf2016)

Read [PHP magic tricks](https://www.owasp.org/images/6/6b/PHPMagicTricks-TypeJuggling.pdf) for more

## SQLi

I am not good in SQLi but most of the time \[OWASP\]\([https://www.owasp.org/index.php/Testing\_for\_SQL\_Injection\_\(OTG-INPVAL-005](https://www.owasp.org/index.php/Testing_for_SQL_Injection_%28OTG-INPVAL-005)\)\) have really have helped me in figuring out.

## LFI/RFI

LFI is [Local file inclusion](https://www.owasp.org/index.php/Testing_for_Local_File_Inclusion) which basically allow us to include a file.

Most common are

* `?page=../../../../etc/passwd` or `?page=../../../../flag`
  * Name of the file could be anything
* `?page=....//....//....//....//etc/passwd`
  * This might sometimes work if the application removes ../ from the url.

RFI is [Remote file inclusion](https://www.owasp.org/index.php/Testing_for_Remote_File_Inclusion), allows you to include file from other server.

```text
?page=http://remote-file.js
```

The url could be anything maybe the link to the same server or maybe you'll have to upload your payload somewhere else and then try to include the payload file. You'll have to figure that out yourself :smile:

## Command Injection

Attack that let you execute command like `ls` or `cat` and display the content of directories and files.

Read [Owasp command injection](https://www.owasp.org/index.php/Command_Injection)

Sometime you can `?exec=;ls;` and this will display a list of file.

**Why** `;ls;` **and not** `ls`**?** Well this actually depends on the challenge whether it allow normal `ls` or not but for information `;ls;` command will stop any command in already execution with the first `;` and then run our command `ls` and then stop that with last `;`\(it's bash code\)

There's lot of type of command injection like `exec` or `system` but you'll have to figure out what it is exactly.

[https://grosquildu.github.io/pentests/web/](https://grosquildu.github.io/pentests/web/) [https://grosquildu.github.io/pentests/mobile/](https://grosquildu.github.io/pentests/mobile/) [https://grosquildu.github.io/pentests/exp/](https://grosquildu.github.io/pentests/exp/)

